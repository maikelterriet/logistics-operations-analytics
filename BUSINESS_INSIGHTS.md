# Logistics Operations Dashboard — Business Insights

**Status:** Working analysis, based on Power BI dashboard screenshots.  
**Filters:** Last 30 Days; all warehouses; all operational gate types.  
**Scope:** Observational insights, not causal conclusions. Warehouse and gate labels are pseudonyms.

## Insight 1 — Queue volume rose while average waiting time fell

**Finding:** The dashboard reports **52,566 queue records**, **29.8% more** than the comparison period, while average queue time is **8.86 minutes**, **3.3% lower** than the comparison period.

**Business relevance:** Higher observed queue activity coincided with slightly shorter average waits. This is worth monitoring as a potential operational improvement, but does not establish why it occurred.

**Recommendation:** Track volume and queue-time trends together, broken down by warehouse, gate type, and day. Check whether the improvement is broad-based or concentrated in a few locations.

**Caveats:** Confirm the prior-period DAX calculation and whether the record count represents unique arrivals. Period comparisons are descriptive; changes in site mix or operating conditions could explain the pattern.

**Evidence:** Executive Overview and Warehouse Performance screenshots, Last 30 Days / All / All.

## Insight 2 — Warehouse 003 is a bottleneck candidate

**Finding:** Warehouse 003 shows **920 queue records**, **45.95 minutes average queue time**, and **143.58 minutes average working time**. Its queue time is roughly **5.2×** the overall **8.86-minute** average.

**Business relevance:** This warehouse has unusually high observed delays, making it a sensible priority for investigation.

**Recommendation:** Examine queue-time distributions by day, gate type, and arrival window; compare staffing, appointment scheduling, and loading/unloading workflow where those data are available.

**Caveats:** The data does not establish the root cause. Check whether Warehouse 003 handles different loads or workflows before comparing it directly with other sites.

**Additional gate-level validation (Warehouse 003 selected, Gate All):** Operational Gate Analysis shows only **Gate C**, with **920 records**, **45.95 min average queue time**, **143.58 min average working time**, and **355.37 min maximum queue time**. The dashboard reports a **33.6% decrease in average queue time**, a **36.9% decrease in records**, a **15.0% decrease in working time**, and a **9.0% decrease in maximum queue time** versus the preceding equal-length period. Despite improvement, the warehouse remains substantially above the network average. Gate C is the only displayed gate type for this warehouse; this does not prove gate design or staffing caused the delays.

**Evidence:** Warehouse Performance matrix (Last 30 Days / All / All) and Operational Gate Analysis (Last 30 Days / Warehouse 003 / All).

## Insight 3 — Higher throughput does not automatically correspond to longer queues

**Finding:** Warehouse 006 handled **3,898 records** with **15.22 minutes average queue time**, compared with Warehouse 003's **920 records** and **45.95 minutes**.

**Business relevance:** Differences in waiting time cannot be explained by record volume alone in this comparison.

**Recommendation:** Compare warehouse performance using queue time alongside throughput, gate type, daily demand and operational context; identify practices worth investigating at better-performing sites.

**Caveats:** Two-warehouse comparison is not a statistical relationship across the full network. No causal efficiency claim is warranted.

**Additional validation (Warehouse 006 selected, Gate All):** Operational Gate Analysis shows **3,898 queue records** (rounded to 4K on the KPI card), **15.22 min average queue time**, **61.21 min average working time**, and **223.78 min maximum queue time**. Relative to its previous equal-length period, queue records increased **21.9%**, average queue time increased **140.5%**, average working time increased **22.4%**, and maximum queue time increased **62.2%**. Thus, Warehouse 006 has shorter waits than Warehouse 003 but has experienced marked recent deterioration in queue-time performance.

**Gate-level finding:** Warehouse 006 has **Gate A (15.25 min average queue time)** and **Gate C (3.54 min)**. Gate A's mean is approximately **4.3 times** Gate C's; however, the chart suggests Gate C has low volume and exact per-gate counts were not verified. Compare counts and workload mix before judging relative gate efficiency.

**Evidence:** Warehouse Performance matrix (Last 30 Days / All / All) and Operational Gate Analysis (Last 30 Days / Warehouse 006 / All).

## Insight 4 — Gate-level delays are concentrated in specific warehouse–gate combinations

**Finding:** The gate heatmap shows **Warehouse 034 / Gate A: 50.08 minutes** and **Warehouse 003 / Gate C: 45.95 minutes** average queue time for the selected period.

**Business relevance:** Warehouse-wide averages may conceal gate-specific problems; investigating individual warehouse–gate combinations may be more actionable.

**Recommendation:** Prioritize high-delay gates for deeper review, but rank them using both average waiting time and record count, plus median and upper-percentile wait times if available.

**Caveats:** The heatmap alone does not show gate-level sample sizes; the Warehouse 034 average is especially sensitive to its low warehouse-level count. Do not infer that Gate A or Gate C is universally slower.

**Validated drill-down (Last 30 Days / Warehouse 034 / All):** 14 queue records; average queue time **43.00 min**; maximum queue time **410.17 min**; average working time **136.75 min**. Gate A: **12 records, 50.08 min** average queue; Gate C: **2 records, 0.55 min** average queue. The warehouse-wide average is dominated by Gate A. This is a *low-volume anomaly worth investigating*, not evidence of a persistent systemic bottleneck. Inspect individual delays, scheduling, data quality, and the median / 90th-percentile queue times before prioritizing intervention. The dashboard shows +250.0% queue-record change and +218.0% maximum-queue-time change versus the prior equal-length period; these percentage shifts should be interpreted cautiously with small counts.

**Evidence:** Operational Gate Analysis heatmap, Last 30 Days / All / All.

## Insight 5 — Small samples can exaggerate apparent bottlenecks

**Finding:** Warehouse 034 shows **43.00 minutes average queue time** but only **14 queue records**. This is among the highest warehouse averages, but its estimate is based on very little activity.

**Business relevance:** Ranking warehouses by average delay alone risks directing attention to unstable results.

**Recommendation:** Add queue-record count next to average queue time, introduce a minimum-volume flag for rankings, and review distributions or confidence intervals before escalating low-volume sites.

**Caveats:** Low sample size does not make the delays unimportant; it means the mean may be less representative of typical performance.

**Evidence:** Warehouse Performance matrix, Last 30 Days / All / All.

## Insight 6 — Warehouse 036 is a high-throughput, low-wait benchmark candidate

**Finding (Last 30 Days / Warehouse 036 / All):** Warehouse 036 processed **6,027 queue records**, with **1.39 minutes average queue time** and **46.63 minutes average working time**. The network-wide average queue time is **8.86 minutes**. Its queue time is approximately **84.3% below** that network average, while it accounts for about **11.5%** of the 52,566 network queue records. The dashboard shows **+81.6%** queue records, **−15.3%** average queue time, **−18.8%** average working time and **+67.5%** unique trucks versus the preceding equal-length period. The unique-truck KPI rounds to ~1K; do not present that as an exact count.

**Trend observation:** The daily queue-time chart is mostly near one minute, with a few short spikes. This visual observation is not a quantified stability measure.

**Business relevance:** A relatively large share of recorded queue activity coincides with short waits, making this warehouse a useful candidate for operational benchmarking. This does not prove higher efficiency, since warehouse workloads and truck mixes may differ.

**Recommendation:** Compare Warehouse 036's scheduling, arrival patterns, gate usage, load mix and working processes against higher-wait warehouses. Identify comparable operations before proposing transfer of practices. Monitor the queue-time distribution and upper percentiles, not only the mean.

**Caveats:** Queue records are not necessarily unique trucks or completed jobs. Relative percentage changes rely on the report's existing previous-period measures. Do not claim causality or universal best practice.

**Evidence:** Warehouse Performance screenshot, Last 30 Days / Warehouse 036 / Operational Gate All.

## Final cross-warehouse prioritization — full Warehouse Performance view

**Filters:** Last 30 Days / Warehouse All / Operational Gate All. **Network:** 52,566 queue records, 8.86 min average queue, 65.18 min average working time. Prior-period indicators: +29.8% queue records, −3.3% average queue, +2.0% average working time.

| Warehouse | Queue records | Avg queue (min) | Interpretation / next action |
|---|---:|---:|---|
| 003 | 920 | 45.95 | Investigate sustained high waits at Gate C; compare workload and arrivals |
| 034 | 14 | 43.00 | Review extreme individual delays, but flag the very small sample |
| 011 | 563 | 25.65 | Secondary queue-time investigation; assess workload and daily pattern |
| 013 | 1,444 | 20.06 | Investigate meaningful aggregate delay exposure |
| 006 | 3,898 | 15.22 | Monitor recent +140.5% queue-time deterioration despite comparatively lower current average |
| 036 | 6,027 | 1.39 | Benchmark candidate for high recorded volume and short queues |

**Recommended management triage:** (1) investigate Warehouse 003 / Gate C; (2) monitor Warehouse 006's deteriorating trend; (3) compare practices at Warehouse 036, controlling for workload differences; (4) assess Warehouses 013 and 011; (5) audit Warehouse 034's long-delay outliers before making investment decisions.

**Important methodological note:** This is a qualitative triage, not a validated ranking or estimate of financial impact. Queue-record count is not necessarily throughput in completed jobs. Warehouse 034's 410.17-min maximum is an extreme observed event, not typical waiting time. Assess gate counts, medians/percentiles, operational comparability and data-quality rules before interventions.

**Evidence:** Warehouse Performance overview screenshot, Last 30 Days / All / All; previously recorded filtered Warehouse 003, 006, 034 and 036 views.

## Before publication

- Verify all numbers and comparison-period logic in Power BI.
- Capture clean screenshots with Last 30 Days / All / All selected.
- Do not publish the current PBIX or original dataset; underlying original identifiers remain in the model.
- Review any SQL/DAX examples for identifying or sensitive information before sharing.
- Create a separate sanitized PBIX later if desired.
