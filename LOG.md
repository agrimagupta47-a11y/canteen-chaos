# Debug log

Your notes. One entry per bug you fixed, using the template below.

This file is read as carefully as your code. A correct fix you cannot
explain counts for little; a bug you could not fix but investigated
honestly still counts for something.

Delete the example before you submit.

# Debug Log — Canteen Chaos

# Bug log

## CC-01 — "The search suggestions are behind everything"

**Reproduced:**

Inspected the search suggestions dropdown and its CSS stacking behaviour to investigate why suggestions could appear behind other page elements and become difficult to click.

**Cause:**

The `.search-wrap` element had `z-index: 1`, while `.suggest-box` had `z-index: 100`. The dropdown's stacking order is constrained by its parent's stacking context.

**Fix:**

Changed `.search-wrap` to use `z-index: 41` in `frontend/style.css` so it can appear above overlapping elements within the filters' stacking context.

**Checked:**

Confirm that the dropdown is fully visible and that the first, middle and last suggestions are clickable after the change. Record the observed result.

**Time:**

25 minutes

## CC-02 — "Can't read anything in dark mode"

**Reproduced:**

Investigated the dish text styling and found that dish names and prices used a hard-coded text colour that did not adapt to the active theme.

**Cause:**

The `.dish-body` rule used a fixed text colour instead of the theme's text colour variable.

**Fix:**

Changed the `.dish-body` text colour to `var(--ink)` in `frontend/style.css`.

**Checked:**

The CSS change was made. Verify dish names and prices in both light and dark modes, including the initial page load, and record the actual result.

**Time:**

10 minutes

## CC-03 — "The menu is wider than my phone"

**Reproduced:**

Attempted to reproduce the reported horizontal overflow at a 375px viewport width, but the complaint could not be reproduced during the initial test.

**Cause:**

Not established because the reported behaviour could not be reproduced.

**Fix:**

No fix applied because the cause was not confirmed.

**Checked:**

Tested at a 375px viewport. Further testing on other mobile viewport sizes may be needed.

**Time:**

30 minutes

## CC-05 — "The category bar scrolls away on my phone"

**Reproduced:**

At a 375 × 812 mobile viewport, scrolling through the menu caused the entire filter and category area to scroll away instead of remaining visible.

**Cause:**

The mobile CSS applied `overflow-x: hidden` to `.view`. This resulted in a computed `overflow-y: auto` value, which interfered with the expected sticky behaviour of the `.filters` element.

**Fix:**

Changed the mobile `.view` rule in `frontend/style.css` from `overflow-x: hidden` to `overflow-x: clip` within the `@media (max-width: 480px)` block.

**Checked:**

Retested at the same mobile viewport after the change. The filter and category area remained visible while scrolling.

**Time:**

25 minutes.

## CC-10 — "Sorting by price is backwards"

**Reproduced:**

The price sorting comparators in `backend/logic/search.js` were reversed. The `price-asc` option sorted prices from high to low, while `price-desc` sorted them from low to high.

**Cause:**

The comparison logic for ascending and descending price sorting was swapped.

**Fix:**

Corrected the comparators:
- `price-asc`: `(a, b) => a.price - b.price`
- `price-desc`: `(a, b) => b.price - a.price`

**Checked:**

The backend smoke test passed the price-sorting and name-sorting checks after restarting the backend. Browser sorting behaved inconsistently until browser caching was disabled, so the cause of that behaviour has not been confirmed.

**Time:**

1 hour

## Could not fix

### CC-03 — "The menu is wider than my phone"

**What I tried:**

Tested the menu at a 375px viewport width to reproduce the reported horizontal overflow.

**Where I got to:**

The reported overflow could not be reproduced during the initial test, so no cause or fix was established.

**What I would try next:**

Test additional mobile viewport sizes and inspect the computed widths of the menu grid, dish cards and their parent containers to identify any horizontal overflow.


