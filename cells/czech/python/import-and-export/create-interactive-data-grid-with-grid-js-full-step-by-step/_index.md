---
category: general
date: 2026-06-21
description: Vytvořte interaktivní datovou mřížku pomocí Grid.js a naučte se, jak
  zobrazit tabulku JSON dat s řazením, stránkováním a vyhledáváním. Ideální pro webové
  dashboardy.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: cs
og_description: Vytvořte interaktivní datovou mřížku během několika minut. Naučte
  se, jak použít Grid.js k zobrazení tabulky JSON dat s stránkováním, řazením a vyhledáváním.
og_title: Vytvořte interaktivní datovou mřížku pomocí Grid.js – kompletní tutoriál
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
title: Vytvořte interaktivní datovou mřížku pomocí Grid.js – Kompletní průvodce krok
  za krokem
url: /cs/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte interaktivní datovou mřížku pomocí Grid.js – Kompletní průvodce krok za krokem

Už jste se někdy zamýšleli, jak **vytvořit interaktivní datovou mřížku**, která uživatelům umožní řadit, vyhledávat a stránkovat řádky bez psaní backendu? Nejste v tom sami. V mnoha řídicích panelech je největším problémem převést statický výpis JSON do elegantní, prohledávatelné tabulky – něco, co se cítí jako tabulkový procesor, ale běží úplně v prohlížeči.

V tomto tutoriálu vás provedeme **jak používat Grid.js** k **zobrazení JSON datové tabulky** na jednoduché HTML stránce. Na konci budete mít funkční příklad, který můžete vložit do jakéhokoli projektu, plus tipy na přizpůsobení panelu nástrojů, práci s velkými datovými sadami a vyhýbání se běžným úskalím.

## Co se naučíte

- Jak načíst JSON soubor, který definuje sloupce a řádky.
- Jak inicializovat **Grid.js** s stránkováním, řazením, vyhledáváním a vlastním panelem nástrojů.
- Jak vykreslit mřížku do cílového kontejneru.
- Volitelné úpravy: vlastní formátování buněk, přepínání témat a zpracování chyb.
- Kompletní, připravený k zkopírování kódový příklad.

### Požadavky

Než se ponoříme, ujistěte se, že máte:

1. Moderní prohlížeč (Chrome, Edge nebo Firefox) – Grid.js spoléhá na funkce ES6.
2. Lokální nebo vzdálenou složku obsahující soubor `grid_data.json` (ukážeme formát).
3. Základní znalost HTML a JavaScriptu – nic složitého, jen schopnost otevřít soubor `.html` v prohlížeči.

Žádné nástroje pro sestavení, žádná instalace npm, žádný server‑side kód. To je krása **vytvoření interaktivní datové mřížky** s Grid.js: funguje přímo z CDN.

---

## Krok 1: Připravte JSON, který definuje vaši tabulku

Prvním, co potřebujete, je JSON payload, který Grid.js říká, jaké sloupce existují a jaké řádky zobrazit. Považujte ho za plán pro vaši **zobrazení JSON datové tabulky**. Zde je minimální příklad, který můžete uložit jako `grid_data.json` ve stejném adresáři jako váš HTML soubor:

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

*Proč tento formát?* Grid.js očekává, že `columns` bude pole řetězců (nebo objektů pro pokročilou konfiguraci) a `rows` bude pole polí, kde každé vnitřní pole odpovídá pořadí sloupců. Samozřejmě můžete přidat další sloupce nebo vnořené objekty – Grid.js je vykreslí, pokud se struktury shodují.

> **Tip:** Pokud načítáte data z API, stačí nahradit statické `fetch('grid_data.json')` URL vašeho koncového bodu. Zbytek kódu zůstane stejný.

---

## Krok 2: Inicializujte Grid.js – Srdce **jak používat gridjs**

Nyní, když je zdroj dat připraven, musíme přenést Grid.js na stránku a říct mu, jak se má chovat. Zde skutečně **vytvoříme interaktivní datovou mřížku** s funkcemi jako stránkování, řazení a praktické tlačítko v panelu nástrojů.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN vám poskytuje nejnovější stabilní verzi a téma Mermaid přidává čistý, moderní vzhled hned po vybalení. Můžete jej vyměnit za `gridjs.min.css`, pokud dáváte přednost výchozímu stylování.

Dále, uvnitř značky `<script>`, načtěte JSON a inicializujte mřížku:

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

### Rozbor možností

| Možnost | Co dělá | Proč je důležité |
|--------|--------------|----------------|
| `pagination` | Rozděluje řádky do stránek (výchozí 10 na stránku) | Udržuje velké tabulky použitelné, aniž by zahltil UI. |
| `sort` | Klikatelné záhlaví sloupců přepínají vzestupné/podřadné pořadí | Uživatelé mohou rychle najít řádky s nejvyššími hodnotami. |
| `search` | Přidá textové pole, které filtruje řádky za běhu | Skvělé pro ad‑hoc vyhledávání bez nutnosti znovu načítat data. |
| `toolbar` | Přidá vlastní tlačítka nebo rozbalovací seznamy nad mřížkou | Ideální pro akce jako „Nápověda“, „Export“ nebo „Obnovit“. |
| `formatter` | Umožňuje vrátit surové HTML pro buňku | Zde převádíme řetězce e‑mailu na klikatelné mailto odkazy. |

> **Proč tento přístup?** Tím, že udržujete konfiguraci mřížky deklarativní, můžete snadno upravit chování, aniž byste zasahovali do hlavní logiky vykreslování. Toto je doporučený způsob **jak používat Grid.js** pro většinu projektů.

---

## Krok 3: Vykreslete mřížku na vaši stránku

Poslední řádek skriptu—`grid.render(document.getElementById('grid-container'))`—vloží plně funkční tabulku do `<div>`, který jste umístili někde v těle HTML:

```html
<div id="grid-container"></div>
```

To je vše. Když se stránka načte, prohlížeč načte JSON, vytvoří instanci Grid.js a vykreslí interaktivní tabulku na obrazovku. Žádné obnovení, žádné volání serveru po počátečním načtení.

---

## Volitelné: Úpravy stylování a tématu

Pokud vám výchozí téma Mermaid nevyhovuje, můžete jej vyměnit za kterékoliv z vestavěných témat (`gridjs.min.css`) nebo napsat vlastní CSS. Například, jak nastavit pozadí záhlaví na jemnou šedou:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Vložte úryvek do značky `<style>` nebo externího stylového souboru. Grid.js respektuje standardní CSS selektory, takže máte plnou kontrolu nad fonty, barvami a rozestupy.

---

## Běžná úskalí a jak se jim vyhnout

| Úskalí | Příznak | Řešení |
|---------|---------|-----|
| **CORS errors** při načítání JSON z jiné domény | Konzole prohlížeče ukazuje „Blocked by CORS policy“ | Umístěte JSON na stejný původ nebo povolte CORS na serveru. |
| **Velké datové sady způsobují zpoždění** | Posouvání se stává trhaným, stránkování pomalé | Použijte serverové stránkování (`pagination: { server: { url: (prev, page, limit) => … } }`) nebo lazy‑load řádky. |
| **Tlačítko v panelu nástrojů se nezobrazuje** | Žádné tlačítko není viditelné i přes `toolbar.enabled: true` | Ujistěte se, že používáte Grid.js verze 2.0+; starší verze měly odlišné API panelu nástrojů. |
| **Odkazy na e‑mail nejsou klikatelné** | Formátovač vrací prostý text | Vraťte `gridjs.html(...)` místo prostého řetězce, jak je ukázáno v příkladu. |

Řešení těchto problémů včas vám ušetří hodiny ladění později.

---

## Kompletní funkční příklad (připravený ke kopírování)

Níže je kompletní HTML soubor, který můžete uložit jako `index.html`. Otevřete jej v prohlížeči a uvidíte plně funkční demo **vytvoření interaktivní datové mřížky**, která **zobrazuje JSON datovou tabulku** s řazením, vyhledáváním a tlačítkem nápovědy.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit seznam validace dat v Excelu pomocí Aspose.Cells pro Java: Průvodce krok za krokem](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Jak vytvořit zaškrtávací políčka v Excelu pomocí Aspose.Cells pro .NET | Tutoriál o validaci dat](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Vytvoření a import XML dat do Excelu pomocí Aspose.Cells pro Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}