---
category: general
date: 2026-06-30
description: Hur man enkelt skapar gridjs med ett komplett JavaScript‑exempel, som
  täcker gridjs‑konfiguration, container‑inställning och renderingsprocess.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: sv
og_description: Hur man enkelt skapar gridjs med ett komplett JavaScript‑exempel,
  som täcker gridjs‑konfiguration, containerinställning och renderingsprocess.
og_title: Hur man skapar Gridjs – Komplett JavaScript‑rutnätsguide
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
title: Hur man skapar Gridjs – Komplett JavaScript‑gridguide
url: /sv/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar Gridjs – Komplett JavaScript Grid‑guide

Har du någonsin undrat **how to create gridjs** och direkt se en snygg datatabell på din sida? Du är inte ensam. Många utvecklare stöter på problem när de första gången försöker sätta upp Gridjs, särskilt kring konfigurationsobjektet och render‑anropet. Den goda nyheten? Det är faktiskt en barnlek när du känner till rätt steg.

I den här handledningen går vi igenom ett verkligt exempel som visar **how to create gridjs** från grunden, hur man skapar en korrekt **gridjs configuration**, hur man binder grid‑en till en **gridjs container**, och slutligen hur man triggar **gridjs render**. När du är klar har du ett fullt fungerande grid som du kan släppa in i vilket projekt som helst – ingen mystik, bara tydlig kod.

## Vad du kommer att lära dig

- Ställ in en minimal HTML‑sida redo för Gridjs.  
- Skriv ett **gridjs configuration**‑objekt som definierar kolumner, data och alternativ.  
- Fäst Gridjs‑instansen på ett **gridjs container**‑element.  
- Anropa **gridjs render** för att visa tabellen.  
- Justera vanliga inställningar (paginering, sortering, styling) och undvik typiska fallgropar.

Inga externa byggverktyg krävs; allt körs i webbläsaren med ett enda script‑tag. Låt oss komma igång.

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. En modern webbläsare (Chrome, Edge, Firefox, Safari) – något som stödjer ES6.  
2. Grundläggande kunskaper i HTML och JavaScript – du behöver inget ramverk.  
3. Tillgång till Gridjs‑biblioteket – vi hämtar det från en CDN, så ingen npm‑install behövs.

Det är allt. Om du redan har en sida du vill förbättra kan du klistra in kodsnuttarna direkt.

## Steg 1: Lägg till Gridjs‑tillgångar på din sida

Först måste vi ladda Gridjs‑s CSS‑ och JavaScript‑filer. CDN‑versionen är lättviktig och perfekt för snabba demo‑exempel.

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

> **Pro tip:** Mermaid‑temat ger tabellen ett rent, modernt utseende utan extra CSS. Byt gärna ut det mot `classic.min.css` om du föredrar en annan stil.

## Steg 2: Definiera **gridjs container**

**gridjs container** är bara en vanlig `<div>` som kommer att hysa den renderade tabellen. I markup‑en ovan har vi redan skapat `<div id="grid"></div>`. `id`‑attributet är avgörande eftersom vi senare använder det för att binda Gridjs‑instansen.

Om du behöver flera grids på samma sida, ge varje container ett unikt ID (`grid1`, `grid2`, …) och upprepa bindningslogiken för varje.

## Steg 3: Skapa ett **gridjs configuration**‑objekt

Nu kommer hjärtat i **how to create gridjs** – konfigurationen. Detta enkla JavaScript‑objekt talar om för Gridjs vilka kolumner som ska visas, vilken data som ska fyllas i och vilka funktioner som ska aktiveras.

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

### Varför denna konfiguration är viktig

- **Columns** – definierar rubriktexten och valfri bredd. Utan detta skulle Gridjs härleda kolumnnamn från den första dataraden, vilket ofta blir mindre läsbart.  
- **Data** – en array av rader, där varje rad är en array av cellvärden. Du kan också leverera en async‑funktion som hämtar data från ett API; biblioteket hanterar automatiskt promises.  
- **Pagination** – begränsar antalet rader per sida och förhindrar att enorma tabeller överväldigar UI‑t.  
- **Search & Sort** – slå på interaktiva funktioner med ett enkelt boolean‑värde, så slipper du skriva egna hanterare.  
- **Language** – anpassa UI‑strängar, perfekt för lokalisering eller varumärkesprofilering.

Känn dig fri att byta ut den statiska data‑arrayen mot ett fetch‑anrop senare; resten av stegen förblir exakt desamma.

## Steg 4: Instansiera Gridjs och bind till **gridjs container**

Med konfigurationen klar skapar vi en ny `GridJs.Grid` (klassnamnet är `gridjs.Grid` i UMD‑bygget) och pekar den på vårt container‑element.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Observera att vi använde `document.getElementById('grid')` – det är **gridjs container** som vi definierade tidigare. Om du har flera containers, upprepa bara den här raden med rätt ID.

## Steg 5: Aktivera **gridjs render**‑anropet

Den sista pusselbiten är **gridjs render**‑metoden. Den tar konfigurationen vi skickade tidigare och injicerar en fullt stylad `<table>` i containern.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Det är allt! När du öppnar sidan i en webbläsare ser du en sökbar, paginerad tabell med de fyra rader vi definierade. Sökfältet visas automatiskt högst upp och pagineringskontrollerna sitter längst ner.

### Förväntat resultat

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

UI‑t anpassar sig när du skriver i sökfältet eller klickar på kolumnrubriker för att sortera.

## Vanliga variationer & kantfall

### Ladda data asynkront

Om din data finns på en server, ersätt den statiska `data`‑arrayen med en funktion som returnerar en Promise:

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

Gridjs visar en laddningsspinner tills promisen löser sig, och renderar sedan tabellen automatiskt.

### Anpassad cellrendering

Ibland behöver du ikoner, knappar eller formaterade datum i celler. Använd `formatter`‑egenskapen på en kolumn:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

`gridjs.h`‑hjälpen skapar virtuella DOM‑element utan att behöva dra in React.

### Flera gridjs på en sida

Upprepa bara steg 2‑5 med olika container‑ID:n:

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

Varje grid fungerar oberoende, så du kan blanda pagineringsgränser, kolumnuppsättningar och till och med teman.

## Pro‑tips & fallgropar att undvika

- **Don’t forget the CSS** – utan stylesheet visas tabellen som en enkel HTML‑tabell och förlorar all fin styling och pagineringskontroller.  
- **Avoid duplicate IDs** – varje **gridjs container** måste ha ett unikt ID; annars skriver Gridjs över den första instansen.  
- **Watch the data shape** – antalet kolumner måste matcha antalet celler i varje rad; felaktiga arrayer ger tysta layout‑buggar.  
- **Use `gridjs.h` for complex cells** – att injicera rå HTML‑strängar kan bryta den virtuella DOM‑diff‑algoritmen.  
- **Mind the version** – CDN‑länken ovan pekar på den senaste 5.x‑releasen (från juni 2026). Om du låser dig till en äldre version kan vissa alternativ (som `language`) saknas.

## Fullt fungerande exempel (kopiera‑klistra in)

Nedan är den kompletta HTML‑filen som du kan spara som `gridjs-demo.html` och öppna direkt i en webbläsare.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Aspose.Cells för Java: Hur man skapar och formaterar Excel‑arbetsböcker effektivt](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Hur man skapar och exporterar Excel till HTML med Aspose.Cells Java \| Arbetsbok Operationsguide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hur man skapar och slår ihop Excel‑arbetsböcker med Aspose.Cells för Java \| Komplett guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}