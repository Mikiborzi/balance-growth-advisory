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

- **Tre file HTML**: `public/index.html` (homepage), `public/fabio.html` (profilo
  Fondatore), `public/michele.html` (profilo Partner). HTML + CSS + JS inline,
  nessun file CSS o JS separato.
- **Immagini**: `public/Img/Foto Fabio Gino Merli.png` e
  `public/Img/FOTO Michele Borzatta.png`.
- **Nessun build step**, nessun framework, nessun backend.
- **Hosting**: Cloudflare Workers (static assets). Worker name: `balanceandgrowth`.
- **Dominio**: `balanceandgrowth.com` e `www.balanceandgrowth.com` (custom
  domain collegati al Worker su Cloudflare).
- **Deploy**: `npx wrangler deploy` dalla cartella del progetto.
- **Specifiche tecniche complete**: vedi `TECH-SPEC.md`.

Mantieni questa semplicità. Niente dipendenze o strumenti nuovi senza una ragione
reale: ogni dipendenza è un nodo in più da sciogliere il giorno della consegna.

**Attenzione CSS**: ogni file HTML contiene un blocco `<style>` inline. Se
modifichi il design system (colori, font, variabili CSS), ricordati di
replicare la modifica in tutti e tre i file.

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
- **5 servizi**: Diagnosi e struttura · Controllo e governo · Direzione
  strategica (CFO/CEO Fractional) · Sviluppo internazionale · Finanza ordinaria
  e straordinaria.
- Formazione: corso "Business Up" sul business plan (7 moduli).
- Partner: DSC Solutions (energia/sostenibilità/rifiuti), AI Academy (Starting Work).
- Contatti pubblici: `info@balanceandgrowth.com` (email visibile sul sito, via
  Cloudflare Email Routing) · `ceobalanceadvisory@protonmail.com` (nel JSON-LD
  strutturato) · `+39 331 680 5428` (nel JSON-LD strutturato).

**Regola ferma**: niente risultati, numeri o testimonianze di clienti finché non
li fornisce Fabio. Non fabbricare prove sociali.

## Fatti su Michele (NON inventare nulla oltre a questi)

- Partner di Balance & Growth Advisory per l'area organizzazione e compliance.
- Consulente e Project Manager, 20+ anni di esperienza in sistemi qualità e
  Modelli Organizzativi D.Lgs. 231/01.
- Lead Auditor ISO 9001:2015 (Unione Professionisti, 2025); Quality Management
  Systems Auditor (BSI Group, 2011).
- Socio fondatore: Starting Work Srl Impresa Sociale, Mestieri Lombardia (rete
  20+ Agenzie per il Lavoro accreditate Regione Lombardia / Ministero Lavoro).
- Membro CdA Fondazione Alessandro Volta di Como.
- Competenze dichiarate: D.Lgs. 231/01, ISO 9001:2015, ISO 37001, ESG/GRI,
  PdR 125:2022, project management, governance cooperativa.

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
- ✅ Repo GitHub: https://github.com/Mikiborzi/balance-growth-advisory
- ✅ Deploy su Cloudflare Workers (Worker: `balanceandgrowth`, account Michele).
  - `balanceandgrowth.com` e `www.balanceandgrowth.com` configurati come custom domain.
  - `workers_dev: false` nel `wrangler.jsonc`.
  - Ultimo deploy: 2026-06-19 — Version ID: `b8a1ba20-4623-4998-911c-9d7d1f174723`.
- ✅ Homepage con 5 servizi, sezione brand, Founder & Partner, formazione, partner.
- ✅ Sottopagine profilo: `fabio.html` e `michele.html` con foto e timeline.
- ✅ Email contatti: `info@balanceandgrowth.com` via Cloudflare Email Routing.
- ✅ Immagini ottimizzate (PNG → JPEG, nomi senza spazi, peso ridotto).
- ✅ Email JSON-LD allineata a `info@balanceandgrowth.com`.
- ✅ Nav bar uniforme in tutte le pagine, con voce "Una rete di Valore" (#partner).
- ⚠️ Criticità residue: vedi `TECH-SPEC.md` sezione 10.
- ⬜ **Prossima fase**: valutare form di contatto. Modifiche ai contenuti solo se
  concordate con Michele.
