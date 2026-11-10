---
category: general
date: 2026-10-13
description: Dowiedz się, jak zapisać plik Excel jako TXT przy użyciu Aspose.Cells.
  Ten przewodnik obejmuje eksport Excela do TXT, zapis wartości w komórce oraz ustawianie
  istotnych cyfr w kilku prostych krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: pl
lastmod: 2026-10-13
og_description: Zapisz plik Excel jako TXT przy użyciu Aspose.Cells. Dowiedz się,
  jak wyeksportować Excel do TXT, zapisać wartość w komórce i ustawić liczbę znaczących
  cyfr w kilku linijkach kodu C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Zapisz Excel jako TXT – przewodnik krok po kroku dla programistów .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Jak zapisać plik Excel jako TXT przy użyciu Aspose.Cells w C#
url: /pl/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać Excel jako TXT przy użyciu Aspose.Cells w C#

Jeśli potrzebujesz szybko **zapisać Excel jako TXT**, ten tutorial pokazuje kompletny proces w mniej niż pięć minut. Zobaczysz, jak wyeksportować Excel do TXT, zapisać wartość w komórce i ustawić znaczące cyfry, aby plik tekstowy zawierał dokładnie dane, których oczekujesz.

Eksportowanie arkusza kalkulacyjnego jako TXT jest przydatne, gdy systemy downstream akceptują wyłącznie dane w formacie czystego tekstu, gdy musisz generować logi lub gdy chcesz uzyskać czytelny dla człowieka zrzut obliczeń. Poniższy przykład działa z Aspose.Cells v25.10 lub nowszym i uruchamia się na dowolnym środowisku .NET 6+.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Licencjonowaną kopię **Aspose.Cells for .NET** (bezpłatna wersja próbna wystarczy do testów).
* Zainstalowany .NET 6 SDK lub nowszy.
* IDE, takie jak Visual Studio 2022, VS Code lub Rider.
* Podstawową znajomość C# — nie wymagana jest zaawansowana automatyzacja Excela.

Możesz zainstalować pakiet NuGet Aspose.Cells za pomocą:

```bash
dotnet add package Aspose.Cells
```

## Krok 1: Utwórz skoroszyt i uzyskaj dostęp do pierwszego arkusza (save excel as txt)

Pierwszą rzeczą, którą robisz, gdy chcesz **zapisać Excel jako TXT**, jest utworzenie obiektu `Workbook`. Obiekt ten reprezentuje cały plik Excel w pamięci.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Dlaczego to ważne:** Klasa `Workbook` jest punktem wejścia dla wszystkich operacji na arkuszach. Rozpoczynając od nowego skoroszytu, unikasz ukrytych formatowań, które mogłyby wpłynąć na wynik w formacie czystego tekstu.

## Krok 2: Zapisz liczbę wysokiej precyzji w komórce (write value to cell)

Teraz musisz **zapisać wartość w komórce** A1. Metoda `PutValue` automatycznie wykrywa typ danych i zapisuje je jako wartość liczbową.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Wskazówka:** Jeśli później będziesz potrzebować zapisać ciągi znaków, daty lub formuły, ta sama metoda `PutValue` działa — wystarczy przekazać odpowiedni typ .NET.

## Krok 3: Skonfiguruj opcje eksportu, aby zachować tylko wymaganą precyzję (set significant digits)

Podczas eksportu do pliku TXT często chcesz ograniczyć liczbę cyfr, aby zmniejszyć rozmiar pliku lub dopasować się do specyfikacji downstream. Klasa `TxtSaveOptions` udostępnia właściwość `SignificantDigits` w tym celu.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Dlaczego warto ustawić znaczące cyfry:** Bez tego ustawienia Aspose.Cells zapisuje pełną wartość podwójnej precyzji, co może skutkować długimi ciągami, takimi jak `12345.6789012345`. Ustawienie `SignificantDigits = 6` przycina wynik do `12345.7`, spełniając większość wymagań raportowych.

## Krok 4: Wyeksportuj skoroszyt jako plik TXT (export excel to txt)

Na koniec **eksportujesz Excel do TXT**, wywołując `Workbook.Save` z wcześniej skonfigurowanymi opcjami.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Po zakończeniu działania kodu, plik `LimitedDigits.txt` zawiera:

```
12345.7
```

> **Weryfikacja wyniku:** Otwórz plik w dowolnym edytorze tekstu (Notepad, VS Code), aby potwierdzić, że obecne są tylko sześć znaczących cyfr i że nie pojawiły się dodatkowe przecinki ani tabulatory jako delimitery.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się samodzielna aplikacja konsolowa, którą możesz skopiować, wkleić i od razu uruchomić.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Wyjaśnienie każdego bloku**

| Blok | Cel |
|-------|---------|
| `using Aspose.Cells;` | Importuje przestrzeń nazw Aspose.Cells wymaganą dla `Workbook`, `Worksheet` i `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Tworzy pusty skoroszyt Excel w pamięci. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 z liczbą podwójnej precyzji. |
| `TxtSaveOptions` | Konfiguruje zachowanie **set significant digits** przy eksporcie do TXT. |
| `workbook.Save(..., txtOptions);` | Wykonuje operację **export excel to txt**, tworząc plik tekstowy. |

## Przypadki brzegowe i dodatkowe wskazówki

| Scenariusz | Jak postąpić |
|----------|---------------|
| **Duże arkusze** (wiele wierszy/kolumn) | Użyj `txtOptions.Encoding = Encoding.UTF8`, jeśli potrzebujesz wsparcia Unicode, i rozważ strumieniowy zapis przy pomocy `Workbook.Save(Stream, txtOptions)`, aby uniknąć dużego zużycia pamięci. |
| **Niestandardowe delimitery** (wartości rozdzielane przecinkami) | `TxtSaveOptions` udostępnia także `Separator` — ustaw go na `','`, aby uzyskać wyjście w stylu CSV, zachowując format TXT. |
| **Zachowanie formuł** | Ustaw `txtOptions.ExportFormulas = true`, aby zapisać tekst formuły zamiast wyliczonej wartości. |
| **Lokalne separatory dziesiętne** | Dostosuj `txtOptions.DecimalSeparator` do `','` dla europejskich ustawień regionalnych. |
| **Wiele arkuszy** | Przejdź pętlą po `workbook.Worksheets` i wywołaj `Save` dla każdego, dodając nazwę arkusza do nazwy pliku. |

## Najczęściej zadawane pytania

**P: Czy `SignificantDigits` zaokrągla czy obcina?**  
O: Zaokrągla do najbliższej wartości na podstawie określonej liczby znaczących cyfr, zapewniając matematyczną dokładność do tej precyzji.

**P: Czy mogę eksportować bezpośrednio do strumienia pamięci?**  
O: Tak. Zastąp ścieżkę pliku instancją `MemoryStream`: `workbook.Save(stream, txtOptions);`. To przydatne w API webowych, które muszą zwrócić zawartość TXT bez zapisywania na dysku.

**P: Co zrobić, jeśli muszę zachować oryginalne formatowanie (np. daty)?**  
O: Użyj `txtOptions.ExportFormattedValues = true`. Wymusza to zapisanie wyświetlanego tekstu komórki zamiast surowej wartości.

## Podsumowanie

Teraz wiesz, jak **zapisać Excel jako TXT** z pełną kontrolą nad precyzją, formatowaniem i miejscem docelowym. Postępując zgodnie z czterema krokami — utwórz skoroszyt, **write value to cell**, **set significant digits** i **export excel to txt** — możesz zintegrować eksport do czystego tekstu w dowolnej aplikacji .NET.

Następnie odkryj powiązane tematy, takie jak **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, lub **use Aspose.Cells to generate JSON reports**. Każdy z nich opiera się na tych samych podstawowych koncepcjach, dając Ci wszechstronne narzędzie do wymiany danych między platformami.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}