---
category: general
date: 2026-06-21
description: Stwórz interaktywną siatkę danych przy użyciu Grid.js i dowiedz się,
  jak wyświetlić tabelę danych JSON z sortowaniem, paginacją i wyszukiwaniem. Idealne
  dla pulpitów webowych.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: pl
og_description: Stwórz interaktywną siatkę danych w kilka minut. Dowiedz się, jak
  używać Grid.js do wyświetlania tabeli danych JSON z paginacją, sortowaniem i wyszukiwaniem.
og_title: Stwórz interaktywną siatkę danych z Grid.js – Kompletny tutorial
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
title: Stwórz interaktywną siatkę danych z Grid.js – pełny przewodnik krok po kroku
url: /pl/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz interaktywną siatkę danych z Grid.js – Pełny przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak **utworzyć interaktywną siatkę danych**, która pozwala użytkownikom sortować, wyszukiwać i przeglądać wiersze bez pisania backendu? Nie jesteś sam. W wielu pulpitach nawigacyjnych największym problemem jest przekształcenie statycznego zrzutu JSON w elegancką, przeszukiwalną tabelę — coś, co działa tak płynnie jak arkusz kalkulacyjny, ale działa całkowicie w przeglądarce.

W tym samouczku przejdziemy przez **how to use Grid.js**, aby **display JSON data table** na zwykłej stronie HTML. Po zakończeniu będziesz mieć działający przykład, który możesz wstawić do dowolnego projektu, a także wskazówki dotyczące dostosowywania paska narzędzi, obsługi dużych zestawów danych i unikania typowych pułapek.

## Czego się nauczysz

- Jak pobrać plik JSON definiujący kolumny i wiersze.  
- Jak zainicjalizować **Grid.js** z paginacją, sortowaniem, wyszukiwaniem i niestandardowym paskiem narzędzi.  
- Jak wyrenderować siatkę w docelowym kontenerze.  
- Opcjonalne poprawki: niestandardowe formatowanie komórek, zmiana motywu i obsługa błędów.  
- Pełny, gotowy do skopiowania kod.

### Wymagania wstępne

1. Nowoczesna przeglądarka (Chrome, Edge lub Firefox) – Grid.js opiera się na funkcjach ES6.  
2. Lokalny lub zdalny folder zawierający plik `grid_data.json` (pokażemy format).  
3. Podstawowa znajomość HTML i JavaScript – nic skomplikowanego, po prostu umiejętność otwarcia pliku `.html` w przeglądarce.  

Bez narzędzi budujących, bez instalacji npm, bez kodu po stronie serwera. To właśnie piękno **create interactive data grid** z Grid.js: działa prosto z CDN.

---

## Krok 1: Przygotuj JSON definiujący Twoją tabelę

Pierwszą rzeczą, której potrzebujesz, jest ładunek JSON, który mówi Grid.js, jakie kolumny istnieją i jakie wiersze wyświetlić. Pomyśl o tym jako o planie dla twojego **display JSON data table**. Oto minimalny przykład, który możesz zapisać jako `grid_data.json` w tym samym katalogu co plik HTML:

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

*Dlaczego taki format?* Grid.js oczekuje, że `columns` będzie tablicą ciągów znaków (lub obiektów dla zaawansowanej konfiguracji), a `rows` będzie tablicą tablic, gdzie każda wewnętrzna tablica odpowiada kolejności kolumn. Oczywiście możesz dodać więcej kolumn lub zagnieżdżone obiekty – Grid.js wyrenderuje je, o ile kształty się zgadzają.

> **Pro tip:** Jeśli pobierasz dane z API, po prostu zamień statyczny `fetch('grid_data.json')` na adres URL swojego endpointu. Reszta kodu pozostaje bez zmian.

---

## Krok 2: Zainicjalizuj Grid.js – Serce **how to use gridjs**

Teraz, gdy źródło danych jest gotowe, musimy wprowadzić Grid.js na stronę i powiedzieć mu, jak ma się zachowywać. To właśnie tutaj faktycznie **create interactive data grid** funkcjonalność, taka jak paginacja, sortowanie i przydatny przycisk w pasku narzędzi.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN dostarcza najnowszą stabilną wersję, a motyw Meri­maid dodaje czysty, nowoczesny wygląd od razu po załadowaniu. Możesz go zamienić na `gridjs.min.css`, jeśli wolisz domyślne stylowanie.

Następnie, wewnątrz tagu `<script>`, pobierz JSON i zainicjalizuj siatkę:

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

### Rozbiór opcji

| Opcja | Co robi | Dlaczego to ważne |
|-------|---------|-------------------|
| `pagination` | Dzieli wiersze na strony (domyślnie 10 na stronę) | Utrzymuje duże tabele użyteczne bez przytłaczania interfejsu. |
| `sort` | Klikalne nagłówki kolumn przełączają kolejność rosnącą/malejącą | Użytkownicy mogą szybko znaleźć wiersze o najwyższych wartościach. |
| `search` | Dodaje pole tekstowe, które na bieżąco filtruje wiersze | Świetne do ad‑hoc wyszukiwań bez ponownego ładowania danych. |
| `toolbar` | Dodaje własne przyciski lub listy rozwijane nad siatką | Idealne dla akcji „Help”, „Export” lub „Refresh”. |
| `formatter` | Pozwala zwrócić surowy HTML dla komórki | Tutaj zamieniamy ciągi e‑mail na klikalne linki mailto. |

> **Dlaczego takie podejście?** Trzymając konfigurację siatki w formie deklaratywnej, możesz łatwo dostosować zachowanie bez modyfikowania logiki renderowania. To zalecany sposób **how to use Grid.js** dla większości projektów.

---

## Krok 3: Renderuj siatkę na swojej stronie

Ostatnia linia skryptu — `grid.render(document.getElementById('grid-container'))` — wstrzykuje w pełni funkcjonalną tabelę do `<div>`, który umieściłeś gdzieś w ciele HTML:

```html
<div id="grid-container"></div>
```

I to wszystko. Gdy strona się załaduje, przeglądarka pobiera JSON, buduje instancję Grid.js i rysuje interaktywną tabelę na ekranie. Bez odświeżeń, bez wywołań serwera po początkowym załadowaniu.

---

## Opcjonalnie: Dostosowanie stylów i motywów

Jeśli domyślny motyw Meri­maid nie jest dla Ciebie, możesz go zamienić na dowolny z wbudowanych motywów (`gridjs.min.css`) lub napisać własny CSS. Na przykład, aby zmienić tło nagłówka na delikatny szary:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Dodaj fragment wewnątrz tagu `<style>` lub w zewnętrznym arkuszu stylów. Grid.js respektuje standardowe selektory CSS, więc masz pełną kontrolę nad czcionkami, kolorami i odstępami.

---

## Częste pułapki i jak ich uniknąć

| Pułapka | Objaw | Rozwiązanie |
|---------|-------|-------------|
| **Błędy CORS** przy pobieraniu JSON z innej domeny | Konsola przeglądarki wyświetla „Blocked by CORS policy” | Hostuj JSON na tej samej domenie lub włącz CORS na serwerze. |
| **Duże zestawy danych powodują opóźnienia** | Przewijanie staje się szarpane, paginacja wolna | Użyj paginacji po stronie serwera (`pagination: { server: { url: (prev, page, limit) => … } }`) lub ładowania leniwego. |
| **Przycisk paska narzędzi nie pojawia się** | Brak przycisku mimo `toolbar.enabled: true` | Upewnij się, że używasz Grid.js w wersji 2.0+; starsze wersje miały inną API paska narzędzi. |
| **Linki e‑mail nie są klikalne** | Formatter zwraca zwykły tekst | Zwróć `gridjs.html(...)` zamiast zwykłego ciągu, jak pokazano w przykładzie. |

Rozwiązywanie tych problemów na wczesnym etapie oszczędza godziny debugowania później.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się kompletny plik HTML, który możesz zapisać jako `index.html`. Otwórz go w przeglądarce, a zobaczysz w pełni funkcjonalny **create interactive data grid** demo, który **display JSON data table** z sortowaniem, wyszukiwaniem i przyciskiem pomocy.

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


## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}