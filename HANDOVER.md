# HANDOVER.md — passaggio di consegne

Scopo: rendere possibile, in qualsiasi momento, consegnare il sito a **Fabio Gino
Merli** in modo rapido e pulito. Tieni questo file aggiornato.

---

## 1. Stato attuale della proprietà

| Risorsa | Dove vive oggi | Intestatario |
|---|---|---|
| Dominio `balanceandgrowth.com` | Cloudflare Registrar | **Michele Borzatta** |
| Hosting (Worker `balanceandgrowth`) | Cloudflare Workers | **Michele Borzatta** |
| Repo del progetto | _(da definire: locale / GitHub)_ | Michele |
| Backend form / dati contatti | _(non ancora attivato)_ | — |
| Email contatti pubblicata sul sito | ceobalanceadvisory@protonmail.com | _(verificare)_ |

Nota: l'account Cloudflare è di Michele, socio storico di Fabio. Va bene per la
fase attuale. Tutto ciò che segue serve a poter cambiare questo stato in fretta.

## 2. Credenziali e accessi (da custodire a parte, NON in questo file)

- [ ] Account Cloudflare (email + 2FA)
- [ ] Accesso al dominio (Cloudflare Registrar)
- [ ] Eventuale repo GitHub (owner + accesso)
- [ ] Account del servizio form (quando attivato)
- [ ] Casella email dei contatti

## 3. Come sganciare il sito a Fabio (procedura)

Tutto il sito vive in **questa cartella**: è il motivo per cui lo sgancio è veloce.

1. **Repo** → consegna questa cartella a Fabio (o trasferisci il repo GitHub).
2. **Hosting** → Fabio fa `npx wrangler login` col **suo** account Cloudflare e
   lancia `npx wrangler deploy`: il sito rinasce identico sul suo account.
3. **Dominio** → trasferisci `balanceandgrowth.com` al Cloudflare di Fabio
   (transfer/push del dominio), poi ricollega il dominio al suo Worker.
4. **Form / dati** → riconfigura il backend del form sull'account di Fabio, così
   i contatti dei clienti diventano suoi.
5. **Email** → se serve, sposta i contatti su una sua casella / dominio.

Fatto: nessun residuo del progetto resta legato all'infrastruttura di Michele.

## 4. Stato del deploy (aggiornato 2026-06-13)

- **Worker**: `balanceandgrowth` su account Cloudflare di Michele Borzatta
- **Dominio principale**: `balanceandgrowth.com` → custom domain sul Worker ✓
- **Sottodominio**: `www.balanceandgrowth.com` → custom domain sul Worker ✓
- **workers.dev**: disabilitato (`"workers_dev": false` in `wrangler.jsonc`)
- **Configurazione**: `wrangler.jsonc` nella root del progetto
- **Ultima versione deployata**: `89794c28-d0da-4ba5-92c1-38056e583aef`

Per pubblicare modifiche: `npx wrangler deploy` (dalla cartella del progetto,
dopo `npx wrangler login` se necessario).

---

## 5. Per Fabio — aggiornare i testi (senza essere tecnico)

Il modo semplice:
1. Apri questa cartella con **Claude Code** (o l'app desktop di Claude).
2. Chiedi a parole, in italiano: «cambia il titolo della sezione X in…»,
   «aggiorna il mio numero di telefono», «aggiungi un servizio…».
3. Quando sei soddisfatto, pubblica con: `npx wrangler deploy`.

In alternativa, i testi sono tutti dentro `public/index.html`: si possono
modificare a mano e ripubblicare con lo stesso comando.
