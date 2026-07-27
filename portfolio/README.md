# Portfolio Data System

## Current scope

The first version stores raw IBKR YTD trades, current open positions, IBKR YTD NAV curve, realized P&L by symbol, stock lot scaffolding, and option allocation rules.

## Default cost and option allocation rules

| Strategy | Default treatment |
|---|---|
| Stock buys | Build lots using trade net amount plus commission. |
| Stock sells | Use IBKR realized P&L as reported first; maintain FIFO lot ledger for local reconstruction. |
| Covered call | Premium lowers strategy cost for the linked stock. Buyback loss increases strategy cost. |
| Cash-secured put | Expired premium counts as strategy income for the target ticker; assignment lowers acquired stock cost. |
| PMCC | LEAPS debit is synthetic long cost. Short-call premium lowers PMCC strategy cost; short-call buyback loss increases it. |
| Standalone option | If no linked stock or LEAPS exists, keep P&L in standalone option trading. |

IBKR YTD performance is `TWR`. The NAV curve is the broker-reported portfolio performance series.
