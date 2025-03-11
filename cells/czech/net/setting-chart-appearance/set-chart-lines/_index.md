---
title: Nastavit čáry grafu
linktitle: Nastavit čáry grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přizpůsobit čáry grafu v Excelu pomocí Aspose.Cells for .NET, pomocí našeho podrobného průvodce krok za krokem.
weight: 14
url: /cs/net/setting-chart-appearance/set-chart-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit čáry grafu

## Zavedení

Vytváření vizuálně přitažlivých a informativních grafů je pro reprezentaci dat zásadní. Ať už jste datový analytik, obchodní manažer nebo jen někdo, kdo miluje organizování dat, grafy mohou výrazně zlepšit způsob, jakým prezentujete své informace. Tento tutoriál vás provede procesem nastavení čar grafu pomocí Aspose.Cells for .NET, výkonné knihovny pro manipulaci se soubory aplikace Excel. Na konci budete vědět, jak vytvořit úžasné grafy plné přizpůsobení, aby se vaše data v Excelu objevila!

## Předpoklady

Než se ponoříte do kódovací části, ujistěte se, že jste vybaveni následujícím:

- Visual Studio: Ujistěte se, že máte nainstalované Visual Studio. Důrazně se doporučuje používat nejnovější verzi, abyste mohli využít všechny funkce.
- .NET Framework: Váš projekt by měl být založen na .NET Framework (nebo .NET Core), kde budete implementovat Aspose.Cells.
-  Aspose.Cells for .NET: Stáhněte a nainstalujte Aspose.Cells z[Aspose webové stránky](https://releases.aspose.com/cells/net/).
- Základní porozumění C#: Při kódování bude užitečná znalost programovacího jazyka C#.

## Importujte balíčky

Chcete-li začít s Aspose.Cells, budete muset do svého projektu importovat potřebné jmenné prostory. To vám umožní přístup ke všem skvělým funkcím a funkcím, které Aspose.Cells nabízí. Zde je návod, jak importovat balíčky do souboru C#:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Pojďme si tento proces rozdělit do zvládnutelných kroků, abyste jej mohli snadno sledovat.

## Krok 1: Definujte svůj výstupní adresář

Nejprve budete potřebovat místo pro uložení nově vytvořeného souboru Excel. Definujte výstupní adresář v horní části kódu takto:

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory";
```

 Vysvětlení: Nahraďte "Your Output Directory" cestou, kam chcete, aby Aspose.Cells soubor uložil, jako např.`C:\\MyExcelFiles\\`.

## Krok 2: Vytvořte instanci objektu sešitu

Nyní vytvoříme objekt sešitu, který slouží jako kontejner pro vaši tabulku.

```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```

 Vysvětlení: Tento řádek vytváří instanci souboru`Workbook`třídy z knihovny Aspose.Cells. Je to jako otevřít nový prázdný soubor Excel, do kterého můžete začít přidávat své listy a data.

## Krok 3: Odkaz na pracovní list

Dále budete muset pracovat s konkrétním listem v sešitu. Vezmeme si první pracovní list.

```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[0];
```

 Vysvětlení: Listy jsou indexovány od 0, takže`worksheets[0]` odkazuje na první pracovní list.

## Krok 4: Přidejte vzorové hodnoty do buněk

Vyplňte některé buňky daty, které později použijeme k vytvoření našeho grafu.

```csharp
// Přidání vzorových hodnot do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Vysvětlení: Zde vyplníme buňky "A1" až "A3" a "B1" až "B3" nějakými číselnými hodnotami. Ty budou zakresleny do našeho grafu později.

## Krok 5: Přidejte graf do listu

Nyní je čas vytvořit graf! Přidáme typ sloupcového grafu.

```csharp
// Přidání grafu do listu
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

Vysvětlení: Tento řádek přidá sloupcový graf na určitých souřadnicích na listu. Parametry definují, kde bude graf na mřížce vykreslen.

## Krok 6: Otevřete nově přidaný graf

Nyní musíte odkazovat na graf, který jste právě vytvořili.

```csharp
// Přístup k instanci nově přidaného grafu
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Vysvětlení: To vám dává kontrolu nad instancí grafu a umožňuje vám ji dále upravovat a stylovat.

## Krok 7: Přidejte datové řady do grafu

Přidejme datové řady pro náš graf.

```csharp
// Přidání SeriesCollection (zdroj dat grafu) do grafu v rozsahu od buňky "A1" po "B3"
chart.NSeries.Add("A1:B3", true);
```

Vysvětlení: Tento řádek dává grafu pokyn, aby vytáhl data ze zadaného rozsahu. Druhý parametr určuje, zda rozsahy dat zahrnují kategorie.

## Krok 8: Přizpůsobte vzhled grafu

Nyní k té zábavnější části – přizpůsobení grafu! Pojďme změnit některé barvy.

```csharp
// Nastavení barvy popředí oblasti vykreslování
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Nastavení barvy popředí oblasti grafu
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Nastavení barvy popředí oblasti kolekce 1. série
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Nastavení barvy popředí oblasti bodu kolekce 1. série
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Vyplnění oblasti kolekce 2. série přechodem
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

Vysvětlení: Zde upravujete barvy různých součástí grafu tak, aby byl vizuálně výrazný. Každý řádek cílí na jiné oblasti grafu.

## Krok 9: Použijte styly čar

Dále můžete upravit styly čar pro datové řady, aby byl graf nejen pěkný, ale také profesionální.

```csharp
// Použití stylu tečkované čáry na čáry kolekce SeriesCollection
chart.NSeries[0].Border.Style = Aspose.Cells.Drawing.LineType.Dot;

// Použití stylu trojúhelníkových značek na datové značky kolekce SeriesCollection
chart.NSeries[0].Marker.MarkerStyle = Aspose.Cells.Charts.ChartMarkerType.Triangle;

// Nastavení váhy všech čar v SeriesCollection na střední
chart.NSeries[1].Border.Weight = Aspose.Cells.Drawing.WeightType.MediumLine;
```

Vysvětlení: Výše uvedený kód přizpůsobuje okraje řad grafu, dává jim tečkovanou čáru a dokonce mění značky datových bodů na trojúhelníky. Je to všechno o tom osobním kontaktu!

## Krok 10: Uložte sešit

Nyní uložme vaši tvrdou práci do souboru aplikace Excel.

```csharp
// Uložení souboru Excel
workbook.Save(outputDir + "outputSettingChartLines.xlsx");
```

Vysvětlení: Tento řádek uloží váš sešit se zadaným názvem do vámi definovaného výstupního adresáře. Nyní jej můžete otevřít a prohlédnout si svůj skvělý graf!

## Krok 11: Potvrzení provedení

Nakonec si pojďme potvrdit, že vše proběhlo hladce.

```csharp
Console.WriteLine("SettingChartLines executed successfully.");
```

Vysvětlení: Jednoduchá zpráva informující o tom, že váš kód byl proveden bez problémů.

## Závěr

Gratuluji! Nyní jste zvládli základy vytváření a přizpůsobení grafů pomocí Aspose.Cells pro .NET. Pomocí několika jednoduchých kroků můžete svou prezentaci dat pozvednout, učinit ji srozumitelnější a vizuálně přitažlivější. Až budete experimentovat s dalšími možnostmi přizpůsobení, pamatujte, že skvělý graf nejen vypráví příběh, ale také zaujme vaše publikum.

## FAQ

### Co je Aspose.Cells pro .NET?  
Aspose.Cells for .NET je výkonná knihovna pro manipulaci s tabulkami aplikace Excel v aplikacích .NET.

### Mohu používat Aspose.Cells zdarma?  
 Ano, Aspose poskytuje bezplatnou zkušební verzi k otestování její funkčnosti. Můžete si jej stáhnout[zde](https://releases.aspose.com/).

### Je k dispozici podpora pro Aspose.Cells?  
 Absolutně! Podporu můžete získat prostřednictvím[Fórum Aspose](https://forum.aspose.com/c/cells/9).

### Mohu pomocí Aspose.Cells vytvářet jiné typy grafů?  
Ano, Aspose podporuje různé typy grafů včetně spojnicových, koláčových a plošných grafů.

### Jak získám dočasnou licenci pro Aspose.Cells?  
 Můžete požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/) prostřednictvím webu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
