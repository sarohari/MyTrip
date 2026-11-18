# Spec 06 — Costs and Currency

**Status:** Proposed for design  
**Requirements:** REQ-COST-001..005; AC-003, AC-005

## Objective

Specify whole-number cost entry, manual exchange rates, home-currency totals, daily/category summaries, and budget comparison.

## Data and calculations

- Each item has optional estimated and actual cost, each paired with a currency code. Entered amounts are whole numbers with no fractional units.
- The trip has a home currency and optional total budget in that currency.
- Store a manual rate per foreign currency. Define rate direction unambiguously in the interface and stored model (suggested: home-currency units per one unit of foreign currency).
- Home-currency item amount = source whole-number amount multiplied by the configured rate; apply a documented whole-number rounding rule only to the converted result.
- If a required rate is missing/invalid, identify the affected costs and exclude them from converted totals rather than silently treating the rate as 1.
- Estimated and actual totals are computed separately. Remaining estimated budget = budget minus estimated total; remaining actual budget = budget minus actual total if shown.
- Summaries group by item category and trip day. Stay cost is assigned in full to its check-in day.
- Only chosen slot options count. Unchosen candidates are excluded. Cancelled items are excluded from planned totals unless a later design decision explicitly adds cancellation accounting.
- Exceeding budget is clearly indicated and never blocks saving.

## Costs view

Show trip home currency, total budget, estimated total, actual total, remaining amount, and category/day breakdowns. Clearly flag missing exchange rates and budget overrun.

## Acceptance checks

- Enter whole-number estimated and actual amounts in home and foreign currencies.
- Set/update a foreign exchange rate and confirm category, day, and trip totals recalculate.
- Confirm stay cost appears on check-in date only.
- Confirm only chosen options count and exceeding the budget displays an advisory indicator.
- Test missing/zero/invalid exchange rates and rounding boundaries.

## Design decisions

- Exchange-rate precision and rounding mode for converted amounts.
- Whether zero cost is distinct from an empty/unset cost.
- Whether actual remaining budget is displayed alongside estimated remaining budget.
- Cancellation treatment for costs of cancelled items.
- Currency display behavior for currencies that conventionally use fractional minor units, given the whole-number product rule.

## Dependencies

Specs 01–05.
