---
category: general
date: 2026-03-30
description: Utwórz skoroszyt Excel w C# z formatowaniem walutowym. Dowiedz się, jak
  zaimportować DataTable, dodać format liczbowy w Excelu i zastosować format waluty
  w kolumnie w kilka minut.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: pl
og_description: Utwórz skoroszyt Excel w C# i natychmiast sformatuj komórki jako walutę.
  Ten krok po kroku poradnik pokazuje, jak zaimportować DataTable do Excela i dodać
  format liczbowy w Excelu dla kolumny.
og_title: Tworzenie skoroszytu Excel w C# – Przewodnik formatowania walut
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz skoroszyt Excel w C# – zastosuj format waluty i zaimportuj DataTable
url: /pl/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel C# – Zastosowanie formatu walutowego i importowanie DataTable

Kiedykolwiek potrzebowałeś **create Excel workbook C#**, który od razu wygląda jak dopracowany raport? Może pobierasz liczby sprzedaży z bazy danych i chcesz, aby kolumna z ceną wyświetlała się w dolarach bez ręcznego formatowania w Excelu. Brzmi znajomo? Nie jesteś sam — większość programistów napotyka ten problem, gdy po raz pierwszy automatyzuje eksport do Excela.

W tym przewodniku przejdziemy krok po kroku przez kompletną, gotową do uruchomienia rozwiązanie, które **creates an Excel workbook C#**, importuje `DataTable` i **formats the Price column as currency**. Na koniec otrzymasz plik o nazwie `StyledTable.xlsx`, który otworzysz i zobaczysz ładnie sformatowane liczby. Bez dodatkowego przetwarzania po fakcie.

> **What you’ll learn**
> - Jak skonfigurować Aspose.Cells w projekcie .NET  
> - Jak **import datatable to excel** przy użyciu tablicy stylów  
> - Jak **add number format excel** dla konkretnej kolumny  
> - Wskazówki dotyczące obsługi większej liczby kolumn lub różnych locale  

> **Prerequisites**  
> - .NET 6+ (lub .NET Framework 4.6+) zainstalowany  
> - Pakiet NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
> - Podstawowa znajomość C# i DataTables  

---

## Krok 1: Przygotowanie DataTable (import datatable to excel)

Najpierw potrzebujemy przykładowych danych. W rzeczywistej aplikacji prawdopodobnie wypełnisz tę tabelę wynikiem zapytania do bazy, ale przykładowy, na sztywno zapisany zestaw ułatwia zrozumienie.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Dlaczego to ważne*: `DataTable` jest mostem między danymi biznesowymi a plikiem Excel. Aspose.Cells może go zaimportować bezpośrednio, zachowując nazwy kolumn i typy danych.

---

## Krok 2: Utworzenie nowego skoroszytu (create excel workbook c#)

Teraz tworzymy rzeczywisty obiekt pliku Excel. Pomyśl o nim jak o czystym płótnie, na którym będziesz malować.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Jeśli potrzebujesz wielu arkuszy, wywołaj `workbook.Worksheets.Add()` i nadaj każdemu znaczącą nazwę.

---

## Krok 3: Definicja stylu walutowego (format cells currency)

Aspose.Cells pozwala stworzyć obiekt `Style`, który opisuje, jak mają wyglądać komórki. Dla waluty używamy wbudowanego formatu liczbowego ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Dlaczego nie ustawić po prostu ciągu formatowania?* Użycie wbudowanego ID zapewnia kompatybilność między wersjami Excela i unika specyficznych dla locale problemów.

---

## Krok 4: Zbudowanie tablicy stylów (apply currency format column)

Podczas importowania `DataTable` możesz przekazać tablicę obiektów `Style` — po jednej na kolumnę. `null` oznacza „użyj domyślnego stylu”. Tutaj stosujemy `priceStyle` tylko do drugiej kolumny.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Jeśli później dodasz więcej kolumn, po prostu rozszerz tablicę. Długość `columnStyles` musi odpowiadać liczbie importowanych kolumn, w przeciwnym razie Aspose zgłosi wyjątek.

---

## Krok 5: Import DataTable ze stylami (import datatable to excel)

Teraz dzieje się magia — nasz `DataTable` trafia do arkusza, a kolumna cen natychmiast wyświetla się jako waluta.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Co jeśli masz więcej niż dwie kolumny?* Rozszerz `columnStyles`, aby każda kolumna otrzymała odpowiedni styl (lub `null` dla domyślnego). To najczystszy sposób na **add number format excel** selektywnie.

---

## Krok 6: Zapis skoroszytu (create excel workbook c#)

Na koniec zapisujemy plik na dysku. Wybierz dowolny folder, do którego masz prawo zapisu.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Otwórz `StyledTable.xlsx` w Excelu i powinieneś zobaczyć:

| Produkt | Cena |
|---------|------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Kolumna **Cena** jest już sformatowana jako waluta — nie są potrzebne żadne dodatkowe kroki.

---

## Przypadki brzegowe i warianty

### Więcej kolumn, różne formaty

Jeśli musisz **format cells currency** dla kilku kolumn (np. Koszt, Podatek, Łącznie), utwórz osobny `Style` dla każdej i wypełnij `columnStyles` odpowiednio:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Waluta specyficzna dla locale

Dla euro lub funta brytyjskiego użyj innych wbudowanych ID (np. 165 dla `€#,##0.00`). Alternatywnie ustaw własny ciąg formatowania:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Duże zestawy danych

Aspose.Cells radzi sobie z milionami wierszy, ale zużycie pamięci rośnie wraz z obiektami stylów. Ponownie używaj jednej instancji `Style` dla wszystkich kolumn walutowych, aby zmniejszyć zużycie pamięci.

### Brakujące style

Jeśli `columnStyles` jest krótszy niż liczba kolumn, Aspose zastosuje domyślny styl do pozostałych kolumn. To przydatne, gdy zależy Ci tylko na kilku kolumnach.

---

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie elementy, o których rozmawialiśmy, oraz kilka pomocnych komentarzy.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Oczekiwany rezultat:** Otwarcie `StyledTable.xlsx` pokazuje kolumnę `Price` z symbolem dolara i dwoma miejscami po przecinku, dokładnie tak, jak wymagało polecenie **format cells currency**.

---

## Najczęściej zadawane pytania

**Q: Czy to działa z .NET Core?**  
A: Absolutnie. Aspose.Cells jest zgodny z .NET standard, więc możesz celować w .NET 5, .NET 6 lub nowsze bez zmian.

**Q: Co jeśli mój DataTable ma 10 kolumn, a ja chcę sformatować tylko kolumnę 5?**  
A: Utwórz `Style[]` o długości 10, wypełnij pozycje 0‑4 i 6‑9 wartością `null`, a własny styl umieść pod indeksem 4 (licząc od zera). Aspose zastosuje każdy wpis.

**Q: Czy mogę ukryć wiersz nagłówka?**  
A: Po imporcie ustaw `worksheet.Cells.Rows[0].Hidden = true;` lub po prostu przekaż `false` dla parametru `includeColumnNames` w metodzie `ImportDataTable`.

---

## Podsumowanie

Właśnie **created an Excel workbook C#**, zaimportowaliśmy `DataTable` i **applied a currency format column** przy użyciu Aspose.Cells. Główne kroki — przygotowanie danych, definiowanie stylu, budowanie tablicy stylów, importowanie za pomocą `ImportDataTable` i zapis — obejmują rdzeń większości zadań automatyzacji Excela.

Od tego momentu możesz eksplorować:

- **add number format excel** dla dat lub procentów  
- Eksportowanie wielu arkuszy w jednym pliku  
- Używanie **format cells currency** z symbolami specyficznymi dla locale  
- Automatyzację tworzenia wykresów na podstawie tych samych danych  

Spróbuj tych pomysłów, a szybko zostaniesz osobą, do której zespół zwróci się po raporty w Excelu. Masz własny pomysł, którym chcesz się podzielić? zostaw komentarz poniżej — miłego kodowania!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}