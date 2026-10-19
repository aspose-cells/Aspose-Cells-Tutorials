---
category: general
date: 2026-06-21
description: Maak een interactieve datagrid met Grid.js en leer hoe je een JSON‑datatabel
  kunt weergeven met sorteren, paginering en zoeken. Perfect voor webdashboards.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: nl
og_description: Maak in enkele minuten een interactieve data‑grid. Leer hoe je Grid.js
  kunt gebruiken om een JSON‑datatabel weer te geven met paginering, sortering en
  zoeken.
og_title: Maak een interactieve datagrid met Grid.js – Complete tutorial
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
title: Maak een interactieve datagrid met Grid.js – Volledige stapsgewijze handleiding
url: /nl/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een interactieve gegevensraster met Grid.js – Volledige stapsgewijze handleiding

Heb je je ooit afgevraagd hoe je een **interactief gegevensraster** kunt **maken** dat gebruikers laat sorteren, zoeken en door de rijen kan bladeren zonder een backend te schrijven? Je bent niet de enige. In veel dashboards is het grootste pijnpunt het omzetten van een statische JSON‑dump naar een slank, doorzoekbaar tabel—iets dat aanvoelt als een spreadsheet maar volledig in de browser draait.

In deze tutorial lopen we stap voor stap door **hoe je Grid.js gebruikt** om een **JSON‑gegevens tabel** weer te geven op een eenvoudige HTML‑pagina. Aan het einde heb je een werkend voorbeeld dat je in elk project kunt gebruiken, plus tips voor het aanpassen van de werkbalk, het verwerken van grote datasets en het vermijden van veelvoorkomende valkuilen.

## Wat je zult leren

- Hoe je een JSON‑bestand ophaalt dat kolommen en rijen definieert.
- Hoe je **Grid.js** initialiseert met paginering, sortering, zoeken en een aangepaste werkbalk.
- Hoe je het raster rendert in een doelcontainer.
- Optionele aanpassingen: aangepaste celopmaak, thema‑wissel en foutafhandeling.
- Een compleet, kant‑klaar code‑voorbeeld.

### Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

1. Een moderne browser (Chrome, Edge of Firefox) – Grid.js maakt gebruik van ES6‑functies.
2. Een lokale of externe map met een `grid_data.json`‑bestand (we laten het formaat zien).
3. Basiskennis van HTML en JavaScript – niets bijzonders, alleen het vermogen om een `.html`‑bestand in een browser te openen.

Geen build‑tools, geen npm‑installatie, geen server‑side code. Dat is het mooie van **interactief gegevensraster maken** met Grid.js: het werkt direct vanaf een CDN.

---

## Stap 1: Bereid de JSON voor die je tabel definieert

The first thing you need is a JSON payload that tells Grid.js what columns exist and what rows to show. Think of it as the blueprint for your **display JSON data table**. Here’s a minimal example you can save as `grid_data.json` in the same directory as your HTML file:

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

*Waarom dit formaat?* Grid.js verwacht dat `columns` een array van strings is (of objecten voor geavanceerde configuratie) en dat `rows` een array van arrays is waarbij elke binnenste array overeenkomt met de kolomvolgorde. Je kunt uiteraard meer kolommen of geneste objecten toevoegen – Grid.js zal ze weergeven zolang de structuren overeenkomen.

> **Pro tip:** Als je gegevens van een API haalt, vervang dan gewoon de statische `fetch('grid_data.json')` door je endpoint‑URL. De rest van de code blijft hetzelfde.

---

## Stap 2: Initialise Grid.js – Het hart van **hoe je gridjs gebruikt**

Nu de gegevensbron klaar is, moeten we Grid.js op de pagina brengen en vertellen hoe het zich moet gedragen. Dit is waar we daadwerkelijk **interactieve gegevensraster** functionaliteit implementeren, zoals paginering, sortering en een handige werkbalkknop.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

De CDN levert de nieuwste stabiele versie, en het Meri­maid‑thema voegt een nette, moderne uitstraling toe direct uit de doos. Je kunt het vervangen door `gridjs.min.css` als je de standaardstijl verkiest.

Next, inside a `<script>` tag, fetch the JSON and initialise the grid:

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

### De opties ontleden

| Optie | Wat het doet | Waarom het belangrijk is |
|-------|--------------|--------------------------|
| `pagination` | Verdeelt rijen over pagina's (standaard 10 per pagina) | Houdt grote tabellen bruikbaar zonder de UI te overweldigen. |
| `sort` | Klikbare kolomkoppen schakelen tussen oplopende/aflopende volgorde | Gebruikers kunnen snel de rijen met de hoogste waarden vinden. |
| `search` | Voegt een tekstinvoer toe die rijen realtime filtert | Ideaal voor ad‑hoc zoekopdrachten zonder data opnieuw te laden. |
| `toolbar` | Voegt aangepaste knoppen of dropdowns toe boven het raster | Perfect voor “Help”, “Export” of “Vernieuwen” acties. |
| `formatter` | Staat toe ruwe HTML voor een cel terug te geven | Hier zetten we e‑mailstrings om in klikbare mailto‑links. |

> **Waarom deze aanpak?** Door de rasterconfiguratie declaratief te houden, kun je het gedrag eenvoudig aanpassen zonder de kern‑renderlogica aan te raken. Dit is de aanbevolen manier om **Grid.js te gebruiken** voor de meeste projecten.

---

## Stap 3: Render het raster in je pagina

The last line of the script—`grid.render(document.getElementById('grid-container'))`—injects the fully‑functional table into a `<div>` you’ve placed somewhere in your HTML body:

```html
<div id="grid-container"></div>
```

Dat is alles. Wanneer de pagina laadt, haalt de browser de JSON op, bouwt de Grid.js‑instantie en tekent de interactieve tabel op het scherm. Geen verversingen, geen server‑aanvragen na de eerste lading.

---

## Optioneel: Styling‑ en themawijzigingen

If the default Meri­maid theme isn’t your cup of tea, you can swap it for any of the built‑in themes (`gridjs.min.css`) or write your own CSS. For example, to make the header background a soft gray:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Add the snippet inside a `<style>` tag or an external stylesheet. Grid.js respects standard CSS selectors, so you have full control over fonts, colors, and spacing.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Valkuil | Symptoom | Oplossing |
|---------|----------|-----------|
| **CORS‑fouten** bij het ophalen van JSON van een ander domein | Browserconsole toont ‘Blocked by CORS policy’ | Host de JSON op dezelfde origin of schakel CORS in op de server. |
| **Grote datasets veroorzaken vertraging** | Scrollen wordt haperig, paginering traag | Gebruik `server`‑paginering (`pagination: { server: { url: (prev, page, limit) => … } }`) of lazy‑load rijen. |
| **Werkbalkknop verschijnt niet** | Geen knop zichtbaar ondanks `toolbar.enabled: true` | Zorg dat je Grid.js versie 2.0+ gebruikt; oudere versies hadden een andere werkbalk‑API. |
| **E‑maillinks niet klikbaar** | Formatter geeft platte tekst terug | Retourneer `gridjs.html(...)` in plaats van een gewone string, zoals in het voorbeeld. |

Het vroeg aanpakken van deze problemen bespaart je later uren aan debuggen.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren en plakken)

Below is the complete HTML file that you can save as `index.html`. Open it in a browser, and you’ll see a fully functional **interactieve gegevensraster** demo that **JSON‑gegevens tabel** with sorting, searching, and a help button.

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


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe maak je een Excel-gegevensvalidatielijst met Aspose.Cells voor Java: Een stapsgewijze handleiding](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Hoe maak je selectievakjes in Excel met Aspose.Cells voor .NET | Gegevensvalidatie‑tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [XML‑gegevens maken & importeren in Excel met Aspose.Cells voor Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}