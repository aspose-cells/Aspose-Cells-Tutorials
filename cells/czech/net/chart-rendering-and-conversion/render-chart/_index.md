---
"description": "Objevte, jak vykreslovat grafy v .NET pomocí Aspose.Cells. Postupujte podle našeho podrobného návodu a bez námahy vytvořte úžasné vizuály."
"linktitle": "Vykreslení grafu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vykreslení grafu"
"url": "/cs/net/chart-rendering-and-conversion/render-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vykreslení grafu

## Zavedení

Grafy jsou základním prvkem v prezentaci a analýze dat, díky čemuž jsou složité informace snadno stravitelné. Pokud pracujete s .NET a potřebujete programově generovat grafy, Aspose.Cells je výkonná knihovna, která poskytuje intuitivní a pokročilé funkce pro práci s excelovými soubory a grafy. V této příručce si projdeme procesem vykreslování grafu pomocí Aspose.Cells pro .NET. Připravte se na ponoření do tohoto podrobného tutoriálu, který je navržen tak, aby byl poutavý a snadno sledovatelný!

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše připravené. Zde je to, co budete potřebovat:

1. Prostředí .NET: Ujistěte se, že máte nastavené vývojové prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné IDE, které podporuje .NET.
2. Aspose.Cells pro .NET: Musíte mít nainstalovanou knihovnu Aspose.Cells. Můžete si ji stáhnout z [Stránka s vydáním Aspose](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům, ale pokud jste nováček, nebojte se – tato příručka vám vše krok za krokem vysvětlí!

## Importovat balíčky

Prvním krokem ve vaší kódovací cestě je import potřebných balíčků. Otevřete projekt v IDE a přidejte následující jmenný prostor:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Tyto jmenné prostory vám poskytnou přístup k funkcím nabízeným knihovnou Aspose.Cells, což vám umožní bezproblémově vytvářet a manipulovat s grafy.


Nyní, když jsme si probrali předpoklady a importy, pojďme se ponořit do detailů vykreslování grafu! Rozdělíme si to do jasných a snadno zvládnutelných kroků.

## Krok 1: Nastavení výstupního adresáře

Než vytvoříme sešit a graf, musíme si určit, kam budou naše výstupy uloženy. Takto budete po vygenerování grafu přesně vědět, kde je najít.

```csharp
string outputDir = "Your Output Directory"; // Zde zadejte výstupní adresář.
```

Nezapomeňte nahradit „Váš výstupní adresář“ cestou, kam chcete ukládat obrázky grafů.

## Krok 2: Vytvořte sešit

Dále si vytvoříme nový sešit. Tady se začne dít všechna ta magie!

```csharp
Workbook workbook = new Workbook();
```

Tento řádek vytvoří novou instanci třídy `Workbook` třída, která nám umožňuje pracovat s listy a grafy.

## Krok 3: Přidání nového pracovního listu

Nyní, když máme sešit, je čas přidat nový pracovní list. Představte si pracovní listy jako různé stránky v poznámkovém bloku, kde si můžete uspořádat data.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Zde přidáme nový pracovní list a získáme na něj odkaz. S tímto pracovním listem budete pracovat pro zadávání dat a grafů.

## Krok 4: Zadání vzorových hodnot

Po vytvoření pracovního listu přidejme do buněk vzorová data. Na těchto datech bude váš graf založen, proto vyberte hodnoty, které odpovídají vašemu typu grafu!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

V tomto úryvku kódu naplníme buňky „A1“ až „A3“ číselnými hodnotami a buňky „B1“ až „B3“ jinou sadou hodnot. Neváhejte si tato čísla přizpůsobit svým potřebám!

## Krok 5: Vytvořte graf

Nyní je čas vytvořit graf. Přidáme sloupcový graf, který se skvěle hodí pro porovnávání hodnot.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Zde přidáváme graf na zadané místo definováním jeho rozvržení: první sada čísel představuje pozici grafu v mřížce.

## Krok 6: Přidání datových řad do grafu

Po vytvoření grafu jej nyní musíme propojit s daty, která jsme zadali v předchozích krocích.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Tato čára spojuje datovou řadu grafu s hodnotami v buňkách „A1“ až „B3“. To znamená, že váš graf bude vizuálně znázorňovat data tak, jak bylo zamýšleno.

## Krok 7: Uložte graf jako obrázek

Nyní převeďme náš graf do obrazového formátu, aby se dal snadno sdílet a prohlížet.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

V tomto kroku uložíme graf jako obrázek EMF (Enhanced Metafile) do zadaného výstupního adresáře. Můžete jej také uložit v různých formátech, jako je BMP nebo PNG.

## Krok 8: Převod grafu na bitmapový obrázek

Pokud dáváte přednost práci s bitmapami, zde je návod, jak převést graf do bitmapového formátu.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Tím se váš graf uloží jako obrázek BMP. Nezapomeňte, že soubory BMP bývají větší, ale mají neuvěřitelně vysokou kvalitu!

## Krok 9: Renderování s pokročilými možnostmi

Graf můžeme také vykreslit s několika pokročilými možnostmi obrázků pro lepší kvalitu a rozlišení. Nastavme si několik možností:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Tyto možnosti pomáhají zlepšit vizuální kvalitu generovaného obrazu, což je obzvláště užitečné pro prezentace nebo publikace.

## Krok 10: Převod grafu na obrázek s pokročilými možnostmi

Nyní graf převedeme pomocí pokročilých možností, které jsme právě nastavili.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Tím se váš graf uloží jako soubor PNG s vylepšeným nastavením kvality.

## Krok 11: Export grafu do PDF

A konečně, pokud chcete propracovaný a snadno sdílitelný dokument, můžete graf exportovat přímo do formátu PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

V tomto kroku vytvoříte PDF soubor s vaším grafem, což ho činí ideálním pro digitální zprávy nebo sdílení s kolegy.

## Závěr 

Gratulujeme! Úspěšně jste vykreslili graf pomocí knihovny Aspose.Cells pro .NET. Tato výkonná knihovna zjednodušuje vytváření a manipulaci s excelovými soubory a grafy, díky čemuž jsou vaše data mnohem přístupnější a vizuálně atraktivnější. Ať už připravujete zprávy, analýzy nebo prezentace, grafy mají významný dopad a s Aspose je můžete snadno programově vytvářet.

## Často kladené otázky

### Jaké typy grafů mohu vytvářet pomocí Aspose.Cells pro .NET?
Můžete vytvářet různé grafy, včetně sloupcových, čárových, koláčových a sloupcových grafů a dalších.

### Mohu si přizpůsobit vzhled grafů?
Ano, Aspose.Cells umožňuje rozsáhlé přizpůsobení, včetně barev, stylů a prvků grafu.

### Je k dispozici bezplatná zkušební verze?
Rozhodně! Zkušební verzi si můžete stáhnout zdarma z [zde](https://releases.aspose.com/).

### Kde mohu získat podporu pro Aspose.Cells?
Podporu a zdroje komunity najdete na [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9).

### Potřebuji licenci k používání Aspose.Cells?
Ano, pro další používání i po uplynutí zkušební doby je vyžadována licence, ale můžete požádat o dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}