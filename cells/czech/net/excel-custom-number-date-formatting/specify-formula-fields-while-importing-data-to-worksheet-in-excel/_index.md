---
"description": "V tomto podrobném návodu se naučíte, jak importovat data do excelových listů se zadanými poli vzorců pomocí Aspose.Cells pro .NET."
"linktitle": "Zadání polí vzorců při importu dat do excelového listu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Zadání polí vzorců při importu dat do excelového listu"
"url": "/cs/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zadání polí vzorců při importu dat do excelového listu

## Zavedení

Pokud jde o programovou práci se soubory Excelu, Aspose.Cells pro .NET je neocenitelný nástroj. Poskytuje robustní funkce pro snadné vytváření, úpravy a manipulaci s tabulkami Excelu. Jednou ze zajímavých funkcí, které nabízí, je možnost specifikovat pole vzorců při importu dat do listu Excelu. Představte si, že pracujete na finanční zprávě a potřebujete automaticky vypočítat součty na základě vstupu uživatele. Tento tutoriál vás krok za krokem provede tím, jak toho dosáhnout čistým a přímočarým způsobem.

## Předpoklady

Než se ponoříme do kódu, ujistěte se, že máte vše, co potřebujete. 

1. Visual Studio nebo jakékoli integrované vývojové prostředí (IDE) pro .NET: Ujistěte se, že máte vhodné IDE pro psaní a spouštění kódu C#.
2. Aspose.Cells pro .NET: Budete si muset stáhnout a odkazovat na knihovnu Aspose.Cells ve svém projektu. Můžete si ji stáhnout z [Aspose uvolňuje](https://releases.aspose.com/cells/net/).
3. Základní znalost jazyka C#: Znalost jazyka C# a konceptů objektově orientovaného programování vám pomůže lépe porozumět příkladům.
4. .NET Framework: Tento tutoriál předpokládá, že používáte .NET Framework 4.5 nebo vyšší.

Jakmile splníte všechny předpoklady, pojďme importovat data do excelového listu se zadanými poli vzorců.

## Importovat balíčky

Než začnete psát kód, budete muset importovat potřebný jmenný prostor Aspose.Cells. To se obvykle provádí na začátku vašeho souboru C#:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

To vám umožňuje používat třídy a metody poskytované knihovnou Aspose.Cells, aniž byste jim museli pokaždé přidávat předponu jmenného prostoru.

Rozdělme si celý proces na zvládnutelné kroky:

## Krok 1: Definování výstupního adresáře

Nejprve si musíte určit, kam chcete soubor Excel uložit. Zde je návod, jak to udělat:

```csharp
static string outputDir = "Your Document Directory"; // zde zadejte adresář s dokumenty
```

Nahradit `"Your Document Directory"` vaší skutečnou cestou k souboru. Zde bude uložen vygenerovaný soubor aplikace Excel.

## Krok 2: Vytvoření uživatelem definované třídy pro datové položky

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

Tento `DataItems` Třída bude obsahovat nezpracovaná celá čísla a vzorce, které budeme zapisovat do excelového listu. 

## Krok 3: Inicializace seznamu pro uchovávání datových položek

Seznam použijeme k uložení více instancí našeho `DataItems` třída.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Krok 4: Přidání datových položek do seznamu

Nyní přidejme do našeho seznamu několik položek. Každá položka bude obsahovat dvě čísla a dva vzorce.

```csharp
// Definujte a přidejte každou datovou položku
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Webové stránky Aspose\")";
dis.Add(di);

// Opakujte pro další datové položky.
```

Nezapomeňte si každý přizpůsobit `DataItems` instance s jedinečnými hodnotami a vzorci.

## Krok 5: Vytvořte sešit a pracovní list aplikace Access

Dále vytvořte sešit a otevřete první list, kam nakonec importujeme data.

```csharp
Workbook wb = new Workbook(); // vytvořit nový sešit
Worksheet ws = wb.Worksheets[0]; // přístup k prvnímu pracovnímu listu
```

## Krok 6: Zadejte možnosti importu tabulky

A tady se děje ta zázrak. Musíte určit, která pole ve vašich datech odpovídají vzorcům. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

V tomto příkladu poslední dvě pole obsahují vzorce, což je označeno symbolem `true`, zatímco první dvě pole jsou nastavena na `false`.

## Krok 7: Import vlastních objektů

Nyní, když je vše nastaveno, importujme náš seznam datových položek do listu.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Tento řádek efektivně importuje data počínaje buňkou A1.

## Krok 8: Výpočet vzorců

Protože jsme importovali některé vzorce, je nezbytné je vypočítat.

```csharp
wb.CalculateFormula();
```

Tato metoda zajišťuje, že vaše vzorce jsou vyhodnocovány na základě jejich závislostí.

## Krok 9: Automatické přizpůsobení sloupcům

Abyste zajistili, že se vaše data budou zobrazovat správně, můžete automaticky přizpůsobit sloupce na základě obsahu.

```csharp
ws.AutoFitColumns();
```

Tento krok optimalizuje rozvržení souboru aplikace Excel. 

## Krok 10: Uložte soubor aplikace Excel

Konečně je čas uložit nově vytvořený soubor aplikace Excel. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Ujistěte se, že název výstupního souboru je relevantní a popisný!

## Krok 11: Kontrola provedení

Jako jednoduchý způsob, jak ověřit, že vše proběhlo správně, můžete vytisknout zprávu.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Díky tomu máte okamžitou zpětnou vazbu, že kód fungoval bez problémů.

## Závěr

tady to máte! Úspěšně jste importovali data do excelového listu pomocí Aspose.Cells pro .NET a zadaných polí vzorců. Dodržováním těchto kroků můžete použít podobné techniky k automatizaci úloh zpracování dat přizpůsobených vašim potřebám. Ať už zpracováváte čísla pro reporty nebo jednoduše spravujete data, zvládnutí umění manipulace s Excelem pomocí Aspose je dovednost, která stojí za to.

## Často kladené otázky

### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET určená pro programově vytvářet, manipulovat a převádět soubory aplikace Excel.

### Jak nainstaluji Aspose.Cells pro .NET?
Můžete si ho stáhnout z [Aspose uvolňuje](https://releases.aspose.com/cells/net/) a odkazujte na něj ve svém projektu.

### Mohu používat Aspose.Cells zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi dostupnou na [tento odkaz](https://releases.aspose.com/).

### Kde najdu další příklady?
Další příklady a dokumentaci naleznete na [Stránka s dokumentací k Aspose](https://reference.aspose.com/cells/net/).

### Co když se při používání Aspose setkám s problémy?
Pomoc můžete vyhledat na fóru podpory Aspose. [zde](https://forum.aspose.com/c/cells/9).
 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}