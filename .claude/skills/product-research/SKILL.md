---
name: product-research
description: Method for product and competitor research. Use when the task is to find which products to sell, compare shops and competitors, or check prices, stock, delivery times or demand for exact products.
---

# Product and competitor research

Goal: answer the open questions in the project's brief with facts a decision can rest on.

## Before searching

1. Read the project's brief in `vault/01-projects/<project>/` and any research already there. Build on it, don't repeat it.
2. Say which open questions this task answers.
3. Work on exact products: brand, line, grade, size, pack. If the task names only a category, list the exact variants first. A different grade, size or pack is a different product.

## What to collect

**Prices and availability.** One row per shop per exact product:

| Product (exact) | Shop (online or physical, country) | Price incl. VAT | Shipping to the customer's city | Delivery time | In stock? | Source | Checked on |
| --- | --- | --- | --- | --- | --- | --- | --- |

- Count what the customer actually pays: VAT, shipping, minimum order, free-shipping threshold.
- "In stock" only when the page says so. "On order" or no stock information is not in stock.
- Physical shops: only what their site, listing or a call confirms.

**Competitors.** For each one: range for the target products, price level, delivery (cost, time, threshold), kits or bundles, advice and content, and what customers complain about in reviews.

**Demand outside the user's circle.** Marketplace reviews and best-seller ranks, questions in forums, groups and Reddit, search interest. Quote and link, don't score.

## Rules

- Use the page itself as the source: shop, brand, distributor, marketplace listing. Not a search snippet or an AI summary.
- Never infer a fact from a URL, a language version, a locale or a meta description. A Spanish-language page doesn't mean a shop ships to Spain: check its shipping or terms page.
- Before saying a shop doesn't sell something, search its whole catalogue for the brand, not one product page. The same grade can be sold in another format on another page.
- Date every price and stock check.
- If a page fails to load or hides prices, say so. Don't guess.
- Stop when the questions are answered. At most about 10 shops per product unless asked for more.

## Output

1. **Answer:** 3 to 5 bullets.
2. **Facts (verified):** the tables above, every row linked and dated.
3. **Hypotheses:** what the facts suggest, each labelled as a hypothesis, with what would confirm it.
4. **Next checks:** the 3 to 5 most useful things to verify next, and who can verify them (the web, a call, a customer, a supplier).

End with one line: which questions are now answered and which are still open. The orchestrator, not you, writes the results into the vault.
