---
"description": "Snadno aktualizujte položky vzorců Power Query v Excelu pomocí Aspose.Cells pro .NET. Podrobný návod pro zefektivnění procesů manipulace s daty."
"linktitle": "Aktualizace položky vzorce Power Query"
"second_title": "Referenční příručka k Aspose.Cells pro .NET API"
"title": "Aktualizace položky vzorce Power Query"
"url": "/cs/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aktualizace položky vzorce Power Query

## Zavedení

Pokud jste někdy pracovali s Excelem, víte, jak mocný může být – zvláště když se začnete ponořovat do Power Queries. Ty jsou tajnou přísadou, která vám umožňuje bez námahy transformovat, čistit a analyzovat data. Jedním šikovným způsobem, jak manipulovat se vzorci Power Query v Excelu, je Aspose.Cells pro .NET. Dnes vás krok za krokem provedeme aktualizací položek vzorců Power Query. Takže, vezměte si programátorskou čepici a pojďme na to!

## Předpoklady

Než se ponoříte do kódu, je třeba mít nastavených několik věcí:

1. Visual Studio: Pro psaní a spouštění kódu .NET budete potřebovat integrované vývojové prostředí (IDE). Visual Studio je tou nejlepší volbou.
2. Knihovna Aspose.Cells: Ujistěte se, že máte ve svém projektu k dispozici knihovnu Aspose.Cells. Můžete si ji stáhnout z [místo](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: I když si to projdeme společně, určité základní znalosti C# jistě pomohou, zejména při navigaci v různých třídách a metodách.
4. Ukázkové soubory aplikace Excel: Budete potřebovat soubory aplikace Excel uvedené v úryvku kódu. Ujistěte se, že máte:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi rozhraní .NET Framework.

Teď, když máme sadu připravenou, můžeme se pustit do zábavné části: psaní kódu!

## Importovat balíčky

Nejdříve budete chtít importovat potřebné jmenné prostory. Zde je návod, jak to udělat:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Přidáním těchto jmenných prostorů dáváte kompilátoru vědět, že máte v úmyslu použít třídy a metody z knihovny Aspose.Cells. Tento krok je klíčový, protože pokládá základy pro následující kód.

Pojďme si rozebrat úryvek kódu, který jste poskytli. Tento tutoriál vás provede jednotlivými částmi a ujistí se, že rozumíte tomu, co se děje.

## Krok 1: Nastavení pracovních adresářů

V tomto kroku definujeme, kde se nacházejí naše zdrojové a výstupní soubory. Tím zajistíme, že Aspose bude vědět, kde má hledat vaše soubory Excelu.

```csharp
// Pracovní adresáře
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Krok 2: Načtení sešitu

Nyní načtěme soubor Excelu, ve kterém se nachází Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
Ten/Ta/To `Workbook` Třída je vaším vstupním bodem do souboru aplikace Excel. Předáním cesty k našemu zdrojovému souboru vytváříme instanci, která nám umožňuje s ním manipulovat. Můžete si to představit jako otevření knihy – chystáte se číst (nebo upravovat) její obsah.

## Krok 3: Přístup k mashupu dat

Dále se budeme zabývat vzorci Power Query uloženými v datovém mashupu sešitu.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
Ten/Ta/To `DataMashup` Třída obsahuje všechny vzorce Power Query spojené s vaším sešitem. Zde se budeme věnovat té nejtěžší práci, podobně jako když otevřete sadu nástrojů pro opravy.

## Krok 4: Procházení vzorců Power Query

Nyní přichází část, kde iterujeme vzorce Power Query, abychom našli ten konkrétní, který chceme aktualizovat.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Procházíme každým `PowerQueryFormula` v `mashupData`.
- V rámci této smyčky se ponoříme do každého `PowerQueryFormulaItem`.
- Zkontrolujeme, zda název položky odpovídá „Zdroj“. Pokud ano, aktualizujeme její hodnotu tak, aby odkazovala na náš nový zdrojový soubor.

Je to podobné jako najít správnou stránku v manuálu a provést potřebné aktualizace – je to přímočarý a pečlivý proces.

## Krok 5: Uložení aktualizovaného sešitu

Po provedení aktualizací je čas uložit změny.

```csharp
// Uložte výstupní sešit.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Ten/Ta/To `Save` Metoda zapíše aktualizovaný sešit do zadaného výstupního adresáře. Je to jako zapečetit vaše úpravy v nové verzi manuálu, připravené k použití ostatními!

## Závěr

Gratulujeme! Úspěšně jste aktualizovali položku vzorce Power Query pomocí Aspose.Cells pro .NET. Pomocí této metody můžete automatizovat úpravy vzorců Power Query v souborech Excelu, což vám ušetří drahocenný čas a úsilí.

## Často kladené otázky

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro manipulaci s excelovými soubory v .NET aplikacích bez nutnosti instalace Microsoft Excelu.

### Potřebuji Microsoft Excel ke spuštění Aspose.Cells?
Ne, Aspose.Cells umožňuje programově vytvářet a upravovat soubory Excelu, aniž byste museli mít Excel na serveru nebo vývojovém počítači.

### S jakými typy souborů aplikace Excel mohu pracovat pomocí Aspose.Cells?
Pomocí Aspose.Cells můžete pracovat s formáty .xlsx, .xls, .xlsm a několika dalšími formáty aplikace Excel.

### Je k dispozici zkušební verze pro Aspose.Cells?
Ano, můžete si stáhnout bezplatnou zkušební verzi z [Stránka s vydáním Aspose Cells](https://releases.aspose.com/).

### Jak mohu získat podporu pro Aspose.Cells?
Podporu můžete získat prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a najít odpovědi od komunity a týmu Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}