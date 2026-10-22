# Prepared, NOT run. Needs Jacob's approval.
cd /workspace/sites/studiostackguide
gh repo create fieldtools/studiostackguide --public --source=. --remote=origin
git push -u origin main
gh api -X POST repos/fieldtools/studiostackguide/pages -f build_type=workflow
gh api -X PUT repos/fieldtools/studiostackguide/pages -f cname=studiostackguide.com
gh workflow run pages.yml -R fieldtools/studiostackguide   # optional; the push already triggers it
gh run watch -R fieldtools/studiostackguide
# After DNS resolves and the certificate is issued:
gh api -X PUT repos/fieldtools/studiostackguide/pages -F https_enforced=true
# Cloudflare DNS (DNS only / grey cloud while the cert is issued):
#   A @ 185.199.108.153, .109.153, .110.153, .111.153 ; CNAME www -> fieldtools.github.io
