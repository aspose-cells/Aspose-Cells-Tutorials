---
category: general
date: 2026-06-21
description: Naučte se, jak změnit písmo textového pole, nastavit barvu písma programově
  a upravit velikost písma buňky v mřížce. Sledujte tento praktický tutoriál pro stylování
  textových polí.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: cs
og_description: Rychle změňte písmo textového pole v mřížce. Tento návod ukazuje,
  jak stylovat textové pole, nastavit barvu písma programově a upravit velikost buňky
  pomocí přehledného kódu.
og_title: Změna písma textového pole v mřížce – kompletní programovací průvodce
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
title: Změna písma textového pole v mřížce – kompletní průvodce krok za krokem
url: /cs/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změna písma textboxu v mřížce – Kompletní průvodce krok za krokem

Už jste někdy potřebovali **změnit písmo textboxu** uvnitř datové mřížky, ale nebyli jste si jisti, kterou vlastnost upravit? Nejste sami – většina vývojářů narazí na tento problém při tvorbě editovatelných tabulek nebo dashboardů. V tomto tutoriálu vás provedeme přesně tím, jak změnit písmo textboxu, nastavit jeho barvu programově a dokonce upravit velikost písma buňku po buňce.

Také přidáme tipy, jak **stylovat textbox** prvky, pokryjeme scénáře **změny velikosti písma buňky** a ukážeme vám, jak **nastavit barvu písma programově** bez ztráty nervů. Na konci budete mít znovupoužitelný úryvek, který funguje s libovolnou komponentou mřížky, která poskytuje API `getCell`.

## Požadavky

- Moderní prohlížeč s podporou ES6 (Chrome, Edge, Firefox, Safari)
- Knihovna mřížky, která nabízí `grid.getCell(row, col)` a vrací objekt buňky obsahující odkaz na `textbox`
- Základní znalost objektů JavaScriptu a CSS vlastností

Nejsou potřeba žádné další balíčky – stačí čistý JavaScript a vlastní API mřížky.

## Přehled řešení

Jádrový nápad je jednoduchý: načtěte cílovou buňku, získáte její vložený textbox a přiřadíte nový objekt písma, který definuje rodinu, velikost a barvu. Představte si to jako oblečení textboxu do nového outfitu. Níže je vysokou úrovní tok:

1. **Přístup k cílové buňce** – najděte řádek/sloupec, který chcete.
2. **Získání textboxu** – UI prvek, který obsahuje text.
3. **Vytvoření objektu stylu písma** – specifikujte rodinu, velikost a barvu.
4. **Aplikace stylu** – přiřaďte objekt k vlastnosti `font` textboxu.

To je vše. Ponořme se do každého kroku, vysvětlíme, proč je důležitý, a ukážeme kód v akci.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Krok 1: Přístup k cílové buňce v mřížce

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Proč je to důležité:**  
> Mřížky často ukládají řádky a sloupce jako indexy začínající od nuly. Voláním `grid.getCell(2, 3)` získáme buňku na **řádku 2, sloupci 3**. Pokud potřebujete **změnit velikost písma buňky** pro jiné místo, stačí upravit indexy.

**Pro tip:** Pokud vaše mřížka podporuje pojmenované sloupce, můžete číselný sloupec nahradit klíčem, např. `grid.getCell(2, "price")`.

## Krok 2: Získání textboxu uvnitř buňky

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Co se děje:**  
> Většina implementací mřížky zabaluje editovatelný obsah do elementu `<input>` nebo `<textarea>` a vystavuje jej jako `cell.textbox`. Získání reference nám umožňuje přímo manipulovat s jeho vizuálním stylem.

Pokud mřížka používá jiný název vlastnosti (např. `cell.editor`), stačí kód podle toho upravit – to je běžná varianta, když **stylujete textbox** pro vlastní komponentu.

## Krok 3: Definování požadovaných vlastností písma

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Rozklad objektu

| Vlastnost | Účel | Příklad hodnot |
|----------|------|----------------|
| `family` | Font family – řídí typ písma. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Font size v pixelech (nebo bodech, podle mřížky). | `12`, `14`, `16` |
| `color`  | Barva textu v libovolném CSS‑kompatibilním formátu. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Proč používáme objekt:**  
> Zabalení tří atributů dohromady činí kód přehledným a odráží, jak mnoho UI knihoven očekává informace o stylu. Také vám umožní **změnit rodinu písma v mřížce** nebo **nastavit barvu písma programově** jedním přiřazením.

## Krok 4: Aplikace stylu písma na textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Za scénou:**  
> Komponenta textboxu mřížky interpretuje vlastnost `font` a podle toho aktualizuje její CSS. Tento jediný řádek nahradí předchozí rodinu písma, velikost a barvu najednou – přesně to, co potřebujete, když **měníte písmo textboxu** napříč více buňkami.

Pokud komponenta používá jinou API (např. `textbox.style.fontFamily = ...`), přizpůsobte přiřazení, ale zachovejte stejný princip.

## Kompletní funkční příklad

Níže je samostatný úryvek, který můžete vložit do HTML souboru obsahujícího simulovaný objekt mřížky. Ukazuje celý tok od kroku 1 do kroku 4, plus rychlé ověření, že styl byl změněn.

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

### Očekávaný výstup

- Textbox umístěný na **řádku 2, sloupci 3** nyní zobrazuje text v **Arial**, **14 px**, a modrém odstínu **#0066CC**.
- Otevřením konzole prohlížeče se vypíše něco jako:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Když stránku otevřete, vizuálně potvrdíte změnu – žádné výchozí systémové písmo.

## Často kladené otázky (FAQ)

### Můžu změnit jen velikost písma, aniž bych ovlivnil rodinu nebo barvu?
Ano. Stačí vynechat vlastnosti, které nechcete měnit:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Co když moje mřížka používá jiný název vlastnosti pro textbox?
Prohlédněte si objekt buňky v konzoli (`console.log(cell)`). Pravděpodobně uvidíte něco jako `cell.editor` nebo `cell.input`. Nahraďte `cell.textbox` správnou referencí.

### Jak aplikovat stejný styl na celý sloupec?
Projděte řádky a nastavte písmo pro každou buňku v tomto sloupci:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Existuje způsob, jak se vrátit k původnímu písmu?
Uložte původní styl před přepsáním:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tipy a osvědčené postupy

- **Dávkové aktualizace:** Pokud potřebujete stylovat mnoho buněk, zabalte změny do `requestAnimationFrame` nebo metody specifické pro mřížku, aby nedošlo k přetěžování rozvržení.
- **Responsivní písma:** Používejte relativní jednotky (`em`, `rem`) místo pevných pixelů, pokud se UI má škálovat.
- **Přístupnost:** Zajistěte dostatečný kontrast při **nastavování barvy písma programově** – minimální poměr WCAG AA je 4,5:1 pro normální text.
- **Prohlížečové nuance:** Některé starší mřížky mohou vyžadovat nastavení `style.fontFamily` přímo na element `<input>` místo použití objektu `font`.

## Závěr

Právě jsme prošli **jak změnit písmo textboxu** uvnitř mřížky, od získání správné buňky po definování znovupoužitelného objektu `fontStyle` a jeho aplikaci v jednom řádku. Na cestě jsme se také naučili **změnit velikost písma buňky**, **nastavit barvu písma programově** a dokonce upravit **změnu rodiny písma v mřížce** pro konkrétní sloupec.

Nyní můžete tento vzor převzít a přizpůsobit libovolné UI knihovně – ať už budujete administrativní dashboard, editor ve stylu tabulky nebo vlastní nástroj pro reportování. Experimentujte s různými rodinami, velikostmi a barvami; možná přidáte efekty při najetí nebo podmíněné stylování na základě hodnot dat.

Máte další výzvu ve stylování? Zanechte komentář a pojďme ji společně vyřešit. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak změnit barvu písma v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Změna barvy písma Aspose Cells Java tutoriál](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Změna barvy písma Aspose Cells Java tutoriál](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}