# TikTok Shop P&L Dashboard

**Live demo:** https://guitpf.github.io/tiktok-shop-pl-dashboard/ (pre-loaded with synthetic data — try editing costs or settings)

## What this is

A profit & loss dashboard built for running a TikTok Shop channel — not a generic sales dashboard, but one built around a real problem: TikTok Shop and Shopify each give you half the picture, and getting from "raw order export" to "what did we actually make after VAT, returns, fulfillment, marketing, and per-product cost of goods" normally means a manual spreadsheet every month.

This tool does that automatically: drop in a raw Shopify order export, and it reconstructs full German-accounting-correct monthly P&L — net revenue after VAT and returns, gross margin, EBIT, and per-product profitability — then tracks it month over month.

The real tool (same code, same import engine) runs on my actual TikTok Shop data privately. This public version is a **look-only demo**, not a tool for others to run their own data through: it's pre-loaded with synthetic data — "Product 1" through "Product 4," fake order numbers — and the data-import entry point is intentionally left out of the UI, so it's safe to show without exposing any employer's real sales figures or functioning as a giveaway tool.

## Why this matters for a marketing role

This is the difference between "I ran a TikTok Shop channel" and actually understanding the unit economics behind one. The tool handles real complexity most marketers wave away: VAT varies by country and has to come out of revenue before margin means anything; a Shopify order export repeats order-level fields only on an order's first line item, so naive parsing double-counts or drops revenue; a "monthly" export often actually contains an order's full history, not just the current month. Getting all of that right — and then turning it into a dashboard — is applied operational and technical understanding, not just marketing fluency.

## What the real tool does

- **Imports** a raw Shopify `orders_export_*.csv`, unmodified, straight from the admin panel.
- **Reconstructs real P&L**: gross revenue → minus returns → minus VAT (per country, correctly backed out of gross) → net revenue → minus cost of goods → gross profit → minus fulfillment, marketing, logistics, and license costs → EBIT.
- **Tracks month over month**: revenue trend, margin trend, a full cost-structure breakdown (% of revenue or absolute €), and a product-profitability ranking.
- **Handles real-world messiness**: multi-month exports get split by order date automatically; missing cost-of-goods prices are flagged, not silently assumed; months missing marketing/logistics entries are visibly marked incomplete rather than quietly wrong.

The full CSV-parsing engine (`parseCSV`/`analyzeCSV` in [`index.html`](index.html)) is in the repo to read — it's just not wired to a visible upload button in this public demo.

## Try it yourself

The live demo loads with three months of synthetic data already in place. Click a month's **"Kosten bearbeiten"** to edit marketing/logistics costs, or **"⚙ Stammdaten"** to adjust cost-of-goods and VAT rates, and watch the KPIs and charts recalculate. Click **"↺ Demo zurücksetzen"** any time to wipe your changes and return to the original synthetic data.

## A note on the data

All figures — order volumes, revenue, product names ("Product 1," "Product 2," etc.) — are synthetic, built to be directionally realistic. No real business metrics from any employer appear anywhere in this repo. The German accounting references in the footer (§15 UStG on deductible input VAT, §277 HGB on returns as revenue reductions) are general legal references, not company-specific information.
