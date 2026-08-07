---
category: general
date: 2026-06-21
description: Crea una griglia dati interattiva usando Grid.js e impara a visualizzare
  una tabella di dati JSON con ordinamento, paginazione e ricerca. Perfetta per i
  cruscotti web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: it
og_description: Crea una griglia dati interattiva in pochi minuti. Scopri come usare
  Grid.js per visualizzare una tabella di dati JSON con paginazione, ordinamento e
  ricerca.
og_title: Crea una griglia dati interattiva con Grid.js – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Crea una griglia dati interattiva con Grid.js – Guida completa passo passo
url: /it/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Griglia Dati Interattiva con Grid.js – Guida Completa Passo‑per‑Passo

Ti sei mai chiesto come **creare una griglia dati interattiva** che consenta agli utenti di ordinare, cercare e paginare le righe senza scrivere un backend? Non sei solo. In molti dashboard il problema più grande è trasformare un dump JSON statico in una tabella elegante e ricercabile—qualcosa che sembra un foglio di calcolo ma gira interamente nel browser.

In questo tutorial vedremo **come usare Grid.js** per **visualizzare una tabella di dati JSON** su una semplice pagina HTML. Alla fine avrai un esempio funzionante che potrai inserire in qualsiasi progetto, oltre a consigli per personalizzare la barra degli strumenti, gestire grandi set di dati e evitare gli errori più comuni.

## Cosa Imparerai

- Come recuperare un file JSON che definisce colonne e righe.  
- Come inizializzare **Grid.js** con paginazione, ordinamento, ricerca e una barra degli strumenti personalizzata.  
- Come renderizzare la griglia in un contenitore di destinazione.  
- Personalizzazioni opzionali: formattazione personalizzata delle celle, cambio di tema e gestione degli errori.  
- Un esempio completo, pronto per copia‑incolla.

### Prerequisiti

Prima di immergerci, assicurati di avere:

1. Un browser moderno (Chrome, Edge o Firefox) – Grid.js si basa su funzionalità ES6.  
2. Una cartella locale o remota contenente un file `grid_data.json` (mostreremo il formato).  
3. Familiarità di base con HTML e JavaScript – niente di sofisticato, solo la capacità di aprire un file `.html` in un browser.

Nessuno strumento di build, nessun `npm install`, nessun codice lato server. Questa è la bellezza di **creare una griglia dati interattiva** con Grid.js: funziona direttamente da un CDN.

---

## Passo 1: Prepara il JSON Che Definisce la Tua Tabella

La prima cosa di cui hai bisogno è un payload JSON che dica a Grid.js quali colonne esistono e quali righe mostrare. Pensalo come il progetto per la tua **visualizzare una tabella di dati JSON**. Ecco un esempio minimale che puoi salvare come `grid_data.json` nella stessa directory del tuo file HTML:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Perché questo formato?* Grid.js si aspetta che `columns` sia un array di stringhe (o oggetti per configurazioni avanzate) e che `rows` sia un array di array dove ogni array interno corrisponde all'ordine delle colonne. Puoi, naturalmente, aggiungere più colonne o oggetti nidificati – Grid.js li renderizzerà finché le forme corrispondono.

> **Consiglio professionale:** Se stai prelevando dati da un'API, sostituisci semplicemente il `fetch('grid_data.json')` statico con l'URL del tuo endpoint. Il resto del codice rimane invariato.

---

## Passo 2: Inizializza Grid.js – Il Cuore di **how to use gridjs**

Ora che la fonte dati è pronta, dobbiamo portare Grid.js nella pagina e dirgli come comportarsi. Qui è dove creiamo effettivamente la funzionalità di **creare griglia dati interattiva** come paginazione, ordinamento e un pratico pulsante nella barra degli strumenti.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

Il CDN ti fornisce l'ultima versione stabile, e il tema Mermaid aggiunge un aspetto pulito e moderno subito pronto all'uso. Puoi sostituirlo con `gridjs.min.css` se preferisci lo stile predefinito.

Successivamente, all'interno di un tag `<script>`, recupera il JSON e inizializza la griglia:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Analisi delle Opzioni

| Opzione | Cosa Fa | Perché è Importante |
|--------|--------------|----------------|
| `pagination` | Divide le righe in pagine (default 10 per pagina) | Mantiene le tabelle grandi usabili senza sovraccaricare l'interfaccia. |
| `sort` | Le intestazioni di colonna cliccabili alternano ordine ascendente/descendente | Gli utenti possono trovare rapidamente le righe con i valori più alti. |
| `search` | Aggiunge un campo di testo che filtra le righe al volo | Ideale per ricerche ad‑hoc senza ricaricare i dati. |
| `toolbar` | Aggiunge pulsanti o menu a tendina personalizzati sopra la griglia | Perfetto per azioni “Aiuto”, “Esporta” o “Aggiorna”. |
| `formatter` | Consente di restituire HTML grezzo per una cella | Qui trasformiamo le stringhe email in link mailto cliccabili. |

> **Perché questo approccio?** Mantenendo la configurazione della griglia dichiarativa, puoi modificare facilmente il comportamento senza toccare la logica di rendering principale. Questo è il modo consigliato per **how to use Grid.js** nella maggior parte dei progetti.

---

## Passo 3: Renderizza la Griglia nella Tua Pagina

L'ultima riga dello script—`grid.render(document.getElementById('grid-container'))`—inietta la tabella completamente funzionale in un `<div>` che hai posizionato da qualche parte nel corpo HTML:

```html
<div id="grid-container"></div>
```

Questo è tutto. Quando la pagina si carica, il browser recupera il JSON, costruisce l'istanza Grid.js e dipinge la tabella interattiva sullo schermo. Nessun refresh, nessuna chiamata al server dopo il caricamento iniziale.

---

## Opzionale: Personalizzazioni di Stile e Tema

Se il tema Mermaid predefinito non è di tuo gradimento, puoi sostituirlo con uno dei temi integrati (`gridjs.min.css`) o scrivere il tuo CSS. Per esempio, per rendere lo sfondo dell'intestazione di un grigio tenue:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Aggiungi lo snippet all'interno di un tag `<style>` o in un foglio di stile esterno. Grid.js rispetta i selettori CSS standard, così hai il pieno controllo su caratteri, colori e spaziature.

---

## Problemi Comuni & Come Evitarli

| Problema | Sintomo | Risoluzione |
|----------|----------|--------------|
| **Errori CORS** quando si recupera JSON da un altro dominio | La console del browser mostra “Blocked by CORS policy” | Ospita il JSON sulla stessa origine o abilita CORS sul server. |
| **Set di dati grandi causano rallentamenti** | Lo scorrimento diventa scattoso, la paginazione lenta | Usa la paginazione `server` (`pagination: { server: { url: (prev, page, limit) => … } }`) o carica le righe in modo lazy. |
| **Il pulsante della toolbar non appare** | Nessun pulsante visibile nonostante `toolbar.enabled: true` | Assicurati di usare Grid.js versione 2.0+; le versioni più vecchie avevano un'API toolbar diversa. |
| **I link email non sono cliccabili** | Il formatter restituisce testo semplice | Restituisci `gridjs.html(...)` invece di una stringa semplice, come mostrato nell'esempio. |

Affrontare questi problemi fin dall'inizio ti farà risparmiare ore di debug in seguito.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il file HTML completo che puoi salvare come `index.html`. Aprilo in un browser e vedrai una demo completamente funzionale di **creare una griglia dati interattiva** che **visualizza una tabella di dati JSON** con ordinamento, ricerca e un pulsante di aiuto.



## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Creare un Elenco di Convalida Dati Excel con Aspose.Cells per Java: Guida Passo‑per‑Passo](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Come Creare Caselle di Controllo in Excel usando Aspose.Cells per .NET | Tutorial di Convalida Dati](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Creare e Importare Dati XML in Excel con Aspose.Cells per Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}