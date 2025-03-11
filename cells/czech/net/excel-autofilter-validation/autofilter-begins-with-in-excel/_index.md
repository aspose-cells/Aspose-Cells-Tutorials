---
title: Automatický filtr začíná v Excelu
linktitle: Automatický filtr začíná v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak bez námahy automaticky filtrovat řádky aplikace Excel pomocí Aspose.Cells v .NET pomocí tohoto podrobného průvodce krok za krokem.
weight: 10
url: /cs/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatický filtr začíná v Excelu

## Zavedení

Pokud jde o práci s daty, Excel se etabloval jako běžná aplikace pro nespočet průmyslových odvětví a účelů. Jednou z jeho nejvýkonnějších funkcí je AutoFilter, díky kterému je prohledávání rozsáhlých datových sad hračkou. Pokud používáte Aspose.Cells pro .NET, můžete tuto funkci využít programově a výrazně vylepšit úkoly správy dat. V této příručce vás provedeme procesem implementace funkce, která filtruje řádky Excelu podle toho, zda začínají určitým řetězcem.

## Předpoklady

Před potápěním se ujistěte, že máte splněny následující předpoklady:

1. Vývojové prostředí: Seznamte se s vývojovým prostředím .NET. Může to být Visual Studio nebo jakékoli jiné IDE podle vašeho výběru.
2.  Aspose.Cells for .NET: Musíte mít nainstalovaný Aspose.Cells for .NET. Pokud jste to ještě neudělali, můžete si jej pohodlně stáhnout[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost C# a práce s knihovnami .NET vám pomůže hladce pokračovat.
4.  Ukázková data: Měli byste mít soubor Excel, nejlépe pojmenovaný`sourseSampleCountryNames.xlsx`, který se nachází ve vámi určeném zdrojovém adresáři. Tento soubor bude obsahovat data, která budeme filtrovat.
5.  Licencování: Pro plnou funkčnost zvažte pořízení licence prostřednictvím tohoto[odkaz](https://purchase.aspose.com/buy) . Pokud chcete otestovat funkce, můžete požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/).

Máte vše připraveno? Jdeme na to!

## Importujte balíčky

Chcete-li začít, importujte potřebné jmenné prostory v horní části souboru C#:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Tím se importuje základní funkce Aspose.Cells spolu se základními funkcemi systému, na které se budeme spoléhat při interakci s konzolí.

Nyní, když máte nastavené prostředí a importované potřebné balíčky, pojďme rozdělit funkci automatického filtru do zvládnutelných kroků. Budeme implementovat filtr, který extrahuje řádky začínající na „Ba“.

## Krok 1: Definujte zdrojové a výstupní adresáře

Nejprve definujme, kde se nachází náš vstupní soubor Excel, a také kam chceme uložit filtrovaný výstup:

```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory\\";

// Výstupní adresář
string outputDir = "Your Document Directory\\";
```

 Vysvětlení: Zde nahraďte`"Your Document Directory\\"` se skutečnou cestou k vašim adresářům. Ujistěte se, že končíte cesty k adresáři dvojitým zpětným lomítkem (`\\`), abyste se vyhnuli problémům s cestou.

## Krok 2: Vytvořte instanci objektu sešitu

Dále vytvoříme objekt Workbook, který ukazuje na náš soubor Excel:

```csharp
// Vytvoření instance objektu Workbook obsahujícího ukázková data
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 Vysvětlení: Tento řádek inicializuje novou instanci sešitu pomocí zadané cesty k souboru. The`Workbook` třída je základní, protože představuje celý soubor Excel.

## Krok 3: Přístup k prvnímu listu

Nyní musíme získat přístup ke konkrétnímu listu, se kterým chceme pracovat:

```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Worksheet worksheet = workbook.Worksheets[0];
```

 Vysvětlení: The`Worksheets` kolekce nám umožňuje přístup k jednotlivým listům. Použití`[0]` odkazuje na první list v souboru Excel, což je obecně běžná praxe při práci se souborem s jedním listem.

## Krok 4: Nastavení automatického filtru

Tady začíná kouzlo! Vytvoříme rozsah automatického filtru pro naše data:

```csharp
// Vytvoření automatického filtru zadáním rozsahu buněk
worksheet.AutoFilter.Range = "A1:A18";
```

 Vysvětlení: The`AutoFilter.Range` vlastnost umožňuje určit, které řádky se mají filtrovat. V tomto případě filtrujeme řádky v rozsahu A1 až A18, o kterých se předpokládá, že obsahují naše data.

## Krok 5: Použijte podmínku filtru

Dalším krokem je definování podmínky filtru. Chceme zobrazit pouze ty řádky, jejichž hodnoty prvního sloupce začínají "Ba":

```csharp
// Inicializovat filtr pro řádky začínající řetězcem "Ba"
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 Vysvětlení: The`Custom` metoda definuje naši logiku filtrování. První argument (`0` ) znamená, že filtrujeme na základě prvního sloupce (A) a`FilterOperatorType.BeginsWith` určuje naši podmínku hledat řádky začínající na "Ba".

## Krok 6: Obnovte filtr

Po použití naší podmínky filtru se musíme ujistit, že se Excel aktualizuje, aby odrážel změny:

```csharp
// Obnovením filtru zobrazíte/skryjete filtrované řádky
worksheet.AutoFilter.Refresh();
```

Vysvětlení: Tento řádek vyvolá aktualizaci automatického filtru, aby se zajistilo, že viditelné řádky odpovídají kritériím použitého filtru. Je to podobné, jako když stisknete tlačítko aktualizace v Excelu.

## Krok 7: Uložte upravený soubor Excel

Nyní je čas uložit změny, které jsme provedli:

```csharp
// Uložení upraveného souboru Excel
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 Vysvětlení: The`Save` metoda zapíše upravený sešit zpět do zadané výstupní cesty. To spadá pod zápis vámi definovaných filtrů do nového souboru, takže vaše původní data zůstanou nedotčena.

## Krok 8: Potvrzení výstupu

Nakonec potvrďte, že naše operace byla úspěšná:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Vysvětlení: Tento jednoduchý řádek odešle do konzole potvrzovací zprávu, která vám dá vědět, že proces filtrování byl dokončen bez chyb.

## Závěr

Ve světě, kde se správa dat může zdát ohromující, vám ovládání funkcí, jako je Automatický filtr v Excelu prostřednictvím Aspose.Cells for .NET, umožňuje efektivně a efektivně manipulovat s daty. Naučili jste se, jak filtrovat řádky Excelu, které začínají na „Ba“, přičemž metodu implementujete krok za krokem. S praxí budete schopni přizpůsobit tuto metodu různým potřebám filtrování dat ve vašich probíhajících projektech.

## FAQ

### Jaký je účel automatického filtru v Excelu?  
Automatický filtr umožňuje uživatelům rychle třídit a filtrovat data v tabulkovém procesoru, což usnadňuje zaměření na konkrétní soubory dat.

### Mohu pomocí Aspose.Cells filtrovat na základě více kritérií?  
Ano, Aspose.Cells podporuje pokročilé možnosti filtrování, které vám umožní nastavit více kritérií.

### Potřebuji licenci pro Aspose.Cells, abych ji mohl používat?  
I když můžete začít s bezplatnou zkušební verzí, pro plnou funkčnost a odstranění jakýchkoli omezení zkušební verze je vyžadována licence.

### Jaké typy filtrování mohu provádět pomocí Aspose.Cells?  
Data můžete filtrovat podle hodnoty, podmínky (např. začíná nebo končí na) a vlastního filtrování, aby vyhovovala vašim konkrétním požadavkům.

### Kde najdu další informace o Aspose.Cells pro .NET?  
 Můžete zkontrolovat dokumentaci[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
