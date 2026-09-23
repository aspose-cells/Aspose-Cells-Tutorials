---
category: general
date: 2026-03-22
description: Dowiedz się, jak sformatować datę i godzinę do formatu ISO podczas wyodrębniania
  daty z Excela i wyświetlić datę w formacie ISO przy użyciu Aspose.Cells w C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: pl
og_description: Formatowanie daty i czasu do ISO stało się proste. Ten przewodnik
  pokazuje, jak wyodrębnić datę z Excela i wyświetlić datę w formacie ISO przy użyciu
  Aspose.Cells.
og_title: formatowanie daty i czasu do ISO w C# – Samouczek krok po kroku
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formatowanie daty i czasu do ISO w C# – Kompletny przewodnik
url: /pl/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# format datetime to iso w C# – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **format datetime to iso**, ale źródło znajduje się w skoroszycie Excel? Może komórka zawiera japoński era, taki jak “令和3年5月1日” i drapiesz się po głowie, zastanawiając się, jak przekształcić to w czysty ciąg `2021‑05‑01`. Nie jesteś sam. W tym samouczku **extract date from excel**, przetworzymy japoński era, a następnie **display iso date** w konsoli — wszystko w kilku linijkach C# i Aspose.Cells.

Przejdziemy przez wszystko, czego potrzebujesz: wymagany pakiet NuGet, dokładny kod, który możesz skopiować‑wkleić, dlaczego każda linia ma znaczenie oraz kilka wskazówek dotyczących przypadków brzegowych. Po zakończeniu będziesz mieć wielokrotnego użytku fragment, który **format datetime to iso** niezależnie od tego, jak dziwnie wygląda oryginalna wartość w Excelu.

## Co będziesz potrzebował

- .NET 6.0 lub nowszy (kod kompiluje się również na .NET Framework 4.6+)
- Visual Studio 2022 (lub dowolny edytor, którego preferujesz)
- **Aspose.Cells for .NET** pakiet NuGet – `Install-Package Aspose.Cells`
- Plik Excel (lub nowy skoroszyt), który zawiera datę w formacie japońskiego era

To wszystko. Żadnych dodatkowych bibliotek, żadnego COM interopu, tylko jedna, dobrze udokumentowana metoda.

## Krok 1: Utwórz skoroszyt i wpisz datę w japońskim erze  

Najpierw potrzebujemy skoroszytu, na którym będziemy pracować. Jeśli już masz plik Excel, możesz go załadować przy pomocy `new Workbook("path")`. W tym przykładzie stworzymy nowy skoroszyt w pamięci i wstawimy ciąg japońskiego era do komórki **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Why we do this:** Aspose.Cells treats cell values as strings by default. By inserting the raw era text we simulate a real‑world scenario where a Japanese client has entered dates in their native calendar.

## Krok 2: Włącz parsowanie japońskiego era i wyodrębnij datę  

Aspose.Cells może automatycznie przetłumaczyć ciągi japońskiego era na obiekty .NET `DateTime` — pod warunkiem, że mu to wskażesz. Flaga `DateTimeParseOptions.EnableJapaneseEra` wykonuje ciężką pracę.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** If you forget the `EnableJapaneseEra` option, the library will return the original string, and your subsequent conversion will fail. Always verify `parsed.Type` if you’re handling mixed content.

## Krok 3: Konwertuj sparsowanego DateTime na ISO 8601  

Teraz, gdy mamy prawidłowy `DateTime`, przekształcenie go w ciąg w formacie ISO jest dziecinnie proste. Wzorzec `"yyyy-MM-dd"` spełnia wymóg części datowej ISO 8601, której oczekuje większość API.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Uruchomienie programu wypisuje:

```
ISO date: 2021-05-01
```

To jest **display iso date**, którego szukałeś.

## Pełny, gotowy do uruchomienia przykład  

Poniżej znajduje się kompletny blok kodu, który możesz skopiować bezpośrednio do projektu konsolowego. Bez ukrytych zależności, bez dodatkowej konfiguracji.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Expected output:** `ISO date: 2021-05-01`

## Szczegółowy podział krok po kroku (Dlaczego każdy element ma znaczenie)

| Krok | Co się dzieje | Dlaczego jest ważne |
|------|---------------|---------------------|
| **Create workbook** | Initializes an in‑memory Excel container. | Gives you a sandbox to test without touching the file system. |
| **PutValue** | Stores the raw Japanese era string in **A1**. | Mimics real data entry; ensures the parser sees the exact text. |
| **GetValue with `EnableJapaneseEra`** | Converts the era string into a .NET `DateTime`. | Handles the calendar conversion automatically—no manual lookup tables needed. |
| **`ToString("yyyy-MM-dd")`** | Formats the `DateTime` to ISO 8601. | Guarantees a culture‑invariant, sortable date string accepted by REST APIs, databases, etc. |
| **Console.WriteLine** | Shows the final ISO date. | Confirms the whole pipeline works end‑to‑end. |

## Obsługa typowych wariantów  

### 1. Inne lokalizacje komórek  

Jeśli Twoja data znajduje się w **B2** lub w nazwanym zakresie, po prostu zamień `"A1"` na odpowiedni adres:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Wiele dat w kolumnie  

Gdy potrzebujesz **extract date from excel** dla wielu wierszy, przeiteruj używany zakres:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Awaryjne rozwiązanie dla dat nie‑era  

Jeśli komórka już zawiera standardowy ciąg daty, parser nadal działa, ale możesz chcieć dodatkowego zabezpieczenia:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Flaga `TryParse` zapobiega wyjątkom i zwraca oryginalną wartość, jeśli konwersja się nie powiedzie.

### 4. Składnik czasu  

Jeśli potrzebujesz także części czasu, użyj `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Daje to pełny znacznik czasu ISO 8601 (`2021-05-01T00:00:00`).

## Pomoc wizualna  

![format datetime to iso example](image.png "Przykład formatowania datetime do iso w C#")

*Alt text:* *przykład formatowania datetime do iso pokazujący wyjście konsoli*

## Najczęściej zadawane pytania  

- **Czy mogę używać tego z plikami .xls?**  
  Tak. Aspose.Cells obsługuje `.xls`, `.xlsx`, `.csv` i wiele innych formatów od razu.

- **Co jeśli skoroszyt jest zabezpieczony hasłem?**  
  Załaduj go przy pomocy `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Czy format ISO jest zależny od ustawień regionalnych?**  
  Nie. Wzorzec `"yyyy-MM-dd"` jest niezależny od kultury, gwarantując ten sam ciąg na każdej maszynie.

- **Czy to działa na .NET Core?**  
  Absolutnie — Aspose.Cells jest zgodny z .NET Standard 2.0.

## Podsumowanie  

Omówiliśmy, jak **format datetime to iso** poprzez **extract date from excel**, parsowanie japońskich era oraz ostateczne **display iso date** w konsoli. Główne kroki — utworzenie skoroszytu, zapis lub załadowanie tekstu era, włączenie parsowania japońskiego era i formatowanie przy użyciu `ToString("yyyy-MM-dd")` — to wszystko, czego potrzebujesz w większości scenariuszy.

Następnie możesz:

- Zapisać daty ISO z powrotem do innej kolumny w celu dalszego przetwarzania.
- Wyeksportować przekształcony skoroszyt do CSV w celu masowego importu.
- Połączyć tę logikę z API webowym, które przyjmuje przesyłane pliki Excel i zwraca daty w formacie JSON‑encoded ISO.

Śmiało eksperymentuj z różnymi formatami dat, strefami czasowymi lub nawet własnymi kalendarzami. Elastyczność Aspose.Cells oznacza, że rzadko napotkasz na przeszkodę.

Miłego kodowania i niech wszystkie Twoje daty będą perfekcyjnie zgodne z ISO!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}