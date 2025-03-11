---
title: Formátování a vzhled kontingenčních tabulek Programově v .NET
linktitle: Formátování a vzhled kontingenčních tabulek Programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Vylepšete své kontingenční tabulky Excel pomocí Aspose.Cells pro .NET. Naučte se formátovat, přizpůsobovat a automatizovat prezentaci dat bez námahy.
weight: 16
url: /cs/net/creating-and-configuring-pivot-tables/formatting-and-look/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formátování a vzhled kontingenčních tabulek Programově v .NET

## Zavedení
Kontingenční tabulky jsou fantastické nástroje v Excelu, které uživatelům umožňují shrnout a analyzovat komplexní datové sady. Dokážou transformovat všední data do vizuálně přitažlivých a informativních zpráv, které uživatelům umožňují rychle získat přehled. V tomto tutoriálu prozkoumáme, jak manipulovat se styly kontingenční tabulky pomocí Aspose.Cells for .NET, což vám umožní bez námahy automatizovat a přizpůsobovat vaše sestavy Excel. Jste připraveni zlepšit své dovednosti v oblasti prezentace dat? Pojďme se ponořit!
## Předpoklady
Než se vydáme na tuto cestu, je třeba mít připraveno několik náležitostí:
1. Visual Studio: Toto bude naše hlavní prostředí pro kódování a testování.
2.  Aspose.Cells for .NET: Ujistěte se, že máte nainstalovanou tuto knihovnu. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
3. Základní porozumění C#: Znalost programování v C# vám pomůže snadno pokračovat.
4. Soubor Excel: Budete potřebovat existující soubor Excel, který obsahuje kontingenční tabulku. Pokud žádný nemáte, můžete si vytvořit jednoduchý pomocí aplikace Microsoft Excel.
Jakmile máte vše nastaveno, přejděme k importu potřebných balíčků!
## Importujte balíčky
Abychom mohli začít, musíme importovat požadované knihovny do našeho projektu C#. Můžete to udělat takto:
### Vytvořte nový projekt C#
Nejprve otevřete Visual Studio a vytvořte nový projekt aplikace konzoly. To nám umožní snadno spustit náš kód.
### Přidat reference
Jakmile je váš projekt nastaven, budete muset přidat odkaz na knihovnu Aspose.Cells:
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte "Aspose.Cells" a nainstalujte balíček.
Po dokončení jste připraveni importovat jmenný prostor Aspose.Cells. Níže je uveden kód pro import potřebných balíčků:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Nyní, když jsme importovali naše balíčky, pojďme se blíže podívat na to, jak manipulovat s formátováním kontingenční tabulky v Excelu.
## Krok 1: Nastavte adresář dokumentů
Nejprve definujeme cestu k našemu souboru Excel. Postup je následující:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou, kde je uložen váš soubor Excel.
## Krok 2: Načtěte sešit
 Dále musíme načíst váš stávající soubor Excel. V tomto kroku využijeme`Workbook` třídy, kterou poskytuje Aspose.Cells.
```csharp
// Načtěte soubor šablony
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Když vyměníte`"Book1.xls"` s vaším skutečným názvem souboru,`workbook` objekt bude nyní obsahovat data aplikace Excel.
## Krok 3: Otevřete sešit a kontingenční tabulku
Nyní chceme uchopit list a kontingenční tabulku, se kterými budeme pracovat:
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
var pivot = workbook.Worksheets[0].PivotTables[0];
```
V tomto případě používáme první list a první kontingenční tabulku. Pokud váš soubor Excel obsahuje více listů nebo kontingenčních tabulek, nezapomeňte odpovídajícím způsobem upravit hodnoty indexu.

Nyní, když máme přístup k kontingenční tabulce, je na čase, aby byla vizuálně přitažlivá! Můžeme nastavit styl a formátovat celou kontingenční tabulku. Zde je postup:
## Krok 4: Nastavení stylu kontingenční tabulky
Aplikujme předdefinovaný styl na naši kontingenční tabulku:
```csharp
pivot.PivotTableStyleType = PivotTableStyleType.PivotTableStyleDark1;
```
Tento řádek kódu změní styl kontingenční tabulky na tmavý motiv. Můžete prozkoumat různé styly dostupné v knihovně Aspose.Cells a najít ten, který vyhovuje vašim potřebám.
## Krok 5: Přizpůsobte styl kontingenční tabulky
Pro další přizpůsobení si můžeme vytvořit svůj styl. Jak skvělé to je? Můžete to udělat takto:
```csharp
Style style = workbook.CreateStyle();
style.Font.Name = "Arial Black";
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
```
V tomto úryvku:
- Písmo určíme jako "Arial Black."
- Barva popředí je nastavena na žlutou.
- Vzor nastavíme na plný.
## Krok 6: Použijte vlastní styl na kontingenční tabulku
Nakonec použijeme tento nově vytvořený styl k formátování celé kontingenční tabulky:
```csharp
pivot.FormatAll(style);
```
Tento řádek použije váš vlastní styl na všechna data v kontingenční tabulce. Nyní by váš stůl měl vypadat fantasticky!
## Krok 7: Uložte změny
Jakmile dokončíte formátování kontingenční tabulky, nezapomeňte uložit změny. Postup uložení dokumentu:
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "output.xls");
```
 Nahradit`"output.xls"` s jakýmkoli názvem, který chcete pro nově naformátovaný soubor Excel. A voilà! Úspěšně jste naformátovali kontingenční tabulku pomocí Aspose.Cells for .NET.
## Závěr
Stručně řečeno, vydali jsme se na cestu k programovému formátování kontingenčních tabulek v Excelu pomocí Aspose.Cells pro .NET. Začali jsme importem potřebných balíčků, načetli jsme existující excelový sešit, přizpůsobili styly kontingenční tabulky a nakonec jsme uložili náš formátovaný výstup. Začleněním těchto dovedností do vašeho pracovního postupu můžete automatizovat únavné úlohy formátování, které vás mohou stát drahocenný čas. Tak proč to nezkusit? Vyzkoušejte si to sami a pozvedněte svou excelovou hru!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro manipulaci se soubory aplikace Excel v aplikacích .NET, která umožňuje snadné dokončení automatizovaných a programových úkolů.
### Mohu vyzkoušet Aspose.Cells zdarma?
 Ano! Kliknutím můžete začít s bezplatnou zkušební verzí[zde](https://releases.aspose.com).
### Jaké typy stylů kontingenčních tabulek jsou k dispozici?
 Aspose.Cells poskytuje různé předdefinované styly, ke kterým lze přistupovat prostřednictvím`PivotTableStyleType`.
### Jak mohu vytvořit kontingenční tabulku v Excelu?
Kontingenční tabulku můžete vytvořit v Excelu pomocí karty "Vložit" na panelu nástrojů a výběrem "Kontingenční tabulka" z možností.
### Kde mohu získat podporu pro Aspose.Cells?
 Pomoc můžete najít na fóru Aspose[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
