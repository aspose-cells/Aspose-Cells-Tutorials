---
category: general
date: 2026-02-15
description: Dowiedz się, jak osadzać czcionki podczas eksportowania Excela do SVG
  i XPS, poprawnie zapisywać znaki Unicode oraz osadzać czcionki w SVG przy użyciu
  Aspose.Cells.
draft: false
keywords:
- how to embed fonts
- export excel to svg
- how to write unicode
- embed fonts in svg
- how to export xps
language: pl
og_description: Jak osadzać czcionki przy eksportowaniu Excela do SVG i XPS, zapisywać
  znaki Unicode oraz osadzać czcionki w SVG przy użyciu Aspose.Cells.
og_title: Jak osadzić czcionki w eksportach Excel w C# – krok po kroku
tags:
- Aspose.Cells
- C#
- Excel Export
- Font Embedding
title: Jak osadzić czcionki w eksportach Excel w C# – Kompletny przewodnik
url: /pl/net/working-with-fonts-in-excel/how-to-embed-fonts-in-c-excel-exports-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak osadzać czcionki w eksportach Excel w C# – Kompletny przewodnik

Czy kiedykolwiek zastanawiałeś się **jak osadzać czcionki** w eksporcie Excel, aby wynik wyglądał dokładnie tak samo na każdym komputerze? Nie jesteś jedyny. Gdy wysyłasz arkusz kalkulacyjny do klienta, który nie ma zainstalowanych tych samych krojów pisma, dokument może wyglądać zniekształcony, szczególnie jeśli zawiera specjalne symbole Unicode. W tym samouczku przeprowadzimy praktyczne rozwiązanie, które nie tylko pokazuje **jak osadzać czcionki**, ale także obejmuje **export excel to svg**, **how to write unicode** oraz **how to export xps** przy użyciu Aspose.Cells.  

Pod koniec przewodnika będziesz mieć gotowy do uruchomienia fragment C# zapisujący znak Unicode z selektorem wariacji, osadzający wymagane czcionki i generujący zarówno pliki XPS, jak i SVG, które renderują się perfekcyjnie wszędzie. Bez zewnętrznych narzędzi, bez hacków po‑procesowych — po prostu czysty, samodzielny kod.

## Wymagania wstępne

- .NET 6.0 lub nowszy (API działa tak samo na .NET Framework 4.8)
- Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`)
- Folder na dysku, w którym można zapisywać generowane pliki
- Podstawowa znajomość składni C# (jeśli jesteś zupełnym początkującym, kod jest obszernie skomentowany)

Jeśli masz już te elementy, świetnie — przejdźmy od razu do implementacji.

## Krok 1: Konfiguracja Workbook i Worksheet (Jak osadzać czcionki – punkt wyjścia)

Pierwszą rzeczą, której potrzebujemy, jest nowy obiekt `Workbook`. Traktuj workbook jako kontener wszystkich arkuszy, stylów i zasobów. Utworzenie go jest trywialne, ale stanowi podstawę każdej operacji **embed fonts in svg**, ponieważ informacje o czcionkach znajdują się na poziomie workbook.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // fresh workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet
```

> **Dlaczego to ważne:** Gdy później eksportujesz do SVG lub XPS, Aspose.Cells przegląda kolekcję stylów workbook, aby zdecydować, które czcionki osadzić. Rozpoczęcie od czystego workbook zapewnia, że żadne niechciane odwołania do czcionek nie zanieczyszczają wyniku.

## Krok 2: Zapisz znak Unicode z selektorem wariacji (Jak zapisywać Unicode)

Znaki Unicode mogą być trudne, szczególnie gdy potrzebny jest konkretny wariant glifu. Znak `𝟘` (MATHEMATICAL DOUBLE‑STRUCK ZERO) połączony z selektorem wariacji‑1 (`\uFE00`) zmusza renderer do wybrania „zwykłej” prezentacji. To doskonała demonstracja **how to write unicode**, ponieważ pokazuje dokładny ciąg, który należy umieścić w komórce.

```csharp
            // Step 2: Write the character '𝟘' followed by Variation Selector-1 into cell A1
            // The literal "\uFE00" is the Variation Selector; it tells the font to use the base glyph.
            ws.Cells["A1"].PutValue("𝟘\uFE00");
```

> **Wskazówka:** Jeśli kiedykolwiek zobaczysz w wyniku pusty kwadrat (�), sprawdź dwukrotnie, czy docelowa czcionka rzeczywiście obsługuje podstawowy znak *oraz* selektor wariacji. Nie wszystkie czcionki to robią.

## Krok 3: Eksportuj Worksheet do XPS (Jak eksportować XPS)

XPS to format o stałym układzie, podobny do PDF, ale natywny dla Windows. Eksportowanie do XPS przy **osadzaniu czcionek** gwarantuje, że dokument będzie wyglądał identycznie na każdym komputerze z Windows, nawet jeśli czcionka nie jest zainstalowana lokalnie.

```csharp
            // Step 3: Export the worksheet to XPS – fonts are embedded automatically
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
```

> **Co zobaczysz:** Otwórz wygenerowany `VarSel.xps` w Windows Reader; podwójny zero pojawia się dokładnie tak jak w Excelu, z zachowanym prawidłowym stylem.

## Krok 4: Eksportuj Worksheet do SVG z osadzonymi czcionkami (Embed Fonts in SVG)

SVG to wektorowy format obrazu, który przeglądarki renderują w locie. Domyślnie Aspose.Cells odwołuje się do czcionki po nazwie, co może prowadzić do problemów z brakującymi glifami, jeśli przeglądarka nie ma tej czcionki zainstalowanej. Klasa `SvgSaveOptions` pozwala nam **embed fonts in SVG**, przekształcając plik w samodzielny pakiet.

```csharp
            // Step 4: Export to SVG with fonts embedded
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true          // crucial flag – forces font embedding
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
```

> **Rezultat:** Otwórz `VarSel.svg` w dowolnej nowoczesnej przeglądarce (Chrome, Edge, Firefox). Znak Unicode renderuje się poprawnie bez żadnych zewnętrznych plików czcionek. Jeśli przejrzysz źródło SVG, zobaczysz blok `<style>` zawierający definicję czcionki zakodowaną w Base64.

## Pełny działający przykład (Wszystkie kroki połączone)

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie powyższe kroki oraz końcowy komunikat w konsoli, abyś wiedział, kiedy proces się zakończy.

```csharp
using Aspose.Cells;
using System;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create workbook and worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Write Unicode character with variation selector
            ws.Cells["A1"].PutValue("𝟘\uFE00");

            // Export to XPS (fonts embedded automatically)
            string xpsPath = @"C:\Exports\VarSel.xps";
            ws.Cells.ExportToXps(xpsPath);
            Console.WriteLine($"XPS exported to: {xpsPath}");

            // Export to SVG with embedded fonts
            string svgPath = @"C:\Exports\VarSel.svg";
            SvgSaveOptions svgOptions = new SvgSaveOptions
            {
                EmbedFonts = true
            };
            ws.Cells.ExportToSvg(svgPath, svgOptions);
            Console.WriteLine($"SVG exported to: {svgPath}");

            Console.WriteLine("All files generated successfully.");
        }
    }
}
```

### Oczekiwany wynik

- **`VarSel.xps`** – jednopaginowy dokument XPS pokazujący podwójny zero w dokładnej czcionce użytej w Excelu.
- **`VarSel.svg`** – plik SVG zawierający osadzony strumień czcionki; otwórz go w przeglądarce, a zobaczysz ten sam glif, bez brakujących znaków.

## Częste pułapki i wskazówki (Jak efektywnie osadzać czcionki)

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| Glyph appears as a square in SVG | Font wasn’t embedded (`EmbedFonts = false`) | Set `EmbedFonts = true` in `SvgSaveOptions`. |
| Variation selector is ignored | Font lacks the variant glyph | Choose a font that explicitly supports the variation selector, e.g., **Cambria Math** or **Arial Unicode MS**. |
| Export fails with “Access denied” | Target folder is read‑only or doesn’t exist | Ensure the folder (`C:\Exports\`) exists and the process has write permissions. |
| XPS file size is huge | Embedding large font files unnecessarily | Use a lightweight font (e.g., **Calibri**) if you only need basic Latin characters. |

> **Pro tip:** Jeśli eksportujesz wiele arkuszy, użyj jednej instancji `SvgSaveOptions`, aby uniknąć tworzenia duplikatów strumieni czcionek, co może zwiększyć rozmiar SVG.

## Rozszerzanie rozwiązania (Co jeśli potrzebujesz więcej?)

- **Batch Export:** Przejdź pętlą po `workbook.Worksheets` i wywołaj `ExportToSvg` dla każdego arkusza, podając unikalną nazwę pliku.
- **Custom Font Substitution:** Użyj `Style.Font.Name`, aby wymusić konkretną czcionkę przed eksportem. Jest to przydatne, gdy źródłowy workbook używa czcionki nieprzyjaznej licencyjnie.
- **Higher‑Resolution Images:** Dla formatów rastrowych (PNG, JPEG) możesz ustawić `Resolution` w `ImageOrPrintOptions` — nie jest to potrzebne dla SVG, ale warto wiedzieć, jeśli później zdecydujesz się generować podglądy PNG.

## Zakończenie

Omówiliśmy **jak osadzać czcionki** w eksportach XPS i SVG, zademonstrowaliśmy **jak zapisywać unicode** znaki z selektorami wariacji oraz pokazaliśmy, jak **export excel to svg** przy zachowaniu czcionek wewnątrz pliku. Postępując zgodnie z powyższymi krokami, eliminujesz problem „brakującej czcionki” i zapewniasz, że każdy — niezależnie od zainstalowanych krojów pisma — zobaczy dokładnie to, co zamierzałeś.

Gotowy na kolejne wyzwanie? Spróbuj osadzić własną czcionkę TrueType, która nie jest zainstalowana na serwerze, lub poeksperymentuj z eksportem do PDF przy zachowaniu osadzonych czcionek. Obie ścieżki opierają się na tych samych zasadach, które tutaj omówiliśmy.

Miłego kodowania i niech Twoje eksportowane dokumenty zawsze wyglądają perfekcyjnie!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}