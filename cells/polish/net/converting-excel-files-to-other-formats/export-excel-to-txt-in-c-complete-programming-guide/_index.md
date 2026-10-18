---
category: general
date: 2026-08-11
description: Eksportuj plik Excel do txt w C# z przewodnikiem krok po kroku. Dowiedz
  się, jak przekonwertować xlsx na zwykły tekst przy użyciu Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: pl
lastmod: 2026-08-11
og_description: Szybko eksportuj Excel do txt w C#. Ten tutorial pokazuje, jak konwertować
  pliki xlsx na zwykły tekst, konfigurować formaty i obsługiwać duże arkusze.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Eksportuj Excel do TXT w C# – przewodnik krok po kroku dla programistów
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Eksportowanie Excela do txt w C# – kompletny przewodnik programistyczny
url: /pl/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie Excela do txt w C# – kompletny przewodnik programistyczny

Jeśli potrzebujesz **export excel to txt** możesz uzyskać wynik przy użyciu kilku linii kodu C#. Ten przewodnik pokazuje, jak przekonwertować skoroszyt `.xlsx` na plik tekstowy, zachowując zdefiniowany format danych.

Eksportowanie arkuszy jako plików tekstowych jest częstym wymaganiem, gdy systemy downstream akceptują jedynie dane rozdzielone delimitatorami lub gdy trzeba audytować surowe wartości komórek. W kolejnych sekcjach dowiesz się, jak konfigurować formaty dat i liczb, obsługiwać duże arkusze oraz unikać typowych pułapek.

## Wymagania wstępne do konwersji xlsx na tekst zwykły

* .NET 6.0 (lub nowszy) zainstalowany – kod jest skierowany do .NET Standard 2.0, więc działa również z .NET Framework 4.6+.
* Licencja na **Aspose.Cells** (darmowa wersja ewaluacyjna działa do testów).
* Środowisko IDE, takie jak Visual Studio 2022 lub Visual Studio Code.
* Plik Excel o nazwie `input.xlsx` umieszczony w folderze, do którego możesz odwołać się w swoim projekcie.

Te elementy są jedynymi zewnętrznymi wymaganiami; tutorial nie zależy od dodatkowych pakietów NuGet.

## Jak wyeksportować excel do txt przy użyciu Aspose.Cells

Aspose.Cells udostępnia klasę `ExportTableOptions`, która pozwala kontrolować, jak wartości komórek są renderowane jako ciągi znaków. Ustawiając `ExportAsString` na `true`, wymuszasz zapis każdej komórki jako tekst, co jest niezbędne, gdy potrzebny jest deterministyczny wynik w postaci zwykłego tekstu.

### Krok 1 – załaduj skoroszyt

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Konstruktor `Workbook` odczytuje plik Excel do pamięci. Jeśli plik nie istnieje, zostaje zgłoszony wyjątek, więc w kodzie produkcyjnym warto otoczyć to wywołanie blokiem try‑catch.*

### Krok 2 – pobierz pierwszy arkusz

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Arkusze są indeksowane od zera, więc indeks 0 odnosi się do pierwszej zakładki. Możesz zamienić indeks na nazwę arkusza (`workbook.Worksheets["Sheet1"]`), gdy potrzebujesz odwołać się do konkretnej zakładki.*

### Krok 3 – zdefiniuj opcje eksportu dla konwersji do tekstu

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` zapewnia, że każda komórka, niezależnie od pierwotnego typu, zostaje zamieniona na ciąg znaków w pliku wyjściowym. Właściwości `DateTimeFormat` i `NumberFormat` pozwalają kontrolować, jak wyświetlane są daty i liczby, co jest kluczowe przy **convert xlsx to plain text** dla systemów oczekujących określonego wzorca.*

### Krok 4 – wyeksportuj arkusz jako plik tekstowy

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` zapisuje zawartość arkusza do pliku tekstowego, używając podanych opcji. Domyślnym separatorem jest znak tabulacji (`\t`). Jeśli potrzebujesz innego separatora, możesz użyć przeciążenia przyjmującego instancję `ExportTableOptions` i określić `ExportTableOptions.Separator`. Powstały plik można otworzyć w dowolnym edytorze tekstu lub zaimportować do bazy danych.*

#### Oczekiwany wynik

Assume `input.xlsx` contains:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Przy powyższych opcjach plik `Exported.txt` będzie zawierał:

```
2023-05-01	1,234.50	Sample text
```

Każda kolumna jest oddzielona tabulatorem, daty mają format `yyyy‑MM‑dd`, a liczby używają przecinka jako separatora tysięcy i dwóch miejsc po przecinku.

## Typowe pułapki przy eksporcie arkusza jako plik tekstowy

| Problem | Dlaczego się pojawia | Jak tego uniknąć |
|---------|----------------------|-----------------|
| Formatowanie liczb zależne od ustawień regionalnych | Domyślny format respektuje kulturę systemu operacyjnego, co może skutkować niejednolitym użyciem przecinków lub kropek. | Jawnie ustaw `NumberFormat` w `ExportTableOptions`. |
| Ukryte wiersze lub kolumny pojawiają się w wyniku | Aspose.Cells eksportuje cały używany zakres, w tym ukryte wiersze. | Ustaw `ExportTableOptions.ExportHiddenRows = false` oraz `ExportHiddenColumns = false`, jeśli chcesz je pominąć. |
| Duże arkusze powodują obciążenie pamięci | Cały skoroszyt jest ładowany do pamięci przed eksportem. | Użyj `Workbook.LoadOptions` z `LoadDataOnly = true`, aby zmniejszyć zużycie pamięci, lub przetwarzaj plik w partiach. |
| Komórki z datami zapisane jako tekst w pliku źródłowym | Jeśli komórka już zawiera sformatowany ciąg, eksporter traktuje ją jako tekst i ignoruje `DateTimeFormat`. | Upewnij się, że skoroszyt źródłowy przechowuje daty jako właściwe typy dat Excel. |

Rozwiązanie tych problemów sprawia, że proces **how to export excel worksheet as text** jest niezawodny w różnych środowiskach.

## Rozszerzanie rozwiązania – własne delimitatory i eksport strumieniowy

Jeśli potrzebujesz pliku wartości rozdzielonych przecinkami (CSV) zamiast pliku z tabulatorem, zmodyfikuj opcje:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Dla plików większych niż 500 MB, strumieniowy zapis zapobiega wyczerpaniu pamięci RAM przez aplikację:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Przeciążenie przyjmujące `Stream` zapisuje wiersze stopniowo, co jest idealne dla zadań wsadowych lub usług internetowych zwracających plik tekstowy bezpośrednio klientowi.

## Zweryfikuj wynik programowo

Po zakończeniu eksportu możesz odczytać pierwszą linię z powrotem do pamięci, aby potwierdzić format:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Uruchomienie tego fragmentu powinno wypisać tę samą linię, co w sekcji *Oczekiwany wynik*, dając pewność, że konwersja zakończyła się sukcesem.

## Podsumowanie pełnego kodu

Połączenie wszystkich elementów daje samodzielny program, który możesz skopiować do aplikacji konsolowej:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Skompiluj i uruchom program; plik `Exported.txt` pojawi się w tym samym katalogu co źródłowy skoroszyt.

## Kolejne kroki i tematy powiązane

* **Export worksheet as text file** – eksperymentuj z różnymi delimiterami, kodowaniami (UTF‑8 vs. ASCII) oraz stylami zakończeń linii dla kompatybilności międzyplatformowej.
* **Bulk conversion** – iteruj przez `workbook.Worksheets`, aby wygenerować osobny plik tekstowy dla każdej zakładki.
* **Integration with databases** – przekieruj wygenerowany tekst bezpośrednio do operacji bulk‑insert dla SQL Server lub PostgreSQL.
* **

## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu wraz z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak eksportować pliki Excel w .NET przy użyciu Aspose.Cells: Kompletny przewodnik](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Jak eksportować widoczne wiersze Excel przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Jak eksportować wykresy Excel do PDF przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}