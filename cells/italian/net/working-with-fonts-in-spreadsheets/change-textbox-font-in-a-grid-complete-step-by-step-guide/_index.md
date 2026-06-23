---
category: general
date: 2026-06-21
description: Scopri come cambiare il font della casella di testo, impostare il colore
  del font programmaticamente e regolare la dimensione del font nella cella di una
  griglia. Segui questo tutorial pratico per lo styling delle caselle di testo.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: it
og_description: Modifica rapidamente il carattere della casella di testo in una griglia.
  Questa guida mostra come stilizzare la casella di testo, impostare il colore del
  carattere programmaticamente e regolare la dimensione della cella con codice chiaro.
og_title: Cambia il font della casella di testo in una griglia – Guida completa alla
  programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Modifica il carattere della casella di testo in una griglia – Guida completa
  passo passo
url: /it/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cambia il Font della Textbox in una Griglia – Guida Completa Passo‑per‑Passo

Ti è mai capitato di dover **cambiare il font della textbox** all’interno di una griglia dati senza sapere quale proprietà modificare? Non sei l’unico: la maggior parte degli sviluppatori incappa in questo ostacolo quando costruisce tabelle editabili o dashboard. In questo tutorial vedremo passo passo come cambiare il font della textbox, impostarne il colore programmaticamente e persino regolare la dimensione del font cella‑per‑cella.

Aggiungeremo anche consigli su **come stilizzare gli elementi textbox**, tratteremo scenari di **cambio della dimensione del font per cella** e ti mostreremo come **impostare il colore del font programmaticamente** senza impazzire. Alla fine avrai uno snippet riutilizzabile che funziona con qualsiasi componente griglia che espone un’API `getCell`.

## Prerequisiti

- Un browser moderno con supporto ES6 (Chrome, Edge, Firefox, Safari)
- Una libreria di griglia che offra `grid.getCell(row, col)` e restituisca un oggetto cella contenente un riferimento a `textbox`
- Conoscenze di base di oggetti JavaScript e proprietà CSS

Non sono necessari pacchetti aggiuntivi: solo JavaScript puro e l’API della griglia.

## Panoramica della Soluzione

L’idea di base è semplice: recuperare la cella di destinazione, prendere la textbox incorporata, quindi assegnare un nuovo oggetto font che definisce famiglia, dimensione e colore. È come dare alla textbox un nuovo outfit. Di seguito il flusso ad alto livello:

1. **Accedi alla cella di destinazione** – individua la riga/colonna desiderata.
2. **Recupera la textbox** – l’elemento UI che contiene il testo.
3. **Crea un oggetto stile font** – specifica famiglia, dimensione e colore.
4. **Applica lo stile** – assegna l’oggetto alla proprietà `font` della textbox.

Tutto qui. Vediamo ogni passo, spieghiamo perché è importante e osserviamo il codice in azione.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Passo 1: Accedi alla Cella di Destinazione nella Griglia

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Perché è importante:**  
> Le griglie spesso memorizzano righe e colonne con indici a base zero. Chiamando `grid.getCell(2, 3)` otteniamo la cella alla **riga 2, colonna 3**. Se devi **cambiare la dimensione del font per una cella** diversa, basta modificare gli indici.

**Suggerimento professionale:** Se la tua griglia supporta colonne nominate, puoi sostituire la colonna numerica con una chiave, ad esempio `grid.getCell(2, "price")`.

## Passo 2: Recupera la Textbox All’interno di Quella Cella

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Cosa sta succedendo:**  
> La maggior parte delle implementazioni di griglia avvolge il contenuto editabile in un elemento `<input>` o `<textarea>` e lo espone come `cell.textbox`. Ottenere il riferimento ci permette di manipolarne lo stile visivo direttamente.

Se la griglia utilizza un nome di proprietà diverso (come `cell.editor`), basta adeguare il codice di conseguenza—questa è una variazione comune quando **si vuole stilizzare la textbox** per un componente personalizzato.

## Passo 3: Definisci le Proprietà Font Desiderate

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Analisi dell’Oggetto

| Proprietà | Scopo | Esempi di Valore |
|-----------|-------|------------------|
| `family`  | Famiglia del font – controlla il tipo di carattere. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`    | Dimensione del font in pixel (o punti, a seconda della griglia). | `12`, `14`, `16` |
| `color`   | Colore del testo in qualsiasi formato CSS compatibile. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Perché usiamo un oggetto:**  
> Raggruppare le tre proprietà rende il codice più ordinato e rispecchia il modo in cui molte librerie UI si aspettano le informazioni di stile. Inoltre ti permette di **cambiare la famiglia del font nella griglia** o **impostare il colore del font programmaticamente** con un’unica assegnazione.

## Passo 4: Applica lo Stile Font alla Textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Dietro le quinte:**  
> Il componente textbox della griglia interpreta la proprietà `font` e aggiorna il suo CSS di conseguenza. Questa singola riga sostituisce la famiglia, la dimensione e il colore del font precedenti in un colpo solo—esattamente ciò che ti serve quando **cambi il font della textbox** su più celle.

Se il componente utilizza un’API diversa (ad esempio `textbox.style.fontFamily = ...`), adatta l’assegnazione mantenendo lo stesso principio.

## Esempio Completo Funzionante

Di seguito trovi uno snippet autonomo che puoi incollare in un file HTML contenente un oggetto griglia mock. Dimostra l’intero flusso dal passo 1 al passo 4, più una rapida verifica che lo stile sia cambiato.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Output Atteso

- La textbox situata alla **riga 2, colonna 3** ora mostra il testo in **Arial**, **14 px**, e una tonalità blu **#0066CC**.
- Aprendo la console del browser verrà stampato qualcosa del genere:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Se apri la pagina, confermerai visivamente il cambiamento—niente più font di sistema predefinito.

## Domande Frequenti (FAQ)

### Posso cambiare solo la dimensione del font senza influire su famiglia o colore?
Assolutamente. Basta omettere le proprietà che non vuoi modificare:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### E se la mia griglia usa un nome di proprietà diverso per la textbox?
Ispeziona l’oggetto cella nella console (`console.log(cell)`). Probabilmente vedrai qualcosa come `cell.editor` o `cell.input`. Sostituisci `cell.textbox` con il riferimento corretto.

### Come applico lo stesso stile a un’intera colonna?
Itera sulle righe e imposta il font per ogni cella di quella colonna:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### C’è un modo per tornare al font originale?
Salva lo stile originale prima di sovrascriverlo:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Consigli & Buone Pratiche

- **Aggiornamenti batch:** Se devi stilizzare molte celle, raggruppa le modifiche in `requestAnimationFrame` o in un metodo batch specifico della griglia per evitare “layout thrashing”.
- **Font responsivi:** Usa unità relative (`em`, `rem`) invece di pixel fissi se la tua UI deve scalare.
- **Accessibilità:** Assicurati un contrasto sufficiente quando **imposti il colore del font programmaticamente**—il minimo WCAG AA è un rapporto 4.5:1 per testo normale.
- **Quirks cross‑browser:** Alcune griglie più vecchie potrebbero richiedere l’impostazione diretta di `style.fontFamily` sull’elemento `<input>` anziché usare un oggetto `font`.

## Conclusione

Abbiamo appena coperto **come cambiare il font della textbox** all’interno di una griglia, dal recuperare la cella giusta alla definizione di un oggetto `fontStyle` riutilizzabile e alla sua applicazione in una sola riga. Lungo il percorso abbiamo anche imparato a **cambiare la dimensione del font per cella**, **impostare il colore del font programmaticamente** e persino a **cambiare la famiglia del font nella griglia** per una colonna specifica.

Ora puoi prendere questo modello e adattarlo a qualsiasi libreria UI—che tu stia costruendo un dashboard amministrativo, un editor tipo foglio di calcolo o uno strumento di reporting personalizzato. Sperimenta con famiglie, dimensioni e colori diversi; magari aggiungi effetti hover o stilizzazioni condizionali basate sui valori dei dati.

Hai un’altra sfida di styling? Lascia un commento e affrontiamola insieme. Buon coding!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑per‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Cambiare il Colore del Font in Excel Usando Aspose.Cells per Java: Guida Completa](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Tutorial per Cambiare il Colore del Font in Aspose Cells Java](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Tutorial per Cambiare il Colore del Font in Aspose Cells Java](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}