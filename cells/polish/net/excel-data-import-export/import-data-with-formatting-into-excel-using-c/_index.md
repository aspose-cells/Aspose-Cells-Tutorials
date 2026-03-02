---
category: general
date: 2026-03-01
description: Importuj dane z formatowaniem do Excela przy użyciu C#. Dowiedz się,
  jak zaimportować DataTable do Excela i dodać kolor tła do komórek w kilku prostych
  krokach.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: pl
og_description: Importuj dane z formatowaniem do Excela przy użyciu C#. Przewodnik
  krok po kroku, który pokazuje, jak zaimportować DataTable i dodać kolor tła do komórek.
og_title: Import danych z formatowaniem do Excela – przewodnik C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importowanie danych z formatowaniem do Excela przy użyciu C#
url: /pl/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Import danych z formatowaniem do Excela przy użyciu C#

Czy kiedykolwiek potrzebowałeś **importować dane z formatowaniem** do skoroszytu Excel, ale otrzymywałeś zwykły, nudny arkusz? Nie jesteś sam. Większość programistów napotyka ten problem, gdy odkrywa, że domyślny import usuwa wszystkie kolory i style, które starannie przygotowali w danych źródłowych.

W tym tutorialu przejdziemy przez kompletną, gotową do uruchomienia rozwiązanie, które **importuje DataTable do Excela** i **dodaje kolor tła do komórek Excela** jednocześnie. Nie wymaga dodatkowego przetwarzania po imporcie — Twój arkusz będzie wyglądał dokładnie tak, jak chcesz, od razu po wygenerowaniu.

## Czego się nauczysz

- Jak pobrać dane do `DataTable`.
- Jak zdefiniować tablicę obiektów `Style`, które zawierają kolory tła.
- Jak wywołać `ImportDataTable` z tymi stylami, aby import zachował formatowanie.
- Pełny, działający przykład, który możesz wkleić do aplikacji konsolowej i od razu zobaczyć wynik.
- Wskazówki, pułapki i warianty dla projektów w rzeczywistym świecie.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+).
- Biblioteka **GemBox.Spreadsheet** (darmowa wersja wystarczy do demonstracji).
- Podstawowa znajomość C# i koncepcji Excela.

Jeśli zastanawiasz się *dlaczego GemBox?* ponieważ oferuje jednowierszową metodę `ImportDataTable`, która przyjmuje tablice stylów — dokładnie tego potrzebujemy, aby **importować dane z formatowaniem** bez pisania pętli.

---

## Krok 1: Skonfiguruj projekt i dodaj GemBox.Spreadsheet

Aby rozpocząć, utwórz nową aplikację konsolową:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Darmowa wersja ogranicza liczbę komórek w arkuszach do 150 k, co jest wystarczające dla demonstracji. Jeśli przekroczysz limit, zaktualizuj wersję lub przejdź na EPPlus, ale API będzie nieco inne.

## Krok 2: Pobierz dane źródłowe jako `DataTable`

Pierwszą rzeczą, której potrzebujemy, jest `DataTable` imitujący dane, które normalnie pobrałbyś z bazy danych. Oto mały pomocnik, który tworzy taką tabelę w pamięci:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Dlaczego to ważne:** Oddzielając pobieranie danych w osobnej metodzie, możesz podmienić dowolne źródło — SQL, CSV, usługę sieciową — bez modyfikacji logiki importu. Dzięki temu kod jest czysty i tutorial **jak importować datatable do excela** jest wielokrotnego użytku.

## Krok 3: Zdefiniuj style, które chcesz zastosować

Teraz przychodzi zabawna część: stworzymy tablicę obiektów `Style`, każdy z odrębnym `ForegroundColor`. GemBox pozwala ustawić `BackgroundPatternColor` (wypełnienie komórki) i `ForegroundColor` (kolor tekstu). W tej demonstracji pokolorujemy pierwsze dwie kolumny inaczej.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explanation:**  
- Obiekty `Style` są lekkimi kontenerami; nie musisz tworzyć nowego dla każdej komórki.  
- Dopasowując kolejność tablicy do kolejności kolumn, GemBox automatycznie stosuje odpowiedni styl podczas importu.  
- To klucz do **importu danych z formatowaniem** — formatowanie podąża za danymi, a nie jest dodawane później.

## Krok 4: Importuj `DataTable` do arkusza z stylami

Mając już dane i style, możemy stworzyć skoroszyt, wybrać pierwszy arkusz i wywołać `ImportDataTable`. Sygnatura metody wygląda tak:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Oto jak jej używamy:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Co dzieje się pod maską?**  
- `true` informuje GemBox, aby zapisał nazwy kolumn w pierwszym wierszu.  
- `0, 0` pozycjonuje import w komórce A1.  
- `importStyles` wiąże każdą kolumnę z kolorami, które zdefiniowaliśmy wcześniej.  

Kiedy otworzysz *Report.xlsx*, zobaczysz, że kolumna **ID** jest podświetlona jasnym niebieskim, kolumna **Name** jasnym zielonym, a kolumna **Score** pozostaje niezmieniona. To **import danych z formatowaniem** w jednym wywołaniu.

## Krok 5: Zweryfikuj wynik (oczekiwany wynik)

Otwórz wygenerowany plik `Report.xlsx`. Powinieneś zobaczyć coś takiego:

| ID (jasny niebieski) | Name (jasny zielony) | Score |
|----------------------|----------------------|-------|
| 1                    | Alice                | 93.5 |
| 2                    | Bob                  | 78.0 |
| 3                    | Charlie              | 85.2 |
| 4                    | Diana                | 91.3 |
| 5                    | Ethan                | 67.8 |

- Komórki w kolumnie **ID** mają tło w jasnym odcieniu niebieskiego.  
- Komórki w kolumnie **Name** mają tło w jasnym odcieniu zielonego.  
- Kolumna **Score** pozostaje z domyślnym białym tłem.

To wizualne wyróżnienie sprawia, że raport jest od razu czytelny — mały detal, który może znacząco poprawić doświadczenie użytkownika.

![Arkusz Excel pokazujący import danych z formatowaniem – kolumna ID w jasnym niebieskim, kolumna Name w jasnym zielonym](excel-screenshot.png "przykład importu danych z formatowaniem")

*Tekst alternatywny obrazu zawiera główne słowo kluczowe pod kątem SEO.*

## Często zadawane pytania i przypadki brzegowe

### Czy mogę zastosować coś więcej niż tylko kolory tła?

Oczywiście. `Style` pozwala ustawić czcionki, obramowania, formaty liczb, a nawet formatowanie warunkowe. Na przykład, aby wyniki powyżej 90 były pogrubione i czerwone:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Co jeśli mój DataTable ma więcej kolumn niż stylów?

GemBox zastosuje style tylko do kolumn, które mają odpowiadający wpis w tablicy. Dodatkowe kolumny użyją domyślnego stylu — nie zostanie zgłoszony błąd.

### Czy to działa z dużymi zestawami danych?

Tak, ale zwróć uwagę na limit darmowej wersji (150 k komórek). Dla bardzo dużych raportów rozważ płatną licencję lub strumieniowe wstawianie danych wiersz po wierszu przy użyciu `worksheet.Cells[row, col].Value = …` — choć stracisz wygodę jednowierszowego rozwiązania.

### Jak zaimportować dane z formatowaniem z istniejącego szablonu Excel?

Możesz najpierw wczytać szablon skoroszytu:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

To pozwala zachować logo nagłówka, stopki i istniejące style, a jednocześnie **importować dane z formatowaniem** dla dynamicznej części.

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Uruchom program (`dotnet run`) i otwórz wygenerowany *Report.xlsx*, aby od razu zobaczyć zastosowane kolory.

## Zakończenie

Masz teraz solidny, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}