# SKN ID — (website)

A working, single-file clone of the SKN ID app, built from its public
Base44 prototype. Open `index.html` in a browser — no build step.

## What actually works in this clone

- Sign-in screen matching the prototype: "Your skin is unique. Your
  identity should be too.", Continue with Google / Continue with
  Email, gated by the required email-consent checkbox.
- Account creation (local, in this browser) and sign-out.
- 5-step SKN profile: skin type, sensitivities, goals, values,
  environment. Selected options turn lime (fixed 2026-10-31:
  multi-select options previously never showed as selected).
  Clicking "Create skin profile" redirects to your profile page.
- Design (from 2026-11-02, Figma site https://skn-id.figma.site/,
  all views studied 2026-11-02): the Figma site is one
  single-page app, not separate pages — landing, a 5-step
  quiz, and dashboard views Home / My Skin / Recommendations
  / My Routine / Account, all on one URL, with no real
  sign-in, no persistence (reload resets it), and several
  placeholder buttons. This build copies that structure and
  design in its own code, then adds real functionality:
  near-black (#0A0B0A) pages, electric lime (#C8FF38)
  accent, bone (#F0EFE7) text, muted grey-green secondary
  text, 1440px container, 86–90px header, 96–104px hero
  heading, flat dark cards, pill buttons, huge uppercase
  display headings, eyebrow labels, arch hero image
  (exact Figma Unsplash image) with lime offset shape,
  “94% routine match” badge and “Your Skin ID” preview
  card, 3-step How it works, and a lime Why band.
  Default theme is this Figma dark look; the About
  Appearance switch still toggles to a light variant of
  the same design, and a saved choice is remembered.
  Views: Landing (exact Figma landing, with real sign-in
  below the hero — Figma's Sign in misleadingly opened
  the quiz, with no sign-in form at all), Quiz (5 steps
  mapping to skin type, sensitivities, goals, values,
  environment, with lime progress, Back / Continue /
  Save &amp; exit, and See my skin profile), Home (greeting
  with real today's date, skin-feel pills, profile card,
  next morning routine, 30-day journey, picked products),
  My Skin (lime SKIN ID panel, summary, takeaways,
  report banner with working download), Recommendations
  (All / AM / PM filters that work, View product modal,
  Save to routine that actually saves), My Routine
  (Morning / Evening toggles, check-off that works,
  add-your-own product, 30-day tracker with working
  check-in), Account (real signed-in user only — never
  the Figma demo account — with preferences toggles,
  Privacy / Support via About, and real Sign out /
  Delete with confirmation). No demo date, demo user,
  or demo match scores are copied as real data.
- Dashboard tab: the only place for your SKN ID and skin
  profile — SKN ID card, completion bar, and detail cards
  for skin type, environment, sensitivities, goals, values
  and first focus, with Copy, Edit and View SKN Report
  actions, plus the create/edit builder. No Account details
  card here, and no Sign out / Delete buttons on the profile
  card. Signing in lands on Dashboard.
- My profile section (header My profile button when signed
  in, or Go to my profile on the landing page): account
  only — the Account details card (name, login email, date
  updated, SKN ID, sign-in provider) with Sign out and
  Delete account. No SKN ID card and no profile detail
  cards here. Sign out and Delete live only here, not on
  Dashboard or on the profile card. A unique SKN ID code
  in SKN A123B format is generated deterministically from
  your email, plus a copy button and a completion bar.
  Edits update the profile and report instantly.
- Login page (step 1, 2026-10-31): new visitors are prompted with
  the sign-in page first. With Supabase Auth connected, sign in
  via Google OAuth or Email OTP (8-digit code, 1 hour validity),
  every sign-in is recorded in login_history, and a returning
  user with a saved session goes straight to their profile.
  Once signed in, the header Sign in button becomes My profile,
  and the My profile tab is now labelled Dashboard (same
  profile page content). The profile page has an Account details
  card (name, login email, date updated, SKN ID, sign-in
  provider) plus Sign out and Delete account. Sign out and
  Delete both open a confirm popup first; Delete then also
  requires typing your exact email and DELETE, archives your
  profile and login history to deleted_accounts, deletes your
  skn_profiles and login_history rows and all local data, then
  signs you out. Prince reported completing Google provider
  setup in Supabase on 2026-10-31 (Part 2 of the guide);
  verification of that provider switch is still to be
  confirmed in the dashboard.
  Note: deleting the Supabase Auth login record itself needs
  a server-side (service-role) step, which is not in browser
  code.
- SKN Report: generated from the profile, downloadable as .txt.
- Removed 2026-10-31 at Prince's request: Yumi, Scanner and
  Community, and later the Dashboard tab. They are no longer in
  the header or code.
- About / Contact, using the prototype's contacts:
  hello@sknid.app, instagram.com/sknid, twitter.com/sknid.

## What is not yet the real Base44 backend

- Accounts and profiles save in the browser
  (localStorage) only, not on a server and not across devices.
- Google sign-in is simulated. Real Google/email auth needs
  Supabase Auth.
- No pricing was shown on the prototype, so none is included.

The Base44 source exploration is now complete (no ZIP export — it is
paywalled). The real app has 21 pages, a 27-question onboarding in
9 sections, a fixed bottom nav, and SknID entities — a faithful v2
rebuild is pending a decision, so this clone remains the simplified
working version for now.

## Make it real with Supabase (next step)

A Supabase project "SKN ID" already exists (West EU, host
blyfnptcpbsqjfvlxyzh.supabase.co) with tables waitlist,
skn_profiles, contact_messages and community_posts, each with
public-insert-only Row Level Security (the community_posts table
remains in the database but is unused since Community was
removed). `index.html` already wires
profile saves to Supabase when
`window.SKN_SUPABASE_ANON_KEY` is set (via secure environment
variables, never in chat or code), and falls back to localStorage
until then. Keep the service_role key out of browser code — use
only the anon key.

## Live site

GitHub Pages is on for daristocrat/SKN-ID (main branch, root):
https://daristocrat.github.io/SKN-ID/ — every push to main
redeploys it automatically. Static site, no build command needed.

- Figma header, as it is (2026-11-02, second Figma check):
  Figma has NO conventional gradient on buttons, cards, lime
  band, tabs or avatar — everything is flat near-black
  #0A0B0A, dark card #171A17 and flat lime #C8FF38, except
  one very faint top-right olive glow (radial, peaking
  around #1B2012 / #191E11, fading into #0A0B0A). This
  build copies that glow, the flat card colour, and the
  Figma dashboard header exactly: logo left, five tabs
  centred (Home / My Skin / Recommendations / My Routine
  / Account), lime avatar circle right with the real
  user's initials. Active tab is a dark pill #2A2E2A with
  cream text, NOT lime; inactive tabs are plain muted
  text, no pill, no underline. There is deliberately NO
  Report or About tab in the header, as in Figma — Report
  is reached from My Skin, Home, Account and the footer,
  About from the footer and Account. Signed-out header
  is Figma landing style: Sign in (plain text) + Get
  started (lime pill), no tabs. Figma's Sign in is only
  a demo entry with no form, so here Sign in / Get
  started / Discover your skin all open the REAL login
  (Google OAuth + Email OTP, consent-gated) on the
  landing sign-in card, and a successful sign-in lands
  on Home with the five Figma tabs and the lime avatar.

- Figma page-by-page rebuild (2026-11-03, second Figma audit):
  Correction: the landing hero image is NOT
  photo-1620916566398 (that was a mis-identification in
  the first measurements task). The actual Figma hero is
  photo-1777450793530-99a0e7b7fc53, and it is reused for
  Recommendations product 1. Only three distinct images
  exist in the whole Figma app: that hero/serum photo,
  photo-1658752293220 (moisturiser card) and
  photo-1586806819282 (sunscreen card); My Skin, My
  Routine, Account and Quiz have no photos. This build
  uses exactly those three URLs, in the same places:
  hero arch, Recommendations left image panels with
  01/02/03 badges, and tilted thumbnails on Home.
  Views rebuilt page by page to the audit: Landing
  (hero body, brand row, How it works lime-circle
  icons, Why label + white pill, two-row footer);
  Quiz (Save & exit text link, Question X of 5, thin
  progress at (step+1)x20%, giant outline number,
  two-column layout, dark option cards with radio
  circles — steps 2–5 headings were not audited, as
  reaching them requires submitting an answer, so
  our profile fields are kept there in Figma layout,
  not invented Figma questions); Home (two-column
  greeting with real date + right-aligned subtext,
  routine-today ring card, journey week card, skin-
  today card, picked-products card with tilted
  thumbnails, lime daily-tip strip); My Skin (lime
  panel with giant outline 01 + dark inset panel,
  How your skin feels 3 cards, What this means 2x2
  grid, disclaimer); Recommendations (Less, but
  better heading, sample warning strip, Show: All 3 /
  AM routine / PM routine filters, wide cards with
  brand, price, Why it fits lime rule, Key
  ingredients, Good to know, View + Save buttons);
  My Routine (Morning 4 steps / 3 min, Evening 3
  steps / 4 min with Figma step names, lime number
  circles + circular check, amber caution card,
  weekly tracker with weekday circles, lime reminder
  strip); Account (profile card with real initials,
  skin-profile card, 3 preferences toggles, settings
  rows, danger-zone card with red Delete text only).
  Real data only — never the Figma demo name, demo
  date, demo streak or demo profile — and real
  sign-in, saving, check-off, check-in, Sign out and
  Delete stay working on top. Product brands/prices
  are the Figma sample data, with the sample warning
  shown, not verified store prices; photos are
  generic stock, not branded packshots.

- Backend + admin panel (2026-11-03): no full rewrite — the
  backend is Supabase, as before. New tables and RLS in
  `~/workspace/skn-id-backend/schema.sql` (admins,
  skn_reports, products, admin_actions, plus admin-read
  policies on skn_profiles, login_history, waitlist and
  contact_messages) and a setup guide in
  `~/workspace/skn-id-backend/README_BACKEND.md`. Run
  the SQL in Supabase SQL Editor, then insert your
  admin email, then sign in: Account shows “Open admin
  dashboard” (admins only; no Admin tab in the Figma
  header for regular users). Admin dashboard tabs:
  Overview, Users (view all profiles + login counts),
  Reports (pick a user, edit, save draft, Publish to
  push — published reports replace the generated one
  in that user's Report view), Products (name, brand,
  category, price, buying_url, image_url, description,
  why_it_fits, key_ingredients, AM/PM, active, sort
  order — active products appear in Recommendations
  and Home, with a Buy link; otherwise the Figma
  sample products are used), Messages (waitlist +
  contact), Audit (every admin action), Admins (add
  another admin by email). Extra features added:
  draft vs published report workflow, report
  versioning (new row per save, latest published
  wins), product soft-deactivate + sort order, CSV
  export for users/products, and admin audit log.
  The service-role key is never used in the browser;
  Auth-user listing/deletion stays as a Phase 2
  Edge Function, not built here.
