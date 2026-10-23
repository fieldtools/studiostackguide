# StudioStackGuide ops log

## Expected state
- Repo: https://github.com/fieldtools/studiostackguide (public, branch main)
- GitHub Pages: build_type `workflow` (.github/workflows/pages.yml, which runs build.py and deploys dist/)
- Custom domain (cname): studiostackguide.com (dist/CNAME is written by build.py)
- HTTPS: certificate pending as of 2026-10-22 ~12:59 CDT; `https_enforced` = false. Enforce once the cert is issued:
  `gh api -X PUT repos/fieldtools/studiostackguide/pages -F https_enforced=true`
- DNS at Cloudflare (all DNS-only / grey cloud):
  - A @ 185.199.108.153
  - A @ 185.199.109.153
  - A @ 185.199.110.153
  - A @ 185.199.111.153
  - CNAME www fieldtools.github.io
- Cloudflare Web Analytics token: 65de38c8090f4a059cfa398886fcd1dd (in build.py layout)

## Log (America/Chicago)
- 2026-10-22 ~12:45: built v1 locally from the tradestackguide template (7 tools, 3 guides, 4 studio-type pages).
- 2026-10-22 12:49-12:50: briefly switched to studiosoftwarehub.com, then reverted to studiostackguide.com. Plain links now use rel="nofollow"; affiliate links use rel="sponsored nofollow".
- 2026-10-22 12:52: created the public repo fieldtools/studiostackguide and pushed main. Pages enabled (workflow); cname set to studiostackguide.com. Run 39826403225 succeeded.
- 2026-10-22 12:53: set the Cloudflare analytics token, pushed. Run 39826593352 succeeded.
- 2026-10-22 ~12:58: DNS resolves publicly (Cloudflare NS). HTTP 200 from GitHub Pages for studiostackguide.com. HTTPS cert not yet issued (GitHub serves *.github.io); HTTPS not enforced.
- 2026-10-22 ~13:20: filled belt/attendance/booking fields for Martialytics (martialytics.com/features), Gymdesk (gymdesk.com homepage FAQ) and MASS belt tracking (mass-system.com homepage). Other unknowns left as unknown (not stated on vendor pages).
- 2026-10-22 ~13:49 [bean] Contact email jacob@studiostackguide.com on About (#contact) and in footer; footer cross-link to TradeStackGuide (plain link); 8 FAQ entries added (4 per page on 3 pages); corrected stale martial-arts belt-tracking FAQ answer to match tools.json; verified data/tools.json vs a3e1257^: only the intended Martialytics/Gymdesk/MASS field changes, no escape-related value changes. FAQPage JSON-LD validated; check_links passed.
- 2026-10-22 ~14:07 [bean] GitHub Pages certificate approved (studiostackguide.com + www, expires 2027-01-20); https://studiostackguide.com/ returns 200 with a valid cert. Set https_enforced=true via Pages API (confirmed true). The box can't reach port 80, so the http-to-https redirect couldn't be checked directly from here.
- 2026-10-22 ~14:30 [bean] Added 4 pages (martialytics-vs-gymdesk, gymdesk-vs-zen-planner, zen-planner-vs-mindbody, martial-arts-software-pricing; backlog rows 5/7/8/20 marked done; row 4 martialytics-vs-kicksite left for the nightly routine). Re-fetched vendor pricing pages this run (martialytics, gymdesk, zenplanner, mindbody, kicksite, sparkmembership, mass ToS); no price changes. Added /membership-revenue-calculator/ (client-side JS, no benchmarks) and /software-buying-checklist/ (printable, mailto signup); nav links Calculator + Checklist in build.py.
- 2026-10-22 ~15:10 [bean] Verified live: 4 new pages, calculator, checklist return 200; run 39837669088 succeeded (8cfcb40).
- 2026-10-22 ~14:45 [bean] Replaced mailto checklist signup on /software-buying-checklist/ with Buttondown embed form (stackguide newsletter, hidden tag=studiostackguide, labeled required email, 'Get updates'); source edited in data/pages/software-buying-checklist.json; FAQ email mention removed. build + check_links passed.
- 2026-10-22 ~14:58: [bean] Pinned all workflow actions to full commit SHAs with tag comments (checkout v4.4.0, setup-python v5.6.0, configure-pages v5.0.0, upload-pages-artifact v3.0.1, deploy-pages v4.0.5).
- 2026-10-22 ~15:30 [bean] Added IndexNow: key file /1c95715bb5595663d833d655477bd8cd.txt (static/indexnow-key.txt, copied by build.py); scripts/indexnow_ping.py diffs built sitemap vs live one (fetched pre-deploy) and POSTs new/changed URLs to api.indexnow.org after deploy-pages (plain run steps, never fails deploy).
- 2026-10-22 ~15:35 [bean] IndexNow: treat missing live key file as first run; added 'all' mode. Ran initial full submission locally (first deploy diff was empty since sitemap pre-existed).
- 2026-10-23 ~02:15 [bean] Added /martialytics-vs-kicksite/ (backlog #4). Re-verified Martialytics and Kicksite pricing (no price changes); Kicksite data filled from vendor pages: 30 days free, Basys rates ($29/mo + 2.9% + $0.25), kiosk check-in, member-portal class registration; corrected stale Kicksite trial/processing lines on best-bjj-gym-software and martial-arts-software-pricing. last_checked -> 2026-10-23. No settings/DNS/workflow/Pages changes.
- 2026-10-23 ~06:40 CDT [bean] IndexNow check: existing key file live (200, body matches); ran `python3 scripts/indexnow_ping.py all` → api.indexnow.org HTTP 200. No new key generated (existing setup already covers this).
- 2026-10-23 ~08:30 CDT Merged themed-images into main (approved by Jacob): themed Pexels WebP header photos on all software pages incl. new nightly pages, homepage hero banner, photo credits on /about/. build + check_links clean. IndexNow `all` ping after deploy.
- 2026-10-23 ~09:00 CDT Bumped Pages deploy workflow actions off Node 20 (approved by Jacob): checkout v4.4.0→v7.0.1, setup-python v5.6.0→v7.1.0, configure-pages v5.0.0→v6.0.0, upload-pages-artifact v3.0.1→v5.0.0, deploy-pages v4.0.5→v5.0.1 (SHA-pinned).
- 2026-10-23 ~09:35 CDT Merged calc-checklist-photos into main (approved by Jacob): dedicated Pexels header photos for the calculator and checklist pages (credits in docs/IMAGE-CREDITS.md + /about/). build + check_links clean. IndexNow `all` ping after deploy.
- 2026-10-23 ~09:36 CDT Added /disclosure/ affiliate disclosure page (approved by Jacob; Martialytics/Zen Planner applications pending, no affiliate links live), linked from footer, trust bar and /about/, plus a short commission line on tool, studio, comparison and guide pages. build + check_links clean. IndexNow `all` ping after deploy.
- 2026-10-23 ~12:02 CDT Published /tools/zen-planner/ page refresh (approved by Jacob): facts re-verified on vendor pricing page, own Pexels header photo (3912956), affiliate status pending (plain link). build + check_links clean. IndexNow `all` ping after deploy.
