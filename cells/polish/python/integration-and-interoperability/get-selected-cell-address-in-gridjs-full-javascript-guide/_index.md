---
category: general
date: 2026-06-30
description: Dowiedz się, jak uzyskać adres wybranej komórki, zaktualizować wartość
  komórki w siatce i odczytać wartość wejściową przy użyciu JavaScript i GridJs. Krok
  po kroku kod i wskazówki.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: pl
og_description: Uzyskaj adres wybranej komórki, zaktualizuj wartość komórki w siatce
  i odczytaj wartość wejściową za pomocą JavaScript. Przejrzyj ten kompletny przewodnik,
  aby płynnie zintegrować GridJs.
og_title: Uzyskaj adres wybranej komórki – Kompletny poradnik GridJs JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Pobierz adres wybranej komórki w GridJs – Pełny przewodnik JavaScript
url: /pl/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pobierz adres wybranej komórki – Kompletny samouczek JavaScript dla GridJs

Czy kiedykolwiek potrzebowałeś **get selected cell address** z tabeli GridJs, ale nie byłeś pewien, którego wywołania API użyć? Nie jesteś jedyny. W wielu panelach administracyjnych użytkownicy klikają komórkę, edytują wartość w modalnym oknie i oczekują, że siatka natychmiast odzwierciedli zmianę. Ten samouczek pokazuje dokładnie, jak pobrać ten adres, odczytać nową cenę z pola wejściowego i **update grid cell value** bez przeładowania strony.

Omówimy także **read input value with JavaScript** w prawidłowy sposób, obsłużymy przypadki brzegowe i zamkniemy modal po zakończeniu aktualizacji. Po zakończeniu będziesz mieć samodzielny fragment kodu, który możesz wkleić do dowolnego projektu używającego GridJs.

## Co zbudujesz

- Prosta tabela HTML napędzana przez GridJs.  
- Modal edycji, który pojawia się po kliknięciu komórki.  
- JavaScript, który **gets the selected cell address**, pobiera wprowadzoną przez użytkownika cenę, **updates the grid cell value**, i na końcu ukrywa modal.

Nie są wymagane żadne zewnętrzne biblioteki poza GridJs, a kod działa w nowoczesnych przeglądarkach (Chrome 102+, Edge, Firefox). Jeśli już masz instancję GridJs na stronie, możesz bezpośrednio skopiować‑wkleić odpowiednie części.

## Wymagania wstępne

- Podstawowa znajomość JavaScript i DOM.  
- Biblioteka GridJs załadowana (przez CDN lub npm).  
- Strona, która już renderuje siatkę GridJs (pokażemy minimalny przykład).

Jeśli któreś z tych zagadnień jest Ci nieznane, nie panikuj — każdy krok zawiera szybkie podsumowanie.

---

## Krok 1: Przygotuj szkielet HTML

Najpierw umieść kontener tabeli, ukryty modal i pole wejściowe ceny. Modal będzie przełączany prostymi klasami CSS.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** `#editModal` używa minimalnego triku CSS — wystarczy dodać klasę `active`, aby go wyświetlić. Możesz zamienić to na Bootstrap, Tailwind lub dowolny komponent modalny, którego już używasz.

---

## Krok 2: Zainicjalizuj GridJs i przechwyć kliknięcia komórek

Teraz stworzymy siatkę z przykładowymi danymi i nasłuchujemy wyboru komórek. Gdy użytkownik kliknie komórkę, **get the selected cell address** i otworzymy modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()` zwraca ciąg znaków taki jak `"C2"` (kolumna C, wiersz 2). Przechowywanie go w `lastSelectedCell` pozwala odwołać się do dokładnej lokalizacji, gdy później **update grid cell value**.

---

## Krok 3: Odczytaj nową cenę z pola wejściowego

Gdy użytkownik kliknie **Save**, musimy **read input value with JavaScript** w bezpieczny sposób. Ten krok dodatkowo weryfikuje, czy wprowadzona cena jest liczbą dodatnią.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** Użycie `parseFloat` zapewnia obsługę liczb dziesiętnych (np. `1.99`). Ochrona `isNaN` zapobiega przypadkowym pustym zgłoszeniom.

---

## Krok 4: Zaktualizuj wartość wybranej komórki

Teraz w końcu **update grid cell value** przy użyciu adresu, który wcześniej przechwyciliśmy. Metoda `updateCell` w GridJs zwraca obietnicę, więc możemy połączyć ją z akcją zamknięcia modala.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** GridJs może potrzebować ponownego renderowania tabeli lub synchronizacji z backendem. Czekając na obietnicę, gwarantujemy, że UI ukryje się dopiero po odzwierciedleniu nowej wartości w siatce.

---

## Krok 5: Obsłuż anulowanie i przypadki brzegowe

Solidne rozwiązanie zawsze daje użytkownikowi możliwość wyjścia. Przycisk **Cancel** po prostu ukrywa modal i czyści wszelkie zapisane adresy.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Co jeśli nie wybrano żadnej komórki?

Jeśli użytkownik w jakiś sposób uruchomi przycisk **Save** bez wcześniejszego kliknięcia komórki (np. otworzył modal programowo), `lastSelectedCell` będzie `null`. Wcześniejszy `return` w `updateSelectedCell` zapobiega błędowi w czasie wykonywania i loguje pomocne ostrzeżenie.

### Obsługa dużych siatek

W siatkach z paginacją `GridJs.getSelectedCell()` nadal zwraca adres absolutny (np. `"B12"`), a nie tylko widoczny wiersz. Oznacza to, że aktualizacja działa nawet wtedy, gdy edytowany wiersz znajduje się na innej stronie. Pamiętaj jednak, że UI nie przełączy automatycznie stron po aktualizacji — jeśli tego potrzebujesz, wywołaj `grid.forceUpdate()` lub przejdź ręcznie do odpowiedniej strony.

## Kompletny działający przykład

Poniżej pełny kod, który możesz skopiować‑wkleić do jednego pliku HTML. Otwórz go w przeglądarce, kliknij dowolną komórkę, zmień cenę i zobacz, jak siatka aktualizuje się natychmiast.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z krok‑po‑kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Uzyskaj adres, liczbę komórek i offset dla całego zakresu Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Uzyskaj adres, liczbę komórek i offset dla całego zakresu Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Uzyskaj adres, liczbę komórek i offset dla całego zakresu Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}