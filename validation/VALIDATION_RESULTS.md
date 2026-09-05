# Validation Results

The executed `06_dashboard_validation.ipynb` reconciles the core Power BI KPIs against Python calculations from the exported star-schema tables.

## Core result

**ALL CORE KPI CHECKS PASSED**

### Sales

| Metric | Python | Power BI Expected | Status |
|---|---:|---:|:---:|
| Total Net Sales | 332,230,025,498 | 332,230,025,498 | PASS |
| Total Cost | 254,170,428,358 | 254,170,428,358 | PASS |
| Total Profit | 78,059,597,140 | 78,059,597,140 | PASS |
| Profit Margin | 23.50% | 23.50% | PASS |
| Total Quantity Sold | 1,174,515 | 1,174,515 | PASS |

### Returns

| Metric | Python |
|---|---:|
| Return Quantity | 27,643 |
| Gross Sold Quantity | 1,202,158 |
| Return Rate | 2.2994% |

### Inventory

| Metric | Python | Power BI Expected | Status |
|---|---:|---:|:---:|
| Latest Inventory Date | 2022-12-31 | 2022-12-31 | PASS |
| Current Inventory Quantity | 93,317 | 93,317 | PASS |
| Products in Latest Snapshot | 12,975 | 12,975 | PASS |
| Products in Stock | 12,975 | 12,975 | PASS |
| Out of Stock Products | 0 | 0 | PASS |

### Brand1 relationship/filter check

Brand1 independently recalculates to:

- Net Sales: 218,118,068,606
- Cost: 169,258,523,121
- Profit: 48,859,545,485
- Profit Margin: 22.40%
- Net Quantity Sold: 1,004,744
- Return Quantity: 21,777
- Return Rate: ~2.12%
- Current Inventory Quantity: 72,110
- Products in Latest Snapshot / Stock: 10,601
- Out of Stock: 0

This confirms that the shared Product dimension filters both Sales and Inventory as intended.
