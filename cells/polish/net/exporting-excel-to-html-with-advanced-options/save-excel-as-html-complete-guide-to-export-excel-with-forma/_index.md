---
category: general
date: 2026-07-14
description: Szybko zapisz plik Excel jako HTML i dowiedz się, jak konwertować Excel
  na HTML z pełnym formatowaniem. Eksportuj Excel z formatowaniem przy użyciu Aspose.Cells
  w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: pl
lastmod: 2026-07-14
og_description: Zapisz Excel jako HTML natychmiast. Ten przewodnik pokazuje, jak przekonwertować
  Excel na HTML, zachowując style i umożliwiając formatowanie liczb w Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Zapisz Excel jako HTML – Eksport krok po kroku z pełnym formatowaniem
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Zapisz Excel jako HTML – Kompletny przewodnik po eksporcie Excela z formatowaniem
url: /pl/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz Excel jako HTML – Kompletny przewodnik po eksporcie Excela z formatowaniem

Zastanawiałeś się kiedyś, jak **zapisać Excel jako HTML** bez utraty kolorów, obramowań czy formatów liczb? Nie jesteś jedyny. W wielu scenariuszach raportowania potrzebny jest widok skoroszytu gotowy do wyświetlenia w przeglądarce, a najszybszym sposobem jest bezpośredni eksport pliku do HTML.  

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby **przekonwertować Excel na HTML** przy użyciu Aspose.Cells, włączyć formatowanie liczb w Grid.js i upewnić się, że wynik wygląda dokładnie tak jak oryginalny arkusz. Po zakończeniu będziesz mieć gotowy plik HTML, który możesz udostępnić z dowolnego serwera WWW.

## Czego się nauczysz

- Wymagania wstępne i instalacja pakietu  
- Ładowanie istniejącego skoroszytu (lub tworzenie go w locie)  
- Konfigurowanie `HtmlSaveOptions` w celu uzyskania idealnej wierności wizualnej  
- Włączanie `GridJsOptions.EnableNumberFormat`, aby zachować formatowanie liczb  
- Zapisywanie pliku i weryfikacja wyniku  

Jeśli kiedykolwiek próbowałeś **eksportować Excel z formatowaniem** przy użyciu ogólnego zrzutu CSV, wiesz, jak frustrujące może być, gdy liczby zamieniają się w zwykły tekst. Ten przewodnik unika tej pułapki.

---

## Wymagania wstępne – Konfiguracja środowiska programistycznego

Zanim zagłębimy się w kod, upewnij się, że masz:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (the tutorial uses .NET 6) | Nowoczesne API i lepsza wydajność |
| Visual Studio 2022 (or VS Code with C# extension) | Wygodna edycja i debugowanie |
| Aspose.Cells for .NET NuGet package | Biblioteka obsługująca `HtmlSaveOptions` i `GridJsOptions` |
| A sample Excel file (`sample.xlsx`) or a workbook you generate in code | Źródło, które zostanie przekonwertowane |

Zainstaluj Aspose.Cells przy użyciu następującego polecenia w konsoli Package Manager:

```powershell
Install-Package Aspose.Cells
```

> **Pro tip:** Jeśli używasz potoku CI, dodaj tę samą linię `dotnet add package` do swojego skryptu budowania, aby zależność była zawsze dostępna.

---

## Krok 1: Ładowanie lub tworzenie skoroszytu

Możesz albo załadować istniejący plik, albo zbudować go programowo. Oto minimalny przykład, który tworzy skoroszyt z kilkoma sformatowanymi komórkami, abyś mógł zobaczyć, że formatowanie przetrwa eksport.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Dlaczego to ważne:** Ustawiając explicite formaty liczb, później zobaczysz, że `GridJsOptions.EnableNumberFormat` utrzyma te formaty w wyjściowym HTML.

---

## Krok 2: Konfiguracja opcji zapisu HTML

Teraz tworzymy instancję `HtmlSaveOptions`. Ten obiekt mówi Aspose.Cells dokładnie, jak ma być renderowany HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Włączanie formatowania liczb w Grid.js

Jeśli planujesz osadzić HTML na stronie używającej **Grid.js** do interaktywnych tabel, będziesz chciał, aby liczby pozostały sformatowane (np. symbole walut, separatory tysięcy). Poniższa linia robi dokładnie to:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Co się dzieje w tle?** `EnableNumberFormat` wstrzykuje mały fragment JavaScript, który instruuje Grid.js, aby interpretował atrybut `data-format` komórki, zachowując formatowanie w stylu Excel w przeglądarce.

---

## Krok 3: Zapisz skoroszyt jako plik HTML

Gdy skoroszyt jest gotowy, a opcje dopasowane, ostatnia linia zapisuje plik HTML na dysku.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Uruchomienie programu generuje plik `gridjs.html`, który wygląda tak (uproszczony widok):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Otwórz plik w dowolnej przeglądarce, a zobaczysz ładnie wystylowaną tabelę, z jasnoszarym tłem nagłówka i formatowaniem walut. Jeśli umieścisz stronę w serwisie, który już ładuje Grid.js, liczby zostaną automatycznie wyświetlone z odpowiednimi przecinkami i symbolami.

---

## Częste pułapki przy **konwersji Excela do HTML**

| Issue | Why it occurs | How to avoid it |
|-------|---------------|-----------------|
| **Lost formulas** | HTML jest statyczny; formuły zamieniają się w zwykłe wartości. | Jeśli potrzebujesz bieżących obliczeń, przechowuj skoroszyt na serwerze i użyj bibliotek JavaScript, takich jak SheetJS. |
| **Missing images** | Obrazy są przechowywane jako osobne zasoby. | Ustaw `HtmlSaveOptions.ExportImagesAsBase64 = true`, aby osadzić je bezpośrednio. |
| **Huge files** | Duże skoroszyty generują ogromny HTML + JS. | Użyj `ExportOnlyVisibleSheets` lub podziel na wiele stron za pomocą `HtmlSaveOptions.OnePagePerSheet`. |
| **Incorrect number locale** | Excel przechowuje liczby w kulturze neutralnej, przeglądarki mogą stosować ustawienia lokalne. | Jawnie ustaw `htmlOptions.Encoding = Encoding.UTF8` i użyj `GridJsOptions.EnableNumberFormat`. |

---

## Zaawansowane: Eksportowanie wielu arkuszy z indywidualnymi instancjami Grid.js

Jeśli Twój skoroszyt zawiera kilka arkuszy i chcesz, aby każdy stał się własną tabelą Grid.js, możesz przeiterować arkusze i zapisać każdy osobno:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Każdy plik będzie zawierał własny element `<table class="gridjs-table">`, gotowy do niezależnej manipulacji.

---

## Weryfikacja wyniku – szybka lista kontrolna

1. **Czy stylizacja jest zachowana?** Porównaj kolory tła komórek i obramowania z oryginalnym widokiem w Excelu.  
2. **Czy formaty liczb są zachowane?** Sprawdź obecność atrybutu `data-format` w elementach `<td>`.  
3. **Czy obrazy są wyświetlane?** Jeśli wyeksportowałeś obrazy jako Base64, powinny pojawić się w linii.  
4. **Czy konsola przeglądarki jest czysta?** Brak błędów JavaScript związanych z Grid.js.  

Jeśli którykolwiek z tych punktów nie przejdzie, sprawdź ponownie odpowiednią właściwość `HtmlSaveOptions` — większość problemów wynika z brakującej flagi.

---

## Podsumowanie

Masz teraz solidną, gotową do produkcji metodę **zapisywania Excela jako HTML**, zachowującą wszystkie style, obramowania i reprezentacje liczb. Konfigurując `HtmlSaveOptions` i włączając `GridJsOptions.EnableNumberFormat`, przekształciłeś statyczny arkusz kalkulacyjny w przyjazną tabelę internetową, która współpracuje płynnie z Grid.js.

Krótko mówiąc, ten samouczek pokazuje, jak **przekonwertować Excel na HTML** i **eksportować Excel z formatowaniem** przy użyciu Aspose.Cells. Śmiało eksperymentuj: wypróbuj różne motywy, osadź wykresy lub nawet udostępnij HTML przez punkt końcowy ASP.NET do konwersji w locie.

Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź dokumentację Aspose.Cells w celu uzyskania bardziej zaawansowanych opcji konfiguracji. Szczęśliwego kodowania!

---

## Co dalej?

- **Zbadaj inne formaty eksportu**: PDF, PNG lub CSV za pomocą `Workbook.Save`.  
- **Integracja z ASP.NET Core**: Zwróć ciąg HTML bezpośrednio z akcji kontrolera.  
- **Połącz z SheetJS**: Wczytaj wygenerowany HTML z powrotem do skoroszytu JavaScript w celu edycji po stronie klienta.  

---

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyeksportować Excel do HTML z liniami siatki przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Eksportowanie Excela do HTML zachowując style obramowań przy użyciu Aspose.Cells dla Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Konwersja HTML do Excela przy użyciu Aspose.Cells .NET: Kompletny przewodnik](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}