# Dashboard Refresh Workflow

The dashboard uses a manual refresh pattern.

## What the button does

The refresh button records the click time as the requested refresh timestamp. In the current secure setup, the browser does not talk directly to IBKR. Codex executes the IBKR pull, recalculation, and GitHub write-back.

## Refresh contract

1. Read `portfolio/raw/last_sync.json`.
2. Use the previous successful sync timestamp as the incremental boundary.
3. Pull IBKR trades, positions, performance, and account summary at the click time.
4. Recompute total return curve, current positions, cash dry powder, available funds, buying power, excess liquidity, and PMCC bindings.
5. Write updated CSV/JSON/SVG/HTML files.
6. Append `sync_log/YYYY-MM-DD.md`.

## Current limitation

The long LEAPS contracts are identified at contract level from current positions. Historical short call rows are currently bound by underlying symbol and timing because the YTD trade snapshot does not expose expiry and strike for each short option trade.
