---
category: general
date: 2026-11-16
description: Utwórz plik Excel z JSON przy użyciu SmartMarker. Dowiedz się, jak konwertować
  JSON do Excela, osadzać JSON w Excelu i zapisywać skoroszyt xlsx w ciągu kilku minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: pl
lastmod: 2026-11-16
og_description: Szybko twórz pliki Excel z JSON. Ten samouczek pokazuje, jak konwertować
  JSON do Excela, osadzać JSON w Excelu oraz zapisywać skoroszyt xlsx przy użyciu
  Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Utwórz Excel z JSON przy użyciu SmartMarker – przewodnik krok po kroku w
  C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Utwórz Excel z JSON przy użyciu SmartMarker w C#
url: /pl/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie pliku Excel z JSON przy użyciu SmartMarker w C#

Jeśli potrzebujesz **utworzyć Excel z JSON** w projekcie .NET, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Korzystając z procesora Smart Marker firmy Aspose.Cells, możesz **konwertować JSON do Excela**, osadzić ciąg JSON bezpośrednio w komórce i **zapisać skoroszyt xlsx** bez ręcznego pisania kodu parsującego.

Zobaczysz, jak zarejestrować źródło danych JSON, wstawić Smart Marker, który wyświetla całą tablicę jako pojedynczy ciąg JSON, przetworzyć arkusz i ostatecznie zapisać plik na dysku. Po zakończeniu tutorialu będziesz mógł wygenerować plik Excel zawierający oryginalny ładunek JSON w komórce A1, gotowy do dalszego przetwarzania lub raportowania.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także z .NET Framework 4.7+)
- Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`)
- Podstawowa znajomość C# i formatowania JSON
- IDE, takie jak Visual Studio lub VS Code

## Krok 1: Utworzenie projektu i import przestrzeni nazw

Utwórz nową aplikację konsolową i dodaj pakiet Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Następnie dołącz wymagane przestrzenie nazw na początku pliku `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Dlaczego?**  
`Aspose.Cells` zapewnia model skoroszytu, natomiast `Aspose.Cells.SmartMarkers` zawiera klasę `SmartMarkerProcessor`, która interpretuje znaczniki `&=` w arkuszu.

## Krok 2: Zdefiniowanie źródła danych JSON

Umieść ciąg JSON w zmiennej. W tym przykładzie mamy tablicę zamówień:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Dlaczego?**  
Smart Marker działa z dowolnym poprawnym JSON. Przechowywanie JSON w ciągu znaków pozwala zarejestrować go bezpośrednio, bez potrzeby pliku na dysku.

## Krok 3: Rejestracja danych JSON w SmartMarkerProcessor

Utwórz instancję `SmartMarkerProcessor` i powiąż ciąg JSON z nazwą, którą później odwołasz w arkuszu:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Dlaczego?**  
`RegisterJsonDataSource` analizuje JSON i udostępnia jego hierarchię Smart Markerom. Nazwa `"OrdersJson"` staje się obiektem głównym w wyrażeniach znacznika.

## Krok 4: Utworzenie skoroszytu i wstawienie Smart Marker

Zainicjuj nowy skoroszyt, pobierz jego pierwszy arkusz i wpisz Smart Marker do komórki A1, który wyświetli całą tablicę `Orders` jako pojedynczy ciąg JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Dlaczego?**  
Wyrażenie `OrdersJson.Orders.ArrayAsSingle` instruuje Smart Marker, aby wziął tablicę `Orders` i ponownie ją zserializował do JSON, umieszczając wynik w docelowej komórce. To najprostszy sposób na **osadzenie JSON w Excelu**.

## Krok 5: Przetworzenie arkusza

Uruchom procesor, aby zamienił znacznik na rzeczywisty ciąg JSON:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Dlaczego?**  
Przetwarzanie przegląda każdą komórkę pod kątem znaczników `&=`, ocenia je względem zarejestrowanych źródeł danych i zapisuje wyliczoną wartość z powrotem w arkuszu.

## Krok 6: Zapis skoroszytu jako plik .xlsx

Na koniec zapisz skoroszyt na dysku. Dostosuj ścieżkę do folderu, w którym masz prawo zapisu:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Dlaczego?**  
`SaveFormat.Xlsx` zapewnia zapis pliku w nowoczesnym formacie Office Open XML, spełniając wymóg **save workbook xlsx**.

## Pełny kod źródłowy

Łącząc wszystkie elementy, otrzymujemy kompletny, gotowy do uruchomienia program:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Oczekiwany wynik w Excelu

Otwórz plik `JsonArraySingleCell.xlsx`. Komórka A1 będzie zawierać:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

Ciąg JSON jest zwartą reprezentacją pierwotnej tablicy `Orders`, co ułatwia transport lub konsumpcję w dalszych przepływach pracy opartych na Excelu.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Dostosowanie |
|-----------|------------|
| **Wiele obiektów JSON** | Zarejestruj każdy obiekt pod inną nazwą (np. `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) i odwołuj się do nich oddzielnymi znacznikami. |
| **JSON sformatowany ładnie w komórce** | Użyj opcji `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Duże ładunki JSON** | Rozważ zapisanie JSON na ukrytym arkuszu lub konwersję do `DataTable` dla lepszej wydajności. |
| **Osadzanie JSON w wielu komórkach** | Umieść różne znaczniki w innych komórkach, np. `&=OrdersJson.Orders[0].Id`, aby pobrać poszczególne pola. |

**Pro tip:** Przy bardzo dużych JSON zwiększ bufor pamięci skoroszytu (`WorkbookSettings.MemorySetting`), aby uniknąć `OutOfMemoryException`.

## Testowanie rozwiązania

1. Zbuduj i uruchom aplikację konsolową (`dotnet run`).  
2. Zweryfikuj, że konsola wypisuje pełną ścieżkę do wygenerowanego pliku.  
3. Otwórz plik w Excelu lub innym przeglądarce arkuszy.  
4. Potwierdź, że komórka A1 zawiera dokładnie ciąg JSON przedstawiony powyżej.

Jeśli w komórce znajduje się tekst znacznika (`&=OrdersJson...`) zamiast JSON, sprawdź, czy procesor został wywołany **po** umieszczeniu znacznika oraz czy ciąg JSON jest prawidłowy.

## Podsumowanie

Teraz wiesz, jak **utworzyć Excel z JSON** przy użyciu Smart Markerów Aspose.Cells, jak **konwertować JSON do Excela**, osadzić ładunek JSON bezpośrednio w komórce i **zapisać skoroszyt xlsx** jedną linijką kodu. To podejście eliminuje ręczne parsowanie, działa z dowolną strukturą JSON i generuje czysty, zgodny ze standardami plik Excel.

### Kolejne kroki

- Poznaj **pętle Smart Marker** (`&=OrdersJson.Orders`), aby wygenerować wiersz dla każdego zamówienia zamiast jednego ciągu JSON.  
- Połącz tę technikę z **formułami Excel** w celu obliczania sum z osadzonych danych.  
- Zbadaj **odczyt JSON z Excela** przy użyciu `Workbook.Load` i `SmartMarkerProcessor` w odwrotnym kierunku.

Śmiało eksperymentuj z różnymi kształtami JSON, wieloma arkuszami lub eksportem do innych formatów, takich jak CSV czy PDF. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}