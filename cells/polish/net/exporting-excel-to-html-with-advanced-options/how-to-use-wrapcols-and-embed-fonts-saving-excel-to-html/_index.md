---
category: general
date: 2026-10-20
description: Dowiedz się, jak używać wrapcols w Aspose.Cells, osadzać czcionki w HTML
  oraz zapisywać Excel jako HTML, korzystając z pełnego przykładu w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: pl
lastmod: 2026-10-20
og_description: Jak używać wrapcols w Aspose.Cells, osadzać czcionki w HTML i konwertować
  skoroszyt na HTML w przejrzystym przewodniku C# dla programistów.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Jak używać wrapcols i osadzać czcionki przy eksportowaniu Excela do HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Jak używać wrapcols i osadzać czcionki przy zapisywaniu Excela do HTML
url: /pl/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać wrapcols i osadzać czcionki zapisując Excel jako HTML

Jeśli potrzebujesz **how to use wrapcols** w formule Aspose.Cells, ten przewodnik pokaże Ci dokładne kroki. Dowiesz się także, jak **osadzać czcionki w HTML** i **zapisać Excel jako HTML**, aby wynik wyglądał identycznie we wszystkich przeglądarkach.  

Samouczek obejmuje trzy praktyczne scenariusze: użycie funkcji `WRAPCOLS`, eksportowanie skoroszytu z osadzonymi czcionkami oraz generowanie raportu master‑detail przy użyciu Smart Markers. Po zakończeniu będziesz mieć pojedynczy, uruchamialny program C#, który demonstruje wszystkie te funkcje.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 (lub nowszy) zainstalowany.
* Aspose.Cells for .NET dodany do projektu (`dotnet add package Aspose.Cells`).
* Podstawowa znajomość C# i formuł Excel.

Nie są wymagane dodatkowe biblioteki firm trzecich; Aspose.Cells obsługuje konwersję HTML i osadzanie czcionek wewnętrznie.

## Krok 1: Zademonstruj funkcję **how to use wrapcols** w formule

Funkcja `WRAPCOLS` dzieli jednowymiarowy zakres na dwuwymiarową tablicę, wypełniając najpierw kolumny. Jest to przydatne, gdy trzeba przekształcić dane do raportowania lub tworzenia wykresów.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Dlaczego to działa:**  
`WRAPCOLS` przyjmuje dwa argumenty – zakres źródłowy i liczbę kolumn. Funkcja wypełnia tablicę kolumnowo, odrzucając nadmiarowe wartości (liczbę `3` w przykładzie). Wynik pojawia się w lewym‑górnym komórce docelowego zakresu (`B1`), a zakres można ręcznie rozszerzyć, jeśli potrzebna jest pełna tablica.

> **Wskazówka:** Po ustawieniu formuły wywołaj `workbook.CalculateFormula()`, aby zapewnić, że wynik jest aktualny przed odczytaniem wartości komórek.

## Krok 2: **Konwertuj skoroszyt do HTML** i **osadź czcionki w html**

Podczas eksportowania pliku Excel do HTML czcionki są często zastępowane domyślnymi czcionkami przeglądarki, co może zepsuć układ wizualny. Aspose.Cells umożliwia osadzenie dokładnych czcionek użytych w skoroszycie bezpośrednio w pliku HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Dlaczego osadzanie czcionek ma znaczenie:**  
Gdy `EmbedFonts` jest ustawione na `true`, Aspose.Cells konwertuje każdą używaną czcionkę TrueType/OpenType na regułę `@font-face` zakodowaną w Base64 w wygenerowanym HTML. Eliminuje to konieczność posiadania tych samych czcionek na komputerze klienta, zapewniając renderowanie pixel‑perfect.

> **Przypadek brzegowy:** Jeśli źródłowy skoroszyt odwołuje się do czcionki, która nie jest zainstalowana na serwerze, Aspose.Cells przełączy się na czcionkę domyślną i wyświetli ostrzeżenie. Upewnij się, że wymagane czcionki są dostępne

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak używać WRAPCOLS w C# – Tworzenie skoroszytu Excel z funkcjami Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Jak osadzać czcionki w HTML – Konwertowanie Excela do HTML przy użyciu C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Jak konwertować pliki Excel do HTML przy użyciu Aspose.Cells dla .NET: Ukrywanie nakładającej się zawartości](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}