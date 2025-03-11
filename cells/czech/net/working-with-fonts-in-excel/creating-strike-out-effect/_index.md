---
title: Vytvoření efektu přeškrtnutí textu v aplikaci Excel
linktitle: Vytvoření efektu přeškrtnutí textu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak aplikovat efekt přeškrtnutí na text v Excelu pomocí Aspose.Cells for .NET v tomto podrobném podrobném tutoriálu.
weight: 15
url: /cs/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření efektu přeškrtnutí textu v aplikaci Excel

## Zavedení
Pokud jde o Excel, vizuální prvky jsou stejně důležité jako samotná data. Ať už zvýrazňujete důležité změny nebo označujete položky, které již nejsou relevantní, efekt přeškrtnutí textu je klasickým způsobem správy vizuální reprezentace v tabulkách. V této příručce vás provedeme procesem implementace efektu přeškrtnutí textu v aplikaci Excel pomocí Aspose.Cells for .NET. Tento výukový program nejen pokryje nezbytné předpoklady, ale také poskytne postup krok za krokem, abyste zajistili, že tento efekt můžete snadno replikovat.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte splněny následující předpoklady:
1. Vývojové prostředí: Měli byste mít nastavené vývojové prostředí .NET. Může to být Visual Studio nebo jakékoli jiné preferované IDE, které podporuje vývoj .NET.
2. Aspose.Cells for .NET: Ujistěte se, že máte ve svém projektu nainstalovaný Aspose.Cells. Můžete si jej stáhnout z následujícího odkazu:[Stáhněte si Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost programování v C# je užitečná, protože příklady budou kódovány v C#.
4. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi .NET Framework, obvykle .NET Core nebo .NET Framework 4.5 a vyšší.
## Importujte balíčky
Než napíšete jakýkoli kód, musíte importovat požadované jmenné prostory z Aspose.Cells. To je zásadní pro přístup k různým funkcím, které knihovna poskytuje. Zde je návod, jak importovat potřebné jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
```
S těmito importy budete mít přístup ke třídám Workbook, Worksheet a Style, které budou použity v tomto kurzu.
Nyní, když jsme připravili scénu, rozdělme proces do zvládnutelných kroků. Každý krok bude doprovázen jasnými pokyny, které vás provedou vytvořením efektu přeškrtnutí textu v Excelu.
## Krok 1: Definujte adresář dokumentů
Začněte definováním cesty, kde budou uloženy vaše excelové dokumenty. Toto bude místo pro uložení vašich výstupních souborů.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou k adresáři, kam chcete soubor Excel uložit. Tím nastavíte adresář pro váš výstup.
## Krok 2: Vytvořte adresář
Dále se musíte ujistit, že adresář, který jste zadali v předchozím kroku, existuje. Pokud neexistuje, můžete jej vytvořit programově.
```csharp
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento kód zkontroluje, zda adresář existuje, a pokud ne, vytvoří jej. To pomáhá vyhnout se chybám při pozdějším pokusu o uložení souboru.
## Krok 3: Vytvořte instanci objektu sešitu
Nyní je čas vytvořit nový objekt Sešit. Toto je základ vašeho souboru Excel, kam budete přidávat data a používat formáty.
```csharp
// Vytvoření instance objektu sešitu
Workbook workbook = new Workbook();
```
 The`Workbook` třída představuje soubor Excel. Vytvořením instance této třídy v podstatě vytváříte nový dokument aplikace Excel.
## Krok 4: Přidejte nový list
Každý sešit může obsahovat více listů. Pokračujme a vytvořte nový list ve vašem sešitu.
```csharp
// Přidání nového listu do objektu aplikace Excel
int i = workbook.Worksheets.Add();
```
 The`Add` metoda`Worksheets` kolekce přidá do sešitu nový list a vrátí jeho index. 
## Krok 5: Získejte odkaz na nový pracovní list
Jakmile vytvoříte list, musíte na něj odkazovat pro budoucí operace.
```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[i];
```
Zde načítáte nově vytvořený list pomocí jeho indexu (`i`). To vám dává přístup k manipulaci s listem.
## Krok 6: Přístup k buňce
 Budete chtít získat přístup ke konkrétní buňce v listu, kde použijete formát přeškrtnutí. V tomto příkladu používáme cell`A1`.
```csharp
// Přístup k buňce "A1" z listu
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 V Excelu se na buňky odkazuje pomocí identifikátorů sloupců a řádků (např. "A1"). Získáváme odkaz na buňku`A1` pro další manipulaci.
## Krok 7: Přidejte hodnotu do buňky
 Dále do buňky vložíme nějaký text. Napíšeme "Ahoj Aspose!" v buňce`A1`.
```csharp
// Přidání nějaké hodnoty do buňky "A1".
cell.PutValue("Hello Aspose!");
```
 The`PutValue` metoda se používá k přiřazení řetězcové hodnoty buňce. Tento řetězec můžete upravit na cokoli, co chcete zobrazit.
## Krok 8: Získejte styl buňky
Nyní, když máme v buňce text, je čas otevřít styl buňky a použít požadované formátování, včetně efektu přeškrtnutí.
```csharp
// Získání stylu buňky
Style style = cell.GetStyle();
```
 The`GetStyle` metoda načte aktuální styl buňky, což vám umožní upravit vlastnosti, jako je typ písma, velikost a efekty.
## Krok 9: Nastavte efekt přeškrtnutí
Aplikujme efekt přeškrtnutí na text v buňce. Upravíme styl písma buňky.
```csharp
// ExStart:SetStrikeout
// Nastavení efektu přeškrtnutí na písmu
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
 Nastavením`IsStrikeout` pravda, dáváte Excelu pokyn, aby vizuálně přeškrtl text ve vybrané buňce – podobně jako když vizuálně označíte něco ze seznamu.
## Krok 10: Použijte styl na buňku
Po úpravě stylu je třeba jej aplikovat zpět na buňku, aby odrážel změny.
```csharp
// Použití stylu na buňku
cell.SetStyle(style);
```
 The`SetStyle` metoda aktualizuje buňku novým stylem, který nyní obsahuje přeškrtnuté formátování.
## Krok 11: Uložte soubor Excel
 Nakonec je čas uložit sešit do určeného adresáře. V tomto příkladu ukládáme soubor s názvem`book1.out.xls`.
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 The`Save`metoda zapíše sešit na disk ve formátu Excel 97-2003. V případě potřeby můžete zadat různé formáty.
## Závěr
Vytvoření efektu přeškrtnutí textu v Excelu pomocí Aspose.Cells for .NET je jednoduchý proces, když jej rozeberete krok za krokem. Podle této příručky nyní máte dovednosti vylepšit své tabulky vizuálními podněty, díky nimž budou vaše data nejen informativní, ale také vizuálně poutavá.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro správu souborů aplikace Excel v aplikacích .NET, která vám umožňuje programově vytvářet, manipulovat a převádět dokumenty aplikace Excel.
### Mohu používat Aspose.Cells zdarma?
 Ano, během zkušební doby jej můžete používat zdarma. Bezplatná zkušební verze je k dispozici na adrese[Bezplatná zkušební verze Aspose.Cells](https://releases.aspose.com/).
### Jak koupím Aspose.Cells?
 Licenci pro Aspose.Cells si můžete zakoupit prostřednictvím jejich webových stránek[Koupit Aspose.Cells](https://purchase.aspose.com/buy).
### Jsou k dispozici příklady použití Aspose.Cells?
 Ano, můžete najít spoustu příkladů a úryvků kódu v[Dokumentace Aspose.Cells](https://reference.aspose.com/cells/net/).
### Kde mohu získat podporu pro Aspose.Cells?
 Můžete získat podporu a pomoc od komunity[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
