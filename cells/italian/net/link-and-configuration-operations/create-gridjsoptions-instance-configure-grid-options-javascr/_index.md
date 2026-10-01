---
category: general
date: 2026-05-30
description: Impara come creare un'istanza di GridJsOptions e configurare le opzioni
  della griglia in JavaScript per tabelle dinamiche. Guida passo‑passo con codice
  completo.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: it
og_description: Crea un'istanza di GridJsOptions e configura le opzioni della griglia
  JavaScript in pochi minuti. Esempio completo, spiegazioni e consigli sulle migliori
  pratiche.
og_title: Crea istanza GridJsOptions – Configura le opzioni della griglia JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Crea un'istanza di GridJsOptions – Configura le opzioni della griglia JavaScript
url: /it/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un'istanza GridJsOptions – Configura le opzioni della griglia JavaScript

Ti sei mai chiesto come **create GridJsOptions instance** senza dover cercare tra documenti sparsi? Non sei il solo. Quando ti serve una tabella elegante e ordinabile su una pagina web, padroneggiare come **configure grid options JavaScript** è il primo passo verso un'interfaccia utente raffinata.

In questo tutorial ti guideremo attraverso il codice esatto di cui hai bisogno, spiegheremo perché ogni impostazione è importante e ti mostreremo un esempio completo e funzionante. Alla fine sarai a tuo agio nel **create GridJsOptions instance**, modificare l'allineamento, la paginazione e persino i renderer personalizzati delle celle — tutto con JavaScript puro.

## Cosa imparerai

- Come **create GridJsOptions instance** da zero.
- Le proprietà chiave che ti permettono di **configure grid options JavaScript** (ordinamento, paginazione, formattazione dei numeri, ecc.).
- Errori comuni (ad esempio, mescolare stringhe e numeri) e come evitarli.
- Una pagina HTML completa che puoi copiare‑incollare in qualsiasi progetto e vedere subito i risultati.

### Prerequisiti

- Un browser moderno (Chrome, Edge, Firefox) – non sono richiesti strumenti di build.
- Familiarità di base con JavaScript (variabili, oggetti, DOM).
- La libreria Grid.js (la prenderemo da un CDN).

Se qualcosa ti è poco familiare, non preoccuparti — ogni passaggio include un rapido ripasso.

---

## Passo 1: Carica Grid.js e prepara lo scheletro HTML

Prima di poter **create GridJsOptions instance**, abbiamo bisogno della libreria stessa. Il modo più semplice è usare il CDN ufficiale. Di seguito trovi uno scheletro HTML minimale che riserva anche un `<div>` dove la griglia verrà renderizzata.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Suggerimento:** Mantieni il link CSS prima dei tuoi stili in modo che il tema predefinito della griglia venga caricato correttamente.

### Perché è importante

Caricare la libreria da un CDN garantisce di avere sempre l'ultima versione stabile senza installazione locale. Il `<div id="grid-wrapper">` è il segnaposto che il costruttore Grid.js utilizzerà una volta che **configure grid options JavaScript**.

---

## Passo 2: Crea una nuova istanza GridJsOptions

Ora arriva il cuore del tutorial: la riga che effettivamente **creates GridJsOptions instance**. In un file separato chiamato `grid-config.js` (referenziato nell'HTML sopra) scriveremo:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Quella singola riga ti fornisce un oggetto pulito che puoi iniziare a popolare con le impostazioni. Pensa a `gridOptions` come al pannello di controllo per ogni funzionalità che abiliterai in seguito.

### Cosa stai configurando

- **NumberFormatAlignment** – allinea automaticamente le stringhe numeriche.
- **Pagination** – controlla la dimensione della pagina e la navigazione.
- **Sorting** – attiva/disattiva l'ordinamento delle colonne.
- **Columns** – definisce intestazioni, tipi di dati e renderer personalizzati.

Puoi aggiungere una qualsiasi di queste proprietà prima di istanziare definitivamente la Grid.

---

## Passo 3: Abilita l'allineamento dei numeri (una necessità comune)

La maggior parte delle tabelle contiene una combinazione di testo e numeri. Per impostazione predefinita Grid.js allinea tutto a sinistra, il che appare strano per valori monetari. Per **configure grid options JavaScript** per un allineamento corretto, imposta il flag `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Perché abilitarlo? Quando il flag è true, Grid.js esamina ogni cella; se sembra un numero (ad esempio “1234”, “12.34%”), lo allinea automaticamente a destra. Questa piccola modifica rende i report molto più leggibili.

---

## Passo 4: Aggiungi paginazione e ordinamento

Una griglia reale raramente si adatta a un'unica schermata. Attiviamo la paginazione (10 righe per pagina) e permettiamo agli utenti di ordinare qualsiasi colonna.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Nota su casi limite

Se in seguito fornisci una fonte dati personalizzata che restituisce già risultati paginati, dovrai disabilitare la paginazione integrata di Grid.js per evitare una doppia paginazione. Basta impostare `gridOptions.Pagination.enabled = false;`.

---

## Passo 5: Definisci colonne e dati di esempio

Ora forniremo alla griglia alcuni dati fittizi e le diremo cosa rappresenta ogni colonna. Qui il pattern **create gridjsoptions instance** brilla davvero — tutto vive in un unico oggetto ordinato.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Nota che manteniamo i valori `id` delle colonne identici alle chiavi di ogni oggetto dati. Questa convenzione permette a Grid.js di mappare i valori automaticamente, risparmiandoti la scrittura di un formatter personalizzato per ogni colonna.

---

## Passo 6: Istanzia la Grid con le nostre opzioni

Infine **configure grid options javascript** passando l'oggetto `gridOptions` al costruttore Grid. La griglia verrà renderizzata all'interno del `<div id="grid-wrapper">` che abbiamo preparato in precedenza.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Questo è tutto. L'intero processo — dal **create gridjsoptions instance** al rendering — richiede meno di un minuto di codice.

### Output previsto

Quando apri il file HTML in un browser dovresti vedere:

- Una riga di intestazione con “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Numeri degli stipendi allineati a destra (grazie a `NumberFormatAlignment`).
- Controlli di paginazione in fondo (se hai aggiunto più di dieci righe).
- Intestazioni di colonna cliccabili che ordinano in modo ascendente/descendente.

Se qualcosa sembra strano, apri la console del browser (F12) e cerca messaggi di errore — la maggior parte dei bug deriva da ID di colonna non corrispondenti o script della libreria mancanti.

---

## Passo 7: Ottimizzazioni avanzate (opzionale)

Di seguito trovi alcune idee rapide che puoi sperimentare una volta che la griglia di base funziona.

| Feature | How to enable | Why it helps |
|---------|---------------|--------------|
| **Renderer personalizzato per le celle** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Evidenzia gli stipendi in grassetto. |
| **Barra di ricerca** | `gridOptions.Search = true;` | Permette agli utenti di filtrare le righe istantaneamente. |
| **Dati lato server** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Scala a migliaia di righe. |
| **Cambio tema** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Si adatta ai design in modalità scura. |

Sentiti libero di combinare le opzioni — Grid.js è deliberatamente flessibile. Ricorda solo di mantenere la riga originale **create gridjsoptions instance** in cima; tutte le modifiche successive dipendono da quell'unico oggetto.

---

## Conclusione

Abbiamo appena illustrato un flusso di lavoro completo per **create GridJsOptions instance** e **configure grid options JavaScript** per una tabella dati funzionale, ordinabile e paginata. Partendo da una semplice pagina HTML, abbiamo caricato la libreria, costruito un oggetto di opzioni, abilitato l'allineamento numerico, aggiunto la paginazione, definito le colonne e infine renderizzato la griglia.

Da qui puoi:

- Sostituire i `sampleData` statici con una chiamata AJAX.
- Aggiungere formatter personalizzati per date, valute o icone.
- Integrare la griglia in un framework come React o Vue (lo stesso oggetto `gridOptions` funziona anche lì).

Le possibilità sono praticamente infinite, e il pattern che abbiamo usato — centralizzare tutte le impostazioni in una singola istanza `GridJsOptions` — mantiene il tuo codice pulito e manutenibile.

Hai un caso d'uso di cui non sei sicuro? Lascia un commento e lo esploreremo insieme. Buon coding e divertiti a creare tabelle dinamiche con Grid.js!

## Cosa dovresti imparare dopo?

- [Come creare e configurare cartelle di lavoro Excel con Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Come creare e formattare tabelle Excel usando Aspose.Cells per .NET | Guida passo‑passo](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Come creare e formattare celle Excel usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}