---
category: general
date: 2026-03-22
description: Samouczek niestandardowego formatu liczb w Excelu, pokazujący, jak zaimportować
  tabelę danych do Excela, ustawić kolor tła kolumny, sformatować kolumnę jako walutę
  i zapisać skoroszyt jako xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: pl
og_description: Samouczek Excel o niestandardowym formacie liczb, który krok po kroku
  pokazuje, jak zaimportować DataTable, ustawić kolor tła kolumny, sformatować kolumnę
  jako walutę i zapisać skoroszyt w formacie xlsx.
og_title: Niestandardowy format liczb w Excelu w C# – Przewodnik krok po kroku
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Niestandardowy format liczb w Excelu w C# – Kompletny przewodnik
url: /pl/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowy format liczb w Excel – Pełny samouczek C# 

Zastanawiałeś się kiedyś, jak zastosować **custom number format excel** bezpośrednio z C#? Być może próbowałeś wyeksportować DataTable do arkusza kalkulacyjnego i zobaczyłeś tylko zwykłe liczby, bez kolorów i formatowania walutowego. To powszechny problem — szczególnie gdy potrzebny jest dopracowany raport dla interesariuszy.

W tym przewodniku rozwiążemy ten problem razem: nauczysz się **import datatable to excel**, **set column background color**, **format column as currency**, a na koniec **save workbook as xlsx** z niestandardowym formatem liczb, który sprawi, że Twoje dane będą się wyróżniać. Bez niejasnych odniesień, tylko kompletny, gotowy do uruchomienia kod, który możesz skopiować i wkleić do swojego projektu.

---

## Co zbudujesz

Pod koniec tego samouczka będziesz mieć samodzielną aplikację konsolową C#, która:

1. Pobiera `DataTable` (możesz zamienić szkielet na własne zapytanie).  
2. Tworzy nowy skoroszyt Excel przy użyciu Aspose.Cells (lub dowolnej kompatybilnej biblioteki).  
3. Stosuje niebieską, pogrubioną czcionkę w pierwszej kolumnie, jasno‑żółte tło w drugiej oraz format waluty (`$#,##0.00`) w trzeciej.  
4. Zapisuje plik jako `DataTableWithStyleArray.xlsx` w wybranym folderze.

Zobaczysz dokładnie, jak każda linia przyczynia się do ostatecznego pliku Excel, i omówimy, dlaczego te wybory mają znaczenie dla utrzymania i wydajności.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+).  
- Aspose.Cells for .NET (free trial or licensed version). Install via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Podstawowa znajomość `DataTable` oraz aplikacji konsolowych C#.

## Krok 1: Pobranie danych źródłowych jako DataTable

Najpierw potrzebujemy danych do eksportu. W rzeczywistym scenariuszu prawdopodobnie wywołasz repozytorium lub uruchomisz zapytanie SQL. Dla ilustracji stworzymy prostą tabelę w pamięci.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** Użycie `DataTable` zapewnia tabelaryczne, świadome schematu źródło, które łatwo mapuje się na wiersze i kolumny Excela. Pozwala także ponownie wykorzystać tę samą logikę eksportu dla dowolnego zestawu danych bez przepisywania kodu.

## Krok 2: Utworzenie nowego skoroszytu i pobranie pierwszego arkusza

Teraz uruchamiamy skoroszyt Excel. Klasa `Workbook` reprezentuje cały plik; jej `Worksheets[0]` to domyślny arkusz, w którym umieścimy nasze dane.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Jeśli potrzebujesz wielu arkuszy, po prostu wywołaj `workbook.Worksheets.Add("SheetName")` i powtórz kroki stylizacji dla każdego.

## Krok 3: Definiowanie stylów kolumn – czcionka, tło i format liczbowy

Stylizacja w Aspose.Cells odbywa się za pomocą obiektów `Style`. Zbudujemy tablicę, w której każdy element odpowiada kolumnie w DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** Przekazanie tablicy do `ImportDataTable` pozwala zastosować odrębny styl dla każdej kolumny w jednym wywołaniu, co jest zarówno zwięzłe, jak i wydajne. Gwarantuje to także, że formatowanie pozostaje zsynchronizowane z kolejnością danych.

## Krok 4: Importowanie DataTable przy zastosowaniu stylów

Oto serce operacji: wprowadzamy `DataTable` do arkusza, informujemy Aspose, aby uwzględnił wiersz nagłówka, i przekazujemy naszą tablicę `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose iteruje po każdej kolumnie, zapisuje nagłówek, a następnie zapisuje wartości kolejnych wierszy. Podczas tego procesu stosuje odpowiedni `Style` z tablicy, dzięki czemu otrzymujesz niebieski nagłówek dla „Product”, żółtą kolumnę „Quantity” i ładnie sformatowaną kolumnę „Revenue”.

## Krok 5: Zapisanie skoroszytu jako plik XLSX

Na koniec zapisujemy skoroszyt na dysku. Metoda `Save` automatycznie wybiera format XLSX na podstawie rozszerzenia pliku.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** Jeśli potrzebujesz strumieniować plik (np. dla API webowego), użyj `workbook.Save(stream, SaveFormat.Xlsx)` zamiast ścieżki do pliku.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego. Kompiluje się i działa od razu, generując sformatowany plik Excel.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Oczekiwany wynik

Po otwarciu `DataTableWithStyleArray.xlsx` zobaczysz:

| **Product** (niebieski, pogrubiony) | **Quantity** (jasno‑żółty) | **Revenue** (waluta) |
|--------------------------------------|----------------------------|-----------------------|
| Widget A                             | 120                        | $3,450.75             |
| Widget B                             | 85                         | $2,190.00             |
| Widget C                             | 60                         | $1,580.40             |

**custom number format excel**, który określiłeś (`$#,##0.00`), zapewnia, że każda komórka przychodu wyświetla znak dolara, separator tysięcy i dwie miejsca po przecinku — dokładnie to, czego oczekują zespoły finansowe.

## Najczęściej zadawane pytania i przypadki brzegowe

### Czy mogę używać tego z inną biblioteką Excel?

Oczywiście. Koncepcja — tworzenie stylu dla każdej kolumny i stosowanie go podczas importu — przekłada się na EPPlus, ClosedXML lub NPOI. Wywołania API różnią się, ale wzorzec pozostaje ten sam.

### Co zrobić, gdy mój DataTable ma więcej kolumn niż stylów?

Aspose zastosuje domyślny styl do każdej kolumny, która nie ma odpowiadającego wpisu w tablicy `columnStyles`. Aby uniknąć niespodzianek, dopasuj rozmiar tablicy do `dataTable.Columns.Count` lub generuj style dynamicznie w pętli.

### Jak ustawić niestandardowy format liczbowy dla dat?

Po prostu ustaw `style.Custom = "dd‑mm‑yyyy"` (lub dowolny prawidłowy ciąg formatu Excel). To samo podejście oparte na tablicy działa dla dat, procentów czy notacji naukowej.

### Czy istnieje sposób na automatyczne dopasowanie szerokości kolumn po imporcie?

Tak — wywołaj `worksheet.AutoFitColumns();` po imporcie. Przeprowadza szybkie obliczenie szerokości na podstawie zawartości komórek.

### Co z dużymi zestawami danych (100 tys.+ wierszy)?

`ImportDataTable` jest zoptymalizowany pod kątem operacji zbiorczych, ale możesz napotkać limity pamięci. W takim wypadku rozważ strumieniowe wprowadzanie wierszy ręcznie przy użyciu `Cells[i, j].PutValue(...)` i ponowne użycie jednego obiektu `Style`, aby zmniejszyć narzut.

## Porady profesjonalne i typowe pułapki

- **Unikaj twardego kodowania ścieżek** w kodzie produkcyjnym; używaj `Environment.GetFolderPath` lub ustawień konfiguracyjnych.  
- **Zwolnij zasoby workbooka** jeśli działa w długotrwałej usłudze — otocz go blokiem `using`, aby zwolnić zasoby natywne.  
- **Uważaj na separatory specyficzne dla kultury**. Niestandardowy format `$#,##0.00` wymusza kropkę jako separator dziesiętny niezależnie od ustawień systemu operacyjnego, co zazwyczaj jest pożądane w raportach finansowych.  
- **Pamiętaj o odwołaniu do System.Drawing** (lub `System.Drawing.Common` w .NET Core) dla struktur kolorów używanych w stylizacji.  
- **Testuj wynik na różnych wersjach Excela**; starsze wersje mogą nieco inaczej interpretować niektóre niestandardowe formaty.

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **custom number format excel** pliki z C#: pobieranie danych z `DataTable`, **import datatable to excel**, zastosowanie **set column background color**, użycie **format column as currency**, i w końcu **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}