# Call-Center-Performance-Dashboard-Power-BI-# Call Center Performance Dashboard (Power BI)

## Overview

An interactive Power BI report that monitors call center service performance across three projects (A, B, C) over 89 days (1 Feb – 30 Apr 2022). It tracks call volume against forecast, answer and abandonment rates, speed of answer (ASA), threshold-based service level, and performance by project, weekday and agent, with drillthrough to an agent-level breakdown.

## Business Problem

Call center managers need to know whether demand matches the forecast, whether calls are being answered fast enough, and where service breaks down. Without a single view, problems such as a short spike in abandoned calls are easy to miss inside monthly averages.

## Objectives

- Monitor volume, answer rate, abandonment, ASA and service-level attainment in one report
- Compare actual calls offered with forecasted calls and measure forecast accuracy
- Compare projects, weekdays and agents to locate where service quality drops
- Provide drillthrough from the summary pages to agent-level detail

## Dataset

- Three monthly CSV files (Feb, Mar, Apr 2022), combined with Power Query's folder import
- 267 rows = 89 days x 3 projects (grain: one row per project per day)
- Fields: Project, Date, Forecasted Calls, Calls Offered, Calls Handled, Calls Handled Within Threshold, Calls Abandon, ASA, Answer Time, Agent Name
- 16 distinct agent names; each project-day row carries a single agent name
- Source / provenance of the data: [ ]
- Service-level threshold (seconds) and ASA unit: [ ]
- Meaning of "Agent Name" (individual agent, shift lead, or queue owner): [ ]

## Tools & Technologies

Power BI Desktop, Power Query (M), DAX. Report features: drillthrough, report-page tooltips, bookmarks, page navigator, decomposition tree, slicers.

## Data Preparation

- Combined the monthly CSVs with Power Query's *Combine Files* pattern (folder source + helper function)
- Set data types (text, date, whole number, decimal)
- Removed the redundant `Month` column and renamed source-file labels
- Added a `Day Name` column from `Date`
- Data checks: [ ] (in the data itself, Calls Handled + Calls Abandon equals Calls Offered on every row, and ASA equals Answer Time / Calls Handled)

## Data Model

Current: a single flat table (`power bi 2`) with no relationships, using Power BI's automatic date/time hierarchy.
Planned: [ ] star schema with `Dim_Date`, `Dim_Project`, `Dim_Agent` and one fact table.

## Key KPIs

| KPI | Definition (as implemented) |
|---|---|
| Total Calls Offered / Handled / Abandoned | Sum of the respective columns |
| Answer Rate | Calls Handled / Calls Offered |
| Abandonment Rate | Calls Abandoned / Calls Offered |
| Threshold Achievement | Calls Handled Within Threshold / Calls Handled |
| Average ASA | [ : update to Answer Time / Calls Handled — see Dashboard notes] |
| Forecast Variance | Calls Offered − Forecasted Calls |
| Forecast Accuracy | 1 − ABS(Variance) / Forecasted Calls |
| Active Agents, Avg Calls per Agent | Distinct agent names; Calls Handled / Active Agents |

## Analysis

- Volume vs forecast by month and weekday
- Answer rate, abandonment and ASA by weekday and project
- Agent comparison: calls handled, ASA, abandonment, threshold achievement
- Forecast variance by weekday; ASA vs answer rate scatter by agent
- Agent drillthrough via decomposition tree (agent > weekday > project)

## Dashboard

| Page | Purpose |
|---|---|
| Overview | Headline KPIs, offered vs forecast trend, handled vs abandoned, answer rate by weekday |
| Calls | ASA, abandonment, threshold achievement, calls handled and workload by agent |
| Agent | Agent scorecard table, threshold achievement by agent, abandoned calls |
| Forecasted | Forecast accuracy and variance, abandonment by weekday, ASA vs answer rate |
| Agents Details | Drillthrough decomposition tree |

Screenshots:
<img width="1332" height="738" alt="Screenshot 2026-10-01 204045" src="https://github.com/user-attachments/assets/ae1670e1-7bf9-49bc-85df-f679ac67b995" />
<img width="1337" height="752" alt="Screenshot 2026-10-01 204021" src="https://github.com/user-attachments/assets/cc94f3ff-1b60-4420-95fe-97f54b6c573f" />
<img width="1331" height="732" alt="Screenshot 2026-10-01 204029" src="https://github.com/user-attachments/assets/f4503882-87b4-4ddf-9190-1753b03ec1bc" />
<img width="1332" height="737" alt="Screenshot 2026-10-01 204037" src="https://github.com/user-attachments/assets/6a4de192-eca0-41a9-9ce7-542a9d18c11c" />
 <img width="1328" height="742" alt="Screenshot 2026-10-01 204053" src="https://github.com/user-attachments/assets/a2cdd7cd-2153-4918-8534-08323654a16b" />

## Key Insights

Figures below were calculated from the dataset (all 3 projects, 1 Feb – 30 Apr 2022).

- **Overall service was healthy:** 1,744,885 calls offered, 98.7% answered, 1.32% abandoned, 92.3% handled within threshold.
- **Abandonment was concentrated in one window:** 2–6 March accounts for about 10% of calls offered but 57% of all abandoned calls (13,119 of 23,043). ASA peaked at about 181 on 5 March (Project B). Outside this window, abandonment is 0.63% and threshold achievement is 96.0%.
- **Demand ran below forecast overall:** offered calls were 28.4% below forecast (1.74M vs 2.44M), giving 71.6% forecast accuracy at total level. Only March came close to forecast.
- **Project B carries the most volume (52%) and the highest abandonment (1.66%)**, mostly because of the March window.
- Weekday and agent rankings change substantially once the 2–6 March window is excluded, so they should be read with that caveat.

## Business Recommendations

- Investigate what happened on 2–6 March (staffing, outage, campaign) — staffing/schedule data: [ ]
- Review the forecasting method; the forecast appears to follow a weekday template and over-predicted Feb and Apr volume
- Track service level and ASA against explicit targets: [  targets]
- Treat agent comparisons carefully until the agent field is clarified
```

## Skills Demonstrated

Power Query (combine files, typing, cleaning) · DAX measures and ratio KPIs · report design with drillthrough, tooltips, bookmarks and navigation · forecast-vs-actual analysis · call center KPIs (ASA, abandonment, service level)

## Conclusion

The report gives a clear operational view of call center performance and shows that service problems were concentrated in a short March window rather than spread across the quarter. Next steps: [ ] (star-schema model, call-weighted ASA, trend page with daily view).
