---
category: general
date: 2026-03-25
description: Utwórz skoroszyt Excel z JSON i zapisz go jako xlsx. Dowiedz się, jak
  wyeksportować JSON do xlsx, wygenerować Excel z JSON oraz wypełnić Excel danymi
  z JSON w kilka minut.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: pl
og_description: Twórz skoroszyt Excel z JSON natychmiast. Ten przewodnik pokazuje,
  jak wyeksportować JSON do XLSX, wygenerować Excel z JSON oraz wypełnić Excel danymi
  z JSON przy użyciu Aspose.Cells.
og_title: Utwórz skoroszyt Excel z JSON – Kompletny samouczek C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Utwórz skoroszyt Excel z JSON – przewodnik krok po kroku
url: /pl/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel z JSON – Kompletny samouczek C#

Czy kiedykolwiek potrzebowałeś **create excel workbook** z ładunku JSON, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam; wielu programistów napotyka tę przeszkodę, gdy próbują przekształcić dane API w schludny arkusz kalkulacyjny. Dobra wiadomość? Kilkoma liniami C# i Aspose.Cells możesz **export json to xlsx**, **generate excel from json** i **populate excel from json** bez używania konwerterów zewnętrznych.

W tym przewodniku przeprowadzimy Cię przez cały proces — od surowego łańcucha JSON, przez wstawienie go do SmartMarker, aż po **save workbook as xlsx** na dysku. Po zakończeniu będziesz mieć gotowy do użycia plik Excel, który wygląda tak:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Jeśli już używasz Aspose.Cells w innym miejscu swojego projektu, możesz ponownie wykorzystać tę samą instancję `Workbook` do wielu importów JSON — świetne rozwiązanie do przetwarzania wsadowego.

## Czego będziesz potrzebować

- **.NET 6+** (lub dowolny nowszy .NET Framework obsługujący C# 10)
- **Aspose.Cells for .NET** – zainstaluj przez NuGet: `dotnet add package Aspose.Cells`
- Podstawowa znajomość składni C# (bez głębokiej wiedzy o Excelu)

To wszystko. Bez zewnętrznych usług, bez interfejsu COM, tylko czysty kod zarządzany.

## Krok 1: Zainicjuj nowy skoroszyt Excel

Pierwszą rzeczą, którą robimy, jest stworzenie nowego obiektu workbook. Traktuj to jak otwarcie pustego pliku Excel, do którego później wstawimy nasze dane.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Dlaczego zaczynać od nowego skoroszytu? Gwarantuje czystą kartę, zapobiega pozostawionym stylom z poprzednich uruchomień i utrzymuje minimalny rozmiar pliku — idealne dla zautomatyzowanych potoków.

## Krok 2: Przygotuj dane JSON, które chcesz zaimportować

Do demonstracji użyjemy małej tablicy JSON, ale możesz zamienić ją na dowolny prawidłowy JSON otrzymany z usługi webowej, pliku lub zapytania do bazy danych.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Zauważ podwójnie escapowane cudzysłowy (`\"`) — to tylko składnia literału łańcucha w C#. W rzeczywistym scenariuszu prawdopodobnie odczytasz to z pliku:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Krok 3: Powiedz SmartMarker, aby traktował całą tablicę jako jeden rekord

Silnik SmartMarker w Aspose.Cells może automatycznie iterować po kolekcjach. Włączając **ArrayAsSingle**, traktujemy całą tablicę JSON jako pojedynczy rekord, co jest dokładnie tym, czego potrzebujemy dla płaskiej tabeli.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Jeśli zapomnisz tego flagi, SmartMarker spróbuje utworzyć osobny arkusz dla każdego elementu — zdecydowanie nie to, czego chcesz przy generowaniu prostej tabeli.

## Krok 4: Umieść token SmartMarker w arkuszu

Tokeny SmartMarker wyglądają tak: `${jsonArray}`. Gdy procesor zostanie uruchomiony, zastępuje token danymi ze źródła JSON. Umieścimy token w komórce **A1**, aby wynik zaczynał się w lewym górnym rogu.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Możesz także wstępnie sformatować wiersz nagłówka przed przetwarzaniem. Na przykład, ustaw pogrubioną czcionkę w pierwszym wierszu:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Krok 5: Uruchom procesor SmartMarker

Teraz dzieje się magia. Procesor odczytuje JSON, mapuje każdą właściwość na kolumnę i zapisuje wiersze pod tokenem.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Za kulisami, Aspose.Cells:

1. Parsuje JSON do obiektu .NET.
2. Dopasowuje nazwy właściwości (`Name`, `Score`) do nagłówków kolumn.
3. Zapisuje każdy element tablicy jako nowy wiersz.

Jeśli Twój JSON zawiera zagnieżdżone obiekty, możesz odwoływać się do nich za pomocą notacji kropkowej (`${parent.child}`) — przydatna funkcja przy bardziej złożonych raportach.

## Krok 6: Zapisz skoroszyt jako plik XLSX

Na koniec zapisz skoroszyt na dysku. Rozszerzenie pliku `.xlsx` informuje Excel (i większość innych aplikacji arkuszy) że jest to skoroszyt OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Oczywiście możesz przesłać skoroszyt bezpośrednio w odpowiedzi HTTP, jeśli tworzysz web API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który zawiera wszystkie powyższe kroki. Skopiuj i wklej go do nowego projektu konsolowego i naciśnij **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Oczekiwany wynik:** Otwierając `json-single.xlsx` zobaczysz dwa wiersze pod pogrubionym nagłówkiem — `John` z wynikiem `90` i `Anna` z `85`. Nazwy kolumn są automatycznie wywnioskowane z nazw właściwości JSON.

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli klucze JSON zawierają spacje lub znaki specjalne?

SmartMarker oczekuje prawidłowych nazw identyfikatorów. Zastąp spacje podkreśleniami lub użyj własnego mapowania:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Jak wyeksportować dużą tablicę JSON (tysiące wierszy)?

Procesor strumieniuje dane wewnętrznie, więc zużycie pamięci pozostaje umiarkowane. Jednak możesz chcieć:

- Zwiększyć limit `MaxRows` arkusza (`worksheet.Cells.MaxRow = 1_048_576;` — maksymalny w Excelu).
- Wyłączyć linie siatki dla wydajności (`worksheet.IsGridlinesVisible = false;`).

### Czy mogę dodać wiele tabel JSON do tego samego skoroszytu?

Oczywiście. Po prostu umieść różne tokeny SmartMarker w oddzielnych zakresach (np. `${orders}` w `A10`, `${customers}` w `D1`) i wywołaj `Process` raz dla każdego tokenu lub raz z złożonym obiektem JSON zawierającym obie tablice.

## Bonus: Dodanie prostego wykresu (Opcjonalnie)

Jeśli chcesz zwizualizować wyniki, dodaj szybki wykres kolumnowy po wypełnieniu danych:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## Zakończenie

Teraz wiesz **how to create excel workbook** z łańcucha JSON, **export json to xlsx**, **generate excel from json** i **populate excel from json** przy użyciu funkcji SmartMarker w Aspose.Cells. Kompletny rozwiązanie — inicjalizacja skoroszytu, konfiguracja SmartMarker, przetwarzanie JSON i zapisywanie pliku — mieści się w kilku linijkach, a jednocześnie skaluje się do ogromnych zestawów danych.

Co dalej? Spróbuj zamienić statyczny JSON na wywołanie API, dodaj formatowanie warunkowe w zależności od wyników lub wygeneruj wiele arkuszy dla różnych domen danych. Ten sam wzorzec działa dla CSV, XML czy nawet zestawów wyników z bazy danych — wystarczy zmienić łańcuch źródłowy i dostosować token SmartMarker.

Miłego kodowania i niech Twoje arkusze zawsze będą uporządkowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}