---
category: general
date: 2026-06-21
description: Skapa ett interaktivt datagrid med Grid.js och lär dig hur du visar en
  JSON-datatabell med sortering, paginering och sökning. Perfekt för webb‑dashboards.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: sv
og_description: Skapa interaktivt datagrid på några minuter. Lär dig hur du använder
  Grid.js för att visa en JSON-datatabell med paginering, sortering och sökning.
og_title: Skapa interaktivt datagrid med Grid.js – Komplett handledning
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
title: Skapa interaktivt datagrid med Grid.js – Fullständig steg‑för‑steg‑guide
url: /sv/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa interaktivt datagrid med Grid.js – Fullständig steg‑för‑steg‑guide

Har du någonsin undrat hur man **skapar interaktivt datagrid** som låter användare sortera, söka och bläddra genom rader utan att skriva ett backend? Du är inte ensam. I många instrumentpaneler är den största smärtan att omvandla en statisk JSON‑dump till ett slimmat, sökbart bord—något som känns lika smidigt som ett kalkylblad men körs helt i webbläsaren.

I den här handledningen går vi igenom **hur man använder Grid.js** för att **visa JSON‑datatabell** på en enkel HTML‑sida. I slutet har du ett fungerande exempel som du kan lägga in i vilket projekt som helst, samt tips för att anpassa verktygsfältet, hantera stora datamängder och undvika vanliga fallgropar.

## Vad du kommer att lära dig

- Hur man hämtar en JSON‑fil som definierar kolumner och rader.
- Hur man initierar **Grid.js** med paginering, sortering, sökning och ett anpassat verktygsfält.
- Hur man renderar gridet i en målbehållare.
- Valfria justeringar: anpassad cellformatering, temabyte och felhantering.
- Ett komplett, kopiera‑och‑klistra‑klart kodexempel.

### Förutsättningar

Innan vi dyker ner, se till att du har:

1. En modern webbläsare (Chrome, Edge eller Firefox) – Grid.js förlitar sig på ES6‑funktioner.
2. En lokal eller fjärrmapp som innehåller en `grid_data.json`‑fil (vi visar formatet).
3. Grundläggande kunskap om HTML och JavaScript – inget avancerat, bara förmågan att öppna en `.html`‑fil i en webbläsare.

Inga byggverktyg, ingen npm‑install, ingen server‑kod. Det är fördelarna med **skapa interaktivt datagrid** med Grid.js: det fungerar direkt från ett CDN.

---

## Steg 1: Förbered JSON‑filen som definierar ditt bord

Det första du behöver är en JSON‑payload som talar om för Grid.js vilka kolumner som finns och vilka rader som ska visas. Tänk på det som ritningen för din **visa JSON‑datatabell**. Här är ett minimalt exempel som du kan spara som `grid_data.json` i samma katalog som din HTML‑fil:

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

*Varför detta format?* Grid.js förväntar sig att `columns` är en array av strängar (eller objekt för avancerad konfiguration) och att `rows` är en array av arrayer där varje inre array matchar kolumnordningen. Du kan naturligtvis lägga till fler kolumner eller nästlade objekt – Grid.js kommer att rendera dem så länge strukturerna stämmer.

> **Proffstips:** Om du hämtar data från ett API, ersätt bara den statiska `fetch('grid_data.json')` med din endpoint‑URL. Resten av koden förblir densamma.

---

## Steg 2: Initiera Grid.js – Kärnan i **how to use gridjs**

Nu när datakällan är klar måste vi lägga in Grid.js på sidan och berätta hur den ska fungera. Här är där vi faktiskt **skapar interaktivt datagrid**‑funktionalitet som paginering, sortering och en praktisk verktygsfältsknapp.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN‑en ger dig den senaste stabila versionen, och Meri­maid‑temat lägger till ett rent, modernt utseende direkt. Du kan byta ut det mot `gridjs.min.css` om du föredrar standardstilen.

Nästa steg, inuti en `<script>`‑tagg, hämta JSON‑filen och initiera gridet:

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

### Genomgång av alternativen

| Alternativ | Vad den gör | Varför det är viktigt |
|------------|-------------|-----------------------|
| `pagination` | Delar upp rader i sidor (standard 10 per sida) | Håller stora tabeller användbara utan att överväldiga UI‑t. |
| `sort` | Klickbara kolumnrubriker växlar mellan stigande/avtagande ordning | Användare kan snabbt hitta rader med högst värde. |
| `search` | Lägger till ett textfält som filtrerar rader i realtid | Perfekt för ad‑hoc‑sökningar utan att ladda om data. |
| `toolbar` | Lägger till anpassade knappar eller rullgardinsmenyer ovanför gridet | Perfekt för “Help”, “Export” eller “Refresh”-åtgärder. |
| `formatter` | Låter dig returnera rå HTML för en cell | Här omvandlar vi e‑poststrängar till klickbara mailto‑länkar. |

> **Varför detta tillvägagångssätt?** Genom att hålla grid‑konfigurationen deklarativ kan du enkelt justera beteendet utan att röra den centrala renderingslogiken. Detta är det rekommenderade sättet att **how to use Grid.js** för de flesta projekt.

---

## Steg 3: Rendera gridet på din sida

Den sista raden i skriptet—`grid.render(document.getElementById('grid-container'))`—injicerar den fullt funktionella tabellen i en `<div>` som du har placerat någonstans i ditt HTML‑body:

```html
<div id="grid-container"></div>
```

Det är allt. När sidan laddas hämtar webbläsaren JSON‑filen, bygger Grid.js‑instansen och ritar det interaktiva bordet på skärmen. Inga omladdningar, inga serveranrop efter den initiala laddningen.

---

## Valfritt: Styling‑ och temajusteringar

Om standardtemat Meri­maid inte är din kopp te, kan du byta det mot något av de inbyggda temana (`gridjs.min.css`) eller skriva din egen CSS. Till exempel, för att göra rubrikens bakgrund till en mjuk grå:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Lägg till kodsnutten i en `<style>`‑tagg eller ett externt stylesheet. Grid.js respekterar standard‑CSS‑selektorer, så du har full kontroll över typsnitt, färger och avstånd.

---

## Vanliga fallgropar & hur man undviker dem

| Fallgrop | Symptom | Lösning |
|----------|---------|---------|
| **CORS‑fel** när JSON hämtas från en annan domän | Webbläsarkonsolen visar “Blocked by CORS policy” | Värd JSON‑filen på samma origin eller aktivera CORS på servern. |
| **Stora datamängder orsakar fördröjning** | Rullning blir hackig, paginering långsam | Använd server‑paginering (`pagination: { server: { url: (prev, page, limit) => … } }`) eller lazy‑load rader. |
| **Verktygsfältsknapp visas inte** | Ingen knapp synlig trots `toolbar.enabled: true` | Säkerställ att du använder Grid.js version 2.0+; äldre versioner hade ett annat verktygsfälts‑API. |
| **E‑postlänkar är inte klickbara** | Formatter returnerar vanlig text | Returnera `gridjs.html(...)` istället för en vanlig sträng, som i exemplet. |

Att åtgärda dessa problem tidigt sparar dig timmar av felsökning senare.

---

## Fullt fungerande exempel (Kopiera‑och‑klistra‑klart)

Nedan är den kompletta HTML‑filen som du kan spara som `index.html`. Öppna den i en webbläsare, så ser du en fullt funktionell **create interactive data grid**‑demo som **display JSON data table** med sortering, sökning och en hjälpknapp.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}