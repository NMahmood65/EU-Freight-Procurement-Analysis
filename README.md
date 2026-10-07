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
