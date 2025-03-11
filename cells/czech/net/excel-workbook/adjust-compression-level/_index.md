---
title: Upravte úroveň komprese
linktitle: Upravte úroveň komprese
second_title: Aspose.Cells for .NET API Reference
description: Naučte se, jak upravit úrovně komprese pro soubory Excel pomocí Aspose.Cells for .NET. Pomocí tohoto podrobného průvodce efektivně optimalizujte velikost souborů.
weight: 50
url: /cs/net/excel-workbook/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Upravte úroveň komprese

## Zavedení

Pokud jde o manipulaci s velkými soubory aplikace Excel, efektivní úložiště je klíčové. Ať už jste vývojář, který hledá optimalizaci velikosti souborů, nebo datový analytik, který chce urychlit přenos souborů, pochopení toho, jak upravit úrovně komprese v Aspose.Cells pro .NET, může změnit hru. V této příručce vás provedeme kroky k úpravě úrovní komprese při ukládání souborů aplikace Excel, čímž zajistíme zachování výkonu bez obětování kvality.

## Předpoklady

Než se ponoříme do těch nejhrubších úrovní komprese, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:

1. Základní znalost C#: Základní znalost programování v C# je nezbytná. Pokud jste spokojeni s proměnnými, smyčkami a základními operacemi se soubory, můžete začít!
2. Aspose.Cells for .NET Library: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout z[webové stránky](https://releases.aspose.com/cells/net/) . Pokud právě začínáte, zvažte možnost bezplatné zkušební verze[zde](https://releases.aspose.com/).
3. Vývojové prostředí: Nastavte své vývojové prostředí, ideálně Visual Studio, pro psaní a spouštění vašeho kódu C#. 
4. Ukázkový soubor Excel: Připravte si velký soubor Excel k testování. Můžete vytvořit jeden nebo použít jakýkoli existující soubor, ale ujistěte se, že je dostatečně velký, abyste viděli účinky komprese.

S těmito předpoklady můžeme začít!

## Importujte balíčky

Než budeme moci manipulovat se soubory Excelu, musíme importovat potřebné jmenné prostory. Toto je zásadní krok, který nám umožňuje přístup ke třídám a metodám poskytovaným Aspose.Cells.

### Importujte jmenný prostor Aspose.Cells

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

 Tento fragment kódu importuje soubor`Aspose.Cells` jmenný prostor, který obsahuje všechny třídy potřebné pro práci se soubory Excel. The`Aspose.Cells.Xlsb` jmenný prostor je speciálně pro zpracování formátů souborů XLSB.

Nyní, když máme vše nastaveno, rozdělíme proces úpravy úrovní komprese do zvládnutelných kroků. Uložíme sešit s různými úrovněmi komprese a změříme čas potřebný pro každou operaci. 

## Krok 1: Nastavte své adresáře

Nejprve musíme definovat, kde budou naše soubory uloženy. To zahrnuje specifikaci zdrojového adresáře pro náš vstupní soubor a výstupního adresáře pro naše komprimované soubory.

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## Krok 2: Načtěte sešit

Dále načteme excelový sešit, který chceme komprimovat. Zde ukážete na svůj velký soubor Excel.

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

 Tento řádek inicializuje nový`Workbook` objekt se zadaným souborem. Ujistěte se, že cesta k souboru je správná; jinak narazíte na chyby.

## Krok 3: Vytvořte možnosti uložení pro XLSB

 Nyní vytvoříme instanci`XlsbSaveOptions`, což nám umožňuje určit, jak chceme náš sešit uložit, včetně úrovně komprese.

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

Tento řádek připravuje možnosti, které použijeme pro uložení našeho sešitu ve formátu XLSB.

## Krok 4: Nastavte a změřte úrovně komprese

Nyní přichází ta zábavná část! Sešit uložíme pomocí různých úrovní komprese a změříme čas potřebný pro každou operaci. 

### Komprese úrovně 1

Začněme s nejnižší úrovní komprese:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

V tomto úryvku nastavíme typ komprese na úroveň 1, uložíme sešit a zaprotokolujeme čas. 

### Komprese úrovně 6

Dále vyzkoušíme střední úroveň komprese:

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

Tentokrát nastavíme typ komprese na úroveň 6 a zopakujeme operaci uložení.

### Komprese úrovně 9

Nakonec uložme pomocí nejvyšší úrovně komprese:

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

V tomto kroku nastavíme typ komprese na úroveň 9, což by mělo poskytnout nejmenší velikost souboru, ale uložení může trvat déle.

## Krok 5: Konečný výstup

Po provedení všech výše uvedených kroků uvidíte na konzole vytištěné uplynulé časy pro každou úroveň komprese. 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

Tento řádek potvrzuje, že celý proces proběhl bez problémů.

## Závěr

Úprava úrovní komprese při ukládání souborů aplikace Excel pomocí Aspose.Cells for .NET je přímočará, ale výkonná technika. Podle kroků uvedených v této příručce můžete snadno manipulovat s velikostí souborů a usnadnit jejich správu pro ukládání a přenos. Ať už potřebujete rychlý přístup k datům nebo hledáte optimalizaci výkonu své aplikace, zvládnutí těchto technik nepochybně zlepší vaše vývojářské dovednosti.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory Excelu programově.

### Jak stáhnu Aspose.Cells?
 Knihovnu Aspose.Cells si můžete stáhnout z[webové stránky](https://releases.aspose.com/cells/net/).

### Mohu používat Aspose.Cells zdarma?
 Ano, Aspose nabízí bezplatnou zkušební verzi, ke které máte přístup[zde](https://releases.aspose.com/).

### Jaké jsou dostupné různé úrovně komprese?
Aspose.Cells podporuje více úrovní komprese od úrovně 1 (nejmenší komprese) po úroveň 9 (maximální komprese).

### Kde najdu podporu pro Aspose.Cells?
 Můžete získat podporu a klást otázky na[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
