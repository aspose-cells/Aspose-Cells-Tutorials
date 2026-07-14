---
category: general
date: 2026-07-13
description: Jak wyeksportować zakres komórek jako tabelę przy użyciu C# i ExportTableOptions.
  Poznaj krok po kroku konfigurację skoroszytu, formatowanie i eksport tabeli.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: pl
lastmod: 2026-07-13
og_description: Jak wyeksportować zakres komórek jako tabelę w C# przy użyciu ExportTableOptions.
  Skorzystaj z tego przewodnika, aby sformatować komórki, utworzyć skoroszyt i bez
  wysiłku wyeksportować tabelę.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Jak wyeksportować zakres komórek jako tabelę – pełny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Jak wyeksportować zakres komórek jako tabelę – Kompletny przewodnik C#
url: /pl/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować zakres komórek jako tabelę – Kompletny przewodnik C#

Zastanawiałeś się kiedyś **jak wyeksportować zakres komórek jako tabelę** bez wyrywania sobie włosów z powodu dziwactw formatowania? Nie jesteś jedyny. Niezależnie od tego, czy przekazujesz dane do potoku raportowego, czy po prostu potrzebujesz szybkiego zrzutu w stylu CSV, opanowanie procesu eksportu może zaoszczędzić Ci godziny ręcznego kopiowania‑wklejania.

W tym samouczku przeprowadzimy Cię krok po kroku przez proces pobrania komórki numerycznej, zastosowania notacji naukowej i wyeksportowania jej jako tabeli przy użyciu **ExportTableOptions**. Po zakończeniu będziesz mieć działający fragment kodu, zrozumiesz *dlaczego* każde wywołanie jest potrzebne i będziesz wiedział, jak dostosować kod do większych zakresów lub innych formatów.

## Wymagania wstępne

- .NET 6 lub nowszy (API działa tak samo na .NET Framework 4.7+)
- Aspose.Cells for .NET zainstalowany (`Install-Package Aspose.Cells`)
- Podstawowa znajomość składni C#; nie są potrzebne głębokie informacje o Excelu

Masz to? Świetnie — zanurzmy się.

## Krok 1: Skonfiguruj opcje eksportu – Jak wyeksportować zakres komórek jako tabelę

Pierwszą rzeczą, której potrzebujesz, jest instancja **ExportTableOptions**, która mówi bibliotece, jak traktować zawartość komórek. Bez tego eksport domyślnie używa surowych wartości liczbowych, co może zepsuć downstreamowe aplikacje oczekujące tekstu.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

> **Dlaczego to ważne:**  
> - `ExportAsString = true` wymusza zapis wyświetlanego tekstu komórki, a nie jej wewnętrznej wartości typu double.  
> - `CustomFormat` pozwala narzucić **eksport w notacji naukowej**, przydatny przy bardzo dużych lub bardzo małych liczbach.  
> 
> **Wskazówka:** Jeśli potrzebujesz formatu daty lub waluty, zamień `"0.00E+00"` na `"yyyy‑MM‑dd"` lub `"$#,##0.00"` odpowiednio.

## Krok 2: Utwórz skoroszyt i pobierz pierwszy arkusz – Obsługa skoroszytu i arkusza

**Workbook** reprezentuje cały plik Excel, natomiast **Worksheet** to pojedyncza karta. Dla prostego eksportu pozostaniemy przy pierwszym arkuszu, który zawsze istnieje pod indeksem 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

> **Dlaczego to ważne:**  
> Utworzenie nowego `Workbook` zapewnia czystą bazę — bez ukrytych stylów czy pozostałych danych, które mogłyby Cię zaskoczyć. Dostęp do `Worksheets[0]` jest najszybszym sposobem na uzyskanie uchwytu do aktywnego arkusza bez martwienia się o nazwy kart.

## Krok 3: Wypełnij docelową komórkę – Formatowanie wartości komórki w C#

Teraz wstawiamy wartość numeryczną do komórki **A1** (wiersz 0, kolumna 0). Wybraną wartość celowo podajemy z długim zapisem dziesiętnym, aby można było zobaczyć notację naukową w działaniu.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

> **Dlaczego to ważne:**  
> Wywołanie `PutValue` automatycznie określa typ danych komórki. Ponieważ później eksportujemy jako string, surowy double zostanie przekształcony przy użyciu wcześniej ustawionego formatu, dając schludny wynik `"1.23E+04"`.

## Krok 4: Wyeksportuj określony zakres komórek jako tabelę – Eksportowanie zakresu komórek jako tabeli

Mając już opcje i dane, ostatnim krokiem jest poinstruowanie Aspose.Cells, aby zapisał zakres. Metoda `ExportTable` oczekuje wiersza/kolumny początkowej, rozmiaru zakresu oraz obiektu opcji, który skonstruowaliśmy.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

> **Dlaczego to ważne:**  
> - `totalRows = 1` i `totalColumns = 1` ograniczają eksport do jednej komórki, ale możesz zwiększyć te liczby, aby objąć większe bloki (np. `5, 3` dla zakresu 5 wierszy × 3 kolumn).  
> - Metoda zapisuje dane w wewnętrznej strukturze tabeli, którą można zapisać jako CSV, HTML lub nawet bezpośrednio przesłać do klienta.

### Zapisywanie wyniku (opcjonalnie)

Jeśli chcesz zachować wyeksportowaną tabelę na dysku, możesz zapisać ją do pliku CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Uruchomienie powyższego wygeneruje plik zawierający:

```
1.23E+04
```

## Przypadki brzegowe i typowe wariacje

| Sytuacja | Co zmienić | Powód |
|-----------|----------------|--------|
| **Eksportowanie wielu wierszy** | Dostosuj `totalRows` i w razie potrzeby iteruj po wierszach | Umożliwia eksport wsadowy bez wielokrotnego wywoływania `ExportTable` |
| **Zachowanie formuł** | Ustaw `ExportAsString = false` | Zachowuje oryginalną formułę zamiast wyświetlanej wartości |
| **Różne delimitery** | Użyj przeciążenia `ExportTableToCSV(..., ',', ...)` | Przełącza z wartości oddzielonych przecinkami na wartości oddzielone tabulatorem lub pionową kreską |
| **Duże arkusze** | Strumieniuj eksport, aby uniknąć `OutOfMemoryException` | Działa dobrze przy >10 000 wierszach |

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania i wklejenia program. Kompiluje się w każdym projekcie konsolowym .NET, który odwołuje się do Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

> **Oczekiwany wynik:**  
> Plik o nazwie `ExportedTable.csv` zawierający jedną linię:

```
1.23E+04
```

Jeśli otworzysz CSV w edytorze tekstu, zobaczysz dokładnie zastosowaną notację naukową, taką jak zdefiniowano.

## Zakończenie

Omówiliśmy **jak wyeksportować zakres komórek jako tabelę** od początku do końca: konfigurację `ExportTableOptions`, tworzenie `Workbook`, wstawianie danych i ostateczne wywołanie `ExportTable`. Rozumiejąc każdy element, możesz teraz skalować podejście na większe zakresy, różne formaty lub nawet zintegrować je z API internetowym, które na bieżąco udostępnia dane pochodzące z Excela.

Patrząc w przyszłość, warto przyjrzeć się:

- **ExportTableToHTML** – podglądy gotowe do wyświetlenia w przeglądarce  
- **ExportTableToDataTable** – bezpośrednie wprowadzanie danych do potoków ADO.NET  
- Zaawansowane **custom formats** dla dat, walut lub procentów  

Wypróbuj te możliwości, a zamienisz prosty eksport komórki w wszechstronny silnik dostarczania danych. Masz pytania lub nietypowy przypadek użycia? zostaw komentarz poniżej — miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak wyeksportować widoczne wiersze Excela przy użyciu Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Jak wyeksportować pliki Excel w .NET przy użyciu Aspose.Cells: kompleksowy przewodnik](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Jak uzyskać dostęp do komórki Excela po nazwie przy użyciu Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}