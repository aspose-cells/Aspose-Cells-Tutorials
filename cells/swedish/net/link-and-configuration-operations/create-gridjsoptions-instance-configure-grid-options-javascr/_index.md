---
category: general
date: 2026-05-30
description: Lär dig hur du skapar en GridJsOptions‑instans och konfigurerar grid‑alternativ
  i JavaScript för dynamiska tabeller. Steg‑för‑steg‑guide med fullständig kod.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: sv
og_description: Skapa en GridJsOptions‑instans och konfigurera gridalternativ i JavaScript
  på några minuter. Fullständigt exempel, förklaringar och bästa praxis‑tips.
og_title: Skapa GridJsOptions‑instans – Konfigurera Grid Options i JavaScript
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
title: Skapa GridJsOptions‑instans – Konfigurera Grid Options JavaScript
url: /sv/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa GridJsOptions-instans – Konfigurera Grid Options JavaScript

Har du någonsin funderat på hur man **create GridJsOptions instance** utan att leta igenom spridda dokument? Du är inte ensam. När du behöver en snygg, sorteringsbar tabell på en webbsida är det första steget att behärska hur du **configure grid options JavaScript** för ett polerat UI.

I den här handledningen går vi igenom exakt den kod du behöver, förklarar varför varje inställning är viktig och visar ett komplett, körbart exempel. I slutet kommer du att känna dig bekväm med att skapa GridJsOptions-instans, justera justering, paginering och till och med anpassade cellrenderare – allt med ren JavaScript.

## Vad du kommer att lära dig

- Hur man **create GridJsOptions instance** från början.
- De viktigaste egenskaperna som låter dig **configure grid options JavaScript** (sortering, paginering, talformattering osv.).
- Vanliga fallgropar (t.ex. blandning av sträng- och numeriska typer) och hur du undviker dem.
- En fullständig HTML-sida som du kan kopiera‑klistra in i vilket projekt som helst och se resultat omedelbart.

### Förutsättningar

- En modern webbläsare (Chrome, Edge, Firefox) – inga byggverktyg krävs.
- Grundläggande kunskap om JavaScript (variabler, objekt, DOM).
- Grid.js-biblioteket (vi hämtar det från en CDN).

Om någon av dessa känns obekant, panik inte – varje steg innehåller en snabb genomgång.

---

## Steg 1: Ladda Grid.js och förbered HTML-skelettet

Innan vi kan **create GridJsOptions instance** behöver vi själva biblioteket. Det enklaste sättet är att använda den officiella CDN:n. Nedan är ett minimalt HTML-skelett som också reserverar en `<div>` där rutnätet kommer att renderas.

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

> **Pro tip:** Behåll CSS‑länken före dina egna stilar så att gridens standardtema laddas korrekt.

### Varför detta är viktigt

Att ladda biblioteket från en CDN säkerställer att du alltid får den senaste stabila versionen utan en lokal installation. `<div id="grid-wrapper">` är platshållaren som Grid.js‑konstruktorn kommer att rikta in sig på när vi **configure grid options JavaScript**.

## Steg 2: Skapa en ny GridJsOptions-instans

Nu kommer hjärtat av handledningen: raden som faktiskt **creates GridJsOptions instance**. I en separat fil som heter `grid-config.js` (refererad i HTML‑koden ovan) kommer vi att skriva:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Den enda raden ger dig ett rent objekt som du kan börja fylla med inställningar. Tänk på `gridOptions` som kontrollpanelen för varje funktion du senare kommer att aktivera.

### Vad du konfigurerar

- **NumberFormatAlignment** – justerar numeriska strängar automatiskt.
- **Pagination** – styr sidstorlek och navigering.
- **Sorting** – växlar kolumnsortering.
- **Columns** – definierar rubriker, datatyper och anpassade renderare.

Du kan lägga till någon av dessa egenskaper innan du slutligen instansierar själva Grid.

## Steg 3: Aktivera nummerjustering (ett vanligt krav)

De flesta tabeller innehåller en blandning av text och siffror. Som standard justerar Grid.js allt åt vänster, vilket ser konstigt ut för monetära värden. För att **configure grid options JavaScript** för korrekt justering, sätt `NumberFormatAlignment`‑flaggan:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Varför aktivera detta? När flaggan är sann inspekterar Grid.js varje cell; om den ser ut som ett tal (t.ex. “1234”, “12.34%”) justeras den automatiskt åt höger. Denna lilla justering gör rapporter mycket mer läsbara.

## Steg 4: Lägg till paginering och sortering

Ett verkligt rutnät får sällan plats på en enda skärm. Låt oss slå på paginering (10 rader per sida) och låta användare sortera vilken kolumn som helst.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Notering om edge‑case

Om du senare tillhandahåller en anpassad datakälla som redan returnerar paginerade resultat, vill du inaktivera Grid.js inbyggda paginering för att undvika dubbel paginering. Sätt helt enkelt `gridOptions.Pagination.enabled = false;`.

## Steg 5: Definiera kolumner och exempeldata

Nu matar vi rutnätet med lite testdata och berättar vad varje kolumn representerar. Det är här **create gridjsoptions instance**‑mönstret verkligen lyser – allt lever i ett prydligt objekt.

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

Observera att vi behåller kolumn‑`id`‑värdena identiska med nycklarna i varje dataobjekt. Denna konvention låter Grid.js mappa värden automatiskt, vilket sparar dig från att skriva en anpassad formatterare för varje kolumn.

## Steg 6: Instansiera Grid med våra alternativ

Vi **configure grid options javascript** slutligen genom att skicka `gridOptions`‑objektet till Grid‑konstruktorn. Rutnätet kommer att renderas i `<div id="grid-wrapper">` som vi förberedde tidigare.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Det är allt. Hela processen – från **create gridjsoptions instance** till rendering – tar mindre än en minut kodning.

### Förväntat resultat

När du öppnar HTML‑filen i en webbläsare bör du se:

- En rubrikrad med “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Högerjusterade lönenummer (tack vare `NumberFormatAlignment`).
- Pagineringkontroller längst ner (om du har lagt till fler än tio rader).
- Klickbara kolumnrubriker som sorterar stigande/avtagande.

Om något ser felaktigt ut, öppna webbläsarens konsol (F12) och leta efter felmeddelanden – de flesta buggar beror på felaktiga kolumn‑ID:n eller saknade biblioteks‑skript.

## Steg 7: Avancerade justeringar (valfritt)

Nedan är några snabba idéer du kan experimentera med när det grundläggande rutnätet fungerar.

| Funktion | Så aktiverar du | Varför det hjälper |
|---------|---------------|--------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Markera löner i fetstil. |
| **Search bar** | `gridOptions.Search = true;` | Låter användare filtrera rader omedelbart. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Skalbar till tusentals rader. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Passar mörkt läge‑designer. |

Känn dig fri att blanda och matcha – Grid.js är avsiktligt flexibelt. Kom bara ihåg att behålla den ursprungliga **create gridjsoptions instance**‑raden högst upp; alla senare justeringar bygger på det enda objektet.

## Slutsats

Vi har just gått igenom ett komplett arbetsflöde för att **create GridJsOptions instance** och **configure grid options JavaScript** för en funktionell, sorteringsbar och paginerad datatabell. Med en enkel HTML‑sida laddade vi biblioteket, byggde ett options‑objekt, aktiverade numerisk justering, lade till paginering, definierade kolumner och renderade slutligen rutnätet.

Från och med nu kan du:

- Ersätt den statiska `sampleData` med ett AJAX‑anrop.
- Lägg till anpassade formatterare för datum, valutor eller ikoner.
- Integrera rutnätet i ett ramverk som React eller Vue (samma `gridOptions`‑objekt fungerar där också).

Möjligheterna är praktiskt taget oändliga, och mönstret vi använde – att centralisera alla inställningar i en enda `GridJsOptions`‑instans – håller din kod ren och underhållbar.

Har du ett användningsfall du är osäker på? Lämna en kommentar så utforskar vi det tillsammans. Lycka till med kodandet, och njut av att bygga dynamiska tabeller med Grid.js!

## Vad bör du lära dig härnäst?

- [Hur man skapar och konfigurerar Excel-arbetsböcker med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hur man skapar och formaterar Excel-tabeller med Aspose.Cells för .NET | Steg‑för‑steg‑guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Hur man skapar och formaterar Excel-celler med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}