---
"description": "Naučte se, jak efektivně používat minigrafy v Excelu s Aspose.Cells pro .NET. Součástí je podrobný návod pro hladký průběh práce."
"linktitle": "Používání miniaturních grafů"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Používání miniaturních grafů"
"url": "/cs/net/advanced-chart-operations/using-sparklines/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Používání miniaturních grafů

## Zavedení

dnešním uspěchaném světě analýzy a vizualizace dat často hledáme rychlé a efektivní způsoby prezentace informací. Minigrafy (microgramy) jsou elegantním řešením – malý, jednoduchý graf nebo tabulka, která poskytuje přehled o trendech a změnách dat v kompaktním formátu. Ať už jste analytik, vývojář nebo někdo, kdo prostě miluje data, naučení se používat minigrafy v dokumentech aplikace Excel pomocí Aspose.Cells pro .NET může vylepšit prezentaci vašich informací. V této příručce prozkoumáme proces implementace minigrafů krok za krokem a zajistíme, abyste mohli efektivně využít sílu této úžasné funkce.

## Předpoklady

Než se ponoříme do světa jisker, pojďme si probrat některé předpoklady, které nám pomohou připravit půdu pro naši cestu:

1. Znalost C#: Základní znalost programování v C# vám pomůže lépe porozumět kódovací části.
2. Nainstalovaný .NET Framework: Ujistěte se, že máte v systému nainstalovaný .NET Framework.
3. Aspose.Cells pro .NET: V projektu budete potřebovat knihovnu Aspose.Cells. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/).
4. Šablona aplikace Excel: Použijeme soubor aplikace Excel s názvem `sampleUsingSparklines.xlsx`Uložte si ho do pracovního adresáře.

Nyní, když máme potřebné nastavení, pojďme si rozebrat kroky k implementaci jisker!

## Importovat balíčky

Před napsáním kódu musíme importovat potřebné balíčky. Do souboru C# vložte následující příkazy using:

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System;
using System.Drawing;
```

Import těchto balíčků vám poskytne přístup ke knihovně Aspose.Cells, funkcím renderování a základním systémovým knihovnám pro práci s barvami a operacemi konzole.

## Krok 1: Inicializace výstupního a zdrojového adresáře

V tomto prvním kroku definujeme adresáře, kam budou uloženy naše výstupní a zdrojové soubory. 

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory"; // zadejte cestu

// Zdrojový adresář
string sourceDir = "Your Document Directory"; // zadejte cestu
```

Zde nahraďte `Your Output Directory` a `Your Document Directory` se skutečnými cestami ve vašem systému.

## Krok 2: Vytvořte a otevřete sešit

Nyní si vytvořme sešit a otevřeme náš soubor šablony aplikace Excel.

```csharp
// Vytvoření instance sešitu
// Otevření souboru šablony
Workbook book = new Workbook(sourceDir + "sampleUsingSparklines.xlsx");
```

Tento kód vytvoří instanci `Workbook` třída a načte zadaný soubor šablony ze zdrojového adresáře.

## Krok 3: Přístup k prvnímu pracovnímu listu

Dále se dostaneme k prvnímu listu v našem sešitu. 

```csharp
// Získejte první pracovní list
Worksheet sheet = book.Worksheets[0];
```

Přístupem k prvnímu pracovnímu listu můžeme začít manipulovat s daty a prvky v něm.

## Krok 4: Přečtěte si existující minigrafy (pokud existují)

Pokud chcete zkontrolovat, zda se v listu nacházejí nějaké existující jiskry, můžete tak učinit pomocí následujícího kódu:

```csharp
// Načíst Sparklines ze souboru šablony (pokud existují)
foreach (SparklineGroup g in sheet.SparklineGroupCollection)
{
    // Zobrazit informace o skupině minigrafů
    Console.WriteLine("sparkline group: type:" + g.Type + ", sparkline items count:" + g.SparklineCollection.Count);
    
    foreach (Sparkline s in g.SparklineCollection)
    {
        // Zobrazení jednotlivých minigrafů a jejich datových rozsahů
        Console.WriteLine("sparkline: row:" + s.Row + ", col:" + s.Column + ", dataRange:" + s.DataRange);
    }
}
```

Spuštěním této funkce se zobrazí informace o všech jiskrových křivkách, které jsou již v souboru Excelu přítomny – užitečný způsob, jak zjistit, jaké trendy v datech jsou již vizualizovány!

## Krok 5: Definování oblasti buňky pro nové minigrafy

Dále chceme definovat, kam budou naše nové jiskry umístěny v listu. 

```csharp
// Definujte oblast buněk D2:D10
CellArea ca = new CellArea();
ca.StartColumn = 4; // E
ca.EndColumn = 4;   // E
ca.StartRow = 1;    // 2
ca.EndRow = 7;      // 8
```

V tomto úryvku kódu nastavujeme v listu oblast s označením D2:D10, kde budou vytvořeny nové mixgrafy. Upravte odkazy na buňky podle toho, kde chcete mixgrafy zobrazit.

## Krok 6: Přidání minigrafů do pracovního listu

S naší definovanou oblastí buňky je čas vytvořit a přidat jiskry!

```csharp
// Přidání nových minigrafů pro datovou oblast do oblasti buněk
int idx = sheet.SparklineGroupCollection.Add(SparklineType.Column, "Sheet1!B2:D8", false, ca);
SparklineGroup group = sheet.SparklineGroupCollection[idx];
```

Zde přidáváme sloupcovou jiskrovou křivku pro data, která se rozprostírají `Sheet1!B2:D8` do dříve definované oblasti buněk. Nezapomeňte upravit rozsah dat podle svých požadavků.

## Krok 7: Úprava barev jiskrových linií

Proč se držet výchozích barev, když můžete mít trochu šmrncu? Pojďme si barvy jiskrových čar přizpůsobit!

```csharp
// Vytvořit buňkyBarva
CellsColor clr = book.CreateCellsColor();
clr.Color = Color.Orange; // Vyberte si požadovanou barvu
group.SeriesColor = clr;
```

tomto kódu vytváříme nový `CellsColor` například nastavením na oranžovou a použitím této barvy na sérii jiskrových čar, kterou jsme právě vytvořili.

## Krok 8: Uložení upraveného sešitu

Nakonec uložme změny do sešitu a dokončíme to!

```csharp
// Uložte soubor Excelu
book.Save(outputDir + "outputUsingSparklines.xlsx");

Console.WriteLine("UsingSparklines executed successfully.");
```

Tato část kódu uloží upravený sešit do zadaného výstupního adresáře. Zobrazí se zpráva o úspěchu potvrzující, že vše proběhlo hladce.

## Závěr

A tady to máte – komplexního podrobného návodu k vytváření a používání mixgrafií v excelových listech pomocí Aspose.Cells pro .NET. Mixgrafie jsou fantastickým způsobem, jak poskytnout vizuálně atraktivní a snadno stravitelné datové přehledy. Ať už se jedná o reporty, prezentace nebo dokonce interní dokumenty, tato dynamická funkce může vaše data učinit působivějšími.

## Často kladené otázky

### Co jsou to jiskry (miskrové čáry)?
Miniaturní grafy (sparklines) se vejdou do jedné buňky a poskytují kompaktní a jednoduchou vizualizaci datových trendů.

### Potřebuji licenci k používání Aspose.Cells?
Ano, k používání všech funkcí Aspose.Cells budete potřebovat platnou licenci. Můžete si ji pořídit [dočasná licence](https://purchase.aspose.com/temporary-license/) pokud teprve začínáte.

### Mohu vytvářet různé typy jisker (mirrorlines)?
Rozhodně! Aspose.Cells podporuje různé typy sparklineů, včetně řádkových, sloupcových a win/loss sparklineů.

### Kde najdu další dokumentaci?
K dispozici je podrobná dokumentace a příklady pro Aspose.Cells pro .NET. [zde](https://reference.aspose.com/cells/net/).

### Je k dispozici bezplatná zkušební verze?
Ano, můžete si stáhnout bezplatnou zkušební verzi Aspose.Cells. [zde](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}