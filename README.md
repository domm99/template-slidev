# Slidev reusable template

Template riusabile per presentazioni [Slidev](https://sli.dev), estratto dal
tema/design system usato in `slides-2026-coordination-phyelds`, ma ripulito
da tutti i contenuti e componenti specifici di quella ricerca (diagrammi
animati sul field-calculus, logo del progetto, riferimenti, ecc.).

## Cosa contiene

```
slides-template/
├── slides.md                  # scaffold con tutti i pattern di slide pronti
├── package.json
├── styles/index.css           # design system (colori, tipografia, utility class)
├── components/
│   ├── BaseImg.vue            # <img> che rispetta il base path (GitHub Pages)
│   ├── QrCard.vue             # card con QR code + titolo
│   ├── Cites.vue              # footnote di citazione per slide
│   ├── References.vue         # slide finale bibliografia, generata da references.ts
│   ├── references.ts          # unica fonte di verità per la bibliografia
│   ├── Logo.vue                # logo segnaposto (SVG), da sostituire col tuo
│   └── FlowDiagram.vue         # diagramma a step animato e riusabile (click-reveal)
├── scripts/postbuild.mjs      # genera redirect per link diretti a singole slide
└── .github/workflows/deploy-slides.yml  # deploy automatico su GitHub Pages
```

## Setup

```bash
npm install
npm run dev      # anteprima locale, http://localhost:3030
npm run build    # build statica in dist/ (con redirect per slide)
npm run export   # esporta in PDF
```

## Pattern di slide disponibili in `slides.md`

Ogni slide usa `class:` nel frontmatter per scegliere un layout definito
in `styles/index.css`:

- **`first-slide` / `deck-cover`** — copertina, contenuto centrato.
- **`stage-slide`** — titolo + prosa, centrato verticalmente. Il default
  per slide argomentative; usa `<v-clicks>` per rivelare i bullet uno a uno.
- **`viz-slide`** — layout a due colonne (`split-grid`): testo a sinistra,
  visual a destra.
- **`code-slide`** — blocco di codice con line-highlight progressivo
  (`{all|3-5|6}`) più una breakdown a 3 colonne sotto.
- **`end-slide`** — per takeaway/riepilogo o slide finale di ringraziamenti.

Classi di utility CSS pronte all'uso: `mark-teal/orange/green` (evidenziazioni),
`u-solid/dashed/wavy/dotted-*` (sottolineature), `comparison-grid` /
`comparison-card`, `three-up`, `pipeline-grid`, `soft-card`, `slide-shell`
(contenitore centrato standard). Guarda `styles/index.css` per l'elenco completo.

## Componenti riusabili

- **`<Logo text="..." />`** — segnaposto SVG. Sostituiscilo con il tuo logo
  reale (o rimpiazza gli usi con `<BaseImg src="logo.png" />`, mettendo il
  file in `public/`).
- **`<QrCard title="..." url="..." :size="6.5" />`** — genera il QR a runtime.
- **`<Cites refs="1,3" />`** e **`<References />`** — sistema di citazioni
  basato su `components/references.ts`: aggiungi/modifica una voce lì e si
  aggiorna automaticamente sia la nota a piè di slide sia la slide finale.
- **`<FlowDiagram :stages="[...]" :click="$clicks" />`** — diagramma a step
  con reveal progressivo legato ai click della presentazione. Pattern
  estratto da `AggregateFlow.vue` del deck originale, ma generico: passi
  i tuoi step invece di ricreare ogni volta un componente ad hoc.

## Come personalizzare

1. Modifica `slides.md`: titolo, autori, contenuto di ogni slide.
2. Aggiorna `components/references.ts` con la tua bibliografia.
3. Sostituisci `Logo.vue` col logo vero (o rimuovilo).
4. Se vuoi i badge ACM artifact evaluation nella cover, metti i PNG in
   `public/badge-available.png` e `public/badge-reusable.png`, altrimenti
   rimuovi il blocco `.cover-badges` da `slides.md`.
5. Per animazioni specifiche del tuo dominio (come `ChannelEvolution.vue`
   o `FlockingStages.vue` nel deck originale), crea nuovi componenti in
   `components/` seguendo il pattern di `FlowDiagram.vue` (props tipizzate,
   prop opzionale `click` per il reveal progressivo, stile scoped che usa
   le CSS variable `--deck-teal/orange/green`).
6. Il deploy su GitHub Pages è già pronto in
   `.github/workflows/deploy-slides.yml`: basta pushare su `main` con questo
   repo pubblico e le Pages configurate su "GitHub Actions".

## Cosa NON è stato portato dal deck originale (di proposito)

Componenti legati al contenuto specifico della ricerca (`AggregateFlow.vue`,
`ArchitectureOverview.vue`, `ChannelEvolution.vue`, `FederatedLearningStep.vue`,
`FieldEvolution.vue`, `FlockingStages.vue`, `LocalRoundLoop.vue`,
`PhyeldsLogo.vue`) non sono stati copiati: sono illustrazioni ad hoc per
quella presentazione, non riusabili in generale. `FlowDiagram.vue` copre lo
stesso bisogno (uno stage-diagram animato) in forma parametrica.
# template-slidev
