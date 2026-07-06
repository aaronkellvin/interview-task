# Notes

## Explain one fix

The PHP 0 booking bug came from `rental_days` using `(to_date - from_date).days`, which counts the gap between dates rather than inclusive rental days. A same-day rental (e.g. Jan 10–Jan 10) produced 0 days, so the total was PHP 0.00. The fix adds `+ 1` so both the start and end day count, matching the business rule stated in the app header.

## Show the failure

Canon DSLR Camera, Jan 8–Jan 12 (existing booking is Jan 10–Jan 15).

## AI use

I ran the app locally and identified bugs by reviewing `app.py` and `index.html`. I used Cursor to verify these bugs and validate my fixes against edge cases, including date range overlaps, inclusive day counting, and maintenance filtering. I also used Cursor to clean up the code for readability and consistency.