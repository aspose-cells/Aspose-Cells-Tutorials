---
title: Sloučit buňky v pojmenovaném rozsahu v Excelu
linktitle: Sloučit buňky v pojmenovaném rozsahu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném kurzu se dozvíte, jak sloučit buňky v pojmenovaném rozsahu pomocí Aspose.Cells for .NET. Zjistěte, jak formátovat, upravovat a automatizovat sestavy Excel.
weight: 11
url: /cs/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sloučit buňky v pojmenovaném rozsahu v Excelu

## Zavedení

Při programové práci se soubory Excelu je jedním z běžných úkolů, se kterými se můžete setkat, slučování buněk v pojmenovaném rozsahu. Ať už automatizujete generování sestav, vytváříte řídicí panely nebo jednoduše spravujete velké datové sady, slučování buněk je základní technikou. V tomto tutoriálu prozkoumáme, jak sloučit buňky v pojmenovaném rozsahu pomocí Aspose.Cells for .NET – výkonné knihovny, která umožňuje vývojářům manipulovat se soubory Excelu, aniž by museli mít nainstalován Microsoft Excel.

## Předpoklady

Než začneme, ujistěte se, že máte připraveno následující:

-  Aspose.Cells for .NET: Můžete si jej stáhnout z[Stránka vydání Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework nainstalovaný na vašem počítači.
- Základní porozumění C#: Pomůže vám znalost pojmů, jako jsou třídy, metody a objekty.

## Importujte balíčky

Než se vrhneme na kódování, musíte importovat potřebné jmenné prostory. Tyto jmenné prostory vám umožní přístup k funkcím knihovny Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

předpoklady a balíčky z cesty, pojďme se přesunout k zábavnější části: kódování!

Zde je rozpis toho, jak můžete sloučit buňky v pojmenované oblasti v listu aplikace Excel pomocí Aspose.Cells for .NET.

## Krok 1: Vytvořte nový sešit

První věc, kterou potřebujeme, je pracovní sešit. Sešit v podmínkách aplikace Excel je ekvivalentem souboru aplikace Excel. Pojďme si jeden vytvořit.

```csharp
// Vytvořte nový sešit.
Workbook wb1 = new Workbook();
```

Inicializací nového sešitu máme nyní prázdný soubor Excel připravený k manipulaci. Je to jako začít s prázdným plátnem!

## Krok 2: Otevřete první list

Každý sešit obsahuje pracovní listy a v tomto případě chceme pracovat s tím prvním. Vezmeme to!

```csharp
// Získejte první pracovní list v sešitu.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Představte si list jako jednotlivé karty v souboru aplikace Excel, kde jsou uložena skutečná data. Ve výchozím nastavení se dostáváme na úplně první kartu.

## Krok 3: Vytvořte rozsah buněk

Nyní, když máme náš pracovní list, je čas vytvořit rozsah. Rozsah označuje blok buněk, který může zahrnovat více řádků a sloupců.

```csharp
//Vytvořte rozsah.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Zde vybíráme buňky od D6 do I12 – blok, který pokrývá více řádků a sloupců. Brzy tento sortiment sloučíme!

## Krok 4: Pojmenujte rozsah

Pojmenování rozsahu usnadňuje pozdější odkazování, zejména při práci s velkými datovými sadami.

```csharp
// Pojmenujte rozsah.
mrange.Name = "TestRange";
```

Pojmenováním tohoto rozsahu „TestRange“ jej můžeme později v kódu rychle načíst, aniž bychom museli znovu zadávat souřadnice buňky.

## Krok 5: Sloučení rozsahu buněk

Nyní ke kouzlu – sloučení buněk v rozsahu, který jsme právě vytvořili!

```csharp
// Sloučit buňky rozsahu.
mrange.Merge();
```

Tento krok sloučí všechny buňky od D6 do I12 do jediné buňky. Ideální pro věci, jako jsou tituly nebo souhrny!

## Krok 6: Načtěte pojmenovaný rozsah

Jakmile jsou buňky sloučeny, můžeme chtít použít nějaké formátování. Nejprve načteme náš pojmenovaný rozsah.

```csharp
// Získejte rozsah.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Načtení rozsahu podle názvu nám umožňuje provádět další operace, jako je přidávání stylů nebo zadávání dat.

## Krok 7: Definujte styl pro sloučené buňky

K čemu je sloučená buňka, když nevypadá vyleštěně? Vytvořme objekt stylu, který zarovná text a použije barvu pozadí.

```csharp
// Definujte objekt stylu.
Style style = wb1.CreateStyle();

// Nastavte zarovnání.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Zde zarovnáváme text vodorovně i svisle na střed a nastavíme světle modrou (aqua) barvu pozadí. Stylové, že?

## Krok 8: Použijte styl na rozsah

Po definování stylu je čas jej aplikovat na sloučený rozsah.

```csharp
// Vytvořte objekt StyleFlag.
StyleFlag flag = new StyleFlag();

// Zapněte atribut relativního stylu.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Použijte styl na rozsah.
range1.ApplyStyle(style, flag);
```

 The`StyleFlag` říká Aspose.Cells, které vlastnosti stylu použít – zarovnání, stínování atd. To vám dává podrobnou kontrolu nad tím, jak je styl aplikován.

## Krok 9: Zadejte data do sloučeného rozsahu

Co je to formátovaný rozsah bez obsahu? Přidejme nějaký text.

```csharp
// Zadejte data do rozsahu.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

To umístí text "Welcome to Aspose APIs" do první buňky našeho sloučeného rozsahu. Při slučování buňky se tento text rozprostírá přes všechny buňky od D6 do I12.

## Krok 10: Uložte soubor Excel

Nakonec uložme sešit jako soubor aplikace Excel.

```csharp
// Uložte soubor aplikace Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Zde je sešit uložen pod názvem "outputMergeCellsInNamedRange.xlsx" ve vámi zadaném adresáři.

## Závěr

A tady to máte! Úspěšně jste sloučili buňky v pojmenovaném rozsahu, použili krásné formátování a dokonce jste vložili některá data – to vše pomocí Aspose.Cells pro .NET. Ať už pracujete na automatizaci sestav, manipulaci s excelovými soubory nebo se jen učíte nové techniky, tento podrobný průvodce by vám měl poskytnout základ, který potřebujete.

## FAQ

### Mohu v Aspose.Cells sloučit více nesouvislých rozsahů?  
Ne, v Aspose.Cells můžete sloučit pouze sousedící buňky.

### Mohu vrátit operaci sloučení programově?  
 Jakmile jsou buňky sloučeny, můžete je zrušit pomocí`UnMerge()` metoda v Aspose.Cells.

### Odstraní sloučení buněk data v nich?  
Pokud jsou v buňkách před sloučením nějaká data, zachovají se data z první buňky rozsahu.

### Mohu použít různé styly na jednotlivé buňky ve sloučeném rozsahu?  
Ne, sloučený rozsah funguje jako jedna buňka, takže na jednotlivé buňky v ní nemůžete použít různé styly.

### Jak získám přístup ke sloučené buňce po sloučení?  
Po sloučení můžete ke sloučené buňce stále přistupovat pomocí souřadnic jejího levého horního rohu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
