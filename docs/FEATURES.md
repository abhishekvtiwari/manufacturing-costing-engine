# Feature walkthrough

[← Back to the overview](../README.md)

Screens from the real application, running on made-up demo data.

## 1. Search & overview

<img src="../images/home.jpg" alt="Search and overview" width="100%">

The home screen answers the most common question, **"what does this product cost today?"** Type a product, customer or material and get the cost and its breakdown straight away. Below that:

- counts of materials, products and active recipes, and how many codes still need fixing
- **cost movement**: which products' costs moved most since a chosen date, and by how much
- the latest raw-material price changes and who made them
- recent activity across the whole system

## 2. One product's cost

<img src="../images/grade.jpg" alt="Product cost breakdown" width="100%">

For any product: cost of goods sold, raw-material cost, target and actual selling price, and the profit or shortfall. Then which materials drive the cost (quantity, price, contribution per kg, share of cost) and the full build-up on the right. You can see it for **domestic or export**, for **a chosen freight city**, and **as on any past date**.

Actions from here: download the breakdown, record a price given to a customer, edit the recipe, substitute a material, copy into a new product.

## 3. Impact analysis

<img src="../images/impact.jpg" alt="Impact analysis" width="100%">

Pick a material and type a new price, or a % change. Every product that uses it is listed with its old and new cost per kg and the difference, **before anything is saved**. Applying the price then asks for a reason and an effective date. The right side shows the real impact of recent price changes.

## 4. Costing sheet

<img src="../images/sheet.jpg" alt="Costing sheet" width="100%">

The layout everyone already knew from Excel (materials down the side, products across, the cost build-up at the bottom), but every number comes live from current prices, recipes and rates. Switch between domestic and export, or filter by product category.

## 5. Product hierarchy

<img src="../images/hierarchy.jpg" alt="Product hierarchy" width="100%">

Item type → category → group → product → grade. Processing cost and default margin set on a level apply to every product below it, and any product can override them. Moving a product to a different level needs a reason and an administrator's approval.

## 6. Raw materials

<img src="../images/raw-materials.jpg" alt="Raw materials" width="100%">

Every material with its codes, category, supplier, make, tax code and status. Each has a full price history and a landed-cost breakdown (basic + freight + duty + other). Codes still waiting for an ERP code are flagged.

## 7. Price register

<img src="../images/prices.jpg" alt="Price register" width="100%">

Prices given to customers, each saved with a **snapshot of the cost on that day**, so you can later see what margin a quote really had.

## 8. Activity log

<img src="../images/activity.jpg" alt="Activity log" width="100%">

The audit trail: when, who, what, which record, old value, new value and the reason. Filter by action or user, or search by record or reason. Nothing is ever overwritten, so this answers "who changed this, and why?"

## Also included

- **Bulk upload** with Excel templates for prices, materials, suppliers, recipes, freight and margins. The whole file is checked first, every problem listed in plain English with a suggested fix where possible, and saved all-or-nothing.
- **Six roles**: admin, costing manager, purchase, management, sales and viewer, each seeing only the actions they're allowed.
- **Approvals** for sensitive changes such as renaming or merging materials.
- **Excel export** of any cost breakdown.
- **First-run guide** that walks each role through their first tasks.

[← Back to the overview](../README.md)
