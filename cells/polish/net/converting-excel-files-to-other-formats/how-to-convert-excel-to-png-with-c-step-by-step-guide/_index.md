---
category: general
date: 2026-10-10
description: Szybko konwertuj Excel na PNG przy użyciu Aspose.Cells w C#. Dowiedz
  się, jak wyeksportować zakres Excela, zapisać plik Excel jako PNG oraz przekonwertować
  arkusz na obraz w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: pl
lastmod: 2026-10-10
og_description: Konwertuj Excel na PNG natychmiast przy użyciu Aspose.Cells. Ten samouczek
  pokazuje, jak wyeksportować zakres Excel, zapisać Excel jako PNG oraz przekonwertować
  arkusz na obraz.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Konwertuj Excel do PNG w C# – kompletny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Jak przekonwertować Excel na PNG w C# – przewodnik krok po kroku
url: /pl/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować Excel na PNG w C# – przewodnik krok po kroku

Jeśli potrzebujesz **konwertować Excel na PNG** programowo, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells dla .NET. Niezależnie od tego, czy tworzysz usługę raportowania, czy zautomatyzowany pulpit nawigacyjny, nauczysz się eksportować zakres Excela, zapisywać wynik jako plik PNG oraz obsługiwać typowe przypadki brzegowe.

Przejdziesz przez każdy wymagany krok — od dodania pakietu NuGet po renderowanie określonego obszaru arkusza — abyś mógł zintegrować rozwiązanie z dowolnym projektem C# bez konieczności szukania dodatkowych zasobów.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy (kod działa również z .NET Framework 4.6+)
* Visual Studio 2022 (lub dowolne IDE obsługujące C#)
* Ważną licencję Aspose.Cells dla .NET (bezpłatna wersja próbna wystarczy do oceny)
* Plik Excel o nazwie **Pivot.xlsx** znajdujący się w folderze, do którego możesz odwołać się w kodzie (w tutorialu użyto `YOUR_DIRECTORY` jako symbolu zastępczego)

> **Pro tip:** Zainstaluj pakiet Aspose.Cells za pomocą konsoli Menedżera Pakietów NuGet:  
> `Install-Package Aspose.Cells`

## Konwersja Excel do PNG – pełny przegląd kodu

Poniższy kompletny program ładuje skoroszyt, konfiguruje opcje obrazu i renderuje określony zakres komórek do pliku PNG. Wszystkie wymagane dyrektywy `using` są uwzględnione, więc możesz skopiować kod do nowego projektu konsolowego i od razu go uruchomić.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Jak działa kod

* **Ładowanie skoroszytu** – `Workbook` odczytuje plik `.xlsx` do pamięci, dając dostęp do wszystkich arkuszy.
* **ImageOrPrintOptions** – Ten obiekt instruuje Aspose.Cells, aby wygenerował PNG (`ImageFormat.Png`). Możesz także dostosować DPI, skalowanie lub kolor tła, jeśli zajdzie taka potrzeba.
* **RenderRangeToImage** – Metoda `RenderRangeToImage` przyjmuje trzy argumenty: zakres komórek (`"A1:H30"`), ścieżkę docelowego pliku oraz opcje obrazu. To podstawowa operacja, która **export excel range** do obrazu PNG.
* **Wynik** – Po wykonaniu znajdziesz plik `Pivot.png` w określonym folderze, zawierający dokładną wizualną reprezentację wybranych komórek.

## Eksport zakresu Excela do PNG – dostosowywanie wyjścia

Jeśli potrzebujesz **export excel range** inny niż `A1:H30`, po prostu zmień zmienną `range`. Metoda akceptuje dowolny adres w stylu Excel, w tym nazwy zakresów:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Możesz także wyeksportować cały arkusz, używając `"A1:Z1000"` (lub większego adresu) albo wywołując `RenderToImage` bez parametru zakresu.

## Zapisz Excel jako PNG z dodatkowymi ustawieniami

Czasami chcesz, aby PNG miał określoną rozdzielczość do druku lub użytku w sieci. Dostosuj `ImageOrPrintOptions` w następujący sposób:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Te ustawienia ilustrują, jak **save excel as png** z niestandardowym DPI i przezroczystością, dając pełną kontrolę nad ostateczną jakością obrazu.

## Jak eksportować Excel – obsługa wielu arkuszy

Przykład odnosi się do pierwszego arkusza (`Worksheets[0]`). Aby **convert worksheet to image** inny arkusz, odwołaj się do niego po indeksie lub nazwie:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Przetwarzanie każdego arkusza w pętli jest proste:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Przypadki brzegowe i rozwiązywanie problemów

| Sytuacja | Zalecane podejście |
|-----------|----------------------|
| **Bardzo duży zakres** (np. cały skoroszyt) | Stopniowo zwiększaj `HorizontalResolution`/`VerticalResolution`, aby uniknąć `OutOfMemoryException`. Rozważ eksportowanie każdego arkusza osobno. |
| **Scalone komórki** | Aspose.Cells automatycznie zachowuje wygląd scalonych komórek, ale sprawdź wynik, jeśli zależy Ci na dokładnych szerokościach kolumn. |
| **Formuły odwołujące się do plików zewnętrznych** | Upewnij się, że te pliki są dostępne przed załadowaniem skoroszytu; w przeciwnym razie renderowany obraz może zawierać nieaktualne wartości. |
| **Brak licencji** | Wersja próbna dodaje znak wodny. Zastosuj ważną licencję (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) przed renderowaniem, aby uzyskać czysty PNG. |

## Kompletny działający przykład

Poniżej znajduje się samodzielny program, który możesz skompilować i uruchomić. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Oczekiwany wynik**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Otwórz `Pivot.png` w dowolnym przeglądarce obrazów — zobaczysz dokładny układ wizualny komórek A1 do H30, łącznie z formatowaniem, kolorami i obramowaniami.

## Podsumowanie

Masz teraz sprawdzoną metodę **convert Excel to PNG** przy użyciu C#. Tutorial obejmował **export excel range**, **save excel as png** oraz **convert worksheet to image** z opcjami konfiguracyjnymi i wskazówkami najlepszych praktyk.  

Od tego momentu możesz:

* Zintegrować kod z API webowym, aby generować obrazy na żądanie.  
* Połączyć wynik PNG z generowaniem PDF dla raportów wieloformatowych.  
* Eksplorować inne formaty obrazu (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) poprzez zmianę właściwości `ImageFormat`.

Śmiało eksperymentuj z różnymi zakresami, rozdzielczościami i wyborem arkuszy, aby dopasować rozwiązanie do swojego scenariusza automatyzacji.

---


## Co warto nauczyć się dalej?


Poniższe tutoriale dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG, TIFF, and PDF in Java using Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Mastering Aspose.Cells Java: Convert Excel to PNG with a Custom Stream Provider](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}