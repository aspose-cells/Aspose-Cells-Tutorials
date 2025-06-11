---
"description": "Naučte se, jak v Aspose.Cells pro .NET zadat HTML CrossType. Postupujte podle našeho podrobného návodu a převeďte soubory Excelu do HTML s přesností."
"linktitle": "Programové zadávání HTML CrossType ve výstupním HTML v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové zadávání HTML CrossType ve výstupním HTML v .NET"
"url": "/cs/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové zadávání HTML CrossType ve výstupním HTML v .NET

## Zavedení
Pokud jde o převod souborů Excelu do HTML v aplikacích .NET, můžete se setkat s potřebou specifikovat, jak se mají ve výstupu zpracovávat křížové odkazy. Třída HtmlSaveOptions v Aspose.Cells pro .NET poskytuje různá nastavení pro řízení procesu převodu a jednou z těchto možností je HtmlCrossType. V tomto tutoriálu si ukážeme, jak programově specifikovat křížový typ HTML při exportu souborů Excelu do formátu HTML. 
## Předpoklady
Než se ponoříte do kódu, ujistěte se, že máte následující:
- Aspose.Cells pro .NET: Ujistěte se, že máte ve svém projektu nainstalovanou knihovnu Aspose.Cells. Můžete si ji stáhnout z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: Funkční instalace Visual Studia nebo jakéhokoli jiného vývojového prostředí .NET.
- Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům.
- Ukázkový soubor Excel: Mějte připravený ukázkový soubor Excel, se kterým budete moci pracovat. V tomto příkladu použijeme `sampleHtmlCrossStringType.xlsx`.
## Importovat balíčky
Chcete-li začít, budete muset importovat potřebné jmenné prostory Aspose.Cells. Zde je návod, jak to udělat:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Pojďme si to rozebrat krok za krokem, abyste si to mohli snadno prostudovat a implementovat tuto funkci do svých vlastních projektů.
## Krok 1: Definujte zdrojové a výstupní adresáře
Nejprve je třeba nastavit adresáře pro zdrojový soubor Excel a kam chcete uložit výstupní soubor HTML.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
## Krok 2: Načtěte ukázkový soubor Excel
Dále nahrajte ukázkový soubor Excelu do `Workbook` předmět. Tady začíná všechna magie.
```csharp
// Načíst ukázkový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Zde nahraďte `"Your Document Directory"` se skutečnou cestou, kde se nachází váš soubor Excel. Tento řádek načte soubor Excel do paměti, abyste s ním mohli manipulovat.
## Krok 3: Zadejte možnosti ukládání HTML
Nyní vytvoříme instanci `HtmlSaveOptions`, který umožňuje nakonfigurovat, jak bude soubor Excel převeden do formátu HTML.
```csharp
// Zadejte křížový typ HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
V tomto kroku jsme nastavili `HtmlCrossStringType` na `HtmlCrossType.Default`, což je jedna z možností dostupných pro zpracování křížových odkazů ve výstupním HTML.
## Krok 4: Změňte typ kříže podle potřeby
Můžete zadat různé typy pro `HtmlCrossStringType` na základě vašich požadavků. Zde jsou různé možnosti, které můžete použít:
- `HtmlCrossType.Default`Výchozí typ kříže.
- `HtmlCrossType.MSExport`Exportuje HTML s chováním podobným MS Excelu.
- `HtmlCrossType.Cross`: Vytváří křížové odkazy.
- `HtmlCrossType.FitToCell`Přizpůsobí křížové odkazy rozměrům buňky.
Můžete upravit `HtmlCrossStringType` takhle:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpnebot;
// nebo 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Krok 5: Uložení výstupního souboru HTML
Jakmile nakonfigurujete možnosti, je čas uložit převedený soubor HTML. Použijte `Save` metoda na vašem `Workbook` objekt:
```csharp
// Výstupní HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Zde pojmenováváme výstupní soubor na základě `HtmlCrossStringType` které jsme nastavili. Tímto způsobem snadno zjistíte, který typ kříže byl použit při převodu.
## Krok 6: Potvrzení úspěšného provedení
Nakonec je vždy dobrým zvykem potvrdit, že operace proběhla úspěšně. Můžete vypsat zprávu do konzole:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Tím zjistíte, že proces proběhl bez chyb.
## Závěr
tady to máte! Úspěšně jste zadali křížový typ HTML pro export do Excelu v .NET pomocí Aspose.Cells. Tato funkce je obzvláště užitečná, když potřebujete ve výstupu HTML zachovat specifické formátování nebo odkazy a zajistit, aby převedené dokumenty splňovaly vaše požadavky.
## Často kladené otázky
### Co je HtmlCrossType v Aspose.Cells?  
HtmlCrossType definuje, jak se křížové odkazy v souboru Excel zpracovávají během převodu HTML. Můžete si vybrat možnosti jako Výchozí, MSExport, Křížový odkaz a Přizpůsobitbuňce.
### Mohu používat Aspose.Cells zdarma?  
Aspose.Cells nabízí bezplatnou zkušební verzi. Můžete si ji stáhnout z jejich [webové stránky](https://releases.aspose.com/).
### Jak nainstaluji Aspose.Cells do svého .NET projektu?  
Aspose.Cells můžete nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu spuštěním příkazu: `Install-Package Aspose.Cells`.
### Kde najdu dokumentaci k Aspose.Cells?  
Komplexní dokumentaci naleznete na Aspose.Cells. [zde](https://reference.aspose.com/cells/net/).
### Co mám dělat, když se při ukládání HTML souboru setkám s chybou?  
Ujistěte se, že cesty k adresářům jsou správné a že máte oprávnění k zápisu do výstupního adresáře. Pokud problém přetrvává, vyhledejte pomoc na fóru podpory Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}