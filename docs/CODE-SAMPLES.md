# Code samples

[← Back to the overview](../README.md)

Short excerpts from the costing engine, to show how it is written. They are not runnable on their own; the full source code is not public.

## Exact money: never a float

```python
def D(value) -> Decimal:
    """Convert anything numeric to Decimal safely (floats via str)."""
    if value is None:
        return ZERO
    if isinstance(value, Decimal):
        return value
    return Decimal(str(value))


def round_money(value: Decimal, places: int = 4) -> Decimal:
    q = Decimal(1).scaleb(-places)
    return value.quantize(q, rounding=ROUND_HALF_UP)
```

## Inputs are frozen and explicit

The engine receives everything it needs, so the same inputs always give the same answer.

```python
@dataclass(frozen=True)
class ComponentInput:
    """One raw-material line of a recipe, with the price that applies."""
    rm_id: int
    code: str
    name: str
    quantity: Decimal                    # % of the recipe
    price: Optional[Decimal]             # per kg; None = no applicable price
    currency: str = "INR"
    price_date: Optional[str] = None     # effective date of the price used (traceability)
    rm_active: bool = True
```

## A recipe is checked before it is costed

```python
seen: set[int] = set()
for c in comps:
    if c.rm_id in seen:
        messages.append(Message("error", "DUPLICATE_RM", f"{c.name}: listed more than once."))
    seen.add(c.rm_id)
    if D(c.quantity) <= ZERO:
        messages.append(Message("error", "NON_POSITIVE_QTY", f"{c.name}: quantity must be greater than 0."))

total_qty = sum((D(c.quantity) for c in comps), ZERO)
if abs(total_qty - HUNDRED) > inp.percent_tolerance:
    messages.append(Message("error", "TOTAL_NOT_100", f"Recipe total = {_fmt(total_qty)}%, expected 100%."))
```

## The cost build-up

Cost heads are applied in two stages: first the ones that make up the cost of goods sold, then the margin.

```python
running = rm_cost
cost_items, margin_items = [], []
for stage, bucket in ((STAGE_COST, cost_items), (STAGE_MARGIN, margin_items)):
    for item in (i for i in inp.cost_items if i.stage == stage):
        amount = _apply(item, rm_cost, running, messages)
        running += amount
        bucket.append(CostItemResult(item.code, item.name, item.basis, item.stage,
                                     D(item.value), amount, item.source))
    if stage == STAGE_COST:
        total_cost = running          # cost of goods sold
target_price = running                # after margin
```

## What a test looks like (simplified)

```python
def test_recipe_not_totalling_100_is_refused():
    result = calculate(CostingInput(components=[
        line("RM Demo 2", qty="70", price="17.80"),
        line("RM Demo 5", qty="29.5", price="98.00"),
    ]))
    assert not result.is_valid()
    assert any(m.code == "TOTAL_NOT_100" for m in result.messages)
```

[← Back to the overview](../README.md)
