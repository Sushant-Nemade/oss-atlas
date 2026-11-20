# OSS Atlas 🧭

**Your GitHub is a story. Make it undeniable.** OSS Atlas is an open-source intelligence cockpit that turns any public GitHub profile into a practical portfolio audit: transparent health score, repository explorer, language footprint, prioritized fixes, and downloadable Markdown report.

## Features
- Portfolio hygiene score (0–100) based on descriptions, licenses, topics, and recent activity.
- Repository explorer with search, stars, forks, language, license, and update dates.
- Actionable findings for missing descriptions/licenses/topics and quiet projects.
- Language footprint, severity filters, and downloadable Markdown report.
- No sign-in, database, cookies, or analytics. Public GitHub API only.
- Typed API route, five-minute cache, input validation, tests, CI, and MIT license.

## Quick start
Requires Node.js 20+.

```bash
git clone https://github.com/Sushant-Nemade/oss-atlas.git
cd oss-atlas
npm install
cp .env.example .env.local
npm run dev
```
Open http://localhost:3000 and scan any public GitHub username.

## Rate limits
Unauthenticated GitHub REST API requests are typically limited to 60/hour per IP. For deployment, create a fine-grained token with read-only access to public profile/repository data and set `GITHUB_TOKEN` in your host environment. Never use a `NEXT_PUBLIC_` variable for secrets or commit a token.

## Quality checks
```bash
npm run typecheck
npm run lint
npm test
npm run build
```

## Scoring model
The score is the equally weighted average of four ratios across non-fork, non-archived repositories: has a description, has a license, has one or more topics, and was pushed to within 180 days. This is an opinionated repository hygiene signal—not a measure of engineering skill, code quality, popularity, or employability. Quiet projects may be complete; archive them or explain their status. Public code without a license is not automatically open source.

## Architecture
Next.js App Router UI → `/api/atlas/[username]` → GitHub public profile and repositories API → pure TypeScript analyzer → cached JSON. The app is stateless and stores no profile data.

## Roadmap
- [ ] Optional side-by-side profile comparison.
- [ ] Contribution activity timeline with API coverage notes.
- [ ] Configurable scoring weights and custom audit rules.
- [ ] Release container images and deployment recipes.
- [ ] Accessibility and localization improvements.

Issues and pull requests are welcome. Open an issue before large changes to align on scope.

## Privacy & security
Only public GitHub endpoints are requested. Optional token is server-side only. No tracking or database. Report vulnerabilities privately using GitHub's Security Advisory feature.

## License
MIT. See [LICENSE](LICENSE).
