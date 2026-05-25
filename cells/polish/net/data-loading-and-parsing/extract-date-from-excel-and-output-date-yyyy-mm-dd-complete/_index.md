---
category: general
date: 2026-03-18
description: Wyodrębnij datę z Excela i wyświetl ją w formacie ISO yyyy‑mm‑dd. Dowiedz
  się, jak odczytywać japońskie daty z erą, konwertować je i wyświetlać daty ISO w
  C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: pl
og_description: Wyodrębnij datę z Excela i wyświetl ją w formacie ISO yyyy‑mm‑dd.
  Szczegółowy samouczek C# krok po kroku z pełnym kodem i wyjaśnieniami.
og_title: Wyodrębnij datę z Excela – Wyświetl datę w formacie yyyy‑mm‑dd w C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Wyodrębnij datę z Excela i wyświetl ją w formacie rrrr‑mm‑dd – Kompletny przewodnik
  C#
url: /pl/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnij datę z Excela – Jak wyświetlić datę yyyy‑mm‑dd w formacie ISO

Kiedykolwiek potrzebowałeś **extract date from Excel**, ale nie byłeś pewien, jak obsłużyć daty w japońskim systemie ery lub uzyskać czysty ciąg `yyyy‑mm‑dd`? Nie jesteś sam. W wielu projektach migracji danych skoroszyt źródłowy przechowuje daty w kalendarzu japońskiego cesarza, a system docelowy oczekuje daty zgodnej z ISO, takiej jak `2024-04-01`.  

W tym przewodniku przeprowadzimy Cię przez kompletną, działającą wersję rozwiązania, które odczytuje komórkę, interpretuje japońską erę i **outputs the date yyyy‑mm‑dd**. Po zakończeniu będziesz dokładnie wiedział, jak **display date ISO format** w dowolnej aplikacji .NET i będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do własnego projektu.

## Czego będziesz potrzebował

- **.NET 6+** (or .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – biblioteka, która pozwala ustawić niestandardowy kalendarz podczas ładowania skoroszytu.  
- Plik Excel (`japan-date.xlsx`) zawierający datę zapisaną w komórce z japońską erą (np. `令和3年4月1日`).  
- Ulubione IDE – Visual Studio, Rider lub nawet VS Code wystarczy.

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells, a kod działa na Windows, Linux i macOS.

## Krok 1: Skonfiguruj projekt i zainstaluj Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Jeśli pracujesz na serwerze CI, przypnij wersję pakietu (`Aspose.Cells 23.12`), aby zapewnić odtwarzalne kompilacje.

## Krok 2: Załaduj skoroszyt z japońskim kalendarzem cesarskim

Kluczem do **extract date from Excel**, gdy źródło używa nie‑gregoriańskiego kalendarza, jest poinformowanie Aspose.Cells, którego kalendarza użyć podczas ładowania. Robimy to za pomocą `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Why this matters:** Bez niestandardowego kalendarza Aspose.Cells potraktowałby komórkę jako zwykły ciąg znaków i utraciłby informację o erze. Przypisując `JapaneseEmperorCalendar`, biblioteka automatycznie konwertuje `令和3年4月1日` na `2021‑04‑01` w tle.

## Krok 3: Pobierz datę z określonej komórki

Teraz, gdy skoroszyt wie, jak interpretować erę, możemy odczytać komórkę jako `DateTime`. Załóżmy, że data znajduje się w pierwszym arkuszu, komórka **A1** (wiersz 0, kolumna 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Jeśli komórka jest pusta lub zawiera wartość nie‑datową, `GetDateTime()` zgłosi wyjątek. Defensywne podejście wygląda tak:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** Niektóre starsze pliki Excel przechowują daty jako liczby (daty seryjne). Aspose.Cells obsługuje je automatycznie, ale nadal powinieneś zweryfikować typ komórki, jeśli spodziewasz się mieszanej zawartości.

## Krok 4: Wyświetl datę yyyy‑mm‑dd (ISO) i zweryfikuj

Mając `DateTime`, sformatowanie go jako **output date yyyy‑mm‑dd** to jednowierszowy kod:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Uruchomienie programu na pliku zawierającym `令和3年4月1日` wypisze:

```
Extracted date (ISO): 2021-04-01
```

To dokładny **display date iso format**, którego wymaga wiele API.

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny, gotowy do skopiowania program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** Zamień `YOUR_DIRECTORY` na rzeczywisty folder zawierający `japan-date.xlsx`. Kod działa z dowolnym arkuszem i dowolną komórką – wystarczy dostosować indeksy.

## Obsługa innych kalendarzy (opcjonalnie)

Jeśli kiedykolwiek będziesz musiał **extract date from Excel**, który używa tajskiego kalendarza buddyjskiego lub hebrajskiego, po prostu zamień instancję kalendarza:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Reszta logiki pozostaje niezmieniona, co pokazuje elastyczność tego podejścia.

## Częste pułapki i jak ich unikać

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | Komórka nie jest datą (może być ciągiem) | Sprawdź `Cell.Type` przed wywołaniem lub użyj `DateTime.TryParse` na `Cell.StringValue`. |
| Nieprawidłowy rok po konwersji | Skoroszyt został załadowany bez ustawienia `Calendar` | Zawsze twórz `LoadOptions` z odpowiednim kalendarzem **przed** otwarciem pliku. |
| Wyjście ISO pokazuje część czasu (`2021-04-01 00:00:00`) | Użyto `ToString()` bez określenia formatu | Użyj specyfikatora formatu `"yyyy-MM-dd"` aby wymusić **output date yyyy‑mm‑dd**. |
| Plik nie znaleziony | Ścieżka względna wskazuje na niewłaściwy folder | Użyj `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` lub podaj ścieżkę bezwzględną. |

## Pro tipy dla kodu gotowego do produkcji

1. **Cache the workbook** jeśli musisz odczytać wiele dat z tego samego pliku – otwieranie skoroszytu jest stosunkowo kosztowne.  
2. **Wrap the extraction logic** w wielokrotnego użytku metodę:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Log the original era string** (`cell.StringValue`) razem z wyjściem ISO dla ścieżek audytu.  
4. **Unit test** metodę przy użyciu kilku zakodowanych plików Excel obejmujących różne ery (Heisei, Reiwa), aby zapewnić poprawność.

## Wizualny przegląd

Below is a quick diagram illustrating the data flow—from Excel cell to ISO string.  

![Przykład wyodrębniania daty z Excela pokazujący Excel → LoadOptions → DateTime → ciąg ISO]  

*Alt text: „wyodrębnianie daty z Excela” diagram przedstawiający przepływ konwersji.*

## Zakończenie

Omówiliśmy wszystko, co potrzebne do **extract date from Excel**, obsługi wartości japońskich er oraz **output date yyyy‑mm‑dd**, aby spełniał **display date iso format**, którego współczesne API potrzebują. Rozwiązanie jest samodzielne, działa z dowolną wersją .NET obsługującą Aspose.Cells i może być rozszerzone na inne kalendarze jedną zmianą wiersza.

Masz na myśli inny kalendarz? A może pobierasz daty z wielu kolumn? Śmiało modyfikuj pomocniczą metodę `ExtractIsoDate` lub zostaw komentarz poniżej. Szczęśliwego kodowania i niech Twoje daty zawsze będą w doskonałej synchronizacji ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}