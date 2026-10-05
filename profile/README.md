<p align="center">
  <a href="https://xylolabs.space">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="brand/logo/xylo-horizontal-reversed.svg">
      <img src="brand/logo/xylo-horizontal.svg" alt="Xylo Labs" width="280">
    </picture>
  </a>
</p>

<p align="center">
  <strong>We build to find out.</strong>
</p>

<p align="center">
  <a href="https://xylolabs.space">xylolabs.space</a>&nbsp;&nbsp;|&nbsp;&nbsp;<a href="https://xylolabs.space/#contact">Contact us</a>&nbsp;&nbsp;|&nbsp;&nbsp;<a href="https://www.linkedin.com/company/xylohq">LinkedIn</a>
</p>

---

## About Xylo Labs

Xylo Labs is an independent product lab. We design, build and ship experiments: products, startups, developer tools, AI
and other ideas for the internet. Some grow into companies with their own name and team. Some stay small and useful.
Some end, and get written up so the next one starts smarter.

This repository is the source of [xylolabs.space](https://xylolabs.space), our public website, and of the Xylo Labs
brand kit.

## Experiments

Everything we start gets a number and ships in public. Status is one of **Live**, **Experiment**, **Building** or
**Archived**.

| No. | Experiment | Category | Status | Year |
|---|---|---|---|---|
| 001 | **Xylo**: stablecoin infrastructure for African markets | Financial infrastructure | Building | 2026 |
| 002 | **eETB**: an Ethiopian birr stablecoin on Ethereum, designed to be fully backed 1:1 (reserves not yet in place), for payments, DeFi and cross-border transfers | Stablecoin | Experiment | 2026 |

The next experiment appears here when it ships. Have one in mind? Use the
[contact form](https://xylolabs.space/#contact).

### 001 Xylo

Xylo is the layer between global onchain liquidity and local African economies. It settles USDC on Base, connects to
local fiat on and off-ramps, and gives developers an API so they can build stablecoin-powered products without
rebuilding the financial plumbing. Xylo is a prototype.

## How we work

Ideas are cheap. Finding out is the work. Every experiment goes through the same four stages:

1. **Question.** Every experiment starts as something we want to know.
2. **Prototype.** The smallest real version, built in weeks rather than quarters.
3. **Ship.** Put it in front of people and watch what they actually do.
4. **Decide.** Spin it out, keep it small, or close it and write up what we learned.

We're currently curious about products, startups, AI, developer tools, Web3 and internet experiments.

## Working with us

We're looking for co-founders, collaborators and early users. If you have a problem worth testing, or want to help
build what's next, use the [contact form](https://xylolabs.space/#contact).

---

## The website

### Stack

- [Next.js 16](https://nextjs.org) (App Router, Turbopack) and React 19
- TypeScript
- [Tailwind CSS v4](https://tailwindcss.com), with design tokens defined in `src/app/globals.css`
- [Geist and Geist Mono](https://vercel.com/font), loaded through `next/font`
- [Lucide](https://lucide.dev) for icons
- [Vercel Web Analytics](https://vercel.com/docs/analytics) for cookieless page views and a few custom events

Every page renders to static HTML, including one page per experiment and their share images. The only server code is
the contact form, a Server Action
(`src/app/actions.ts`) that emails each message through [Resend](https://resend.com). There's no database.

### Getting started

You need Node.js 20.9 or later.

```bash
npm install
cp .env.example .env.local   # then fill in the values below
npm run dev                  # start the dev server at http://localhost:3000
```

| Variable | Required | What it's for |
|---|---|---|
| `RESEND_API_KEY` | Yes | Resend API key used to send contact form messages |
| `CONTACT_TO_EMAIL` | Yes | The inbox that receives contact form messages |
| `CONTACT_FROM_EMAIL` | No | Sender address. Defaults to Resend's test sender, which can only deliver to the email you signed up to Resend with. Set it to an address on a domain you've verified in Resend. |

Without these, the site still runs and the form shows a "not connected yet" message instead of sending. In
production, set them in Vercel under Project → Settings → Environment Variables.

| Command | What it does |
|---|---|
| `npm run dev` | Starts the development server with hot reload |
| `npm run build` | Creates a production build |
| `npm run start` | Serves the production build |
| `npm run lint` | Runs ESLint |

> [!NOTE]
> This project uses Next.js 16, which has breaking changes from earlier versions. Before changing framework code,
> read the bundled docs in `node_modules/next/dist/docs/`. See [`AGENTS.md`](AGENTS.md).

### Project structure

```text
.
├── brand/                    Brand kit: logo masters, PNGs, icons, guidelines
├── public/brand/             Logo files served by the website
└── src/
    ├── app/
    │   ├── layout.tsx        Root layout, fonts, metadata and analytics
    │   ├── opengraph-image.tsx  Share image for the homepage
    │   ├── experiments/[slug]/  One page and one share image per experiment
    │   ├── privacy/          Privacy page
    │   ├── sitemap.ts, robots.ts
    │   ├── actions.ts        Contact form Server Action (validation, spam checks, Resend)
    │   ├── page.tsx          Landing page sections and their content
    │   ├── globals.css       Design tokens and animations
    │   ├── icon.svg          Favicon
    │   └── apple-icon.png    Apple touch icon
    ├── components/
    │   ├── navbar.tsx              Header that follows the light/dark section beneath it
    │   ├── hero-field.tsx          Hero mark with echo layers and cursor parallax
    │   ├── experiment-feature.tsx  Editorial block for one experiment
    │   ├── experiment-artwork.tsx  Grained stage with cursor-following light
    │   ├── flow-diagram.tsx        Experiment artwork: a three-stage flow, drawn from data
    │   ├── status.tsx              Live / Experiment / Building / Archived indicator
    │   ├── interest-list.tsx       "What we're curious about" index
    │   ├── manifesto.tsx           Statement that lights up word by word on scroll
    │   ├── contact-form.tsx        Contact form in the footer
    │   ├── site-footer.tsx         Footer shared by every page: contact form, links, disclaimer
    │   ├── track-clicks.tsx        Sends analytics events for elements marked data-track
    │   ├── logo.tsx                Logo mark in its full, compact and reversed cuts
    │   └── reveal.tsx              Scroll-triggered reveal
    └── lib/
        ├── experiments.ts          The experiment index and the list of interests
        ├── contact.ts              Contact form topics
        ├── share-image.tsx         Renderer for the 1200×630 share images (uses src/assets/fonts)
        └── site.ts                 Site name, tagline, email and the shared page container
```

### Editing content

| To change | Edit |
|---|---|
| Experiments and their details | the `experiments` array in `src/lib/experiments.ts` |
| An experiment's artwork | its `flow` in `src/lib/experiments.ts` |
| "What we're curious about" | the `interests` array in `src/lib/experiments.ts` |
| The four stages in "The lab" | the `process` array in `src/app/page.tsx` |
| Contact form topics | `contactTopics` in `src/lib/contact.ts` |
| Who receives contact form messages | the `CONTACT_TO_EMAIL` environment variable |
| Site description and tagline | `src/lib/site.ts` |
| Colours and motion | the `@theme` block and keyframes in `src/app/globals.css` |
| Page title and social metadata | `src/app/layout.tsx` |

To add an experiment, append it to `experiments` with the next number and a `slug`. Its homepage block, its page at
`/experiments/<slug>`, its share image and its sitemap entry are generated from that entry. Fill in its `flow`
(the artwork), `parts`, `standing` and `disclaimer` accurately, and add its early-access topic to
`src/lib/contact.ts`. Only list experiments that exist.

### Analytics

Page views are tracked by Vercel Web Analytics; enable it in the Vercel dashboard under the project's **Analytics**
tab. Custom events:

| Event | Properties | Fired when |
|---|---|---|
| `Early access click` | `experiment` | Someone clicks "Request early access" |
| `Pitch click` | none | Someone clicks "Have one in mind? Tell us" |
| `Contact submitted` | `topic` | A contact form message is actually delivered |

To track another link, add `data-track="Event name"` and optional `data-track-<property>="value"` attributes.

### Standards

- **Accessibility.** Keyboard focus stays visible, decorative graphics are hidden from screen readers, and every
  animation is turned off when `prefers-reduced-motion` is set.
- **Progressive enhancement.** Scroll reveals hide content only after JavaScript has loaded, so the page is fully
  readable without it.
- **Responsive.** Every section is designed from 360px phones up to wide desktops.
- **Brand.** The site follows the brand kit: monochrome, Geist, and the Strata mark. Atmosphere comes from light and
  grain, never from colour.

## Brand

The Xylo Labs mark, **Strata**, is an X built from stacked layers. It stands for the layers we build, one experiment at
a time, and nods to the bars of a xylophone. The identity is monochrome by design.

| Colour | Hex | Use |
|---|---|---|
| Ink | `#0A0A0A` | Logo, type and dark surfaces |
| Paper | `#FFFFFF` | Backgrounds and the reversed logo |
| Muted | `#6B6B6B` | Secondary text |
| Line | `#E7E7E7` | Rules and borders |

Logo files, clear space, minimum sizes, icons and usage rules are in [`brand/README.md`](brand/README.md). Please use
the supplied artwork rather than recreating the logo or retyping the wordmark.

## Contributing

This repository is maintained by the Xylo Labs team. To report a problem with the website, or for anything else,
use the [contact form](https://xylolabs.space/#contact).

When you commit, use [Conventional Commits](https://www.conventionalcommits.org) (`feat:`, `fix:`, `docs:`, `chore:`),
as the existing history does. Run `npm run lint` and `npm run build` before opening a pull request.

## License

Copyright © 2026 Xylo Labs. All rights reserved.

The Xylo Labs name, the Strata mark and the contents of `brand/` are trademarks and brand assets of Xylo Labs, and you
may not use them without permission. The Geist typefaces are used under the SIL Open Font License 1.1.
