---
"description": "Naučte se, jak snadno přidávat obrázky do grafů v Excelu pomocí Aspose.Cells pro .NET. Vylepšete své grafy a prezentace v několika jednoduchých krocích."
"linktitle": "Přidat obrázek do grafu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidat obrázek do grafu"
"url": "/cs/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat obrázek do grafu

## Zavedení

Už vás nebaví nudné grafy, které postrádají osobní nádech? Chcete se naučit, jak oživit vizuály v Excelu přidáním obrázků? Máte štěstí! V tomto tutoriálu se ponoříme do světa Aspose.Cells pro .NET a naučíme se, jak přidávat obrázky do grafů v Excelu. Takže si vezměte svůj oblíbený šálek kávy a pojďme na to!

## Předpoklady

Než se pustíme do detailů kódování, je třeba splnit několik předpokladů, abyste mohli plynule postupovat:

- Visual Studio: Zde budete psát a spouštět kód .NET. Ujistěte se, že ho máte nainstalovaný.
- Aspose.Cells pro .NET: Tuto knihovnu budete potřebovat pro práci se soubory aplikace Excel. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/).
- Základní znalost C#: I když vás kódem provedu, znalost základů C# vám vše usnadní.

### Kroky instalace

1. Instalace Aspose.Cells: Soubor Aspose.Cells můžete do projektu Visual Studia přidat pomocí Správce balíčků NuGet. To provedete tak, že přejdete do nabídky Nástroje > Správce balíčků NuGet > Spravovat balíčky NuGet pro řešení a vyhledáte „Aspose.Cells“. Klikněte na Instalovat.
2. Nastavení projektu: Vytvořte nový projekt konzolové aplikace C# ve Visual Studiu.

## Importovat balíčky

Jakmile máte vše nastavené, dalším krokem je import potřebných balíčků do vašeho projektu. Zde je návod, jak to udělat:

### Importujte požadované jmenné prostory

V horní části souboru s kódem C# budete muset importovat následující jmenné prostory:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Toto říká vašemu programu: „Hej! Použiji tyto skvělé funkce z Aspose.Cells.“

Nyní, když máme připravené všechny předpoklady, pojďme si celý proces rozdělit na několik kroků. 

## Krok 1: Definujte své adresáře

Nejdříve musíme nastavit cesty pro naše vstupní a výstupní soubory. Tento krok je klíčový, protože potřebujeme vědět, kde najít náš existující soubor Excelu a kam uložit upravený soubor.

```csharp
//Zdrojový adresář
string sourceDir = "Your Document Directory/";

//Výstupní adresář
string outputDir = "Your Output Directory/";
```

Nahradit `Your Document Directory` a `Your Output Directory` se skutečnými cestami ve vašem počítači. 

## Krok 2: Načtení existujícího sešitu

Nyní si načtěme existující soubor aplikace Excel, kam chceme do grafu přidat náš obrázek.

```csharp
// Otevřete existující soubor.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Tento kód otevře sešit a připraví ho k úpravám.

## Krok 3: Příprava obrazového streamu

Než přidáme obrázek, musíme si ho přečíst. 

```csharp
// Získejte soubor s obrázkem do streamu.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Ujistěte se, že máte obrázek uložený v zadaném adresáři.

## Krok 4: Zaměřte se na graf

Nyní určíme, do kterého grafu přidáme náš obrázek. V tomto příkladu se zaměříme na první graf na prvním listu.

```csharp
// Získejte návrhářský graf na druhém listu.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

K libovolnému listu se dostanete odpovídající změnou indexu.

## Krok 5: Přidání obrázku do grafu

S vybraným grafem je čas přidat obrázek! 

```csharp
// Přidejte do grafu nový obrázek.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Zde, `50` a `50` jsou souřadnice X a Y, kam bude obrázek umístěn, a `200` je šířka a výška obrázku.

## Krok 6: Úprava formátu čar obrázku

Chcete svému obrázku dodat trochu šmrncu? Můžete si upravit jeho okraj! Zde je návod, jak to udělat:

```csharp
// Získá typ řádkového formátu obrázku.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Nastavte styl pomlčky.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Nastavte tloušťku čáry.
lineformat.Weight = 4;    
```

Tento úryvek vám umožňuje zvolit vzhled a tloušťku okraje. Vyberte si jakýkoli styl, který odpovídá vaší prezentaci!

## Krok 7: Uložení upraveného sešitu

Po vší té tvrdé práci si uložme vaše úpravy spuštěním následujícího řádku kódu:

```csharp
// Uložte soubor Excelu.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Nyní je váš obrázek úspěšně integrován do grafu a výstupní soubor je připraven k prohlížení!

## Krok 8: Označení úspěchu

Nakonec můžete přidat jednoduchou zprávu, která potvrdí, že operace proběhla úspěšně:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Závěr

V tomto tutoriálu jsme prozkoumali, jak dodat vašim excelovým grafům trochu osobitosti přidáním obrázků pomocí Aspose.Cells pro .NET. Stačí jen pár jednoduchých kroků a vaše prezentace se stanou nezapomenutelnými. Tak na co čekáte? Zkuste to a nechte své grafy zazářit!

## Často kladené otázky

### Mohu do jednoho grafu přidat více obrázků?
Ano! Můžete zavolat `AddPictureInChart` metodu několikrát, abyste přidali tolik obrázků, kolik chcete.

### Jaké formáty obrázků podporuje Aspose.Cells?
Aspose.Cells podporuje různé obrazové formáty, včetně PNG, JPEG, BMP a GIF.

### Mohu si přizpůsobit polohu obrázku?
Jistě! Souřadnice X a Y v `AddPictureInChart` metoda umožňuje přesné umístění.

### Je Aspose.Cells zdarma k použití?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro plné funkce je vyžadována licence. Ceník naleznete [zde](https://purchase.aspose.com/buy).

### Kde najdu další příklady?
Podívejte se na [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobnější příklady a funkce.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}