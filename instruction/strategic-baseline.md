# Luminous Nebula — Strategic Baseline (Lean Digest)

**Purpose.** The current strategic decisions that govern the build — read this for live
context. Superseded and historical decisions (the digest of the previous-version reports)
live in `instruction/decision-history.md`.

**Last updated:** 2026-06-06.

---

## Read-first: current strategic baseline

The live decisions that govern the build. If you read nothing else, read these.

- **Business shape — pure product, not services.** Manual-service income lines were removed; all hours go to product + sales/content. Break-even ~W11-12, max drawdown ~$450.
- **Billing — Paddle as Merchant of Record** for all paid SaaS; Newsletter on Beehiiv; auth via Supabase Auth. Defer Stripe Direct until incorporated AND >$20K MRR.
- **Product names (authoritative):** Luminous Newsletter · Luminous Sentinel · Luminous JUnit Forge · **Luminous Full Forge** (the old "Luminous Forge" product — renamed to free the company name). Don't retro-edit older docs.
- **Sequencing — multi-product portfolio, single-product attention.** One primary product per phase, rest in maintenance. True parallel work is not viable at 40 hrs/wk capacity. Sentinel is the wedge; Full Forge deferred to month 6+ behind a ≥$1,500 MRR gate.
- **Capacity baseline:** 40 hrs/wk split ~22 eng / 8 sales / 5 content / 3 CS / 2 ops. Cloud ceiling ~$35/wk. Binding constraint is sales/market, not engineering.

## Living conventions (permanent reference)

- **Monorepo** at `<source-code-path>` (Turborepo + pnpm, one repo). Branching/commit/PR rules, per-persona ownership, PRs <400 lines, single reviewer (Doradus Nebula).
- **Design/code split:** design artifacts → `design/`; code artifacts → `packages/shared-ui/src/`; Figma cloud indexed via `design/figma-index.md`. WCAG 2.2 AA, 44×44 tap targets.
