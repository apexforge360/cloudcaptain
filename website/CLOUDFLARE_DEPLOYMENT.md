# CloudCaptain Cloudflare Pages Deployment

## 1. Architecture

CloudCaptain is a static Docusaurus site deployed through a Git-connected Cloudflare Pages project:

```text
Docusaurus -> GitHub -> Cloudflare Pages -> cloudcaptain.apexforge360.com
```

Use a dedicated Cloudflare Pages project for this site only. Do not modify existing ApexForge360 Workers, Pages projects, routes, or unrelated DNS records.

## 2. Git Repository Detected

- Repository: `https://github.com/nomadicmehul/CloudCaptain.git`
- Git repository root: `/home/asif/CloudCaptain`
- Docusaurus app directory: `/home/asif/CloudCaptain/website`

## 3. Production Branch

- Production branch: `main`
- Remote default branch: `main`

## 4. Cloudflare Project Name

Preferred Cloudflare Pages project name:

```text
cloudcaptain
```

If unavailable, use:

```text
apexforge360-cloudcaptain
```

Create this as a Git-connected Cloudflare Pages project, not a Direct Upload project.

## 5. Root Directory

Because `package.json` and `docusaurus.config.ts` are inside `website/` relative to the Git repository root, configure Cloudflare Pages with:

```text
website
```

## 6. Build Command

```bash
npm run build
```

## 7. Build Output Directory

```text
build
```

## 8. Node Version

Use Node.js 22 for Cloudflare builds.

The project includes:

```text
.nvmrc -> 22
```

Cloudflare Pages can also be configured with:

```text
NODE_VERSION=22
```

The package requires Node `>=20.0`.

## 9. Custom Domain

Production hostname:

```text
cloudcaptain.apexforge360.com
```

After the first successful Cloudflare Pages deployment, add the custom domain in the Cloudflare dashboard:

```text
Workers & Pages -> cloudcaptain -> Custom domains -> Set up a domain
```

Only configure `cloudcaptain.apexforge360.com`. Do not change `apexforge360.com`, `www.apexforge360.com`, existing Worker routes, or unrelated DNS records.

## 10. Future Deployment Workflow

```text
Edit documentation in VS Code
        ->
test locally
        ->
npm run build
        ->
git commit
        ->
git push
        ->
Cloudflare automatically builds
        ->
cloudcaptain.apexforge360.com updates
```

## 11. Rollback Procedure

Use Cloudflare Pages deployment history to roll back to a previously successful deployment.

For source-level rollback:

```bash
git log --oneline
git revert <commit-sha>
git push origin main
```

Do not force push unless there is a separately reviewed recovery plan.

## 12. Troubleshooting

- If Cloudflare uses the wrong project root, confirm the Pages root directory is `website`.
- If Node version errors appear, confirm `.nvmrc` is committed and set `NODE_VERSION=22` in Cloudflare Pages environment variables.
- If dependencies fail to install, use `npm ci` and confirm `website/package-lock.json` is committed.
- If routing fails on direct URLs, confirm Docusaurus has `url: 'https://cloudcaptain.apexforge360.com'` and `baseUrl: '/'`.
- If assets fail to load, check that image references match files in `website/static/img/` with exact case-sensitive filenames.
- If a deployment updates the wrong ApexForge360 property, stop and verify the Pages project is the dedicated `cloudcaptain` project before changing any Cloudflare settings.
