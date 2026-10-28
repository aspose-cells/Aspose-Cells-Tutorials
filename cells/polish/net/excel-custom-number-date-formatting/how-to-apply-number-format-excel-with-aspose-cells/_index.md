---
category: general
date: 2026-10-10
description: Szybko zastosuj formatowanie liczb w Excelu, importując DataTable, ustawiając
  formaty dat i walut oraz zachowując wiersz nagłówka w jednym kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: pl
lastmod: 2026-10-10
og_description: Zastosuj format liczbowy w Excelu w C# przy użyciu Aspose.Cells. Dowiedz
  się, jak ustawić format daty w Excelu, format waluty w Excelu oraz zachować wiersz
  nagłówka w Excelu przy importowaniu DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Zastosuj format liczbowy w Excelu w C# – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Jak zastosować format liczbowy w Excelu z Aspose.Cells
url: /pl/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zastosować format liczbowy w Excelu przy użyciu Aspose.Cells

Jeśli potrzebujesz **zastosować format liczbowy w Excelu** podczas ładowania danych z `DataTable`, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Dowiesz się także, jak **ustawić format daty w Excelu**, **ustawić format waluty w Excelu** oraz **zachować wiersz nagłówka w Excelu** podczas importu, tak aby wynikowy arkusz wyglądał profesjonalnie bez dodatkowego przetwarzania po zakończeniu.

Omówimy wszystko, od instalacji biblioteki po napisanie kompletnego, działającego fragmentu kodu. Po zakończeniu będziesz w stanie zaimportować dowolny `DataTable` do skoroszytu Excel, automatycznie sformatować kolumny liczbowe i zachować wiersz nagłówka – wszystko w kilku linijkach C#.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
* Visual Studio 2022 (lub dowolne IDE C#, które preferujesz)
* **Aspose.Cells for .NET** – zainstaluj przez NuGet:

```bash
dotnet add package Aspose.Cells
```

* Źródło `DataTable` – w przykładzie używana jest metoda pomocnicza `GetTable()`, która zwraca przykładowe dane.

> **Pro tip:** Aspose.Cells jest komercyjną biblioteką, ale oferuje darmowy tryb ewaluacji, który wyłącza znak wodny na okres do 30 dni.

## Krok 1: Utwórz skoroszyt i uzyskaj dostęp do pierwszego arkusza

Obiekt workbook jest punktem wejścia dla wszystkich operacji w Excelu. Tworząc nowy workbook, otrzymujesz domyślny arkusz o indeksie 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Dlaczego ten krok?*  
`Workbook` zarządza formatem pliku, silnikiem obliczeniowym i repozytorium stylów. Wczesny dostęp do `Worksheet` pozwala nam przekazać docelowy arkusz do metody importu później.

## Krok 2: Pobierz dane źródłowe jako DataTable

W rzeczywistych projektach dane często pochodzą z zapytania do bazy danych, parsera CSV lub odpowiedzi API. Dla ilustracji generujemy prosty `DataTable` z trzema kolumnami: **Product**, **Price** i **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Dlaczego ten krok?*  
`DataTable` zapewnia tabelaryczną reprezentację w pamięci, którą Aspose.Cells może importować bezpośrednio, zachowując kolejność kolumn i typy danych.

## Krok 3: Przygotuj tablicę `Style` – jeden styl na kolumnę

Aspose.Cells pozwala zastosować odrębny styl do każdej kolumny podczas importu, przekazując tablicę obiektów `Style`. Długość tablicy musi odpowiadać liczbie kolumn w tabeli źródłowej.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Dlaczego ten krok?*  
Jeśli pominiesz explicite tworzenie (`CreateStyle()`), próba ustawienia `Number` spowoduje `NullReferenceException`. Inicjalizacja każdego `Style` zapewnia, że późniejsze przypisania się powiodą.

## Krok 4: Przypisz formaty liczb – waluta i data

Excel identyfikuje wbudowane formaty liczb po ID.  
* **14** – Waluta (np. `$1,234.00`)  
* **22** – Krótka data (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Uwaga:** Jeśli potrzebujesz własnego formatu (np. `"¥#,##0.00"`), użyj `Style.Custom = "¥#,##0.00"` zamiast wbudowanego ID.

*Dlaczego ten krok?*  
Zastosowanie właściwego **formatu liczbowego** w czasie importu eliminuje potrzebę drugiego przebiegu, w którym trzeba przechodzić po komórkach i zmieniać formatowanie. Gwarantuje to także, że **format excel cells date** i **set currency format excel** są spójne we wszystkich wierszach.

## Krok 5: Importuj DataTable, zachowując wiersz nagłówka

Metoda `ImportDataTable` może kopiować dane, zachować pierwszy wiersz jako nagłówek i zastosować przygotowane style kolumn.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Oczekiwany wynik** – Otwórz `FormattedReport.xlsx` i zobaczysz:

| Produkt | Cena (waluta) | Data wydania (data) |
|---------|----------------|----------------------|
| Widget A| $12.99         | 05/01/2023           |
| Widget B| $23.50         | 06/15/2023           |
| Widget C| $7.75          | 07/30/2023           |

Wiersz nagłówka pozostaje nienaruszony, kolumna **Cena** wyświetla symbol waluty, a kolumna **Data wydania** pokazuje krótki format daty – wszystko bez dodatkowego kodu stylizacji.

### Obsługa typowych przypadków brzegowych

| Sytuacja                                 | Rozwiązanie |
|------------------------------------------|-------------|
| **Więcej kolumn niż stylów**              | Upewnij się, że `columnStyles.Length` równa się `sourceTable.Columns.Count`. Brakujące pozycje przyjmują domyślny styl skoroszytu. |
| **Wartości null w kolumnach liczbowych** | Excel traktuje `null` jako pustą komórkę; format liczbowy nadal obowiązuje, gdy później zostanie wprowadzona wartość. |
| **Waluta specyficzna dla lokalizacji**   | Użyj `columnStyles[i].Custom = "\"€\"#,##0.00"` i ustaw `columnStyles[i].Number = -1`, aby wyłączyć wbudowane ID. |
| **Duże tabele (> 100 000 wierszy)**      | Rozważ użycie przeciążenia `ImportDataTable` z `ImportTableOptions`, aby strumieniować dane i zmniejszyć obciążenie pamięci. |
| **Stosowanie tego samego stylu w wielu kolumnach** | Ponownie użyj tej samej instancji `Style` w tablicy (np. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Użycie własnego ciągu formatowania

Jeśli wbudowane ID nie spełniają Twoich wymagań, możesz zdefiniować własny format liczbowy:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

To podejście daje pełną kontrolę nad **format excel cells date** i **set currency format excel** poza predefiniowanymi ID.

## Podsumowanie

Teraz wiesz, jak **zastosować format liczbowy w Excelu** efektywnie podczas importu `DataTable` przy użyciu Aspose.Cells. Tworząc tablicę `Style` per kolumna, przypisując wbudowane lub własne ID formatów liczbowych oraz używając przeciążenia `ImportDataTable`, które **preserve header row excel**, możesz generować gotowe do publikacji arkusze w jednej operacji.

### Co dalej?

* Eksploruj **set date format excel** z własnymi wzorcami, takimi jak `"dddd, mmmm dd, yyyy"`.
* Połącz tę technikę z **conditional formatting**, aby podświetlać wartości poza zakresem.
* Użyj **format excel cells date** w tabelach przestawnych lub wykresach do dynamicznego raportowania.

Śmiało eksperymentuj z różnymi ID formatów lub własnymi ciągami, aby dopasować je do wytycznych stylu Twojej organizacji. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}