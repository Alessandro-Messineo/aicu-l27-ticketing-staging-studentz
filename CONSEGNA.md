# Esercizio L27 - Pubblicare uno staging verificabile

## Obiettivo

Pubblica questa applicazione su Render e raccogli prove sufficienti per
rispondere a entrambe le domande:

```txt
Il servizio e' disponibile?
L'URL pubblico sta servendo il commit che mi aspetto?
```

Non devi sviluppare una nuova feature e non devi collegare un provider AI
reale.

## Prima di iniziare

1. Crea un repository GitHub personale a partire da questa cartella.
2. Verifica che GitHub contenga anche `.github/workflows/quality.yml`.
3. Attendi una pipeline `Quality` verde sul branch `main`.
4. Assicurati di poter accedere a Render.

## 1. Leggi il contratto

Apri `render.yaml` e collega ogni campo a una responsabilita':

- ambiente di esecuzione;
- installazione delle dipendenze;
- avvio del server;
- momento in cui puo' iniziare un deploy;
- endpoint usato per decidere se l'app e' pronta;
- provider AI attivo.

Non modificare campi che non sai collegare a un requisito osservabile.

In questo esercizio il servizio usa il runtime Node gestito da Render. Il
`Dockerfile` presente nella codebase non viene usato dal Blueprint.

## 2. Crea lo staging

Su Render crea un nuovo Blueprint dal tuo repository GitHub. Usa il branch
`main` e lascia che Render legga `render.yaml`.

Segui il primo deploy distinguendo almeno queste fasi:

```txt
commit GitHub
-> pipeline Quality
-> build Render
-> avvio del servizio
-> controllo di salute
-> release Live
```

Se una fase fallisce, fermati su quella evidenza prima di cambiare file.

## 3. Verifica il servizio

Apri nel browser:

```txt
<URL_STAGING>/health
<URL_STAGING>/incident.html
```

`/health` deve mostrare:

```txt
status = ok
provider = replay
release = commit pubblicato
```

Recupera il commit locale:

```bash
git rev-parse HEAD
```

Poi esegui:

```bash
pnpm verify:remote -- <URL_STAGING> <COMMIT_ATTESO>
```

Prova anche un commit volutamente diverso e osserva perche' il controllo
diventa rosso.

## 4. Conserva la baseline

Prima di terminare annota:

- URL dello staging;
- commit confermato dal controllo remoto;
- link alla pipeline verde;
- stato `Live` del deploy Render.

Continuerai a usare lo stesso repository e lo stesso servizio nel laboratorio
successivo.

## Criteri di accettazione

Il lavoro e' completo quando:

- `main` ha una pipeline verde;
- Render mostra una release `Live`;
- `/health` risponde con `status: ok` e `provider: replay`;
- `/incident.html` e' utilizzabile;
- `release` coincide con il commit atteso;
- `pnpm verify:remote -- <URL_STAGING> <COMMIT_ATTESO>` termina in verde.

## Fuori scope

- produzione reale e domini personalizzati;
- Mistral o altre API esterne;
- database persistente o gestito;
- modifiche alla feature AI;
- ottimizzazioni del piano Render.
