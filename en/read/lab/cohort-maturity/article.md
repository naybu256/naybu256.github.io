# Campaign Cohort Analysis: Compare Equally Mature Results

Canonical: https://theorganiclub.com/en/read/lab/cohort-maturity/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: hypothesis

Day-seven conversion should cover people given seven full days to convert.

![A small tomato seedling pushes two green leaves above dry brown soil.](https://theorganiclub.com/images/editorial/cohort-maturity.jpg)

Ksheera Piraati. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: 4f0a3b5f6801bc6c97e59c31a53e6d0adbc51709.

## The takeaway

Day-seven conversion should cover people given seven full days to convert. Mixing mature and recent cohorts distorts comparisons.

## The argument

Define journey start and conversion. Compare cohorts at equal ages while showing missing data. Monthly purchases divided by monthly visits is not automatically a cohort conversion rate: buyers may have arrived long before the displayed window.

For daily cohorts, keep entry date and measurement cutoff. A table can show recent cohorts without calculating their final rate. This preserves visibility into new activity while protecting comparisons. Immature data is not bad data; it simply concerns a question whose full observation time has not elapsed. Make that distinction visible rather than silently including recent arrivals in a denominator they have not had time to complete.

## Give every post the same time to become a result

A dashboard checked on Friday can compare Monday's post after several days with Friday's post after a few hours. That is convenient for a calendar report and unfair for a performance comparison. Define a measurement age for the question being asked, such as a fixed elapsed period after publication, and retain the timestamp of each observation. If some posts have not reached that age, mark them pending. Filling their cells with early numbers makes the newest cohort look weak by construction.

Different outcomes mature at different speeds. A view can arrive before a site visit, and a purchase may follow several sessions later. Choose an attribution and observation window that matches the decision, then resist comparing incomplete recent buyers with fully observed older cohorts. Report the number of mature units alongside the result. A fast operational dashboard and a slower evaluation report can coexist, provided their labels make the distinction clear. Speed is useful for detecting broken publication; patience is necessary for judging what the publication accomplished.

### One campaign, several clocks

- **Published:** The post becomes available to the audience.

- **Observed:** A defined age makes post outcomes comparable.

- **Converted:** Downstream actions may require a longer window.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### Day seven does not exist for yesterday’s visitor.
Day-seven conversion should cover people given seven full days to convert.

### Cohort maturity
Day-seven conversion should cover people given seven full days to convert. Mixing mature and recent cohorts distorts comparisons.

### What can mislead.
A purchase during a period is not necessarily attributable to a visit in that period.

## Story: From concept to practice.

### Choose the starting event and outcome.
Adapt this to your audience, budget and test scope.

### Exclude immature journeys from day-seven rates.
Adapt this to your audience, budget and test scope.

## TokPortal workflow: Ask for a defined series, then interpret it

A common observation window is easier to maintain when the measurement request is explicit. This read-only example asks for daily gained views over a stated period; change the dates to your evaluation window.

Endpoint: GET /api/ext/analytics/series

```json
{
  "tool": "tokportal_get_analytics_series",
  "arguments": {
    "metric": "views",
    "granularity": "day",
    "mode": "gained",
    "from": "2026-09-01",
    "to": "2026-09-07"
  }
}
```

No chart of customer results is invented here. Read the returned series and its availability before drawing conclusions. Views describe distribution; first purchases and attribution still need their own event evidence.

- **Read the contract:** GET /api/ext/analytics/contract describes the available metrics and their meaning.

- **Respect missing data:** Series and exports depend on plan access. Missing or redacted values mean unavailable, not zero.

- **Compare like windows:** GET /api/ext/analytics/export/videos provides a plan-aware CSV for further analysis. Keep mature cohorts separate from recent posts.

## Put it to work

1. Choose the starting event and outcome.

2. Exclude immature journeys from day-seven rates.

Limit: A purchase during a period is not necessarily attributable to a visit in that period.

## Sources

- https://developers.tokportal.com/analytics/

- https://developers.tokportal.com/mcp/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
