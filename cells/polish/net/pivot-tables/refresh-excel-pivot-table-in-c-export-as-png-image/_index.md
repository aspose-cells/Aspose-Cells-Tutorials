---
category: general
date: 2026-02-23
description: Odśwież tabelę przestawną Excel w C# i wyeksportuj ją jako obraz PNG.
  Dowiedz się, jak wczytać skoroszyt Excel w C#, odświeżyć tabelę przestawną i zapisać
  wynik.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: pl
og_description: Odśwież tabelę przestawną w Excelu w C# i wyeksportuj ją jako obraz
  PNG. Przewodnik krok po kroku z pełnym kodem i praktycznymi wskazówkami.
og_title: Odśwież tabelę przestawną w Excelu w C# – eksportuj jako obraz PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Odśwież tabelę przestawną Excela w C# – Eksportuj jako obraz PNG
url: /pl/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odśwież tabelę przestawną Excel w C# – Eksport jako obraz PNG

Kiedykolwiek potrzebowałeś **odświeżyć tabelę przestawną Excel** z aplikacji C# i zamienić ją w obraz? Nie jesteś jedynym, który się nad tym zastanawia. W tym samouczku pokażemy dokładnie, jak **odświeżyć tabelę przestawną Excel**, **wczytać skoroszyt Excel w C#**, i w końcu **wyeksportować tabelę przestawną jako obraz** — wszystko w czystym, gotowym do uruchomienia fragmencie kodu.

Na końcu otrzymasz plik PNG, który wygląda dokładnie tak jak tabela przestawna w Excelu, gotowy do osadzenia w raportach, e‑mailach lub pulpitach nawigacyjnych. Bez ręcznego kopiowania, bez skomplikowanego COM interop, po prostu prosty kod .NET.

## Prerequisites

- .NET 6+ (lub .NET Framework 4.7+)
- Aspose.Cells for .NET (wersja próbna lub licencjonowana) – możesz pobrać ją z NuGet za pomocą `Install-Package Aspose.Cells`.
- Istniejący plik `input.xlsx` zawierający przynajmniej jedną tabelę przestawną.
- Folder, w którym masz uprawnienia do zapisu obrazu wyjściowego.

> **Wskazówka:** Jeśli używasz Visual Studio, włącz **nullable reference types** (`<Nullable>enable</Nullable>`), aby wcześnie wykrywać błędy związane z null.

## Krok 1: Wczytaj skoroszyt Excel w C#

Pierwszą rzeczą, której potrzebujemy, jest obiekt `Workbook` wskazujący na nasz plik źródłowy. Traktuj to jak programowe otwarcie pliku Excel.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Dlaczego to ważne:** Wczytanie skoroszytu daje dostęp do arkuszy, komórek i — co najważniejsze — tabel przestawnych, które stworzyłeś. Jeśli plik nie zostanie znaleziony, Aspose zgłasza wyraźny `FileNotFoundException`, który możesz przechwycić, aby zapewnić eleganckie rozwiązanie.

## Krok 2: Skonfiguruj opcje eksportu obrazu (Eksport tabeli przestawnej jako obrazu)

Aspose.Cells pozwala określić, jak tabela przestawna ma być renderowana. Tutaj wybieramy PNG, ponieważ jest bezstratny i szeroko wspierany.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Dlaczego PNG?** W przeciwieństwie do JPEG, PNG zachowuje wyraźne linie siatki i cieniowanie tekstu, na których opierają się tabele przestawne. Jeśli potrzebujesz mniejszego pliku, możesz przełączyć się na `ImageFormat.Jpeg` i dostosować jakość, ale utracisz nieco klarowności.

## Krok 3: Odśwież tabelę przestawną

Zanim przechwycimy wizualizację, musimy upewnić się, że tabela przestawna odzwierciedla najnowsze dane. To jest sedno **odświeżania tabeli przestawnej Excel**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Co się dzieje w tle?** `Refresh()` przelicza tabelę przestawną na podstawie zakresu źródłowego. Jeśli dodałeś wiersze do danych źródłowych po zapisaniu skoroszytu, to wywołanie je pobierze. Pominięcie tego kroku skutkuje przestarzałym obrazem, który nie odpowiada aktualnym danym.

## Krok 4: Renderuj tabelę przestawną do PNG (Eksport obrazu tabeli przestawnej Excel)

Teraz, gdy wszystko jest aktualne, możemy renderować tabelę przestawną bezpośrednio do pliku obrazu.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Rezultat:** Otwórz `pivot.png` i zobaczysz idealny podgląd odświeżonej tabeli przestawnej. Ten plik może być załączony do e‑maila, osadzony na stronie internetowej lub przekazany do silnika raportowania.

### Oczekiwany wynik

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Jeśli przejdziesz do folderu, PNG powinien wyświetlać te same wiersze, kolumny i filtry, które widzisz w Excelu.

## Obsługa typowych przypadków brzegowych

| Sytuacja | Co zrobić |
|-----------|------------|
| **Wiele tabel przestawnych** | Iteruj po `worksheet.PivotTables` i wywołaj `Refresh()` / `RenderToImage()` dla każdej. |
| **Dynamiczne nazwy arkuszy** | Użyj `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` lub wyszukaj po `worksheet.Name`. |
| **Duże zestawy danych** | Ustaw `imgOptions.OnePagePerSheet = false` i określ `imgOptions.PageWidth`/`PageHeight`, aby kontrolować podział na strony. |
| **Brak licencji Aspose.Cells** | Wersja próbna dodaje znak wodny. Uzyskaj licencję i wywołaj `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` przed wczytaniem skoroszytu. |
| **Problemy ze ścieżką pliku** | Użyj `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`, aby uniknąć twardo zakodowanych separatorów. |

## Wskazówki i najlepsze praktyki

- **Poprawne zwalnianie zasobów** – Umieść `Workbook` w bloku `using` lub wywołaj `wb.Dispose()` po zakończeniu, aby zwolnić zasoby natywne.
- **Cache'uj renderowane obrazy** – Jeśli potrzebujesz tego samego obrazu tabeli przestawnej wielokrotnie, zapisz PNG na dysku i używaj go ponownie zamiast renderować za każdym razem.
- **Bezpieczeństwo wątków** – Każdy wątek powinien pracować z własną instancją `Workbook`; obiekty Aspose.Cells nie są bezpieczne wątkowo.
- **Wydajność** – Renderowanie dużych tabel przestawnych może być intensywne pamięciowo. Ustaw `imgOptions.ImageFormat` na `Bmp` dla szybszych, ale większych plików, lub obniż DPI, aby przyspieszyć renderowanie.

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Uruchom program, otwórz `pivot.png` i zobacz odświeżoną tabelę przestawną dokładnie tak, jak wygląda w Excelu.

## Najczęściej zadawane pytania

**Q: Czy to działa z plikami .xlsx utworzonymi w LibreOffice?**  
A: Tak. Aspose.Cells odczytuje format Open XML niezależnie od aplikacji źródłowej, więc możesz **load excel workbook c#** z LibreOffice, eksportu Google Sheets lub dowolnego innego źródła.

**Q: Czy mogę wyeksportować wiele arkuszy jednocześnie?**  
A: Oczywiście. Iteruj po `wb.Worksheets` i zastosuj tę samą logikę `RenderToImage` dla każdego arkusza. Pamiętaj tylko, aby nadać każdemu wynikowi unikalną nazwę pliku.

**Q: Co zrobić, gdy tabela przestawna używa zewnętrznego źródła danych?**  
A: Aspose.Cells może odświeżać zewnętrzne połączenia, jeśli są osadzone w pliku, ale będziesz musiał programowo podać ciąg połączenia i dane uwierzytelniające. Zobacz dokumentację Aspose dotyczącą `DataSourceOptions`.

## Zakończenie

Masz teraz solidne, kompleksowe rozwiązanie do **refresh excel pivot table** z C# oraz **export excel pivot image** jako PNG. Kod pokazuje, jak **load excel workbook c#**, skonfigurować ustawienia obrazu, zapewnić, że tabela przestawna odzwierciedla najnowsze dane i ostatecznie wyrenderować ją do pliku.

Następnie możesz zbadać **export pivot as image** w innych formatach (PDF, SVG) lub zautomatyzować proces dla wielu skoroszytów w zadaniu wsadowym. Chcesz osadzić PNG w raporcie Word? Ta sama klasa `ImageOrPrintOptions` działa z Aspose.Words.

Śmiało eksperymentuj, łam rzeczy i zadawaj pytania w komentarzach — powodzenia w kodowaniu!

![Zrzut ekranu odświeżania tabeli przestawnej Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}