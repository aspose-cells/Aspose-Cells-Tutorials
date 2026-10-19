---
category: general
date: 2026-06-30
description: Scopri come ottenere l'indirizzo della cella selezionata, aggiornare
  il valore della cella della griglia e leggere il valore di input con JavaScript
  usando GridJs. Codice passo‑passo e consigli.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: it
og_description: Ottieni l'indirizzo della cella selezionata, aggiorna il valore della
  cella della griglia e leggi il valore di input con JavaScript. Segui questa guida
  completa per un'integrazione fluida di GridJs.
og_title: Ottieni l'indirizzo della cella selezionata – Tutorial completo di GridJs
  JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Ottieni l'indirizzo della cella selezionata in GridJs – Guida completa a JavaScript
url: /it/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni l'indirizzo della cella selezionata – Tutorial completo di GridJs JavaScript

Ti è mai capitato di dover **get selected cell address** da una tabella GridJs ma non sapevi quale chiamata API utilizzare? Non sei il solo. In molti pannelli di amministrazione, gli utenti cliccano su una cella, modificano un valore in un modal e si aspettano che la griglia rifletta il cambiamento immediatamente. Questo tutorial ti mostra esattamente come recuperare quell'indirizzo, leggere il nuovo prezzo da un campo di input e **update grid cell value** senza ricaricare la pagina.

Tratteremo anche **read input value with JavaScript** nel modo corretto, gestiremo i casi limite e chiuderemo il modal una volta terminato l'aggiornamento. Alla fine avrai uno snippet autonomo da inserire in qualsiasi progetto che utilizza GridJs.

## Cosa costruirai

- Una semplice tabella HTML alimentata da GridJs.  
- Un modal di modifica che appare quando si clicca una cella.  
- JavaScript che **gets the selected cell address**, recupera il prezzo inserito dall'utente, **updates the grid cell value**, e infine nasconde il modal.

Non sono necessarie librerie esterne oltre a GridJs, e il codice funziona con i browser moderni (Chrome 102+, Edge, Firefox). Se hai già un'istanza GridJs nella pagina, puoi copiare‑incollare direttamente le parti rilevanti.

## Prerequisiti

- Conoscenza di base di JavaScript e del DOM.  
- Libreria GridJs caricata (via CDN o npm).  
- Una pagina che già rende una griglia GridJs (mostreremo un esempio minimale).

Se qualcuno di questi punti ti è poco familiare, non preoccuparti: ogni passaggio include un rapido riepilogo.

---

## Passo 1: Configura lo scheletro HTML

Per prima cosa, disponi il contenitore della tabella, il modal nascosto e l'input del prezzo. Il modal verrà attivato con semplici classi CSS.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** Il `#editModal` utilizza un trucco CSS minimale—basta aggiungere la classe `active` per mostrarlo. Puoi sostituirlo con Bootstrap, Tailwind o qualsiasi componente modal che già usi.

---

## Passo 2: Inizializza GridJs e cattura i click delle celle

Ora creeremo una griglia con dati di esempio e ascolteremo le selezioni di cella. Quando un utente clicca una cella, **get the selected cell address** e apriremo il modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()` restituisce una stringa come `"C2"` (colonna C, riga 2). Memorizzandola in `lastSelectedCell` possiamo fare riferimento alla posizione esatta quando più tardi **update grid cell value**.

---

## Passo 3: Leggi il nuovo prezzo dal campo di input

Quando l'utente clicca **Save**, dobbiamo **read input value with JavaScript** in modo sicuro. Questo passaggio valida anche che il prezzo inserito sia un numero positivo.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** L'uso di `parseFloat` garantisce l'accettazione dei decimali (es., `1.99`). Il controllo `isNaN` evita invii accidentali di campi vuoti.

---

## Passo 4: Aggiorna il valore della cella selezionata

Ora finalmente **update grid cell value** usando l'indirizzo catturato in precedenza. Il metodo `updateCell` di GridJs restituisce una promise, così possiamo concatenare un'azione di chiusura del modal.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** GridJs potrebbe dover ri‑renderizzare la tabella o sincronizzarsi con un backend. Attendendo la promise garantiamo che l'interfaccia si nasconda solo dopo che la griglia ha riflettuto il nuovo valore.

---

## Passo 5: Gestisci Annulla e i casi limite

Una soluzione robusta offre sempre all'utente un'uscita. Il pulsante **Cancel** nasconde semplicemente il modal e cancella qualsiasi indirizzo memorizzato.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Cosa succede se nessuna cella è selezionata?

Se un utente in qualche modo attiva il pulsante **Save** senza aver prima cliccato una cella (forse ha aperto il modal programmaticamente), `lastSelectedCell` sarà `null`. Il ritorno anticipato in `updateSelectedCell` impedisce un errore di runtime e registra un avviso utile.

### Gestire Griglie di grandi dimensioni

Per le griglie con paginazione, `GridJs.getSelectedCell()` restituisce comunque l'indirizzo assoluto (es., `"B12"`), non solo la riga visibile. Questo significa che l'aggiornamento funziona anche se la riga modificata si trova su un'altra pagina. Basta essere consapevoli che l'interfaccia non cambierà automaticamente pagina dopo un aggiornamento—se ti serve, chiama `grid.forceUpdate()` o naviga manualmente alla pagina appropriata.

---

## Esempio completo funzionante

Di seguito trovi il codice completo da copiare‑incollare in un unico file HTML. Aprilo in un browser, clicca su qualsiasi cella, modifica il prezzo e osserva la griglia aggiornarsi istantaneamente.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Ottieni indirizzo, conteggio celle e offset per l'intero intervallo Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Ottieni indirizzo, conteggio celle e offset per l'intero intervallo Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Ottieni indirizzo, conteggio celle e offset per l'intero intervallo Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}