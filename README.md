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
