# Ticketing staging - L27

Questa repository contiene un'applicazione ticketing gia' verificata in
locale e in CI. Il lavoro della lezione consiste nel pubblicarla in staging e
dimostrare quale commit sta realmente servendo l'URL pubblico.

Il provider AI predefinito e' Replay: non servono chiavi API.

## Requisiti

- Node.js `>=24 <27`
- pnpm `11.5.1`
- Git e un repository GitHub personale
- account Render

## Avvio locale

```bash
corepack enable
pnpm install --frozen-lockfile
pnpm check
pnpm test
pnpm dev:replay
```

Apri:

```txt
http://127.0.0.1:3001/incident.html
```

Per eseguire i controlli browser la prima volta:

```bash
pnpm exec playwright install chromium
pnpm test:e2e
```

## File da conoscere

- `.github/workflows/quality.yml`: controlli automatici prima del deploy;
- `render.yaml`: contratto del servizio di staging;
- `server/app.js`: endpoint `/health`;
- `scripts/verify-remote.js`: verifica del commit realmente online;
- `CONSEGNA.md`: percorso dell'esercizio.

Il `Dockerfile` resta come risultato del lavoro precedente, ma in questa
lezione Render usa il runtime Node dichiarato in `render.yaml`: non esegue una
build Docker.

Quando carichi i file su GitHub, assicurati che sia presente anche la cartella
nascosta `.github`.

## Comando remoto

Dopo il deploy userai:

```bash
pnpm verify:remote -- <URL_STAGING> <COMMIT_ATTESO>
```

Un URL raggiungibile non basta: il comando deve confermare anche provider,
funzioni minime e commit servito.
