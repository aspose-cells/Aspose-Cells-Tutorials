---
category: general
date: 2026-03-27
description: Jak utworzyć tabelę przestawną w C# przy użyciu Aspose.Cells – dowiedz
  się, jak dodać dane, włączyć odświeżanie i zapisać skoroszyt jako xlsx w jednym
  samouczku.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: pl
og_description: Jak utworzyć tabelę przestawną w C# przy użyciu Aspose.Cells. Ten
  przewodnik pokazuje, jak dodać dane, włączyć odświeżanie i zapisać skoroszyt jako
  xlsx.
og_title: Jak utworzyć tabelę przestawną w C# – Kompletny samouczek Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak utworzyć tabelę przestawną w C# – pełny przewodnik z Aspose.Cells
url: /pl/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć tabelę przestawną w C# – Kompletny samouczek Aspose.Cells

Zastanawiałeś się kiedyś **jak utworzyć tabelę przestawną** w C# bez walki z COM interop? Nie jesteś jedyny. W wielu aplikacjach opartych na danych potrzebujemy szybkiego sposobu na przekształcenie surowych danych sprzedażowych w przejrzyste podsumowanie, a Aspose.Cells sprawia, że to pestka.  

W tym samouczku przejdziemy przez każdy krok: dodawanie danych, budowanie tabeli przestawnej, włączenie automatycznego odświeżania oraz w końcu **zapisanie skoroszytu jako xlsx**, aby użytkownicy mogli od razu otworzyć go w Excelu. Po zakończeniu będziesz mieć gotowy plik `PivotRefresh.xlsx` oraz solidne zrozumienie, dlaczego każda linia ma znaczenie.

## Wymagania wstępne

- .NET 6+ (lub .NET Framework 4.7.2 i nowszy) – każdy nowoczesny runtime działa.  
- Aspose.Cells for .NET – możesz go pobrać z NuGet (`Install-Package Aspose.Cells`).  
- Podstawowa znajomość składni C# – nie wymaga głębokiej wiedzy o Excelu.  

> **Porada:** Jeśli pracujesz na komputerze firmowym, upewnij się, że licencja Aspose jest zastosowana; w przeciwnym razie na wygenerowanym pliku pojawi się znak wodny.

## Krok 1 – Jak dodać dane do nowego skoroszytu

Zanim tabela przestawna może istnieć, musi istnieć tabela źródłowa. Utworzymy nowy skoroszyt, nazwimy pierwszy arkusz *SalesData* i wstawimy kilka wierszy, które naśladują rzeczywisty zestaw danych sprzedażowych.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Dlaczego to jest ważne:**  
- Użycie `PutValue` automatycznie ustawia typ komórki, więc nie musisz martwić się później o niezgodności między ciągiem znaków a liczbą.  
- Definiowanie nagłówków w wierszu 1 daje silnikowi tabeli przestawnej coś, do czego może się odwołać przy mapowaniu pól.

## Krok 2 – Utwórz arkusz, który będzie hostował tabelę przestawną

Tabela przestawna znajduje się na osobnym arkuszu, co utrzymuje dane źródłowe w czystości i raport w porządku.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Co jeśli już masz arkusz?** Po prostu odwołaj się do niego po indeksie (`workbook.Worksheets["MySheet"]`) zamiast dodawać nowy.

## Krok 3 – Zdefiniuj zakres źródłowy (Jak dodać dane → Zdefiniuj zakres)

Aspose.Cells potrzebuje `CellArea` lub ciągu określającego zakres, który obejmuje zarówno nagłówki, jak i dane. Tutaj zakładamy maksymalnie 100 wierszy; dostosuj w razie potrzeby.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Przypadek brzegowy:** Jeśli Twój zestaw danych jest dynamiczny, możesz obliczyć ostatni używany wiersz za pomocą `salesDataSheet.Cells.MaxDataRow` i odpowiednio zbudować zakres.

## Krok 4 – Jak utworzyć tabelę przestawną – Wstaw tabelę przestawną

Teraz najciekawsza część: instruujemy Aspose.Cells, aby utworzył tabelę przestawną powiązaną z zakresem, który właśnie zdefiniowaliśmy.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Zwróć uwagę na odwołanie w stylu formuły (`=SalesData!A1:D100`). To ta sama składnia, którą wpisałbyś w Excelu, co sprawia, że API jest intuicyjne.

## Krok 5 – Skonfiguruj pola wierszy, kolumn i danych (Jak dodać dane → Pola)

Umieścimy *Region* w wierszach, *Product* w kolumnach oraz zsumujemy zarówno *Units*, jak i *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Dlaczego te indeksy?**  
- Aspose.Cells indeksuje kolumny zaczynając od 0, więc `0` wskazuje na *Region*. Metoda `DataFields.Add` pozwala zmienić nazwę pola (np. „Sum of Units”) i wybrać typ agregacji – `Sum` jest najczęściej używany dla danych liczbowych.

## Krok 6 – Jak włączyć odświeżanie – Spraw, aby tabela przestawna automatycznie aktualizowała się przy otwarciu

Jeśli dane źródłowe zmienią się później, prawdopodobnie chcesz, aby tabela przestawna automatycznie odzwierciedlała te zmiany. W tym miejscu przydaje się `RefreshDataOnOpen`.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Uwaga:** Ta flaga działa tylko wtedy, gdy skoroszyt jest otwierany w Excelu; nie zostanie przeliczone wewnątrz Aspose.Cells, chyba że ręcznie wywołasz `pivotTable.RefreshData()`.

## Krok 7 – Zapisz skoroszyt jako XLSX (Jak zapisać skoroszyt jako XLSX)

Na koniec zapisujemy plik na dysku. Format `.xlsx` to nowoczesny, oparty na zipie typ pliku Excel, który działa wszędzie.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Uruchomienie programu tworzy plik o nazwie **PivotRefresh.xlsx** w folderze wykonywania. Otwórz go w Excelu, a zobaczysz starannie ułożoną tabelę przestawną z wierszami *Region*, kolumnami *Product* oraz sumowanymi wartościami *Units* i *Revenue*. Ponieważ włączyliśmy odświeżanie, wszelkie zmiany wprowadzone w arkuszu *SalesData* automatycznie zaktualizują tabelę przestawną przy następnym otwarciu skoroszytu.

### Oczekiwany wynik

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Liczby będą się różnić w zależności od dodanych wierszy.)*

---

## Często zadawane pytania i warianty

### Co zrobić, jeśli potrzebuję wielu tabel przestawnych?

Możesz powtórzyć **Krok 4** z inną nazwą i lokalizacją. Każde wywołanie `PivotTables.Add` zwraca nowy indeks, którego możesz użyć do pobrania obiektu tabeli.

### Jak zmienić agregację na *Average* zamiast *Sum*?

Zastąp `PivotTableDataAggregationType.Sum` przez `PivotTableDataAggregationType.Average` w wywołaniach `DataFields.Add`.

### Czy mogę stylizować tabelę przestawną (czcionki, kolory)?

Tak. Po utworzeniu tabeli przestawnej możesz uzyskać dostęp do jej właściwości `Style` lub zastosować formatowanie komórek do zakresu zawierającego tabelę przestawną. Na przykład:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Czy można dodać więcej wierszy po zapisaniu skoroszytu?

Oczywiście. Załaduj plik za pomocą `new Workbook("PivotRefresh.xlsx")`, dopisz wiersze do arkusza *SalesData* i wywołaj `pivotTable.RefreshData()` przed ponownym zapisaniem.

## Pełny działający przykład (Gotowy do kopiowania i wklejenia)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Zapisz plik, uruchom go i otwórz wygenerowany **PivotRefresh.xlsx** – właśnie opanowałeś **tworzenie tabeli przestawnej** w C#.

## Podsumowanie

Omówiliśmy **tworzenie tabel przestawnych** programowo, jak **dodawać dane**, jak **włączać odświeżanie**, a na koniec jak **zapisać skoroszyt jako xlsx** przy użyciu Aspose.Cells. Kod

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}