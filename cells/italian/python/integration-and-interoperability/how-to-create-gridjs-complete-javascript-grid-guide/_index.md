---
category: general
date: 2026-06-30
description: Come creare gridjs facilmente con un esempio completo in JavaScript,
  coprendo la configurazione di gridjs, l'impostazione del contenitore e il processo
  di rendering.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: it
og_description: Come creare gridjs facilmente con un esempio completo in JavaScript,
  coprendo la configurazione di gridjs, l'impostazione del contenitore e il processo
  di rendering.
og_title: Come creare Gridjs – Guida completa alla griglia JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Come creare Gridjs – Guida completa alla griglia JavaScript
url: /it/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare Gridjs – Guida completa al grid JavaScript

Ti sei mai chiesto **come creare gridjs** e vedere istantaneamente una tabella dati elegante sulla tua pagina? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando provano per la prima volta a configurare Gridjs, soprattutto per quanto riguarda l'oggetto di configurazione e la chiamata di render. La buona notizia? È davvero un gioco da ragazzi una volta che conosci i passaggi giusti.

In questo tutorial percorreremo un esempio reale che mostra **come creare gridjs** da zero, come creare una corretta **gridjs configuration**, come collegare il grid a un **gridjs container**, e infine come attivare il **gridjs render**. Alla fine avrai un grid completamente funzionale da inserire in qualsiasi progetto—senza misteri, solo codice chiaro.

## Cosa imparerai

- Configurare una pagina HTML minima pronta per Gridjs.  
- Scrivere un oggetto **gridjs configuration** che definisce colonne, dati e opzioni.  
- Collegare l'istanza Gridjs a un elemento **gridjs container**.  
- Chiamare **gridjs render** per visualizzare la tabella.  
- Regolare impostazioni comuni (paginazione, ordinamento, stile) ed evitare le insidie più frequenti.

Non sono necessari strumenti di build esterni; tutto funziona nel browser con un unico tag script. Iniziamo.

## Prerequisiti

Prima di immergerci, assicurati di avere:

1. Un browser moderno (Chrome, Edge, Firefox, Safari) – qualsiasi supporti ES6.  
2. Conoscenze di base di HTML e JavaScript – non serve alcun framework.  
3. Accesso alla libreria Gridjs – la prenderemo da un CDN, quindi non è necessario installare npm.

Questo è tutto. Se hai già una pagina che vuoi migliorare, puoi incollare gli snippet direttamente.

## Passo 1: Aggiungi le risorse Gridjs alla tua pagina

Per prima cosa, dobbiamo caricare i file CSS e JavaScript di Gridjs. La versione CDN è leggera e perfetta per demo rapide.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** Il tema Mermaid dà alla tabella un aspetto pulito e moderno senza CSS aggiuntivo. Sentiti libero di sostituirlo con `classic.min.css` se preferisci uno stile diverso.

## Passo 2: Definisci il **gridjs container**

Il **gridjs container** è semplicemente un normale `<div>` che ospiterà la tabella renderizzata. Nel markup sopra abbiamo già creato `<div id="grid"></div>`. L'attributo `id` è fondamentale perché lo useremo per collegare l'istanza Gridjs in seguito.

Se ti servono più grid nella stessa pagina, assegna a ciascun container un ID unico (`grid1`, `grid2`, …) e ripeti la logica di binding per ognuno.

## Passo 3: Crea un oggetto **gridjs configuration**

Ora arriva il cuore di **come creare gridjs** – la configurazione. Questo semplice oggetto JavaScript indica a Gridjs quali colonne mostrare, quali dati inserire e quali funzionalità abilitare.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Perché questa configurazione è importante

- **Columns** – definiscono il testo dell'intestazione e la larghezza opzionale. Senza questo, Gridjs inferirebbe i nomi delle colonne dalla prima riga di dati, il che è spesso meno leggibile.  
- **Data** – un array di righe, ogni riga è un array di valori di cella. Puoi anche fornire una funzione asincrona che recupera i dati da un'API; la libreria gestirà le promesse automaticamente.  
- **Pagination** – limita le righe per pagina, evitando tabelle enormi che sovraccaricano l'interfaccia.  
- **Search & Sort** – attiva le funzionalità interattive con un singolo booleano, risparmiandoti la scrittura di handler personalizzati.  
- **Language** – personalizza le stringhe UI, perfetto per la localizzazione o il branding.

Sentiti libero di sostituire l'array di dati statici con una chiamata `fetch` in seguito; il resto dei passaggi rimane esattamente lo stesso.

## Passo 4: Istanzia Gridjs e collegalo al **gridjs container**

Con la configurazione pronta, creiamo un nuovo `GridJs.Grid` (il nome della classe è `gridjs.Grid` nella build UMD) e lo puntiamo al nostro elemento container.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Nota che abbiamo usato `document.getElementById('grid')`—questo è il **gridjs container** definito prima. Se hai più container, ripeti semplicemente questa riga con l'ID appropriato.

## Passo 5: Attiva la chiamata **gridjs render**

L'ultimo pezzo del puzzle è il metodo **gridjs render**. Prende la configurazione passata in precedenza e inietta un `<table>` completamente stilizzato nel container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Fatto! Quando apri la pagina in un browser, vedrai una tabella ricercabile e paginata con le quattro righe che abbiamo definito. La casella di ricerca appare automaticamente in alto, e i controlli di paginazione sono in basso.

### Output previsto

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

L'interfaccia si adatterà quando digiti nella casella di ricerca o clicchi le intestazioni delle colonne per ordinare.

## Varianti comuni & casi limite

### Caricamento dati in modo asincrono

Se i tuoi dati risiedono su un server, sostituisci l'array statico `data` con una funzione che restituisce una Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs mostrerà uno spinner di caricamento finché la promise non si risolve, quindi renderizzerà la tabella automaticamente.

### Rendering personalizzato delle celle

A volte servono icone, pulsanti o date formattate all'interno delle celle. Usa la proprietà `formatter` su una colonna:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

L'helper `gridjs.h` crea elementi virtual DOM senza introdurre React.

### Più grid in una sola pagina

Basta ripetere i passi 2‑5 con ID container diversi:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Ogni grid funziona in modo indipendente, così puoi mescolare limiti di paginazione, set di colonne e persino temi diversi.

## Pro Tips & Trappole da evitare

- **Non dimenticare il CSS** – senza il foglio di stile la tabella apparirà come una semplice tabella HTML, perdendo tutta la bella grafica e i controlli di paginazione.  
- **Evita ID duplicati** – ogni **gridjs container** deve avere un ID unico; altrimenti Gridjs sovrascriverà la prima istanza.  
- **Controlla la forma dei dati** – il numero di colonne deve corrispondere al numero di celle in ogni riga; array non corrispondenti causano glitch di layout silenziosi.  
- **Usa `gridjs.h` per celle complesse** – inserire stringhe HTML grezze può rompere l'algoritmo di diff del virtual DOM.  
- **Fai attenzione alla versione** – il link CDN sopra punta all'ultima release 5.x (a giugno 2026). Se blocchi a una versione più vecchia, alcune opzioni (come `language`) potrebbero mancare.

## Esempio completo funzionante (copia‑incolla)

Di seguito trovi il file HTML completo che puoi salvare come `gridjs-demo.html` e aprire direttamente in un browser.



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aspose.Cells per Java: Come creare e formattare cartelle di lavoro Excel in modo efficiente](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java | Guida alle operazioni su cartelle di lavoro](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Come creare e unire cartelle di lavoro Excel usando Aspose.Cells per Java | Guida completa](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}