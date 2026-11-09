# Case Study: Front-End Modernization of a Production Business Platform

Built at Canyon Rim Consulting · July–Sept 2026  
**The platform:** a multi-tenant, NetSuite-connected business platform (sales portal, CPQ, quality control and labor costing) used by manufacturing and retail clients  
**Role:** Front-end/UI lead. I designed and built the new navigation, theme, launcher, header,
in-app help and configurator UX, delivered as **17 merged pull requests (~12K lines added)**,
each reviewed by the platform's lead backend developer.
**Stack:** React 19, TypeScript, an in-house component library (migrated from Ant Design), CSS-in-TS design tokens, Vitest/Jest + Testing Library, FlexSearch

> The source belongs to my former employer and is private. This write-up covers the
> decisions and engineering, without proprietary code, client data or screenshots.

---

## Starting point

The platform worked, but it looked and felt like an internal tool. A fixed left sidebar
ate horizontal space on the tablets the sales floor actually uses. The header took two rows.
Colors had drifted from the brand guide. Key flows had UX dead ends. I set out to modernize
the app in reviewable slices, and kept a **modernization roadmap in the repo** so the plan
survived between sessions and other people could see what was done and what was next.

## 1. Navigation: left sidebar → bottom bar and command palette

**The biggest change:** I retired the left sidebar entirely (component, resize handle,
context, constants and footer, along with their tests) and replaced it with a **bottom
navigation model** like the one NetSuite's newer UI uses:

- **Persistent bottom bar:** Home, Menu, and a live-filtering **search pill (Cmd/Ctrl+K)**.
- **Slide-up navigation overlay** with Shortcuts, Create and Menu sections, carrying over
  everything the old sidebar offered.
- **Search-first command palette:** a FlexSearch index over every resource plus recent pages,
  so users can type where they want to go instead of hunting through menus.
- **Main content now uses the full width**, since the layout no longer has to leave room for
  a sidebar.
- A consistent "raised button" depth treatment across the header, bottom bar and overlay.
- A **full keyboard tab-order and focus-visible audit** from the bottom bar through the
  overlay to every leaf link.

One PR: **60 files, +3,162 / −3,098.** It was front-end only, with no new endpoints, so the
backend team wasn't blocked.

**A bug only a real iPad could show.** After merge, an iPad Pro in Safari showed the search
bar too tall and off-center. It didn't reproduce in desktop browsers or Playwright's WebKit,
because they always report a zero safe-area inset. I worked out the cause from first
principles: the bar counted the iPad's home-indicator gap twice, once through a fixed height
and again through separate padding. I restructured it to match the header's correct pattern,
removed an input type that triggered iOS's native search styling, and confirmed the fix with
computed-style checks under a simulated non-zero inset. The same PR fixed the notification
badge pushing its bell button out of place. I added that as an **opt-in prop** rather than
changing the default, because about 15 other components relied on the existing behavior.

## 2. Brand and theme

- A palette rebuilt to match the company's **official brand style guide**, plus fixed black
  chrome that stays the same in light and dark mode while content areas follow the theme.
- **Self-hosted webfonts.** The main typeface was referenced in the CSS but had never
  actually been loaded.
- **Bugs found along the way:**
  - Help callouts were unreadable in dark mode.
  - On phones, the header's tenant switcher overflowed off-screen with no way to reach it. It
    now collapses to icons with proper `aria-label`s.
  - Success and error toasts had nowhere to render in 3 of 5 states of two switcher
    components.

## 3. Launcher redesign (the app's landing page)

- **"Liquid Glass" tiles**: translucent glass using backdrop blur and saturation, a sliding
  module switcher, and a per-tile color wash taken from each shortcut's accent color, tuned
  separately for light and dark mode.
- **A grid that actually centers.** I switched from `auto-fill` to `auto-fit` with a capped
  column width. The old grid left invisible empty columns that pushed short rows to the left.
  I also normalized icon sizes with a data migration so every default tile lines up.
- **An app-wide textured background** with mobile WebP variants to keep pages light.
- A **personalized, time-of-day greeting**, a **Presets** quick-start for adding shortcuts,
  and reliable drag-and-drop on iPad.
- I prototyped an alternative circular tile shape, reviewed it live, and **shelved it**. The
  branch was kept in case it's worth revisiting.

## 4. Header and in-app help

- **The header went from two rows to one**, freeing vertical space for content. The "Name
  (Role)" button became a real dropdown that consolidates account, logout, and **tenant and
  subsidiary switching**. I wired switching directly to the underlying state instead of
  embedding the existing switcher components, because their nested pop-ups broke inside
  another dropdown (a documented limitation of the app's dismiss handling).
- **In-app Help hub** with topic cards for Navigation & Search, Quality Control, CPQ and
  Labor Costing. Each topic only appears for clients licensed for that feature. The copy is
  plain language **checked against the live UI** rather than paraphrased from engineering
  docs. I also wrote a **staleness checker** that links each help page to the source files it
  was verified against, so the docs can't quietly drift.

## 5. Product configurator: UX audit, then fixes

The configure-price-quote (CPQ) screen is where salespeople specify custom furniture and lock
in a price. Before changing any code, I **audited it against live sandbox data** and traced
each problem to the line of code causing it:

- **17 findings ranked by value ÷ effort.** 15 could ship as front-end-only changes. 2 needed
  a data-model decision, so I flagged them for the backend lead instead of working around them.
- **Shipped:**
  - Save now always explains what's blocking it.
  - Every field is tagged Required or Optional.
  - The summary and action bar are sticky, with a live price.
  - Controls are consistent touch size.
  - Error text is cleaned before display.
  - A **touch-scroll fix in the shared dropdown component**, so every dropdown in the app
    stopped jumping or vanishing on tablets.
- **Sectional Preconfigurator re-skin** (69 files, +1,206 / −562):
  - A new shared **`GlassCard`** component built on design tokens I pulled out of the
    launcher, so the look carries across the app.
  - 38 rendered product images replacing emoji placeholders.
  - Two wizard dead ends fixed.
  - App-wide dark-mode fixes: invisible dropdown placeholders and icons, and an invisible
    segmented control.

## How the work was verified

- **TypeScript clean and lint clean** on every PR; the full local CI gate (6 jobs) green before review.
- **Full front-end suite runs of 13,700+ tests.** When an unrelated test failed, I proved
  it was pre-existing by stashing my changes, re-running, and comparing against the base
  branch, then logged it separately rather than hiding it.
- **Manual checks on real layouts**: light and dark mode, iPad portrait and landscape,
  iPhone width, keyboard-only navigation.
- **Code review taken seriously.** I addressed every review comment, and in one case
  **reverted my own fix** after review showed it changed behavior another flow depended on.

## What I'd do next

The roadmap in the repo lists the remaining pages for the same treatment, and a short list of
orphaned pages that need a keep-or-delete decision before anyone spends design effort on them.

---

*Built with Claude Code as an AI pair programmer. I owned the design direction, UX
decisions, prioritization, live and on-device testing, and the review process.*
