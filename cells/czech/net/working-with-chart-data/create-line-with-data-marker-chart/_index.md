---
title: Vytvořte řádek s grafem značek dat
linktitle: Vytvořte řádek s grafem značek dat
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak vytvořit graf Line with Data Markers v Excelu pomocí Aspose.Cells for .NET. Chcete-li snadno generovat a přizpůsobovat grafy, postupujte podle tohoto podrobného průvodce.
weight: 10
url: /cs/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte řádek s grafem značek dat

## Zavedení

Přemýšleli jste někdy o tom, jak vytvořit úžasné grafy v Excelu programově? No, připoutejte se, protože dnes se ponoříme do vytváření Line with Data Marker Chart pomocí Aspose.Cells for .NET. Tento výukový program vás provede každým krokem a zajistí, že budete mít pevný přehled o generování grafů, i když s Aspose.Cells teprve začínáte.

## Předpoklady

Než začneme, ujistěte se, že máte vše na svém místě, abyste mohli plynule pokračovat.

1. Aspose.Cells for .NET Library – budete muset nainstalovat tuto. Můžeš to chytit[zde](https://releases.aspose.com/cells/net/).
2. .NET Framework – Zajistěte, aby vaše vývojové prostředí bylo nastaveno na nejnovější verzi .NET.
3. IDE (Integrated Development Environment) – doporučuje se Visual Studio.
4.  Platná licence Aspose.Cells – Pokud ji nemáte, můžete požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/) nebo se podívejte na jejich[zkušební verze zdarma](https://releases.aspose.com/).

Jste připraveni jít? Pojďme to rozebrat!

## Import nezbytných balíčků

Nejprve se ujistěte, že jste do svého projektu importovali následující jmenné prostory. Ty poskytnou potřebné třídy a metody k vytvoření vašeho grafu.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Jakmile to pochopíte, můžeme začít kódovat!

## Krok 1: Nastavte si sešit a pracovní list

Nejprve musíte vytvořit nový sešit a otevřít první list.

```csharp
//Výstupní adresář
static string outputDir = "Your Document Directory";
		
// Vytvořte instanci sešitu
Workbook workbook = new Workbook();

// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```

Představte si sešit jako soubor aplikace Excel a list jako konkrétní list v něm. V tomto případě pracujeme s prvním listem.

## Krok 2: Naplňte list daty

Nyní, když máme svůj pracovní list, vyplníme jej některými údaji. Vytváříme náhodné datové body pro dvě řady hodnot.

```csharp
// Nastavit název sloupců
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Náhodná data pro generování grafu
Random R = new Random();

// Vytvořte náhodná data a uložte je do buněk
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Zde k simulaci dat používáme náhodná čísla, ale v reálných aplikacích je můžete naplnit skutečnými hodnotami z vaší datové sady.

## Krok 3: Přidejte graf do listu

Dále přidáme graf do listu a zvolíme typ – v tomto případě Line with Data Markers Chart.

```csharp
// Přidejte graf do listu
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Přístup k nově vytvořenému grafu
Chart chart = worksheet.Charts[idx];
```

Tento úryvek přidá do listu spojnicový graf se značkami dat a umístí jej do určitého rozsahu (1,3 až 20,20). Docela jednoduché, že?

## Krok 4: Přizpůsobte vzhled grafu

Jakmile je graf vytvořen, můžete si jej upravit podle svých představ. Pojďme změnit pozadí, nadpis a styl grafu.

```csharp
// Nastavit styl grafu
chart.Style = 3;

// Nastavte hodnotu automatického škálování na true
chart.AutoScaling = true;

// Nastavte barvu popředí na bílou
chart.PlotArea.Area.ForegroundColor = Color.White;

//Nastavte vlastnosti nadpisu grafu
chart.Title.Text = "Sample Chart";

// Nastavte typ grafu
chart.Type = ChartType.LineWithDataMarkers;
```

Zde dáváme grafu čistý vzhled nastavením bílého pozadí, automatického škálování a dáváme mu smysluplný název.

## Krok 5: Definujte sérii a vykreslete datové body

Nyní, když náš graf vypadá dobře, musíme definovat datové řady, které se budou vykreslovat.

```csharp
// Nastavte vlastnosti názvu osy kategorie
chart.CategoryAxis.Title.Text = "Units";

// Definujte dvě řady pro graf
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Tyto řady odpovídají rozsahům datových bodů, které jsme naplnili dříve.

## Krok 6: Přidejte barvy a přizpůsobte značky sérií

Udělejme tento graf ještě atraktivnějším přidáním vlastních barev do našich datových značek.

```csharp
// Přizpůsobte první sérii
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Přizpůsobte druhou sérii
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Přizpůsobením barev je graf nejen funkční, ale také vizuálně poutavý!

## Krok 7: Nastavte hodnoty X a Y pro každou sérii

Nakonec přiřaďme hodnoty X a Y pro každou naši řadu.

```csharp
// Nastavte hodnoty X a Y první série
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Nastavte hodnoty X a Y druhé řady
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Hodnoty jsou založeny na datech, která jsme naplnili v kroku 2.

## Krok 8: Uložte sešit

Nyní, když je vše nastaveno, uložíme sešit, abychom viděli graf v akci.

```csharp
// Uložte sešit
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

A je to! Právě jste vytvořili spojnicový graf s datovými značkami pomocí Aspose.Cells pro .NET.

## Závěr

Vytváření grafů programově v Excelu se může zdát skličující, ale s Aspose.Cells pro .NET je to stejně snadné, jako postupovat podle receptu krok za krokem. Od nastavení sešitu až po přizpůsobení vzhledu grafu, tato výkonná knihovna zvládne vše. Ať už vytváříte sestavy, řídicí panely nebo vizualizace dat, Aspose.Cells vám to umožní udělat snadno.

## FAQ

### Mohu graf dále upravit?  
Absolutně! Aspose.Cells nabízí spoustu možností přizpůsobení, od písem po mřížky a další.

### Potřebuji licenci k používání Aspose.Cells?  
 Ano, pro plnou funkčnost je nutná licence. Můžete získat a[dočasná licence](https://purchase.aspose.com/temporary-license/) nebo začít s a[zkušební verze zdarma](https://releases.aspose.com/).

### Jak mohu přidat další datové řady?  
 Stačí přidat další série pomocí`NSeries.Add` určující rozsahy buněk pro nová data.

### Mohu exportovat graf jako obrázek?  
 Ano, grafy můžete exportovat přímo jako obrázky pomocí`Chart.ToImage` metoda.

### Podporuje Aspose.Cells 3D grafy?  
Ano, Aspose.Cells podporuje širokou škálu typů grafů, včetně 3D grafů.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
