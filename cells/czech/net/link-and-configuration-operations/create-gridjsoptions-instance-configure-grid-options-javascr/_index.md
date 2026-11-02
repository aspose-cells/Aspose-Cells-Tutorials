---
category: general
date: 2026-05-30
description: Naučte se, jak vytvořit instanci GridJsOptions a nakonfigurovat možnosti
  mřížky v JavaScriptu pro dynamické tabulky. Průvodce krok za krokem s kompletním
  kódem.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: cs
og_description: Vytvořte instanci GridJsOptions a během několika minut nakonfigurujte
  možnosti mřížky v JavaScriptu. Kompletní příklad, vysvětlení a tipy na osvědčené
  postupy.
og_title: Vytvořte instanci GridJsOptions – Konfigurujte možnosti mřížky v JavaScriptu
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
title: Vytvořit instanci GridJsOptions – Konfigurace možností mřížky v JavaScriptu
url: /cs/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření instance GridJsOptions – Konfigurace možností mřížky v JavaScriptu

Už jste se někdy zamýšleli, jak **vytvořit instanci GridJsOptions** bez zbytečného prohledávání roztříštěné dokumentace? Nejste v tom sami. Když potřebujete na webové stránce elegantní, řaditelnou tabulku, zvládnutí toho, jak konfigurovat možnosti mřížky v JavaScriptu, je prvním krokem k vylepšenému UI.

V tomto tutoriálu projdeme přesný kód, který potřebujete, vysvětlíme, proč je každé nastavení důležité, a ukážeme kompletní, spustitelný příklad. Na konci budete pohodlně vytvářet instanci GridJsOptions, ladit zarovnání, stránkování a dokonce vlastní renderery buněk – vše pomocí čistého JavaScriptu.

## Co se naučíte

- Jak **vytvořit instanci GridJsOptions** od nuly.
- Klíčové vlastnosti, které vám umožní **konfigurovat možnosti mřížky v JavaScriptu** (řazení, stránkování, formátování čísel atd.).
- Časté úskalí (např. míchání řetězcových a číselných typů) a jak se jim vyhnout.
- Kompletní HTML stránku, kterou můžete zkopírovat‑vložit do libovolného projektu a okamžitě vidět výsledek.

### Předpoklady

- Moderní prohlížeč (Chrome, Edge, Firefox) – žádné nástroje pro sestavení nejsou potřeba.
- Základní znalost JavaScriptu (proměnné, objekty, DOM).
- Knihovna Grid.js (načteme ji z CDN).

Pokud vám některý z těchto bodů není známý, nepanikařte – každý krok obsahuje rychlý úvod.

---

## Krok 1: Načtení Grid.js a příprava HTML kostry

Než budeme **vytvářet instanci GridJsOptions**, potřebujeme samotnou knihovnu. Nejjednodušší cesta je použít oficiální CDN. Níže je minimální HTML kostra, která také rezervuje `<div>`, kam se mřížka vykreslí.

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

> **Tip:** Umístěte odkaz na CSS před své vlastní styly, aby se načetlo výchozí téma mřížky správně.

### Proč je to důležité

Načtení knihovny z CDN zajišťuje, že vždy získáte nejnovější stabilní verzi bez lokální instalace. `<div id="grid-wrapper">` je zástupný prvek, na který konstruktor Grid.js cílí, jakmile **konfigurujete možnosti mřížky v JavaScriptu**.

---

## Krok 2: Vytvoření nové instance GridJsOptions

Nyní přichází jádro tutoriálu: řádek, který skutečně **vytváří instanci GridJsOptions**. V samostatném souboru nazvaném `grid-config.js` (odkazovaném v HTML výše) napíšeme:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Ten jediný řádek vám poskytne čistý objekt, který můžete začít naplňovat nastavením. Představte si `gridOptions` jako ovládací panel pro každou funkci, kterou později povolíte.

### Co tím nastavujete

- **NumberFormatAlignment** – automaticky zarovnává číselné řetězce.
- **Pagination** – řídí velikost stránky a navigaci.
- **Sorting** – zapíná řazení sloupců.
- **Columns** – definuje hlavičky, datové typy a vlastní renderery.

Tyto vlastnosti můžete přidat před tím, než nakonec vytvoříte samotnou Grid.

---

## Krok 3: Zapnutí zarovnání čísel (častý požadavek)

Většina tabulek obsahuje směs textu a čísel. Ve výchozím nastavení Grid.js vše zarovnává doleva, což vypadá divně u finančních hodnot. Aby **konfigurovat možnosti mřížky v JavaScriptu** pro správné zarovnání, nastavte příznak `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Proč to zapnout? Když je příznak nastaven na `true`, Grid.js prozkoumá každou buňku; pokud vypadá jako číslo (např. „1234“, „12.34%“), automaticky ji zarovná vpravo. Tento malý zásah učiní zprávy mnohem čitelnějšími.

---

## Krok 4: Přidání stránkování a řazení

Reálná mřížka se zřídka vejde na jednu obrazovku. Zapneme stránkování (10 řádků na stránku) a umožníme uživatelům řadit libovolný sloupec.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Poznámka k okrajovým případům

Pokud později poskytnete vlastní zdroj dat, který už vrací stránkované výsledky, budete chtít vypnout vestavěné stránkování Grid.js, aby nedošlo k dvojitému stránkování. Stačí nastavit `gridOptions.Pagination.enabled = false;`.

---

## Krok 5: Definice sloupců a ukázkových dat

Nyní naplníme mřížku nějakými testovacími daty a řekneme jí, co každý sloupec představuje. Zde opravdu zazáří vzor **create gridjsoptions instance** – vše žije v jednom přehledném objektu.

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

Všimněte si, že hodnoty `id` sloupců jsou shodné s klíči v každém datovém objektu. Tento konvence umožňuje Grid.js automaticky mapovat hodnoty, čímž se vyhnete psaní vlastního formátoru pro každý sloupec.

---

## Krok 6: Vytvoření Grid s našimi možnostmi

Nakonec **konfigurujeme možnosti mřížky v JavaScriptu** předáním objektu `gridOptions` konstruktoru Grid. Mřížka se vykreslí uvnitř `<div id="grid-wrapper">`, který jsme připravili dříve.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

A to je vše. Celý proces – od **create gridjsoptions instance** po vykreslení – zabere méně než minutu kódování.

### Očekávaný výstup

Po otevření HTML souboru v prohlížeči byste měli vidět:

- Hlavičkový řádek s „ID“, „Employee“, „Salary ($)“, „Dept.“.
- Čísla ve sloupci platů zarovnaná vpravo (díky `NumberFormatAlignment`).
- Ovládací prvky stránkování ve spodní části (pokud máte více než deset řádků).
- Klikatelné hlavičky sloupců, které řadí vzestupně/sestupně.

Pokud něco vypadá špatně, otevřete konzoli prohlížeče (F12) a podívejte se na chybové zprávy – většina chyb pramení z nesouladu ID sloupců nebo chybějících skriptů knihovny.

---

## Krok 7: Pokročilé úpravy (volitelné)

Níže najdete několik rychlých nápadů, které můžete vyzkoušet, jakmile základní mřížka funguje.

| Funkce | Jak povolit | Proč to pomáhá |
|---------|---------------|--------------|
| **Vlastní renderer buňky** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Zvýrazní platy tučně. |
| **Vyhledávací lišta** | `gridOptions.Search = true;` | Umožní uživatelům okamžitě filtrovat řádky. |
| **Data na straně serveru** | `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Škáluje na tisíce řádků. |
| **Přepínání tématu** | `gridOptions.ClassName = "gridjs-theme-dark";` | Ladí se s designy v tmavém režimu. |

Klidně kombinujte – Grid.js je záměrně flexibilní. Jen nezapomeňte ponechat původní řádek **create gridjsoptions instance** na začátku; všechny další úpravy na něm závisí.

---

## Závěr

Právě jsme prošli kompletním pracovním postupem, jak **vytvořit instanci GridJsOptions** a **konfigurovat možnosti mřížky v JavaScriptu** pro funkční, řaditelnou a stránkovanou datovou tabulku. Začali jsme s čistou HTML stránkou, načetli knihovnu, sestavili objekt nastavení, zapnuli zarovnání čísel, přidali stránkování, definovali sloupce a nakonec vykreslili mřížku.

Od sem můžete:

- Nahradit statické `sampleData` AJAX voláním.
- Přidat vlastní formátování pro data, měny nebo ikony.
- Integrovat mřížku do frameworku jako React nebo Vue (stejný objekt `gridOptions` funguje i tam).

Možnosti jsou prakticky neomezené a vzor, který jsme použili – centralizace všech nastavení v jediné instanci `GridJsOptions` – udržuje váš kód čistý a udržovatelný.

Máte případ, o kterém si nejste jisti? Zanechte komentář a podíváme se na to společně. Šťastné kódování a užívejte si tvorbu dynamických tabulek s Grid.js!

## Co se naučíte dál?

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}