---
title: Použít motivy v grafu
linktitle: Použít motivy v grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak aplikovat motivy na grafy v Excelu pomocí Aspose.Cells for .NET s naším jednoduchým průvodcem krok za krokem. Vylepšete svou prezentaci dat.
weight: 10
url: /cs/net/setting-chart-appearance/apply-themes-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použít motivy v grafu

## Zavedení

Vytváření vizuálně atraktivních grafů v Excelu je zásadní pro efektivní komunikaci vašich dat. Použitím motivů můžete zlepšit estetiku svých grafů, díky čemuž budou informace nejen dostupné, ale také poutavé. V této příručce prozkoumáme, jak aplikovat motivy pomocí Aspose.Cells pro .NET. Vezměte si svou oblíbenou svačinu a pojďme se ponořit do kreativního světa žebříčků!

## Předpoklady

Než se pustíme do sekce kódování, je potřeba splnit několik předpokladů.

### Požadovaný software

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Poskytuje přátelské prostředí pro vývoj aplikací .NET.
2. .NET Framework nebo .NET Core: V závislosti na vašich preferencích byste měli mít nastaveno buď .NET Framework nebo .NET Core, abyste mohli následovat náš kód.
3.  Aspose.Cells pro .NET: Tohle si nemůžete nechat ujít! Chcete-li začít, stáhněte si Aspose.Cells for .NET. Můžete najít knihovny DLL[zde](https://releases.aspose.com/cells/net/).
4. Základní znalost C#: I když vás provedeme kódem krok za krokem, určitá základní znalost C# vám určitě pomůže.

## Importujte balíčky

Pro práci s Aspose.Cells for .NET je prvním krokem import potřebných balíčků. Do svého projektu C# zahrňte následující jmenný prostor:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

Nyní, když máme pokryty naše předpoklady, pojďme si krok za krokem rozebrat proces použití motivů na graf v Excelu.

## Krok 1: Nastavte svůj výstupní a zdrojový adresář

První věc, kterou musíme udělat, je vytvořit náš výstupní adresář a zdrojový adresář. Zde budete načítat soubory aplikace Excel a kam se uloží upravené soubory.

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory";

// Zdrojový adresář
string sourceDir = "Your Document Directory";
```

 Tady, vyměňte`Your Output Directory` a`Your Document Directory` s vašimi konkrétními cestami. Jasně definované tyto adresáře zefektivní váš pracovní postup a vyhnete se jakémukoli zmatku.

## Krok 2: Vytvořte sešit

 Dále je čas otevřít soubor Excel, který obsahuje graf, který chcete upravit. Toho dosáhneme vytvořením instance`Workbook` třídy a načtení našeho zdrojového souboru.

```csharp
// Vytvořte instanci sešitu a otevřete soubor obsahující graf
Workbook workbook = new Workbook(sourceDir + "sampleApplyingThemesInChart.xlsx");
```

 Zajistěte to`sampleApplyingThemesInChart.xlsx` existuje ve vašem zdrojovém adresáři.

## Krok 3: Otevřete sešit

Nyní, když máme sešit nastavený, je dalším krokem přístup ke konkrétnímu listu, který obsahuje náš graf. 

```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
```

V tomto případě jednoduše uchopíme první list, který je pro tento příklad dostačující. Pokud máte více listů, můžete určit index nebo název listu na základě vašich požadavků.

## Krok 4: Získejte graf

S pracovním listem v ruce máme nyní přístup k grafu, který hodláme upravit.

```csharp
// Získejte první graf v listu
Chart chart = worksheet.Charts[0];
```

Zde získáváme první graf. Pokud váš list obsahuje více grafů a vy chcete konkrétní, stačí odpovídajícím způsobem změnit index.

## Krok 5: Naneste na sérii Solid Fill

Před použitím motivu se ujistěte, že naše série grafů má plnou výplň. Můžete to nastavit takto:

```csharp
// Určete typ FillFormat na Solid Fill první řady
chart.NSeries[0].Area.FillFormat.FillType = Aspose.Cells.Drawing.FillType.Solid;
```

Tento řádek kódu zajišťuje, že první řada v grafu je nastavena tak, aby používala plnou výplň.

## Krok 6: Nakonfigurujte barvu

 Nyní, když je naše série připravena, musíme upravit její barvu. To zahrnuje vytvoření a`CellsColor` objekt a určení barvy motivu. Pro tento příklad zvolíme styl přízvuku.

```csharp
//Získejte CellsColor SolidFill
CellsColor cc = chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor;

// Vytvořte motiv ve stylu Accent
cc.ThemeColor = new ThemeColor(ThemeColorType.Accent6, 0.6);
```

Zde je to, co se děje:
1. Získáme barvu pevné výplně.
2.  Použití`ThemeColor` , nastavíme barvu naší plné výplně. Můžete se změnit`Accent6` na jakoukoli jinou barvu motivu podle toho, co se vám líbí.

## Krok 7: Použijte motiv na sérii

Po konfiguraci barvy je čas použít tento nový motiv na naši sérii. 

```csharp
// Použijte motiv na sérii
chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor = cc;
```

Tento řádek efektivně aktualizuje barvy v grafu. 

## Krok 8: Uložte sešit

Po vší té tvrdé práci musíme uložit naše změny do nového souboru Excel.

```csharp
// Uložte soubor aplikace Excel
workbook.Save(outputDir + "outputApplyingThemesInChart.xlsx");
```

Zde ukládáme upravený sešit do výstupního adresáře, který jste zadali dříve. 

## Krok 9: Výstup potvrzení

Abychom věděli, že proces byl úspěšně proveden, můžeme vytisknout potvrzovací zprávu:

```csharp
Console.WriteLine("ApplyingThemesInChart executed successfully.");
```

Tento řádek zobrazí v konzole zprávu, že úloha byla dokončena.

## Závěr

Použití motivů na grafy v aplikaci Excel pomocí Aspose.Cells for .NET může zcela změnit způsob, jakým jsou vaše data prohlížena. Nejen, že vaše grafy budou esteticky příjemné, ale také to pomůže efektivněji předat vaše sdělení. Podle kroků uvedených v této příručce můžete snadno přizpůsobit své grafy a prezentovat svá data způsobem, který upoutá pozornost publika.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje vývojářům programově manipulovat se soubory aplikace Excel.

### Mohu Aspose.Cells před nákupem vyzkoušet?
 Ano, můžete si stáhnout bezplatnou zkušební verzi[zde](https://releases.aspose.com/).

### Jaké typy motivů grafů mohu použít?
Aspose.Cells podporuje různé barvy motivů včetně stylů Accent a dalších.

### Je možné použít motivy na více grafů?
Absolutně! Můžete procházet`worksheet.Charts` a aplikujte motivy podle potřeby.

### Kde mohu získat podporu pro Aspose.Cells?
 Můžete získat podporu a zapojit se do komunity uživatelů[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
