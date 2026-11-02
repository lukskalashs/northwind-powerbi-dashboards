# Northwind Sales & Shipping Performance: Power BI Dashboards

Three interactive Power BI dashboards built on the Northwind sample database for the CSID6823 Business Intelligence module (2026). Two dashboards recreate a supplied performance design; the third is an independent design built around exploration and automated insight.

**Live report (owner access only):** [Open in Power BI Service](https://app.powerbi.com/groups/me/reports/850da408-14ab-4854-8a7d-1fc112bac10b?experience=power-bi)
> This link requires access to the author's Power BI workspace. Screenshots are provided below for everyone else.

---

## Data Source

- **Northwind OData feed** (anonymous): `https://services.odata.org/Northwind/Northwind.svc/`
- Tables used: `Order_Details`, `Categories`, `Suppliers`
- Data prepared in Power Query (nested Order, Customer, Employee and Shipper fields expanded and trimmed to the required columns; unused columns removed).

### Data Model
- `Suppliers` (1) → (Many) `Categories`
- `Categories` (1) → (Many) `Order_Details`

### Calculated Columns and Measures
| Name | Type | Purpose |
|---|---|---|
| Gross Revenue | Column | `UnitPrice * Quantity` |
| Discount ($) | Column | `Gross Revenue * Discount` |
| Net Revenue | Column | `Gross Revenue - Discount ($)` |
| Days to Ship | Column | `ShippedDate - OrderDate`, returns `BLANK()` when either date is missing |
| Orders | Measure | `DISTINCTCOUNT(OrderID)` |
| Net Revenue Per Order | Measure | `SUM(Net Revenue) / Orders`, guarded with `BLANK()` |

---

## Dashboard 1: Performance Overview

<img width="1556" height="737" alt="Screenshot 2026-10-01 221245" src="https://github.com/user-attachments/assets/5b4a5045-ede8-49a2-a991-1598a3e3995b" />


A high-level view of revenue, discounts, orders and shipping performance, filterable by product, geography, employee and date range.

**Visuals**
- **Slicers:** CategoryName/ProductName, Country/City and Title/FirstName hierarchy dropdowns, plus a Between date-range slicer on OrderDate
- **Cards + Column charts:** Gross Revenue and Net Revenue by Year
- **Card + Line chart:** Discount ($) by Year
- **Card + Bar chart:** Orders by Year
- **Gauge:** Average Days to Ship (min, average and max driven by the data)
- **Funnel chart:** Average Days to Ship by Shipper Company
- **Map:** Net Revenue by Country and City, with bubble size and a conditional-formatting colour gradient on Net Revenue
- **Dual-axis line chart:** Orders and Gross Revenue by Year and Quarter

---

## Dashboard 2: Category & Product Analysis

<img width="1396" height="732" alt="Screenshot 2026-10-01 221328" src="https://github.com/user-attachments/assets/a86793cd-65f3-4e87-9dac-48c451921c82" />


A category-level breakdown of sales performance and inventory, with drill-down from category to product.

**Visuals**
- **Matrix:** Category and Product Level Performance, with expandable rows, data bars on Gross and Net Revenue, and a totals row
- **Bar charts:** Top 3 and Bottom 3 Categories by Orders (Top N filters)
- **Drill-down clustered column chart:** Units In Stock vs Units On Order by Category, drilling to Product Name

---

## Dashboard 3: Independent Design (Explore & Insight)

<img width="1345" height="748" alt="Screenshot 2026-10-01 221357" src="https://github.com/user-attachments/assets/d7b87c9d-9252-42e5-b7e0-ed2f15558280" />


**Idea:** Dashboards 1 and 2 report what happened. This dashboard lets the viewer investigate: spot unusual periods, choose their own breakdown, and read a plain-language summary.

**Advanced features used**
- **Anomaly Detection** on a Net Revenue line chart by Year/Quarter, flagging unusual periods and suggesting contributing factors
- **Field Parameter** (Selection Dimension) letting one bar chart switch between CategoryName, Supplier CompanyName and Country
- **Smart Narrative** with custom dynamic values highlighting the top Category and Company by Gross Revenue

---

## Design Principles Applied

- **Colour-blind-safe palette:** blue and orange with navy accents; no red/green pairings
- **Limited colours** so the audience doesn't need to keep checking a legend
- **No pie charts;** bars, columns and lines used for easier comparison
- **Readable orientation:** horizontal bars for long labels, clear titles and axis labels
- **Functional interactivity:** slicers, drill-down, field parameters and cross-filtering on every page

---



## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
2. Download the `.pbix` file from the `dashboards` folder.
3. Open it and refresh the data when prompted (the OData feed is public and anonymous, so the first refresh can take a while).

---
