---
title: Přidejte ovládací prvek TextBox do grafu
linktitle: Přidejte ovládací prvek TextBox do grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat TextBox do grafů v Excelu pomocí Aspose.Cells for .NET. Vylepšete vizualizaci dat bez námahy.
weight: 12
url: /cs/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte ovládací prvek TextBox do grafu

## Zavedení

Vytváření dynamických a vizuálně přitažlivých grafů v Excelu je fantastický způsob, jak efektivně reprezentovat data. Jedna šikovná funkce, kterou můžete použít, je přidání textového pole do grafu. S Aspose.Cells pro .NET se tento úkol stává snadným a zábavným! V této příručce vás krok za krokem provedeme procesem integrace textového pole do vašeho grafu. Ať už jste zkušený vývojář nebo teprve začínáte, tento tutoriál vám poskytne všechny nástroje, které potřebujete k vylepšení vašich grafů Excel. Tak co, jste připraveni se ponořit?

## Předpoklady

Než se pustíme do kódování, měli byste mít připraveno několik věcí:

- Základní porozumění C#: Základní znalost programování C# bude užitečná. Nebojte se; nemusíte být expert, stačí se pohodlně orientovat v syntaxi.
-  Nainstalovaná knihovna Aspose.Cells: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells for .NET. Můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/) pokud jste to ještě neudělali.
- Visual Studio: Nezbytná je znalost sady Visual Studio nebo jakéhokoli IDE, které chcete používat pro rozhraní .NET.
- Existující soubor aplikace Excel: V tomto příkladu budeme pracovat s existujícím souborem aplikace Excel s názvem "sampleAddingTextBoxControlInChart.xls". Můžete si jej vytvořit nebo si stáhnout ukázku.

Nyní, když máme vše na svém místě, pojďme k části kódování!

## Importujte balíčky

Nejprve musíme importovat potřebné jmenné prostory Aspose.Cells do našeho projektu C#. Můžete to snadno provést vložením následujících řádků do horní části souboru kódu:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Krok 1: Definujte zdrojový a výstupní adresář

Než začneme pracovat se souborem Excel, je důležité definovat, kde se nachází váš vstupní soubor a kam chcete uložit výstupní soubor. To pomáhá udržet váš projekt organizovaný.

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";

// Výstupní adresář
string outputDir = "Your Output Directory";
```
 Nahradit`"Your Document Directory"` a`"Your Output Directory"` se skutečnými cestami ve vašem systému.

## Krok 2: Otevřete existující soubor Excel

Dále musíme otevřít soubor Excel, který obsahuje graf, který chceme upravit. To nám umožní načíst graf a provést změny.

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Tento řádek inicializuje nový objekt Workbook s naším zadaným souborem.

## Krok 3: Otevřete graf v listu

Vzhledem k tomu, že grafy v aplikaci Excel jsou uloženy v listu, musíme nejprve otevřít list a poté získat požadovaný graf. V tomto příkladu přistoupíme k prvnímu grafu v prvním listu.

```csharp
// Získejte graf návrháře na prvním listu.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Změnou hodnoty indexu můžete vybrat různé listy nebo grafy, pokud jich soubor obsahuje více.

## Krok 4: Přidejte do grafu nové textové pole

Nyní jsme připraveni přidat náš TextBox. Jeho polohu a velikost upřesníme při jeho vytváření.

```csharp
// Přidejte do grafu nové textové pole.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
tomto příkazu parametry definují umístění (x, y) a velikost (šířka, výška) textového pole v grafu. Upravte tyto hodnoty na základě vašich konkrétních potřeb rozvržení.

## Krok 5: Nastavte text pro textové pole

Jakmile je TextBox na svém místě, je čas jej naplnit obsahem. Můžete přidat libovolný text, který považujete za nezbytný pro svůj graf.

```csharp
// Vyplňte text.
textbox0.Text = "Sales By Region";
```
Neváhejte nahradit „Prodej podle regionu“ jakýmkoli textem relevantním pro vaše data.

## Krok 6: Upravte vlastnosti textového pole

Nyní pojďme, aby náš TextBox vypadal dobře! Můžete přizpůsobit různé vlastnosti, jako je barva písma, velikost a styl.

```csharp
// Nastavte barvu písma.
textbox0.Font.Color = Color.Maroon; // Změňte na požadovanou barvu

// Nastavte písmo na tučné.
textbox0.Font.IsBold = true;

// Nastavte velikost písma.
textbox0.Font.Size = 14;

// Nastavte atribut písma na kurzívu.
textbox0.Font.IsItalic = true;
```

Každý z těchto řádků upravuje vzhled textu uvnitř textového pole, čímž zvyšuje viditelnost a přitažlivost.

## Krok 7: Naformátujte vzhled textového pole

Je také nezbytné formátovat pozadí a ohraničení TextBoxu. Díky tomu vynikne na grafu.

```csharp
// Získejte formát výplně textového pole.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Získejte typ formátu řádku textového pole.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Nastavte tloušťku čáry.
lineformat.Weight = 2;

// Nastavte styl čárky na plnou.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Tyto možnosti umožňují nastavit výplň pozadí textového pole a přizpůsobit jeho ohraničení.

## Krok 8: Uložte upravený soubor Excel

Posledním krokem je uložení změn, které jste provedli do nového souboru Excel. Tím zajistíte, že váš původní soubor zůstane nedotčen.

```csharp
// Uložte soubor aplikace Excel.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Nahradit`"outputAddingTextBoxControlInChart.xls"` s libovolným názvem souboru.

## Závěr

Gratuluji! Úspěšně jste přidali ovládací prvek TextBox do grafu pomocí Aspose.Cells pro .NET. Tato jednoduchá, ale účinná změna může učinit vaše grafy informativnějšími a vizuálně přitažlivějšími. Reprezentace dat je klíčem k efektivní komunikaci as nástroji, jako je Aspose, máte možnost tuto prezentaci vylepšit s minimálním úsilím.

## FAQ

### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je výkonná knihovna pro vytváření, manipulaci a konverzi souborů aplikace Excel, aniž byste se museli spoléhat na Microsoft Excel.

### Mohu přidat více textových polí do jednoho grafu?
Ano! Můžete přidat tolik textových polí, kolik potřebujete, opakováním kroků vytváření textových polí s různými pozicemi.

### Je Aspose.Cells zdarma k použití?
Aspose.Cells je placená knihovna, ale můžete si stáhnout bezplatnou zkušební verzi[zde](https://releases.aspose.com/).

### Kde najdu další dokumentaci na Aspose.Cells?
 Máte přístup ke komplexní dokumentaci[zde](https://reference.aspose.com/cells/net/).

### Jak získám podporu, pokud narazím na problémy?
 Pomoc můžete vyhledat prostřednictvím fóra podpory Aspose[zde](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
