# BIDA — Codex implementation guide

Prepared 13 October 2026. Status: proposed implementation brief, awaiting Milestone 0 approval. No application has been scaffolded or deployed.

## 1. Copy-ready Codex master prompt

Paste the following prompt into Codex in the intended BIDA repository. Attach the approved BIDA assets or place them in the documented asset directories. A prompt does not give another Codex session access to this conversation's files.

```text
You are implementing the BIDA public marketing website as a senior frontend engineer and UI designer. Work in the current repository. Inspect existing files, package scripts, lockfiles, and applicable AGENTS.md instructions before editing. Preserve existing work. Verify version-sensitive APIs using installed package documentation and official sources. Follow the existing package manager; for a new repository use npm and commit its lockfile.

PRODUCT AND SCOPE
BIDA is a remittance mobile app for overseas Filipino workers and people sending money to the Philippines. Build a marketing and app-download experience. Start with the homepage, using an architecture that can later support additional pages. Do not implement accounts, balances, a remittance dashboard, payments, authentication, a rate calculator, or transactional functionality.

CONFIRMED STACK
Next.js App Router, strict TypeScript, Tailwind CSS, shadcn/ui, GSAP with ScrollTrigger, @gsap/react, Lucide React, and Vercel deployment. Use stable compatible releases at setup time, record installed versions, and preserve the lockfile. Use the generated Tailwind configuration conventions for that version. Do not mix Tailwind version setups or assume deprecated Next.js lint commands.

VISUAL DIRECTION
Premium light-first hybrid: approximately 70% white or light-gray visual surface area and 30% deep navy/purple, assessed across the full homepage, not by section count. Apply the actual BIDA identity and supplied mobile screens. Use Apple-inspired editorial spacing, clear typography, large product imagery, simple navigation, and restrained rounded panels. Inspiration is composition and hierarchy, not copied graphics or Apple trade dress.
Use authentic, licensed OFW and Filipino family lifestyle imagery when supplied and approved. Do not use competitor lifestyle images as BIDA assets. Avoid generic fintech blobs, excessive globes, neon effects, excessive glass effects, icon-card repetition, and automatically rotating hero carousels. Make the mobile composition intentional rather than a compressed desktop layout.
Extract candidate brand tokens from the supplied BIDA assets and identify them as provisional until approved. Preserve logo proportions and screenshot contents. Never redraw or invent app screens. Keep screenshots readable and undistorted in restrained phone frames; do not crop out essential UI. The opening screen is a brand asset, not evidence of a product feature.
TYPOGRAPHY — CONFIRMED SUPPLIED SET
The user confirms that all six supplied font files are free to use. Proceed on that confirmation; record it as user-provided permission, not independent license verification. Use next/font/local. Internal metadata has been checked:
- PPNeueMontreal-Light(1).otf: 300 normal.
- PPNeueMontrealText-Book(1).otf: 350 normal.
- PPNeueMontreal-Regular(1).otf: 400 normal.
- PPNeueMontreal-Semibold(1).otf: 600 normal.
- PPNeueMontreal-Extrabold(1).otf: 800 normal.
- PPNeueMontreal-ExtraboldItalic(1).otf: 800 italic.
Use Text Book 350 for body text, Regular 400 for general UI, Semibold 600 for buttons/subheadings, and Extrabold 800 for main headlines. Light 300 and Extrabold Italic are optional accents; do not preload all six faces just because they exist. Do not map Book to 400 or synthesize unavailable 500/700 weights. Use explicit weights or named typography tokens. Load Text Book as its own family when needed to preserve its text-specific metrics; validate visual pairing with the display family. Keep a system fallback and check font loading/layout stability. WOFF2 is an optimization option; retain original OTF files and do not change outlines.

AVAILABLE IMAGE ASSETS — 38 TOTAL
All these source assets exist; do not replace them with generic imagery or mark them as missing. Check that they are actually present in this repository; if working in another Codex session, report precisely which files still need transferring.
Brand (public/brand/): bida-primary-logo.svg, bida-primary-logo-with-bg.svg, bida-secondary-logo.svg, bida-secondary-logo-with-bg.svg. Inspect their actual light/dark rendering before selecting variants. Their SVG containers include raster imagery; do not assume pure vector scaling or strip embedded data during optimization.
App screens (public/app/): iPhone 13 mini - 956.png; homepage-Philippines.png; homepage-Philippines-with-va.png; homepage-hongkong-with-va.png; homepage-singapore.png; exchange.png; exchange-details.png; transfer.png; transfer-to-country-region.png; select-bank-transfer.png; transfer-amount-input.png; transfer-result.png.
Lifestyle/imagery direction (public/lifestyle/): image 75.png, image 76.png, image 205.png, image 206.png, image 207.png. Use supplied imagery in internal review, with publication rights/provenance recorded as pending until confirmed.
Reference-only (references/): Screenshot_1.png through Screenshot_16.png, plus bida-app-ui-color.png. Reference screenshots guide visual composition; the UI color reference informs candidate tokens. Do not publish competitor reference screenshots.
Preserve original filenames in the asset register. If normalizing spaces or '(1)' suffixes for implementation, retain an explicit original-to-project-path mapping. Place fonts in src/assets/fonts/ for next/font/local rather than making every source file a public asset.
Select one compelling actual screen for the hero; use the opening screen selectively for brand moments and the download panel. Select 3–5 authentic screens for the broader showcase based on visual suitability. Screens showing countries, fees, rates, bank logos, account details or marketing banners still require release review and do not establish approved product claims.

CONTENT INTEGRITY — NONNEGOTIABLE
Never invent product features, fees, rates, delivery times, supported countries, currencies, payout methods, app-store URLs, contact details, partner relationships, customer counts, ratings, testimonials, regulatory approvals, or security guarantees.
Screenshots document visual UI, not current commercial availability or approved marketing claims. Competitor references are never evidence about BIDA.
Centralize content, URLs, assets, provenance, and readiness states. Use explicit states such as missing, draft, and approved. Unknown URLs must be null, never '#' or fabricated URLs. Draft copy must be distinguishable from approved facts.
In review builds, render missing content as [PLACEHOLDER: description needed]. In production, omit optional unapproved sections; fail the release-readiness check for required missing content. Do not let placeholders silently disappear into believable claims.
For unknown store URLs, show noninteractive labeled status text in the download section: [PLACEHOLDER: App Store link needed] and [PLACEHOLDER: Google Play link needed]. Do not display fake functional store badges, QR codes, waitlist forms, or 'coming soon' claims. Once approved URLs exist, use official badges and real links. QR codes must encode a verified destination and have a textual link alternative.
Keep sample rates or amounts visible inside genuine screenshots as part of the image only; do not extract them into live marketing copy. Flag screenshot suitability and sensitive data before publication.

HOMEPAGE STRUCTURE
1. Header: BIDA identity, links to available on-page sections, primary 'Get the app' anchor to #download. Mobile navigation with keyboard support, focus management, Escape handling, and clear labels. Do not link to future pages that do not exist.
2. Light hero: one clear H1, brief audience explanation, primary download-section anchor, secondary 'Explore BIDA' anchor to #app, real BIDA phone visual. Suggested draft headline: 'Closer to home, wherever you are.' Suggested draft description: 'Meet BIDA, a remittance app for overseas Filipinos and people sending money to the Philippines.' Mark these as draft awaiting copy approval.
3. Light product introduction: actual approved app screens with short approved captions. Select from the 12 supplied app screens; do not create fictional feature cards or infer approved availability from visible UI.
4. Light lifestyle story: approved OFW/family imagery and draft emotional brand copy; no testimonials or unsupported promises. Omit from production until assets and copy are approved.
5. Optional product walkthrough: only approved steps and capabilities. Do not invent a three-step flow just because it is common. Keep this section deferred until confirmed content exists.
6. Deep navy/purple download section: recognizable BIDA visual, concise approved invitation, verified app-store actions when available, explicit placeholders in review otherwise.
7. Optional FAQ: approved questions and answers only. No generic answers about cost, timing, availability, verification, or security.
8. Footer: brand, confirmed operator identity/contact and actual legal/support routes when available. Draft placeholders in review; no fake business details or empty legal pages.
Choose section ordering and spacing as an editorial narrative. Start with a lean homepage and expand only when approved content supports it.

ARCHITECTURE
Keep page composition and static content as Server Components. Isolate interactive mobile navigation, FAQ behavior, and motion into small Client Components. Do not add 'use client' to the root layout or full homepage for convenience. Do not introduce a global state library, CMS, database, authentication, or backend in phase one.
Use a shared marketing layout, site shell, section/container primitives, centralized design tokens, typed homepage content, asset manifest, and site configuration. Use shadcn selectively for real interactive primitives; create a distinctive marketing layout rather than reproducing a dashboard template. Use Lucide for supporting UI icons, never to replace BIDA identity or app-store brands.
Keep future /about, /help, /privacy, and /terms as planned routes only. Create and expose them when approved content is available. A route group is organizational and must not add a URL prefix.

MOTION
Implement the static responsive homepage first and obtain approval before adding motion. Use GSAP/ScrollTrigger and useGSAP scoped cleanup. Animate transform and opacity, mainly for restrained reveals and one product demonstration. Keep text and content available before JS initializes and when JS is disabled. Do not hide all sections in global CSS.
Honor prefers-reduced-motion and respond to preference changes. Reduced-motion users get complete static content. Use responsive motion rules; disable pinned storytelling and expensive parallax on small screens. Never hijack scrolling. Keep navigation and downloads usable during animations. Avoid animation-caused layout shifts and repeated refresh loops. Clean up timelines, triggers, and listeners on unmount and route changes. Load animation code only where needed.

ACCESSIBILITY AND PERFORMANCE
Aim for WCAG 2.2 AA, including visible focus, semantic landmarks, skip link, sensible heading hierarchy, readable contrast, accessible menus and accordions, useful alt text, and comfortable touch targets. Verify with keyboard and assistive-technology-oriented checks; do not claim certification.
Use next/image with intrinsic dimensions and accurate sizes, prioritize only the critical hero image using the installed Next.js version's supported API, lazy-load below-fold visuals, and optimize approved imagery. Preserve screen readability when compressing. Use next/font/local with the supplied fonts and the user-confirmed permission recorded in the asset register. Reserve image and font space to reduce layout shift.
Target good Core Web Vitals: LCP <=2.5s, INP <=200ms, CLS <=0.1 at the 75th percentile once field data exists. During development, report lab measurements and limitations; do not imply field results. Aim for Lighthouse mobile performance >=90 and accessibility >=95 on the production build, but report actual results and investigate failures instead of claiming success by intent.

SEO AND RELEASE
Use server-rendered content, accurate title and description, real social assets, and metadata appropriate to the installed Next.js version. Set canonical URL, metadataBase, sitemap, and production robots only after the domain is confirmed. Protect draft previews with platform access controls and noindex; robots is not access control. Include only real published routes in the sitemap.
Do not fabricate SoftwareApplication or financial-service structured data, prices, reviews, or operator details. Add structured data only from approved facts. Avoid analytics and advertising scripts until provider, events, consent requirements, and ownership are agreed. Do not collect personal data in phase one.
Do not publish without an explicit final release approval. Use a Vercel preview for review only when approved; do not silently substitute another framework or hosting platform.

WORKFLOW AND APPROVAL GATES
Work one milestone at a time. Before every gate, make the result concrete and reviewable, run appropriate checks, provide a concise change summary, list unresolved placeholders, and ask for approval. Stop dependent implementation until approval arrives. Fix problems within the current milestone without asking for every small edit.
Milestone 0: implementation brief, asset/content inventory, homepage structure, architecture, provisional design direction.
Milestone 1: project foundation, design tokens, shared shell, content/readiness model, one responsive header/hero slice. Show desktop and mobile previews or screenshots if tooling supports them; disclose any QA limit.
Milestone 2: complete static responsive homepage using available approved assets, with clearly marked review placeholders.
Milestone 3: accessible restrained motion added to the approved homepage.
Milestone 4: validated content, real downloads, approved legal routes, SEO, accessibility/performance checks, and Vercel release candidate. Production publication is a separate explicit approval.

VERIFICATION AND HANDOFF
For code milestones, run configured lint, TypeScript checks, and production build. Add meaningful interaction tests for the mobile menu, verified download destinations, readiness checks, and reduced-motion behavior where supported. Do not create tests that merely mirror JSX or snapshot every stylistic choice.
Review widths of 360, 390, 768, 1024, and 1440 pixels, plus 320-pixel reflow, keyboard navigation, touch use, 200% zoom, reduced motion, and content availability without animation JS. Check horizontal overflow, image quality, broken links, hydration errors, console errors, and cleanup on navigation.
Keep README setup instructions, content gaps, asset provenance, decisions, and milestone status current. Report actual commands/results. Distinguish completed, proposed, blocked, and untested work.

FIRST ACTION
Inspect the repository and assets. If Milestone 0 has not been approved, prepare the implementation brief and stop for approval. If it has been approved, implement Milestone 1 only. Do not build the whole website in a single pass.
```

## 2. Proposed repository architecture

```text
bida-marketing/
  src/
    app/
      layout.tsx                # document, font, metadata defaults
      globals.css               # Tailwind entry and brand tokens
      (marketing)/
        layout.tsx              # shared header/footer
        page.tsx                # server-rendered homepage composition
      not-found.tsx
      robots.ts                 # draft noindex policy; production domain-dependent
      sitemap.ts                # add when production domain/routes are confirmed
    components/
      layout/                   # SiteHeader, MobileNav, SiteFooter
      home/                     # Hero, AppShowcase, LifestyleStory, DownloadSection
      shared/                   # Container, SectionHeading, PhoneFrame, ContentPlaceholder
      motion/                   # isolated GSAP client components
      ui/                       # selected shadcn primitives
    content/
      home.ts                   # typed copy and approval states
      assets.ts                 # dimensions, provenance, alt text, readiness
      gaps.ts                   # outstanding content/asset decisions
    config/site.ts              # domain, real URLs, operator/contact readiness
    lib/
      utils.ts
      content-readiness.ts      # required production content checks
    types/content.ts
    assets/fonts/               # supplied local fonts; load only used faces
  public/
    brand/                      # approved SVG/PNG identity and social assets
    app/                        # authentic approved mobile screenshot exports
    lifestyle/                  # licensed approved photography
  references/                   # inspiration; never served as website content
  docs/                         # brief, content gaps, decisions, asset register
  tests/                        # meaningful interaction/readiness checks as needed
  package.json
  package-lock.json
  components.json
  next.config.ts
  tsconfig.json
  eslint.config.mjs
  README.md
```

Start with no API routes. Homepage section links are enough for launch architecture; do not create empty pages to fill navigation. Future routes share the marketing layout when content is ready. Keep decorative styling separate from content status so a missing asset can be substituted without rewriting the page.

Example content contract:

```ts
type Approval = 'missing' | 'draft' | 'approved';
type ContentItem<T> = {
  value: T | null;
  status: Approval;
  source: string | null;
  note?: string;
};

// Until the destinations are supplied and approved:
const downloads = {
  apple: { value: null, status: 'missing', source: null },
  google: { value: null, status: 'missing', source: null },
} satisfies Record<string, ContentItem<string>>;
```

No CMS is necessary for the first homepage. Centralized typed content makes a later CMS migration possible without committing to one now.

## 3. Asset and information checklist

### Available assets reviewed

| Asset | Role | Implementation treatment |
|---|---|---|
| iPhone 13 mini - 956.png | BIDA opening screen: deep navy, white BIDA wordmark, violet emblem | Use as an authentic opening-screen visual alongside supplied logo variants |
| Screenshot_1–7.png | Apple layout references: generous space, focused product imagery, highlight panels, grids | Inspiration only; never ship these screenshots as BIDA website graphics |
| Screenshot_8–12.png | Purple payment-site references, product compositions, asymmetrical panels | Borrow hierarchy/composition selectively; do not imply their functionality or partners |
| Screenshot_13–16.png | Filipino payment lifestyle and trust/statistic examples | Inform human-centered composition only; their imagery, figures, promises and logos are not BIDA content |
| PPNeueMontreal-Light(1).otf | 300 normal | Optional large supporting text |
| PPNeueMontrealText-Book(1).otf | 350 normal | Body text |
| PPNeueMontreal-Regular(1).otf | 400 normal | General UI |
| PPNeueMontreal-Semibold(1).otf | 600 normal | Buttons/subheadings |
| PPNeueMontreal-Extrabold(1).otf | 800 normal | Headlines |
| PPNeueMontreal-ExtraboldItalic(1).otf | 800 italic | Optional emphasis |

Correction after full asset inventory, 13 October 2026: 38 BIDA-related image assets are accessible: 12 app screens including the opening screen, 16 website inspiration screenshots, five imagery-direction images, four SVG logo variants, and one UI color reference. The initial inventory was incomplete. All PNG assets have been visually reviewed; SVG files are accessible and their document dimensions have been inspected. All six font files have been inspected for weight/style metadata. The user confirms they are free to use; permission is user-provided, not independently verified.

Additional actual app screens: homepage-Philippines.png, homepage-Philippines-with-va.png, homepage-hongkong-with-va.png, homepage-singapore.png, exchange.png, exchange-details.png, transfer.png, transfer-to-country-region.png, select-bank-transfer.png, transfer-amount-input.png, transfer-result.png.

Supplied imagery-direction files: image 75.png (family at home), image 76.png (traveler at an airport), image 205.png (family reunion), image 206.png (worker using a phone), image 207.png (woman using a phone indoors). These files are available; origin, rights and publication approval still need confirmation.

Supplied identity: bida-primary-logo.svg, bida-primary-logo-with-bg.svg, bida-secondary-logo.svg, bida-secondary-logo-with-bg.svg. These SVG containers are approximately 441 KB each and include embedded raster imagery; inspect rendering and optimize carefully rather than assuming pure vector artwork. bida-app-ui-color.png is the supplied UI color reference.

Use these actual assets in the foundation and homepage instead of missing-asset placeholders. Retain approval checks for screenshot contents, current product availability, image rights and brand token selection. Visible countries, banks, fee banners and exchange figures in app screens do not authorize equivalent marketing claims.

### Needed for a convincing homepage

| Item | Needed detail | If missing |
|---|---|---|
| Standalone BIDA logo | Four SVG variants supplied; verify rendering, variant usage and embedded-image optimization | Use actual supplied logo; usage rules pending |
| App icon and favicon | Approved exports at appropriate sizes | Clearly documented gap |
| Brand palette | UI color reference supplied; approve mapping to marketing surfaces | Provisional referenced tokens, labeled as proposed |
| Typography | Six fonts supplied; weights verified; user confirms free use | Integrate local fonts, use system fallback during load; WOFF2 optional |
| Product screenshots | 12 authentic app screens supplied; select strongest 3–5 and approve release suitability | Use actual supplied screens, preserve contents and proportions |
| Screenshot release check | Confirm no personal data; approve visible sample amounts/rates and UI version | Block affected images from public release |
| OFW/family imagery | Five files supplied; verify usage rights and approve crop choices | Use for internal review; publication rights still pending |
| Homepage copy | Approved headline, description and product captions | Draft labeling in content register and review UI |
| Product availability | Confirmed launch status, countries, currencies, payout methods and capabilities if mentioned | Omit those claims |
| Store destinations | Exact approved Apple and Google URLs, platform availability | Noninteractive explicit placeholders; no invented launch status |
| Operator and contact | Legal company name and verified support/contact channels | Required footer/release gaps |
| Privacy and terms | Approved documents/routes or confirmed hosted URLs | No invented legal copy or dead links; release gap |
| Production domain | Confirmed hostname and ownership | Preview noindex; canonical and production sitemap deferred |
| FAQ and proof | Approved answers, permission for genuine testimonials or verified proof | Omit optional section |
| Social card | Approved BIDA image/copy | Mark draft; create final only from approved assets |

Keep originals intact. Put inspiration outside public/. Record source filename, dimensions, rights, approval status, intended section, and derivatives for every production asset. Do not use AI to reconstruct product UI or create apparent customer testimonials.

## 4. Homepage design proposal

| Area | Surface | Purpose | Dependency |
|---|---|---|---|
| Header + hero | White | Explain who BIDA is for and lead toward download | Identity, draft copy, opening screen |
| App showcase | Light gray/white | Let visitors recognize the real mobile app | Authentic additional screens and approved captions |
| Human story | White/light gray | Connect the experience with life abroad and home | Licensed imagery and approved brand copy |
| Optional walkthrough | Light | Explain confirmed usage | Approved workflow; deferred until supplied |
| Download panel | Deep navy/purple | Focus the main conversion action | Verified store URLs; review placeholders until supplied |
| Optional FAQ | Light | Resolve confirmed practical questions | Approved answers |
| Footer | Deep navy or white, tuned for overall balance | Operator, contact and legal navigation | Approved business/legal details |

The 70/30 direction is an approximate visual balance, not a rigid formula. Use a light hero for product clarity; reserve the strongest dark treatment for the download moment. Lifestyle imagery should support the product narrative without dominating it. No market-superiority claims are established by these design choices.

Draft hero copy for approval:

> Closer to home, wherever you are.
>
> Meet BIDA, a remittance app for overseas Filipinos and people sending money to the Philippines.

Primary action: Get the app → #download. Secondary action: Explore BIDA → #app. These work in review even while external store destinations are unavailable. On mobile, keep the heading, purpose, CTA and recognizable phone image near the beginning; avoid a tall cinematic introduction that delays understanding.

## 5. Phased development and approval plan

| Milestone | Concrete deliverable | Verification | Approval decision |
|---|---|---|---|
| 0 — Brief | This guide, proposed architecture, asset gaps, section order, draft hero copy | Check against supplied assets and confirmed scope | Approve foundation scope/design direction |
| 1 — Foundation | Working Next.js project, pinned dependency tree, tokens, typed content, shared shell, header/hero slice | Lint, typecheck, build; mobile/desktop review; placeholder and menu behavior | Approve typography, color direction, hierarchy and foundation |
| 2 — Static homepage | All approved sections responsive; honest review placeholders for unresolved assets | Widths, reflow, keyboard, links, screenshot integrity, build | Approve layout and content placement before motion |
| 3 — Motion | Scoped reveals/product animation on approved layout | Reduced motion, cleanup, touch scrolling, no hidden content, performance comparison | Approve animation intensity and usability |
| 4 — Release candidate | Final assets/copy, verified downloads, legal links, domain metadata, accessibility/performance report | Production build, link and readiness checks, Vercel preview review when authorized | Approve production publication explicitly |

Parallel independent cleanup within a milestone is fine; crossing approval gates is not. Missing optional material need not block foundation work. Missing store links, required operator/legal details, and required rights/content approval prevent calling the site launch-ready.

## 6. Step-by-step start in VS Code / Codex

### Step 1 — Approve Milestone 0

Approve the proposed homepage structure, draft hero direction, provisional brand-token approach, and Milestone 1 scope. Decide whether implementation happens in your local VS Code repository or a repository accessible here. No existing repository has been selected and no scaffold has been created in this turn.

### Step 2 — Create the project after approval

From the parent folder in a terminal:

```bash
npx create-next-app@latest bida-marketing --ts --tailwind --eslint --app --src-dir --import-alias "@/*" --use-npm
cd bida-marketing
npm install gsap @gsap/react lucide-react
npx shadcn@latest init
npx shadcn@latest add button sheet
```

Review the CLI prompts and resulting versions; do not select a different framework. Choose a neutral shadcn starting palette and then bind it to the approved BIDA tokens. Add accordion later only if approved FAQ content exists. On a Windows PowerShell setup that blocks npm.ps1/npx.ps1, use npm.cmd and npx.cmd with the same arguments.

Use an active Node.js LTS release meeting the installed Next.js engine requirement and verify it locally. Record versions in README instead of relying on a remembered version number. Commit the generated lockfile. Do not automatically rewrite an existing repository using create-next-app.

### Step 3 — Place the implementation brief and assets

Copy this guide to docs/implementation-guide.md, put original references in references/, and approved production assets into their designated public/ subdirectories. Add docs/content-gaps.md and an asset register. Place the six supplied fonts in src/assets/fonts/ and record the user-confirmed permission and verified weight/style mapping. Separate approved facts from draft copy in content/home.ts.

### Step 4 — Give Codex a bounded kickoff

```text
Milestone 0 is approved. Read docs/implementation-guide.md and implement Milestone 1 only.
Inspect this repo and supplied assets first. Set up the confirmed Next.js stack, brand tokens, typed approval-aware content, shared marketing layout, accessible responsive header, and a static hero using a selected authentic BIDA app screen. Integrate the supplied local fonts with verified weights; use the opening screen selectively for brand moments. Use the supplied BIDA SVG logo, actual app screens, color reference and imagery-direction files. Use clear placeholders for missing store links and unapproved copy. Check image rights and screenshot release suitability before publication. Do not add GSAP animation yet.
Run lint, TypeScript validation and a production build. Show the header/hero at mobile and desktop sizes where tooling allows. Report actual results, content gaps and any verification limits, then stop for my Milestone 1 approval.
```

### Step 5 — Review the foundation

Run the development script and inspect the header/hero. Check brand recognition, text wrapping, readable screenshot scale, touch targets, menu focus behavior and whether the download anchor leads to an honest placeholder section. Approve or request edits before Codex builds the full static homepage.

Typical verification commands after scripts are configured:

```bash
npm run dev
# In a separate terminal; stop the dev server when finished:
npx tsc --noEmit
npx eslint .
npm run build
```

Prefer repository scripts when provided. Make lint and typecheck explicit package scripts during foundation. This guide has not executed these application commands or measured a running website.

## 7. Technical source references

Official references checked while preparing the guide; recheck at actual setup time:

- Next.js installation: https://nextjs.org/docs/app/getting-started/installation
- create-next-app flags: https://nextjs.org/docs/app/api-reference/cli/create-next-app
- Tailwind Next.js setup: https://tailwindcss.com/docs/installation/framework-guides/nextjs
- shadcn Next.js setup: https://ui.shadcn.com/docs/installation/next
- GSAP ScrollTrigger: https://www.gsap.com/docs/v3/Plugins/ScrollTrigger/

No product research result, regulatory assertion, BIDA feature availability, or market ranking is claimed by this guide.
