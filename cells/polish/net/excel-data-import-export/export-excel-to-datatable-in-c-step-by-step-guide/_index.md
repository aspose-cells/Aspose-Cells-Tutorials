---
category: general
date: 2026-03-25
description: Dowiedz się, jak szybko wyeksportować Excel do DataTable w C#. Ten samouczek
  obejmuje eksport Excela z nazwami kolumn oraz eksport danych z Excela jako ciąg
  znaków dla niezawodnego przetwarzania danych.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: pl
og_description: Eksportuj Excel do DataTable w C# z nazwami kolumn i konwersją na
  ciągi znaków. Skorzystaj z tego zwięzłego poradnika, aby uzyskać gotowe do uruchomienia
  rozwiązanie.
og_title: Eksportuj Excel do DataTable w C# – Kompletny przewodnik
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Eksportuj Excel do DataTable w C# – Przewodnik krok po kroku
url: /pl/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie Excela do DataTable w C# – Przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **export Excel to DataTable**, ale nie byłeś pewien, które flagi włączyć? Nie jesteś sam — wielu programistów napotyka ten sam problem, gdy po raz pierwszy próbują pobrać dane z arkusza kalkulacyjnego do `DataTable`.  

Dobre wieści? W zaledwie kilku linijkach kodu możesz **export Excel with column names** i nawet **export Excel data as string**, aby uniknąć problemów z niezgodnością typów. Poniżej znajdziesz kompletny, działający przykład oraz wyjaśnienie „dlaczego” przy każdym ustawieniu, abyś mógł dostosować go do dowolnego projektu bez zgadywania.

## Co obejmuje ten samouczek

* Jak utworzyć skoroszyt w pamięci (bez fizycznego pliku).  
* Wypełnienie kilkoma przykładowymi wierszami, aby od razu zobaczyć wynik.  
* Konfigurowanie `ExportTableOptions`, aby każda komórka była traktowana jako ciąg znaków.  
* Eksportowanie prostokątnego zakresu do `DataTable` przy zachowaniu pierwszego wiersza jako nagłówków kolumn.  
* Weryfikacja wyniku i wypisanie pierwszego wiersza w konsoli.  

Nie potrzebujesz zewnętrznych linków do dokumentacji — wszystko, czego potrzebujesz, znajduje się tutaj. Jeśli masz już plik Excel na dysku, po prostu zamień linię tworzenia skoroszytu na `new Workbook("path/to/file.xlsx")` i gotowe.

---

## Krok 1: Skonfiguruj projekt i dodaj pakiet NuGet Aspose.Cells

Zanim napiszemy jakikolwiek kod, upewnij się, że Twój projekt odwołuje się do **Aspose.Cells for .NET** (biblioteki obsługującej klasę `Workbook`). Możesz dodać ją za pomocą Menedżera pakietów NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Wskazówka:** Użyj najnowszej stabilnej wersji (stan na marzec 2026, to 22.12), aby uzyskać najnowsze poprawki błędów i ulepszenia wydajności.

---

## Krok 2: Utwórz skoroszyt i wypełnij go przykładowymi danymi

Zaczniemy od zupełnie nowego `Workbook` i zapisujemy kilka wierszy, abyś mógł zobaczyć eksport w działaniu. Ten krok również pokazuje **how to export excel to datatable**, gdy dane źródłowe znajdują się wyłącznie w pamięci.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Dlaczego to ważne:* Wstawiając najpierw wiersz nagłówka (`A1` & `B1`), możemy później nakazać eksporterowi traktowanie pierwszego wiersza jako nazw kolumn — dokładnie to, co oznacza **export excel with column names**.

---

## Krok 3: Powiedz Aspose.Cells, aby traktował każdą komórkę jako ciąg znaków

Podczas eksportu komórek liczbowych lub dat, Aspose próbuje odgadnąć typ .NET. Może to powodować subtelne błędy, jeśli Twój dalszy kod oczekuje ciągów znaków. Flaga `ExportTableOptions.ExportAsString` wymusza jednolitą konwersję do ciągu.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Dlaczego warto to używać?* Wyobraź sobie kolumnę, która czasami zawiera liczby, a czasami tekst (np. „00123” vs. „ABC”). Eksportując wszystko jako ciąg, unikniesz utraty wiodących zer lub wywołania wyjątków konwersji typów.

---

## Krok 4: Eksportuj wybrany zakres do DataTable

Teraz faktycznie **export excel to datatable**. Metoda `ExportDataTable` przyjmuje wiersz/kolumnę początkową, liczbę wierszy/kolumn, flagę określającą wyodrębnianie nazw kolumn oraz opcje, które właśnie skonfigurowaliśmy.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Co się dzieje w tle?*  
- `startRow: 0` wskazuje na pierwszy wiersz Excela (wiersz nagłówka).  
- `exportColumnNames: true` nakazuje Aspose przenieść „Name” i „Age” do kolekcji kolumn `DataTable`.  
- `totalRows`/`totalColumns` mogą być większe niż rzeczywiste dane; nadmiarowe komórki stają się pustymi ciągami dzięki `ExportAsString`.

---

## Krok 5: Zweryfikuj wynik — wypisz pierwszy wiersz

Szybkie wypisanie w konsoli dowodzi, że konwersja się powiodła i że nazwy kolumn są zachowane.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Oczekiwany wynik**

```
First row: Alice, 30
```

Jeśli zmienisz przykładowe dane, konsola automatycznie odzwierciedli te zmiany — nie potrzebny jest dodatkowy kod.

---

## Najczęściej zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę wyeksportować arkusz, który już istnieje na dysku?** | Tak — zamień `new Workbook()` na `new Workbook("myFile.xlsx")`. Reszta kroków pozostaje identyczna. |
| **Co jeśli mój plik Excel zawiera scalone komórki?** | Scalane komórki są rozwijane; wartość lewą‑górną komórki jest używana dla całego zakresu scalonego. |
| **Czy muszę martwić się o formaty liczb zależne od kultury?** | Nie, gdy `ExportAsString = true`; wszystko przychodzi jako surowy ciąg znaków wyświetlany w Excelu. |
| **Ile wierszy mogę wyeksportować jednorazowo?** | Aspose.Cells radzi sobie z milionami wierszy, ale zużycie pamięci rośnie wraz z rozmiarem `DataTable`. Rozważ stronicowanie, jeśli napotkasz limity. |
| **A co z ukrytymi kolumnami?** | Ukryte kolumny są eksportowane, chyba że ustawisz `ExportHiddenColumns = false` w `ExportTableOptions`. |

---

## Bonus: Eksportowanie do CSV zamiast DataTable

Czasami możesz woleć plik płaski. Te same `ExportTableOptions` można ponownie użyć z `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Ten jednowierszowy kod daje gotowy do importu CSV, jednocześnie **exporting excel data as string**.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Uruchom program (`dotnet run`), a zobaczysz wynik **export excel to datatable** wypisany w konsoli. Zamień przykładowe dane, zmień `totalRows`/`totalColumns` lub wskaż skoroszyt na rzeczywisty plik — wszystko skaluje się.

---

## Zakończenie

Masz teraz **kompletne, samodzielne rozwiązanie do eksportowania Excela do DataTable** w C#. Konfigurując `ExportTableOptions.ExportAsString`, zapewniasz **export excel data as string**, a ustawiając `exportColumnNames: true` otrzymujesz znane nagłówki kolumn, które oczekujesz przy **export excel with column names**.  

Od tego momentu możesz:

* Przekazać `DataTable` do Entity Framework lub Dappera w celu masowych wstawień.  
* Przesłać go do silnika raportowego, takiego jak **FastReport** lub **RDLC**.  
* Przekonwertować go na JSON jako odpowiedź API (`JsonConvert.SerializeObject(table)`).

Śmiało eksperymentuj — spróbuj wyeksportować większy arkusz lub połącz to z **how to export excel to datatable** z udziału sieciowego. Wzorzec pozostaje ten sam, a kod jest gotowy do produkcji.

![Diagram przepływu konwersji Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "diagram eksportu excel do datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}