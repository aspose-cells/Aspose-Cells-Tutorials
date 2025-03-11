---
title: Vykreslit graf
linktitle: Vykreslit graf
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte, jak vykreslovat grafy v .NET pomocí Aspose.Cells. Postupujte podle našeho podrobného návodu a bez námahy vytvořte úžasné vizuály.
weight: 10
url: /cs/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vykreslit graf

## Zavedení

Grafy jsou základním prvkem prezentace a analýzy dat, díky čemuž jsou složité informace snadno stravitelné. Pokud pracujete s .NET a potřebujete generovat grafy programově, Aspose.Cells je výkonná knihovna, která poskytuje intuitivní a pokročilé funkce pro práci se soubory a grafy aplikace Excel. V této příručce projdeme procesem vykreslování grafu pomocí Aspose.Cells for .NET. Připravte se na ponoření do tohoto podrobného návodu, který je navržen tak, aby byl poutavý a snadno sledovatelný!

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše připraveno. Zde je to, co potřebujete:

1. Prostředí .NET: Ujistěte se, že máte nastavené vývojové prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné IDE, které podporuje .NET.
2.  Aspose.Cells for .NET: Musíte mít nainstalovanou knihovnu Aspose.Cells. Můžete si jej stáhnout z[Stránka vydání Aspose](https://releases.aspose.com/cells/net/).
3. Základní znalosti C#: Znalost programování v C# vám pomůže lépe porozumět příkladům, ale nebojte se, pokud jste noví – tato příručka vysvětlí vše krok za krokem!

## Importujte balíčky

Prvním krokem na vaší cestě kódování je import potřebných balíčků. Otevřete svůj projekt ve svém IDE a přidejte následující jmenný prostor:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Tyto jmenné prostory vám poskytnou přístup k funkcím nabízeným knihovnou Aspose.Cells, což vám umožní bezproblémově vytvářet a manipulovat s grafy.


Nyní, když jsme pokryli předpoklady a importy, pojďme se ponořit do hrubšího vykreslení grafu! Rozdělíme to do jasných, zvládnutelných kroků.

## Krok 1: Nastavte svůj výstupní adresář

Než vytvoříme náš sešit a graf, musíme určit, kam budou naše výstupy uloženy. Tímto způsobem, když je náš graf vygenerován, budete přesně vědět, kde jej najít.

```csharp
string outputDir = "Your Output Directory"; // Zde zadejte výstupní adresář.
```

Nezapomeňte nahradit "Váš výstupní adresář" cestou, kam chcete uložit obrázky grafu.

## Krok 2: Vytvořte sešit

Dále vytvoříme nový sešit. Tady se odehrává všechna ta kouzla!

```csharp
Workbook workbook = new Workbook();
```

 Tento řádek vytvoří novou instanci souboru`Workbook` třídy, která nám umožňuje pracovat s listy a grafy.

## Krok 3: Přidejte nový list

Nyní, když máme náš sešit, je čas přidat nový list. Představte si pracovní listy jako různé stránky v poznámkovém bloku, kde můžete mít svá data uspořádaná.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Zde přidáme nový pracovní list a získáme na něj odkaz. S tímto listem budete pracovat při zadávání dat a grafů.

## Krok 4: Zadejte vzorové hodnoty

S vytvořeným pracovním listem přidejte do buněk nějaká ukázková data. Na těchto datech bude váš graf založen, takže vyberte hodnoty, které dávají smysl vašemu typu grafu!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

tomto úryvku vyplňujeme buňky „A1“ až „A3“ některými číselnými hodnotami a buňky „B1“ až „B3“ jinou sadou hodnot. Neváhejte a upravte tato čísla tak, aby vyhovovala vašim potřebám!

## Krok 5: Vytvořte graf

Nyní je čas vytvořit graf. Přidáme typ sloupcového grafu, který je skvělý pro porovnávání hodnot.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Zde přidáváme graf do určeného umístění definováním jeho rozložení: první sada čísel představuje pozici grafu na mřížce.

## Krok 6: Přidání datových řad do grafu

Po vytvoření grafu jej nyní musíme svázat s daty, která jsme zadali v předchozích krocích.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Tento řádek spojuje datovou řadu grafu s hodnotami v buňkách "A1" až "B3". To znamená, že váš graf bude vizuálně reprezentovat data tak, jak bylo zamýšleno.

## Krok 7: Uložte graf jako obrázek

Nyní převedeme náš graf do obrazového formátu, aby jej bylo možné snadno sdílet a prohlížet.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

tomto kroku uložíme graf jako obrázek EMF (Enhanced Metafile) do zadaného výstupního adresáře. Můžete jej také uložit v různých formátech, jako je BMP nebo PNG.

## Krok 8: Převeďte graf na bitmapu

Pokud dáváte přednost práci s bitmapami, zde je návod, jak převést graf do bitmapového formátu.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Tím se váš graf uloží jako obrázek BMP. Pamatujte, že soubory BMP bývají větší, ale jsou neuvěřitelně kvalitní!

## Krok 9: Vykreslování s pokročilými možnostmi

Můžeme také vykreslit graf s některými pokročilými možnostmi obrázků pro lepší kvalitu a rozlišení. Nastavíme několik možností:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Tyto možnosti pomáhají zlepšit vizuální kvalitu obrazu, který generujete, zvláště užitečné pro prezentace nebo publikace.

## Krok 10: Převeďte graf na obrázek s pokročilými možnostmi

Nyní převedeme graf pomocí pokročilých možností, které jsme právě nastavili.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Tím se graf uloží jako soubor PNG s vylepšeným nastavením kvality.

## Krok 11: Export grafu do PDF

konečně, pokud chcete vyleštěný, snadno sdílený dokument, můžete svůj graf exportovat přímo do formátu PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Tento krok vytvoří PDF, které obsahuje váš graf, takže je ideální pro digitální zprávy nebo sdílení s kolegy.

## Závěr 

Gratuluji! Úspěšně jste vykreslili graf pomocí Aspose.Cells for .NET. Tato výkonná knihovna zjednodušuje vytváření a manipulaci se soubory a grafy aplikace Excel, díky čemuž jsou vaše data mnohem dostupnější a vizuálně přitažlivější. Ať už připravujete zprávy, analýzy nebo prezentace, grafy mají významný dopad a s Aspose je můžete snadno vytvářet programově.

## FAQ

### Jaké typy grafů mohu vytvořit pomocí Aspose.Cells pro .NET?
Můžete vytvářet různé grafy, včetně sloupcových, spojnicových, výsečových a sloupcových grafů.

### Mohu přizpůsobit vzhled grafů?
Ano, Aspose.Cells umožňuje rozsáhlé přizpůsobení, včetně barev, stylů a prvků grafu.

### Je k dispozici bezplatná zkušební verze?
Absolutně! Můžete si stáhnout bezplatnou zkušební verzi z[zde](https://releases.aspose.com/).

### Kde mohu získat podporu pro Aspose.Cells?
 Podporu komunity a zdroje najdete na[Aspose Support Forum](https://forum.aspose.com/c/cells/9).

### Potřebuji licenci k používání Aspose.Cells?
 Ano, pro další používání po zkušební době je vyžadována licence, ale můžete požádat o dočasnou licenci[zde](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
