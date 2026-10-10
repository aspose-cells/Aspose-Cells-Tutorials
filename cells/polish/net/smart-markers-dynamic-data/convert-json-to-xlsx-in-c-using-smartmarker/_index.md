---
category: general
date: 2026-10-10
description: Konwertuj JSON do XLSX w C# przy użyciu SmartMarker – dowiedz się, jak
  zaimportować JSON do Excela i programowo wypełnić skoroszyt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: pl
lastmod: 2026-10-10
og_description: Konwertuj JSON do XLSX w C# za pomocą SmartMarker. Postępuj zgodnie
  z tym przewodnikiem, aby zaimportować JSON do Excela, utworzyć skoroszyt Excel w
  C# i wypełnić go danymi z JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Konwertuj JSON do XLSX w C# – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Konwertuj JSON do XLSX w C# przy użyciu SmartMarker
url: /pl/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie JSON do XLSX w C# przy użyciu SmartMarker

Jeśli potrzebujesz **konwertować JSON do XLSX w C#**, ten przewodnik pokaże Ci, jak **importować JSON do Excela** i **wypełnić Excel danymi z JSON** przy użyciu kilku linii kodu. Zobaczysz, jak **utworzyć skoroszyt Excel w C#**, skonfigurować procesor SmartMarker oraz ostatecznie **importować JSON do komórek arkusza**.

> **Co otrzymasz** – w pełni działający przykład, który odczytuje tablicę JSON, traktuje ją jako pojedynczy rekord i zapisuje dane do pliku `.xlsx` gotowego do dalszego raportowania lub analizy.

## Konwersja JSON do XLSX – przegląd

SmartMarker jest częścią biblioteki Aspose.Cells i umożliwia wiązanie JSON, XML lub dowolnego obiektu .NET bezpośrednio z szablonem Excel. W tym samouczku wykonamy:

1. **Utworzyć skoroszyt Excel** w pamięci.
2. **Załadować dane JSON**, które reprezentują prostą listę osób.
3. **Skonfigurować SmartMarker**, aby traktował tablicę JSON jako pojedynczy rekord (`ArrayAsSingle = true`).
4. **Przetworzyć arkusz**, pozwalając SmartMarker zastąpić znaczniki wartościami z JSON.
5. **Zapisz skoroszyt** jako plik `.xlsx`.

Cały przepływ działa na .NET 6+ i wymaga jedynie pakietu NuGet `Aspose.Cells`.

## Krok 1: Utwórz skoroszyt Excel w C#

Najpierw dodaj pakiet Aspose.Cells do swojego projektu:

```bash
dotnet add package Aspose.Cells
```

Teraz możesz utworzyć nowy obiekt `Workbook`. Skoroszyt zaczyna się pusty, ale możesz dodać arkusz i umieścić znaczniki SmartMarker tam, gdzie mają pojawić się dane JSON.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Dlaczego najpierw tworzymy skoroszyt** – SmartMarker działa na istniejącym obiekcie `Worksheet`; skoroszyt zapewnia kontener dla wszystkich kolejnych operacji.

## Krok 2: Zdefiniuj dane JSON i skonfiguruj SmartMarker

Użyjemy małego ładunku JSON, który zawiera dwie osoby. Opcja `ArrayAsSingle` mówi SmartMarker, aby traktował całą tablicę jako jeden logiczny rekord, co jest idealne, gdy potrzebna jest prosta tabela bez zagnieżdżonych pętli.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

**Wskazówka:** Jeśli pominiesz `ArrayAsSingle`, SmartMarker spróbuje utworzyć osobny rekord dla każdego elementu tablicy, co może prowadzić do duplikatów wierszy lub nieoczekiwanego układu.

## Krok 3: Wstaw znaczniki SmartMarker do arkusza

Znaczniki SmartMarker to zwykłe tekstowe zastępniki otoczone znakiem `&`. Umieść je w komórkach, w których mają pojawić się wartości JSON. W tym przykładzie zapisujemy znaczniki bezpośrednio w kodzie, ale możesz także najpierw zaprojektować szablon w Excelu.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

**Wyjaśnienie:** `&=Name&` instruuje SmartMarker, aby zastąpił komórkę polem `Name` z obiektu JSON, natomiast `&=Age&` robi to samo dla `Age`.

## Krok 4: Przetwórz arkusz – wypełnij Excel danymi z JSON

Teraz pozwól SmartMarker odczytać ciąg JSON i wypełnić zastępniki.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

W tle SmartMarker parsuje `jsonData`, mapuje każdą właściwość obiektu na odpowiedni znacznik i automatycznie rozszerza wiersze, ponieważ `ArrayAsSingle` jest ustawione na `true`. Po przetworzeniu arkusz wygląda następująco:

| Imię | Wiek |
|------|-----|
| John | 30  |
| Anna | 25  |

## Krok 5: Zapisz plik XLSX

Ostatecznie zapisz wypełniony skoroszyt na dysku.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Uruchomienie programu tworzy `SmartMarkerJson.xlsx` na pulpicie. Otwarcie pliku w Excelu pokazuje czystą tabelę z poprawnie zaimportowanymi danymi JSON.

## Typowe pułapki przy importowaniu JSON do arkusza

| Problem | Dlaczego się dzieje | Jak tego uniknąć |
|---------|---------------------|-----------------|
| **Brak znaczników SmartMarker** | SmartMarker zastępuje tylko komórki zawierające `&=...&`. | Sprawdź dokładną pisownię i wielkość liter znacznika. |
| **Nieprawidłowy format JSON** | Pojedyncze cudzysłowy (`'`) nie są prawidłowym JSON dla wbudowanego parsera. | Użyj podwójnych cudzysłowów (`"`) lub pozwól Aspose.Cells obsłużyć luźny format, jak pokazano. |
| **Tablica traktowana jako wiele rekordów** | Domyślne `ArrayAsSingle` jest `false`. | Ustaw `processor.Options.ArrayAsSingle = true`, gdy potrzebna jest płaska tabela. |
| **Zapisywanie do folderu tylko do odczytu** | `workbook.Save` zgłasza wyjątek. | Wybierz katalog z prawami zapisu (np. Pulpit lub folder tymczasowy). |

## Rozszerzanie rozwiązania

- **Wiele arkuszy:** Utwórz dodatkowe arkusze i wywołaj `processor.Process` na każdym z nich, używając różnych źródeł JSON.
- **Stylizacja:** Po przetworzeniu zastosuj style komórek (czcionki, obramowania) tak jak w każdej standardowej operacji Aspose.Cells.
- **Duże zestawy danych:** Przy tysiącach wierszy rozważ strumieniowanie skoroszytu, aby zmniejszyć zużycie pamięci (`WorkbookDesigner` lub `SaveOptions` z `EnableMemoryOptimization`).

## Zakończenie

Teraz wiesz, jak **konwertować JSON do XLSX w C#** przy użyciu Aspose.Cells SmartMarker. Pełny przepływ pracy — **utworzyć skoroszyt Excel w C#**, dodać znaczniki SmartMarker, skonfigurować procesor, **wypełnić Excel danymi z JSON** i zapisać plik — pozwala **importować JSON do komórek arkusza** przy minimalnej ilości kodu.  

Śmiało eksperymentuj z bardziej złożonymi strukturami JSON, dodawaj formuły lub generuj wykresy bezpośrednio z wypełnionych danych. Jeśli podobał Ci się ten przewodnik, wypróbuj kolejny samouczek o **importowaniu JSON do Excela** w celu tworzenia wykresów lub o **tworzeniu skoroszytu Excel w C#** z zaawansowanym formatowaniem.

---

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Konwertowanie JSON do Excela w C# – Przewodnik krok po kroku](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Jak wstawić JSON do szablonu Excel – Krok po kroku](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Utwórz skoroszyt Excel w C# – Wstaw JSON i zapisz jako XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}