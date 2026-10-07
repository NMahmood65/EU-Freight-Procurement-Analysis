# Pan-European Road Freight Procurement & Network Analysis

An end-to-end commercial freight procurement project simulating the day-to-day operations of a lead logistics partner (LLP) managing European full truckload (FTL) haulage. 

This project analyses haulage rates, monitors haulier punctuality, and flags network risks across 90 cross-border corridors in Europe.

---

## Business Problem & Context

Managing transport across European trade lanes involves balancing three core factors:
1. **Cost Control**: Keeping line-haul rates and fuel surcharges (BAF) competitive against open market spot rates.
2. **Reliability**: Ensuring hauliers consistently meet strict on-time delivery (OTD) customer service agreements (target $\ge 94\%$).
3. **Operational Resilience**: Having reliable backup hauliers ready when routes face cross-border friction, driver shortages, or severe weather.

When primary hauliers lack capacity or decline bookings, loads fall into secondary or emergency spot markets. This project evaluates a quarterly network of 3,500 shipments to uncover where fallback routing eroded profit margins and where procurement should intervene.

## Key Findings at a Glance

* **Total Freight Spend**: €4,044,868 across 3,500 completed shipments.
* **Network Punctuality (OTD)**: 92.8% (slightly below the 94.0% SLA target).
* **Net Cost Avoidance**: +€66,811 saved compared to open market spot benchmarks.
* **The Fallback Cost Penalty**:
  * **Primary Contracted Loads**: 94.1% on-time | €153,831 saved vs open market rates.
  * **Contingency / Backup Loads**: 87.1% on-time | -€52,939 cost penalty.
  * **Spot Market Emergency Loads**: 86.5% on-time | -€34,080 cost penalty.
* **High-Risk Exposure**: Two underperforming hauliers (`CAR-04 Alps Cargo Line` and `CAR-07 Iberia-Gaul Intermodal`) accounted for €538,000 in spend with punctuality hovering near 85%, driving down overall network reliability.

## Project Architecture

The workbook is structured into four interconnected worksheets:

* `Executive_Summary`: Senior leadership dashboard featuring high-level KPI cards, haulier allocation and spend tables, strategic procurement notes, and an embedded spend distribution chart.
* `Daily_Shipment_Log`: Operational ledger tracking 3,500 individual journeys across Europe, detailing cargo specs, carrier assignments, invoiced costs, on-time delivery flags, and route disruption notices.
* `Rate_Matrix`: Master pricing database covering 90 distinct origin-destination corridors, benchmarking negotiated primary contract rates against European spot market indices and secondary fallback rates.
* `Carrier_Master`: Haulier directory profiling 8 transport partners with metrics on fleet size, risk scores (rated 1 to 5), ESG carbon ratings, and automated contingency allocation statuses.

### Folder & File Hierarchy

EU-Freight-Procurement-Analysis/
├── Executive_Summary    # KPI scorecards, carrier allocation matrix, strategy notes, spend chart
├── Daily_Shipment_Log   # 3,500 operational shipments, costs, service performance, disruption tags
├── Rate_Matrix          # 90 cross-border routes, contract rates vs spot benchmarks, fallback deltas
└── Carrier_Master       # Profiles for 8 hauliers, fleet capacity, risk ratings (1-5), status logic


## Project Architecture

The workbook is structured into four interconnected worksheets:

## Step-by-Step Implementation

### Step 1: Data Architecture & Network Design
* Designed 90 authentic European freight routes connecting core manufacturing hubs (e.g., Düsseldorf, Venlo, Antwerp, Lille, Lyon, Poznań, Wrocław, Verona, and Milton Keynes).
* Assigned realistic transit distances (200 km to 1,050 km) and equipment types (13.6 m standard curtainsiders, box trailers, and mega trailers).
* Structured standard rates alongside an 8.5% Bunker Adjustment Factor (BAF fuel surcharge) to reflect industry rate indexation.

### Step 2: Rate Benchmarking & Contingency Rules
* Calculated contract rate deltas against European spot market indices:
  $$\text{Variance \%} = \frac{\text{Spot Benchmark} - \text{Contract Rate}}{\text{Spot Benchmark}}$$
* Built dynamic switching premium calculations to quantify the cost impact of falling back to secondary hauliers (typically an 8% to 22% rate increase).
* Implemented operational Route Advisory Status (RAS) triggers simulating Alpine weather, ferry cancellations, and Channel crossing delays.

## Core Excel Formulas Demonstrated

### 1. Dynamic Carrier Names (`XLOOKUP`)
Enriched raw operational logs with real haulier names:
```excel
=XLOOKUP(G2, Carrier_Master!A:A, Carrier_Master!B:B, "Unknown Carrier")
=XLOOKUP("Mannheim" & "|" & "Wrocław", Rate_Matrix!B:B & "|" & Rate_Matrix!D:D, Rate_Matrix!J:J, "Rate Not Found")

=COUNTIF(Daily_Shipment_Log!G:G, "CAR-01")
=SUMIF(Daily_Shipment_Log!G:G, "CAR-01", Daily_Shipment_Log!K:K)
=AVERAGEIF(Daily_Shipment_Log!G:G, "CAR-01", Daily_Shipment_Log!M:M)

=COUNTA(Daily_Shipment_Log!A:A)-1

=IF(E2>=4, "REQUIRES BACKUP - HIGH RISK", IF(E2>=3, "WATCHLIST", "CORE ALLOCATION"))






