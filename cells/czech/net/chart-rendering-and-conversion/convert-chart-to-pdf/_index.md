---
"description": "Naučte se převádět grafy z Excelu do PDF pomocí Aspose.Cells pro .NET s tímto jednoduchým podrobným návodem. Prozkoumejte základní tipy a příklady kódování."
"linktitle": "Převod grafu do PDF"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Převod grafu do PDF"
"url": "/cs/net/chart-rendering-and-conversion/convert-chart-to-pdf/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Převod grafu do PDF

## Zavedení

Pokud jde o práci s tabulkami, grafy často hrají klíčovou roli v efektivní vizualizaci dat. Ať už připravujete zprávu, provádíte prezentaci nebo jednoduše provádíte analýzu dat, převod těchto grafů do PDF vám poskytne profesionální vzhled. Zde vás provedeme kroky pro převod grafu aplikace Excel do formátu PDF pomocí Aspose.Cells pro .NET, výkonné knihovny určené ke zjednodušení manipulace s Excelem.

## Předpoklady

Než se pustíte do tutoriálu, musíte se ujistit, že máte správné nastavení. Zde je to, co budete potřebovat:

### .NET Framework
Ujistěte se, že máte na svém počítači nainstalovaný .NET framework. Aspose.Cells je kompatibilní s různými verzemi, ale obvykle funguje nejlépe s nejnovějšími.

### Knihovna Aspose.Cells
Budete potřebovat knihovnu Aspose.Cells pro .NET. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/)Knihovna je dodávána s bohatým API, které zahrnuje všechny funkce potřebné pro manipulaci s Excelem.

### Visual Studio
Nainstalované Visual Studio je nezbytné, protože je to skvělé IDE pro bezproblémový psaní kódu .NET.

### Základní znalost C#
Znalost programovacího jazyka C# vám pomůže lépe porozumět jednotlivým segmentům kódu.

## Importovat balíčky

Pro úspěšné použití Aspose.Cells ve vašem projektu je nutné importovat potřebné balíčky. Zde je návod, jak to udělat:

### Vytvořit nový projekt

Začněte vytvořením nového projektu C# ve Visual Studiu:

1. Otevřete Visual Studio.
2. Klikněte na „Vytvořit nový projekt“.
3. Vyberte možnost „Konzolová aplikace (.NET Core)“ nebo „Konzolová aplikace (.NET Framework)“ na základě vašich požadavků.
4. Pojmenujte svůj projekt a klikněte na tlačítko „Vytvořit“.

### Přidat odkaz na Aspose.Cells

Po vytvoření projektu musíte přidat odkaz na knihovnu Aspose.Cells:

1. V Průzkumníku řešení klikněte pravým tlačítkem myši na váš projekt.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.Cells“ a nainstalujte jej.

Jakmile máte knihovnu zahrnutou do projektu, můžete přejít k kódu.

### Importujte požadované jmenné prostory

Na vrcholu tvého `Program.cs` soubor, přidejte následující jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Charts;
using System.IO;
```

Zde je návod, jak systematicky převést graf z Excelu do PDF. Postupujte krok za krokem!

## Krok 1: Nastavení výstupních a zdrojových adresářů

Abyste mohli začít s kódem, musíte nejprve určit, kam uložíte výstup a kde se nachází zdrojový dokument.

```csharp
// Výstupní adresář
string outputDir = "Your Output Directory";

// Zdrojový adresář
string sourceDir = "Your Document Directory";
```

Nezapomeňte vyměnit `"Your Output Directory"` a `"Your Document Directory"` se skutečnou cestou, kde se vaše soubory nacházejí.

## Krok 2: Načtení sešitu aplikace Excel

Nyní si načtěme soubor Excelu, který obsahuje grafy, které chcete převést. Je to docela jednoduché:

```csharp
// Načíst excelový soubor s grafy
Workbook workbook = new Workbook(sourceDir + "sampleChartToPdf.xlsx");
```

Tento kód inicializuje nový objekt sešitu a načte zadaný soubor aplikace Excel. Ujistěte se, že název souboru odpovídá názvu souboru ve zdrojovém adresáři.

## Krok 3: Přístup k pracovnímu listu

Dále je potřeba otevřít list, který obsahuje graf, který chcete převést. Postupujte takto:

```csharp
// Přístup k prvnímu listu
Worksheet worksheet = workbook.Worksheets[0];
```

Tento kód přistupuje k prvnímu listu ve vašem sešitu a umožňuje vám s ním pracovat.

## Krok 4: Přístup k grafu 

Jakmile máte pracovní list, je čas přistupovat ke konkrétnímu grafu, který chcete převést:

```csharp
// Přístup k prvnímu grafu v pracovním listu
Chart chart = worksheet.Charts[0];
```

Tento řádek zobrazuje první graf v listu. Pokud váš list obsahuje více grafů a potřebujete se zaměřit na konkrétní, upravte index odpovídajícím způsobem.

## Krok 5: Převod grafu do PDF

Nyní přichází ta vzrušující část – převod grafu do formátu PDF. Můžete ho uložit buď do souboru, nebo do paměťového streamu.

### Možnost 1: Uložení grafu do souboru

Chcete-li uložit graf přímo do souboru PDF, použijte následující kód:

```csharp
// Uložte graf do formátu pdf
chart.ToPdf(outputDir + "outputChartToPdf.pdf");
```

Abyste se vyhnuli chybám, ujistěte se, že výstupní adresář skutečně existuje.

### Možnost 2: Uložení grafu do paměťového streamu

Pokud chcete s PDF souborem dále manipulovat nebo jej potřebujete okamžitě použít ve své aplikaci, může být lepší volbou jeho uložení do paměťového proudu:

```csharp
// Uložit graf do formátu PDF v streamu
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```

Zde uložíte PDF do paměťového proudu, který lze použít podle potřeb vaší aplikace.

## Krok 6: Zobrazení zprávy o úspěchu

Nakonec je vždy dobré uvést, že operace proběhla úspěšně. Můžete jednoduše vypsat zprávu o úspěchu do konzole:

```csharp
Console.WriteLine("ChartToPdf executed successfully.");
```

## Závěr

tady to máte! Využitím Aspose.Cells pro .NET se převod excelových grafů do formátu PDF stává procházkou růžovým sadem. Ať už se rozhodnete ukládat do souboru nebo do paměťového streamu, knihovna slibuje flexibilitu a snadné použití. Tak proč to nezkusit? Vaše zprávy budou s profesionálně formátovanými grafy v PDF vypadat mnohem ostřeji!

## Často kladené otázky

### Může Aspose.Cells převést více grafů najednou?
Ano, můžete procházet `worksheet.Charts` kolekce pro převod každého grafu jednotlivě.

### Je Aspose.Cells vhodný pro velké soubory aplikace Excel?
Rozhodně! Aspose.Cells je optimalizován pro výkon a dokáže efektivně zpracovávat velké soubory aplikace Excel.

### Jaké verze .NET podporuje Aspose.Cells?
Aspose.Cells podporuje různé verze .NET, včetně .NET Framework a .NET Core.

### Kde najdu podrobnou dokumentaci?
Navštivte [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) pro podrobné informace a příklady.

### Je k dispozici bezplatná zkušební verze?
Ano! Zkušební verzi zdarma si můžete stáhnout z [zde](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}