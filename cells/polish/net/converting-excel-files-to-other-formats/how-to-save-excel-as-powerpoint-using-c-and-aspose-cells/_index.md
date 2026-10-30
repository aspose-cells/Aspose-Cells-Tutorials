---
category: general
date: 2026-08-17
description: Zapisz Excel jako PowerPoint w C# – krok po kroku przewodnik, jak konwertować
  pliki XLSX, uczynić pola tekstowe edytowalnymi i wygenerować plik PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: pl
lastmod: 2026-08-17
og_description: Zapisz Excel jako PowerPoint w C# z pełnym przykładem kodu. Dowiedz
  się, jak konwertować pliki XLSX, uczynić pola tekstowe edytowalnymi i eksportować
  do PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Zapisz Excel jako PowerPoint w C# – kompletny przewodnik konwersji
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Jak zapisać Excel jako PowerPoint przy użyciu C# i Aspose.Cells
url: /pl/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać Excel jako PowerPoint przy użyciu C# i Aspose.Cells

Jeśli potrzebujesz **zapisać Excel jako PowerPoint** w projekcie .NET, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak wczytać skoroszyt XLSX, uczynić każde pole tekstowe na arkuszu edytowalnym oraz wyeksportować wynik do pliku PPTX — wszystko w kilku linijkach C#.

Konwersja Excela do PowerPointa jest częstym wymogiem przy tworzeniu pulpitów raportowych, zestawów slajdów lub automatycznego generowania prezentacji. Ten tutorial obejmuje także **edytowanie pól tekstowych** programowo, dzięki czemu możesz dostosować zawartość slajdu przed zapisaniem.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 (lub nowszy) SDK zainstalowany  
* Środowisko programistyczne, takie jak Visual Studio 2022 lub VS Code  
* Licencję Aspose.Cells for .NET (lub darmowy klucz ewaluacyjny) – pobierz ze [Aspose website](https://products.aspose.com/cells/net/)  
* Plik `input.xlsx`, który chcesz przekonwertować  

> **Pro tip:** Jeśli używasz wersji ewaluacyjnej, wynikowy plik PPTX będzie zawierał znak wodny. Licencjonowana wersja go usuwa.

## Krok 1: Zainstaluj pakiet NuGet Aspose.Cells

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.Cells
```

Spowoduje to dodanie zestawu `Aspose.Cells`, który udostępnia klasy `Workbook`, `Worksheet` i `Shape` niezbędne do konwersji.

## Krok 2: Utwórz szkielet aplikacji konsolowej

Utwórz nowy projekt konsolowy (jeśli jeszcze go nie masz):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Zastąp wygenerowany plik `Program.cs` kodem pokazanym w kolejnych krokach.

## Krok 3: Wczytaj skoroszyt i wybierz pierwszy arkusz

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Dlaczego to ważne:**  
`Workbook` wczytuje plik Excel do pamięci, natomiast `Worksheet` daje dostęp do komórek, wykresów i kształtów arkusza. Pierwszy arkusz jest zazwyczaj domyślnym raportem, który chcesz przedstawić.

## Krok 4: Uczyń każde pole tekstowe na arkuszu edytowalnym

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Dlaczego tego potrzebujesz:**  
Domyślnie pola tekstowe importowane z Excela są tylko do odczytu po renderowaniu w PowerPointcie. Ustawienie `IsEditable = true` umożliwia (lub późniejszym użytkownikom PowerPointa) modyfikację tekstu bezpośrednio na slajdzie.

## Krok 5: Zapisz skoroszyt jako prezentację PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Co się dzieje w tle:**  
`Workbook.Save` rozpoznaje wartość wyliczenia `SaveFormat.Pptx` i przetwarza układ arkusza Excel — w tym wiersze, kolumny, wykresy oraz teraz edytowalne pola tekstowe — na obiekty slajdów PowerPointa.

## Pełny kod źródłowy (do uruchomienia)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu (`dotnet run`) powinieneś zobaczyć:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Otwarcie pliku `output.pptx` w Microsoft PowerPoint wyświetli slajd odzwierciedlający oryginalny arkusz Excel. Wszystkie pola tekstowe można edytować bezpośrednio, podwójnie klikając je.

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę przekonwertować konkretny arkusz zamiast pierwszego?** | Tak. Zamień `workbook.Worksheets[0]` na `workbook.Worksheets["SheetName"]` lub dowolny potrzebny indeks. |
| **Co jeśli skoroszyt zawiera wiele arkuszy?** | Wywołaj `workbook.Save` osobno dla każdego arkusza, podając odrębne nazwy plików PPTX, lub połącz je w jedną prezentację używając obiektów `Presentation` z Aspose.Slides. |
| **Czy wykresy zostaną zachowane?** | Aspose.Cells automatycznie konwertuje wykresy Excela na obiekty wykresów PowerPointa. Nie wymaga dodatkowego kodu. |
| **Jak zmienić rozmiar slajdu?** | Po `workbook.Save` możesz wczytać wygenerowany PPTX przy pomocy Aspose.Slides i dostosować `Presentation.SlideSize`. |
| **Co jeśli muszę edytować tekst pola przed zapisem?** | Dostęp do `shapeItem.TextBox.Text` wewnątrz pętli, zmodyfikuj go, a następnie ustaw `IsEditable = true`. Przykład: `shapeItem.TextBox.Text = "Nowy tytuł";` |

## Porady dotyczące rozwiązywania problemów

* **„ShapeType.TextBox” nie znaleziono** – Upewnij się, że używasz wersji Aspose.Cells 25.11 lub nowszej; wcześniejsze wersje nie posiadają właściwości `IsEditable`.  
* **Błędy „plik nie znaleziony”** – Sprawdź, czy `YOUR_DIRECTORY` jest ścieżką bezwzględną lub czy ścieżka względna wskazuje właściwe miejsce.  
* **Licencja nie została zastosowana** – Wywołaj `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` przed wczytaniem skoroszytu, aby usunąć znak wodny wersji ewaluacyjnej.

## Zakończenie

Teraz wiesz, jak **zapisać Excel jako PowerPoint** przy użyciu C#, wczytując skoroszyt XLSX, czyniąc każde pole tekstowe edytowalnym i eksportując do PPTX. Metoda ta automatycznie obsługuje wykresy, obrazy i formatowanie komórek, dostarczając gotowy do prezentacji zestaw slajdów.

Następnie eksploruj pokrewne tematy, takie jak **konwersja Excel do PowerPoint przy użyciu Aspose.Slides**, **edytowanie pól tekstowych programowo po konwersji** lub **przetwarzanie wsadowe wielu skoroszytów**. Każdy z nich bazuje na podstawowych krokach opisanych tutaj i może dodatkowo zautomatyzować Twój przepływ pracy raportowej.

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [How to Save Excel Files in Multiple Formats Using Aspose.Cells .NET (2023 Guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}