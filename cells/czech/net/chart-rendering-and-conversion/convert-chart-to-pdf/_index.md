---
title: Převést graf do PDF
linktitle: Převést graf do PDF
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se převádět grafy Excelu do PDF pomocí Aspose.Cells for .NET pomocí tohoto jednoduchého průvodce krok za krokem. Prozkoumejte základní tipy a příklady kódování.
weight: 11
url: /cs/net/chart-rendering-and-conversion/convert-chart-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převést graf do PDF

## Zavedení

Pokud jde o práci s tabulkami, grafy často hrají klíčovou roli při efektivní vizualizaci dat. Ať už připravujete zprávu, provádíte prezentaci nebo jednoduše usnadňujete analýzu dat, převod těchto grafů do PDF poskytuje profesionální přístup. Zde vás provedeme kroky k převodu grafu Excel do formátu PDF pomocí Aspose.Cells for .NET, výkonné knihovny navržené pro zjednodušení manipulace s Excelem.

## Předpoklady

Než se pustíte do výukového programu, musíte se ujistit, že máte správné nastavení. Zde je to, co potřebujete:

### .NET Framework
Ujistěte se, že máte na svém počítači nainstalovaný .NET framework. Aspose.Cells je kompatibilní s různými verzemi, ale obvykle funguje nejlépe s nejnovějšími.

### Knihovna Aspose.Cells
 Budete potřebovat knihovnu Aspose.Cells for .NET. Můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/). Knihovna je dodávána s bohatým rozhraním API, které zahrnuje všechny funkce, které byste potřebovali pro manipulaci s Excelem.

### Visual Studio
Mít nainstalované Visual Studio je zásadní, protože je to skvělé IDE pro bezproblémové psaní kódu .NET.

### Základní znalost C#
Určitá znalost programovacího jazyka C# vám pomůže lépe porozumět segmentům kódu.

## Importujte balíčky

Pro úspěšné použití Aspose.Cells ve vašem projektu je třeba importovat potřebné balíčky. Můžete to udělat takto:

### Vytvořit nový projekt

Začněte vytvořením nového projektu C# ve Visual Studiu:

1. Otevřete Visual Studio.
2. Klikněte na „Vytvořit nový projekt“.
3. Vyberte „Console App (.NET Core)“ nebo „Console App (.NET Framework)“ na základě vašeho požadavku.
4. Pojmenujte svůj projekt a klikněte na „Vytvořit“.

### Přidejte odkaz Aspose.Cells

Po vytvoření projektu musíte přidat odkaz na knihovnu Aspose.Cells:

1. V Průzkumníku řešení klikněte pravým tlačítkem na svůj projekt.
2. Vyberte „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.Cells“ a nainstalujte jej.

Jakmile budete mít knihovnu zahrnutou do svého projektu, jste připraveni přejít ke kódu.

### Importujte požadované jmenné prostory

 V horní části vašeho`Program.cs` soubor, přidejte následující jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Charts;
using System.IO;
```

Zde je návod, jak systematicky převést graf Excel do PDF. Postupujte krok za krokem!

## Krok 1: Nastavte výstupní a zdrojové adresáře

Chcete-li začít s kódem, musíte nejprve určit, kam uložíte výstup a kde se nachází zdrojový dokument.

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory";

// Zdrojový adresář
string sourceDir = "Your Document Directory";
```

 Nezapomeňte vyměnit`"Your Output Directory"` a`"Your Document Directory"` se skutečnou cestou, kde jsou umístěny vaše soubory.

## Krok 2: Načtěte sešit aplikace Excel

Nyní načteme soubor Excel, který obsahuje grafy, které chcete převést. Toto je docela jednoduché:

```csharp
// Načtěte excelový soubor obsahující grafy
Workbook workbook = new Workbook(sourceDir + "sampleChartToPdf.xlsx");
```

Tento kód inicializuje nový objekt sešitu a načte zadaný soubor aplikace Excel. Ujistěte se, že název souboru odpovídá názvu, který máte ve zdrojovém adresáři.

## Krok 3: Otevřete sešit

Dále musíte získat přístup k listu, který obsahuje graf, který chcete převést. Jak na to:

```csharp
// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```

Tento kód přistupuje k prvnímu listu ve vašem sešitu a umožňuje vám s ním pracovat.

## Krok 4: Přístup k grafu 

Jakmile budete mít list, je čas otevřít konkrétní graf, který chcete převést:

```csharp
// Přístup k prvnímu grafu uvnitř listu
Chart chart = worksheet.Charts[0];
```

Tento řádek zachycuje první graf obsažený v listu. Pokud váš list obsahuje více grafů a potřebujete cílit na konkrétní, upravte podle toho index.

## Krok 5: Převeďte graf do PDF

Nyní přichází ta vzrušující část – převod grafu do formátu PDF. Můžete jej uložit do souboru nebo do paměti.

### Možnost 1: Uložit graf do souboru

Chcete-li uložit graf přímo do souboru PDF, použijte následující kód:

```csharp
// Uložte graf do formátu pdf
chart.ToPdf(outputDir + "outputChartToPdf.pdf");
```

Jen se ujistěte, že výstupní adresář skutečně existuje, aby se předešlo chybám.

### Možnost 2: Uložit graf do Memory Stream

Pokud chcete s PDF dále manipulovat nebo jej potřebujete okamžitě použít ve své aplikaci, uložení do paměťového streamu může být lepší volbou:

```csharp
// Uložte graf ve formátu pdf ve streamu
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```

Zde uložíte PDF do paměťového toku, který lze použít podle potřeb vaší aplikace.

## Krok 6: Zobrazte zprávu o úspěchu

Nakonec je vždy příjemné označit, že vaše operace byla úspěšná. Můžete jednoduše vytisknout zprávu o úspěchu na konzoli:

```csharp
Console.WriteLine("ChartToPdf executed successfully.");
```

## Závěr

tady to máte! Díky využití Aspose.Cells pro .NET se převod grafů Excelu do formátu PDF stává procházkou růžovým sadem. Ať už se rozhodnete pro uložení do souboru nebo paměťového toku, knihovna slibuje flexibilitu a snadné použití. Tak proč to nezkusit? Vaše sestavy budou vypadat mnohem ostřeji s profesionálně formátovanými grafy PDF!

## FAQ

### Může Aspose.Cells převést více grafů najednou?
 Ano, můžete procházet`worksheet.Charts` kolekce pro převod každého grafu jednotlivě.

### Je Aspose.Cells vhodný pro velké soubory Excel?
Absolutně! Aspose.Cells je optimalizován pro výkon a dokáže efektivně zpracovávat velké soubory aplikace Excel.

### Jaké verze .NET podporuje Aspose.Cells?
Aspose.Cells podporuje různé verze .NET, včetně .NET Framework a .NET Core.

### Kde najdu podrobnou dokumentaci?
 Navštivte[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné informace a příklady.

### Je k dispozici bezplatná zkušební verze?
 Ano! Bezplatnou zkušební verzi si můžete stáhnout z[zde](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
