---
"description": "Naučte se, jak v Excelu vytvořit čárový graf s datovými značkami pomocí Aspose.Cells pro .NET. Postupujte podle tohoto podrobného návodu a snadno vytvářejte a upravujte grafy."
"linktitle": "Vytvořit čárový graf s datovými značkami"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vytvořit čárový graf s datovými značkami"
"url": "/cs/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit čárový graf s datovými značkami

## Zavedení

Přemýšleli jste někdy, jak programově vytvářet úžasné grafy v Excelu? Tak se do toho dejte, protože dnes se ponoříme do vytváření čárového grafu s datovými značkami pomocí Aspose.Cells pro .NET. Tento tutoriál vás provede každým krokem a zajistí, že budete mít pevné znalosti o generování grafů, i když s Aspose.Cells teprve začínáte.

## Předpoklady

Než začneme, ujistěte se, že máte vše připravené, abyste mohli plynule pokračovat.

1. Knihovna Aspose.Cells pro .NET – Budete si ji muset nainstalovat. Můžete si ji stáhnout. [zde](https://releases.aspose.com/cells/net/).
2. .NET Framework – Ujistěte se, že vaše vývojové prostředí je nastaveno s nejnovější verzí .NET.
3. IDE (integrované vývojové prostředí) – doporučuje se Visual Studio.
4. Platná licence Aspose.Cells – Pokud ji nemáte, můžete si o ni požádat. [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo se podívejte na jejich [bezplatná zkušební verze](https://releases.aspose.com/).

Jste připraveni vyrazit? Pojďme si to rozebrat!

## Import potřebných balíčků

Pro začátek se ujistěte, že do projektu importujete následující jmenné prostory. Ty poskytnou potřebné třídy a metody pro vytvoření grafu.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Jakmile tohle zvládneš, můžeme začít s kódováním!

## Krok 1: Nastavení sešitu a pracovního listu

Nejdříve je potřeba vytvořit nový sešit a přistupovat k prvnímu listu.

```csharp
//Výstupní adresář
static string outputDir = "Your Document Directory";
		
// Vytvoření instance sešitu
Workbook workbook = new Workbook();

// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```

Představte si sešit jako váš excelový soubor a pracovní list jako konkrétní list v něm. V tomto případě pracujeme s prvním listem.

## Krok 2: Naplnění pracovního listu daty

Nyní, když máme pracovní list, naplňme ho daty. Vytváříme náhodné datové body pro dvě řady hodnot.

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

Zde používáme k simulaci dat náhodná čísla, ale v reálných aplikacích je můžete naplnit skutečnými hodnotami z vaší datové sady.

## Krok 3: Přidání grafu do pracovního listu

Dále přidáme graf do listu a vybereme typ – v tomto případě čárový graf s datovými značkami.

```csharp
// Přidání grafu do listu
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Přístup k nově vytvořenému grafu
Chart chart = worksheet.Charts[idx];
```

Tento úryvek přidá do listu spojnicový graf s datovými značkami a umístí ho do určitého rozsahu (1, 3 až 20, 20). Docela jednoduché, že?

## Krok 4: Přizpůsobte vzhled grafu

Jakmile je graf vytvořen, můžete si ho upravit podle svých představ. Změňme pozadí, název a styl grafu.

```csharp
// Nastavení stylu grafu
chart.Style = 3;

// Nastavit hodnotu automatického škálování na true
chart.AutoScaling = true;

// Nastavit barvu popředí na bílou
chart.PlotArea.Area.ForegroundColor = Color.White;

// Nastavení vlastností názvu grafu
chart.Title.Text = "Sample Chart";

// Nastavit typ grafu
chart.Type = ChartType.LineWithDataMarkers;
```

Zde grafu dodáváme čistý vzhled nastavením bílého pozadí, automatickým škálováním a smysluplným názvem.

## Krok 5: Definování řady a vykreslení datových bodů

Nyní, když náš graf vypadá dobře, musíme definovat datové řady, které budeme vykreslovat.

```csharp
// Nastavení vlastností názvu osy kategorií
chart.CategoryAxis.Title.Text = "Units";

// Definujte dvě řady pro graf
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Tyto řady odpovídají rozsahům datových bodů, které jsme dříve vyplnili.

## Krok 6: Přidání barev a úprava značek sérií

Pojďme tento graf ještě vylepšit přidáním vlastních barev k našim datovým značkám.

```csharp
// Přizpůsobit první sérii
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Přizpůsobit druhou sérii
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Úpravou barev učiníte graf nejen funkčním, ale i vizuálně poutavým!

## Krok 7: Nastavení hodnot X a Y pro každou sérii

Nakonec přiřaďme hodnoty X a Y pro každou z našich řad.

```csharp
// Nastavení hodnot X a Y první série
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Nastavení hodnot X a Y druhé série
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Hodnoty jsou založeny na datech, která jsme vyplnili v kroku 2.

## Krok 8: Uložení sešitu

Teď, když je vše nastaveno, uložme si sešit, abychom viděli graf v akci.

```csharp
// Uložit sešit
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

A to je vše! Právě jste vytvořili spojnicový graf s datovými značkami pomocí Aspose.Cells pro .NET.

## Závěr

Programové vytváření grafů v Excelu se může zdát náročné, ale s Aspose.Cells pro .NET je to stejně snadné jako postupovat podle podrobného návodu. Od nastavení sešitu až po úpravu vzhledu grafu, tato výkonná knihovna zvládne vše. Ať už vytváříte sestavy, dashboardy nebo vizualizace dat, Aspose.Cells vám to umožní udělat hračkou.

## Často kladené otázky

### Mohu si graf dále přizpůsobit?  
Rozhodně! Aspose.Cells nabízí spoustu možností přizpůsobení, od písem po mřížku a další.

### Potřebuji licenci k používání Aspose.Cells?  
Ano, pro plnou funkčnost je vyžadována licence. Můžete si ji pořídit [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo začněte s [bezplatná zkušební verze](https://releases.aspose.com/).

### Jak mohu přidat další datové řady?  
Stačí přidat další série pomocí `NSeries.Add` metodu, která určuje rozsahy buněk pro nová data.

### Mohu exportovat graf jako obrázek?  
Ano, grafy můžete exportovat přímo jako obrázky pomocí `Chart.ToImage` metoda.

### Podporuje Aspose.Cells 3D grafy?  
Ano, Aspose.Cells podporuje širokou škálu typů grafů, včetně 3D grafů.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}