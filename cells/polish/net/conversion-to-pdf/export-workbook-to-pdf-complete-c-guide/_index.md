---
category: general
date: 2026-02-26
description: Eksportuj skoroszyt do PDF z osadzonymi czcionkami oraz eksportuj wykresy
  do PowerPointa w C#. Dowiedz się, jak skopiować arkusz tabeli przestawnej i zapisać
  skoroszyt jako PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: pl
og_description: Eksportuj skoroszyt do PDF z osadzonymi czcionkami oraz eksportuj
  wykresy do PowerPointa w C#. Postępuj zgodnie z przewodnikiem krok po kroku, aby
  skopiować tabele przestawne i zapisać jako PPTX.
og_title: Eksportowanie skoroszytu do PDF – Kompletny przewodnik C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Eksportowanie skoroszytu do PDF – Kompletny przewodnik C#
url: /pl/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie skoroszytu do PDF – Kompletny przewodnik C#

Eksportowanie skoroszytu do PDF jest częstym wymogiem, gdy trzeba udostępnić raporty interesariuszom, którzy nie mają zainstalowanego Excela. W tym samouczku pokażemy także, jak **wyeksportować wykresy do PowerPoint**, skopiować **arkusz tabeli przestawnej** oraz osadzić czcionki, aby PDF wyglądał dokładnie tak jak projekt na ekranie.  

Zastanawiałeś się kiedyś, dlaczego niektóre pliki PDF tracą pierwotny układ lub dlaczego slajdy PowerPoint kończą się brakującymi kształtami? Odpowiedź zwykle leży w brakujących opcjach podczas procesu eksportu. Po przeczytaniu tego przewodnika będziesz mieć jedną, wielokrotnego użytku metodę C#, która rozwiązuje wszystkie te problemy – koniec z ręcznym kopiowaniem‑wklejaniem i kombinowaniem ustawień eksportu.

## Czego się nauczysz

- Jak utworzyć skoroszyt, dodać wyrażenia Smart Marker i je przetworzyć.  
- Jak **skopiować arkusz tabeli przestawnej** bez uszkadzania źródła danych.  
- Jak **wyeksportować wykresy, kształty i pola tekstowe** do prezentacji PowerPoint, zachowując ich edytowalność.  
- Jak **osadzić standardowe czcionki** podczas eksportu do PDF, aby uzyskać spójne renderowanie na dowolnym komputerze.  
- Jak **zapisać skoroszyt jako PPTX** przy użyciu podejścia `save workbook as pptx`.  

Wszystko to działa z najnowszymi bibliotekami Aspose.Cells i Aspose.Slides .NET (wersja 23.11 w momencie pisania). Bez zewnętrznych narzędzi, bez skryptów post‑processingowych – czysty C#.

> **Wskazówka:** Jeśli już używasz Aspose w swoim projekcie, możesz wkleić fragmenty kodu tak, jak są; w przeciwnym razie najpierw dodaj pakiety NuGet `Aspose.Cells` i `Aspose.Slides`.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7.2).  
- Visual Studio 2022 (lub dowolne inne IDE).  
- Aspose.Cells .NET i Aspose.Slides .NET zainstalowane przez NuGet.  
- Podstawowa znajomość C# oraz koncepcji Excela, takich jak Smart Markers i Tabele przestawne.

---

![Diagram eksportu skoroszytu do PDF](export-workbook-to-pdf.png "Schemat przepływu eksportu skoroszytu do PDF pokazujący wyjścia PDF i PPTX")

## Eksportowanie skoroszytu do PDF – implementacja krok po kroku

Poniżej pełny, gotowy do uruchomienia przykład. Tworzy skoroszyt, wstrzykuje wyrażenia Smart Marker, przetwarza je, kopiuje zakres tabeli przestawnej i na końcu zapisuje zarówno plik PDF, jak i PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Dlaczego to działa

1. **Przetwarzanie Smart Marker** pozwala wypełnić skoroszyt dowolnym źródłem danych (JSON, DataTables itp.) bez pisania pętli.  
2. **DetailSheetNewName** tworzy osobny arkusz dla każdego działu, dając czystą zakładkę per‑dział.  
3. **Kopiowanie zakresu** (`sourceRange.Copy`) duplikuje tabelę przestawną *łącznie* z jej pamięcią podręczną, więc skopiowany arkusz zachowuje się dokładnie tak jak oryginał.  
4. **PresentationOptions** z `ExportCharts`, `ExportShapes` i `ExportTextBoxes` instruuje Aspose, aby renderował te obiekty jako natywne elementy PowerPoint, zachowując ich edytowalność.  
5. **PdfSaveOptions.EmbedStandardFonts** zapewnia, że PDF wygląda identycznie na maszynach, które nie mają zainstalowanych oryginalnych czcionek.

Wynikiem są dwa pliki – `FinalReport.pdf` i `FinalPresentation.pptx` – które można wysłać e‑mailem, zarchiwizować lub otworzyć w dowolnym przeglądarce bez utraty jakości.

## Eksport wykresów do PowerPoint (zapis skoroszytu jako PPTX)

Jeśli Twój raport zawiera wykresy, prawdopodobnie będziesz chciał, aby były edytowalne w PowerPoint. Kluczem jest klasa `PresentationOptions`. Oto skoncentrowany fragment kodu pokazujący wyłącznie część eksportu wykresów:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Co się dzieje „pod maską”?** Aspose tłumaczy każdy wykres Excel na natywny wykres PowerPoint, zachowując serie, tytuły osi i formatowanie. To znacznie lepsze niż eksportowanie wykresu jako statyczny obraz, ponieważ odbiorca może później modyfikować punkty danych.

## Kopiowanie arkusza tabeli przestawnej bez utraty danych

Tabele przestawne są często najtrudniejszą częścią eksportu, ponieważ opierają się na ukrytej pamięci podręcznej. Prosta metoda `Copy` działa, ponieważ Aspose kopiuje zarówno widoczny zakres **jak i** obiekt pamięci podręcznej.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Uwaga:** Jeśli potrzebujesz tabeli przestawnej tylko na nowym arkuszu w tym samym skoroszycie, podejście `sourceRange.Copy` jest lżejsze i unika tworzenia całego nowego skoroszytu.

## Osadzanie czcionek przy eksporcie do PDF – dlaczego to ważne

Gdy otwierasz PDF na komputerze, który nie ma oryginalnych czcionek, tekst może się przemieszczać, zmieniać się podziały wierszy lub znaki mogą znikać. Ustawienie `EmbedStandardFonts = true` mówi Aspose, aby osadził najpopularniejsze czcionki (Arial, Times New Roman itp.) bezpośrednio w strumieniu PDF.

Jeśli używasz własnych czcionek, przełącz na `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Przykład:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Teraz każdy odbiorca zobaczy dokładnie taki sam układ, jaki zaprojektowałeś – bez niespodzianek.

## Podsumowanie pełnego działającego przykładu

Łącząc wszystko razem, kompletny program (pokazany wcześniej) wykonuje następujące kroki:

1. **Tworzy** skoroszyt z miejscami na Smart Marker.  
2. **Przetwarza** znaczniki, generując arkusz szczegółowy nazwany po nazwie działu.  
3. **Kopiuje** zakres zawierający tabelę przestawną do nowego arkusza, zachowując jej funkcjonalność.  
4. **Eksportuje** skoroszyt do PowerPoint, utrzymując wykresy, kształty i pola tekstowe edytowalne.  
5. **Eksportuje** ten sam skoroszyt do PDF, osadzając standardowe czcionki dla niezawodnego renderowania.

Uruchom program, otwórz wygenerowane pliki i zobaczysz:

- **PDF**: Wyraźne tabele, osadzone czcionki i taki sam styl wizualny jak w źródłowym Excelu.  
- **PowerPoint**: Edytowalne wykresy, które możesz kliknąć prawym przyciskiem → *Edit Data* w PowerPoint, oraz kształty, które pozostają w pełni manipulowalne.

---

## Najczęściej zadawane pytania (FAQ)

**P: Czy to działa z .NET Core?**  
Tak – Aspose.Cells i Aspose.Slides są wieloplatformowe. Wystarczy celować w .NET 6 lub nowszy, a ten sam kod działa na Windows, Linux i macOS.

**P: Co zrobić, jeśli potrzebuję wyeksportować tylko wybrane arkusze?**  
Użyj `Workbook.Save` z `SaveOptions`, które pozwalają określić `SheetNames`. Przykład: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**P: Czy mogę zaszyfrować PDF?**  
Oczywiście. Ustaw `PdfSaveOptions.EncryptionDetails` z hasłem przed wywołaniem `Save`.

**P: Moja tabela przestawna korzysta z zewnętrznego źródła danych – czy kopiowanie zerwie połączenie?**  
Operacja kopiowania obejmuje pamięć podręczną, nie zewnętrzne połączenie. Tabela będzie działać offline, ale nie odświeży się względem oryginalnego źródła. Jeśli potrzebujesz aktualizacji na żywo, wyeksportuj dane źródłowe razem ze skoroszytem.

---

## Kolejne kroki i tematy pokrewne

- **Dynamiczne źródła danych** – Dowiedz się, jak podawać JSON lub DataTable do Smart Markers w celu raportowania w czasie rzeczywistym.  
- **Zaawansowane stylowanie PDF** – Zbadaj `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}