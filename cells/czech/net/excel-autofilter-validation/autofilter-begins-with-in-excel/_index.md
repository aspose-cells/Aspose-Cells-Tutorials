---
"description": "Naučte se, jak bez námahy automaticky filtrovat řádky Excelu pomocí Aspose.Cells v .NET s tímto komplexním podrobným návodem."
"linktitle": "Automatický filtr začíná v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Automatický filtr začíná v Excelu"
"url": "/cs/net/excel-autofilter-validation/autofilter-begins-with-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatický filtr začíná v Excelu

## Zavedení

Pokud jde o práci s daty, Excel se etabloval jako běžná aplikace pro nespočet odvětví a účelů. Jednou z jeho nejvýkonnějších funkcí je automatický filtr, který usnadňuje procházení rozsáhlých datových sad. Pokud používáte Aspose.Cells pro .NET, můžete tuto funkci programově využít a výrazně vylepšit své úkoly správy dat. V této příručce vás provedeme procesem implementace funkce, která filtruje řádky Excelu na základě toho, zda začínají určitým řetězcem.

## Předpoklady

Než se do toho pustíte, ujistěte se, že máte splněny následující předpoklady:

1. Vývojové prostředí: Seznamte se s vývojovým prostředím .NET. Může to být Visual Studio nebo jakékoli jiné IDE dle vašeho výběru.
2. Aspose.Cells pro .NET: Musíte mít nainstalovaný Aspose.Cells pro .NET. Pokud jste tak ještě neučinili, můžete si ho snadno stáhnout. [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# a práce s knihovnami .NET vám pomůže bez problémů sledovat daný text.
4. Ukázková data: Měli byste mít soubor aplikace Excel, nejlépe s názvem `sourseSampleCountryNames.xlsx`, který se nachází ve vámi určeném zdrojovém adresáři. Tento soubor bude obsahovat data, která budeme filtrovat.
5. Licence: Pro plnou funkčnost zvažte získání licence prostřednictvím této [odkaz](https://purchase.aspose.com/buy)Pokud chcete funkce otestovat, můžete požádat o [dočasná licence](https://purchase.aspose.com/temporary-license/).

Máte všechno připravené? Pojďme na to!

## Importovat balíčky

Chcete-li začít, importujte potřebné jmenné prostory v horní části souboru C#:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Tím se importuje základní funkcionalita Aspose.Cells spolu se základními systémovými funkcemi, na které se budeme spoléhat pro interakci s konzolí.

Nyní, když máte nastavené prostředí a importované potřebné balíčky, pojďme rozdělit funkci automatického filtrování do snadno zvládnutelných kroků. Implementujeme filtr, který extrahuje řádky začínající na „Ba“.

## Krok 1: Definování zdrojového a výstupního adresáře

Nejprve si definujme, kde se nachází náš vstupní soubor Excel a také kam chceme uložit náš filtrovaný výstup:

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory\\";

// Výstupní adresář
string outputDir = "Your Document Directory\\";
```

Vysvětlení: Zde nahraďte `"Your Document Directory\\"` se skutečnou cestou k vašim adresářům. Ujistěte se, že cesty k adresářům ukončíte dvojitým zpětným lomítkem (`\\`), abyste se vyhnuli problémům s cestou.

## Krok 2: Vytvoření instance objektu Workbook

Dále vytvoříme objekt Workbook, který bude odkazovat na náš soubor aplikace Excel:

```csharp
// Vytvoření instance objektu Workbook obsahujícího vzorová data
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

Vysvětlení: Tento řádek inicializuje novou instanci sešitu pomocí zadané cesty k souboru. `Workbook` Třída je základní, protože představuje celý soubor aplikace Excel.

## Krok 3: Přístup k prvnímu pracovnímu listu

Nyní potřebujeme přistupovat ke konkrétnímu pracovnímu listu, se kterým chceme pracovat:

```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```

Vysvětlení: `Worksheets` kolekce nám umožňuje přístup k jednotlivým listům. Použití `[0]` odkazuje na první list v souboru aplikace Excel, což je obecně běžná praxe při práci s jedním listem souboru.

## Krok 4: Nastavení automatického filtru

A tady začíná kouzlo! Vytvoříme pro naše data rozsah automatického filtru:

```csharp
// Vytvoření automatického filtru zadáním rozsahu buněk
worksheet.AutoFilter.Range = "A1:A18";
```

Vysvětlení: `AutoFilter.Range` Vlastnost umožňuje určit, které řádky se mají filtrovat. V tomto případě filtrujeme řádky v rozsahu A1 až A18, u kterých se předpokládá, že obsahují naše data.

## Krok 5: Použití podmínky filtru

Dalším krokem je definování podmínky filtru. Chceme zobrazit pouze ty řádky, jejichž hodnoty v prvním sloupci začínají na „Ba“:

```csharp
// Inicializovat filtr pro řádky začínající řetězcem „Ba“
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

Vysvětlení: `Custom` Metoda definuje naši logiku filtrování. První argument (`0`) označuje, že filtrujeme na základě prvního sloupce (A) a `FilterOperatorType.BeginsWith` určuje naši podmínku pro hledání řádků začínajících na „Ba“.

## Krok 6: Obnovte filtr

Po použití podmínky filtru se musíme ujistit, že se Excel aktualizuje, aby se změny projevily:

```csharp
// Aktualizujte filtr pro zobrazení/skrytí filtrovaných řádků
worksheet.AutoFilter.Refresh();
```

Vysvětlení: Tento řádek vyvolá aktualizaci automatického filtru, aby se zajistilo, že viditelné řádky odpovídají použitým kritériím filtru. Je to podobné jako stisknutí tlačítka pro aktualizaci v Excelu.

## Krok 7: Uložení upraveného souboru aplikace Excel

Nyní je čas uložit provedené změny:

```csharp
// Uložení upraveného souboru aplikace Excel
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

Vysvětlení: `Save` Metoda zapíše upravený sešit zpět do zadané výstupní cesty. To spadá pod zápis definovaných filtrů do nového souboru, aby původní data zůstala zachována.

## Krok 8: Potvrzení výstupu

Nakonec si ověřme, že naše operace proběhla úspěšně:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Vysvětlení: Tento jednoduchý řádek vypíše do konzole potvrzovací zprávu, která vás informuje, že proces filtrování byl dokončen bez chyb.

## Závěr

Ve světě, kde se správa dat může zdát ohromující, vám zvládnutí funkcí, jako je automatický filtr v Excelu prostřednictvím Aspose.Cells pro .NET, umožní efektivně a účinně manipulovat s daty. Naučili jste se, jak filtrovat řádky Excelu začínající na „Ba“, a postupně jste tuto metodu implementovali. S praxí budete schopni tuto metodu přizpůsobit různým potřebám filtrování dat ve vašich probíhajících projektech.

## Často kladené otázky

### K čemu slouží automatický filtr v Excelu?  
Automatický filtr umožňuje uživatelům rychle třídit a filtrovat data v tabulce, což usnadňuje zaměření na konkrétní datové sady.

### Mohu filtrovat na základě více kritérií pomocí Aspose.Cells?  
Ano, Aspose.Cells podporuje pokročilé možnosti filtrování, které umožňují nastavit více kritérií.

### Potřebuji licenci pro používání Aspose.Cells?  
I když můžete začít s bezplatnou zkušební verzí, pro plnou funkčnost a odstranění jakýchkoli omezení zkušební verze je vyžadována licence.

### Jaké typy filtrování mohu provádět pomocí Aspose.Cells?  
Data můžete filtrovat podle hodnoty, podmínky (například začíná na nebo končí na) a přizpůsobit filtrování tak, aby splňovalo vaše specifické požadavky.

### Kde najdu více informací o Aspose.Cells pro .NET?  
Můžete si prohlédnout dokumentaci [zde](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}