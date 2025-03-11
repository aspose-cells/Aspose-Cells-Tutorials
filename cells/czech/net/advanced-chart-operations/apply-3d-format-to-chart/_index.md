---
title: Použít 3D formát na graf
linktitle: Použít 3D formát na graf
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte, jak vytvořit úžasné 3D grafy v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho jednoduchého průvodce krok za krokem.
weight: 10
url: /cs/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použít 3D formát na graf

## Zavedení

V době, kdy je vizualizace dat prvořadá, způsob, jakým prezentujeme naše data, přesahuje základní grafy a tabulky. Pomocí nástrojů, jako je Aspose.Cells for .NET, můžete pozvednout své prezentace dat pomocí ohromujících 3D grafů, které nejen upoutají pozornost, ale také efektivně předávají informace. Tento průvodce vás provede kroky k použití 3D formátu na graf pomocí Aspose.Cells a transformuje vaše nezpracovaná data na poutavé zobrazení.

## Předpoklady

Než se ponoříme do toho nejnutnějšího použití 3D formátu na graf, ujistěte se, že máte vše, co potřebujete.

### Softwarové požadavky

- Visual Studio: Ujistěte se, že máte nainstalované Visual Studio pro práci s aplikacemi .NET.
-  Aspose.Cells for .NET: Pokud jste to ještě neudělali, stáhněte si a nainstalujte Aspose.Cells z[zde](https://releases.aspose.com/cells/net/).

### Nastavení prostředí kódování

1. Vytvoření nového projektu .NET: Otevřete Visual Studio, vyberte „Vytvořit nový projekt“ a vyberte aplikaci konzoly.
2. Přidejte referenci Aspose.Cells: Prostřednictvím Správce balíčků NuGet přidejte Aspose.Cells vyhledáním nebo prostřednictvím konzoly Správce balíčků:

```bash
Install-Package Aspose.Cells
```

3. Nastavení výstupního adresáře: Určete výstupní adresář, kam se budou ukládat vygenerované soubory – to může být stejně jednoduché jako vytvoření složky na ploše.

Nyní, když jste vše nastavili, je čas skočit do kódu a vytvořit oslnivé 3D grafy!

## Importujte balíčky

Chcete-li začít, musíte importovat potřebné jmenné prostory. To vám pomůže získat přístup ke třídám a metodám poskytovaným Aspose.Cells. Postupujte takto:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Tato část rozdělí proces do zvládnutelných kroků a poskytne vám jasné pochopení každé fáze.

## Krok 1: Inicializujte svůj sešit

 Nejprve musíte vytvořit instanci souboru`Workbook` třída. Tento objekt bude sloužit jako základ pro váš dokument Excel.

```csharp
//Výstupní adresář
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Mysli na tohle`Workbook` jako prázdné plátno – připravené na to, abyste jej naplnili barevnými daty a působivými vizualizacemi.

## Krok 2: Přejmenujte první list

Dále přejmenujme první list. Díky tomu je jasné, s jakými údaji pracujeme.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Názvy by měly být intuitivní. V tomto případě to pojmenujeme „DataSheet“, abychom věděli, kde naše data žijí.

## Krok 3: Vytvořte data pro graf

Nyní do našeho "DataSheet" přidáme některá data. Vyplňte jej hodnotami, které použije náš graf.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Stejně jako recept závisí na přísadách, účinnost vašeho grafu závisí na kvalitě a organizaci vašich vstupních dat.

## Krok 4: Nastavení nového listu s grafem

Je čas vytvořit nový list pro samotný graf. To pomáhá udržet vaši vizualizaci dat organizovanou.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Považujte tento list za svou fázi – kde se odvíjí výkon vašich dat.

## Krok 5: Přidejte graf

Zde do nově vytvořeného listu přidáme sloupcový graf.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Definujeme prostor pro náš graf a určujeme, o jaký typ se jedná. Berte to jako výběr typu rámu pro vaše umělecké dílo.

## Krok 6: Přizpůsobte vzhled grafu

Nyní přizpůsobíme vzhled grafu nastavením barev pozadí. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Díky čistému bílému pozadí často vyniknou barvy vašich dat a zlepší se viditelnost.

## Krok 7: Přidejte datové řady do grafu

Je čas naplnit náš graf daty. Přidáme datovou řadu z našeho "DataSheet", abychom zajistili, že náš graf odráží data, která potřebujeme.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

To je obdoba kuchaře připravujícího pokrm ze specifických surovin. Každý datový bod je důležitý!

## Krok 8: Přístup k datové řadě a její formátování

Nyní, když máme svá data propojená, vezměme datové řady a začněme aplikovat nějaké 3D efekty.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Připravujeme se přidat do našeho pokrmu nějaký šmrnc – představte si to jako koření, které zvýrazní celkovou chuť.

## Krok 9: Použijte 3D efekty zkosení

Dále přidáme efekt zkosení, aby náš graf získal nějaký rozměr.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Stejně jako sochař tvaruje kámen, vytváříme hloubku, díky které náš graf ožívá!

## Krok 10: Přizpůsobte povrchový materiál a osvětlení

Ať náš graf jasně září! Upravíme povrchový materiál a nastavení osvětlení.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Správné osvětlení a materiál dokáže proměnit plochý objekt v podmanivý vizuál. Představte si filmový set odborně nasvícený, aby vylepšil každou scénu.

## Krok 11: Poslední úpravy vzhledu série

Nyní dokončit vzhled naší datové řady úpravou její barvy.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Správná barva může vyvolat určité pocity a reakce — kaštanová dodává nádech elegance a sofistikovanosti.

## Krok 12: Uložte sešit

Konečně je čas zachránit své mistrovské dílo! Nezapomeňte uvést místo určení, kam jej chcete uložit.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Uložení vaší práce je jako umístění vašeho umění do galerie; je to chvíle, kterou si můžete vážit a sdílet.

## Závěr

Gratuluji! Úspěšně jste vytvořili vizuálně přitažlivý 3D graf pomocí Aspose.Cells pro .NET. Dodržováním těchto kroků nyní máte k dispozici výkonný nástroj pro vylepšení vašich datových prezentací, díky nimž budou nejen informativní, ale také vizuálně podmanivé. Při vylepšování grafů pamatujte, že každá vizualizace je příběh – zajistěte, aby byla poutavá, jasná a působivá!

## FAQ

### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je výkonná knihovna, která vývojářům umožňuje programově manipulovat s dokumenty Excelu, včetně vytváření grafů a diagramů.

### Mohu přizpůsobit typy grafů v Aspose.Cells?
Ano! Aspose.Cells podporuje různé typy grafů, jako je sloupec, čára, koláč a mnoho dalších, které lze snadno přizpůsobit.

### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
 Absolutně! Bezplatnou zkušební verzi si můžete stáhnout z[zde](https://releases.aspose.com/).

### Mohu na grafy použít jiné efekty než 3D formáty?
Ano, můžete použít různé efekty, jako jsou stíny, přechody a různé styly, abyste vylepšili své grafy nad rámec 3D.

### Kde najdu podporu pro Aspose.Cells?
 Pro podporu můžete navštívit[Fórum Aspose](https://forum.aspose.com/c/cells/9) za pomoc a pomoc komunitě.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
