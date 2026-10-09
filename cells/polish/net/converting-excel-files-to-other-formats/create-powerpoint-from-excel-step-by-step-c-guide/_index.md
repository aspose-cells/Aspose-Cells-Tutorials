---
category: general
date: 2026-03-30
description: Szybko twórz prezentacje PowerPoint z Excela przy użyciu Aspose.Cells
  i Aspose.Slides. Dowiedz się, jak wyeksportować arkusz jako obraz i zapisać prezentację
  jako PPTX w C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: pl
og_description: Utwórz prezentację PowerPoint z Excela w C# przy użyciu Aspose. Wyeksportuj
  arkusz jako obraz, zachowaj edytowalne kształty i zapisz wynik jako plik PPTX.
og_title: Utwórz PowerPoint z Excela – Kompletny samouczek C#
tags:
- Aspose
- C#
- Office Automation
title: Tworzenie PowerPointa z Excela – Przewodnik krok po kroku w C#
url: /pl/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PowerPoint z Excela – Kompletny samouczek C#

Kiedykolwiek potrzebowałeś **utworzyć PowerPoint z Excela**, ale nie byłeś pewien, która biblioteka pozwoli zachować edytowalność wykresów? Nie jesteś sam. W wielu scenariuszach raportowania chcesz zamienić arkusz kalkulacyjny w zestaw slajdów, nie tracąc możliwości późniejszej edycji pól tekstowych. Ten przewodnik pokazuje dokładnie, jak **przekształcić Excel w PowerPoint** przy użyciu Aspose.Cells i Aspose.Slides, a także jak **wyeksportować arkusz jako obraz** i w końcu **zapisać prezentację jako PPTX**.

Przejdziemy przez każdy wiersz kodu, wyjaśnimy *dlaczego* każde ustawienie ma znaczenie i omówimy, co zrobić, gdy Twój skoroszyt zawiera złożone wykresy, które wolisz wyeksportować jako obraz. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową C#, która przyjmuje `ShapesDemo.xlsx` i generuje `Result.pptx` – wszystko z edytowalnymi polami tekstowymi i wyraźnymi obrazami.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (API działa także z .NET Framework, ale .NET 6 jest optymalnym wyborem).  
- Pakiety NuGet **Aspose.Cells** i **Aspose.Slides** (darmowe licencje trial działają w testach).  
- Podstawowa znajomość składni C# – jeśli potrafisz napisać `Console.WriteLine`, jesteś gotowy.  

Nie potrzebujesz dodatkowego COM interopu, nie musisz mieć zainstalowanego Office na serwerze i nie musisz ręcznie kopiować‑wklejać obrazów. Wszystko jest obsługiwane programowo.

---

## Utwórz PowerPoint z Excela – Załaduj skoroszyt i ustaw opcje eksportu

Pierwszą rzeczą, którą robimy, jest otwarcie pliku Excel i poinformowanie Aspose.Cells, jak ma zostać wyrenderowany arkusz. Obiekt `ImageOrPrintOptions` to miejsce, w którym dzieje się magia: włączamy `ExportShapes` i `ExportEditableTextBoxes`, aby wszystkie kształty (w tym wykresy) stały się częścią slajdu **i** pozostały edytowalne po konwersji.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Dlaczego te flagi?**  
- `OnePagePerSheet` zapobiega podziałowi arkusza na wiele slajdów – otrzymujesz jedną, pełnowymiarową grafikę.  
- `ExportShapes` instruuje Aspose.Cells, aby rasteryzował wykresy *i* wektorowe kształty, zachowując ich wygląd.  
- `ExportEditableTextBoxes` to tajny składnik, który pozwala dwukrotnie kliknąć pole tekstowe w PowerPoint i edytować tekst bez ponownego otwierania Excela.

> **Pro tip:** Jeśli potrzebujesz tylko statycznego obrazu wykresu, ustaw `ExportShapes = false` i użyj metody `ExportExcelChartAsPicture` później (zobacz sekcję końcową).

## Konwertuj Excel do PowerPoint – Generuj obraz z arkusza

Mając gotowe opcje, przekształcamy arkusz w obiekt `System.Drawing.Image`. `WorksheetToImageConverter` wykonuje ciężką pracę, stosując właśnie zdefiniowane ustawienia.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Argument `0` wskazuje pierwszą stronę (mamy tylko jedną ze względu na `OnePagePerSheet`). Powstały `sheetImage` zachowuje oryginalną rozdzielczość DPI, więc Twój slajd nie będzie wyglądał pikselowo nawet na wyświetlaczach o wysokiej rozdzielczości.

## Zapisz prezentację jako PPTX – Wstaw obraz na slajd

Teraz tworzymy nowy plik PowerPoint, dodajemy slajd i umieszczamy bitmapę. Aspose.Slides traktuje obraz jako kształt *picture frame*, który możesz później skalować lub przesuwać tak, jak każdy natywny obiekt PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Co zrobić, gdy obraz jest większy niż rozmiar slajdu?**  
> PowerPoint automatycznie przytnie wszystko, co wykracza poza wymiary slajdu. Szybkim rozwiązaniem jest skalowanie obrazu przed wstawieniem:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Następnie możesz przekazać `newWidth` i `newHeight` do `AddPictureFrame`.

## Eksportuj arkusz jako obraz – Zapisz plik PPTX

Na koniec zapisujemy prezentację na dysku. Flaga `SaveFormat.Pptx` zapewnia nowoczesny format OpenXML, który działa we wszystkich recentnych wersjach PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Gdy otworzysz `Result.pptx`, zobaczysz pojedynczy slajd wyglądający dokładnie jak Twój arkusz Excel, ale nadal możesz kliknąć dowolne pole tekstowe i edytować jego zawartość bezpośrednio w PowerPoint.

## Eksportuj wykres Excel jako obraz – Gdy preferowane są obrazy rastrowe

Czasami nie potrzebujesz edytowalnych kształtów; wystarczy wysokiej jakości PNG wykresu. Aspose.Cells może wyeksportować konkretny wykres do obrazu bez konwertowania całego arkusza:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Następnie możesz osadzić `chart.png` na slajdzie w ten sam sposób, w jaki dodaliśmy `sheetImage`. To podejście zmniejsza rozmiar pliku PPTX i jest przydatne, gdy otaczające dane nie są potrzebne na slajdzie.

## Częste pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Tekst jest rozmyty** | Eksport przy niskim DPI (domyślnie 96). | Ustaw `imageOptions.Dpi = 300;` przed konwersją. |
| **Kształty znikają** | `ExportShapes` ustawiono na `false`. | Upewnij się, że `ExportShapes = true`, gdy potrzebujesz edytowalnej grafiki. |
| **Niezgodność rozmiaru slajdu** | Obraz większy niż wymiary slajdu. | Skaluj obraz (zobacz fragment kodu) lub zmień rozmiar slajdu poprzez `presentation.SlideSize`. |
| **Wyjątek licencyjny** | Używanie wersji trial bez prawidłowej aktywacji. | Wywołaj `License license = new License(); license.SetLicense("Aspose.Total.lic");` na początku `Main`. |

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program, gotowy do wklejenia w nowym projekcie konsolowym. Zamień `YOUR_DIRECTORY` na folder, w którym znajduje się Twój plik Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Oczekiwany wynik:**  
Uruchomienie programu wypisuje `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Otwarcie pliku PPTX pokazuje pojedynczy slajd odzwierciedlający oryginalny arkusz Excel, z edytowalnymi polami tekstowymi.

## Podsumowanie i kolejne kroki

Teraz wiesz, jak **utworzyć PowerPoint z Excela** przy użyciu potężnych API Aspose, jak **wyeksportować arkusz jako obraz** oraz jak **zapisać prezentację jako PPTX**, zachowując edytowalność. Ten sam wzorzec działa dla skoroszytów wielo‑arkuszowych – po prostu iteruj po `workbook.Worksheets` i dodawaj nowy slajd dla każdego.

**Co warto zbadać dalej?**  

- **Konwersja wsadowa:** Przejdź przez folder plików Excel i generuj zestaw slajdów dla każdego pliku.  
- **Dynamiczne układy:** Użyj `slide.LayoutSlide`, aby zastosować wcześniej zaprojektowane szablony PowerPoint.  
- **Eksport tylko wykresu:** Połącz fragment „Export Excel chart as picture” z placeholderami slajdów, aby uzyskać lżejszą prezentację.  
- **Zaawansowane stylizacje:** Dodaj własne tła slajdów, przejścia lub animacje za pomocą Aspose.Slides.

Śmiało eksperymentuj – zmieniaj DPI, zamień `ShapeType.Ellipse` na okrągłą ramkę obrazu, a nawet osadzaj wiele obrazów na jednym slajdzie. Niebo jest granicą, gdy masz programistyczną kontrolę nad

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}