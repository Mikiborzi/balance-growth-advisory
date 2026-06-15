# HANDOVER.md — passaggio di consegne

Scopo: rendere possibile, in qualsiasi momento, consegnare il sito a **Fabio Gino
Merli** in modo rapido e pulito. Tieni questo file aggiornato.

---

## 1. Stato attuale della proprietà

| Risorsa | Dove vive oggi | Intestatario |
|---|---|---|
| Dominio `balanceandgrowth.com` | Cloudflare Registrar | **Michele Borzatta** |
| Hosting (Worker `balanceandgrowth`) | Cloudflare Workers | **Michele Borzatta** |
| Email `info@balanceandgrowth.com` | Cloudflare Email Routing | **Michele Borzatta** (indirizzo di inoltro: da verificare nel pannello) |
| Repo del progetto | GitHub: https://github.com/Mikiborzi/balance-growth-advisory | Michele (verificare se pubblico o privato) |
| Backend form / dati contatti | _(non ancora attivato)_ | — |

Nota: l'account Cloudflare è di Michele, socio storico di Fabio. Va bene per la
fase attuale. Tutto ciò che segue serve a poter cambiare questo stato in fretta.

## 2. Credenziali e accessi (da custodire a parte, NON in questo file)

- [ ] Account Cloudflare (email `michele.borzatta@gmail.com` + 2FA)
- [ ] Accesso al dominio (Cloudflare Registrar)
- [ ] Cloudflare Email Routing — indirizzo di destinazione per `info@balanceandgrowth.com`
- [ ] Repo GitHub (trasferire ownership a Fabio o invitarlo come collaboratore)
- [ ] Account del servizio form (quando attivato)

## 3. Come sganciare il sito a Fabio (procedura)

Tutto il sito vive in **questa cartella**: è il motivo per cui lo sgancio è veloce.

1. **Repo** → consegna questa cartella a Fabio (o trasferisci il repo GitHub).
2. **Hosting** → Fabio fa `npx wrangler login` col **suo** account Cloudflare e
   lancia `npx wrangler deploy`: il sito rinasce identico sul suo account.
3. **Dominio** → trasferisci `balanceandgrowth.com` al Cloudflare di Fabio
   (transfer/push del dominio), poi ricollega il dominio al suo Worker.
4. **Email** → riconfigurate Cloudflare Email Routing su `info@balanceandgrowth.com`
   verso la casella di Fabio (o una nuova casella intestata a lui).
5. **Form / dati** → riconfigura il backend del form sull'account di Fabio, così
   i contatti dei clienti diventano suoi.

Fatto: nessun residuo del progetto resta legato all'infrastruttura di Michele.

## 4. Struttura del sito (as-built al 2026-06-15)

```
public/
├── index.html          ← homepage (hero, 5 servizi, clienti, brand, team, formazione, partner, contatto)
├── fabio.html          ← profilo Fabio Gino Merli (fondatore)
├── michele.html        ← profilo Michele Borzatta (partner)
└── Img/
    ├── Foto Fabio Gino Merli.png    (416 KB)
    └── FOTO Michele Borzatta.png    (3 MB — da ottimizzare)
```

Per la documentazione tecnica completa (design system, link esterni, criticità):
vedi `TECH-SPEC.md`.

## 5. Stato del deploy (aggiornato 2026-06-15)

- **Worker**: `balanceandgrowth` su account Cloudflare di Michele Borzatta
- **Account ID**: `420533bd2631c03f53302979bcf16a8c`
- **Dominio principale**: `balanceandgrowth.com` → custom domain sul Worker ✓
- **Sottodominio**: `www.balanceandgrowth.com` → custom domain sul Worker ✓
- **Email**: `info@balanceandgrowth.com` via Cloudflare Email Routing ✓
- **workers.dev**: disabilitato (`"workers_dev": false` in `wrangler.jsonc`)
- **compatibility_date**: `2026-06-13`
- **Configurazione**: `wrangler.jsonc` nella root del progetto
- **Ultima versione deployata**: 2026-06-15 — Version ID: `ffa6a802-f636-4fa7-9818-0720ebbf55c0`

Per pubblicare modifiche: `npx wrangler deploy` (dalla cartella del progetto,
dopo `npx wrangler login` se necessario).

---

## 6. Per Fabio — aggiornare i testi (senza essere tecnico)

Il modo semplice:
1. Apri questa cartella con **Claude Code** (o l'app desktop di Claude).
2. Chiedi a parole, in italiano: «cambia il titolo della sezione X in…»,
   «aggiorna il mio numero di telefono», «aggiungi un servizio…».
3. Quando sei soddisfatto, pubblica con: `npx wrangler deploy`.

In alternativa, i testi sono dentro `public/index.html`, `public/fabio.html` e
`public/michele.html`: si possono modificare a mano e ripubblicare con lo stesso
comando.
