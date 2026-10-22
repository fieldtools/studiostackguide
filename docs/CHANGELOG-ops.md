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
