---
title: Vykreslit sekvenční stránky v Aspose.Cells
linktitle: Vykreslit sekvenční stránky v Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se vykreslovat sekvenční stránky v Excelu pomocí Aspose.Cells pro .NET. Tento návod krok za krokem poskytuje podrobného průvodce převodem vybraných stránek na obrázky.
weight: 18
url: /cs/net/rendering-and-export/render-limited-number-of-sequential-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vykreslit sekvenční stránky v Aspose.Cells

## Zavedení
Vykreslování konkrétních stránek z excelového sešitu může být neuvěřitelně užitečné, zvláště když potřebujete pouze určité datové vizuály bez celého souboru. Aspose.Cells for .NET je výkonná knihovna, která nabízí přesnou kontrolu nad dokumenty aplikace Excel v aplikacích .NET, což umožňuje vykreslovat vybrané stránky, měnit formáty a další. Tento kurz vás provede převodem konkrétních stránek listu aplikace Excel do obrazových formátů – ideální pro vytváření přizpůsobených snímků dat.
## Předpoklady
Než skočíte do kódu, ujistěte se, že máte nastaveny následující položky:
-  Knihovna Aspose.Cells for .NET: Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Jakékoli prostředí s podporou .NET, jako je Visual Studio.
- Soubor Excel: Ukázkový soubor Excel s více stránkami uložený ve vašem místním adresáři.
 Kromě toho se ujistěte, že máte bezplatnou zkušební verzi nebo si kupte licenci, pokud ji nemáte. Podívejte se na[dočasná licence](https://purchase.aspose.com/temporary-license/) k prozkoumání všech funkcí před nákupem.
## Importujte balíčky
Chcete-li začít, budeme muset importovat Aspose.Cells a všechny potřebné jmenné prostory do vašeho prostředí .NET.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```
Tyto balíčky poskytují všechny třídy a metody potřebné k manipulaci a vykreslování souborů aplikace Excel. Nyní si podrobně rozeberme jednotlivé části procesu vykreslování.
## Krok 1: Nastavte zdrojový a výstupní adresář
Nejprve definujeme adresáře pro vstupní a výstupní soubory, abychom zajistili, že náš program ví, kam soubory načíst a uložit.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
Zadáním zdrojových a výstupních adresářů zjednodušíte přístup k souborům pro operace čtení i zápisu. Ujistěte se, že tyto adresáře existují, abyste předešli chybám za běhu.
## Krok 2: Načtěte ukázkový soubor Excel
 Dále načteme náš soubor Excel pomocí Aspose.Cells'`Workbook` třída. Tento soubor bude obsahovat data a stránky, které chceme vykreslit.
```csharp
// Načtěte ukázkový soubor Excel
Workbook wb = new Workbook(sourceDir + "sampleImageOrPrintOptions_PageIndexPageCount.xlsx");
```
 The`Workbook`class je jako váš hlavní obslužný program Excelu v Aspose.Cells, který poskytuje přímý přístup k listům, stylům a dalším.
## Krok 3: Přístup k cílovému listu
Nyní si vybereme konkrétní list, se kterým chceme pracovat. V tomto tutoriálu použijeme první list, ale můžete jej upravit na libovolný list, který potřebujete.
```csharp
// Otevřete první pracovní list
Worksheet ws = wb.Worksheets[0];
```
Každý sešit může mít více listů a klíčový je výběr toho správného. Tento řádek uděluje přístup k zadanému listu, kde bude probíhat vykreslování.
## Krok 4: Nastavte možnosti obrázku nebo tisku
Abychom mohli ovládat způsob vykreslování našich stránek, definujeme některé možnosti tisku. Zde určíme, které stránky se mají vykreslit, formát obrázku a další nastavení.
```csharp
// Zadejte možnosti obrázku nebo tisku
ImageOrPrintOptions opts = new ImageOrPrintOptions();
opts.PageIndex = 3; // Začněte na straně 4
opts.PageCount = 4; // Vykreslit čtyři stránky
opts.ImageType = Drawing.ImageType.Png;
```
 S`ImageOrPrintOptions` , můžete nastavit`PageIndex` (úvodní stránka),`PageCount` (počet stránek k vykreslení) a`ImageType` (formát pro výstup). Toto nastavení vám dává přesnou kontrolu nad procesem vykreslování.
## Krok 5: Vytvořte objekt vykreslení listu
Nyní vytvoříme a`SheetRender` objekt, který vezme naše možnosti listu a obrázku a vykreslí každou zadanou stránku jako obrázek.
```csharp
// Vytvořte objekt vykreslení listu
SheetRender sr = new SheetRender(ws, opts);
```
 The`SheetRender` třída je nezbytná pro vykreslování pracovních listů do obrázků, PDF nebo jiných formátů. Ke generování výstupů používá list a možnosti, které jste nakonfigurovali.
## Krok 6: Vykreslení a uložení každé stránky jako obrázku
Nakonec projdeme každou zadanou stránku a uložíme ji jako obrázek. Tato smyčka se stará o vykreslení každé stránky a její uložení s jedinečným názvem.
```csharp
// Vytiskněte všechny stránky jako obrázky
for (int i = opts.PageIndex; i < sr.PageCount; i++)
{
    sr.ToImage(i, outputDir + "outputImage-" + (i + 1) + ".png");
}
```
Zde je rozpis toho, co se děje:
-  The`for` smyčka prochází každou stránku v určeném rozsahu.
- `ToImage` se používá k vykreslení každé stránky jako obrázku s vlastním formátem názvu souboru pro rozlišení každé stránky.
## Krok 7: Potvrďte dokončení
Po dokončení vykreslování přidejte jednoduchou potvrzovací zprávu. Tento krok je volitelný, ale může být užitečný pro ověření úspěšného provedení.
```csharp
Console.WriteLine("RenderLimitedNoOfSequentialPages executed successfully.\r\n");
```
Tento poslední řádek potvrzuje, že vše fungovalo tak, jak bylo zamýšleno. Tato zpráva se zobrazí ve vaší konzoli po vykreslení a uložení všech stránek.
## Závěr
A tady to máte! Vykreslování konkrétních stránek v excelovém sešitu pomocí Aspose.Cells for .NET je přímočarý, ale výkonný způsob, jak přizpůsobit výstup dat. Ať už potřebujete snímek klíčových metrik nebo konkrétní datové vizuály, tento kurz vám pomůže. Podle těchto kroků nyní můžete vykreslit jakoukoli stránku nebo rozsah stránek ze souborů aplikace Excel do krásných obrazových formátů.
 Neváhejte a prozkoumejte další možnosti v rámci`ImageOrPrintOptions` a`SheetRender` pro ještě větší kontrolu. Šťastné kódování!
## FAQ
### Mohu vykreslit více listů současně?  
 Ano, můžete procházet`Worksheets` shromažďovat a aplikovat proces vykreslování jednotlivě na každý list.
### Do jakých dalších formátů mohu vykreslovat stránky kromě PNG?  
 Aspose.Cells podporuje několik formátů, včetně JPEG, BMP, TIFF a GIF. Stačí se změnit`ImageType` v`ImageOrPrintOptions`.
### Jak zpracuji velké soubory aplikace Excel s mnoha stránkami?  
velkých souborů zvažte rozdělení vykreslování na menší části, abyste efektivně řídili využití paměti.
### Je možné upravit rozlišení obrazu?  
 Ano,`ImageOrPrintOptions` umožňuje nastavení DPI pro vlastní rozlišení pomocí`HorizontalResolution` a`VerticalResolution`.
### Co když potřebuji vykreslit pouze část stránky?  
Můžete použít`PrintArea` majetek v`PageSetup` k definování konkrétních oblastí na listu k vykreslení.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
