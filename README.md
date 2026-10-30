# SKN ID — Working Clone (website)

A working, single-file clone of the SKN ID app, built from its public
Base44 prototype. Open `index.html` in a browser — no build step.

## What actually works in this clone

- Sign-in screen matching the prototype: "Your skin is unique. Your
  identity should be too.", Continue with Google / Continue with
  Email, gated by the required email-consent checkbox.
- Account creation (local, in this browser) and sign-out.
- 5-step SKN profile: skin type, sensitivities, goals, values,
  environment. Edits update the dashboard and report instantly.
- Dashboard with a SKN ID card and quick actions.
- Yumi: chat that tailors answers to the saved profile (rule-based
  guidance in this clone, not a live LLM).
- Scanner: sample products scored against the saved profile, plus a
  custom ingredient checker.
- Community feed: sample posts plus your own posts and likes, saved
  locally.
- SKN Report: generated from the profile, downloadable as .txt.
- About / Contact, using the prototype's contacts:
  hello@sknid.app, instagram.com/sknid, twitter.com/sknid.

## What is not yet the real Base44 backend

- Accounts, profiles, posts and messages save in the browser
  (localStorage) only, not on a server and not across devices.
- Google sign-in is simulated. Real Google/email auth needs
  Supabase Auth.
- Yumi is not a live AI model, and the scanner uses a small sample
  product list, not a live product/ingredient database.
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
public-insert-only Row Level Security. `index.html` already wires
profile saves and community posts to Supabase when
`window.SKN_SUPABASE_ANON_KEY` is set (via secure environment
variables, never in chat or code), and falls back to localStorage
until then. Keep the service_role key out of browser code — use
only the anon key.

## Deploy to Vercel (after GitHub)

Push this folder to GitHub, then in Vercel: New Project -> Import
repo -> Deploy. Static site, no build command needed.
