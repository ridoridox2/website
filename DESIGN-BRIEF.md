# DESIGN BRIEF — SwissPeak Partners
Estratto dal codice live del sito (`index.html`, `about.html` — CSS identico in `:root` su tutte le pagine). Nessun file del progetto è stato modificato: questo è un nuovo documento di riferimento per ricreare lo stesso stile in una presentazione 16:9.

---

## 1. Palette colori

### a. Colori usati (hex) e ruolo

| Variabile CSS | Hex | Ruolo |
|---|---|---|
| `--ink` | `#1b2530` | Testo principale / titoli su sfondo chiaro |
| `--graphite` | `#343f4b` | Testo secondario poco più chiaro di `--ink` (es. voci della fact-list) |
| `--granite` | `#69737e` | Testo body / paragrafi su sfondo chiaro |
| `--mist` | `#9ba5af` | Testo muted, etichette minori, scrollbar — su sfondo chiaro |
| `--fog` | `#dde2e8` | Bordi hairline, divisori, outline bottoni — su sfondo chiaro |
| `--snow` | `#eef1f5` | Sfondo sezione alternata (chiaro, leggermente grigio) |
| `--paper` | `#ffffff` | Sfondo principale chiaro / testo bianco pieno su sfondo scuro |
| `--swiss` | `#4f6d86` | Accento raro — parola evidenziata in un H2 (sezione mappa) |
| `--swiss-deep` | `#3c5469` | Variante scura di `--swiss`, dichiarata ma usata pochissimo |
| `--flag` | `#c0392b` | Rosso bandiera svizzera — **solo decorativo**: mirino del cursore custom e "flag pin". Mai su testo, bottoni o card |
| `--alpine` | `#202935` | Sfondo scuro secondario — dropdown nav mobile |
| `--alpine-2` | `#29333f` | Variante di `--alpine`, uso raro (hover/variante) |
| `--stone` | `#1c201e` | Sfondo scuro principale — hero, footer, sezioni CTA, contatti, dropdown desktop |
| `--stone-2` | `#2b2723` | Variante di `--stone`, usata come bordo della "bolla" risposta FAQ scura |
| `--ice` | `#5b9bd1` | Azzurro accento secondario — testo evidenziato su sfondo scuro, puntino "acc" dei dots, eyebrow glow |
| `--ice-deep` | `#3a80ba` | Azzurro primario — bottoni, CTA, link, stato attivo, prefisso "\|" degli eyebrow |
| *(hover, no var)* | `#2f6a9c` | Hover di bottoni/link primari (scurimento di `--ice-deep`) |

Testo su sfondo scuro non usa mai un hex fisso: è sempre bianco a opacità variabile in base alla gerarchia —
- Titoli: `#ffffff` (100%, solido)
- Body: `rgba(255,255,255,.6)` (index) / `.5` (about/contatti)
- Etichette/muted: `rgba(255,255,255,.45)` / `.35` / `.25` (più profondo = meno importante)

### b. Gradienti

Un solo pattern di gradiente, riusato identico in più punti (`.hero-divider`, `.straight-sep`):
```
linear-gradient(90deg, transparent 0%, var(--ice) 20%, var(--ice) 80%, transparent 100%)
```
Linea orizzontale sottile (2px) che sfuma ai due estremi — usata come separatore a fine hero e tra sezioni. Nessun'altra angolazione o stop diversi nel sito: niente gradienti diagonali o radiali.

Oltre al gradiente, il grafico delle montagne usa un **tint fill** piatto (non gradiente): `rgba(91,155,209,.08)` — cioè `--ice` all'8% di opacità come riempimento del silhouette montano.

### c. Dominanti vs rari

- **Dominanti**: `--ink`, `--paper`, `--stone`, `--granite`, `--snow`, `--fog`, `--ice-deep` — presenti in ogni pagina, sono la spina dorsale cromatica (testo/sfondo/bottoni/bordi).
- **Rari / decorativi**: `--flag` (rosso, solo cursore e flag-pin), `--swiss`/`--swiss-deep` (una sola parola enfatizzata), `--alpine-2`, `--stone-2` (varianti di bordo, non sfondi autonomi), colore ambra `#d99248` (usato solo nella variante "amber" di una card audience, non è nemmeno nelle CSS variables — hardcoded localmente).

---

## 2. Tipografia

### a. Font family

- **Titoli e corpo testo**: `Poppins` — Google Fonts, pesi caricati: 300, 400, 500, 600, 700, 800, 900.
- **Eyebrow / etichette tecniche / numeri**: `IBM Plex Mono` — Google Fonts, pesi 400, 500.
- Nessun font self-hosted: entrambi via un unico `<link>`:
  ```
  https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800;900&family=IBM+Plex+Mono:wght@400;500&display=swap
  ```
- CSS vars: `--sans:'Poppins',system-ui,sans-serif` · `--mono:'IBM Plex Mono',monospace`

### b. Scala, pesi, line-height, letter-spacing

| Elemento | font-size | peso | line-height | letter-spacing |
|---|---|---|---|---|
| Hero H1 (home, `.hero-name`) | `clamp(2.6rem,24cqw,7.5rem)` | 800 | .95 | -.03em |
| Hero H1 (pagine interne) | `clamp(2.8rem,6.4vw,6rem)` | 800 | 1 | -.03em |
| Hero sub (home, `.hero-sub`) | `clamp(1.4rem,15cqw,3.8rem)` | 800 | 1 | -.02em |
| H2 sezione (canonico, ripetuto ovunque) | `clamp(2rem,4vw,3.4rem)` | 800 | ~1.15 | -.02em |
| H2 statement/CTA (centrato) | `clamp(2rem,4.5vw,3.8rem)` | 800 | 1.15 | -.02em |
| H2 sezione mappa (il più grande del sito) | `clamp(2.4rem,5.5vw,5.5rem)` | 800 | 1 | -.03em |
| H3 card audience | `clamp(2.3rem,4.2vw,3.6rem)` | 800 | 1.05 | -.02em |
| H3 link-row (lista servizi) | `clamp(1.3rem,2.4vw,1.9rem)` | 800 | normale | normale |
| Numero statistica (`.stat-n`) | `clamp(3.5rem,6vw,5.5rem)` | 800 | 1 | -.03em |
| Body / paragrafo standard | `1.05rem` (16.8px, fisso) | 400 | 1.75 | normale |
| Hero lead | `clamp(1.1rem,1.6vw,1.4rem)` | 400 | 1.75 | normale |
| Trust lead (frase breve, quote-like) | `clamp(1.1rem,1.8vw,1.5rem)` | 700 | 1.35 | -.01em |
| Intro "zoom" paragraph | `clamp(1.3rem,3vw,2.6rem)` | 700 (span enfasi: 800) | 1.3 | -.02em |
| Testimonial — simbolo virgolette | `4rem` | 800 | .7 (opacity .5) | — |
| Testimonial — testo | `1.05rem` | 400 | 1.75 | — |
| Etichetta statistica (`.stat-t`) | `.72rem` | 600 | normale | .16em, uppercase |
| Eyebrow mono (hero, pagine interne) | `1rem` | 400 | normale | .22em, uppercase |
| Hero greeting mono (home) | `clamp(1.2rem,1.6vw,2.2rem)` | 400 | normale | .08em |
| Sec-label (eyebrow sans, in ogni sezione) | `1rem` | 600 | normale | normale, uppercase |
| Tag card audience (mono) | `1rem` | 400 | normale | .2em, uppercase |
| Bottoni | `.8rem`–`.82rem` | 700 | normale | .06–.07em, uppercase |
| Footer `h5` (mono) | `.62rem` | 400 | normale | .2em, uppercase |
| Footer link/paragrafo | `.85rem` | 400 | 1.5–1.6 | normale |
| Voce fact-list | `.98rem` | 600 | 1.4 | normale |

Rapporto titolo/corpo canonico: **~1.9:1 al minimo, ~3.24:1 al massimo** (32px vs 54.4px, su un body fisso di 16.8px).

### c. Maiuscolo, corsivo, tracking

- **Ogni eyebrow/etichetta è in MAIUSCOLO con tracking ampio** (.14em–.22em): è la firma stilistica ricorrente che apre ogni sezione/card.
- **Nessun corsivo reale**: le parole enfatizzate usano `<em>` ma con `font-style:normal` forzato — l'enfasi è puramente cromatica (colore `--ice`), non tipografica.
- I numeri statistici hanno lo stesso tracking negativo dei titoli (-.03em), ma l'**unità** (`+`, `%`) è colorata diversamente (`--ice-deep`) per creare contrasto *dentro* lo stesso numero, senza cambiare peso o stile.
- I bottoni sono l'unico elemento con **tracking positivo** (.06–.07em) in un sito dominato da tracking negativo sui titoli — è il segnale visivo che distingue "azione" da "contenuto".

---

## 3. Layout e componenti

### a. Larghezze, griglie, spaziature, radius, ombre

- **Larghezza massima contenuto**: `1280px` (`--maxw`), via `.wrap{max-width:var(--maxw);margin:0 auto;padding:0 48px}` (24px su mobile <680px). Alcune sezioni "ampie" (mappa, intro zoom) usano 1400px.
- **Padding verticale sezione standard**: `120px 0` (classe `.sec`). Hero: full-height (`100svh` in home) o `130px` top padding (pagine interne).
- **Griglie ricorrenti**:
  - Switzerland graphic (`.ch-grid`): `1.1fr .9fr`, gap 64px
  - Fact list (`.fact-grid`): 2 colonne, gap `20px 28px`
  - Trust/stat block (`.trust-inner`): `1fr 1px 2fr` (testo / linea divisoria / 3 statistiche)
  - Stat columns (`.trust-stats`): `repeat(3,1fr)`
  - Audience cards (`.aud-grid`): `1fr 1fr`, gap 28px
  - Testimonial grid (`.testi-grid`): `repeat(3,1fr)`, gap **2px** (il gap minimo crea un effetto "griglia a celle" con bordo sottile tra le card)
  - Footer (`.foot-top`): `1.8fr 1fr 1fr 1fr`, gap 48px
  - Contatti (`.contact-inner`): `1fr 1.3fr`, gap 100px
- **Spaziature ricorrenti** (px): 8, 12, 16, 20, 24, 28, 32, 40, 48, 56, 64, 80, 120 — non una griglia da 8pt rigida, ma tutto multiplo di 4px.
- **Breakpoint**: 1180px (riassetto hero/mountain) · 900px (grid → stack) · 680px (padding wrap) · 560px (ulteriore stack).
- **Border-radius**: 4px (bottoni, voci dropdown, pillola nav) · 6px (dropdown container, map placeholder) · 8px (flag-pin, testimonial grid) · 16px (bolle chat FAQ, con un angolo forzato a 4px per effetto "coda" fumetto) · 50% (cerchi: icone, avatar) · 99px (pillola scrollbar).
- **Ombre**: minime e mirate — `0 10px 24px -8px rgba(19,22,26,.5)` (freccia FAQ), `0 10px 26px rgba(192,57,43,.35)` (flag-pin rosso), `0 4px 24px rgba(0,0,0,.3)` (FAB WhatsApp). Nessuna ombra su card o testo: la profondità è data da contrasto colore, non da shadow diffuse.
- **Bordi**: quasi sempre 1px, colore `--fog` su chiaro o `rgba(255,255,255,.07–.15)` su scuro — mai bordi spessi o colorati, tranne gli accent-bar animati (3px, `--ice`/`--ice-deep`) su hover di card/statistiche.

### b. Costruzione dei componenti principali

- **Hero**: full-bleed `--stone` scuro, sfondo "dots" animato (vedi 3c), eyebrow mono o greeting animato sopra un H1 enorme bianco, lead paragraph bianco trasparente, riga CTA (bottone pieno `--ice-deep` + bottone outline), e una linea-gradiente (`.hero-divider`) a chiudere il bordo inferiore. In home, un grafico 3D di montagna (canvas) appare dietro al testo sulla destra.
- **Trust / stat block**: striscia scura sotto l'hero, 2 colonne: quote breve e bold a sinistra, 3 celle statistiche a destra separate da sottili bordi verticali. Ogni cella: numero enorme (800, fino a 5.5rem) con unità colorata, etichetta uppercase piccola sotto, e una barra di avanzamento (3px, `--ice-deep`) che si anima da 0 a 100% quando la cella entra in viewport.
- **Card audience** (2 grandi riquadri "For companies / For candidates"): sfondo pieno scuro che si scurisce ulteriormente al hover, padding generoso (90px 70px), bordo superiore animato che si espande da sinistra al hover, icona SVG che appare (opacity+scale) al hover, tag mono uppercase, H3 enorme bianca, paragrafo chiaro trasparente, link con freccia "→" che si sposta al hover. Esiste una variante colore "amber" (`#d99248`) per differenziare la seconda card dalla prima (`--ice`).
- **Link-row** (lista servizi, es. Permanent Hiring / Project Solutions / Nearshoring): riga semplice con bordo superiore sottile, titolo a sinistra e freccia a destra che si muove al hover; l'ultima riga ha anche un bordo inferiore per chiudere visivamente il blocco.
- **Fact list**: icona circolare (36px, bordo `--fog`, icona stroke `--ice-deep`) + testo bold accanto, in griglia 2 colonne.
- **Testimonial card**: griglia 3 colonne con gap di 2px (crea un effetto "linea divisoria" sottilissima), grande simbolo virgolette (`--ice`, opacity .5) in alto, testo citazione, riga autore con avatar circolare grigio e bordo superiore.
- **CTA / statement**: sfondo scuro, testo centrato, H2 enorme con parola enfatizzata in `--ice` (spesso animata come "typewriter" via JS), paragrafo descrittivo, riga CTA centrata.
- **Contatti**: sfondo scuro, griglia `1fr 1.3fr` (testo+info a sinistra, form a destra); info con icone stroke `--ice`; input semi-trasparenti (bg bianco 6%, bordo bianco 10%, focus → bordo `--ice`).
- **Footer**: sfondo scuro, griglia 4 colonne (brand+payoff / servizi / company / contatti), bordo superiore sottile come separatore, riga finale con copyright e link legali.

### c. Elementi grafici distintivi

- **Motivo "montagna"** (coerente col nome *SwissPeak*): nella sezione "Why Switzerland" è un SVG stilizzato a zig-zag di una catena montuosa, con riempimento `--ice` all'8% di opacità e contorno `--ice-deep` da 2px, più due piccole "cime innevate" bianche semi-trasparenti sugli apici più alti, e un **flag-pin** rosso (quadrato arrotondato con croce bianca, stile pin/bandiera svizzera) posizionato sopra il grafico. In home, l'hero include anche una montagna 3D renderizzata via canvas/JS dietro al testo.
- **Bandiera/croce svizzera**: usata in due soli punti — (1) il mirino del cursore custom a forma di croce, (2) il flag-pin sul grafico montano. Il rosso `#c0392b` è riservato esclusivamente a questi due usi decorativi, mai a testo, link o bottoni.
- **Logo/wordmark**: SVG `fill:currentColor` (icona montagna stilizzata + "SwissPeak" + "Partners" in 3 blocchi di path) — eredita automaticamente il colore del contesto (bianco in header/hero, bianco 60% opaco nel footer).
- **Eyebrow decorativo**: ogni sezione apre con una piccola etichetta uppercase (mono o sans) prefissata da un trattino colorato o dal carattere "`|`" in `--ice-deep` — è il marcatore ricorrente che segnala l'inizio di ogni blocco.
- **Sistema "dots"**: sfondo decorativo presente in quasi ogni sezione — SVG assoluto full-bleed con decine di cerchietti (raggio 1.2–2.5px) posizionati pseudo-random, un singolo cerchio "accent" più grande (r=3, colorato `--ice`/`--ice-deep`) come punto focale, animazione di drift lento (14–20s, delay negativi per desincronizzare) più parallasse al scroll. Due varianti: `dots-dark` (cerchi bianchi trasparenti, su sfondi scuri) e `dots-light` (cerchi grigio-granite, su sfondi chiari).
- **Mappa Europa**: asset SVG dedicato (`europe_map.svg` / `map_europe_ok.svg`) per illustrare la copertura geografica Svizzera + Europa.
- **Fotografia**: le pagine principali (home/about) sono quasi 100% grafica vettoriale/CSS, pochissime foto. Le foto reali presenti nel repo (montagne, stretta di mano, colloqui, ambienti corporate) sono usate solo nelle pagine di servizio interne — stile: scatti professionali, colori naturali/freddi, soggetti legati a montagne svizzere, colloqui e contesti business.
- **Cursore custom e microinterazioni** (mirino a croce rosso, particelle, reveal-on-scroll a cascata con delay di 80ms per elemento): dettagli di branding molto specifici dell'esperienza web — da intendersi come riferimento di "personalità" del brand, non direttamente replicabili in un PDF/slide statico.

---

## Nota pratica per il template slide 16:9

Elementi da portare 1:1 nel deck: palette (in particolare `--stone` come sfondo scuro dominante, `--ice-deep`/`--ice` come accento), coppia di font Poppins 800/IBM Plex Mono, eyebrow uppercase con tracking ampio, H2 con letter-spacing negativo, il motivo grafico della montagna + flag-pin come elemento distintivo ricorrente (al posto del logo da solo), e il sistema "dots" come texture di sfondo statica (senza animazione) per le slide scure.

Da **non** portare: cursore custom, animazioni di scroll/typewriter, hover states — sono interazioni web, non hanno equivalente in uno slide deck statico.
