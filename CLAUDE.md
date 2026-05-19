# AGENTS.md v1.0.0 · 2026-05-19

## Project

This theme is based on the [Shopify Horizon theme](https://github.com/Shopify/horizon).

Follow Horizon conventions when making changes: server-rendered Liquid first, vanilla Web Components (via `assets/component.js`), theme blocks as first-class components, declarative `on:{event}` binding, `@theme/*` import maps, and native HTML over custom JS. See Shopify's `.cursor/rules/` for detailed standards.

Edit `.liquid`, `.js`, `.css`, and `.json` files directly. Unless otherwise noted, there is no build step, no bundler, and no project test framework.

## Priorities

When tradeoffs arise, prioritize in this order:

1. Correctness and merchant safety
2. Accessibility and performance
3. Horizon conventions and upgradeability
4. Minimal code and dependencies

## Workflow

- **Pull before you push.** Always sync the latest (keeping in mind changes may have been made from the Shopify admin) before making changes. If you cannot, surface it as a blocker and stop.
- **Make the smallest correct change.** Prefer the narrowest implementation that solves the problem cleanly.
- **Commit theme updates raw before fixing them.** Commit upstream theme updates as-is first, then fix regressions in follow-up commits.
- **Validate before finalizing.** Run the project's configured theme validation/checking process before finalizing changes.
- **Explain impact clearly.** Summarize the change, merchant-facing effects, manual QA needs, follow-up work, and risks.

## Implementation Guidelines

- **Prefer Horizon-native patterns.** Use Liquid-first rendering, Web Components via `assets/component.js`, declarative event binding, `@theme/*` imports, and existing Horizon events/utilities where appropriate.
- **Minimize core file edits.** Prefer extension patterns and additive files. Edit core files only when necessary, and keep diffs minimal for easier upstream merges.
- **Watch for Admin-created artifacts.** Blocks and sections prefixed `ai-` are merchant/admin-generated theme artifacts. Inspect before modifying, avoid deleting or renaming them unless explicitly instructed, and preserve compatibility with them when editing related templates, sections, blocks, or schemas.
- **Never mutate existing schema IDs.** In `{% schema %}` blocks, never change existing `id` values. Add new settings and deprecate old ones instead of renaming.
- **Maintain accessibility.** Meet WCAG 2.1 AA with semantic HTML, minimal ARIA, visible focus states, and full keyboard operability.
- **Maintain internationalization.** Do not hardcode user-facing strings. Use translation keys for storefront text (`{{ 'key' | t }}`) and `t:` for translatable schema/editor text.
- **Scope CSS to components.** Use component-scoped CSS, BEM-style naming, component-namespaced custom properties, logical properties, and container queries over viewport breakpoints where practical.
- **Respect shared theme state.** Prefer existing Horizon/native events over manual DOM patching or custom state trackers.
- **Protect core conversion flows.** Any changes touching cart UI, cart APIs, add-to-cart behavior, checkout integrations, or standard form submission must be explicitly flagged for manual QA. Ensure custom JavaScript does not block, delay, or race standard form submissions.
- **Protect performance.** Keep changes performance-neutral or better. Prefer native browser APIs and Horizon patterns over external libraries where practical, and avoid unnecessary JavaScript, layout shift, and unnecessary dependencies.
- **Control binary/media assets.** Do not add large binary/media assets to `assets/` by default. This includes large images, videos, fonts, PDFs, archives, and other non-code files. Prefer Shopify CMS/admin-managed media or other project-approved hosting for large or merchant-editable assets. Add binary assets to `assets/` only when they are theme-critical, optimized, reasonably small, intentionally version-controlled, and explicitly required for the implementation.
- **Protect live settings and local secrets.** Never commit, publish, or include `config/settings_data.json` in a release; it contains live store settings. Settings should flow one way: admin to local, never pushed back. Never commit `.env`, `.env.*`, or `.shopify/`.

## Definition of Done

- Latest source-of-truth version was synced before work began.
- The smallest correct change was made.
- The project's configured theme validation/checking process passes.
- New or changed UI is accessible, keyboard operable, and performance-neutral or better.
- User-facing strings are internationalized.
- Existing schema IDs were not mutated.
- Protected local/live files were not committed, published, or included in a release.
- Cart, add-to-cart, cart API, or checkout-adjacent changes are explicitly flagged for manual QA.
- Merchant/admin follow-up, risks, and remaining work are clearly summarized.
