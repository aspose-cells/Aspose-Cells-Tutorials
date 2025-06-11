---
"description": "Naučte se, jak upravit úroveň komprese sešitů aplikace Excel pomocí Aspose.Cells pro .NET v tomto podrobném návodu. Optimalizujte správu souborů."
"linktitle": "Úprava úrovně komprese v sešitu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Úprava úrovně komprese v sešitu"
"url": "/cs/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Úprava úrovně komprese v sešitu

## Zavedení
Pokud jde o správu velkých souborů aplikace Excel, komprese je zásadní změnou. Nejenže šetří úložný prostor, ale také urychluje a zefektivňuje přenos souborů. Pokud pracujete s Aspose.Cells pro .NET, můžete snadno upravit úroveň komprese svých sešitů. V této příručce vás krok za krokem provedeme celým procesem a ujistíme se, že rozumíte každé části kódu a tomu, jak funguje.
## Předpoklady
Než se ponoříme do kódu, je třeba splnit několik předpokladů:
1. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
2. Knihovna Aspose.Cells: Musíte mít nainstalovanou knihovnu Aspose.Cells. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/).
3. Visual Studio: Pro spuštění kódu bude nutné vývojové prostředí, jako je Visual Studio.
4. .NET Framework: Ujistěte se, že váš projekt je nastaven s kompatibilní verzí .NET Framework.
## Importovat balíčky
Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Zde je návod, jak to udělat:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
Tyto balíčky jsou nezbytné pro práci s excelovými soubory pomocí knihovny Aspose.Cells. `Aspose.Cells` jmenný prostor obsahuje všechny třídy, které potřebujete k manipulaci se soubory aplikace Excel, zatímco `Aspose.Cells.Xlsb` nabízí možnosti ukládání souborů ve formátu XLSB.
Nyní si rozdělme proces úpravy úrovně komprese v sešitu na zvládnutelné kroky.
## Krok 1: Definování zdrojového a výstupního adresáře
Nejprve je třeba určit, kde se nacházejí zdrojové soubory a kam chcete uložit výstupní soubory. To je klíčové pro to, aby váš program věděl, kde najít soubory, se kterými potřebuje pracovat.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou k vašim adresářům. To pomůže programu najít soubory, které chcete komprimovat.
## Krok 2: Načtení sešitu
Dále načtete sešit, který chcete komprimovat. A tady začíná kouzlo!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
tomto řádku vytvoříme novou instanci třídy `Workbook` třídu a načtěte existující soubor aplikace Excel. Ujistěte se, že název souboru odpovídá názvu souboru ve zdrojovém adresáři.
## Krok 3: Nastavení možností ukládání
Nyní je čas nakonfigurovat možnosti ukládání. Nastavíme typ komprese výstupního souboru. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
Ten/Ta/To `XlsbSaveOptions` Třída umožňuje zadat různé možnosti při ukládání sešitu ve formátu XLSB, včetně úrovní komprese.
## Krok 4: Změřte dobu komprese pro úroveň 1
Začněme s první úrovní komprese. Změříme, jak dlouho trvá uložení sešitu s touto úrovní komprese.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Zde nastavíme typ komprese na úroveň 1, uložíme sešit a poté změříme uplynulý čas. To nám dává představu o tom, jak dlouho proces trvá.
## Krok 5: Změřte dobu komprese pro úroveň 6
Dále se podívejme, jak si vede komprese úrovně 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Tento krok je podobný předchozímu, ale úroveň komprese změníme na úroveň 6. Všimněte si, že doba potřebná k vyplnění se může lišit v závislosti na složitosti sešitu.
## Krok 6: Změřte dobu komprese pro úroveň 9
Nakonec se podívejme na výkon s nejvyšší úrovní komprese.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
V tomto kroku nastavíme úroveň komprese na úroveň 9. Zde obvykle dojde k nejvýznamnějšímu zmenšení velikosti souboru, ale zpracování může trvat déle.
## Krok 7: Konečný výstup
Po spuštění všech úrovní komprese můžete zobrazit zprávu oznamující, že proces byl úspěšně dokončen.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Tento jednoduchý řádek kódu potvrzuje, že váš program proběhl bez jakýchkoli zádrhelů.
## Závěr
Úprava úrovně komprese sešitů pomocí Aspose.Cells pro .NET je přímočarý proces, který může vést k významným výhodám, pokud jde o velikost souboru a výkon. Dodržováním kroků uvedených v této příručce můžete snadno implementovat kompresi ve svých aplikacích a zlepšit efektivitu správy souborů v Excelu.
## Často kladené otázky
### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti používat Microsoft Excel.
### Jak nainstaluji Aspose.Cells?  
Aspose.Cells si můžete stáhnout a nainstalovat z [Webové stránky Aspose](https://releases.aspose.com/cells/net/).
### Jaké jsou k dispozici úrovně komprese?  
Aspose.Cells podporuje několik úrovní komprese od úrovně 1 (nejnižší komprese) do úrovně 9 (nejvyšší komprese).
### Mohu si Aspose.Cells vyzkoušet zdarma?  
Ano! Můžete získat bezplatnou zkušební verzi Aspose.Cells. [zde](https://releases.aspose.com/).
### Kde najdu podporu pro Aspose.Cells?  
případě jakýchkoli dotazů nebo potřeby podpory můžete navštívit fórum podpory Aspose. [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}