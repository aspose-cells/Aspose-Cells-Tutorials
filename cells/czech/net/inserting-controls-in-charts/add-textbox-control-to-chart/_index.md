---
"description": "Naučte se, jak přidat textové pole do grafů v Excelu pomocí Aspose.Cells pro .NET. Vylepšete si vizualizaci dat bez námahy."
"linktitle": "Přidat ovládací prvek TextBox do grafu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidat ovládací prvek TextBox do grafu"
"url": "/cs/net/inserting-controls-in-charts/add-textbox-control-to-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat ovládací prvek TextBox do grafu

## Zavedení

Vytváření dynamických a vizuálně poutavých grafů v Excelu je fantastický způsob, jak efektivně reprezentovat data. Jednou z šikovných funkcí, kterou můžete použít, je přidání textového pole do grafu. S Aspose.Cells pro .NET se tento úkol stává snadným a zábavným! V této příručce vás krok za krokem provedeme procesem integrace textového pole do grafu. Ať už jste zkušený vývojář, nebo teprve začínáte, tento tutoriál vám poskytne všechny nástroje, které potřebujete k vylepšení svých excelových grafů. Takže, jste připraveni se do toho pustit?

## Předpoklady

Než se pustíme do kódování, je třeba mít připraveno několik věcí:

- Základní znalost C#: Základní znalost programování v C# bude užitečná. Nebojte se, nemusíte být expert, stačí, když se budete dobře orientovat v syntaxi.
- Nainstalovaná knihovna Aspose.Cells: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells for .NET. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/) pokud jste tak ještě neučinili.
- Visual Studio: Znalost Visual Studia nebo jakéhokoli IDE, které preferujete používat pro framework .NET, je nezbytná.
- Existující soubor aplikace Excel: V tomto příkladu budeme pracovat s existujícím souborem aplikace Excel s názvem „sampleAddingTextBoxControlInChart.xls“. Můžete si jej vytvořit nebo si stáhnout vzorek.

Teď, když máme vše připravené, pojďme se pustit do kódování!

## Importovat balíčky

Nejdříve musíme do našeho projektu v C# importovat potřebné jmenné prostory Aspose.Cells. To snadno provedete přidáním následujících řádků na začátek souboru s kódem:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Krok 1: Definujte zdrojové a výstupní adresáře

Než začneme pracovat s excelovým souborem, je důležité definovat, kde se nachází vstupní soubor a kam chcete uložit výstupní soubor. To pomůže udržet váš projekt v pořádku.

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";

// Výstupní adresář
string outputDir = "Your Output Directory";
```
Nahradit `"Your Document Directory"` a `"Your Output Directory"` se skutečnými cestami ve vašem systému.

## Krok 2: Otevřete existující soubor aplikace Excel

Dále musíme otevřít soubor aplikace Excel, který obsahuje graf, který chceme upravit. To nám umožní graf načíst a provést změny.

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Tento řádek inicializuje nový objekt Workbook s námi zadaným souborem.

## Krok 3: Otevření grafu v pracovním listu

Protože grafy v Excelu jsou uloženy v listu, musíme nejprve přistupovat k listu a poté k požadovanému grafu. V tomto příkladu přistupujeme k prvnímu grafu v prvním listu.

```csharp
// Získejte návrhářský graf na prvním listu.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Změnou hodnoty indexu můžete vybrat různé listy nebo grafy, pokud jich váš soubor obsahuje více.

## Krok 4: Přidání nového textového pole do grafu

Nyní jsme připraveni přidat náš TextBox. Jeho pozici a velikost určíme při jeho vytváření.

```csharp
// Přidejte do grafu nové textové pole.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
V tomto příkazu parametry definují umístění (x, y) a velikost (šířku, výšku) textového pole v grafu. Upravte tyto hodnoty podle vašich specifických potřeb rozvržení.

## Krok 5: Nastavení textu pro textové pole

Jakmile je textové pole na místě, je čas ho naplnit obsahem. Můžete přidat jakýkoli text, který považujete za potřebný pro váš graf.

```csharp
// Doplňte text.
textbox0.Text = "Sales By Region";
```
Neváhejte nahradit text „Prodej podle regionu“ jakýmkoli textem relevantním pro vaše data.

## Krok 6: Úprava vlastností textového pole

A teď si pojďme vylepšit vzhled našeho TextBoxu! Můžete si přizpůsobit různé vlastnosti, jako je barva písma, velikost a styl.

```csharp
// Nastavte barvu písma.
textbox0.Font.Color = Color.Maroon; // Změňte na požadovanou barvu

// Nastavte písmo na tučné.
textbox0.Font.IsBold = true;

// Nastavte velikost písma.
textbox0.Font.Size = 14;

// Nastavit atribut písma na kurzívu.
textbox0.Font.IsItalic = true;
```

Každý z těchto řádků upravuje vzhled textu uvnitř textového pole, čímž zvyšuje viditelnost a atraktivitu.

## Krok 7: Formátování vzhledu textového pole

Je také nezbytné formátovat pozadí a okraj textového pole. Díky tomu bude v grafu výraznější.

```csharp
// Získejte formát výplně textového pole.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Získá typ formátu řádku textového pole.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Nastavte tloušťku čáry.
lineformat.Weight = 2;

// Nastavte styl čárkování na plný.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Tyto možnosti umožňují nastavit výplň pozadí textového pole a přizpůsobit jeho ohraničení.

## Krok 8: Uložení upraveného souboru aplikace Excel

Posledním krokem je uložení provedených změn do nového souboru aplikace Excel. Tím zajistíte, že původní soubor zůstane nedotčen.

```csharp
// Uložte soubor Excelu.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
Nahradit `"outputAddingTextBoxControlInChart.xls"` s libovolným názvem souboru, který preferujete.

## Závěr

Gratulujeme! Úspěšně jste přidali ovládací prvek TextBox do grafu pomocí Aspose.Cells pro .NET. Tato jednoduchá, ale efektivní změna může vaše grafy učinit informativnějšími a vizuálně atraktivnějšími. Reprezentace dat je klíčem k efektivní komunikaci a s nástroji, jako je Aspose, máte možnost tuto prezentaci vylepšit s minimálním úsilím.

## Často kladené otázky

### Co je Aspose.Cells pro .NET?
Aspose.Cells pro .NET je výkonná knihovna pro vytváření, manipulaci a převod souborů aplikace Excel bez nutnosti spoléhat se na Microsoft Excel.

### Mohu do jednoho grafu přidat více textových polí?
Ano! Můžete přidat libovolný počet textových polí opakováním kroků pro jejich vytvoření s různými pozicemi.

### Je Aspose.Cells zdarma k použití?
Aspose.Cells je placená knihovna, ale bezplatnou zkušební verzi si můžete stáhnout z [zde](https://releases.aspose.com/).

### Kde najdu další dokumentaci k Aspose.Cells?
Můžete získat přístup k komplexní dokumentaci [zde](https://reference.aspose.com/cells/net/).

### Jak získám podporu, pokud narazím na problémy?
Pomoc můžete vyhledat prostřednictvím fóra podpory Aspose. [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}