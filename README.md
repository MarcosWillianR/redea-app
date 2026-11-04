# Rédea · public site

Public website of **Rédea**, a Brazilian personal-finance app for people who want to get out of debt.
It shows how much you can spend today, tracks every installment down to the last one and warns you
before each bill is due.

**Live:** https://marcoswillianr.github.io/redea-app/ · [Em português](#em-português)

![The landing page: the light rein, the headline and the Início screen rising from the bottom edge](assets/og.jpg)

The screens on the page come from the new version (4.0), which is in closed testing on TestFlight, and
they show demo data. The App Store still has version 3.1.

## Pages

| Page | What it is |
|---|---|
| [`index.html`](index.html) | Landing page with the screens of the new version |
| [`privacidade.html`](privacidade.html) | Privacy policy (LGPD), linked from the App Store listing and from inside the app |
| [`excluir-conta.html`](excluir-conta.html) | How to delete the account with or without the app (Google Play requires this page) |
| [`suporte.html`](suporte.html) | FAQ and contact |

These URLs are in the App Store listing and hard-coded in the app. The site moved here when the
repository was renamed, and since GitHub Pages does not redirect a renamed project site, a small
repository at the old address sends every page here, so the links in older builds keep working.

## How it's built

- **Plain HTML and CSS.** No framework, no build step and no JavaScript: four pages don't need them.
  `.nojekyll` makes GitHub Pages serve the files exactly as they are in the repository.
- **No third-party requests.** DM Sans, the app's typeface, is served from here as WOFF (licence in
  [`assets/fonts/OFL.txt`](assets/fonts/OFL.txt)), and the site has no analytics or tracking. The app
  has no third-party analytics either: as the privacy policy says, it measures usage only through the
  each account's event history, in totals across all accounts. A Content-Security-Policy on every page
  makes the browser enforce the site's part.
- **The app's own artwork.** The light rein behind the hero is adapted from the app's `ReinGlow`
  component (React Native SVG): the same curve shape, colour stops and bright core, scaled to sit
  behind the phone, under the app's grain texture.
- **Light screens.** Captures from the iOS Simulator (iPhone 17 Pro, demo account), converted to WebP
  with `cwebp` at about 50 KB each. Every image has explicit dimensions, so nothing shifts while it
  loads, and images below the fold load lazily. On phones, pairs of screens scroll sideways with
  scroll snapping instead of shrinking.
- **Accessible.** Landmarks and a heading outline, a skip link, alt text that says what each screen
  shows, text contrast of at least 5:1 (WCAG AA), visible keyboard focus, and layouts checked from 320 px
  up.

## Publishing

GitHub Pages serves `main` from the root. The source lives in the app's monorepo (`site/`), next to the
code the privacy policy describes, and each change is copied here when it is published.

## About the app

I'm Marcos Willian, and I build Rédea end to end. The app's repository is private. In short:

- **Mobile:** Expo SDK 57 (React Native 0.86, React 19 with the React Compiler, TypeScript),
  expo-router, TanStack Query, Reanimated 4 and iOS widgets.
- **API:** Fastify 5 and PostgreSQL with Drizzle ORM, hosted on Fly.io and Neon in São Paulo, so account
  data is stored in Brazil.
- **Shared code:** a pure, unit-tested domain package that holds every business rule (installments,
  Tabela Price amortization, early payoff, matching statement lines to upcoming bills), and Zod schemas
  as the contract between the app and the API.
- **Accounts:** Sign in with Apple or Google, the API's own short-lived JWTs with rotating refresh
  tokens, and isolation tests that check one person can't read or change another's data.
- **Bank statements:** an OFX/SGML parser with bank profiles (Nubank, Inter), de-duplication by
  transaction id (FITID), and detection of recurring bills and installments.
- **Process:** an npm workspaces monorepo. CI on GitHub Actions runs type checks, lint, architecture
  rules, tests, a dependency audit, the API's Docker build and the app bundle, and decisions are
  recorded as ADRs.

## Em português

Site público da **Rédea**, app de finanças pessoais para quem quer sair das dívidas: mostra quanto dá
para gastar hoje, acompanha cada parcela até a última e avisa antes de cada conta vencer. No ar em
https://marcoswillianr.github.io/redea-app/.

- As telas da página são da nova versão, em testes fechados no TestFlight, com dados de demonstração.
  A App Store ainda tem a versão 3.1.
- `privacidade.html`, `excluir-conta.html` e `suporte.html` estão na ficha da App Store e no app. O
  site veio para este endereço quando o repositório foi renomeado e, como o GitHub Pages não
  redireciona, um repositório no endereço antigo manda cada página para cá: os links das versões
  antigas do app continuam funcionando.
- HTML e CSS puros, sem framework nem JavaScript, e sem chamar nenhum outro endereço: a DM Sans é
  servida daqui, não há analytics, e a CSP de cada página faz o navegador garantir isso.
- A rédea de luz do topo é o desenho do próprio app (o componente `ReinGlow`) adaptado para SVG.
- A fonte fica no monorepo do app (`site/`) e é copiada para cá a cada publicação.
