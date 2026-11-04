---
category: general
date: 2026-10-01
description: Dowiedz się, jak osadzać czcionki w HTML podczas konwertowania Excela
  do HTML przy użyciu Aspose.Cells. Wyeksportuj Excel jako HTML z osadzonymi czcionkami
  w kilku krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: pl
lastmod: 2026-10-01
og_description: Jak osadzić czcionki w HTML przy eksportowaniu plików Excel. Postępuj
  zgodnie z tym przewodnikiem krok po kroku, aby przekonwertować Excel na HTML z osadzonymi
  czcionkami.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Jak osadzić czcionki w HTML z Excela – przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Jak osadzić czcionki przy konwersji Excela do HTML za pomocą Aspose.Cells
url: /pl/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak osadzić czcionki przy konwertowaniu Excela do HTML przy użyciu Aspose.Cells

Osadzanie czcionek w HTML podczas konwertowania skoroszytu Excel jest niezbędne, aby zachować oryginalny wygląd we wszystkich przeglądarkach. Jeśli potrzebujesz konwertować Excel do HTML, zachowując własne czcionki, ten przewodnik pokazuje kompletny proces. Zobaczysz także, jak wyeksportować Excel jako HTML oraz dlaczego osadzanie czcionek w HTML ma znaczenie dla spójnego renderowania.

Ten tutorial obejmuje wszystko, co musisz wiedzieć: wymagane biblioteki, konfigurację kodu oraz weryfikację wygenerowanego pliku HTML. Po zakończeniu będziesz w stanie wyeksportować Excel jako HTML z osadzonymi czcionkami w zaledwie kilku linijkach C#.

## Czego będziesz potrzebować

Przed rozpoczęciem upewnij się, że masz:

* **.NET 6.0 lub nowszy** – kod jest skierowany do .NET 6, ale każda wersja .NET obsługująca Aspose.Cells będzie działać.
* **Aspose.Cells for .NET** – zdobądź licencję lub użyj darmowej wersji ewaluacyjnej ze strony Aspose.
* Środowisko programistyczne **C#** (Visual Studio, Rider lub VS Code) – dowolne IDE, które potrafi kompilować projekty .NET.
* Skoroszyt Excel (`Styled.xlsx`) wykorzystujący własne czcionki, które chcesz zachować.

## Krok 1: Skonfiguruj Aspose.Cells w swoim projekcie .NET

Najpierw dodaj pakiet NuGet Aspose.Cells do swojego projektu:

```bash
dotnet add package Aspose.Cells
```

Następnie dołącz przestrzeń nazw na początku pliku C#:

```csharp
using Aspose.Cells;
```

Dodanie pakietu udostępnia klasy `Workbook`, `HtmlSaveOptions` oraz powiązane klasy.

## Krok 2: Załaduj skoroszyt Excel

Ładowanie skoroszytu jest pierwszym konkretnym krokiem w **how to export Excel** danych. Konstruktor `Workbook` odczytuje plik z dysku:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Dlaczego to ważne:* Aspose.Cells analizuje skoroszyt, w tym style komórek, formuły i informacje o czcionkach. Jeśli plik nie zostanie znaleziony, zostanie zgłoszony wyjątek, więc upewnij się, że ścieżka jest prawidłowa.

## Krok 3: Skonfiguruj opcje zapisu HTML, aby osadzić czcionki

Sednem **embed fonts in html** jest klasa `HtmlSaveOptions`. Ustaw `EmbedFonts` na `true`, aby każda czcionka użyta w skoroszycie została zapisana w wyjściowym HTML jako reguła `@font-face` zakodowana w Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Dlaczego to ważne:* Domyślnie Aspose.Cells odwołuje się do zewnętrznych plików czcionek, które mogą nie być dostępne na komputerze klienta. Włączenie `EmbedFonts` zapewnia, że renderowany HTML wygląda identycznie jak oryginalny arkusz Excel, niezależnie od zainstalowanych czcionek u odbiorcy.

### Przypadek brzegowy: nieobsługiwane czcionki

Jeśli skoroszyt używa czcionki, która nie jest zainstalowana na serwerze, Aspose.Cells przechodzi na domyślną czcionkę systemową. Aby tego uniknąć, zainstaluj wymagane czcionki na serwerze lub osadź je ręcznie po eksporcie.

## Krok 4: Zapisz skoroszyt jako HTML przy użyciu skonfigurowanych opcji

Teraz możesz zapisać plik HTML. Metoda `Save` przyjmuje ścieżkę wyjściową oraz instancję `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Po wykonaniu, `Styled.html` zawiera dane arkusza oraz blok `<style>` z definicjami `@font-face` zakodowanymi w Base64 dla każdej własnej czcionki.

## Krok 5: Zweryfikuj osadzone czcionki

Otwórz `Styled.html` w przeglądarce. Sprawdź sekcję `<head>`; powinieneś zobaczyć coś podobnego do:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Jeśli czcionki wyświetlają się poprawnie w renderowanej tabeli, osadzanie powiodło się. Jeśli zauważysz brakujące glify, sprawdź ponownie, czy pliki źródłowych czcionek są zainstalowane na maszynie wykonującej konwersję.

## Common variations and additional options

### Converting multiple worksheets

Jeśli potrzebujesz **convert Excel to HTML** dla wszystkich arkuszy, ustaw `ExportActiveWorksheetOnly = false` (wartość domyślna). Aspose.Cells utworzy osobny plik HTML dla każdego arkusza.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Controlling CSS output

Możesz zmniejszyć rozmiar HTML, wyłączając wbudowany CSS:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Using a stream instead of a file

Podczas integracji z API webowym, zapisz HTML do `MemoryStream` i zwróć go bezpośrednio:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro tip: License the product to remove evaluation watermarks

Jeśli używasz wersji ewaluacyjnej, wygenerowany HTML może zawierać komentarz z znakiem wodnym. Zastosuj licencję Aspose.Cells przed załadowaniem skoroszytu, aby uzyskać czysty wynik:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Full working example

Poniżej znajduje się kompletny, uruchamialny program, który demonstruje **how to embed fonts**, **convert excel to html** oraz **export excel as html** w jednym kroku:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Expected output:** Po uruchomieniu programu, `Styled.html` pojawi się w `YOUR_DIRECTORY`. Otwierając plik w dowolnej nowoczesnej przeglądarce, zobaczysz arkusz z takimi samymi czcionkami jak w oryginalnym pliku Excel, nawet na maszynach, które ich nie mają.

## Conclusion

Teraz wiesz, **how to embed fonts** podczas **convert Excel to HTML** przy użyciu Aspose.Cells, i widziałeś pełny przepływ od ładowania skoroszytu po weryfikację osadzonych czcionek. To podejście zapewnia zachowanie wizualnej wierności Twoich plików Excel w wygenerowanym HTML, co jest idealne dla raportowania webowego, newsletterów e‑mailowych lub każdego scenariusza, w którym musisz **export Excel as HTML** z własną typografią.

Następnie odkryj powiązane tematy, takie jak **exporting Excel as PDF**, **styling HTML output with custom CSS**, lub **batch‑processing multiple workbooks**. Wszystkie te zagadnienia opierają się na tym samym wzorcu `HtmlSaveOptions`, więc możesz dostosować kod przy minimalnych zmianach.

Happy coding!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyeksportować Excel do HTML – przewodnik krok po kroku](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Jak osadzić czcionki w HTML – kompletny przewodnik C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [Jak osadzić czcionki przy konwertowaniu Excela do PDF – przewodnik krok po kroku](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}