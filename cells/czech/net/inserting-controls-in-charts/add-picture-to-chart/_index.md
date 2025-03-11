---
title: Přidat obrázek do grafu
linktitle: Přidat obrázek do grafu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se snadno přidávat obrázky do grafů aplikace Excel pomocí Aspose.Cells for .NET. Vylepšete své grafy a prezentace v několika jednoduchých krocích.
weight: 11
url: /cs/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat obrázek do grafu

## Zavedení

Už vás nebaví nudné tabulky, které postrádají osobní nádech? Chcete se naučit, jak okořenit své excelové vizuály přidáním obrázků? Tak to máš štěstí! V tomto tutoriálu se ponoříme do světa Aspose.Cells pro .NET a naučíme se přidávat obrázky do grafů v Excelu. Vezměte si svůj oblíbený šálek kávy a můžeme začít!

## Předpoklady

Než se pustíme do hrubky kódování, existuje několik předpokladů, které musíte hladce dodržovat:

- Visual Studio: Zde budete psát a spouštět svůj kód .NET. Ujistěte se, že jej máte nainstalovaný.
-  Aspose.Cells for .NET: Tuto knihovnu budete potřebovat pro práci se soubory aplikace Excel. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Základní porozumění C#: I když vás provedu kódem, znalost základů C# bude věci jasnější.

### Kroky instalace

1. Instalace Aspose.Cells: Aspose.Cells můžete přidat do svého projektu Visual Studio prostřednictvím NuGet Package Manager. Udělejte to tak, že přejdete na Nástroje > Správce balíčků NuGet > Spravovat balíčky NuGet pro řešení a vyhledáte „Aspose.Cells“. Klepněte na tlačítko Instalovat.
2. Nastavení projektu: Vytvořte nový projekt konzolové aplikace C# ve Visual Studiu.

## Importujte balíčky

Jakmile máte vše nastaveno, dalším krokem je import potřebných balíčků do vašeho projektu. Jak na to:

### Importujte požadované jmenné prostory

V horní části souboru kódu C# budete muset importovat následující jmenné prostory:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

To říká vašemu programu: „Hej! Budu používat tyto skvělé funkce od Aspose.Cells.“

Nyní, když máme připraveny naše předpoklady, pojďme si celý proces rozdělit na malé kroky. 

## Krok 1: Definujte své adresáře

Nejprve musíme nastavit cesty pro naše vstupní a výstupní soubory. Tento krok je zásadní, protože potřebujeme vědět, kde najít náš stávající soubor Excel a kam uložit upravený soubor.

```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory/";

//Výstupní adresář
string outputDir = "Your Output Directory/";
```

 Nahradit`Your Document Directory` a`Your Output Directory` se skutečnými cestami ve vašem počítači. 

## Krok 2: Načtěte existující sešit

Nyní načteme existující soubor Excel, kam chceme přidat náš obrázek do grafu.

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Tento kód otevře sešit a připraví jej k úpravám.

## Krok 3: Připravte tok obrázků

Před přidáním obrázku si musíme přečíst obrázek, který chceme do grafu vložit. 

```csharp
// Získejte soubor obrázku do streamu.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Ujistěte se, že máte obrázek uložený v určeném adresáři.

## Krok 4: Zaměřte se na graf

Nyní upřesníme, do kterého grafu přidáme náš obrázek. V tomto příkladu zacílíme na první graf na prvním listu.

```csharp
// Získejte graf návrháře na druhém listu.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Přístup k libovolnému listu získáte odpovídající změnou indexu.

## Krok 5: Přidejte obrázek do grafu

S vybraným grafem je čas přidat obrázek! 

```csharp
// Přidejte do grafu nový obrázek.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Zde,`50` a`50` jsou souřadnice X a Y, kam bude obrázek umístěn, a`200` je šířka a výška obrázku.

## Krok 6: Upravte formát čar obrázku

Chcete svému obrázku dodat nějaký šmrnc? Můžete si přizpůsobit jeho okraj! Jak na to:

```csharp
// Získejte typ formátu řádku obrázku.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Nastavte styl čárky.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Nastavte tloušťku čáry.
lineformat.Weight = 4;    
```

Tento úryvek vám umožňuje vybrat, jak bude okraj vypadat a jak silný bude. Vyberte si jakýkoli styl, který rezonuje s vaší prezentací!

## Krok 7: Uložte upravený sešit

Po vší té tvrdé práci uložme vaše úpravy provedením následujícího řádku kódu:

```csharp
// Uložte soubor aplikace Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Nyní je váš obrázek úspěšně integrován do grafu a váš výstupní soubor je připraven k prohlížení!

## Krok 8: Označte úspěch

Nakonec můžete přidat jednoduchou zprávu, která potvrdí, že vaše operace byla úspěšná:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Závěr

V tomto tutoriálu jsme prozkoumali, jak vnést trochu osobitosti do grafů aplikace Excel přidáním obrázků pomocí Aspose.Cells pro .NET. Pomocí několika jednoduchých kroků můžete své prezentace povýšit ze světských na nezapomenutelné. Tak na co čekáš? Vyzkoušejte to a nechte své žebříčky zářit!

## FAQ

### Mohu přidat více obrázků do jednoho grafu?
 Ano! Můžete zavolat na`AddPictureInChart` vícekrát přidat tolik obrázků, kolik si přejete.

### Jaké formáty obrázků podporuje Aspose.Cells?
Aspose.Cells podporuje různé formáty obrázků, včetně PNG, JPEG, BMP a GIF.

### Mohu upravit polohu obrázku?
 Jistě! Souřadnice X a Y v`AddPictureInChart` metoda umožňuje přesné polohování.

### Je Aspose.Cells zdarma k použití?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plné funkce je vyžadována licence. Cenu najdete[zde](https://purchase.aspose.com/buy).

### Kde najdu další příklady?
 Podívejte se na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobnější příklady a funkce.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
