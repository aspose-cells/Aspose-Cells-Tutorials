---
category: general
date: 2026-03-27
description: Jak vytvořit kontingenční tabulku v C# pomocí Aspose.Cells – naučte se
  přidávat data, povolit aktualizaci a uložit sešit jako xlsx v jednom tutoriálu.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: cs
og_description: Jak vytvořit kontingenční tabulku v C# s Aspose.Cells. Tento průvodce
  vám ukáže, jak přidat data, povolit aktualizaci a uložit sešit jako xlsx.
og_title: Jak vytvořit kontingenční tabulku v C# – Kompletní tutoriál Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak vytvořit kontingenční tabulku v C# – Kompletní průvodce s Aspose.Cells
url: /cs/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit kontingenční tabulku v C# – Kompletní tutoriál Aspose.Cells

Už jste se někdy zamýšleli **jak vytvořit kontingenční tabulku** v C# bez zbytečného boje s COM interop? Nejste jediní. V mnoha aplikacích založených na datech potřebujeme rychlý způsob, jak převést surová prodejní čísla na přehledné shrnutí, a Aspose.Cells to dělá hračkou.  

V tomto tutoriálu projdeme každý krok: přidání dat, vytvoření kontingenční tabulky, zapnutí automatického obnovení a nakonec **uložení sešitu jako xlsx**, aby si jej uživatelé mohli okamžitě otevřít v Excelu. Na konci budete mít připravený soubor `PivotRefresh.xlsx` a pevné pochopení, proč každá řádka kódu má smysl.

## Požadavky

- .NET 6+ (nebo .NET Framework 4.7.2 a novější) – funguje jakékoli aktuální prostředí.
- Aspose.Cells for .NET – můžete jej stáhnout z NuGet (`Install-Package Aspose.Cells`).
- Základní znalost syntaxe C# – není potřeba hluboké znalosti Excelu.

> **Pro tip:** Pokud pracujete na firemním počítači, ujistěte se, že je použita licence Aspose; jinak se na vygenerovaném souboru objeví vodoznak.

## Krok 1 – Jak přidat data do nového sešitu

Než může existovat kontingenční tabulka, musí být zdrojová tabulka. Vytvoříme nový sešit, pojmenujeme první list *SalesData* a vložíme několik řádků, které napodobují reálný výpis prodejů.

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

**Proč je to důležité:**  
- Použití `PutValue` automaticky nastaví typ buňky, takže se později nemusíte starat o nesoulad mezi řetězci a čísly.  
- Definování hlaviček v řádku 1 poskytne kontingenčnímu enginu něco, na co se může při mapování polí odkazovat.

## Krok 2 – Vytvořit list, který bude hostit kontingenční tabulku

Kontingenční tabulka sídlí na vlastním listu, čímž zůstane zdrojová data čistá a přehled zůstane přehledný.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Co když už máte list?** Stačí na něj odkazovat podle indexu (`workbook.Worksheets["MySheet"]`) místo přidávání nového.

## Krok 3 – Definovat zdrojový rozsah (Jak přidat data → Definovat rozsah)

Aspose.Cells potřebuje `CellArea` nebo řetězec rozsahu, který zahrnuje jak hlavičky, tak data. Zde předpokládáme maximálně 100 řádků; upravte podle potřeby.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Hraniční případ:** Pokud je váš datový soubor dynamický, můžete poslední použitý řádek spočítat pomocí `salesDataSheet.Cells.MaxDataRow` a rozsah sestavit podle toho.

## Krok 4 – Jak vytvořit kontingenční tabulku – Vložit kontingenční tabulku

Nyní zábavná část: řekneme Aspose.Cells, aby vytvořil kontingenční tabulku propojenou s rozsahem, který jsme právě nastavili.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Všimněte si reference ve stylu vzorce (`=SalesData!A1:D100`). Jedná se o stejnou syntaxi, jakou zadáváte v Excelu, což činí API intuitivním.

## Krok 5 – Nastavit řádkové, sloupcové a datové pole (Jak přidat data → Pole)

Umístíme *Region* do řádků, *Product* do sloupců a sečteme jak *Units*, tak *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Proč tyto indexy?**  
Aspose.Cells indexuje sloupce od 0, takže `0` odkazuje na *Region*. Metoda `DataFields.Add` vám umožní přejmenovat pole (např. „Sum of Units“) a zvolit typ agregace – `Sum` je nejčastější pro číselná data.

## Krok 6 – Jak povolit automatické obnovení – Kontingenční tabulka se aktualizuje při otevření

Pokud se zdrojová data později změní, pravděpodobně chcete, aby se kontingenční tabulka automaticky přizpůsobila. Zde vstupuje do hry `RefreshDataOnOpen`.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Poznámka:** Tento příznak funguje pouze při otevření sešitu v Excelu; v Aspose.Cells se neprovede přepočet, pokud nevoláte `pivotTable.RefreshData()` ručně.

## Krok 7 – Uložit sešit jako XLSX (Jak uložit sešit jako XLSX)

Nakonec soubor uložíme na disk. Formát `.xlsx` je moderní, zip‑založený typ souboru Excel, který funguje všude.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Po spuštění programu se vytvoří soubor **PivotRefresh.xlsx** ve složce, odkud byl program spuštěn. Otevřete jej v Excelu a uvidíte přehledně uspořádanou kontingenční tabulku s řádky *Region*, sloupci *Product* a součty *Units* a *Revenue*. Protože jsme povolili automatické obnovení, jakékoli úpravy listu *SalesData* automaticky aktualizují kontingenční tabulku při dalším otevření sešitu.

### Očekávaný výstup

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Čísla se budou lišit podle vámi přidaných řádků.)*

---

## Často kladené otázky a varianty

### Co když potřebuji více kontingenčních tabulek?

Můžete opakovat **Krok 4** s jiným názvem a umístěním. Každé volání `PivotTables.Add` vrátí nový index, který můžete použít k získání objektu tabulky.

### Jak změnit agregaci na *Average* místo *Sum*?

Nahraďte `PivotTableDataAggregationType.Sum` za `PivotTableDataAggregationType.Average` v voláních `DataFields.Add`.

### Můžu stylovat kontingenční tabulku (písma, barvy)?

Ano. Po vytvoření kontingenční tabulky můžete přistupovat k její vlastnosti `Style` nebo aplikovat formátování buněk na rozsah, který tabulku obsahuje. Například:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Je možné přidat další řádky po uložení sešitu?

Rozhodně. Načtěte soubor pomocí `new Workbook("PivotRefresh.xlsx")`, připojte řádky do listu *SalesData* a před dalším uložením zavolejte `pivotTable.RefreshData()`.

---

## Kompletní funkční příklad (připravený ke zkopírování)

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

Uložte soubor, spusťte jej a otevřete vygenerovaný **PivotRefresh.xlsx** – právě jste si osvojili **jak vytvořit kontingenční tabulku** v C#.

---

## Závěr

Probrali jsme **jak vytvořit kontingenční tabulky** programově, jak **přidat data**, jak **povolit automatické obnovení** a nakonec jak **uložit sešit jako xlsx** pomocí Aspose.Cells. Kód

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}