# Notes

## Explain one fix

The PHP 0 booking bug came from `rental_days` using `(to_date - from_date).days`, which counts the gap between dates rather than inclusive rental days. A same-day rental (e.g. Jan 10–Jan 10) produced 0 days, so the total was PHP 0.00. The fix adds `+ 1` so both the start and end day count, matching the business rule stated in the app header.

## Show the failure

Canon DSLR Camera, Jan 8–Jan 12 (existing booking is Jan 10–Jan 15).

## AI use

I used Cursor/AI to read the codebase, identify the bugs, and verify changes. I double checked each change by tracing the logic against the stated business rules (inclusive billing, full overlap detection, maintenance status), mentally reproducing the Jan 8–12 double-booking case against the old `dates_overlap` check, and confirming the frontend was missing a `change` listener on the end-date field.