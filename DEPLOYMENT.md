# Deployment guide

## Vercel (recommended)

1. Sign in to Vercel and choose **Add New → Project**.
2. Import `Sushant-Nemade/oss-atlas` from GitHub.
3. Keep the detected Next.js framework and default build settings.
4. Add `GITHUB_TOKEN` as a server-side environment variable (optional but recommended for a public deployment). Use a fine-grained token with read-only public profile/repository access only.
5. Deploy. Vercel will build on each push to `main` and create preview deployments for pull requests.

No database, storage, or other environment variables are required. Without a token, the app still works within GitHub's unauthenticated API quota.

## Docker

The included Dockerfile uses Next.js standalone output and a non-root runtime user.

```bash
docker build -t oss-atlas .
docker run --rm -p 3000:3000 -e GITHUB_TOKEN=your_read_only_token oss-atlas
```

Open `http://localhost:3000`.

## Any Node host

- Node.js 20 or newer
- Install: `npm install`
- Build: `npm run build`
- Start: `npm run start`
- Port: `3000` by default
- Optional server environment variable: `GITHUB_TOKEN`

## Operational notes

- GitHub unauthenticated REST API requests are typically limited to 60/hour per IP; authenticated requests have a higher quota.
- The API caches results for five minutes and allows stale responses for another ten minutes.
- Never expose the token through `NEXT_PUBLIC_GITHUB_TOKEN`, client-side code, or logs.
- The service reads public profile and repository information only and does not persist user scans.
- GitHub API changes or rate limits can temporarily affect scan availability; the UI displays a useful error rather than inventing data.

## Release checklist

- [ ] CI passes typecheck, lint, tests, and production build.
- [ ] Verify a normal public profile, a user with no public repositories, an unknown username, and rate-limit behavior.
- [ ] Confirm token is configured only as a server-side secret.
- [ ] Check keyboard navigation and mobile layout.
- [ ] Publish a tagged release and update the changelog.
