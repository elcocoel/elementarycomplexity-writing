# Writing publication rules

Read `README.md` before publishing. The canonical deployment strategy lives in the
website repository’s `docs/PRODUCTION.md`.

- This repository owns Markdown posts and their media; the website is a derivative.
- Production publication is manual. Never add a push-triggered deployment workflow,
  Vercel deploy hook, or `VERCEL_DEPLOY_HOOK` secret.
- Review, commit, and push writing to `main`, then pin its full commit SHA in the
  website’s `writing.lock.json`. Commit and push the website before deploying.
- Deploy only through `node scripts/deploy-site.mjs ec` from the website repository,
  after its `--check` preflight. A Git push alone does not publish an article.
- Verify the live article and writing index after an authorized deployment.
