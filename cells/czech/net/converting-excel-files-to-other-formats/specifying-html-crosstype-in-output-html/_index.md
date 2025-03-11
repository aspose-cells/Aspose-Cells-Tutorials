---
title: Určení HTML CrossType ve výstupním HTML Programově v .NET
linktitle: Určení HTML CrossType ve výstupním HTML Programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak určit HTML CrossType v Aspose.Cells pro .NET. Postupujte podle našeho podrobného výukového programu a převeďte soubory Excel do HTML s přesností.
weight: 17
url: /cs/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Určení HTML CrossType ve výstupním HTML Programově v .NET

## Zavedení
Pokud jde o převod souborů aplikace Excel na HTML v aplikacích .NET, možná budete muset určit, jak se ve výstupu zachází s křížovými odkazy. Třída HtmlSaveOptions v Aspose.Cells for .NET poskytuje různá nastavení pro řízení procesu převodu a jednou z těchto možností je HtmlCrossType. V tomto tutoriálu si projdeme, jak programově určit křížový typ HTML při exportu souborů aplikace Excel do formátu HTML. 
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte následující:
-  Aspose.Cells for .NET: Ujistěte se, že máte v projektu nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
- Visual Studio: Funkční instalace sady Visual Studio nebo jakéhokoli jiného vývojového prostředí .NET.
- Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům.
-  Ukázkový soubor Excel: Připravte si vzorový soubor Excel, se kterým můžete pracovat. Pro tento příklad použijeme`sampleHtmlCrossStringType.xlsx`.
## Importujte balíčky
Chcete-li začít, budete muset importovat potřebné jmenné prostory Aspose.Cells. Můžete to udělat takto:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Pojďme si to rozebrat krok za krokem, abyste mohli snadno sledovat a implementovat tuto funkci ve svých vlastních projektech.
## Krok 1: Definujte zdrojový a výstupní adresář
Nejprve musíte nastavit adresáře pro váš zdrojový soubor Excel a kam chcete uložit výstupní soubor HTML.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
## Krok 2: Načtěte ukázkový soubor Excel
 Dále načtěte vzorový soubor Excel do a`Workbook` objekt. Tady začíná veškerá magie.
```csharp
// Načtěte ukázkový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Tady, vyměňte`"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor Excel. Tento řádek načte soubor aplikace Excel do paměti, abyste s ním mohli manipulovat.
## Krok 3: Zadejte možnosti uložení HTML
 Nyní vytvoříme instanci`HtmlSaveOptions`, který vám umožňuje nakonfigurovat, jak bude soubor Excel převeden do HTML.
```csharp
// Zadejte křížový typ HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 V tomto kroku jsme nastavili`HtmlCrossStringType` na`HtmlCrossType.Default`, což je jedna z dostupných možností pro zpracování křížových odkazů ve výstupním HTML.
## Krok 4: Změňte typ kříže podle potřeby
 Můžete zadat různé typy pro`HtmlCrossStringType` na základě vašich požadavků. Zde jsou různé možnosti, které můžete použít:
- `HtmlCrossType.Default`: Výchozí typ kříže.
- `HtmlCrossType.MSExport`: Exportuje HTML s chováním podobným MS Excel.
- `HtmlCrossType.Cross`: Vytváří křížové odkazy.
- `HtmlCrossType.FitToCell`: Přizpůsobí křížové odkazy rozměrům buněk.
 Můžete upravit`HtmlCrossStringType` takhle:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// nebo
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// nebo
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Krok 5: Uložte výstupní soubor HTML
 Jakmile nakonfigurujete své možnosti, je čas uložit převedený soubor HTML. Použijte`Save` metoda na vašem`Workbook` objekt:
```csharp
// Výstup Html
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Zde pojmenováváme výstupní soubor na základě`HtmlCrossStringType` nastavili jsme. Snadno tak poznáte, který typ kříže byl při převodu použit.
## Krok 6: Potvrďte úspěšné provedení
Nakonec je vždy dobrým zvykem potvrdit, že vaše operace byla úspěšná. Můžete vytisknout zprávu do konzole:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
To vám dá vědět, že proces byl dokončen bez jakýchkoli chyb.
## Závěr
tady to máte! Úspěšně jste zadali křížový typ HTML pro export Excelu v .NET pomocí Aspose.Cells. Tato funkce je zvláště užitečná, když potřebujete zachovat specifické formátování nebo odkazy ve výstupu HTML a zajistit, aby vaše převedené dokumenty splňovaly vaše požadavky.
## FAQ
### Co je HtmlCrossType v Aspose.Cells?  
HtmlCrossType definuje, jak jsou křížové odkazy v souboru Excel zpracovány během převodu HTML. Můžete si vybrat možnosti jako Výchozí, MSExport, Cross a FitToCell.
### Mohu používat Aspose.Cells zdarma?  
 Aspose.Cells nabízí bezplatnou zkušební verzi. Můžete si jej stáhnout z jejich[webové stránky](https://releases.aspose.com/).
### Jak nainstaluji Aspose.Cells do svého .NET projektu?  
 Aspose.Cells můžete nainstalovat přes NuGet Package Manager ve Visual Studiu spuštěním příkazu:`Install-Package Aspose.Cells`.
### Kde najdu dokumentaci k Aspose.Cells?  
 Kompletní dokumentaci najdete na Aspose.Cells[zde](https://reference.aspose.com/cells/net/).
### Co mám dělat, pokud při ukládání souboru HTML narazím na chybu?  
Ujistěte se, že jsou cesty k adresáři správné a že máte oprávnění k zápisu do výstupního adresáře. Pokud problém přetrvává, vyhledejte pomoc na fóru podpory Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
