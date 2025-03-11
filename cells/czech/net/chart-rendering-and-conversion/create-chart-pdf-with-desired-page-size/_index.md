---
title: Vytvořte graf PDF s požadovanou velikostí stránky
linktitle: Vytvořte graf PDF s požadovanou velikostí stránky
second_title: Aspose.Cells .NET Excel Processing API
description: Vytvořte PDF s grafem Excel pomocí Aspose.Cells pro .NET. Naučte se, jak na to, pomocí tohoto podrobného průvodce.
weight: 12
url: /cs/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte graf PDF s požadovanou velikostí stránky

## Zavedení

Vytváření vizuálně přitažlivých a informativních grafů je nezbytné pro reprezentaci dat v různých oblastech. Ať už pracujete s údaji o prodeji, metrikami výkonu nebo jakýmkoli jiným typem informací, schopnost vytvářet vysoce kvalitní grafy dává vašim zjištěním hloubku a jasnost. Pokud pracujete s aplikacemi .NET, Aspose.Cells je výkonná knihovna, se kterou je manipulace s dokumenty Excelu a generování grafů hračkou. V tomto tutoriálu vás provedeme procesem vytváření PDF s grafem ze souboru aplikace Excel s požadovanou velikostí stránky.

## Předpoklady

Než se ponoříte do kódu, existuje několik předpokladů, které musíte splnit, abyste zajistili hladký průběh:

### Základní znalost C# a .NET

Budete potřebovat základní znalosti programování v C# a frameworku .NET. To vám pomůže pochopit strukturu kódu, se kterou se v této příručce setkáte.

### Aspose.Cells pro .NET

Ujistěte se, že máte nainstalovaný Aspose.Cells for .NET. Veškeré podrobnosti najdete na[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/). 

### Vývojové prostředí

 Nastavte své vývojové prostředí. Může to být Visual Studio nebo jakékoli jiné IDE, které podporuje C#. Stáhněte a nainstalujte knihovnu Aspose.Cells z[stránka ke stažení](https://releases.aspose.com/cells/net/).

### Ukázkový soubor Excel

Budete potřebovat vzorový soubor Excel, který obsahuje alespoň jeden graf. Můžete vytvořit ukázkový soubor nebo si jej stáhnout a použít ho v tomto kurzu.

## Importujte balíčky

Chcete-li začít pracovat s Aspose.Cells, musíte do vaší aplikace C# importovat potřebné jmenné prostory. Postupujte takto:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Tyto obory názvů vám umožňují přístup ke třídám a metodám potřebným k manipulaci se sešity aplikace Excel a jejich obsahem.

Nyní, když máme všechny předpoklady vyřešené, pojďme si proces rozdělit do podrobných kroků.

## Krok 1: Nastavte výstupní a zdrojové adresáře

Chcete-li začít, musíte definovat, kam se uloží výstupní PDF a kde se nachází váš zdrojový dokument Excel.

```csharp
//Výstupní adresář
string outputDir = "Your Output Directory";

//Zdrojový adresář
string sourceDir = "Your Document Directory";
```

Ujistěte se, že jste nahradili "Váš výstupní adresář" a "Váš adresář dokumentů" skutečnými cestami ve vašem systému. To určuje, kam Aspose uloží vygenerované PDF a kde najde soubor Excel.

## Krok 2: Načtěte ukázkový soubor Excel

Dále musíte načíst soubor Excel, který obsahuje graf. Zde je postup:

```csharp
//Načtěte ukázkový soubor Excel obsahující graf.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 The`Workbook` třída je zásadní pro interakci s vaším dokumentem Excel. Ujistěte se, že cesta ukazuje správně na váš soubor Excel – chyba zde zabrání spuštění zbytku kódu.

## Krok 3: Otevřete první pracovní list

Po načtení sešitu je dalším krokem přístup k listu obsahujícímu požadovaný graf.

```csharp
//Přístup k prvnímu listu.
Worksheet ws = wb.Worksheets[0];
```

 V Aspose.Cells jsou listy indexovány od nuly, takže`Worksheets[0]` odkazuje na první list.

## Krok 4: Přístup k prvnímu grafu

Nyní se dostaneme k grafu, který chcete exportovat do PDF. Tento krok předpokládá, že váš list obsahuje alespoň jeden graf.

```csharp
//Přístup k prvnímu grafu uvnitř listu.
Chart ch = ws.Charts[0];
```

Opět se tím přistupuje k prvnímu grafu v listu; ujistěte se, že struktura vašeho listu tomuto přístupu vyhovuje.

## Krok 5: Vytvořte PDF s požadovanou velikostí stránky

Nakonec je čas vytvořit PDF z grafu se zadanou velikostí stránky. Zde je kouzelná čára kódu, která to všechno zvládne:

```csharp
//Vytvořte graf pdf s požadovanou velikostí stránky.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

V tomto kódu:
- PDF se uloží do výstupního adresáře, který jste zadali dříve.
-  Čísla`7, 7` představují šířku a výšku požadované velikosti stránky.
- PageLayoutAlignmentType.Center zajišťuje, že je graf na stránce vycentrován.

## Krok 6: Potvrzující zpráva

Abyste sobě (i ostatním) dali vědět, že vše proběhlo hladce, vložte na konec kódu potvrzovací zprávu:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Tato zpráva se objeví v okně konzoly po dokončení procesu a signalizuje, že vaše PDF bylo vytvořeno bez problémů.

## Závěr

Gratuluji! Právě jste se naučili, jak využít Aspose.Cells pro .NET k vytvoření PDF z grafu obsaženého v souboru aplikace Excel. Tato výkonná knihovna zjednodušuje proces manipulace s dokumenty aplikace Excel a generování vizuálních reprezentací dat, což vám ušetří hodiny ručního formátování. Nezapomeňte prozkoumat množství dalších funkcí, které Aspose.Cells nabízí nad rámec pouhého generování PDF – nikdy nevíte, co může vaše projekty dále vylepšit!

## FAQ

### K čemu slouží Aspose.Cells for .NET?  
Aspose.Cells for .NET se používá k vytváření, úpravám a převodu dokumentů aplikace Excel programově v aplikacích .NET.

### Mohu používat Aspose.Cells zdarma?  
 Ano, Aspose.Cells nabízí a[zkušební verze zdarma](https://releases.aspose.com/) pro účely hodnocení.

### Existuje způsob, jak prodloužit zkušební období nad rámec počátečního období?  
 Můžete požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro rozšířené testování.

### Co když narazím na problémy nebo mám otázky?  
 Na jejich stránkách můžete vyhledat pomoc od komunity Aspose[fórum podpory](https://forum.aspose.com/c/cells/9).

### Jak mohu zakoupit Aspose.Cells?  
 Můžete si koupit Aspose.Cells od[nákupní stránku](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
