# Template per tesi triennale - Laurea in Informatica UniPD

Questo file è un promemoria personale e una guida su come è strutturato il template e come usarlo.
Il template originale è mantenuto da [FIUP](https://github.com/FIUP/Thesis-template) per il corso di Laurea in Informatica dell'Università di Padova.

---

## Struttura della repo

```
tesi/
├── config/
│   ├── variables.tex         ← variabili da modificare
│   ├── thesis-config.tex     ← configurazioni avanzate, comandi custom
│   └── packages.tex          ← dichiarazione pacchetti LaTeX
├── preface/
│   ├── title-page.tex        ← frontespizio (automatico da variables.tex)
│   ├── summary.tex           ← sommario/abstract
│   ├── dedication.tex        ← dedica
│   ├── copyright.tex         ← pagina copyright
│   └── table-of-contents.tex ← indice (automatico)
├── chapters/                 ← struttura dei capitoli (da modificare)
│   ├── introduzione.tex
│   ├── descrizione-stage.tex
│   ├── analisi-requisiti.tex
│   ├── valutazione-competitor.tex
│   ├── implementazione-tecnica.tex
│   ├── quality-observability.tex
│   ├── sviluppo-sicuro.tex
│   ├── business-intelligence.tex
│   └── conclusioni.tex
├── appendix/
│   ├── glossary-entries.tex  ← definizioni glossario e acronimi
│   ├── bibliography.bib      ← voci bibliografiche
│   ├── bibliography.tex      ← struttura automatica bibliografia
│   └── acknowledgements.tex  ← ringraziamenti
├── images/
│   └── unipd-logo.png        ← qui vanno tutte le immagini
├── structure.tex             ← ordine di inclusione dei file
├── thesis.tex                ← file radice (quello da compilare)
└── printable-thesis.tex      ← versione per la stampa
```

### Guida ai file principali

- **`config/variables.tex`** — la prima cosa da aprire. Definisce tutte le variabili che riempiono automaticamente il documento: titolo, nome, matricola, professore ecc. Riempie anche i metadati del PDF finale.
- **`config/thesis-config.tex`** — definizioni di comandi custom e configurazioni dei pacchetti. Di solito non va toccato, ma puoi modificarlo se vuoi personalizzare qualcosa.
- **`config/packages.tex`** — dichiarazione di tutti i pacchetti usati. Niente di rilevante da cambiare qui.
- **`preface/`** — tutto ciò che viene prima dei capitoli: frontespizio, sommario, dedica, ringraziamenti, indice. Il frontespizio si riempie automaticamente dalle variabili. Se il titolo della tesi è molto lungo potresti dover aggiustare leggermente gli spazi in `title-page.tex`.
- **`chapters/`** — qui passerai la maggior parte del tempo. Contiene i capitoli veri e propri. Usa nomi di file che riflettano il contenuto (es. `architettura-sistema.tex`), evita nomi generici come `capitolo-03.tex`. Trovi già dei capitoli di esempio che mostrano come usare glossario, bibliografia, use case, tabelle dei requisiti ecc.
- **`structure.tex`** — non contiene contenuto vero e proprio: definisce solo l'ordine in cui vengono inclusi tutti i file. Ogni volta che aggiungi o rimuovi un capitolo devi aggiornarlo.
- **`thesis.tex`** — il file radice da compilare per ottenere il PDF digitale.
- **`printable-thesis.tex`** — produce una versione ottimizzata per la stampa: margini asimmetrici, capitoli che aprono a destra, link non colorati.
- **`images/`** — dove il template cerca le immagini quando le includi nel testo.
- **`appendix/bibliography.bib`** — dove inserire le voci bibliografiche in formato BibTeX.
- **`appendix/glossary-entries.tex`** — dove definire le voci del glossario, seguendo la sintassi degli esempi già presenti.
- **`appendix/bibliography.tex`** — struttura automatica della bibliografia. Non serve modificarlo.

---

## Ordine delle sezioni nella tesi

| Sezione | Posizione |
|---|---|
| Frontespizio | Inizio |
| Copyright | Inizio |
| Dedica | Inizio |
| Sommario | Inizio |
| Indice / Liste figure e tabelle | Inizio |
| Capitoli (introduzione → conclusioni) | Corpo |
| Appendici | Fine |
| Acronimi | Fine |
| Glossario | Fine |
| Bibliografia | Fine |
| Ringraziamenti | Fine |

> La dedica va sempre all'inizio. I ringraziamenti sono alla fine.

---

## Prima cosa da fare: `config/variables.tex`

Apri questo file e compila tutti i campi:

```latex
\newcommand{\myName}{Mario Rossi}
\newcommand{\myID}{1234567}
\newcommand{\myTitle}{Titolo della mia tesi}
\newcommand{\myDegree}{Tesi di laurea}
\newcommand{\myUni}{Università degli Studi di Padova}
\newcommand{\myFaculty}{Corso di Laurea in Informatica}
\newcommand{\myDepartment}{Dipartimento di Matematica ``Tullio Levi-Civita''}
\newcommand{\profTitle}{Prof.}
\newcommand{\myProf}{Nome Cognome}
\newcommand{\myLocation}{Padova}
\newcommand{\myAA}{2024-2025}
\newcommand{\myTime}{Luglio 2025}
```

Aggiorna anche il blocco `\begin{filecontents*}` subito sotto, con titolo, autore e parole chiave per i metadati del PDF.

> ⚠️ Dopo aver modificato i metadati PDF elimina la cartella `build/` prima di ricompilare, altrimenti le modifiche non vengono recepite.

---

## Installazione

### Linux (Ubuntu/Debian)

Installa una versione leggera di TeX Live (circa 1-2 GB, molto meno di `texlive-full` che pesa 5-7 GB):

```bash
sudo apt install texlive-base texlive-latex-extra texlive-fonts-recommended texlive-lang-italian biber latexmk
```

Poi installa i pacchetti specifici richiesti dal template:

```bash
sudo tlmgr update --self && sudo tlmgr update --all
sudo tlmgr install pdfx xcolor xmpincl caption changepage csquotes emptypage \
  epigraph nextpage eurosym layaureo listings microtype mparhack relsize \
  quoting booktabs glossaries glossaries-italian glossaries-english biber \
  biblatex babel babel-italian cm-super greek-fontenc latexmk fancyhdr
```

### macOS

```bash
brew install basictex
```

Poi installa i pacchetti con `tlmgr` come indicato sopra per Linux.

In alternativa puoi scaricare **MacTeX** (installazione completa) da [tug.org/mactex](https://tug.org/mactex).

### Windows — Opzione 1: MiKTeX (più semplice)

La scelta più immediata su Windows. MiKTeX installa automaticamente i pacchetti mancanti alla prima compilazione, senza bisogno di usare il terminale.

1. Scarica e installa MiKTeX da [miktex.org/download](https://miktex.org/download)
2. Alla prima compilazione ti verrà chiesto se installare i pacchetti mancanti: conferma sempre

### Windows — Opzione 2: WSL (consigliata se sei a tuo agio col terminale)

WSL ti dà un terminale Linux dentro Windows, evitando i classici problemi di compatibilità di LaTeX su Windows. VS Code si integra nativamente con WSL.

Attiva WSL aprendo PowerShell come amministratore:

```powershell
wsl --install
```

Riavvia il PC, apri Ubuntu dal menu Start e segui i passaggi della sezione Linux qui sopra.

---

## Editor

### VS Code (consigliato)

Il modo più comodo se hai già la repo su GitHub, perché puoi committare e pushare le modifiche direttamente dall'editor.

1. Installa [VS Code](https://code.visualstudio.com)
2. Installa l'estensione **LaTeX Workshop** dal marketplace
3. Apri la cartella della repo in VS Code

La repo include già `.vscode/settings.json` preconfigurato per usare `latexmk`, quindi puoi compilare direttamente con il tasto ▶ senza toccare il terminale.

### TeXStudio

Editor dedicato a LaTeX, molto usato in ambito accademico. Ha suggerimenti automatici per i comandi LaTeX. Per configurarlo con `latexmk` segui i primi 3 punti di [questa guida](https://latex.ti.bfh.ch/doc_gettingStarted/configuration/texstudio.html).

### Overleaf

Editor online, nessuna installazione richiesta. Utile per lavorare da browser o condividere facilmente col relatore. Il piano gratuito va bene per uso personale, ma la sincronizzazione con GitHub richiede l'abbonamento a pagamento.

---

## Compilazione

### Comando base

```bash
latexmk thesis.tex
```

Per sovrascrivere e forzare la compilazione (se è già presente la cartella build/):
```bash
latexmk -gg thesis.tex
```

Latexmk gestisce automaticamente tutti i passaggi necessari (bibliografia, glossario ecc.), quindi non servono più esecuzioni manuali di `pdflatex`. Il PDF viene generato nella cartella `build/`.

Per la versione ottimizzata per la stampa:

```bash
latexmk printable-thesis.tex
```

### Glossario o bibliografia non compaiono?

È normale alla prima compilazione. Latexmk dovrebbe risolverlo da solo, ma se il problema persiste forza una ricompilazione completa:

```bash
latexmk -gg thesis.tex
```

### Altre opzioni utili

```bash
latexmk -help           # mostra tutte le opzioni disponibili
latexmk -g thesis.tex   # forza ricompilazione
latexmk -gg thesis.tex  # forza ricompilazione completa (più aggressiva)
```

---

## Supporto immagini SVG

Le immagini SVG sono supportate (e consigliate). Richiedono la dipendenza `cairosvg`:

```bash
pip install cairosvg
```

Per i diagrammi draw.io è necessario un ambiente POSIX per via dell'uso di `sed` (disponibile nativamente su Linux e macOS; su Windows funziona tramite WSL).

---

## Come aggiungere un capitolo

1. Crea il file `.tex` nella cartella `chapters/` con un nome che rifletta il contenuto (es. `architettura-sistema.tex`)
2. Aprilo con `\chapter{Titolo capitolo}` e il relativo `\label{cap:...}`
3. Registralo in `structure.tex` nell'ordine corretto:

```latex
\input{chapters/architettura-sistema}
```

---

## Glossario

Le voci si definiscono in `appendix/glossary-entries.tex`. Ci sono due tipi:

```latex
% Acronimo
\newacronym{api}{API}{Application Program Interface}

% Voce di glossario estesa
\newglossaryentry{apig}{
    name=\glslink{api}{API},
    text=Application Program Interface,
    sort=api,
    description={descrizione estesa...}
}
```

Per usare un termine nel testo:
- `\gls{api}` → prima occorrenza con marcatore [g], poi solo il termine
- `\Gls{api}` → come sopra ma con iniziale maiuscola

---

## Bibliografia

Aggiungi le voci in `appendix/bibliography.bib` in formato BibTeX:

```bibtex
@book{cognome:titolo-breve,
    author    = {Nome Cognome},
    title     = {Titolo del libro},
    publisher = {Editore},
    year      = {2023}
}

@online{site:nome-sito,
    title = {Titolo pagina},
    url   = {https://esempio.com}
}
```

Per citare nel testo:
- `\cite{cognome:titolo-breve}` → citazione inline
- `\footcite{cognome:titolo-breve}` → citazione a piè di pagina

---

## Fonti ufficiali UniPD

- Regolamento didattico e scadenze: [math.unipd.it](https://www.math.unipd.it/didattica/informazioni-per-la-laurea/)
- Conseguimento titolo e upload tesi: portale **Uniweb**
- Indicazioni specifiche: chiedere direttamente al relatore prima di iniziare
