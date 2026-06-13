# Balance & Growth Advisory — sito

Sito vetrina dello studio di consulenza di **Fabio Gino Merli**.
Sito statico (un solo file HTML), nessun build, ospitato su Cloudflare Workers.
Dominio: **balanceandgrowth.com**

---

## Com'è fatto

```
balance-growth-advisory/
├── public/
│   └── index.html        ← il sito (l'unico file che va online)
├── wrangler.jsonc        ← configurazione per pubblicare su Cloudflare
├── CLAUDE.md             ← istruzioni per lavorare con Claude Code
├── HANDOVER.md           ← passaggio di consegne (proprietà, credenziali, sgancio)
├── README.md             ← questo file
└── .gitignore
```

## Vedere il sito in locale

Apri semplicemente `public/index.html` nel browser (doppio click).
Oppure, da terminale, dentro la cartella del progetto:

```bash
npx wrangler dev
```

## Pubblicare le modifiche online

Dalla cartella del progetto:

```bash
npx wrangler login      # solo la prima volta
npx wrangler deploy
```

Il deploy aggiorna il sito live e mantiene il dominio collegato.

## Modificare i contenuti

Il modo più semplice è aprire questa cartella con **Claude Code** (o l'app
desktop di Claude) e chiedere le modifiche a parole. Le regole e il contesto
del progetto sono già scritti in `CLAUDE.md`: Claude Code li legge da solo.
