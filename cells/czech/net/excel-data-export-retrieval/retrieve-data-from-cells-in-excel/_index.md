---
title: Načítání dat z buněk v Excelu
linktitle: Načítání dat z buněk v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak načíst data z buněk aplikace Excel pomocí Aspose.Cells for .NET v tomto podrobném tutoriálu, který je ideální pro začátečníky i zkušené vývojáře.
weight: 10
url: /cs/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načítání dat z buněk v Excelu

## Zavedení

Pokud jde o správu dat v Excelu, schopnost číst a získávat informace z buněk je zásadní. Aspose.Cells for .NET je výkonná knihovna, která umožňuje vývojářům bezproblémově manipulovat se soubory aplikace Excel. V tomto tutoriálu se ponoříme do toho, jak načíst data z buněk v excelovém sešitu pomocí Aspose.Cells. Ať už jste zkušený vývojář nebo teprve začínáte, tento průvodce vás provede procesem krok za krokem.

## Předpoklady

Než se pustíme do kódu, je potřeba splnit několik předpokladů:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Je to IDE, které budeme používat k psaní a provádění našeho kódu.
2.  Aspose.Cells for .NET: Musíte mít knihovnu Aspose.Cells. Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům.
4. Soubor Excel: Připravte si soubor Excel (např.`book1.xls`), který budete používat pro tento tutoriál.

Jakmile máte tyto předpoklady seřazeny, můžeme začít zkoumat, jak načíst data z buněk Excelu.

## Importujte balíčky

Chcete-li začít, musíte do svého projektu C# importovat potřebné jmenné prostory. To vám umožní využívat třídy a metody poskytované Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

S importovanými těmito jmennými prostory jste připraveni začít kódovat. Pojďme si tento proces rozdělit na zvládnutelné kroky.

## Krok 1: Nastavte adresář dokumentů

Prvním krokem je definovat cestu k adresáři dokumentů, kde se nachází váš soubor Excel. To je zásadní, protože to aplikaci říká, kde má najít soubor, se kterým chcete pracovat.


```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```

 Nahradit`"Your Document Directory"` se skutečnou cestou, kde jste`book1.xls` soubor je uložen. Tato cesta je místo, kde bude Aspose.Cells hledat soubor, když se jej pokusíte otevřít.

## Krok 2: Otevřete existující sešit

Nyní, když máte nastavený adresář dokumentů, je dalším krokem otevření sešitu (soubor Excel), se kterým chcete pracovat.


```csharp
//Otevření existujícího sešitu
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

 Zde vytvoříme a`Workbook` objekt předáním úplné cesty k souboru aplikace Excel. Tento krok inicializuje sešit a připraví jej pro načtení dat.

## Krok 3: Otevřete první pracovní list

Po otevření sešitu budete chtít získat přístup ke konkrétnímu listu, ze kterého chcete načíst data. V tomto případě přistoupíme k prvnímu listu.


```csharp
// Přístup k prvnímu pracovnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```

 The`Worksheets` kolekce umožňuje přístup k různým listům v sešitu. Index`[0]` odkazuje na první pracovní list. Chcete-li získat přístup k dalším listům, můžete odpovídajícím způsobem změnit index.

## Krok 4: Smyčka přes buňky

Nyní, když máte list, je čas projít každou buňku a načíst data. Tady se děje kouzlo!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Proměnné pro ukládání hodnot různých datových typů
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Předání typu dat obsažených v buňce k vyhodnocení
    switch (cell1.Type)
    {
        // Vyhodnocení datového typu dat buňky pro hodnotu řetězce
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Vyhodnocení datového typu dat buňky na dvojnásobnou hodnotu
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //Vyhodnocení datového typu dat buňky na booleovskou hodnotu
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Vyhodnocení datového typu dat buňky pro hodnotu data/času
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Vyhodnocení neznámého datového typu dat buňky
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Ukončení typové kontroly typu dat buňky je null
        case CellValueType.IsNull:
            break;
    }
}
```

 V tomto kroku procházíme každou buňku v listu. U každé buňky zkontrolujeme její datový typ pomocí a`switch` prohlášení. V závislosti na typu načteme hodnotu a vytiskneme ji do konzole. Zde je rozpis případů:

-  IsString: Pokud buňka obsahuje řetězec, načteme jej pomocí`StringValue`.
-  IsNumeric: Pro číselné hodnoty používáme`DoubleValue`.
-  IsBool: Pokud buňka obsahuje booleovskou hodnotu, přistupujeme k ní pomocí`BoolValue`.
-  IsDateTime: Pro hodnoty data a času používáme`DateTimeValue`.
- IsUnknown: Pokud je datový typ neznámý, stále získáme reprezentaci řetězce.
- IsNull: Pokud je buňka prázdná, jednoduše ji přeskočíme.

## Závěr

Načítání dat z buněk aplikace Excel pomocí Aspose.Cells for .NET je jednoduchý proces. Pomocí těchto kroků můžete efektivně extrahovat různé typy dat ze souborů aplikace Excel. Ať už vytváříte nástroj pro vytváření sestav, automatizujete zadávání dat nebo jen potřebujete data analyzovat, Aspose.Cells poskytuje flexibilitu a výkon, které potřebujete k dokončení své práce.

## FAQ

### Co je Aspose.Cells?  
Aspose.Cells je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.

### Mohu používat Aspose.Cells zdarma?  
 Ano, Aspose.Cells nabízí bezplatnou zkušební verzi, kterou můžete použít k otestování jejích funkcí. Můžete si jej stáhnout[zde](https://releases.aspose.com/).

### Jaké typy dat mohu načíst z buněk aplikace Excel?  
Můžete načíst různé typy dat, včetně řetězců, čísel, booleanů a hodnot data/času.

### Jak získám podporu pro Aspose.Cells?  
 Podporu můžete získat návštěvou stránky[Aspose fórum](https://forum.aspose.com/c/cells/9) kde můžete klást otázky a získat pomoc od komunity.

### Je k dispozici dočasná licence?  
 Ano, Aspose nabízí dočasnou licenci pro účely hodnocení. Více informací naleznete[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
