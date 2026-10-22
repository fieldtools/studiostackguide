# Prepared, NOT run. Needs Jacob's approval.
cd /workspace/sites/studiostackguide
gh repo create fieldtools/studiosoftwarehub --public --source=. --remote=origin
git push -u origin main
gh api -X POST repos/fieldtools/studiosoftwarehub/pages -f build_type=workflow
gh api -X PUT repos/fieldtools/studiosoftwarehub/pages -f cname=studiosoftwarehub.com
gh workflow run pages.yml -R fieldtools/studiosoftwarehub   # optional; the push already triggers it
gh run watch -R fieldtools/studiosoftwarehub
# After DNS resolves and the certificate is issued:
gh api -X PUT repos/fieldtools/studiosoftwarehub/pages -F https_enforced=true
# Cloudflare DNS (DNS only / grey cloud while the cert is issued):
#   A @ 185.199.108.153, .109.153, .110.153, .111.153 ; CNAME www -> fieldtools.github.io
