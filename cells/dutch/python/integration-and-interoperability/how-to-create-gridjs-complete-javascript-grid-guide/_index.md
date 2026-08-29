---
category: general
date: 2026-06-30
description: Hoe maak je gridjs eenvoudig met een volledig JavaScript‑voorbeeld, inclusief
  gridjs‑configuratie, containerinstelling en renderproces.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: nl
og_description: Hoe maak je eenvoudig gridjs met een volledig JavaScript-voorbeeld,
  inclusief gridjs-configuratie, containerinstelling en renderproces.
og_title: Hoe maak je Gridjs – Complete JavaScript Gridgids
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Hoe maak je Gridjs – Complete JavaScript Grid-gids
url: /nl/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Gridjs te Maken – Complete JavaScript Grid Gids

Heb je je ooit afgevraagd **hoe je gridjs maakt** en direct een strakke datatabel op je pagina ziet? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze voor het eerst Gridjs proberen te integreren, vooral rond het configuratie‑object en de render‑aanroep. Het goede nieuws? Het is eigenlijk een eitje zodra je de juiste stappen kent.

In deze tutorial lopen we een real‑world voorbeeld door dat laat zien **hoe je gridjs maakt** vanaf nul, hoe je een juiste **gridjs configuratie** opstelt, hoe je het raster bindt aan een **gridjs container**, en tenslotte hoe je de **gridjs render** activeert. Aan het einde heb je een volledig functioneel raster dat je in elk project kunt gebruiken—geen mysterie, gewoon duidelijke code.

## Wat je zult leren

- Een minimale HTML‑pagina opzetten die klaar is voor Gridjs.
- Een **gridjs configuratie** object schrijven dat kolommen, data en opties definieert.
- De Gridjs‑instantie koppelen aan een **gridjs container** element.
- **gridjs render** aanroepen om de tabel weer te geven.
- Veelvoorkomende instellingen (paginering, sorteren, styling) aanpassen en typische valkuilen vermijden.

Er zijn geen externe build‑tools nodig; alles draait in de browser met één script‑tag. Laten we beginnen.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

1. Een moderne browser (Chrome, Edge, Firefox, Safari) – alles wat ES6 ondersteunt.
2. Basiskennis van HTML en JavaScript – je hebt geen framework nodig.
3. Toegang tot de Gridjs‑bibliotheek – we halen deze van een CDN, dus geen npm‑installatie nodig.

Dat is alles. Als je al een pagina hebt die je wilt verbeteren, kun je de fragmenten direct plakken.

## Stap 1: Voeg Gridjs‑assets toe aan je pagina

Eerst moeten we de CSS‑ en JavaScript‑bestanden van Gridjs laden. De CDN‑versie is lichtgewicht en perfect voor snelle demo’s.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** Het Mermaid‑thema geeft de tabel een schone, moderne uitstraling zonder extra CSS. Voel je vrij om het te vervangen door `classic.min.css` als je een andere stijl verkiest.

## Stap 2: Definieer de **gridjs container**

De **gridjs container** is gewoon een normale `<div>` die de gerenderde tabel host. In de markup hierboven hebben we al `<div id="grid"></div>` aangemaakt. Het `id`‑attribuut is cruciaal omdat we het later gebruiken om de Gridjs‑instantie te binden.

Als je meerdere rasters op dezelfde pagina nodig hebt, geef elke container een unieke ID (`grid1`, `grid2`, …) en herhaal de bind‑logica voor elk.

## Stap 3: Maak een **gridjs configuratie** Object

Nu komt het hart van **hoe je gridjs maakt** – de configuratie. Dit eenvoudige JavaScript‑object vertelt Gridjs welke kolommen getoond moeten worden, welke data ingevuld moet worden en welke functies ingeschakeld moeten worden.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Waarom deze configuratie belangrijk is

- **Columns** – definieer de header‑tekst en optionele breedte. Zonder dit zou Gridjs kolomnamen afleiden uit de eerste datarij, wat vaak minder leesbaar is.
- **Data** – een array van rijen, waarbij elke rij een array van celwaarden is. Je kunt ook een async‑functie leveren die data van een API ophaalt; de bibliotheek handelt promises automatisch af.
- **Pagination** – beperkt het aantal rijen per pagina, zodat enorme tabellen de UI niet overweldigen.
- **Search & Sort** – schakel interactieve functies in met één boolean, zodat je geen eigen handlers hoeft te schrijven.
- **Language** – pas UI‑teksten aan, perfect voor lokalisatie of branding.

Voel je vrij om later de statische data‑array te vervangen door een fetch‑aanroep; de rest van de stappen blijft exact hetzelfde.

## Stap 4: Instantieer Gridjs en bind aan de **gridjs container**

Met de configuratie klaar, maken we een nieuwe `GridJs.Grid` (de klassenaam is `gridjs.Grid` in de UMD‑build) en wijzen we deze toe aan ons container‑element.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Merk op dat we `document.getElementById('grid')` gebruiken – dat is de **gridjs container** die we eerder hebben gedefinieerd. Als je meerdere containers hebt, herhaal deze regel dan met de juiste ID.

## Stap 5: Activeer de **gridjs render**‑aanroep

Het laatste puzzelstukje is de **gridjs render**‑methode. Deze neemt de configuratie die we eerder hebben doorgegeven en injecteert een volledig gestylede `<table>` in de container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Dat is alles! Wanneer je de pagina in een browser opent, zie je een doorzoekbare, gepagineerde tabel met de vier rijen die we hebben gedefinieerd. Het zoekvak verschijnt automatisch bovenaan, en de pagineringsbesturingen staan onderaan.

### Verwachte output

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

De UI past zich aan wanneer je in het zoekvak typt of op kolomkoppen klikt om te sorteren.

## Veelvoorkomende variaties & randgevallen

### Data asynchroon laden

Als je data op een server staat, vervang dan de statische `data`‑array door een functie die een Promise retourneert:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs toont een laad‑spinner totdat de promise is opgelost, waarna de tabel automatisch wordt gerenderd.

### Aangepaste cel‑rendering

Soms heb je iconen, knoppen of geformatteerde datums in cellen nodig. Gebruik de `formatter`‑eigenschap op een kolom:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

De `gridjs.h`‑helper maakt virtuele DOM‑elementen zonder React te importeren.

### Meerdere rasters op één pagina

Herhaal simpelweg stappen 2‑5 met verschillende container‑ID’s:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Elk raster werkt onafhankelijk, zodat je pagineringslimieten, kolomsets en zelfs thema’s kunt mixen.

## Pro‑tips & valkuilen om te vermijden

- **Vergeet de CSS niet** – zonder de stylesheet verschijnt de tabel als een gewone HTML‑tabel, zonder de mooie styling en pagineringsbesturingen.
- **Vermijd dubbele ID’s** – elke **gridjs container** moet een unieke ID hebben; anders overschrijft Gridjs de eerste instantie.
- **Let op de datastructuur** – het aantal kolommen moet overeenkomen met het aantal cellen in elke rij; mismatches veroorzaken stille layout‑glitches.
- **Gebruik `gridjs.h` voor complexe cellen** – het injecteren van ruwe HTML‑strings kan het virtuele DOM‑diff‑algoritme breken.
- **Let op de versie** – de CDN‑link hierboven wijst naar de nieuwste 5.x release (vanaf juni 2026). Als je vastzet op een oudere versie, kunnen sommige opties (zoals `language`) ontbreken.

## Volledig werkend voorbeeld (Kopie‑Plak)

Hieronder vind je het volledige HTML‑bestand dat je kunt opslaan als `gridjs-demo.html` en direct in een browser kunt openen.



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose.Cells for Java: Hoe Excel‑werkboeken efficiënt maken en opmaken](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Hoe Excel exporteren naar HTML met Aspose.Cells Java | Werkboek‑operaties gids](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hoe Excel‑werkboeken maken en samenvoegen met Aspose.Cells for Java | Complete gids](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}