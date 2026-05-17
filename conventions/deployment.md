# Deployment Convention — Opita Code Ecosystem

> **Regla de oro**: Todo deploy a producción pasa por CI. Manual deploy = solo `dev` stage.

## Dominios y Pipelines

| Dominio | CloudFront | S3 Bucket | Pipeline | Repo |
|---------|------------|-----------|----------|------|
| `vibe.opitacode.com` | `EONGVOV3BDAVI` | `vibe-landing-728741135483` | 3 GH Actions | `vibe-studio` |
| `opitacode.com` | `EO2EU8EVU2RVR` | `opitacode.com` | GH Actions | `opitacode-web` |
| `dev.opitacode.com` | `EHQLGHNKD091K` | `dev.opitacode.com` | Manual only | `vibe-studio` |
| `developer.opitacode.com` | `E297ZMSJM7FP9V` | `developer.opitacode.com` | Manual | `opita-developer-web` |
| `cuenta.opitacode.com` | `E1072DTN2FPISQ` | `opita-account-ui-prod` | `deploy.ps1` | `opita-os` |
| `api.opitacode.com` | `E1KO6ZMHUX4HF9` | SST Router | GH Actions | `vibe-studio` |
| `go.opitacode.com` | `E3K1TGT72GTOSV` | SST Lambda | SST deploy | `opita-links` |

## Vibe Studio — 4 Deploy Targets

```
vibe-studio repo
├── deploy-backend.yml    → SST Lambdas + DynamoDB (api.opitacode.com)
│   └── Triggers: sst.config.ts, packages/**
├── deploy-landing.yml    → Static HTML → S3 root (vibe.opitacode.com/)
│   └── Triggers: landing/**
├── deploy-web-app.yml    → Vite build → S3 /app/ (vibe.opitacode.com/app/)
│   └── Triggers: src/**, index.html, vite.config.*, package.json
└── build-tauri.yml       → Desktop binaries → GitHub Releases
    └── Triggers: version tags (v*)
```

## Prohibiciones (Anti-Patterns)

1. **NUNCA hacer `npx sst deploy --stage prod` desde terminal local.** Las env vars del `.env` local no están sincronizadas con GitHub Secrets. Usar CI.
2. **NUNCA agregar `dev.opitacode.com` al CORS de Lambdas de producción.** Staging tiene su propio stack.
3. **NUNCA hacer deploy de frontend sin build mode correcto.** Prod = `npm run build`. Staging = `npx vite build --mode staging`.
4. **NUNCA hacer `aws s3 sync dist/ s3://vibe-landing-728741135483/` sin `--exclude "app/*"`.** Esto borraría toda la web app.

## Deploy Manual (Solo Dev)

Solo se permite deploy manual al stage `dev`:

```bash
# Backend
npx sst deploy --stage dev

# Frontend
npx vite build --mode staging
aws s3 sync dist/ s3://dev.opitacode.com/app/ --delete
aws cloudfront create-invalidation --distribution-id EHQLGHNKD091K --paths "/app/*"
```

## Secrets

Todos los secrets de producción están en **GitHub Secrets** del repo `opita-vibe-studio`.
Para agregar o actualizar un secret:

```bash
echo "valor" | gh secret set NOMBRE_SECRET -R Opita-Code/opita-vibe-studio
```

| Secret | Usado por |
|--------|-----------|
| `JWT_SECRET` | CoreAPI, ChatStream, Storage |
| `AI_STUDIO_GOOGLE` | ChatStream |
| `WOMPI_PUBLIC_KEY` | BillingAPI |
| `WOMPI_WEBHOOK_SECRET` | BillingAPI |
| `WOMPI_INTEGRITY_SECRET` | BillingAPI |
| `OPITA_LINKS_API_KEY` | CoreAPI |
| `SES_FROM_EMAIL` | CoreAPI |
| `AWS_ACCESS_KEY_ID` | All workflows |
| `AWS_SECRET_ACCESS_KEY` | All workflows |

## Versioning (Desktop Releases)

1. Bump version en `package.json`, `src-tauri/tauri.conf.json`, `src-tauri/Cargo.toml`
2. Commit: `chore(release): bump to vX.Y.Z`
3. Tag: `git tag vX.Y.Z && git push origin vX.Y.Z`
4. GitHub Actions compila binarios para Windows, macOS, Linux automáticamente
