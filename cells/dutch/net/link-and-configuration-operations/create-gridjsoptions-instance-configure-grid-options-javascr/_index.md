---
category: general
date: 2026-05-30
description: Leer hoe je een GridJsOptions‑instantie maakt en de grid‑opties in JavaScript
  configureert voor dynamische tabellen. Stapsgewijze handleiding met volledige code.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: nl
og_description: Maak een GridJsOptions‑instantie aan en configureer grid‑opties in
  JavaScript binnen enkele minuten. Volledig voorbeeld, uitleg en best‑practice‑tips.
og_title: Maak GridJsOptions‑instantie – Configureer Grid‑opties JavaScript
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
title: Maak GridJsOptions‑instantie – Configureer Grid‑opties JavaScript
url: /nl/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak GridJsOptions‑instantie – Configureer Grid‑opties JavaScript

Heb je je ooit afgevraagd hoe je een **GridJsOptions‑instantie** kunt **maken** zonder door verspreide documentatie te hoeven zoeken? Je bent niet de enige. Wanneer je een strakke, sorteerbare tabel op een webpagina nodig hebt, is het beheersen van het configureren van grid‑opties JavaScript de eerste stap naar een gepolijste UI.

In deze tutorial lopen we stap voor stap de exacte code door die je nodig hebt, leggen we uit waarom elke instelling belangrijk is, en laten we je een volledig, uitvoerbaar voorbeeld zien. Aan het einde kun je moeiteloos een GridJsOptions‑instantie maken, uitlijning, paginering en zelfs aangepaste cel‑renderers aanpassen – allemaal met gewone JavaScript.

## Wat je zult leren

- Hoe je een **GridJsOptions‑instantie** vanaf nul **maakt**.
- De belangrijkste eigenschappen die je in staat stellen **grid‑opties JavaScript te configureren** (sorteren, paginering, getal‑formattering, enz.).
- Veelvoorkomende valkuilen (bijv. het mengen van string‑ en numerieke types) en hoe je ze kunt vermijden.
- Een volledige HTML‑pagina die je kunt kopiëren‑plakken in elk project en direct resultaten ziet.

### Vereisten

- Een moderne browser (Chrome, Edge, Firefox) – geen build‑tools nodig.
- Basiskennis van JavaScript (variabelen, objecten, DOM).
- De Grid.js‑bibliotheek (we halen deze van een CDN).

Als een van deze onbekend klinkt, geen paniek – elke stap bevat een korte opfrisser.

---

## Stap 1: Laad Grid.js en bereid de HTML‑skelet voor

Voordat we een **GridJsOptions‑instantie** kunnen **maken**, hebben we de bibliotheek zelf nodig. De makkelijkste manier is via de officiële CDN. Hieronder staat een minimale HTML‑skelet die ook een `<div>` reserveert waar het raster wordt gerenderd.

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

> **Pro tip:** Plaats de CSS‑link vóór je eigen stijlen zodat het standaardthema van het raster correct wordt geladen.

### Waarom dit belangrijk is

Het laden van de bibliotheek vanaf een CDN zorgt ervoor dat je altijd de nieuwste stabiele versie krijgt zonder een lokale installatie. De `<div id="grid-wrapper">` is de placeholder die de Grid.js‑constructor zal targeten zodra we **grid‑opties JavaScript configureren**.

---

## Stap 2: Maak een nieuwe GridJsOptions‑instantie

Nu volgt het hart van de tutorial: de regel die daadwerkelijk een **GridJsOptions‑instantie** **maakt**. In een apart bestand genaamd `grid-config.js` (verwezen in de HTML hierboven) schrijven we:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Die ene regel geeft je een schoon object dat je kunt gaan vullen met instellingen. Beschouw `gridOptions` als het controlepaneel voor elke functie die je later inschakelt.

### Wat je aan het configureren bent

- **NumberFormatAlignment** – lijnt numerieke strings automatisch uit.
- **Pagination** – regelt paginagrootte en navigatie.
- **Sorting** – schakelt kolomsortering in of uit.
- **Columns** – definieert kopteksten, gegevenstypen en aangepaste renderers.

Je kunt elk van deze eigenschappen toevoegen voordat je uiteindelijk de Grid zelf instantiateert.

---

## Stap 3: Schakel getal‑uitlijning in (een veelvoorkomende eis)

De meeste tabellen bevatten een mix van tekst en cijfers. Standaard lijnt Grid.js alles links uit, wat er vreemd uitziet bij monetaire waarden. Om **grid‑opties JavaScript te configureren** voor juiste uitlijning, zet je de `NumberFormatAlignment`‑vlag:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Waarom dit inschakelen? Wanneer de vlag `true` is, inspecteert Grid.js elke cel; ziet het eruit als een getal (bijv. “1234”, “12.34%”), dan wordt het automatisch rechts uitgelijnd. Deze kleine aanpassing maakt rapporten veel leesbaarder.

---

## Stap 4: Voeg paginering en sortering toe

Een real‑world raster past zelden op één scherm. Laten we paginering inschakelen (10 rijen per pagina) en gebruikers toestaan elke kolom te sorteren.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Edge‑case opmerking

Als je later een aangepaste gegevensbron levert die al gepagineerde resultaten teruggeeft, wil je de ingebouwde paginering van Grid.js uitschakelen om dubbele paginering te voorkomen. Zet simpelweg `gridOptions.Pagination.enabled = false;`.

---

## Stap 5: Definieer kolommen en voorbeeldgegevens

Nu voeren we wat mock‑data in het raster en vertellen we wat elke kolom betekent. Dit is waar het **create gridjsoptions instance**‑patroon echt schittert – alles leeft in één net object.

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

Let op: we houden de kolom‑`id`‑waarden identiek aan de sleutels in elk gegevensobject. Deze conventie laat Grid.js waarden automatisch mappen, waardoor je geen aangepaste formatter voor elke kolom hoeft te schrijven.

---

## Stap 6: Instantieer de Grid met onze opties

We **configureren grid‑opties JavaScript** eindelijk door het `gridOptions`‑object aan de Grid‑constructor door te geven. Het raster wordt gerenderd binnen de `<div id="grid-wrapper">` die we eerder hebben voorbereid.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Dat is alles. Het volledige proces – van **create gridjsoptions instance** tot renderen – duurt minder dan een minuut coderen.

### Verwachte output

Wanneer je het HTML‑bestand in een browser opent, zie je:

- Een koprij met “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Rechts‑uitgelijnde salariscijfers (dankzij `NumberFormatAlignment`).
- Paginering‑besturingselementen onderaan (als je meer dan tien rijen hebt toegevoegd).
- Klikbare kolomkoppen die oplopend/aflopend sorteren.

Als er iets niet klopt, open dan de browser‑console (F12) en kijk naar foutmeldingen – de meeste bugs komen voort uit niet‑overeenkomende kolom‑ID’s of ontbrekende bibliotheek‑scripts.

---

## Stap 7: Geavanceerde tweaks (optioneel)

Hieronder een paar snelle ideeën die je kunt uitproberen zodra het basisraster werkt.

| Functie | Hoe in te schakelen | Waarom het helpt |
|---------|---------------------|-------------------|
| **Aangepaste cel‑renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Markeer salarissen vetgedrukt. |
| **Zoekbalk** | `gridOptions.Search = true;` | Laat gebruikers rijen direct filteren. |
| **Server‑side data** | `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Schaalbaar tot duizenden rijen. |
| **Thema‑wissel** | `gridOptions.ClassName = "gridjs-theme-dark";` | Past bij dark‑mode ontwerpen. |

Voel je vrij om te mixen en matchen – Grid.js is opzettelijk flexibel. Vergeet alleen niet de oorspronkelijke **create gridjsoptions instance**‑regel bovenaan; alle latere tweaks vertrouwen op dat ene object.

---

## Conclusie

We hebben zojuist een volledige workflow doorlopen om een **GridJsOptions‑instantie** te **maken** en **grid‑opties JavaScript te configureren** voor een functionele, sorteerbare en gepagineerde datatabel. Beginnend met een eenvoudige HTML‑pagina laadden we de bibliotheek, bouwden we een opties‑object, schakelden we numerieke uitlijning in, voegden we paginering toe, definieerden we kolommen en renderden we uiteindelijk het raster.

Vanaf hier kun je:

- De statische `sampleData` vervangen door een AJAX‑call.
- Aangepaste formatters toevoegen voor datums, valuta of iconen.
- Het raster integreren in een framework zoals React of Vue (hetzelfde `gridOptions`‑object werkt daar ook).

De mogelijkheden zijn praktisch eindeloos, en het patroon dat we gebruikten – alle instellingen centraliseren in één `GridJsOptions`‑instantie – houdt je code schoon en onderhoudbaar.

Heb je een use‑case waar je niet uitkomt? Laat een reactie achter, en we bekijken het samen. Veel plezier met coderen, en geniet van het bouwen van dynamische tabellen met Grid.js!

## Wat moet je hierna leren?

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}