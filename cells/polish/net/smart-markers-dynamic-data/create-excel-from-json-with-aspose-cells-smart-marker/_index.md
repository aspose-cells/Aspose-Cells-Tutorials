---
category: general
date: 2026-08-07
description: Utwórz plik Excel z JSON przy użyciu Aspose.Cells Smart Marker – dowiedz
  się, jak wypełnić szablon Excela, zastosować dynamiczne nazewnictwo arkuszy i wygenerować
  wiele arkuszy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: pl
lastmod: 2026-08-07
og_description: Utwórz plik Excel z JSON przy użyciu Aspose.Cells Smart Marker, aby
  szybko wypełniać szablony, stosować dynamiczne nazwy arkuszy i generować wiele arkuszy.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Utwórz Excel z JSON – przewodnik po Aspose.Cells Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz Excel z JSON przy użyciu Aspose.Cells Smart Marker
url: /pl/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz Excel z JSON przy użyciu Aspose.Cells Smart Marker

Jeśli potrzebujesz **utworzyć Excel z JSON**, ten tutorial pokazuje kompletną, gotową do produkcji rozwiązanie. Zobaczysz, jak **wypełnić szablon Excela**, skonfigurować **dynamiczne nazewnictwo arkuszy** oraz **automatycznie generować wiele arkuszy** przy użyciu silnika **Aspose.Cells Smart Marker**.

Przewodnik przeprowadzi Cię przez każdy wymagany krok, od zdefiniowania źródłowego obiektu w stylu JSON po zapisanie finalnego skoroszytu. Nie są potrzebne żadne zewnętrzne skrypty, a kod działa na .NET 6 lub nowszym.

## Co osiągniesz

* Wczytaj obiekt danych w stylu JSON do pamięci.  
* Wstaw placeholder Smart Marker do szablonu skoroszytu.  
* Zastosuj wzorzec nazewnictwa, aby każdy zduplikowany arkusz szczegółowy otrzymał unikalną nazwę.  
* Przetwórz szablon, aby utworzyć osobny arkusz dla każdego zamówienia w kolekcji.  
* Zapisz wynik jako plik `.xlsx` gotowy do dalszego wykorzystania.

Wymagania wstępne: Visual Studio 2022 (lub dowolne IDE C#), .NET 6+ oraz pakiet NuGet **Aspose.Cells**. Przykład używa C#; te same koncepcje mają zastosowanie w VB.NET lub innych językach .NET.

## Tworzenie Excela z JSON – ogólny przepływ pracy

Poniższe sekcje dzielą przepływ pracy na pięć logicznych kroków. Każdy krok zawiera dokładny kod, wyjaśnienie, dlaczego jest ważny, oraz wskazówki dotyczące skalowania rozwiązania.

### Krok 1: Zdefiniuj źródłowe dane kompatybilne z JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Dlaczego to jest ważne** – Obiekt `ordersData` odzwierciedla strukturę, którą otrzymałbyś z prawdziwego API JSON. Aspose.Cells Smart Marker odczytuje publiczne właściwości, więc typ anonimowy działa, pod warunkiem że nazwy właściwości pasują do tagów markerów (`{{Orders}}`). Gdy później zamienisz typ anonimowy na zdeserializowany obiekt JSON, nie będą potrzebne żadne zmiany w kodzie.

### Krok 2: Przygotuj szablon skoroszytu i wstaw Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Dlaczego to jest ważne** – Marker `{{Orders}}` informuje procesor, aby iterował po kolekcji `Orders`. Umieszczenie markera w komórce `A1` pierwszego arkusza sprawia, że ten arkusz staje się arkuszem *głównym*. Procesor sklonuje ten arkusz dla każdego zamówienia, zachowując wszelkie formatowanie, które dodasz później.

> **Wskazówka:** Jeśli masz wstępnie zaprojektowany szablon (np. z nagłówkami, formułami lub stylami), załaduj go przy użyciu `new Workbook("Template.xlsx")` zamiast tworzyć pusty skoroszyt.

### Krok 3: Skonfiguruj dynamiczne nazewnictwo arkuszy

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Dlaczego to jest ważne** – Domyślnie Aspose.Cells nazywa zduplikowane arkusze `Sheet1`, `Sheet2` itd. Wzorzec `DetailSheetNewName` wstawia indeks inkrementalny (`{0}`), dzięki czemu każdy arkusz otrzymuje znaczącą nazwę. Możesz osadzić dodatkowe placeholdery (np. `{Id}`), aby uwzględnić dane z bieżącego rekordu.

> **Pro tip:** Użyj `DetailSheetNewName = "Order_{Id}"`, aby nazwać arkusze po identyfikatorze zamówienia, co ułatwia nawigację w dużych skoroszytach.

### Krok 4: Przetwórz szablon z danymi i opcjami nazewnictwa

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Dlaczego to jest ważne** – `SmartMarkerProcessor` łączy `ordersData` ze skoroszytem, tworzy nowy arkusz dla każdego elementu w `Orders` i stosuje wcześniej zdefiniowany wzorzec nazewnictwa. Procesor także rozwija wszelkie zagnieżdżone kolekcje (np. `Items`), jeśli dodasz dodatkowe markery wewnątrz arkusza szczegółowego.

### Krok 5: Zapisz wynikowy skoroszyt

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Dlaczego to jest ważne** – Metoda `Save` zapisuje w pełni wypełniony skoroszyt na dysk. Plik zawiera teraz arkusz główny (który może być ukryty lub usunięty) oraz serię arkuszy szczegółowych nazwanych `DetailSheet_1`, `DetailSheet_2`, …, z których każdy przechowuje dane jednego zamówienia.

#### Oczekiwany wynik

| Nazwa arkusza | Zawartość (uproszczona)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Wszystkie arkusze zachowują wszelkie formatowanie, które zastosowałeś w arkuszu głównym przed przetworzeniem.

## Zaawansowane warianty

### Wypełnij szablon Excela dodatkowymi polami

Jeśli Twój JSON zawiera więcej właściwości (np. `CustomerName`, `TotalAmount`), dodaj odpowiadające markery do szablonu:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Procesor zastąpi każdy marker odpowiednią wartością właściwości.

### Generuj wiele arkuszy z zagnieżdżonych kolekcji

Możesz utworzyć drugi poziom duplikacji, umieszczając marker wewnątrz arkusza szczegółowego, który odwołuje się do zagnieżdżonej kolekcji, takiej jak `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Podczas przetwarzania Aspose.Cells tworzy wiersz dla każdego elementu w tablicy `Items`, umożliwiając generowanie listy pozycji dla każdego zamówienia.

### Niestandardowe nazewnictwo z danymi z rekordu

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Teraz arkusze są nazwane `Order_1`, `Order_2`, co dopasowuje nazwę arkusza do identyfikatora biznesowego.

## Częste pułapki i jak ich unikać

| Pułapka                              | Rozwiązanie |
|--------------------------------------|----------|
| Tekst markera nie pasuje do nazwy właściwości (uwzględniając wielkość liter) | Upewnij się, że marker (`{{Orders}}`) dokładnie odpowiada nazwie właściwości, łącznie z wielkością liter. |
| Szablon zawiera scalone komórki obejmujące obszar markera | Rozscal komórki lub umieść marker w jednej, nie scalonej komórce, aby zapobiec nieoczekiwanym zmianom układu. |
| Duże kolekcje JSON powodują obciążenie pamięci | Przetwarzaj dane w partiach lub strumieniuj JSON do `DataTable` i użyj `SmartMarkerProcessor` z `DataSource`. |
| Ścieżka zapisanego pliku jest nieprawidłowa | Użyj `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` lub sprawdź uprawnienia do zapisu. |

## Pełny działający przykład

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Uruchomienie programu generuje plik Excel na pulpicie zawierający dwa arkusze szczegółowe (`DetailSheet_1` i `DetailSheet_2`). Każdy arkusz odzwierciedla odpowiadający rekord zamówienia.

## Podsumowanie

Teraz wiesz, jak **utworzyć Excel z JSON** przy użyciu **Aspose.Cells Smart Marker**, jak **wypełnić szablon Excela**, zastosować **dynamiczne nazewnictwo arkuszy** oraz **automatycznie generować wiele arkuszy**. Ten sam wzorzec skaluje się do dziesiątek lub tysięcy rekordów, obsługuje zagnieżdżone kolekcje i integruje się bezproblemowo z dowolną biblioteką deserializacji JSON w .NET.

### Kolejne kroki

* Zbadaj **formatowanie warunkowe** w arkuszu szczegółowym, aby podświetlić zamówienia o wysokiej wartości.  
* Zastąp obiekt anonimowy modelem silnie typowanym deserializowanym przy użyciu `System.Text.Json`.  
* Połącz Smart Markery z generowaniem **PivotTable** w celu zaawansowanego raportowania.  

Eksperymentuj ze wzorcem nazewnictwa, dodawaj więcej markerów i integruj ten przepływ pracy z istniejącymi pipeline'ami eksportu danych. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Generuj dynamiczne raporty Excel przy użyciu Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Wypełnij Excel danymi przy użyciu Aspose.Cells i Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Jak tworzyć i scalać skoroszyty Excel przy użyciu Aspose.Cells dla Java | Kompletny przewodnik](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}