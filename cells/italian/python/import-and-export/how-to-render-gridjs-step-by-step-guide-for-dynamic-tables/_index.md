---
category: general
date: 2026-07-03
description: Scopri come renderizzare Gridjs in pochi minuti con un esempio completo
  HTML/JS. Include il CDN della libreria Gridjs, caricamento lazy e consigli sulla
  configurazione JSON.
draft: false
keywords:
- how to render gridjs
- gridjs configuration JSON
- gridjs lazy loading
- gridjs library CDN
- gridjs render method
language: it
og_description: 'Come rendere Gridjs rapidamente: usa il CDN, recupera un JSON di
  configurazione e chiama il metodo render. Perfetto per tabelle dati dinamiche.'
og_title: Come renderizzare Gridjs – Guida completa all'implementazione
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  headline: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  type: TechArticle
- description: Learn how to render Gridjs in minutes with a full HTML/JS example.
    Includes Gridjs library CDN, lazy loading, and configuration JSON tips.
  name: How to Render Gridjs – Step‑by‑Step Guide for Dynamic Tables
  steps:
  - name: Why Use the CDN?
    text: '- **Performance:** Browsers cache the file across sites, so returning visitors
      may already have it. - **Simplicity:** No bundler configuration, just a single
      `<script>` tag. - **Lazy loading:** You can defer the script with `defer` or
      load it only when needed, which ties into our next step.'
  - name: Breaking Down the Code
    text: '| Line | What It Does | Why It Matters | |------|--------------|----------------|
      | `fetch(''YOUR_DIRECTORY/lazygrid.json'')` | Retrieves the configuration JSON
      via HTTP GET. | Keeps the HTML clean and allows you to change the grid layout
      without touching the page code. | | `.then(response => response'
  - name: Sample `lazygrid.json`
    text: Below is a minimal yet functional configuration file. Save it as `lazygrid.json`
      in the same directory as your HTML (or adjust the fetch path accordingly).
  - name: 1. Using Custom Render Functions
    text: 'Sometimes you need to format a cell—say, add a badge for ages over 28.
      Extend the column definition:'
  - name: 2. Server‑Side Pagination
    text: If your dataset is huge, fetching the entire JSON can be slow. Gridjs supports
      server‑side pagination—just set `pagination.server` to `true` and implement
      an API endpoint that returns slices of data based on `page` and `limit` query
      parameters.
  - name: 3. Styling with CSS Variables
    text: 'The Mermaid theme uses CSS variables for colors. Override them in a `<style>`
      block:'
  - name: 4. Accessibility Considerations
    text: Gridjs adds ARIA attributes automatically, but you can enhance keyboard
      navigation by ensuring your placeholder `<div>` is focusable (`tabindex="0"`).
      This helps screen‑reader users interact with the table.
  type: HowTo
tags:
- JavaScript
- Front‑end
- Data Tables
title: Come rendere Gridjs – Guida passo passo per tabelle dinamiche
url: /it/python/import-and-export/how-to-render-gridjs-step-by-step-guide-for-dynamic-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rendere Gridjs – Guida passo‑passo per tabelle dinamiche

Ti sei mai chiesto **come rendere Gridjs** su una semplice pagina HTML senza dover includere un framework pesante? Non sei l’unico. Molti sviluppatori hanno bisogno di una tabella leggera e ordinabile che possa ricevere dati da un file JSON, e Gridjs lo rende un gioco da ragazzi. In questo tutorial percorreremo ogni riga di codice necessaria, dal caricamento della CDN della libreria Gridjs al recupero pigro di un JSON di configurazione e, infine, alla chiamata del metodo render.

Inseriremo anche alcuni consigli di best‑practice—come il motivo per cui il lazy loading della configurazione Gridjs può migliorare la velocità della pagina, e come strutturare il tuo JSON affinché il metodo render di Gridjs funzioni perfettamente. Alla fine avrai una griglia completamente funzionante da inserire in qualsiasi progetto.

## Cosa costruirai

- Una pagina HTML minimale che carica Gridjs da una CDN  
- Un file `lazygrid.json` che definisce colonne, dati e plugin opzionali  
- JavaScript che recupera il JSON, crea un'istanza Gridjs e la rende in un placeholder  

Nessuno strumento di build, nessun npm, solo HTML puro e un po' di vanilla JS. Perfetto per siti statici, portali di documentazione o prototipi rapidi.

## Prerequisiti

- Conoscenza di base di HTML e JavaScript (nessun framework richiesto)  
- Un server web o un ambiente di sviluppo locale che possa servire file statici (es. VS Code Live Server)  
- Il file `lazygrid.json` posizionato in un luogo accessibile al browser  

Se ti senti a tuo agio con questi punti, immergiamoci.

## Step 1: Includi la CDN della libreria Gridjs

Il modo più veloce per ottenere Gridjs nella pagina è fare riferimento al suo bundle UMD da una CDN. Questo elimina la necessità di installazioni npm e mantiene il tutorial leggero.

```html
<!-- Step 1: Include the Gridjs library -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
```

> **Pro tip:** Il foglio di stile `theme/mermaid.min.css` aggiunge un aspetto pulito e moderno. Sostituiscilo con un altro tema se preferisci uno stile diverso.

### Perché usare la CDN?

- **Performance:** I browser memorizzano nella cache il file tra i siti, quindi i visitatori di ritorno potrebbero già averlo.  
- **Semplicità:** Nessuna configurazione di bundler, solo un singolo tag `<script>`.  
- **Lazy loading:** Puoi differire lo script con `defer` o caricarlo solo quando necessario, il che si collega al nostro prossimo passo.

## Step 2: Aggiungi un elemento placeholder per la griglia

Gridjs ha bisogno di un nodo DOM su cui montare la tabella. Crea un `<div>` con un ID unico—questo è dove il metodo render di Gridjs inietterà il markup della tabella.

```html
<!-- Step 2: Placeholder where Gridjs will appear -->
<div id="grid"></div>
```

Puoi stilizzare questo contenitore con CSS se hai bisogno di larghezze o margini personalizzati. Per ora, lo stile predefinito del tema manterrà le cose ordinate.

## Step 3: Carica un JSON di configurazione Gridjs e rendi la griglia

Ecco dove avviene la magia. Recupereremo un file JSON (`lazygrid.json`) che descrive le colonne, le righe di dati e i plugin che desideri. Poi istanzieremo Gridjs con quella configurazione e chiameremo il suo metodo render.

```html
<!-- Step 3: Fetch config and render Gridjs -->
<script>
  // Step 3.1: Pull the JSON config (replace the path as needed)
  fetch('YOUR_DIRECTORY/lazygrid.json')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(config => {
      // Step 3.2: Create a Gridjs instance using the fetched configuration
      const grid = new GridJs(config);
      // Step 3.3: Render the grid inside the placeholder element
      grid.render(document.getElementById('grid'));
    })
    .catch(error => console.error('Error loading Gridjs config:', error));
</script>
```

### Analisi del codice

| Linea | Cosa fa | Perché è importante |
|------|--------------|----------------|
| `fetch('YOUR_DIRECTORY/lazygrid.json')` | Recupera il JSON di configurazione tramite HTTP GET. | Mantiene pulito l'HTML e ti permette di modificare il layout della griglia senza toccare il codice della pagina. |
| `.then(response => response.json())` | Converte la risposta in un oggetto JavaScript. | Garantisce che tu stia passando un oggetto corretto a Gridjs. |
| `new GridJs(config)` | Costruisce un'istanza Gridjs con la configurazione fornita. | Questo è il punto di ingresso del **metodo render di gridjs**; la configurazione guida colonne, dati e plugin. |
| `grid.render(document.getElementById('grid'))` | Inserisce la tabella nel `<div id="grid">`. | L'ultimo passo che effettivamente **renderizza Gridjs** sullo schermo. |
| `.catch(...)` | Gestisce errori di rete o di parsing in modo elegante. | Impedisce che la pagina si rompa silenziosamente e fornisce informazioni di debug. |

### Esempio di `lazygrid.json`

Di seguito trovi un file di configurazione minimale ma funzionante. Salvalo come `lazygrid.json` nella stessa directory del tuo HTML (oppure adatta il percorso di fetch di conseguenza).

```json
{
  "columns": [
    "Name",
    "Email",
    { "id": "age", "name": "Age", "type": "number" }
  ],
  "data": [
    ["Alice", "alice@example.com", 30],
    ["Bob", "bob@example.com", 25],
    ["Carol", "carol@example.com", 27]
  ],
  "search": true,
  "pagination": {
    "enabled": true,
    "limit": 5
  }
}
```

- **gridjs configuration JSON**: L'array `columns` può contenere stringhe semplici o oggetti per un controllo maggiore (es. renderer personalizzati).  
- **gridjs lazy loading**: Memorizzando questo JSON separatamente, puoi sostituirlo senza dover ridistribuire la pagina HTML.  
- **gridjs render method**: La chiamata `grid.render(...)` legge questa configurazione e costruisce la tabella dinamicamente.

## Step 4: Verifica l'output

Apri il file HTML in un browser. Dovresti vedere una tabella ricercabile e paginata che corrisponde ai dati in `lazygrid.json`. Il tema predefinito Mermaid aggiunge sfumature sottili ed effetti al passaggio del mouse.

**Output previsto:**

| Nome  | Email               | Età |
|-------|---------------------|-----|
| Alice | alice@example.com   | 30  |
| Bob   | bob@example.com     | 25  |
| Carol | carol@example.com   | 27  |

Se non vedi la tabella:

1. Apri la console del browser (F12) e cerca errori.  
2. Assicurati che il percorso in `fetch('YOUR_DIRECTORY/lazygrid.json')` punti alla posizione corretta.  
3. Verifica che lo script CDN sia stato caricato (controlla la scheda Network).  

## Suggerimenti avanzati e casi particolari

### 1. Utilizzare funzioni di render personalizzate

A volte è necessario formattare una cella—ad esempio, aggiungere un badge per le età superiori a 28. Estendi la definizione della colonna:

```json
{
  "id": "age",
  "name": "Age",
  "formatter": (cell) => {
    return cell > 28 ? `<span style="color:red;">${cell}</span>` : cell;
  }
}
```

> **Nota:** Il formatter deve essere una funzione JavaScript, quindi dovrai incorporare la configurazione direttamente nello script o caricarla come modulo se vuoi mantenerla in JSON.

### 2. Paginazione lato server

Se il tuo dataset è enorme, recuperare l'intero JSON può essere lento. Gridjs supporta la paginazione lato server—basta impostare `pagination.server` a `true` e implementare un endpoint API che restituisca porzioni di dati in base ai parametri di query `page` e `limit`.

### 3. Styling con variabili CSS

Il tema Mermaid utilizza variabili CSS per i colori. Sovrascrivile in un blocco `<style>`:

```html
<style>
  :root {
    --gridjs-header-bg: #2c3e50;
    --gridjs-header-color: #ecf0f1;
  }
</style>
```

### 4. Considerazioni di accessibilità

Gridjs aggiunge automaticamente attributi ARIA, ma puoi migliorare la navigazione da tastiera assicurandoti che il tuo `<div>` placeholder sia focalizzabile (`tabindex="0"`). Questo aiuta gli utenti di screen‑reader a interagire con la tabella.

## Esempio completo funzionante

Mettendo tutto insieme, ecco un unico file HTML che puoi copiare‑incollare e eseguire localmente.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Render Gridjs Demo</title>
  <!-- Gridjs library CDN -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
  <style>
    /* Optional custom theme tweaks */
    :root {
      --gridjs-header-bg: #34495e;
      --gridjs-header-color: #ecf0f1;
    }
  </style>
</head>
<body>
  <!-- Placeholder for the grid -->
  <div id="grid"></div>

  <!-- Fetch config and render Gridjs -->
  <script>
    fetch('lazygrid.json')
      .then(r => r.ok ? r.json() : Promise.reject('Failed to load'))
      .then(cfg => {
        const grid = new GridJs(cfg);
        grid.render(document.getElementById('grid'));
      })
      .catch(err => console.error(err));
  </script>

  <!-- Optional screenshot for documentation -->
  <img src="gridjs-screenshot.png" alt="Screenshot demonstrating how to render Gridjs grid" style="display:none;">
</body>
</html>
```

Salvalo come `index.html` accanto a `lazygrid.json`, aprilo in un browser e guarda la griglia apparire istantaneamente.

## Conclusione

Ora hai una risposta chiara, end‑to‑end, a **come rendere Gridjs**: carica la CDN della libreria Gridjs, fornisci un `gridjs configuration JSON`, recuperalo in modo lazy, istanzia un oggetto Gridjs e chiama il `gridjs render method`. Questo approccio mantiene il tuo HTML ordinato, sfrutta il lazy loading per migliori prestazioni e ti dà pieno controllo su colonne, dati e plugin.

Cosa fare dopo? Prova ad aggiungere:

- **gridjs lazy loading** di grandi set di dati tramite paginazione lato server.  
- Renderer di celle personalizzate per grafici o barre di avanzamento.  
- Plugin di esportazione per permettere agli utenti di scaricare file CSV o Excel.  

Sentiti libero di sperimentare, e se incontri difficoltà, lascia un commento qui sotto. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Render Excel Sheets as Images Using Aspose.Cells .NET for Seamless Data Visualization](/cells/english/net/import-export/render-excel-sheets-images-aspose-cells-dotnet/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}