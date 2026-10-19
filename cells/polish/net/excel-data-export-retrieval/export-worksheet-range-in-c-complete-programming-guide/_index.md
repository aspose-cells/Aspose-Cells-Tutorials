---
category: general
date: 2026-05-04
description: Eksportuj zakres arkusza przy użyciu C# z niestandardowym formatowaniem.
  Dowiedz się, jak wyeksportować zakres Excela i jak dostosować eksport komórek w
  kilku prostych krokach.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: pl
og_description: Eksportuj zakres arkusza kalkulacyjnego przy użyciu C#. Ten przewodnik
  pokazuje, jak szybko i niezawodnie eksportować zakres Excela oraz dostosowywać eksport
  komórek.
og_title: Eksport zakresu arkusza w C# – Kompletny przewodnik programistyczny
tags:
- C#
- Excel
- Data Export
title: Eksport zakresu arkusza w C# – Kompletny przewodnik programistyczny
url: /pl/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport zakresu arkusza w C# – Kompletny przewodnik programistyczny

Kiedykolwiek potrzebowałeś **eksportować zakres arkusza**, ale domyślny wynik po prostu nie spełniał Twoich oczekiwań? Nie jesteś sam — wielu programistów napotyka ten problem, gdy próbują wyciągnąć blok komórek do pliku CSV lub JSON. Dobra wiadomość? Kilka linijek C# pozwoli Ci nie tylko **eksportować zakres Excel**, ale także **dostosować eksport komórek** do dowolnego formatu wyjściowego.

W tym samouczku przejdziemy przez realistyczny scenariusz: pobranie komórek *A1:D10* z skoroszytu Excel, zamiana każdej wartości na łańcuch w nawiasach kwadratowych oraz zapis wyniku do pliku. Po zakończeniu będziesz dokładnie wiedział **jak eksportować zakres arkusza** z pełną kontrolą nad reprezentacją każdej komórki oraz poznasz kilka wskazówek dotyczących przypadków brzegowych, które mogą się pojawić później.

## Czego będziesz potrzebować

- .NET 6 lub nowszy (kod działa również z .NET Framework 4.7+)  
- Pakiet NuGet **GemBox.Spreadsheet** (lub dowolna biblioteka oferująca `ExportTableOptions`; prezentowane API pochodzi z GemBox)  
- Podstawowa znajomość składni C# – nic skomplikowanego, tylko standardowe instrukcje `using` i tworzenie obiektów  

Jeśli masz to wszystko, możesz od razu przystąpić do działania.

## Krok 1: Konfiguracja opcji eksportu – główny punkt kontrolny  

Pierwszą rzeczą, którą robisz, jest utworzenie instancji `ExportTableOptions` i ustawienie, aby każda komórka była traktowana jako łańcuch znaków. To podstawa **jak eksportować zakres Excel** przy zachowaniu spójnego typu danych.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Dlaczego wymusić eksport jako łańcuch?*  
Gdy później będziesz dostosowywać każdą komórkę, wstawisz nawiasy i ewentualnie inne symbole. Trzymanie wszystkiego jako łańcucha zapobiega niespodziewanym konwersjom typów (np. daty zamieniające się w liczby seryjne).

## Krok 2: Podłączenie się do zdarzenia CellExport – dostosowywanie każdej komórki  

Teraz przychodzi najciekawsza część: **jak dostosować eksport komórek**. GemBox wywołuje zdarzenie `CellExport` dla każdej komórki, która ma zostać zapisana. Obsługując je, możesz otoczyć wartość nawiasami, dodać prefiks lub nawet całkowicie pominąć komórkę.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Wskazówka:* Jeśli chcesz modyfikować tylko komórki liczbowe, sprawdź `e.Value.GetType()` przed dodaniem nawiasów. Ten mały warunek może uchronić Cię przed przypadkowym zniekształceniem tekstu nagłówka.

## Krok 3: Eksport żądanego zakresu – główna akcja  

Mając już skonfigurowane opcje, wywołujesz `ExportTable`. Metoda przyjmuje wczytany skoroszyt, adres zakresu, który chcesz wyeksportować, oraz wcześniej przygotowane opcje.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Przeciążenie, którego użyliśmy, zapisuje bezpośrednio do pliku (domyślnie CSV). Jeśli wolisz łańcuch w pamięci, zamień ostatni argument na `StringWriter` i odczytaj wynik później.

### Pełny działający przykład

Poniżej znajduje się samodzielna aplikacja konsolowa, którą możesz wkleić do nowego projektu i uruchomić od razu (wystarczy podmienić ścieżki plików).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Oczekiwany wynik (fragment CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Każda komórka od *A1* do *D10* jest teraz otoczona nawiasami kwadratowymi, dokładnie tak, jak zdefiniowano w obsłudze `CellExport`.

## Obsługa typowych przypadków brzegowych  

### 1. Puste komórki  
Jeśli komórka jest pusta, `e.Value` będzie `null`. Próba sformatowania jej przy użyciu interpolacji łańcucha spowoduje wyjątek. Zabezpiecz się przed tym:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Duże zakresy  
Eksport milionów wierszy może przekroczyć limity pamięci. W takim scenariuszu strumieniuj wyjście zamiast ładować cały skoroszyt do pamięci:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Różne separatorki  
CSV to nie jedyny format, którego możesz potrzebować. Zmien separator, modyfikując `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Najczęściej zadawane pytania  

**P: Czy to działa z plikami .xlsx tworzonymi w Excel 365?**  
Zdecydowanie tak. GemBox odczytuje nowoczesny format OpenXML bez dodatkowej konfiguracji.

**P: Czy mogę wyeksportować wiele nieciągłych zakresów jednocześnie?**  
Nie bezpośrednio przy użyciu pojedynczego wywołania `ExportTable`. Musisz przeiterować każdy zakres (`"A1:D10"`, `"F1:H5"` itp.) i samodzielnie połączyć wyniki.

**P: Co zrobić, jeśli potrzebuję zastosować różne formatowanie w zależności od kolumny?**  
W obsłudze `CellExport` masz dostęp do `e.ColumnIndex`. Użyj instrukcji `switch`, aby zastosować logikę specyficzną dla danej kolumny.

## Podsumowanie  

Omówiliśmy **jak eksportować zakres arkusza** z pełną kontrolą nad wyglądem każdej komórki, pokazaliśmy **jak eksportować zakres Excel** przy użyciu `ExportTableOptions` oraz **jak dostosować eksport komórek** za pomocą zdarzenia `CellExport`. Kompletny kod mieści się w kilkudziesięciu linijkach C#, a jednocześnie jest na tyle elastyczny, by sprawdzić się w produkcyjnych scenariuszach.

Co dalej? Spróbuj zamienić otaczające nawiasy na format przyjazny JSON lub poeksperymentuj z logiką warunkową pomijającą ukryte wiersze. Możesz także zbadać eksport bezpośrednio do `MemoryStream` w odpowiedziach API webowych — bez potrzeby tworzenia plików tymczasowych.

Jeśli dotrzymałeś instrukcji, masz teraz solidny, wielokrotnego użytku wzorzec do eksportowania dowolnego zakresu arkusza dokładnie w taki sposób, jaki potrzebujesz. Powodzenia w kodowaniu i daj znać w komentarzu, jeśli napotkasz trudności!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}