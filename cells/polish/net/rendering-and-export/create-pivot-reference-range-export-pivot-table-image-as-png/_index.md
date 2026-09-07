---
category: general
date: 2026-02-09
description: Utwórz zakres odniesienia tabeli przestawnej w C# i wyeksportuj obraz
  tabeli przestawnej. Dowiedz się, jak zapisać zakres Excela jako PNG przy użyciu
  Aspose.Cells – szybki, kompletny przewodnik.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: pl
og_description: Utwórz zakres odniesienia tabeli przestawnej w C# i wyeksportuj obraz
  tabeli przestawnej do formatu PNG. Kompletny przewodnik krok po kroku, jak zapisać
  zakres Excela jako PNG.
og_title: Utwórz zakres odniesienia przestawnej – Eksportuj obraz tabeli przestawnej
  jako PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Utwórz zakres odniesienia przestawnego – Eksportuj obraz tabeli przestawnej
  jako PNG
url: /pl/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz zakres odniesienia tabeli przestawnej – wyeksportuj obraz tabeli przestawnej jako PNG

Potrzebujesz **utworzyć zakres odniesienia tabeli przestawnej** w skoroszycie Excel przy użyciu C#? Możesz także **wyeksportować obraz tabeli przestawnej** i **zapisać zakres Excela jako png** w kilku linijkach kodu. Z mojego doświadczenia, przekształcenie żywej tabeli przestawnej w statyczny obraz to wygodny sposób na osadzenie analiz w raportach, e‑mailach lub pulpitach nawigacyjnych bez przenoszenia całego skoroszytu.

W tym samouczku przejdziemy krok po kroku przez wszystko, co musisz wiedzieć: wymagane biblioteki, dokładny kod, dlaczego każde wywołanie ma znaczenie oraz kilka pułapek, na które możesz natrafić. Po zakończeniu będziesz w stanie wygenerować plik PNG dowolnej tabeli przestawnej z pełnym przekonaniem i zrozumiesz, jak dostosować ten schemat do wielu arkuszy lub własnych formatów obrazu.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **Aspose.Cells for .NET** (bezpłatna wersja próbna wystarczy do testów).  
- **.NET 6.0** lub nowszy – używane API jest w pełni kompatybilne z .NET Standard 2.0+, więc starsze frameworki również się skompilują.  
- Podstawowy projekt C# (aplikacja konsolowa, WinForms lub ASP.NET – cokolwiek, co może odwołać się do pakietu NuGet).  

Jeśli nie zainstalowałeś jeszcze Aspose.Cells, uruchom:

```bash
dotnet add package Aspose.Cells
```

To wszystko – bez COM interop, bez zainstalowanego Excela na serwerze.

## Krok 1: Otwórz skoroszyt i uzyskaj dostęp do pierwszego arkusza

Pierwsze, co robisz, to wczytujesz plik skoroszytu i pobierasz arkusz, w którym znajduje się tabela przestawna. Świadomie wybieramy **pierwszy arkusz** (`Worksheets[0]`), ponieważ większość plików demonstracyjnych umieszcza tam pivot, ale możesz zamienić indeks na nazwę, jeśli wolisz.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Dlaczego to ważne:* `Worksheet` jest punktem wejścia dla każdej operacji opartej na zakresie. Jeśli wskażesz niewłaściwy arkusz, kolejne wywołanie `PivotTables[0]` spowoduje `IndexOutOfRangeException`.

## Krok 2: Utwórz zakres odniesienia tabeli przestawnej

Teraz prosimy samą tabelę przestawną o podanie **zakresu odniesienia**. Ten zakres reprezentuje dokładne komórki tworzące pivot – nagłówki, wiersze danych i sumy. Metoda `CreateReferenceRange()` wykonuje całą ciężką pracę wewnętrznie, obsługując scalone komórki i ukryte wiersze.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Jeśli Twój skoroszyt zawiera wiele pivotów, iteruj `worksheet.PivotTables` i wybierz ten, którego potrzebujesz, na podstawie właściwości `Name`.

## Krok 3: Renderuj zakres odniesienia jako obraz

Aspose.Cells może renderować dowolny `Range` do obrazu. Zwracany obiekt obsługuje zarówno formaty rastrowe (PNG, JPEG), jak i wektorowe (SVG). Tutaj prosimy o domyślny obraz rastrowy, czyli obiekt kompatybilny z `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Co się dzieje „pod maską”?* API tworzy migawkę wizualnego układu zakresu, zachowując style komórek, czcionki i formatowanie warunkowe. To w zasadzie to samo, co zrobienie zrzutu ekranu, ale programowo i bez interfejsu UI.

## Krok 4: Zapisz wygenerowany obraz do pliku

Na koniec zapisujemy obraz. Metoda `Save` automatycznie wybiera PNG, gdy podasz rozszerzenie “.png”. Możesz także przekazać obiekt `SaveOptions`, jeśli potrzebujesz kontroli DPI lub innego formatu.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Po wykonaniu tej linii otwórz `pivot.png` i zobaczysz pikselowo‑idealną migawkę tabeli przestawnej, gotową do osadzenia gdziekolwiek.

## Pełny działający przykład

Łącząc wszystko w całość, oto samodzielny program konsolowy, który możesz skopiować i uruchomić:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Oczekiwany wynik:** plik o nazwie `pivot.png` znajdujący się w `YOUR_DIRECTORY`. Otwórz go w dowolnym przeglądarce obrazów – powinieneś zobaczyć dokładny układ oryginalnego pivotu, łącznie z nagłówkami kolumn, wierszami danych i sumami końcowymi.

## Eksport obrazu tabeli przestawnej – dostosowywanie rozmiaru i DPI

Czasami domyślny obraz jest za mały dla slajdu prezentacji. Rozdzielczość możesz kontrolować, przekazując obiekt `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Dlaczego warto zmienić DPI?* Wyższe DPI daje ostrzejsze krawędzie, szczególnie gdy PNG jest skalowany w PowerPointcie lub PDF‑ie.

## Zapisz zakres Excela jako PNG – obsługa wielu arkuszy

Jeśli musisz wyeksportować pivoty z kilku arkuszy, przeiteruj `Workbook.Worksheets` i powtórz kroki. Oto zwięzły fragment:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Ten wzorzec **export pivot table image** dla każdego pivotu w całym skoroszycie, a każdy plik jest nazwany po arkuszu i nazwie pivotu – idealny do przetwarzania wsadowego.

## Typowe pułapki i jak ich uniknąć

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| `IndexOutOfRangeException` przy `PivotTables[0]` | Arkusz nie zawiera tabel przestawnych. | Sprawdź `worksheet.PivotTables.Count` przed dostępem. |
| Pusty obraz | Pivot jest filtrowany tak, że ukrywa wszystkie wiersze. | Upewnij się, że pivot ma widoczne dane lub wywołaj `pivot.RefreshData();` przed tworzeniem zakresu. |
| Niska rozdzielczość PNG | Domyślne DPI to 96. | Użyj `ImageOrVectorSaveOptions.Resolution` jak pokazano wyżej. |
| Błędy ścieżki pliku | Nieprawidłowe znaki w `YOUR_DIRECTORY`. | Użyj `Path.Combine` i `Path.GetInvalidPathChars()` do sanitizacji. |

## Weryfikacja – szybki test

Po uruchomieniu pełnego przykładu:

1. Otwórz `pivot.png` w Windows Photo Viewer.  
2. Zweryfikuj, że nagłówki kolumn, wiersze danych i wiersze sumy zgadzają się z widokiem w Excelu.  
3. Jeśli zauważysz brakujące wiersze, ponownie sprawdź, czy metoda **RefreshData** pivotu została wywołana przed `CreateReferenceRange()`.

## Bonus: Osadzenie PNG w dokumencie Word

Ponieważ obraz jest już w formacie PNG, możesz go od razu przekazać do Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Teraz masz raport Word, który zawiera dokładną migawkę Twojego pivotu – bez ręcznego kopiowania i wklejania.

## Podsumowanie

Właśnie nauczyłeś się, jak **create pivot reference range**, **export pivot table image** i **save Excel range as png** przy użyciu Aspose.Cells w C#. Najważniejsze wnioski:

- Użyj `PivotTable.CreateReferenceRange()` aby wyodrębnić wizualny obszar pivotu.  
- Przekształć ten zakres w obraz za pomocą `Range.ToImage()`.  
- Zapisz obraz jako PNG, opcjonalnie dostosowując DPI dla jakości druku.  

Od tego momentu możesz eksplorować eksport wsadowy, różne formaty obrazu (SVG, JPEG) lub nawet osadzanie PNG w PDF‑ach lub dokumentach Word. Możliwości są nieograniczone, gdy masz pivot zamknięty w statycznej grafice.

Masz pytania lub trudny scenariusz? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}