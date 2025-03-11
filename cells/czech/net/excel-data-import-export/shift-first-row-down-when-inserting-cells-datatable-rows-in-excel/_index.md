---
title: Shift první řádek dolů při vkládání řádků DataTable v Excelu
linktitle: Shift první řádek dolů při vkládání řádků DataTable v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se vkládat řádky DataTable do Excelu bez posunutí prvního řádku dolů pomocí Aspose.Cells for .NET. Průvodce krok za krokem pro automatizaci bez námahy.
weight: 11
url: /cs/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Shift první řádek dolů při vkládání řádků DataTable v Excelu

## Zavedení

Nebaví vás ruční posouvání řádků při vkládání nových dat do excelových tabulek? Tak to máš štěstí! V tomto článku se ponoříme do toho, jak tento proces automatizovat pomocí Aspose.Cells for .NET. Na konci tohoto kurzu se nejen naučíte pracovat s datovými tabulkami v Excelu, ale také jak upravit možnosti importu tak, aby lépe vyhovovaly vašim potřebám. Věř mi; to vám může ušetřit spoustu času a námahy! Takže, vezměte si šálek kávy a můžeme začít!

## Předpoklady

Než se pustíme do kódování, ujistěte se, že máte vše nastaveno:

1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio (2017 nebo novější by mělo fungovat dobře).
2.  Aspose.Cells for .NET: Musíte mít knihovnu Aspose.Cells. Pokud jste to ještě neudělali, můžete si ji stáhnout[zde](https://releases.aspose.com/cells/net/).
3. Základní porozumění C# a Excelu: Základní znalost programování v C# a toho, jak Excel funguje, vám jistě pomůže efektivněji pokračovat.

 Budete také chtít mít po ruce vzorový soubor Excel. V této příručce použijeme ukázku s názvem`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Tento soubor můžete vytvořit nebo najít šablonu, která vyhovuje vašim potřebám.

## Importujte balíčky

Než se vrhneme na kódování, musíme se ujistit, že importujeme potřebné balíčky. Ve svém projektu C# zahrňte následující jmenné prostory:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Tyto balíčky jsou nezbytné pro práci se sešitem, pracovním listem a tabulkami.

## Krok 1: Nastavte svůj projekt

### Vytvořte nový projekt C#

Začněte vytvořením nové konzolové aplikace C# v sadě Visual Studio. Dejte svému projektu vhodný název, například „ExcelDataImport“.

### Přidejte balíček NuGet Aspose.Cells

Chcete-li přidat balíček Aspose.Cells, klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení, vyberte Spravovat balíčky NuGet a vyhledejte „Aspose.Cells“. Nainstalujte balíček, abyste se ujistili, že máte přístup ke všem funkcím, které potřebujeme.

## Krok 2: Definujte tabulku dat

 Dále implementujeme`ICellsDataTable` rozhraní k vytvoření třídy, která poskytuje data k importu. Zde je návod, jak můžete strukturovat`CellsDataTable` třída:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Implementovat další členy...
}
```

Zde definujeme názvy sloupců a data pro každý sloupec, což usnadní strukturu naší importované tabulky.

## Krok 3: Implementujte členy rozhraní ICellsDataTable

 V rámci`CellsDataTable` třídy, musíte implementovat členy`ICellsDataTable` rozhraní. Zde je požadovaná implementace:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Tato část třídy zpracovává načítání dat, definuje počet řádků a sloupců a spravuje aktuální stav indexu.

## Krok 4: Napište hlavní funkci

 Nyní vytvoříme`Run`metoda pro orchestraci celého procesu importu tabulky:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Krok 5: Nastavte možnosti importu

 Chcete-li řídit chování importu, měli byste vytvořit instanci`ImportTableOptions` a podle toho nastavte vlastnosti. Konkrétně chceme nastavit`ShiftFirstRowDown` na`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Nechceme posouvat první řadu dolů
```

## Krok 6: Importujte tabulku DataTable

 Nyní můžeme importovat data z našeho`CellsDataTable` do pracovního listu.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Tento příkaz přímo vloží vaši datovou tabulku počínaje zadaným řádkem a sloupcem.

## Krok 7: Uložte sešit

Nakonec upravený sešit uložíme zpět do souboru:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Závěr

A tady to máte! Naučili jste se, jak vložit řádky DataTable do listu aplikace Excel bez přesunutí prvního řádku pomocí Aspose.Cells for .NET. Tento proces nejen zefektivňuje manipulaci s daty v Excelu, ale také zvyšuje výkon vaší aplikace automatizací obvykle těžkopádného úkolu. S těmito znalostmi ve vaší sadě nástrojů budete lépe vybaveni ke zvládnutí úloh automatizace Excelu, což vám ušetří čas a námahu.

## FAQ

### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je programovací knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel v aplikacích .NET.

### Potřebuji licenci k používání Aspose.Cells?
Ano, pro plné funkce budete potřebovat platnou licenci. Pro počáteční testování je však k dispozici bezplatná zkušební verze.

### Mohu používat Aspose.Cells ve webových aplikacích?
Absolutně! Aspose.Cells je ideální pro desktopové, webové a cloudové aplikace vyvinuté v .NET.

### Jaké typy souborů aplikace Excel mohu vytvořit pomocí Aspose.Cells?
Můžete vytvářet různé formáty souborů aplikace Excel, včetně XLSX, XLS, CSV a dalších.

### Kde mohu získat podporu pro Aspose.Cells?
 Můžete se ptát nebo najít pomoc v[Aspose fóra](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
