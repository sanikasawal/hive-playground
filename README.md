# hive-playground

A small TypeScript billing app used to try Hive with real coding agents. Prices are stored and
computed in US dollars as decimals today. The repository is deliberately simple: a catalog,
pricing, tax, invoice formatting, and two UI labels, plus a passing test suite.

## Run
```bash
npm install
npm test
npm run typecheck
```

## Try Hive with real agents
1. Ask your Hive admin for a member token (Connect screen on the Hive dashboard).
2. Clone this repo, `npm install`, then run the Connect screen's one-line setup in this folder.
3. Start Claude Code here. Each teammate does the same on their own laptop.
4. Give each agent one of the tasks below. They collide on the price unit by design.

### Agent tasks
- **Pricing agent:** "Money bugs keep appearing from floating point. Change pricing so that
  `getPrice` returns integer cents instead of decimal dollars, and update the catalog and
  `applyDiscount` accordingly. Keep tests green."
- **Invoice agent:** "Add a `buildReceipt(invoice)` function in `src/invoice.ts` that returns a
  plain-text receipt with one line per item and the total in dollars, and add tests for it."
- **UI agent:** "Rename the export button label to 'Download invoice' and add a
  `cancelButtonLabel`. Add a test for `renderButton`."

The pricing and invoice agents share `getPrice` and disagree about its unit. Hive should raise
the finding, one agent should propose a Ghost Contract (for example an explicit `unit`
parameter or a new `getPriceCents` function), both should acknowledge it, and `npm test`
against the real code is what finally verifies it. The UI agent should never be blocked.
