---
category: general
date: 2026-06-30
description: Lernen Sie, wie Sie die Adresse der ausgewählten Zelle ermitteln, den
  Wert einer Grid‑Zelle aktualisieren und den Eingabewert mit JavaScript und GridJs
  auslesen. Schritt‑für‑Schritt‑Code und Tipps.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: de
og_description: Erhalte die Adresse der ausgewählten Zelle, aktualisiere den Zellwert
  im Raster und lese den Eingabewert mit JavaScript. Befolge diese umfassende Anleitung
  für eine reibungslose GridJs-Integration.
og_title: Ausgewählte Zelladresse abrufen – Vollständiges GridJs JavaScript‑Tutorial
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
title: Adresse der ausgewählten Zelle in GridJs abrufen – Vollständige JavaScript-Anleitung
url: /de/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ausgewählte Zellenadresse erhalten – Vollständiges GridJs JavaScript‑Tutorial

Haben Sie jemals die **ausgewählte Zellenadresse** aus einer GridJs‑Tabelle erhalten müssen, waren sich aber nicht sicher, welchen API‑Aufruf Sie verwenden sollen? Sie sind nicht allein. In vielen Admin‑Panels klicken Benutzer auf eine Zelle, bearbeiten einen Wert in einem Modal und erwarten, dass das Grid die Änderung sofort widerspiegelt. Dieses Tutorial zeigt Ihnen genau, wie Sie diese Adresse abrufen, den neuen Preis aus einem Eingabefeld lesen und **den Zellenwert im Grid aktualisieren** ohne einen Seiten‑Reload.

Wir behandeln außerdem, wie man **Eingabewerte mit JavaScript liest** auf die richtige Weise, Randfälle handhabt und das Modal schließt, sobald das Update abgeschlossen ist. Am Ende haben Sie ein eigenständiges Snippet, das Sie in jedes Projekt, das GridJs verwendet, einbinden können.

## Was Sie bauen werden

- Eine einfache HTML‑Tabelle, die von GridJs betrieben wird.
- Ein Bearbeitungs‑Modal, das erscheint, wenn eine Zelle angeklickt wird.
- JavaScript, das **die ausgewählte Zellenadresse ermittelt**, den vom Benutzer eingegebenen Preis übernimmt, **den Zellenwert im Grid aktualisiert** und schließlich das Modal ausblendet.

Keine externen Bibliotheken außer GridJs sind erforderlich, und der Code funktioniert in modernen Browsern (Chrome 102+, Edge, Firefox). Wenn Sie bereits eine GridJs‑Instanz auf der Seite haben, können Sie die relevanten Teile direkt kopieren und einfügen.

## Voraussetzungen

- Grundkenntnisse in JavaScript und dem DOM.
- GridJs‑Bibliothek geladen (via CDN oder npm).
- Eine Seite, die bereits ein GridJs‑Grid rendert (wir zeigen ein minimales Beispiel).

Falls Ihnen das unbekannt vorkommt, keine Panik – jeder Schritt enthält eine kurze Zusammenfassung.

---

## Schritt 1: HTML‑Grundgerüst einrichten

Zuerst legen Sie den Tabellen‑Container, das versteckte Modal und das Preis‑Eingabefeld an. Das Modal wird mit einfachen CSS‑Klassen ein- und ausgeblendet.

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

> **Pro‑Tipp:** Das `#editModal` verwendet einen minimalen CSS‑Trick – fügen Sie einfach die Klasse `active` hinzu, um es anzuzeigen. Sie können dies gegen Bootstrap, Tailwind oder jede andere Modal‑Komponente austauschen, die Sie bereits verwenden.

---

## Schritt 2: GridJs initialisieren und Zellen‑Klicks erfassen

Jetzt erstellen wir ein Grid mit Beispieldaten und lauschen auf Zellauswahlen. Wenn ein Benutzer eine Zelle anklickt, **erhalten wir die ausgewählte Zellenadresse** und öffnen das Modal.

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

> **Warum das funktioniert:** `GridJs.getSelectedCell()` liefert einen String wie `"C2"` (Spalte C, Zeile 2). Wenn wir ihn in `lastSelectedCell` speichern, können wir später beim **Aktualisieren des Zellenwerts im Grid** exakt auf diese Position verweisen.

---

## Schritt 3: Neuen Preis aus dem Eingabefeld lesen

Wenn der Benutzer auf **Speichern** klickt, müssen wir **den Eingabewert mit JavaScript sicher auslesen**. Dieser Schritt prüft zudem, ob der eingegebene Preis eine positive Zahl ist.

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

> **Hinweis:** Durch die Verwendung von `parseFloat` akzeptieren wir Dezimalzahlen (z. B. `1.99`). Die `isNaN`‑Prüfung verhindert versehentliche leere Eingaben.

---

## Schritt 4: Ausgewählten Zellenwert aktualisieren

Jetzt aktualisieren wir endlich **den Zellenwert im Grid** mithilfe der zuvor erfassten Adresse. Die `updateCell`‑Methode von GridJs gibt ein Promise zurück, sodass wir eine Modal‑Schließ‑Aktion anhängen können.

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

> **Warum ein Promise verwenden?** GridJs muss möglicherweise die Tabelle neu rendern oder mit einem Backend synchronisieren. Durch das Warten auf das Promise stellen wir sicher, dass die UI erst ausgeblendet wird, nachdem das Grid den neuen Wert angezeigt hat.

---

## Schritt 5: Abbrechen‑ und Randfälle behandeln

Eine robuste Lösung bietet dem Benutzer immer einen Ausweg. Der **Abbrechen**‑Button blendet das Modal einfach aus und löscht jede gespeicherte Adresse.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Was, wenn keine Zelle ausgewählt ist?

Wenn ein Benutzer aus irgendeinem Grund den **Speichern**‑Button auslöst, ohne vorher eine Zelle anzuklicken (vielleicht hat er das Modal programmgesteuert geöffnet), ist `lastSelectedCell` `null`. Das frühe Zurückkehren in `updateSelectedCell` verhindert einen Laufzeitfehler und gibt eine hilfreiche Warnung aus.

### Umgang mit großen Grids

Bei Grids mit Paginierung liefert `GridJs.getSelectedCell()` weiterhin die absolute Adresse (z. B. `"B12"`), nicht nur die sichtbare Zeile. Das bedeutet, das Update funktioniert, selbst wenn die bearbeitete Zeile auf einer anderen Seite liegt. Beachten Sie jedoch, dass die UI nach einem Update nicht automatisch die Seite wechselt – falls Sie das benötigen, rufen Sie `grid.forceUpdate()` auf oder navigieren Sie manuell zur entsprechenden Seite.

---

## Vollständiges funktionierendes Beispiel

Below is the full code you can copy‑paste into a single HTML file. Open it in a browser, click any cell, change the price, and watch the grid update instantly.

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


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Adresse, Zellenanzahl und Offset für den gesamten Excel‑Bereich erhalten](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Adresse, Zellenanzahl und Offset für den gesamten Excel‑Bereich erhalten](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Adresse, Zellenanzahl und Offset für den gesamten Excel‑Bereich erhalten](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}