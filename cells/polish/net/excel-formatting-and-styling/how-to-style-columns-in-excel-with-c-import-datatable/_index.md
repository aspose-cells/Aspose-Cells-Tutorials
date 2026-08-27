---
category: general
date: 2026-02-21
description: Dowiedz się, jak stylizować kolumny podczas importowania DataTable do
  Excela przy użyciu C#. Zawiera wskazówki, jak pokolorować drugą kolumnę w Excelu
  oraz importować DataTable do Excela w C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: pl
og_description: Jak stylować kolumny przy importowaniu DataTable do Excela przy użyciu
  C#. Krok po kroku kod, kolorowanie drugiej kolumny w Excelu oraz najlepsze praktyki.
og_title: Jak stylizować kolumny w Excelu przy użyciu C# – Kompletny przewodnik
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Jak stylować kolumny w Excelu przy użyciu C# – Importowanie DataTable
url: /pl/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

**, **Score**) to Polish equivalents: ID stays ID? Could keep ID as ID (common). Name -> Imię, Score -> Wynik. But also the parentheses (red) etc. Should translate. However maybe keep the bold formatting. So we can translate to **ID** (czerwony) etc. Keep bold markers.

Also blockquote > **Prerequisite:** etc. Translate.

Also the "Pro tip:" etc.

Make sure to keep the markdown formatting.

Let's produce the final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stylizować kolumny w Excelu przy użyciu C# – Import DataTable

Zastanawiałeś się kiedyś **jak stylizować kolumny** w arkuszu Excel, pobierając dane bezpośrednio z `DataTable`? Nie jesteś sam. Wielu programistów napotyka problem, gdy potrzebują szybkiego akcentu koloru — na przykład czerwonego dla pierwszej kolumny, niebieskiego dla drugiej — bez ręcznego formatowania każdej komórki po imporcie.  

Dobre wieści? Odpowiedź to kilka linijek kodu C#, a otrzymasz w pełni sformatowany arkusz w momencie, gdy dane zostaną załadowane. W tym samouczku omówimy także **import datatable to excel**, pokażemy **color second column excel**, i wyjaśnimy, dlaczego podejście działa zarówno w projektach .NET Framework, jak i .NET 6+.

---

## Co się nauczysz

- Pobierzesz wypełniony `DataTable` (lub utworzysz go w locie).  
- Zdefiniujesz obiekty `Style` dla poszczególnych kolumn, aby ustawić kolory czcionki.  
- Utworzysz skoroszyt, pobierzesz pierwszy arkusz i zaimportujesz tabelę ze zastosowanymi stylami.  
- Poradzisz sobie z przypadkami brzegowymi, takimi jak puste tabele, niestandardowe wiersze początkowe i dynamiczna liczba kolumn.  

Po zakończeniu będziesz mógł wkleić stylowany plik Excel do dowolnego potoku raportowania — bez konieczności dodatkowego przetwarzania.

> **Wymaganie wstępne:** Podstawowa znajomość C# oraz odwołanie do biblioteki obsługującej `ImportDataTable` (np. Aspose.Cells, GemBox.Spreadsheet lub EPPlus z pomocnikiem). Poniższy kod używa **Aspose.Cells**, ponieważ jego przeciążenie `ImportDataTable` przyjmuje bezpośrednio `Style[]`.

---

## Krok 1: Konfiguracja projektu i dodanie biblioteki Excel

Zanim będziemy mogli cokolwiek stylizować, potrzebujemy projektu, który odwołuje się do biblioteki manipulującej plikami Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Wskazówka:* Jeśli pracujesz w .NET 6, dodaj pakiet poleceniem `dotnet add package Aspose.Cells`. Biblioteka działa na Windows, Linux i macOS, więc jesteś przygotowany na przyszłość.

---

## Krok 2: Pobranie lub zbudowanie źródłowego DataTable

Rdzeń samouczka koncentruje się na stylizacji, ale nadal potrzebujesz `DataTable`. Poniżej znajduje się szybki pomocnik, który tworzy przykładowe dane; w produkcji zamień go na własne wywołanie `GetTable()`.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Dlaczego to ważne:** Użycie `DataTable` sprawia, że źródło danych jest neutralne — niezależnie od tego, czy pochodzi z SQL, CSV, czy kolekcji w pamięci, logika importu pozostaje taka sama. To podstawa **how to import datatable** w sposób efektywny.

---

## Krok 3: Definiowanie stylów kolumn (Serce „How to Style Columns”)

Teraz mówimy arkuszowi, jak ma wyglądać każda kolumna. Klasa `Style` pozwala ustawiać czcionki, kolory, obramowania i wiele więcej. W tym przykładzie zmieniamy jedynie kolor czcionki.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*Co zrobić, jeśli masz więcej kolumn?* Po prostu zwiększ rozmiar tablicy i wypełnij style, które Cię interesują. Kolumny bez stylu automatycznie dziedziczą domyślny styl arkusza.

---

## Krok 4: Utworzenie skoroszytu i import DataTable ze stylami

Mając gotowe dane i style, czas połączyć wszystko w jedną całość.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Co się właśnie stało?**  
- `ImportDataTable` kopiuje wiersze, kolumny i *opcjonalnie* wiersz nagłówka.  
- Przekazując `columnStyles`, każda kolumna otrzymuje wcześniej zdefiniowany `Style`.  
- Wywołanie to jedna linijka, co oznacza, że **import datatable excel c#** jest tak proste.

---

## Krok 5: Weryfikacja wyniku – Oczekiwany rezultat

Otwórz `StyledDataTable.xlsx` w Excelu (lub LibreOffice). Powinieneś zobaczyć:

| **ID** (czerwony) | **Imię** (niebieski) | **Wynik** (domyślny) |
|-------------------|----------------------|----------------------|
| 1                 | Alice                | 92.5                 |
| 2                 | Bob                  | 85.3                 |
| …                 | …                    | …                    |

- Tekst w pierwszej kolumnie jest **czerwony**, spełniając wymóg „how to style columns”.  
- Tekst w drugiej kolumnie jest **niebieski**, co jednocześnie odpowiada zapytaniu **color second column excel**.  

Jeśli plik otworzy się bez błędów, pomyślnie opanowałeś **how to import datatable** przy jednoczesnym stylizowaniu kolumn.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, gdy DataTable jest pusty?
`ImportDataTable` i tak utworzy wiersz nagłówka (jeśli przekazano `true`). Nie zostaną dodane wiersze danych, ale style nadal zostaną zastosowane do komórek nagłówka.

### Potrzeba rozpocząć import w innym miejscu?
Zmień parametry `rowIndex` i `columnIndex` w `ImportDataTable`. Na przykład, aby rozpocząć od `B2`, użyj `1, 1` zamiast `0, 0`.

### Chcę stylizować wiersze zamiast kolumn?
Możesz przejść przez `worksheet.Cells.Rows` po imporcie i przypisać `Style` każdemu wierszowi. Jednak stylizacja na poziomie kolumn jest znacznie wydajniejsza, ponieważ biblioteka stosuje styl raz na kolumnę.

### Używam EPPlus lub ClosedXML?
Te biblioteki nie udostępniają bezpośredniego przeciążenia `ImportDataTable` z tablicą stylów. Obejście polega na najpierw zaimportowaniu tabeli, a następnie iteracji po zakresie kolumn i ustawieniu `Style.Font.Color.SetColor(...)`. Logika pozostaje taka sama, tylko wymaga kilku dodatkowych linii kodu.

---

## Pro tipy do kodu gotowego na produkcję

- **Wykorzystuj ponownie style:** Tworzenie nowego `Style` dla każdej kolumny może być kosztowne. Przechowuj style w słowniku kluczowanym według koloru lub grubości czcionki.  
- **Unikaj sztywno zakodowanych liczb kolumn:** Wykryj `dataTable.Columns.Count` i dynamicznie buduj tablicę `columnStyles`.  
- **Bezpieczeństwo wątkowe:** Jeśli generujesz wiele skoroszytów równocześnie, twórz osobny `Workbook` dla każdego wątku; obiekty Aspose.Cells nie są wątkowo‑bezpieczne.  
- **Wydajność:** Dla tabel większych niż 10 k wierszy rozważ wyłączenie `AutoFitColumns` (przeszukuje każdą komórkę) i ustaw szerokości kolumn ręcznie.

---

## Pełny działający przykład (gotowy do skopiowania)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Uruchom program, otwórz wygenerowany `StyledDataTable.xlsx` i od razu zobaczysz pokolorowane kolumny. To całość **import datatable excel c#** w kilku linijkach.

---

## Zakończenie

Właśnie omówiliśmy **how to style columns** podczas **import datatable to excel** przy użyciu C#. Definiując tablicę `Style[]` i przekazując ją do `ImportDataTable`, możesz pokolorować pierwszą kolumnę na czerwono, drugą na niebiesko, a pozostałe pozostawić bez zmian — wszystko w jednej linijce kodu.  

Podejście skaluje się: dodaj kolejne obiekty `Style` dla dodatkowych kolumn, dostosuj wiersze początkowe lub zamień Aspose.Cells na inną bibliotekę o podobnym API. Teraz możesz generować eleganckie raporty Excel bez ręcznej edycji pliku.

**Kolejne kroki**, które możesz rozważyć:

- Skorzystaj z **formatowania warunkowego**, aby dynamicznie podświetlać wartości (wiąże się z „color second column excel”).  
- Eksportuj wiele arkuszy z jednego zestawu `DataTable` (idealne dla miesięcznych pulpitów).  
- Połącz to z **CSV → DataTable** konwersją, aby zbudować kompletny proces od…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}