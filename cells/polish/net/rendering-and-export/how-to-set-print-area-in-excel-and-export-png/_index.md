---
category: general
date: 2026-09-27
description: Ustaw obszar wydruku w Excelu i dowiedz się, jak eksportować obrazy PNG
  wybranych komórek. Ten przewodnik obejmuje także zapisywanie zakresu jako obrazu
  oraz dodawanie obrazka do arkusza.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: pl
lastmod: 2026-09-27
og_description: Ustaw obszar wydruku w Excelu i wyeksportuj PNG za pomocą Aspose.Cells.
  Postępuj zgodnie z tym przewodnikiem krok po kroku, aby zapisać zakres jako obraz
  i dodać obraz do arkusza.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Ustaw obszar wydruku w Excelu – eksportuj PNG w C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Jak ustawić obszar wydruku w Excelu i wyeksportować PNG
url: /pl/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić obszar wydruku w Excelu i wyeksportować PNG

Jeśli potrzebujesz **set print area excel** przed tworzeniem obrazu, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Dowiesz się także, jak **how to export png** pliki z określonego zakresu, **save range as image**, oraz **add picture to worksheet** w jednym, powtarzalnym procesie.

Praca z Excelem programowo często oznacza, że chcesz, aby tylko podzbiór komórek — na przykład tabela przestawna lub wykres — stał się obrazem. Definiując najpierw obszar wydruku, zapewniasz, że wyeksportowany PNG zawiera dokładnie te komórki, których oczekujesz, nie więcej i nie mniej. Ten samouczek przeprowadzi Cię przez każdy krok, od wczytania skoroszytu po zapisanie końcowego pliku PNG, i wyjaśni, dlaczego każde ustawienie ma znaczenie.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE C#)  
* Pakiet NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Plik Excel (`input.xlsx`) znajdujący się w znanym katalogu  

Te wymagania zapewniają, że kod działa bez dodatkowej konfiguracji.

## Krok 1: Wczytaj skoroszyt, z którym chcesz pracować

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Klasa `Workbook` reprezentuje cały plik Excel. Wczytanie jej najpierw daje dostęp do arkuszy, komórek i opcji ustawień strony.

## Krok 2: **Set print area excel** dla docelowego zakresu

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Ustawienie **print area** informuje Excel (i Aspose.Cells), które komórki należą do drukowalnej strony. Gdy później wyeksportujesz arkusz jako obraz, renderowany będzie tylko ten obszar, co jest niezbędne dla czystego **export selected cells image**.

## Krok 3: Skonfiguruj opcje eksportu obrazu – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` kontroluje format wyjściowy. Wybierając `ImageFormat.Png`, zapewniasz obraz o wysokiej rozdzielczości i przezroczystym tle, który dobrze działa w kontekstach webowych i desktopowych.

## Krok 4: Utwórz obraz z określonego zakresu i **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Metoda `Pictures.Add` wstawia nowy obraz do arkusza. Przekazując zakres utworzony w Kroku 2, **save range as image** bezpośrednio na arkuszu, co jest przydatne, jeśli później będziesz musiał odwołać się do obrazu w innych częściach skoroszytu.

## Krok 5: **Save the picture as an image file** – ukończenie przepływu **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Wywołanie `Save` zapisuje obraz w systemie plików przy użyciu opcji zdefiniowanych w Kroku 3. Powstały `selected_range.png` zawiera dokładnie komórki określone poleceniem **set print area excel**.

## Pełny, działający przykład

Połączenie wszystkich elementów daje Ci kompaktowy program, który możesz wkleić do dowolnej aplikacji konsolowej:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

A znajdziesz plik `selected_range.png`, który pokazuje tylko komórki od A1 do G20 z `input.xlsx`.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Eksportowany obraz zawiera cały arkusz | Nie zdefiniowano obszaru wydruku | Upewnij się, że **set print area excel** przed tworzeniem obrazu |
| PNG jest rozmyty | Domyślne DPI jest niskie | Ustaw `imageOptions.DpiX` i `imageOptions.DpiY` na wyższą wartość (np. 300) |
| Błąd pliku nie znaleziono | Nieprawidłowa ścieżka katalogu | Użyj `Path.Combine` lub sprawdź dwukrotnie, czy folder istnieje |
| Obraz jest przesunięty | Nieprawidłowe indeksy wiersza/kolumny | Pierwsze dwa parametry `Pictures.Add` to komórka w lewym górnym rogu, w której obraz jest umieszczany; pozostaw je na `0,0` dla czystego eksportu |

## Porada: Eksportuj wiele zakresów w jednym uruchomieniu

Jeśli potrzebujesz **export selected cells image** dla kilku obszarów, powtórz Kroki 2‑5 wewnątrz pętli, zmieniając `printArea` w każdej iteracji. Pamiętaj, aby nadać każdemu obrazowi unikalną nazwę pliku, w przeciwnym razie późniejsze zapisanie nadpisze poprzedni plik.

## Zakończenie

Teraz wiesz, jak **set print area excel**, skonfigurować **how to export png**, **save range as image** oraz **add picture to worksheet** przy użyciu Aspose.Cells. To kompleksowe rozwiązanie pozwala przekształcić dowolny blok komórek w wysokiej jakości PNG przy użyciu kilku linii kodu C#.

Następnie możesz zbadać:

* Dodawanie ramek lub znaków wodnych do wyeksportowanego PNG (wyszukaj *add picture to worksheet* z stylizacją)
* Eksportowanie bezpośrednio do PDF dla raportów do druku (*export selected cells image* → przepływ pracy PDF)
* Automatyzacja procesu dla wielu skoroszytów w zadaniu wsadowym

Śmiało eksperymentuj z różnymi zakresami, ustawieniami DPI lub formatami obrazu, aby dopasować je do potrzeb swojego projektu. Szczęśliwego kodowania!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Ustaw obszar wydruku w Excelu i wyeksportuj do PowerPoint – przewodnik krok po kroku](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Eksportuj obszar wydruku Excel do HTML z Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Jak ustawić obszar wydruku w Excelu przy użyciu Aspose.Cells dla .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}