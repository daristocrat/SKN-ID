# SKN ID — (website)

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
- SKN Report: generated from the profile, downloadable as .txt.
- Removed 2026-10-31 at Prince's request: Yumi, Scanner and
  Community. They are no longer in the header, dashboard or code.
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

## Deploy to Vercel (after GitHub)

Push this folder to GitHub, then in Vercel: New Project -> Import
repo -> Deploy. Static site, no build command needed.
