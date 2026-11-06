# Market Rewind — GitHub Pages edition

A complete static educational stock game. No build, server, API key, subscription, or Sites dependency is required. Source is plain HTML, CSS and JavaScript. All market data is bundled in prices.js. Fonts are bundled locally, with their licenses in fonts/. No external stylesheet or background market-data request is needed.

## Publish on GitHub Pages

1. Unzip this archive.
2. Create a GitHub repository and upload the contents of this folder (index.html, style.css, app.js, prices.js, .nojekyll and the entire fonts folder) into the root of its main branch. Upload the files themselves, not an enclosing folder.
3. Open repository Settings → Pages.
4. Choose Deploy from a branch, main, and /(root), then Save.
5. Open the URL GitHub provides after deployment. The site supports both a user site and a repository subfolder, such as https://YOUR-NAME.github.io/YOUR-REPOSITORY/.

Official instructions: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

GitHub Pages is generally publicly accessible; the private Sites preview does not make the GitHub deployment private.

## Preview locally

For a normal HTTP preview, run `python -m http.server 8080` in this folder and visit http://localhost:8080. Python is only a preview convenience; it is not needed by visitors or GitHub Pages.

## Features

- Six introductory lessons (including volume) with simple visuals and a seventh further-reading page.
- Twelve real stocks (AAPL, MSFT, NVDA, TSLA, DIS, INTC, PTON, SNAP, PYPL, ZM, NKE and ROKU), including losing historical outcomes; random actual trading session from 2023 through 2025.
- All requested ranges: 1D, 1W, 1M, 1Y, 2Y, 5Y, 10Y and MAX (full available provider history).
- Daily candle and line charts, volume, moving average and historical 52-week range.
- Market, limit and stop buy orders; selectable holding horizon; pass and reveal.
- $10,000 fresh paper cash each round; fractional shares and dollar-amount purchases; idealized fills that ignore gaps and available volume.
- Limit-order explanations for fills and non-fills; revealed charts show a horizontal limit price and vertical fill date when it is in view. The limit price is included in the chart scale.
- Outcome review, process-focused technical context and a browser-local journal.
- Stock identity hidden until a buy or pass decision; clear calendar-day holding choices.
- Relative asset URLs and hash navigation: no routing rewrites needed.

## Data and limitations

Source: Yahoo Finance chart endpoint. Retrieved November 5, 2026. Fixed daily snapshot: original six stocks through November 5, 2026; six added stocks through November 4, 2026. Each round shows its actual last available date; not a live feed. Dates are explicitly displayed in the game. No intraday records: 1D shows one daily OHLC candle. Historical OHLC prices are split-adjusted by the provider, so they are not an exact vintage market screen. No dividends, fees, taxes, spread, slippage or real liquidity are modeled. No historical market cap is shown because reliable dated shares outstanding are not included. MAX covers available provider records, which can start after an IPO.

Orders are buy-only paper entries, entered as dollars or fractional shares. Market orders fill immediately at the displayed historical close. A $10,000 dollar order always invests the full $10,000. Limit buys fill at the exact limit when a later daily low reaches it; stop buys fill at the exact trigger when a later daily high reaches it. Gaps and available volume do not affect or prevent fills, even if real trading skipped the trigger. Entries expire after 30 calendar days or the chosen end date. Filled positions are valued at the final close. This is an idealized price-decision game, not a realistic execution simulator.

Holding choices are 1 calendar day, 1 week, 30 days, 365 days, or the latest available date. Targets are counted from the decision date; if closed, the next recorded market day is used. Data availability caps all results. Fractional quantities use normal JavaScript number precision; display rounding does not change internal P/L calculations.

The 12-stock sample includes many losses but still has selection and survivorship bias. Stock identities are concealed in the interface until the decision; the static data remains inspectable. Technical observations are descriptive, not predictive. Future data is bundled and can be inspected by a technical visitor; this is not a secure competition.

## Update the snapshot

prices.js assigns an object to window.MARKET_DATA. Each ticker has a name, source URL, firstTradeDate and rows. A row is [YYYY-MM-DD, open, high, low, close, volume]. Rows must be chronological, unique and contain finite positive prices and nonnegative volume. Preserve full available history for the long chart ranges.

To refresh, retrieve the provider's full daily history for each ticker using explicit period1 and period2 timestamps with interval=1d (range=max may silently aggregate). Validate the response, remove incomplete/null sessions and set a consistent completed-session cutoff. Replace prices.js only after all twelve symbols succeed. Update the latest-data option and the data/methodology dates in app.js, and this README, to match the new verified cutoff. Do not automatically assume that a response contains today's completed close. Provider licensing and access policies apply separately from this application source.

## Privacy

No account or analytics. The journal is kept in localStorage on the visitor's browser. It is not encrypted and should not contain sensitive personal information. Only the latest 30 validated records are kept. Clear it in the game or through browser storage settings. The hosting service handles requests under its own policy. Fonts and other assets are served from the same site.

## Educational references

- SEC Investor.gov — Stocks: https://www.investor.gov/introduction-investing/investing-basics/investment-products/stocks
- SEC Investor.gov — Types of Orders: https://www.investor.gov/introduction-investing/investing-basics/how-stock-markets-work/types-orders
- FINRA — Frequent Intraday Trading: https://www.finra.org/investors/insights/frequent-intraday-trading
- Fidelity / Wiley — Swing Trading Setups: https://www.fidelity.com/learning-center/trading-investing/trading/swing-trading

- Fidelity — Reading volume: https://www.fidelity.com/viewpoints/active-investor/stock-volume

## Security maintenance

The page declares a restrictive Content Security Policy before loading any assets: scripts/styles/fonts from this site only, no inline script or style attributes, no dynamic code evaluation, no background network connections, no embedded frames or plug-ins, no base-URL override, and no form navigation. Event handlers are registered by the local app script. A no-referrer policy is also declared. Keep assets local when making edits; third-party embeds or APIs will require a deliberate policy review.

Lesson URLs are validated. Stored journal records are size-limited, schema-checked and escaped before display. Trading controls are validated again by the calculation function, rather than trusting only HTML input constraints. The game has no application server, package dependencies, real financial transactions or API secrets.

HTTP-only protections such as frame-ancestors, HSTS and MIME-sniffing controls are hosting responsibilities and cannot be fully configured through an HTML meta policy. Do not interpret an HTML policy as a substitute for server security. The GitHub Pages export has no authentication; use private hosting if access must be restricted.

Future prices and paper results remain client-side and can be inspected or changed by a visitor. This design is suitable for private practice, not trusted rankings or prize contests. The security review is a scoped code/browser review, not an assurance about the hosting provider, browsers or account security.
