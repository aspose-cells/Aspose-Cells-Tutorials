---
title: Upravte úroveň komprese v sešitu
linktitle: Upravte úroveň komprese v sešitu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném průvodci se dozvíte, jak upravit úroveň komprese sešitů aplikace Excel pomocí Aspose.Cells for .NET. Optimalizujte správu souborů.
weight: 14
url: /cs/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravte úroveň komprese v sešitu

## Zavedení
Pokud jde o správu velkých souborů aplikace Excel, komprese mění hru. Nejen, že šetří úložný prostor, ale také zrychluje a zefektivňuje přenos souborů. Pokud pracujete s Aspose.Cells pro .NET, můžete snadno upravit úroveň komprese vašich sešitů. V této příručce vás provedeme procesem krok za krokem a zajistíme, že rozumíte každé části kódu a tomu, jak funguje.
## Předpoklady
Než se ponoříte do kódu, musíte mít splněno několik předpokladů:
1. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
2.  Knihovna Aspose.Cells: Musíte mít nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Visual Studio: Ke spuštění kódu bude nutné vývojové prostředí, jako je Visual Studio.
4. .NET Framework: Ujistěte se, že je váš projekt nastaven s kompatibilní verzí rozhraní .NET Framework.
## Importujte balíčky
Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Můžete to udělat takto:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Tyto balíčky jsou nezbytné pro práci se soubory Excel pomocí knihovny Aspose.Cells. The`Aspose.Cells` jmenný prostor obsahuje všechny třídy, které potřebujete k manipulaci se soubory aplikace Excel`Aspose.Cells.Xlsb` poskytuje možnosti pro ukládání souborů ve formátu XLSB.
Nyní si rozeberme proces úpravy úrovně komprese v sešitu do zvládnutelných kroků.
## Krok 1: Definujte zdrojové a výstupní adresáře
Nejprve musíte určit, kde jsou umístěny vaše zdrojové soubory a kam chcete uložit výstupní soubory. To je zásadní pro zajištění toho, aby váš program věděl, kde najít soubory, se kterými potřebuje pracovat.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou k vašim adresářům. To pomůže programu najít soubory, které chcete komprimovat.
## Krok 2: Načtěte sešit
Dále načtete sešit, který chcete komprimovat. Tady začíná kouzlo!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
 tomto řádku vytvoříme novou instanci`Workbook` třídy a načtěte existující soubor Excel. Ujistěte se, že název souboru odpovídá názvu, který máte ve zdrojovém adresáři.
## Krok 3: Nastavte možnosti uložení
Nyní je čas nakonfigurovat možnosti ukládání. Nastavíme typ komprese pro výstupní soubor. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 The`XlsbSaveOptions` class umožňuje určit různé možnosti při ukládání sešitu ve formátu XLSB, včetně úrovní komprese.
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
Zde nastavíme typ komprese na Level 1, uložíme sešit a poté změříme uplynulý čas. To nám dává představu, jak dlouho proces trvá.
## Krok 5: Změřte dobu komprese pro úroveň 6
Dále se podívejme, jak funguje komprese úrovně 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Tento krok je podobný předchozímu, ale změníme úroveň komprese na úroveň 6. Všimnete si, že čas se může lišit v závislosti na složitosti sešitu.
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
V tomto kroku nastavíme úroveň komprese na úroveň 9. Zde obvykle zaznamenáte nejvýraznější zmenšení velikosti souboru, ale zpracování může trvat déle.
## Krok 7: Konečný výstup
Po spuštění všech úrovní komprese můžete vydat zprávu o úspěšném dokončení procesu.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Tento jednoduchý řádek kódu potvrzuje, že váš program dokončil provádění bez jakýchkoli problémů.
## Závěr
Úprava úrovně komprese vašich sešitů pomocí Aspose.Cells for .NET je přímočarý proces, který může vést k významným výhodám, pokud jde o velikost souboru a výkon. Podle kroků uvedených v této příručce můžete snadno implementovat kompresi do svých aplikací a zlepšit efektivitu správy souborů Excel.
## FAQ
### Co je Aspose.Cells?  
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel bez potřeby aplikace Microsoft Excel.
### Jak nainstaluji Aspose.Cells?  
 Aspose.Cells si můžete stáhnout a nainstalovat z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
### Jaké úrovně komprese jsou k dispozici?  
Aspose.Cells podporuje více úrovní komprese od úrovně 1 (nejnižší komprese) po úroveň 9 (nejvyšší komprese).
### Mohu testovat Aspose.Cells zdarma?  
 Ano! Můžete získat bezplatnou zkušební verzi Aspose.Cells[zde](https://releases.aspose.com/).
### Kde najdu podporu pro Aspose.Cells?  
 V případě jakýchkoli dotazů nebo podpory můžete navštívit fórum podpory Aspose[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
