# Generic Product Customizer – How to Start

This plan uses your current map poster store as the baseline and helps you bootstrap a cleaner, scalable React architecture for a generic product customizer.

## 1) Define the new domain boundaries (before coding)

- Keep **Customizer Engine** generic (options, layers, pricing rules, preview data).
- Treat each product type (poster, mug, t-shirt, phone case, etc.) as a plugin/config package.
- Separate concerns into:
  - `catalog` (products + variants)
  - `customizer` (state + rules + rendering)
  - `cart/checkout`
  - `content/pages`

## 2) Pick a modern baseline stack

- Build tool: **Vite + React + TypeScript** (faster dev loop than CRA).
- Routing: `react-router-dom` data APIs.
- Server state: `@tanstack/react-query`.
- App state: `zustand` (or Redux Toolkit if team prefers strict patterns).
- Forms: `react-hook-form` + `zod`.
- Styling: Tailwind or CSS Modules (choose one and standardize).
- Testing: Vitest + React Testing Library + Playwright.

## 3) Suggested project structure

```txt
src/
  app/
    router/
    providers/
    store/
  shared/
    ui/
    lib/
    hooks/
    types/
  entities/
    product/
    customization/
    cart/
    order/
  features/
    choose-product/
    customize-product/
    add-to-cart/
    checkout/
  widgets/
    navbar/
    footer/
    product-gallery/
  pages/
    home/
    product/
    customizer/
    checkout/
    info/
```

## 4) Build the customizer as a reusable engine

Core contracts to define first:

- `ProductDefinition`
  - base price
  - dimensions / printable area
  - supported option groups
- `OptionDefinition`
  - type (`color`, `text`, `image`, `layout`, `material`)
  - validation rules
  - visibility conditions
- `PricingRule`
  - additive, multiplicative, conditional rules
- `RenderModel`
  - normalized shape sent to preview renderer and checkout payload

This lets you add product types by config instead of rewriting screens.

## 5) Migrate in slices (strangler approach)

1. Start a new repo (`product-customizer-web`) and set quality gates.
2. Port shared primitives first (layout shell, navigation, footer).
3. Implement one generic customizer flow for your existing **poster** product.
4. Add a second product type to validate generic design.
5. Integrate checkout/payment once customizer contracts are stable.

## 6) Quality gates from day one

- TypeScript strict mode.
- ESLint + Prettier + import ordering + no-unused rules.
- Husky pre-commit: lint + unit tests on changed files.
- CI pipeline: `lint`, `typecheck`, `test`, `build`.
- Basic observability: error tracking and analytics events for funnel steps.

## 7) Two-week bootstrap execution plan

### Week 1

- Day 1–2: Architecture decisions + scaffolding.
- Day 3–4: Routing, app providers, API client, auth/cart skeleton.
- Day 5: Customizer state model + validation schema.

### Week 2

- Day 1–2: Poster customizer UI + live preview integration.
- Day 3: Pricing engine + add-to-cart payload.
- Day 4: Tests (unit + integration) and performance pass.
- Day 5: Deploy preview and internal QA checklist.

## 8) What to do immediately next

1. Freeze and document current feature set from the existing app.
2. Write a one-page architecture decision record (ADR) for stack + state management.
3. Scaffold the new app with the structure above.
4. Implement only one vertical slice: `Product page -> Customize -> Add to cart`.

---

If you want, next I can draft:

- a concrete folder/file scaffold command list,
- initial TypeScript interfaces for `ProductDefinition`, `OptionDefinition`, and `PricingRule`,
- and a migration checklist that maps old folders/components to new architecture.
