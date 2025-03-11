---
title: Vytvořit spojnicový graf
linktitle: Vytvořit spojnicový graf
second_title: Aspose.Cells .NET Excel Processing API
description: Vytvářejte úžasné spojnicové grafy pomocí Aspose.Cells pro .NET. Chcete-li efektivně vizualizovat svá data, postupujte podle našeho podrobného průvodce.
weight: 11
url: /cs/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit spojnicový graf

## Zavedení

Jste připraveni vizualizovat svá data v ohromující jasnosti? Spojnicové grafy jsou skvělým způsobem, jak zobrazit trendy v čase nebo vztah mezi dvěma proměnnými. Ať už spravujete data pro obchodní projekt nebo analyzujete osobní metriky, možnost programově vytvářet spojnicové grafy vám může ušetřit čas a umožnit větší flexibilitu. V této příručce vás provedeme každým krokem vytváření spojnicového grafu pomocí Aspose.Cells for .NET. Jste připraveni se ponořit? Začněme!

## Předpoklady

Než se vrhneme na to, jak vytvořit spojnicový graf, ujistěte se, že jste připraveni následovat:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio, protože je to jedno z nejpopulárnějších IDE pro vývoj .NET.
2.  Aspose.Cells for .NET Library: Budete potřebovat knihovnu Aspose.Cells, kterou si můžete stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programovacího jazyka C# vám pomůže lépe porozumět příkladům a úryvkům kódu.
4. .NET Framework nebo .NET Core: Základní nastavení obou frameworků, protože to bude základem pro naše aplikace.

Jakmile máte tyto předpoklady vyřešené, jste připraveni vytvořit nějaké grafy!

## Importujte balíčky

Nyní, když jsme nastavili naše prostředí, musíme importovat potřebné balíčky do našeho kódu C#. Stejně jako při shromažďování nástrojů před zahájením projektu je import balíčků nezbytný, abyste zajistili, že budete mít vše, co potřebujete.

Postup je následující:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Tento řádek importuje`Aspose.Cells` jmenný prostor, který obsahuje všechny třídy a metody, které použijeme k vytvoření našeho spojnicového grafu.

Nyní si celý proces rozdělíme do jednoduchých, stravitelných kroků. Každý krok vás provede logickým postupem vytváření spojnicového grafu pomocí Aspose.Cells for .NET.

## Krok 1: Nastavte výstupní adresář

Prvním krokem je definovat, kam chcete výstupní soubor uložit. Je to jako nastavit si pracovní prostor, než si začnete špinit ruce. 

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory";
```
 Nahradit`"Your Output Directory"`se skutečnou cestou, kam chcete uložit vygenerovaný soubor Excel.

## Krok 2: Vytvořte instanci objektu sešitu

Dále musíme vytvořit novou instanci sešitu. Přemýšlejte o sešitu jako o plátně, kde bude proudit vaše kreativita. 

```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```
Tento řádek inicializuje nový sešit, který bude obsahovat všechna vaše data a vizuály.

## Krok 3: Otevřete sešit

V našem nově vytvořeném sešitu potřebujeme získat odkaz na list, do kterého budeme vkládat naše data. Pokud je pracovní sešit naším plátnem, pak je pracovní list naší paletou.

```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[0];
```
 Zde se dostaneme k prvnímu listu (index`0`).

## Krok 4: Přidejte vzorové hodnoty do buněk

Nyní přichází ta zábavná část! Do našeho pracovního listu vložíme několik vzorových hodnot. Tato data budou sloužit jako základ pro náš spojnicový graf. 

```csharp
// Přidání vzorových hodnot do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
V tomto úryvku přidáváme hodnoty do buněk ve sloupcích A a B. Sloupec A představuje hodnoty osy X, zatímco sloupec B představuje hodnoty osy Y.

## Krok 5: Přidejte do listu spojnicový graf

Dále zavedeme náš spojnicový graf do listu. Zde vaše data skutečně ožijí!

```csharp
// Přidání grafu do listu
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Zde přidáme spojnicový graf na zadané místo. Parametry (5, 0, 25, 10) definují polohu a velikost grafu v rámci listu.

## Krok 6: Otevřete novou instanci grafu

Jakmile jsme přidali náš graf, je čas dostat do rukou nově vytvořený objekt grafu. 

```csharp
// Přístup k instanci nově přidaného grafu
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Tento kód nás spojuje s grafem, abychom s ním mohli dále manipulovat.

## Krok 7: Přidejte SeriesCollection do grafu

Nyní musíme našemu grafu říci, jaká data má zobrazit. Zde definujeme zdroj dat pro náš spojnicový graf přidáním SeriesCollection.

```csharp
// Přidání SeriesCollection (zdroj dat grafu) do grafu v rozsahu od buňky "A1" po "B3"
chart.NSeries.Add("A1:B3", true);
```
V tomto příkladu říkáme grafu, aby použil hodnoty v buňkách A1 až B3.

## Krok 8: Uložte soubor Excel

Velké finále! Po vší vaší tvrdé práci je čas uložit soubor Excel a podívat se na váš spojnicový graf v akci.

```csharp
// Uložení souboru Excel
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Tento řádek uloží váš sešit do zadaného výstupního adresáře s názvem`outputHowToCreateLineChart.xlsx`.

## Krok 9: Proveďte a ověřte

Konečně můžete nyní spustit svůj kód a ověřit, že čárový graf byl úspěšně vytvořen ve vašem výstupním adresáři! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Tím se na konzoli zobrazí zpráva, která vám dá vědět, že vše proběhlo hladce.

## Závěr

Vytvoření spojnicového grafu pomocí Aspose.Cells for .NET je efektivní způsob, jak přivést svá data k životu. Podle tohoto podrobného průvodce můžete snadno vizualizovat trendy a vztahy ve vašich datových sadách. Ať už jste zkušený vývojář nebo teprve začínáte, Aspose.Cells vám poskytuje flexibilitu a výkon pro automatizaci vašich úloh vizualizace dat. 

## FAQ

### Co je Aspose.Cells pro .NET?  
Aspose.Cells for .NET je výkonná knihovna navržená pro programovou správu a manipulaci se soubory Excel, která umožňuje vývojářům vytvářet, upravovat a převádět tabulky.

### Podporuje Aspose.Cells grafy?  
Ano, Aspose.Cells poskytuje rozsáhlou podporu pro různé typy grafů, včetně spojnicových grafů, koláčových grafů, sloupcových grafů a dalších.

### Mohu používat Aspose.Cells zdarma?  
Ano, můžete si stáhnout bezplatnou zkušební verzi a prozkoumat její funkce. Pro dlouhodobé používání zvažte zakoupení licence.

### Existuje nějaké fórum pro podporu?  
 Absolutně! Odpovědi a dotazy můžete najít na[Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).

### Jak si koupím licenci?  
 Licence lze snadno zakoupit prostřednictvím[nákupní stránku](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
