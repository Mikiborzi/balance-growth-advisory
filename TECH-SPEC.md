# TECH-SPEC.md — Specifiche tecniche as-built

> Documento generato il 2026-06-15 leggendo i file reali ed eseguendo
> `npx wrangler whoami` e `npx wrangler deployments list`.
> Aggiornare ogni volta che cambia la struttura del progetto.

---

## 1. Panoramica e scopo

**Balance & Growth Advisory** è un sito vetrina che promuove le attività di
consulenza di **Fabio Gino Merli** (CFO e Direttore Generale, 25+ anni) verso
le PMI italiane. Il sito presenta il brand, i servizi, il team (Founder +
Partner), un percorso di formazione e i partner di rete.

Gestito da **Michele Borzatta** (socio storico di Fabio). Progettato per essere
indipendente e portabile: nessun framework, nessun build step, nessun backend.

---

## 2. Albero dei file

```
balance-growth-advisory/
├── public/                             ← cartella servita da Cloudflare
│   ├── index.html                      ← homepage (471 righe, ~32 KB)
│   ├── fabio.html                      ← profilo Fabio Gino Merli (242 righe, ~14 KB)
│   ├── michele.html                    ← profilo Michele Borzatta (265 righe, ~16 KB)
│   └── Img/                            ← immagini (cartella con I maiuscola)
│       ├── foto-fabio-merli.jpg        ← foto profilo Fabio (71 KB, 556×558 px)
│       └── foto-michele-borzatta.jpg   ← foto profilo Michele (85 KB, 900×758 px)
├── wrangler.jsonc                      ← configurazione Cloudflare Workers
├── CLAUDE.md                           ← istruzioni per Claude Code
├── HANDOVER.md                         ← passaggio di consegne
├── README.md                           ← introduzione rapida al progetto
├── .gitignore                          ← esclude node_modules/, .wrangler/, .DS_Store, *.log
└── Michele Borzatta_CV_26 (1).pdf      ← [⚠️ NON in git, non nella public/ — file residuo]
```

---

## 3. Hosting e deploy

| Parametro | Valore |
|---|---|
| Piattaforma | Cloudflare Workers (static assets) |
| Worker name | `balanceandgrowth` |
| `compatibility_date` | `2026-06-13` |
| Cartella asset | `./public/` |
| `workers_dev` | `false` (disabilitato) |
| Dominio primario | `balanceandgrowth.com` (custom domain) |
| Dominio secondario | `www.balanceandgrowth.com` (custom domain) |
| Account Cloudflare | `michele.borzatta@gmail.com` |
| Account ID | `420533bd2631c03f53302979bcf16a8c` |
| Versione Wrangler | 4.100.0 |
| Repo GitHub | https://github.com/Mikiborzi/balance-growth-advisory |

**Comando di pubblicazione:**
```bash
npx wrangler login    # solo la prima volta / se token scaduto
npx wrangler deploy
```

**Ultimo deployment:** 2026-06-15 — Version ID: `301e85e3-6460-463e-9263-111402640653`

---

## 4. Pagine e sezioni

### 4.1 `index.html` — Homepage

URL: `https://www.balanceandgrowth.com/`

| Sezione | Anchor/ID | Note |
|---|---|---|
| Navigazione fissa | `#nav` | Logo brand, link sezioni, burger mobile, CTA "Parliamone" |
| Hero | `#top` | Headline "Prima l'equilibrio. Poi la crescita.", CTA, elemento grafico "&" fulcrum |
| Manifesto | _(no anchor)_ | Citazione istituzionale in blocco scuro |
| Servizi | `#servizi` | 5 card servizi (vedi sotto) |
| Con chi operiamo | `#clienti` | 2 profili clienti: PMI in crescita / PMI in ristrutturazione |
| Il brand | `#brand` | Presentazione brand + timeline Fabio (su sfondo scuro) |
| Founder & Partner | `#team` | 2 card fotografiche (Fabio + Michele) con link a sottopagine |
| Formazione | `#formazione` | Corso "Business Up" — 7 moduli |
| Partner di rete | `#partner` | 2 partner: DSC Solutions, AI Academy _(non in nav)_ |
| Contatto | `#contatto` | Email `info@balanceandgrowth.com`, nessun form |
| Footer | — | Brand + copyright 2026 |

**5 servizi presenti:**
1. `01 · Diagnosi` — Diagnosi e struttura
2. `02 · Controllo` — Controllo e governo
3. `03 · Direzione` — Direzione strategica (CFO/CEO Fractional)
4. `04 · Internazionalizzazione` — Sviluppo internazionale
5. `05 · Finanza` — Finanza ordinaria e straordinaria

**Nav voci:** Home · Servizi · Con chi operiamo · Brand · Founder & Partner ·
Formazione · Parliamone (CTA)
_(la sezione `#partner` NON è in nav — visibile solo scrollando)_

---

### 4.2 `fabio.html` — Profilo Fabio Gino Merli

URL: `https://www.balanceandgrowth.com/fabio.html`

| Sezione | Note |
|---|---|
| Hero profilo | Foto, titolo, ruolo, citazione (blockquote) |
| Bio + competenze | Paragrafi biografici + tag pill competenze (10 tag) |
| Timeline | 5 posizioni: B&G Advisory (2021–oggi), Cappellini (2018–2021), Lattonedil (2007–2018), Fitness First (2006–2007), Adecco (2000–2004) |
| CTA | Link a `/#contatto` |
| Footer | Standard |

**Nav sottopagina:** Servizi · Clienti · Il brand · Formazione · Parliamone
_(manca #team come voce di ritorno; back-link punta a `/#brand`)_

---

### 4.3 `michele.html` — Profilo Michele Borzatta

URL: `https://www.balanceandgrowth.com/michele.html`

| Sezione | Note |
|---|---|
| Hero profilo | Foto, titolo, ruolo, citazione (blockquote) |
| Bio + competenze | Paragrafi biografici + tag pill competenze (11 tag) |
| Certificazioni | 4 card: Lead Auditor ISO 9001:2015, Quality Mgmt Auditor BSI, 2 certificati Regione Lombardia |
| Timeline | 4 posizioni: consulente indipendente (2022–oggi), Mestieri Lombardia (2014–oggi), Starting Work (2010–oggi), cooperative sociali (1998–2022) |
| CTA | Link a `/#contatto` |
| Footer | Standard |

**Nav sottopagina:** identica a `fabio.html`

---

## 5. Design system

### 5.1 Variabili CSS (`:root`) — identiche in tutti e tre i file

```css
/* Colori */
--ink:          #11302E   /* petrolio profondo — sfondo sezioni scure, testo */
--ink-2:        #0B2422   /* petrolio più scuro — footer, gradienti */
--paper:        #F4F1E9   /* carta calda — sfondo principale */
--paper-2:      #ECE7DA   /* carta leggermente più scura — sezioni alternate */
--brass:        #B07D2B   /* ottone — CTA, accenti, bordi */
--brass-soft:   #C9A05A   /* ottone soft — testi su scuro, hover */
--green:        #2E6B47   /* verde misurato — tag sezione clienti */
--text-soft:    #445B57   /* testo secondario su carta */
--on-ink-soft:  #A9C0BB   /* testo secondario su scuro */
--line:         #D8D1C0   /* bordi su carta */
--line-ink:     rgba(201,160,90,.22)  /* bordi sottili su scuro */

/* Font */
--serif:  'Fraunces', Georgia, 'Times New Roman', serif
--sans:   'Archivo', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif
--mono:   'JetBrains Mono', ui-monospace, SFMono-Regular, Menlo, monospace

/* Layout */
--maxw:   1140px
--gutter: clamp(20px, 5vw, 64px)
```

### 5.2 Uso dei font

| Font | Uso |
|---|---|
| Fraunces (serif) | Titoli (`h1`–`h3`), blockquote, nome brand, testi corsivi |
| Archivo (sans) | Corpo del testo, paragrafi |
| JetBrains Mono | Eyebrow label, CTA button, tag numerici, metadati, footer note |

### 5.3 Pattern ricorrenti

- **`.eyebrow`** — etichetta monocromatica ottone, maiuscola, con linea decorativa sinistra
- **`.reveal`** — animazione fade-up on scroll (via `IntersectionObserver`); disabilitata con `prefers-reduced-motion`
- **`.btn-primary`** — bottone ottone pieno, font mono
- **`.btn-ghost`** — bottone outline ottone
- **`.team-card`** / **`.partner`** / **`.svc`** — card con bordo sottile, hover su `--brass`
- **`.timeline`** — lista verticale con linea e pallino ottone
- **`.tag-pill`** — chip con bordo arrotondato, font mono
- **Nav scrolled** — nav trasparente diventa opaca (backdrop blur) al scroll > 40px

---

## 6. Immagini

| File | Dimensione | Dimensioni px | Riferimenti |
|---|---|---|---|
| `public/Img/foto-fabio-merli.jpg` | 71 KB | 556×558 | `index.html` (sezione #team), `fabio.html` (hero) |
| `public/Img/foto-michele-borzatta.jpg` | 85 KB | 900×758 | `index.html` (sezione #team), `michele.html` (hero) |

### Note immagini

| # | Nota | Dettaglio |
|---|---|---|
| 1 | **Nomi normalizzati** | ✅ Rinominati in lowercase con trattini, senza spazi (risolto 2026-06-15). |
| 2 | **Peso ottimizzato** | ✅ Convertiti da PNG a JPEG: Fabio −83% (407 KB → 71 KB), Michele −97% (2,9 MB → 85 KB, scalata a 900 px). |
| 3 | **Nessun favicon esterno** | Il favicon è un SVG inline codificato in base64 direttamente nell'HTML — nessun file `.ico` o `.png` separato. Funziona, ma non è cacheato separatamente. |

---

## 7. Link esterni e dipendenze

| Risorsa | URL | Tipo | File |
|---|---|---|---|
| Google Fonts (Fraunces + Archivo + JetBrains Mono) | `https://fonts.googleapis.com/css2?...` | Font esterno, preconnect | tutti e 3 |
| DSC Solutions | `https://www.dsc-solutions.it/` | Partner, `target="_blank" rel="noopener"` | `index.html` |
| AI Academy (Starting Work) | `https://sw-aiacademy.duckdns.org` | Partner, `target="_blank" rel="noopener"` | `index.html` |

**Dipendenze npm / package.json:** nessuna. Wrangler viene usato via `npx`
senza essere installato localmente nel progetto (nessun `package.json`).

---

## 8. Contatti presenti nel codice

| Campo | Valore | Dove |
|---|---|---|
| Email visibile (sezione #contatto) | `info@balanceandgrowth.com` | `index.html` riga 443 |
| Email nel JSON-LD (strutturata) | `info@balanceandgrowth.com` | `index.html` riga 20 |
| Telefono nel JSON-LD (strutturato) | `+39 331 680 5428` | `index.html` riga 20 |
| Canonical URL homepage | `https://www.balanceandgrowth.com/` | `index.html` |
| Canonical URL Fabio | `https://www.balanceandgrowth.com/fabio.html` | `fabio.html` |
| Canonical URL Michele | `https://www.balanceandgrowth.com/michele.html` | `michele.html` |

Il numero di telefono compare solo nel JSON-LD, non nel corpo visivo della pagina (vedi C4).

---

## 9. Impostazioni lato Cloudflare da annotare a mano

Queste configurazioni non sono nel codice e vanno verificate nel pannello
Cloudflare (https://dash.cloudflare.com).

| Impostazione | Descrizione | Da verificare |
|---|---|---|
| **Custom domains** | `balanceandgrowth.com` e `www.balanceandgrowth.com` collegati al Worker `balanceandgrowth` | Pannello Workers & Pages → balanceandgrowth → Settings → Domains & Routes |
| **Email Routing** | `info@balanceandgrowth.com` instrada le email in entrata verso un indirizzo di destinazione (presumibilmente ProtonMail o Gmail di Fabio/Michele) | Pannello Email → Email Routing → Routes |
| **DNS** | Record A/CNAME per `balanceandgrowth.com` e `www.balanceandgrowth.com` gestiti da Cloudflare (proxy arancione) | Pannello DNS → Records |
| **Registrar** | `balanceandgrowth.com` registrato tramite Cloudflare Registrar, intestato a Michele Borzatta | Pannello Domain Registration |
| **SSL/TLS** | Certificato automatico Cloudflare (Universal SSL) — da verificare che sia attivo e in modalità Full o Full (Strict) | Pannello SSL/TLS |
| **Wrangler deployment UUID** | Ultimo deployment attivo: da confrontare con `npx wrangler deployments list` | L'UUID corretto è quello più recente nella lista (`npx wrangler deployments list`) |

---

## 10. Criticità note

| # | Criticità | Priorità |
|---|---|---|
| ~~C1~~ | ~~Foto Michele pesa 3 MB~~ | ✅ Risolto 2026-06-15 — convertita a JPEG 85 KB |
| ~~C2~~ | ~~Spazi nei nomi file immagini~~ | ✅ Risolto 2026-06-15 — rinominati in lowercase con trattini |
| ~~C3~~ | ~~Email inconsistente~~ | ✅ Risolto 2026-06-15 — JSON-LD allineato a `info@balanceandgrowth.com` |
| C4 | **Telefono solo nel JSON-LD** — `+39 331 680 5428` non compare nel corpo visivo. Valutare se aggiungerlo alla sezione #contatto. | Media |
| C5 | **Sezione `#partner` assente dalla nav** — DSC Solutions e AI Academy non sono raggiungibili dal menu. Valutare se aggiungere voce nav o anchor dal footer. | Bassa |
| C6 | **Back-link delle sottopagine punta a `#brand`** — `fabio.html` e `michele.html` hanno il link "← Il brand" che porta a `#brand` anziché a `#team`. Semanticamente scorretto (le card foto sono in `#team`). | Bassa |
| C7 | **`Michele Borzatta_CV_26 (1).pdf` nella root** — file non in git, non nella `public/`, probabilmente residuo. Va spostato o rimosso. | Bassa |
| C8 | **AI Academy usa dominio `duckdns.org`** — non è un dominio professionale. Da aggiornare quando disponibile un dominio proprio. | Bassa |
| C9 | **Repo GitHub: stato pubblico/privato non allineato** — CLAUDE.md dice "pubblico", HANDOVER.md dice "privato". Da verificare e allineare. | Bassa |
| C10 | **Nessun form di contatto** — le email arrivano solo se l'utente ha un client mail. Un servizio gestito (Web3Forms / Formspree) o un Worker Cloudflare migliorebbe la conversione. | Da pianificare |
| C11 | **CSS duplicato** — i tre file HTML contengono ciascuno un blocco `<style>` quasi identico. Non è un bug (il progetto è volutamente senza build), ma qualsiasi modifica al design system va replicata manualmente tre volte. | Da pianificare |
