---
category: general
date: 2026-02-26
description: Szybko zastosuj format liczbowy w Excelu i dowiedz się, jak sformatować
  kolumnę jako walutę, ustawić format liczbowy kolumny oraz kolor czcionki kolumny
  w zaledwie kilku linijkach C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: pl
og_description: Zastosuj format liczbowy w Excelu w C# w prostych krokach. Dowiedz
  się, jak sformatować kolumnę jako walutę, ustawić format liczbowy kolumny oraz zmienić
  kolor czcionki kolumny, aby uzyskać profesjonalne arkusze kalkulacyjne.
og_title: Zastosuj format liczbowy w Excelu – Kompletny przewodnik po stylizacji kolumn
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Zastosuj format liczbowy w Excelu – Przewodnik krok po kroku po formatowaniu
  kolumn
url: /pl/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Jak stylować kolumny Excela w C#

Zastanawiałeś się kiedyś, jak **apply number format excel** podczas iteracji po `DataTable`? Nie jesteś jedyny. Większość programistów napotyka problem, gdy potrzebują nagłówka z niebieską czcionką *oraz* kolumny sformatowanej jako waluta w tej samej operacji importu. Dobre wieści? Dzięki kilku liniom C# i odpowiednim obiektom stylu, możesz to zrobić bez dodatkowego przetwarzania arkusza.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **format column as currency**, **set column number format** dla dowolnej innej kolumny oraz **set column font color** dla nagłówków. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec, który możesz wstawić do dowolnego projektu Aspose.Cells (lub podobnego).

## Czego się nauczysz

- Jak pobrać `DataTable` i przypisać każdą kolumnę do konkretnego `Style`.
- Dokładne kroki do **apply number format excel** przy użyciu `Worksheet.Cells.ImportDataTable`.
- Dlaczego tworzenie stylów z góry jest bardziej wydajne niż formatowanie komórek pojedynczo.
- Obsługa przypadków brzegowych, gdy tabela źródłowa ma więcej kolumn niż stylizowano.
- Pełny, gotowy do kopiowania i wklejania fragment kodu, który możesz uruchomić już dziś.

**Prerequisite:** Ten przewodnik zakłada, że masz w projekcie odwołanie do Aspose.Cells for .NET (lub dowolnej biblioteki udostępniającej API `Workbook`, `Worksheet`, `Style`). Jeśli używasz innej biblioteki, koncepcje przekładają się bezpośrednio — po prostu zamień nazwy typów.

---

## Krok 1: Pobranie danych źródłowych jako DataTable

Zanim można zastosować jakikolwiek styl, potrzebujesz surowych danych. W większości rzeczywistych scenariuszy dane znajdują się w bazie danych, pliku CSV lub API. Dla przejrzystości zasymulujemy prosty `DataTable` z dwiema kolumnami: *Product* (string) i *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

**Why this matters:** Pobranie danych do `DataTable` daje Ci tabelaryczną, pamięciową reprezentację, którą `ImportDataTable` może bezpośrednio wykorzystać, eliminując potrzebę ręcznego wstawiania komórek pojedynczo.

## Krok 2: Utworzenie tablicy stylów – po jednym dla każdej kolumny

Przeciążenie `ImportDataTable`, którego użyjemy, przyjmuje tablicę obiektów `Style`. Każdy element odpowiada indeksowi kolumny. Jeśli pozostawisz element jako `null`, kolumna odziedziczy domyślny styl skoroszytu.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

**Pro tip:** Deklarowanie tablicy *po* uzyskaniu `DataTable` zapewnia, że rozmiar jest dokładnie dopasowany, zapobiegając późniejszemu `IndexOutOfRangeException`.

## Krok 3: Ustawienie koloru czcionki kolumny (niebieski) dla pierwszej kolumny

Częstym żądaniem jest podświetlenie nagłówka lub kluczowych kolumn odrębnym kolorem czcionki. Tutaj ustawiamy niebieski kolor tekstu pierwszej kolumny.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

**Why use a style object?** Style są wielokrotnego użytku i stosowane zbiorczo, co jest znacznie szybsze niż iterowanie po każdej komórce po imporcie. Skoroszyt buforuje styl raz, a potem używa go dla każdej komórki w tej kolumnie.

## Krok 4: Sformatowanie drugiej kolumny jako waluta

Wbudowane formaty liczb w Excelu są identyfikowane przez indeks. `14` odpowiada domyślnemu formatowi waluty (np. `$1,234.00`). Jeśli potrzebujesz własnego formatu, możesz zamiast tego przypisać ciąg formatowania.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

**Edge case:** Jeśli Twój skoroszyt używa ustawień regionalnych, w których symbol waluty nie jest `$`, ten sam indeks dostosuje się automatycznie (np. `€` dla niemieckich ustawień regionalnych).

## Krok 5: Importowanie DataTable z zdefiniowanymi stylami

Teraz łączymy wszystko. Metoda `ImportDataTable` wklei dane zaczynając od komórki `A1` (wiersz 0, kolumna 0) i zastosuje przygotowane style.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Drugi parametr `true` informuje Aspose.Cells, że pierwszy wiersz `DataTable` należy traktować jako nagłówki kolumn.
- Współrzędne `0, 0` określają lewy górny róg, od którego rozpoczyna się import.
- `columnStyles` mapuje każdą kolumnę do jej odpowiedniego stylu.

## Krok 6: Zapisanie skoroszytu (opcjonalnie, ale przydatne do weryfikacji)

Jeśli chcesz zobaczyć wynik w Excelu, po prostu zapisz skoroszyt na dysku. Ten krok nie jest wymagany dla logiki stylizacji, ale jest przydatny przy debugowaniu.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Oczekiwany wynik

| **Product** (niebieska czcionka) | **Price** (waluta) |
|--------------------------|----------------------|
| Apple                    | $1.25                |
| Banana                   | $0.75                |
| Cherry                   | $2.10                |

- Kolumna *Product* wyświetlana jest na niebiesko, co wyróżnia ją.
- Kolumna *Price* pokazuje wartości z domyślnym symbolem waluty i dwoma miejscami po przecinku.

---

## Najczęściej zadawane pytania i warianty

### Jak **set column number format** dla więcej niż dwóch kolumn?

Po prostu rozszerz tablicę `columnStyles`. Na przykład, aby wyświetlić procent w trzeciej kolumnie:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Co zrobić, jeśli potrzebny jest *custom* format waluty, np. „USD 1,234.00”?

Zastąp właściwość `Number` ciągiem formatowania:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Czy mogę zastosować **set column font color** do kolumny numerycznej bez wpływu na jej format liczbowy?

Oczywiście. Style są kompozycyjne. Możesz ustawić zarówno `Font.Color`, jak i `Number` w tej samej instancji `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Co się stanie, jeśli `DataTable` ma więcej kolumn niż stylów?

Każda kolumna bez wyraźnie określonego stylu (`null` entry) odziedziczy domyślny styl skoroszytu. Aby uniknąć przypadkowych `null`, możesz najpierw zainicjalizować całą tablicę bazowym stylem:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Następnie nadpisz tylko te kolumny, które Cię interesują.

### Czy to podejście działa przy dużych zestawach danych (10 tys.+ wierszy)?

Tak. Ponieważ stylizacja jest stosowana *raz na kolumnę* przed importem, operacja pozostaje O(N) względem liczby wierszy, a zużycie pamięci pozostaje niskie. Unikaj iteracji po każdej komórce po imporcie — to właśnie tam wydajność spada.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Uruchom program, otwórz `StyledReport.xlsx`, a zobaczysz wynik **apply number format excel** natychmiast.

## Zakończenie

Właśnie pokazaliśmy czysty, wydajny sposób na **apply number format excel** do zaimportowanego `DataTable`. Przygotowując z góry tablicę `Style[]`, możesz **format column as currency**, **set column number format** i **set column font color** w jednym wywołaniu — bez potrzeby dodatkowego przetwarzania.  

Śmiało rozbudowuj wzorzec: dodawaj formatowanie warunkowe, scalaj komórki w nagłówkach lub nawet wstawiaj formuły. Te same zasady obowiązują, utrzymując kod schludnym, a arkusze wyglądają profesjonalnie.

### Co dalej?

- Zbadaj **conditional formatting**, aby podświetlić wartości przekraczające określony próg.
- Połącz tę technikę z **pivot table generation** dla dynamicznego raportowania.
- Spróbuj **setting column number format** dla dat, procentów lub własnej notacji naukowej.

Masz własny pomysł, który wypróbowałeś? Podziel się nim w komentarzach — utrzymujmy the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}