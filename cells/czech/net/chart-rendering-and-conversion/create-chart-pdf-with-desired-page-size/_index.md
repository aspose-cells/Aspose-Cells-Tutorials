---
"description": "Vytvořte PDF s vaším excelovým grafem pomocí Aspose.Cells pro .NET. Naučte se jak v tomto podrobném návodu."
"linktitle": "Vytvořte PDF grafu s požadovanou velikostí stránky"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vytvořte PDF grafu s požadovanou velikostí stránky"
"url": "/cs/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte PDF grafu s požadovanou velikostí stránky

## Zavedení

Vytváření vizuálně poutavých a informativních grafů je nezbytné pro reprezentaci dat v různých oblastech. Ať už pracujete s prodejními daty, metrikami výkonnosti nebo jakýmkoli jiným typem informací, schopnost vytvářet vysoce kvalitní grafy dodá vašim zjištěním hloubku a přehlednost. Pokud pracujete s aplikacemi .NET, Aspose.Cells je výkonná knihovna, která usnadňuje práci s dokumenty Excel a generování grafů. V tomto tutoriálu vás provedeme procesem vytvoření grafu ve formátu PDF ze souboru Excel s požadovanou velikostí stránky.

## Předpoklady

Než se ponoříme do kódu, je třeba splnit několik předpokladů, aby byl zajištěn hladký průběh:

### Základní znalost C# a .NET

Budete potřebovat základní znalosti programování v jazyce C# a frameworku .NET. To vám pomůže pochopit strukturu kódu, se kterým se v této příručce setkáte.

### Aspose.Cells pro .NET

Ujistěte se, že máte nainstalovaný Aspose.Cells pro .NET. Veškeré podrobnosti naleznete na [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/). 

### Vývojové prostředí

Nastavte si vývojové prostředí. Může to být Visual Studio nebo jakékoli jiné IDE, které podporuje C#. Stáhněte a nainstalujte knihovnu Aspose.Cells z [stránka ke stažení](https://releases.aspose.com/cells/net/).

### Ukázkový soubor Excelu

Budete potřebovat vzorový soubor aplikace Excel, který obsahuje alespoň jeden graf. Můžete si vytvořit vzorový soubor nebo si ho stáhnout a používat ho v celém tomto tutoriálu.

## Importovat balíčky

Abyste mohli začít pracovat s Aspose.Cells, musíte do své aplikace v C# importovat potřebné jmenné prostory. Postupujte takto:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Tyto jmenné prostory vám poskytují přístup ke třídám a metodám potřebným k manipulaci s excelovými sešity a jejich obsahem.

Nyní, když máme vyřešené všechny předpoklady, pojďme si proces rozebrat na podrobné kroky.

## Krok 1: Nastavení výstupních a zdrojových adresářů

Nejprve je třeba definovat, kam bude uložen výstupní PDF a kde se nachází váš zdrojový dokument Excel.

```csharp
//Výstupní adresář
string outputDir = "Your Output Directory";

//Zdrojový adresář
string sourceDir = "Your Document Directory";
```

Nezapomeňte nahradit „Váš výstupní adresář“ a „Adresář dokumentů“ skutečnými cestami ve vašem systému. To určuje, kam Aspose uloží vygenerovaný PDF a kde najde soubor Excel.

## Krok 2: Načtěte ukázkový soubor Excel

Dále je třeba načíst soubor aplikace Excel, který obsahuje graf. Postupujte takto:

```csharp
//Načtěte ukázkový soubor Excelu obsahující graf.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

Ten/Ta/To `Workbook` Třída je klíčová pro interakci s vaším dokumentem aplikace Excel. Ujistěte se, že cesta správně ukazuje na váš soubor aplikace Excel – chyba v tomto případě zabrání spuštění zbytku kódu.

## Krok 3: Přístup k prvnímu pracovnímu listu

Jakmile je sešit načten, dalším krokem je přístup k listu obsahujícímu požadovaný graf.

```csharp
//Zpřístupněte první pracovní list.
Worksheet ws = wb.Worksheets[0];
```

V Aspose.Cells jsou pracovní listy indexovány od nuly, takže `Worksheets[0]` odkazuje na první list.

## Krok 4: Přístup k prvnímu grafu

Nyní si otevřeme graf, který chcete exportovat do PDF. Tento krok předpokládá, že váš list obsahuje alespoň jeden graf.

```csharp
//Otevřete první graf v pracovním listu.
Chart ch = ws.Charts[0];
```

Opět se tím zpřístupní první graf v listu; ujistěte se, že struktura vašeho listu tomuto přístupu vyhovuje.

## Krok 5: Vytvořte PDF s požadovanou velikostí stránky

Konečně je čas vytvořit PDF z grafu se zadanou velikostí stránky. Zde je kouzelný řádek kódu, který to všechno udělá:

```csharp
//Vytvořte PDF s grafem s požadovanou velikostí stránky.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

V tomto kódu:
- PDF bude uložen do výstupního adresáře, který jste dříve zadali.
- Čísla `7, 7` představují šířku a výšku požadované velikosti stránky.
- PageLayoutAlignmentType.Center zajišťuje, že graf je na stránce vycentrován.

## Krok 6: Potvrzovací zpráva

Abyste sobě (a ostatním) dali vědět, že vše proběhlo hladce, přidejte na konec kódu potvrzovací zprávu:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Tato zpráva se zobrazí v okně konzole po dokončení procesu, což signalizuje, že váš PDF soubor byl vytvořen bez problémů.

## Závěr

Gratulujeme! Právě jste se naučili, jak využít Aspose.Cells pro .NET k vytvoření PDF z grafu obsaženého v souboru Excelu. Tato výkonná knihovna zjednodušuje proces manipulace s dokumenty Excelu a generování vizuálních reprezentací dat, čímž vám ušetří hodiny ručního formátování. Nezapomeňte prozkoumat nepřeberné množství dalších funkcí, které Aspose.Cells nabízí nad rámec pouhého generování PDF – nikdy nevíte, co může vaše projekty ještě vylepšit!

## Často kladené otázky

### K čemu se používá Aspose.Cells pro .NET?  
Aspose.Cells pro .NET se používá k programovému vytváření, úpravě a převodu dokumentů aplikace Excel v aplikacích .NET.

### Mohu používat Aspose.Cells zdarma?  
Ano, Aspose.Cells nabízí [bezplatná zkušební verze](https://releases.aspose.com/) pro účely hodnocení.

### Existuje způsob, jak prodloužit zkušební dobu po uplynutí původní doby?  
Můžete požádat o [dočasná licence](https://purchase.aspose.com/temporary-license/) pro prodloužené testování.

### Co když narazím na problémy nebo budu mít otázky?  
Pomoc můžete vyhledat v komunitě Aspose na jejich [fórum podpory](https://forum.aspose.com/c/cells/9).

### Jak si mohu zakoupit Aspose.Cells?  
Aspose.Cells si můžete koupit od [stránka nákupu](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}