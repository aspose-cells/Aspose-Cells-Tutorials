---
title: Při importu dat do listu aplikace Excel zadejte pole vzorců
linktitle: Při importu dat do listu aplikace Excel zadejte pole vzorců
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném kurzu se dozvíte, jak importovat data do listů aplikace Excel se zadanými poli vzorců pomocí Aspose.Cells for .NET.
weight: 11
url: /cs/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Při importu dat do listu aplikace Excel zadejte pole vzorců

## Zavedení

Pokud jde o programové zpracování souborů aplikace Excel, Aspose.Cells for .NET je neocenitelný nástroj. Poskytuje robustní funkce pro snadné vytváření, úpravy a manipulaci s tabulkami aplikace Excel. Jednou ze zajímavých funkcí, které nabízí, je možnost specifikovat pole vzorců při importu dat do listu aplikace Excel. Představte si, že pracujete na finanční zprávě a potřebujete automaticky vypočítat součty na základě uživatelského vstupu. Tento tutoriál vás krok za krokem provede, jak toho dosáhnout čistým a přímočarým přístupem.

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte vše, co potřebujete. 

1. Visual Studio nebo jakékoli integrované vývojové prostředí (IDE) .NET: Ujistěte se, že máte vhodné IDE pro psaní a spouštění kódu C#.
2.  Aspose.Cells for .NET: Budete si muset stáhnout a odkazovat na knihovnu Aspose.Cells ve svém projektu. Můžete si jej stáhnout z[Aspose vydání](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost C# a objektově orientovaného programování vám pomůže lépe porozumět příkladům.
4. .NET Framework: Tento kurz předpokládá, že používáte rozhraní .NET Framework 4.5 nebo vyšší.

Jakmile máte vytříděné předpoklady, přistoupíme k importu některých dat do listu Excelu se zadanými poli vzorců.

## Importujte balíčky

Než začnete psát svůj kód, budete muset importovat potřebný jmenný prostor Aspose.Cells. To se obvykle provádí v horní části souboru C#:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

To vám umožňuje používat třídy a metody poskytované knihovnou Aspose.Cells, aniž byste je pokaždé museli předponovat jmenným prostorem.

Pojďme si celý proces rozdělit do zvládnutelných kroků:

## Krok 1: Definujte výstupní adresář

Nejprve musíte určit, kam chcete soubor Excel uložit. Můžete to udělat takto:

```csharp
static string outputDir = "Your Document Directory"; // zde zadejte svůj adresář dokumentů
```

 Nahradit`"Your Document Directory"` s vaší skutečnou cestou k souboru. Zde se uloží vygenerovaný soubor Excel.

## Krok 2: Vytvořte uživatelem definovanou třídu pro datové položky

Dále definujeme třídu pro strukturování dat, která plánujeme importovat.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Tento`DataItems` třída bude obsahovat nezpracovaná celá čísla a vzorce, které zapíšeme do listu Excel. 

## Krok 3: Inicializujte seznam pro uložení datových položek

 Použijeme seznam k uložení více instancí našeho`DataItems` třída.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Krok 4: Přidejte datové položky do seznamu

Nyní přidáme několik položek do našeho seznamu. Každý záznam bude obsahovat dvě čísla a dva vzorce.

```csharp
// Definujte a přidejte každou datovou položku
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Web Aspose\")";
dis.Add(di);

// Opakujte pro další datové položky
```

 Ujistěte se, že si každý přizpůsobíte`DataItems` instance s jedinečnými hodnotami a vzorci.

## Krok 5: Vytvořte sešit a Access Worksheet

Dále vytvořte sešit a otevřete první list, do kterého nakonec importujeme data.

```csharp
Workbook wb = new Workbook(); // vytvořit nový sešit
Worksheet ws = wb.Worksheets[0]; // přístup k prvnímu pracovnímu listu
```

## Krok 6: Určete možnosti importu tabulky

Tady se děje kouzlo. Musíte určit, která pole ve vašich datech odpovídají vzorcům. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 V tomto příkladu poslední dvě pole obsahují vzorce, což je označeno`true` , zatímco první dvě pole jsou nastavena na`false`.

## Krok 7: Import vlastních objektů

Nyní, když je vše nastaveno, importujme náš seznam datových položek do listu.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Tento řádek efektivně importuje data počínaje buňkou A1.

## Krok 8: Vypočítejte vzorce

Protože jsme importovali některé vzorce, je důležité je vypočítat.

```csharp
wb.CalculateFormula();
```

Tato metoda zajišťuje, že vaše vzorce jsou vyhodnoceny na základě jejich závislostí.

## Krok 9: Automatické přizpůsobení sloupců

Abyste zajistili, že se vaše data budou zobrazovat dobře, můžete sloupce automaticky přizpůsobit podle obsahu.

```csharp
ws.AutoFitColumns();
```

Tento krok optimalizuje rozložení souboru Excel. 

## Krok 10: Uložte soubor Excel

Konečně je čas uložit nově vytvořený soubor Excel. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Ujistěte se, že váš výstupní název souboru je relevantní a popisný!

## Krok 11: Kontrola provedení

Jako jednoduchý způsob, jak ověřit, že vše proběhlo správně, můžete vytisknout zprávu.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

To vám dává okamžitou zpětnou vazbu, že kód fungoval bez problémů.

## Závěr

tady to máte! Úspěšně jste importovali data do listu aplikace Excel pomocí Aspose.Cells for .NET a zadaných polí vzorců. Podle těchto kroků můžete použít podobné techniky k automatizaci úloh zpracování dat přizpůsobených vašim potřebám. Ať už zpracováváte čísla pro sestavy nebo jednoduše udržujete data, zvládnutí umění manipulace s Excelem s Aspose je dovednost, kterou stojí za to mít.

## FAQ

### Co je Aspose.Cells?
Aspose.Cells je .NET knihovna určená pro vytváření, manipulaci a převod souborů aplikace Excel programově.

### Jak nainstaluji Aspose.Cells pro .NET?
 Můžete si jej stáhnout z[Aspose vydání](https://releases.aspose.com/cells/net/) a odkazujte na něj ve svém projektu.

### Mohu používat Aspose.Cells zdarma?
 Ano, Aspose nabízí bezplatnou zkušební verzi dostupnou na[tento odkaz](https://releases.aspose.com/).

### Kde najdu další příklady?
 Další příklady a dokumentaci naleznete na[Aspose dokumentační stránku](https://reference.aspose.com/cells/net/).

### Co když při používání Aspose narazím na problémy?
 Pomoc můžete vyhledat na fóru podpory Aspose[zde](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
