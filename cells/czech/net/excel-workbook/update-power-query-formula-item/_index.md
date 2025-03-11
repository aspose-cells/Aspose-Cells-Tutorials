---
title: Aktualizujte položku vzorce Power Query
linktitle: Aktualizujte položku vzorce Power Query
second_title: Aspose.Cells for .NET API Reference
description: Položky vzorců Power Query v Excelu snadno aktualizujte pomocí Aspose.Cells for .NET. Podrobný průvodce pro zefektivnění vašich procesů manipulace s daty.
weight: 160
url: /cs/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktualizujte položku vzorce Power Query

## Zavedení

Pokud jste někdy pracovali s Excelem, víte, jak výkonný může být – zvláště když se začnete ponořit do Power Queries. Toto je tajná omáčka, která vám umožňuje transformovat, čistit a analyzovat vaše data bez námahy. Jeden šikovný způsob, jak manipulovat se vzorci Power Query v Excelu, je přes Aspose.Cells for .NET. Dnes vás provedeme aktualizací položek vzorce Power Query krok za krokem. Takže popadněte svůj kódovací klobouk a můžeme začít!

## Předpoklady

Než se ponoříte do kódu, je několik věcí, které budete chtít nastavit:

1. Visual Studio: K psaní a spouštění kódu .NET budete potřebovat integrované vývojové prostředí (IDE). Visual Studio je tou správnou volbou.
2.  Knihovna Aspose.Cells: Ujistěte se, že máte v projektu k dispozici knihovnu Aspose.Cells. Můžete si jej stáhnout z[místo](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: I když si tím společně projdeme, určité základní znalosti C# jistě pomohou, zvláště při procházení různými třídami a metodami.
4. Ukázkové soubory aplikace Excel: Budete potřebovat soubory aplikace Excel uvedené ve fragmentu kódu. Ujistěte se, že máte:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi rozhraní .NET Framework.

Nyní, když máme naši sadu připravenou, můžeme přistoupit k té zábavné části: psaní kódu!

## Importujte balíčky

Nejprve budete chtít importovat potřebné jmenné prostory. Jak na to:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Přidáním těchto jmenných prostorů dáváte kompilátoru vědět, že hodláte použít třídy a metody z knihovny Aspose.Cells. Tento krok je zásadní, protože pokládá základy pro kód, který následuje.

Pojďme si rozebrat fragment kódu, který jste poskytli. Tento tutoriál vás provede každou částí a zajistí, že pochopíte, co se děje.

## Krok 1: Nastavte pracovní adresáře

tomto kroku definujeme, kde jsou umístěny naše zdrojové a výstupní soubory. To zajišťuje, že Aspose ví, kde hledat vaše soubory Excel.

```csharp
// Pracovní adresáře
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Krok 2: Načtěte sešit

Nyní načteme soubor Excel, kde je umístěn Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 The`Workbook` třída je vaším vstupním bodem do souboru Excel. Předáním cesty k našemu zdrojovému souboru vytváříme instanci, která nám umožňuje s ním manipulovat. Můžete si to představit jako otevření knihy – připravujete se na čtení (nebo úpravu) jejího obsahu.

## Krok 3: Přístup k Data Mashup

Dále přistoupíme k vzorcům Power Query uloženým v sešitu Data Mashup.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 The`DataMashup` třída obsahuje všechny vzorce Power Query přidružené k vašemu sešitu. Tady budeme těžce zvedat, podobně jako když otevřete krabici s nářadím pro opravy.

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

-  Procházíme každým`PowerQueryFormula` v`mashupData`.
-  rámci této smyčky se ponoříme do každého`PowerQueryFormulaItem`.
- Zkontrolujeme, zda se název položky shoduje se „Zdroj“. Pokud ano, aktualizujeme jeho hodnotu, aby odkazovala na náš nový zdrojový soubor.

Je to podobné, jako byste našli správnou stránku v příručce a poté provedli potřebné aktualizace – je to přímočarý a pečlivý proces.

## Krok 5: Uložte aktualizovaný sešit

Po provedení aktualizací je čas uložit naše změny.

```csharp
// Uložte výstupní sešit.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 The`Save` metoda zapíše aktualizovaný sešit do zadaného výstupního adresáře. Je to jako zapečetění vašich úprav v nové verzi manuálu, připravené pro ostatní!

## Závěr

Gratuluji! Úspěšně jste aktualizovali položku vzorce Power Query pomocí Aspose.Cells for .NET. Pomocí této metody můžete automatizovat úpravy vzorců Power Query v souborech Excelu, což vám ušetří drahocenný čas a úsilí.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro manipulaci se soubory aplikace Excel v aplikacích .NET bez nutnosti instalace aplikace Microsoft Excel.

### Potřebuji ke spuštění Aspose.Cells Microsoft Excel?
Ne, Aspose.Cells vám umožňuje vytvářet a upravovat soubory Excelu programově bez nutnosti aplikace Excel na vašem serveru nebo vývojovém počítači.

### S jakými typy souborů Excel mohu pracovat pomocí Aspose.Cells?
Pomocí Aspose.Cells můžete pracovat s .xlsx, .xls, .xlsm a několika dalšími formáty aplikace Excel.

### Je k dispozici zkušební verze pro Aspose.Cells?
 Ano, můžete si stáhnout bezplatnou zkušební verzi z[Stránka vydání Aspose Cells](https://releases.aspose.com/).

### Jak mohu získat podporu pro Aspose.Cells?
 K podpoře se můžete dostat přes[Aspose fórum](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a hledat odpovědi od komunity a týmu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
