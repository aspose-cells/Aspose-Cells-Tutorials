---
"description": "Naučte se, jak vytvořit koláčový graf v Excelu pomocí Aspose.Cells pro .NET s tímto podrobným návodem. Vizualizujte svá data bez námahy."
"linktitle": "Vytvořit koláčový graf"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vytvořit koláčový graf"
"url": "/cs/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit koláčový graf

## Zavedení

Vytváření grafů je nezbytné pro vizuální reprezentaci dat a koláčové grafy jsou jedním z nejoblíbenějších způsobů, jak ilustrovat, jak části tvoří celek. S Aspose.Cells pro .NET můžete snadno automatizovat generování koláčových grafů v souborech Excelu. V tomto tutoriálu se ponoříme do toho, jak vytvořit koláčový graf od nuly pomocí Aspose.Cells pro .NET, s podrobným návodem, který celý proces usnadní a zjednoduší. Ať už jste s tímto nástrojem nováčkem, nebo si chcete vylepšit své dovednosti v automatizaci Excelu, tento průvodce vám pomůže!

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte následující nastavení:

1. Knihovna Aspose.Cells pro .NET: Ujistěte se, že máte ve svém projektu nainstalovanou knihovnu Aspose.Cells. Pokud ji ještě nemáte nainstalovanou, můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET: Ujistěte se, že je váš projekt nastaven pro použití .NET Framework nebo .NET Core.
3. Základní znalost C#: Měli byste se orientovat v programování v C#, zejména v objektově orientovaném programování (OOP).

Pro pokročilé uživatele je možné použít dočasnou licenci k odemčení všech funkcí Aspose.Cells. O licenci si můžete požádat od [zde](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Pro začátek importujte potřebné jmenné prostory a balíčky potřebné pro tento tutoriál. Patří mezi ně základní I/O operace a balíček Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Krok 1: Vytvořte nový sešit

Nejprve musíme vytvořit instanci `Workbook` třída, která představuje soubor aplikace Excel. Sešit obsahuje více listů a v našem příkladu budeme pracovat se dvěma listy – jedním pro data a jedním pro koláčový graf.

```csharp
Workbook workbook = new Workbook();
```

Tím se inicializuje nový sešit aplikace Excel. Ale kam se data dávají? Pojďme se o to postarat v dalším kroku.

## Krok 2: Přidání dat do pracovního listu

Jakmile je sešit vytvořen, musíme přistupovat k prvnímu listu a pojmenovat ho. Zde zadáme data potřebná pro koláčový graf.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Nyní můžeme zadat některá data o prodeji z různých regionů:

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

Zde přidáváme dva sloupce: jeden pro regiony a druhý pro údaje o prodeji. Tato data budou znázorněna v koláčovém grafu.

## Krok 3: Přidání listu s grafem

Dále přidáme samostatný list pro uložení koláčového grafu.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Tento nový list bude obsahovat koláčový graf. Pojmenování, například „Graf“, zajistí, že uživatelé budou vědět, co mohou při otevření souboru očekávat.

## Krok 4: Vytvořte koláčový graf

Nyní je čas vytvořit samotný graf. Určíme, že chceme koláčový graf a definujeme jeho umístění na listu.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

Metoda `Add()` přijímá parametry pro typ grafu (v tomto případě `ChartType.Pie`) a jeho umístění na listu. Čísla představují pozice řádků a sloupců.

## Krok 5: Přizpůsobení vzhledu grafu

Výsečový graf by nebyl úplný bez úprav! Vylepšeme si graf vizuálně atraktivně úpravou barev, popisků a názvu.

### Nastavit název grafu
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Přizpůsobit oblast grafu
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Nastavíme přechodovou výplň pro oblast grafu a skryjeme okraj pro čistší vzhled.

## Krok 6: Definování dat grafu

Je čas propojit graf s našimi daty. `NSeries` Vlastnost grafu propojuje prodejní údaje a regiony s koláčovým grafem.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

První řádek určuje, že používáme data o prodeji z buněk. `B2:B8`Také grafu říkáme, aby používal názvy regionů z `A2:A8` jako popisky kategorií.

## Krok 7: Přidání popisků dat

Přidání popisků přímo k segmentům grafu může usnadnit pochopení. Zahrňme názvy regionů a hodnoty prodeje do segmentů koláčového grafu.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Krok 8: Přizpůsobení oblasti grafu a legendy

Nakonec doladíme oblast grafu a legendu. To vylepší celkovou prezentaci grafu.

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

## Krok 9: Uložení sešitu

Nakonec uložíme sešit do souboru aplikace Excel. V případě potřeby můžete zadat výstupní adresář a název souboru.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Závěr

Vytvoření koláčového grafu pomocí Aspose.Cells pro .NET je přímočarý a přizpůsobitelný proces. Dodržováním tohoto návodu můžete v několika krocích vygenerovat profesionálně vypadající graf, který poskytne cenné informace. Ať už se jedná o obchodní reporting nebo vzdělávací účely, zvládnutí tvorby grafů zlepší vaše dovednosti v oblasti automatizace v Excelu. Nezapomeňte, že Aspose.Cells poskytuje flexibilitu, kterou potřebujete k snadnému vytváření úžasných datově orientovaných souborů Excelu.

## Často kladené otázky

### Mohu pomocí Aspose.Cells pro .NET vytvářet i jiné typy grafů?
Ano! Aspose.Cells podporuje různé typy grafů, včetně sloupcových grafů, spojnicových grafů a bodových grafů.

### Potřebuji placenou licenci k používání Aspose.Cells pro .NET?
Bezplatnou verzi můžete používat s určitými omezeními. Pro plné funkce budete potřebovat licenci, kterou si můžete zakoupit. [zde](https://purchase.aspose.com/buy).

### Mohu exportovat graf do formátů jako PDF nebo obrázky?
Rozhodně! Aspose.Cells umožňuje exportovat grafy do různých formátů, včetně PDF a PNG.

### Je možné každý kousek koláče ozdobit různými barvami?
Ano, na každý řez můžete použít různé barvy nastavením `IsColorVaried` majetek `true`, jak je znázorněno v tutoriálu.

### Mohu automatizovat generování více grafů v jednom sešitu?
Ano, v jednom souboru aplikace Excel můžete vytvořit a upravit libovolný počet grafů.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}