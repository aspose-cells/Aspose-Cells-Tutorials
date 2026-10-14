---
category: general
date: 2026-03-18
description: Jak wyeksportować dane z Excela do DataTable w C# przy użyciu kodu obsługującego
  konkretne komórki, konwertującego Excel na DataTable i formatującego liczby. Dowiedz
  się, jak eksportować określone komórki i więcej.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: pl
og_description: Jak wyeksportować dane z Excela do DataTable w C#. Ten tutorial pokazuje,
  jak wyeksportować konkretne komórki, przekształcić Excel w DataTable oraz łatwo
  formatować liczby.
og_title: Jak wyeksportować Excel do DataTable w C# – Kompletny przewodnik
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Jak wyeksportować Excel do DataTable w C# – Przewodnik krok po kroku
url: /pl/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować Excel do DataTable w C# – Przewodnik krok po kroku

Zastanawiałeś się kiedyś, **jak wyeksportować dane z Excela** do `DataTable` bez utraty formatowania? Nie jesteś jedyny — programiści stale potrzebują wyciągnąć fragment arkusza do pamięci w celu raportowania, walidacji lub operacji masowego wstawiania. Dobra wiadomość? Kilka linijek C# wystarczy, aby wyeksportować dokładny zakres (np. *A1:F11*), wymusić traktowanie każdej komórki jako ciągu znaków i nawet zastosować własny format liczbowy.

W tym samouczku omówimy wszystko, co musisz wiedzieć: od ładowania skoroszytu, konfiguracji **eksportu konkretnych komórek**, konwersji zakresu do `DataTable`, po obsługę przypadków brzegowych, takich jak puste wiersze czy liczby zależne od lokalizacji. Po zakończeniu będziesz mieć metodę, którą możesz ponownie wykorzystać w scenariuszach **excel to datatable c#** w kodzie produkcyjnym.

> **Wymagania wstępne** – Będziesz potrzebować biblioteki Aspose.Cells for .NET (lub dowolnego podobnego API oferującego `ExportDataTable`). Przykład zakłada .NET 6+, ale koncepcje mają zastosowanie również do wcześniejszych wersji.

---

## Czego się nauczysz

- Jak **przekształcić Excel do DataTable** przy użyciu Aspose.Cells.  
- Eksportowanie własnego zakresu (`excel range to datatable`) przy traktowaniu wszystkich wartości jako ciągów znaków.  
- Zastosowanie formatu liczbowego z dwoma miejscami po przecinku (`#,#00.00`) podczas eksportu.  
- Typowe pułapki (puste wiersze, ukryte kolumny) i sposoby ich unikania.  
- Gotowy do skopiowania, w pełni działający przykład kodu.

---

## Wymagania wstępne i konfiguracja

Zanim przejdziemy do kodu, upewnij się, że masz:

1. **Aspire.Cells for .NET** zainstalowany przez NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Plik Excel (`input.xlsx`) umieszczony w folderze, do którego możesz odwołać się, np. `YOUR_DIRECTORY/input.xlsx`.  
3. Projekt targetujący .NET 6 lub nowszy (pokażone poniżej instrukcje `using` działają od razu).

> **Pro tip:** Jeśli używasz innej biblioteki (np. EPPlus lub ClosedXML), koncepcja pozostaje taka sama — załaduj skoroszyt, wybierz zakres i wywołaj metodę zwracającą `DataTable`.

---

## Krok 1: Załaduj skoroszyt i pobierz pierwszą arkusz

Pierwszą rzeczą, której potrzebujesz, jest obiekt `Workbook` reprezentujący Twój plik Excel. Gdy go masz, możesz uzyskać dostęp do dowolnego arkusza po indeksie lub nazwie.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Dlaczego to ważne:** Wczesne załadowanie skoroszytu pozwala przejrzeć jego strukturę (ukryte arkusze, zabezpieczenia) zanim zdecydujesz, które komórki wyeksportować. Jeśli plik jest duży, rozważ użycie `LoadOptions`, aby strumieniować tylko potrzebne części.

---

## Krok 2: Skonfiguruj opcje eksportu – traktuj wszystkie wartości jako ciągi znaków

Podczas eksportu danych do dalszego przetwarzania (np. masowego wstawiania do SQL) często chcesz mieć **spójną reprezentację tekstową**. To eliminuje późniejsze błędy niezgodności typów.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Wyjaśnienie:**  
- `ExportAsString = true` instruuje Aspose.Cells, aby zignorował natywny typ komórki i zwrócił sformatowany tekst.  
- `NumberFormat = "#,##0.00"` zapewnia, że liczby takie jak `1234.5` staną się `"1,234.50"` — przydatne w raportach finansowych.

Jeśli potrzebujesz oryginalnych typów danych, po prostu ustaw `ExportAsString` na `false` i samodzielnie zajmij się konwersją.

---

## Krok 3: Eksportuj konkretny zakres (A1:F11) do DataTable

Teraz przechodzimy do sedna **eksportu konkretnych komórek**. Metoda `ExportDataTable` przyjmuje indeksy początkowego i końcowego wiersza/kolumny (liczone od zera) oraz flagę określającą, czy uwzględnić nagłówki.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Co otrzymujesz:** `DataTable` z 11 wierszami (wliczając nagłówek) i 6 kolumnami (`A`‑`F`). Wszystkie wartości są ciągami znaków sformatowanymi zgodnie z `exportOptions`.

---

## Krok 4: Zweryfikuj wynik – wypisz na konsolę

Zawsze warto sprawdzić poprawność wyniku przed przekazaniem tabeli innemu komponentowi.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Powinieneś zobaczyć coś w rodzaju:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Zauważ, że kolumny liczbowe wyświetlają dwie cyfry po przecinku, dokładnie tak, jak określiliśmy.

---

## Pełny działający przykład (gotowy do skopiowania)

Poniżej znajduje się kompletny program, który łączy wszystkie elementy. Wstaw go do nowego projektu konsolowego, dostosuj ścieżkę do pliku i uruchom — nie wymaga dodatkowej konfiguracji.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Kluczowe wnioski z kodu:**

- Obiekt `ExportTableOptions` jest wielokrotnego użytku; możesz go przekazać do wielu wywołań `ExportDataTable`, jeśli musisz wyeksportować kilka zakresów.  
- Indeksowanie zaczyna się od **0**, więc `A1` odpowiada `(0,0)`.  
- Ustawienie `includeColumnNames` na `true` automatycznie używa pierwszego wiersza jako nagłówków kolumn — przydatne w dalszych operacjach na `DataTable`.

---

## Obsługa przypadków brzegowych i najczęstsze pytania

### Co zrobić, gdy arkusz ma ukryte wiersze lub kolumny?

Aspose.Cells domyślnie respektuje widoczność. Jeśli potrzebujesz wyeksportować ukryte dane, ustaw `exportOptions.ExportHiddenRows = true` oraz `ExportHiddenColumns = true`.

### Mój plik Excel zawiera formuły — czy otrzymam wyliczone wartości?

Tak. Domyślnie `ExportDataTable` zwraca **wartość wyświetlaną** (rezultat formuły). Jeśli chcesz surowy tekst formuły, ustaw `exportOptions.ExportFormulas = true`.

### Jak pominąć całkowicie puste wiersze?

Po eksporcie możesz oczyścić `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Czy mogę wyeksportować nieciągły zakres (np. A1:B5 i D1:E5)?

Aspose.Cells nie obsługuje rozłącznych zakresów w jednym wywołaniu. Zamiast tego wyeksportuj każdy blok osobno, a następnie ręcznie połącz otrzymane `DataTable`.

---

## Wskazówki dotyczące wydajności

- **Ponownie używaj `ExportTableOptions`** przy wielu eksportach; tworzenie nowej instancji za każdym razem dodaje znikomy narzut, ale zaśmieca kod.  
- **Strumieniuj duże pliki** przy pomocy `LoadOptions`, aby uniknąć ładowania całego skoroszytu do pamięci.  
- **Unikaj `DataTable`**, jeśli potrzebujesz jedynie szybkiego eksportu CSV — `ExportDataTable` jest wygodny, ale nie najefektywniejszy pamięciowo przy ogromnych arkuszach.

---

## Podsumowanie

Przeprowadziliśmy Cię przez **eksport danych z Excela** do `DataTable` z kontrolą formatowania, obsługą konkretnych zakresów komórek i zapewnieniem, że każda wartość trafia jako ciąg znaków. Pełny przykład demonstruje czyste, gotowe do produkcji podejście, które możesz dostosować do **convert excel to datatable**, **export specific cells** lub dowolnego scenariusza **excel range to datatable**, z którym się spotkasz.

Śmiało eksperymentuj: zmień zakres, przełącz `ExportAsString`, lub przekaż `DataTable` bezpośrednio do Entity Framework w celu masowego wstawiania. Nie ma limitów, gdy masz solidne podstawy.

---

### Kolejne kroki i powiązane tematy

- **Importowanie DataTable z powrotem do Excela** – poznaj odwrotną operację przy użyciu `ImportDataTable`.  
- **Masowe wstawianie DataTable do SQL Server** – użyj `SqlBulkCopy` dla błyskawicznego ładowania.  
- **Praca z EPPlus lub ClosedXML** – zobacz, jak to samo zadanie wygląda przy użyciu alternatywnych bibliotek.  
- **Formatowanie komórek przy eksporcie** – zgłęb `ExportTableOptions` pod kątem formatów dat, własnych ustawień kultury i nie tylko.

Masz pytania lub inny przypadek użycia? zostaw komentarz, a rozmowa będzie trwała dalej. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}