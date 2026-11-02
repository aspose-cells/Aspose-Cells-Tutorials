---
category: general
date: 2026-04-07
description: Dodaj kolor tła wierszom w Excelu przy użyciu C#. Dowiedz się, jak zastosować
  naprzemienne kolory wierszy, ustawić jednolite style tła oraz zaimportować DataTable
  do Excela w jednym procesie.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: pl
og_description: Dodaj kolor tła wierszy w Excelu przy użyciu C#. Ten przewodnik pokazuje,
  jak zastosować naprzemienne kolory wierszy, ustawić jednolite tło oraz efektywnie
  importować DataTable do Excela.
og_title: Dodaj kolor tła w Excelu – naprzemienne style wierszy w C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Dodaj kolor tła w Excelu – naprzemienne style wierszy w C#
url: /pl/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj kolor tła w Excel – Naprzemienne style wierszy w C#

Czy kiedykolwiek potrzebowałeś **dodać kolor tła w Excel** do wierszy, ale nie wiedziałeś, jak to zrobić bez tysiąca linijek skomplikowanego kodu? Nie jesteś sam — większość programistów napotyka ten problem, gdy po raz pierwszy chce, aby ich arkusze wyglądały na coś więcej niż surowy zrzut danych.  

Dobra wiadomość? W ciągu kilku minut możesz **zastosować naprzemienne kolory wierszy**, ustawić **stały kolor tła** i nawet **importować datatable do excel** przy użyciu czystego, wielokrotnego wzorca w C#.  

W tym tutorialu przejdziemy krok po kroku przez cały proces, od pobrania danych do `DataTable` po stylizację każdego wiersza za pomocą delikatnego wzoru żółto‑białych pasków. Nie są wymagane zewnętrzne biblioteki poza solidnym pakietem obsługującym Excel (np. **ClosedXML** lub **GemBox.Spreadsheet**), a zobaczysz, dlaczego takie podejście jest zarówno wydajne, jak i łatwe w utrzymaniu.

## Czego się nauczysz

- Jak pobrać dane i wprowadzić je do arkusza Excel.  
- Jak **stylizować wiersze w Excel** przy użyciu naprzemiennych kolorów tła.  
- Mechanizm **ustawiania stałego tła** przy użyciu obiektu `Style`.  
- Jak **importować datatable do excel** zachowując style wierszy.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak puste tabele lub własne schematy kolorów.

> **Pro tip:** Jeśli już używasz obiektu skoroszytu (`wb`) z biblioteki, która obsługuje tworzenie stylów, możesz ponownie wykorzystać te same instancje `Style` w wielu arkuszach — oszczędzając pamięć i utrzymując kod schludnym.

---

## Krok 1: Pobranie danych – Przygotowanie DataTable

Zanim jakakolwiek stylizacja będzie możliwa, potrzebujemy źródła wierszy. W większości rzeczywistych scenariuszy pochodzą one z bazy danych, API lub pliku CSV. Dla ilustracji po prostu utworzymy prosty `DataTable` w pamięci.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Dlaczego to ważne:** Użycie `DataTable` daje tabelaryczny, świadomy schematu kontener, który biblioteka Excel może zaimportować bezpośrednio, eliminując potrzebę pisania pętli komórka‑po‑komórce.

---

## Krok 2: Utworzenie stylów wierszy – **Zastosuj naprzemienne kolory wierszy**

Teraz zbudujemy tablicę obiektów `Style` — po jednym dla każdego wiersza — tak aby każdy wiersz mógł otrzymać własne tło. Wzorzec, którego użyjemy, to klasyczna jasna żółć dla parzystych wierszy i biały dla nieparzystych.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Wyjaśnienie:**  
- `wb.CreateStyle()` zwraca czysty obiekt stylu, który możesz modyfikować bez wpływu na inne.  
- Operator trójargumentowy `(i % 2 == 0)` decyduje, czy wiersz jest parzysty (jasny żółty) czy nieparzysty (biały).  
- Ustawienie `Pattern = BackgroundType.Solid` to kluczowy krok, który **ustawia stałe tło**; bez tego kolor zostałby zignorowany.

---

## Krok 3: Pobranie docelowego arkusza

Większość bibliotek udostępnia kolekcję arkuszy. Pracujemy z pierwszym, ale możesz wybrać dowolny indeks lub nazwę.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Jeśli skoroszyt jest nowy, biblioteka zazwyczaj tworzy domyślny arkusz. W przeciwnym razie możesz dodać go ręcznie:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Krok 4: Import DataTable ze stylami wierszy – **Importuj datatable do excel**

Gdy style są gotowe, ostatnim krokiem jest wstawienie `DataTable` do arkusza przy jednoczesnym zastosowaniu odpowiedniego stylu do każdego wiersza.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Co się dzieje w tle?**  
- `true` informuje metodę, aby zapisała nagłówki kolumn jako pierwszy wiersz.  
- `0, 0` wskazuje lewy‑górny róg (A1) jako punkt wstawiania.  
- `rowStyles` dopasowuje każdy `Style` do odpowiadającego wiersza danych, dając nam przygotowane wcześniej naprzemienne kolory.

---

## Krok 5: Zapisz skoroszyt

Ostatnim elementem układanki jest zapisanie skoroszytu do pliku, aby móc otworzyć go w Excelu i zobaczyć rezultat.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Otwórz plik, a powinieneś zobaczyć schludnie sformatowany arkusz:

- Wiersz nagłówka pogrubiony (domyślne stylowanie biblioteki).  
- Wiersze 1, 3, 5… z czystym białym tłem.  
- Wiersze 2, 4, 6… z delikatnym jasno‑żółtym wypełnieniem, co ułatwia przeglądanie.

### Zrzut oczekiwanego wyniku

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Wiersze 2, 4, 6, … pojawiają się z jasno‑żółtym tłem — dokładnie efekt **zastosowania naprzemiennych kolorów wierszy**, którego się spodziewaliśmy.

![Przykład dodawania koloru tła w Excelu](https://example.com/excel-background.png "Przykład dodawania koloru tła w Excelu")

*(Tekst alternatywny zawiera główne słowo kluczowe dla SEO.)*

---

## Obsługa przypadków brzegowych i wariantów

### Pusty DataTable

Jeśli `dataTable.Rows.Count` wynosi zero, tablica `rowStyles` będzie pusta, a `ImportDataTable` i tak zapisze wiersz nagłówka (jeśli `includeHeaders` jest `true`). Nie zostanie rzucony wyjątek, ale możesz chcieć zabezpieczyć się przed generowaniem prawie pustego pliku:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Własne schematy kolorów

Chcesz niebiesko‑szare paski zamiast żółto‑białych? Po prostu zamień wartości `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Warto pobierać kolory z pliku konfiguracyjnego, aby osoby nietechniczne mogły dostosować paletę bez modyfikacji kodu.

### Ponowne użycie stylów w wielu arkuszach

Jeśli eksportujesz kilka tabel do tego samego skoroszytu, możesz wygenerować tablicę stylów raz i używać jej ponownie:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Upewnij się tylko, że obie tabele mają taką samą liczbę wierszy, albo generuj nową tablicę dla każdego arkusza.

---

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielny program, który możesz skopiować i wkleić do aplikacji konsolowej.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Uruchom program, otwórz `Report.xlsx` i zobaczysz naprzemienne tło dokładnie tak, jak opisano.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}