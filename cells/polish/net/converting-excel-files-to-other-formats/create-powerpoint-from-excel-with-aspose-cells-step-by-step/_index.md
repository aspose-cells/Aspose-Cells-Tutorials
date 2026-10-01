---
category: general
date: 2026-10-01
description: Utwórz prezentację PowerPoint z pliku Excel przy użyciu Aspose.Cells
  w C#. Eksportuj Excel do PowerPoint i szybko konwertuj XLSX na PPTX, korzystając
  z pełnego przykładu kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: pl
lastmod: 2026-10-01
og_description: Utwórz prezentację PowerPoint z Excela przy użyciu Aspose.Cells w
  C#. Dowiedz się, jak wyeksportować Excel do PowerPoint i przekonwertować XLSX na
  PPTX w kilku linijkach kodu.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Tworzenie prezentacji PowerPoint z Excela przy użyciu Aspose.Cells – szybki
  przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Utwórz PowerPoint z Excela przy użyciu Aspose.Cells – przewodnik krok po kroku
url: /pl/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie PowerPointa z Excela przy użyciu Aspose.Cells – przewodnik krok po kroku

Jeśli potrzebujesz **utworzyć PowerPointa z Excela**, ten tutorial pokaże Ci, jak to zrobić przy pomocy Aspose.Cells dla .NET. Nauczysz się **eksportować Excel do PowerPointa**, konwertować skoroszyt XLSX na prezentację PPTX oraz dostosowywać powstałe slajdy bez opuszczania projektu C#.

Poradnik obejmuje wszystko, co jest potrzebne do uruchomienia kodu na .NET 6 lub nowszym, w tym konfigurację projektu, wymagane pakiety NuGet oraz kompletny, gotowy do uruchomienia przykład. Po zakończeniu będziesz mieć plik PowerPoint, który zawiera oryginalny wykres Excel dokładnie tak, jak wygląda w skoroszycie.

## Co będzie potrzebne

| Wymaganie | Powód |
|---|---|
| .NET 6 SDK lub nowszy | Dostarcza środowisko uruchomieniowe dla aplikacji konsolowej C# |
| Visual Studio 2022 (lub dowolne IDE) | Umożliwia łatwe tworzenie projektu i debugowanie |
| Pakiet NuGet Aspose.Cells dla .NET | Udostępnia klasę `Workbook` oraz API eksportu |
| Plik Excel (`.xlsx`) zawierający przynajmniej jeden wykres | Źródłowe dane dla slajdu PowerPoint |

> **Pro tip:** Aspose.Cells działa na Windows, Linux i macOS, więc możesz uruchamiać ten sam kod w kontenerach Docker lub w pipeline’ach CI.

## Krok 1: Utwórz nowy projekt konsolowy i dodaj Aspose.Cells

Otwórz terminal (lub konsolę Menedżera Pakietów w Visual Studio) i uruchom:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

Polecenie `dotnet add package` pobiera najnowszą stabilną wersję **Aspose.Cells**, która zawiera metodę `ExportPptx` używaną później.

## Krok 2: Dodaj źródłowy skoroszyt Excel

Umieść plik Excel, który chcesz skonwertować, w folderze projektu. W tym tutorialu używamy `ChartOle.xlsx`, który zawiera pojedynczy wykres na pierwszym arkuszu.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Krok 3: Napisz kod, który **tworzy PowerPointa z Excela**

Otwórz `Program.cs` i zastąp jego zawartość następującym kodem. Przykład demonstruje **podstawową operację eksportu** oraz pokazuje, jak obsłużyć typowe przypadki brzegowe, takie jak brakujące pliki i nieobsługiwane typy wykresów.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Dlaczego to działa

* `Workbook` odczytuje cały plik Excel, w tym osadzone wykresy, tabele i formatowanie.
* `ExportPptx` konwertuje aktywny arkusz w zestaw slajdów PPTX. Metoda automatycznie przekształca wykresy Excel w kształty PowerPointa, zachowując wierność wizualną.
* Kod otacza operację w bloku `try/catch`, aby wyświetlić błędy, takie jak niepowodzenia **convert XLSX to PPTX** spowodowane uszkodzonymi plikami.

## Krok 4: Uruchom program i zweryfikuj wynik

Uruchom aplikację:

```bash
dotnet run
```

Powinieneś zobaczyć komunikat w konsoli:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Otwórz `Exported.pptx` w Microsoft PowerPoint lub dowolnym kompatybilnym podglądzie. Pierwszy slajd wyświetla wykres dokładnie tak, jak wyglądał w `ChartOle.xlsx`. To potwierdza, że pomyślnie **wygenerowano PowerPointa z Excela**.

## Krok 5: Zaawansowane – eksport wielu arkuszy lub własne układy slajdów

Podstawowy przykład eksportuje tylko pierwszy arkusz. W rzeczywistych scenariuszach możesz potrzebować:

* **Eksportować kilka arkuszy** do oddzielnych slajdów.
* **Kontrolować rozmiar slajdu** lub dodać placeholder tytułu.
* **Uwzględnić ukryte arkusze** w konwersji.

Poniżej znajduje się zwięzły fragment kodu, który iteruje po wszystkich arkuszach i dodaje każdy jako osobny slajd:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Uwaga:** Zaawansowany fragment wymaga biblioteki **Aspose.Slides for .NET**. Jeśli potrzebujesz tylko prostej konwersji jednego arkusza, wcześniejsze wywołanie `ExportPptx` jest wystarczające.

## Typowe pułapki i jak ich unikać

| Problem | Przyczyna | Rozwiązanie |
|---|---|---|
| Pusty slajd po eksporcie | Arkusz nie zawiera widocznych obiektów | Upewnij się, że przed wywołaniem `ExportPptx` istnieje przynajmniej jeden wykres, tabela lub kształt. |
| Brak czcionek w PowerPoint | Czcionka nie jest zainstalowana na maszynie, na której otwierany jest PPTX | Osadź wymagane czcionki w skoroszycie Excel lub zainstaluj je na docelowym systemie. |
| Nieoczekiwane skalowanie | Duży wykres przekracza wymiary slajdu | Dostosuj właściwość `PageSetup.Zoom` arkusza przed eksportem. |
| `convert XLSX to PPTX` rzuca `NotSupportedException` | Typ wykresu nieobsługiwany przez Aspose.Cells (np. mapy 3‑D) | Zamień wykres na obsługiwany typ lub najpierw wyeksportuj arkusz jako obraz. |

Rozwiązanie tych przypadków brzegowych zapewnia niezawodny **workflow eksportu Excel do PowerPoint** w środowiskach produkcyjnych.

## Podsumowanie

Teraz wiesz, jak **tworzyć PowerPointa z Excela** przy użyciu Aspose.Cells dla .NET. Tutorial obejmował:

* Konfigurację projektu i instalację NuGet
* Ładowanie skoroszytu Excel i wywołanie `ExportPptx`
* Uruchomienie kodu i weryfikację wygenerowanego PPTX
* Rozszerzenie rozwiązania o obsługę wielu arkuszy i własnych układów
* Praktyczne wskazówki, jak unikać typowych problemów konwersji

Dzięki tej wiedzy możesz automatyzować generowanie raportów, budować pipeline’y prezentacji lub integrować konwersję Excel‑do‑PowerPoint w dowolnej aplikacji C#. Eksperymentuj z różnymi typami wykresów, dodawaj tytuły slajdów lub łącz eksport z Aspose.Slides, aby uzyskać pełnoprawne tworzenie prezentacji.

--- 

*Gotowy na dalsze eksploracje? Sprawdź powiązane tematy, takie jak **convert Excel to PDF**, **embed Excel data in Word**, lub **use Aspose.Slides to programmatically edit PPTX files**.*

## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}