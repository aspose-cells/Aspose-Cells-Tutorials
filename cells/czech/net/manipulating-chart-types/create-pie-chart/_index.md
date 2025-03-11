---
title: Vytvořte koláčový graf
linktitle: Vytvořte koláčový graf
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak vytvořit výsečový graf v Excelu pomocí Aspose.Cells for .NET, pomocí tohoto podrobného průvodce. Vizualizujte svá data bez námahy.
weight: 12
url: /cs/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte koláčový graf

## Zavedení

Vytváření grafů je nezbytné pro vizuální reprezentaci dat a koláčové grafy jsou jedním z nejoblíbenějších způsobů, jak ilustrovat, jak části tvoří celek. S Aspose.Cells for .NET můžete snadno automatizovat generování koláčových grafů v souborech aplikace Excel. V tomto tutoriálu se ponoříme do toho, jak vytvořit výsečový graf od začátku pomocí Aspose.Cells pro .NET, s podrobným průvodcem, aby byl proces hladký a přímočarý. Ať už s tímto nástrojem začínáte, nebo chcete zlepšit své dovednosti v automatizaci Excelu, tato příručka vás pokryje!

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte následující nastavení:

1.  Aspose.Cells for .NET Library: Ujistěte se, že máte ve svém projektu nainstalovaný Aspose.Cells. Pokud jste jej ještě nenainstalovali, můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Ujistěte se, že je váš projekt nastaven tak, aby používal rozhraní .NET Framework nebo .NET Core.
3. Základní znalost C#: Měli byste být spokojeni s programováním v C#, zejména objektově orientované programování (OOP).

 Pro pokročilé uživatele lze použít dočasnou licenci k odemknutí všech funkcí Aspose.Cells. Můžete o něj požádat[zde](https://purchase.aspose.com/temporary-license/).

## Importujte balíčky

Chcete-li začít, importujte potřebné obory názvů a balíčky požadované pro tento výukový program. Patří mezi ně základní I/O operace a balíček Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Krok 1: Vytvořte nový sešit

 Nejprve musíme vytvořit instanci`Workbook` třídy, která představuje soubor Excel. Sešit obsahuje více listů a v našem příkladu budeme pracovat se dvěma listy – jedním pro data a jedním pro výsečový graf.

```csharp
Workbook workbook = new Workbook();
```

Tím se inicializuje nový sešit aplikace Excel. Ale kam jdou data? Postarejme se o to v dalším kroku.

## Krok 2: Přidejte data do listu

Jakmile je sešit vytvořen, musíme získat přístup k prvnímu listu a pojmenovat jej. Zde zadáme data požadovaná pro koláčový graf.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Nyní můžeme vložit nějaké fiktivní údaje o prodeji představující různé regiony:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Zde přidáváme dva sloupce: jeden pro regiony a druhý pro údaje o prodeji. Tato data budou reprezentována v koláčovém grafu.

## Krok 3: Přidejte list s grafem

Dále přidáme samostatný list, do kterého bude výsečový graf uložen.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Tento nový list bude hostit výsečový graf. Pojmenování, jako je „Chart“, zajistí, že uživatelé budou vědět, co mohou při otevření souboru očekávat.

## Krok 4: Vytvořte výsečový graf

Nyní je čas vytvořit skutečný graf. Zadáme, že chceme výsečový graf, a definujeme jeho pozici na listu.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Metoda`Add()`přijímá parametry pro typ grafu (v tomto případě`ChartType.Pie`) a jeho umístění na listu. Čísla představují pozice řádků a sloupců.

## Krok 5: Přizpůsobte vzhled grafu

Koláčový graf by nebyl úplný bez určitého přizpůsobení! Udělejme náš graf vizuálně přitažlivým tím, že vyladíme barvy, štítky a název.

### Nastavte název grafu
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Přizpůsobit oblast pozemku
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Nastavíme přechodovou výplň pro oblast vykreslování a skryjeme ohraničení pro čistší vzhled.

## Krok 6: Definujte data grafu

 Je čas propojit graf s našimi daty. The`NSeries` Vlastnost grafu spojuje údaje o prodeji a regiony s výsečovým grafem.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 První řádek určuje, že používáme údaje o prodeji z buněk`B2:B8` . Také říkáme grafu, aby používal názvy regionů`A2:A8` jako štítky kategorií.

## Krok 7: Přidejte štítky dat

Přidání štítků přímo do segmentů grafu může usnadnit pochopení. Zahrneme názvy regionů a hodnoty prodeje do výsečí výsečového grafu.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Krok 8: Přizpůsobte oblast grafu a legendu

Na závěr ještě dolaďme oblast grafu a legendu. To zlepšuje celkovou prezentaci grafu.

### Oblast grafu
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Krok 9: Uložte sešit

Nakonec sešit uložíme do souboru Excel. Podle potřeby můžete zadat výstupní adresář a název souboru.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Závěr

Vytvoření koláčového grafu pomocí Aspose.Cells for .NET je jednoduchý a přizpůsobitelný proces. Podle tohoto průvodce můžete vytvořit profesionálně vyhlížející graf, který v několika krocích zprostředkuje cenné poznatky. Ať už pro obchodní výkaznictví nebo vzdělávací účely, zvládnutí tvorby grafů zvýší vaše dovednosti v automatizaci Excelu. Pamatujte, že Aspose.Cells poskytuje flexibilitu, kterou potřebujete k snadnému vytváření úžasných souborů Excel založených na datech.

## FAQ

### Mohu pomocí Aspose.Cells pro .NET vytvářet jiné typy grafů?
Ano! Aspose.Cells podporuje různé typy grafů, včetně sloupcových grafů, spojnicových grafů a bodových grafů.

### Potřebuji k používání Aspose.Cells pro .NET placenou licenci?
Bezplatnou verzi můžete používat s určitými omezeními. Pro plné funkce budete potřebovat licenci, kterou si můžete zakoupit[zde](https://purchase.aspose.com/buy).

### Mohu exportovat graf do formátů, jako je PDF nebo obrázky?
Absolutně! Aspose.Cells umožňuje exportovat grafy do různých formátů, včetně PDF a PNG.

### Je možné upravit každý plátek koláče různými barvami?
 Ano, na každý řez můžete použít různé barvy nastavením`IsColorVaried` majetek do`true`, jak je uvedeno v tutoriálu.

### Mohu automatizovat generování více grafů v jednom sešitu?
Ano, můžete vytvořit a přizpůsobit tolik grafů, kolik potřebujete, v rámci jednoho souboru aplikace Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
