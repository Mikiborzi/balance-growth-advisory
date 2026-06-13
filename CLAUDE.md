# CLAUDE.md — istruzioni di progetto

> Leggi questo file prima di toccare qualsiasi cosa. Descrive cos'è il progetto,
> come è fatto, cosa puoi e non puoi fare.

## Cos'è

Sito vetrina di **Balance & Growth Advisory**, lo studio di consulenza di
**Fabio Gino Merli** (CFO e Direttore Generale, 25+ anni). Il sito serve a
**promuovere le sue attività di consulenza** rivolte alle PMI italiane.

Il sito è gestito attualmente da Michele Borzatta (socio storico di Fabio).
Va tenuto **indipendente e portabile**: deve poter essere consegnato a Fabio in
qualsiasi momento senza dipendere da altre infrastrutture. Vedi `HANDOVER.md`.

## Stack & architettura (semplice di proposito)

- **Un solo file**: `public/index.html`. HTML + CSS + un po' di JS, tutto inline.
- **Nessun build step**, nessun framework, nessun backend.
- **Hosting**: Cloudflare Workers (static assets). Worker name: `balanceandgrowth`.
- **Dominio**: balanceandgrowth.com (collegato al Worker su Cloudflare).
- **Deploy**: `npx wrangler deploy` dalla cartella del progetto.

Mantieni questa semplicità. Niente dipendenze o strumenti nuovi senza una ragione
reale: ogni dipendenza è un nodo in più da sciogliere il giorno della consegna.

## Sistema visivo (non cambiarlo senza accordo)

- **Concetto-firma**: la "&" come *fulcro* tra Balance (struttura) e Growth
  (crescita). È l'elemento identitario, va preservato.
- **Palette** (variabili CSS in `:root`): petrolio profondo `--ink:#11302E`,
  carta calda `--paper:#F4F1E9`, ottone `--brass:#B07D2B`, verde misurato
  `--green:#2E6B47`.
- **Font**: Fraunces (titoli, serif), Archivo (testo), JetBrains Mono
  (etichette, numeri, dati — richiama precisione/audit).
- **Tono**: sobrio, premium, autorevole ma con calore. Mai gergo gonfio.
- **Tesi del sito**: «Prima l'equilibrio. Poi la crescita.»
- Rispetta `prefers-reduced-motion`. Non usare `localStorage`/`sessionStorage`.

## Fatti su Fabio (NON inventare nulla oltre a questi)

- 25+ anni come CFO e Direttore Generale, gruppi nazionali e multinazionali,
  manifatturiero e servizi. Laurea in Economia e Commercio (Torino).
- Percorso: Adecco Italia Holding (Dir. Amm. e Finanza), Fitness First Italia
  (Finance Manager), Gruppo Lattonedil (CFO, 10 società, team 38 persone,
  membro OdV 231), Angelo Cappellini & C. (Direttore Generale).
- Servizi: Diagnosi e struttura · Controllo e governo (controllo di gestione
  finanziario e patrimoniale) · Direzione strategica (CFO/CEO Fractional).
- Formazione: corso "Business Up" sul business plan (7 moduli).
- Partner: DSC Solutions (energia/sostenibilità), AI Academy (Starting Work).
- Contatti: ceobalanceadvisory@protonmail.com · +39 331 680 5428.

**Regola ferma**: niente risultati, numeri o testimonianze di clienti finché non
li fornisce Fabio. Non fabbricare prove sociali.

## Quando aggiungi un FORM (raccolta dati)

Un sito statico non raccoglie dati da solo. Due strade pulite:
1. **Servizio gestito** (Web3Forms / Formspree): rapido, le richieste arrivano
   via email. Buono per partire.
2. **Cloudflare-native**: un Worker che riceve il POST e salva su D1/KV o invia
   via email. I dati restano nell'ecosistema Cloudflare.

In ottica handover: l'account che raccoglie i dati dei clienti dovrebbe essere
**di Fabio**, non legato ad altre infrastrutture personali di Michele.

## Pubblicare

```bash
npx wrangler login      # prima volta (account Cloudflare di Michele)
npx wrangler deploy
```

## Stato del lavoro

- ✅ Struttura tecnica e organizzativa (questa cartella).
- ✅ Repo GitHub: https://github.com/Mikiborzi/balance-growth-advisory (pubblico).
- ✅ Deploy su Cloudflare Workers (Worker: `balanceandgrowth`, account Michele).
  - `balanceandgrowth.com` e `www.balanceandgrowth.com` configurati come custom domain.
  - `workers_dev: false` nel `wrangler.jsonc`.
  - Ultima versione: `89794c28` (2026-06-13).
- ⬜ **Prossima fase**: ricostruire i contenuti in forma più professionale —
  da fare insieme a Michele. Fino ad allora, modifiche solo se concordate.
