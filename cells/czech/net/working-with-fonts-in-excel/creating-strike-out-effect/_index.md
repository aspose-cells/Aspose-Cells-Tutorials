---
"description": "Naučte se v tomto podrobném návodu krok za krokem, jak v Excelu pomocí Aspose.Cells pro .NET aplikovat efekt přeškrtnutí na text."
"linktitle": "Vytvoření efektu přeškrtnutí textu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Vytvoření efektu přeškrtnutí textu v Excelu"
"url": "/cs/net/working-with-fonts-in-excel/creating-strike-out-effect/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření efektu přeškrtnutí textu v Excelu

## Zavedení
Excelu jsou vizuální prvky stejně důležité jako samotná data. Ať už zvýrazňujete důležité změny nebo označujete položky, které již nejsou relevantní, efekt přeškrtnutí textu je klasický způsob správy vizuální reprezentace v tabulkách. V této příručce vás provedeme procesem implementace efektu přeškrtnutí textu v Excelu pomocí Aspose.Cells pro .NET. Tento tutoriál nejen pokryje nezbytné předpoklady, ale také vám poskytne podrobný postup, který vám zajistí snadnou replikaci tohoto efektu.
## Předpoklady
Než se pustíte do tutoriálu, ujistěte se, že máte splněny následující předpoklady:
1. Vývojové prostředí: Měli byste mít nastavené vývojové prostředí pro .NET. Může to být Visual Studio nebo jakékoli jiné IDE, které preferujete a které podporuje vývoj v .NET.
2. Aspose.Cells pro .NET: Ujistěte se, že máte ve svém projektu nainstalovaný Aspose.Cells. Můžete si ho stáhnout z následujícího odkazu: [Stáhnout Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Základní znalost programování v C# je užitečná, protože příklady budou kódovány v C#.
4. .NET Framework: Ujistěte se, že váš projekt cílí na kompatibilní verzi .NET Framework, obvykle .NET Core nebo .NET Framework 4.5 a vyšší.
## Importovat balíčky
Než začnete psát jakýkoli kód, je třeba importovat požadované jmenné prostory z Aspose.Cells. To je klíčové pro přístup k různým funkcím poskytovaným knihovnou. Zde je návod, jak importovat potřebné jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
```
Díky těmto importům budete mít přístup ke třídám Workbook, Worksheet a Style, které budou v tomto tutoriálu použity.
Nyní, když jsme si připravili půdu, pojďme si proces rozdělit na zvládnutelné kroky. Každý krok bude doprovázen jasnými pokyny, které vás provedou vytvořením efektu přeškrtnutí textu v Excelu.
## Krok 1: Definování adresáře dokumentů
Začněte definováním cesty, kam budou uloženy vaše dokumenty aplikace Excel. Toto bude umístění pro ukládání výstupních souborů.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou k adresáři, kam chcete uložit soubor Excel. Tím se nastaví adresář pro váš výstup.
## Krok 2: Vytvořte adresář
Dále je třeba ověřit, zda adresář, který jste zadali v předchozím kroku, existuje. Pokud neexistuje, můžete jej programově vytvořit.
```csharp
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento kód zkontroluje, zda adresář existuje, a pokud ne, vytvoří ho. To pomáhá předejít chybám při pozdějším pokusu o uložení souboru.
## Krok 3: Vytvoření instance objektu Workbook
Nyní je čas vytvořit nový objekt Sešit. To je základ vašeho souboru aplikace Excel, kam budete přidávat data a používat formáty.
```csharp
// Vytvoření instance objektu Workbook
Workbook workbook = new Workbook();
```
Ten/Ta/To `Workbook` Třída představuje soubor aplikace Excel. Vytvořením instance této třídy v podstatě vytváříte nový dokument aplikace Excel.
## Krok 4: Přidání nového pracovního listu
Každý sešit může obsahovat více listů. Pojďme si ve vašem sešitu vytvořit nový list.
```csharp
// Přidání nového listu do objektu aplikace Excel
int i = workbook.Worksheets.Add();
```
Ten/Ta/To `Add` metoda `Worksheets` Kolekce přidá do sešitu nový list a vrátí jeho index. 
## Krok 5: Získejte referenční číslo nového pracovního listu
Jakmile vytvoříte pracovní list, musíte na něj odkazovat pro budoucí operace.
```csharp
// Získání odkazu na nově přidaný list předáním jeho indexu listu
Worksheet worksheet = workbook.Worksheets[i];
```
Zde načítáte nově vytvořený pracovní list pomocí jeho indexu (`i`). To vám umožní přístup k manipulaci s pracovním listem.
## Krok 6: Přístup k buňce
Budete chtít otevřít konkrétní buňku v listu, kde použijete formát přeškrtnutí. V tomto příkladu používáme buňku `A1`.
```csharp
// Přístup k buňce „A1“ z listu
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
V Excelu se na buňky odkazuje pomocí identifikátorů sloupců a řádků (např. „A1“). Získáváme odkaz na buňku `A1` pro další manipulaci.
## Krok 7: Přidání hodnoty do buňky
Dále vložíme do buňky nějaký text. Do buňky napíšeme „Ahoj Aspose!“. `A1`.
```csharp
// Přidání hodnoty do buňky „A1“
cell.PutValue("Hello Aspose!");
```
Ten/Ta/To `PutValue` Metoda se používá k přiřazení řetězcové hodnoty buňce. Tento řetězec můžete upravit na cokoli, co chcete zobrazit.
## Krok 8: Získejte styl buňky
Nyní, když máme v buňce text, je čas přejít ke stylu buňky a použít požadované formátování, včetně efektu přeškrtnutí.
```csharp
// Získání stylu buňky
Style style = cell.GetStyle();
```
Ten/Ta/To `GetStyle` Metoda načte aktuální styl buňky, což umožňuje upravit vlastnosti, jako je typ písma, velikost a efekty.
## Krok 9: Nastavení efektu přeškrtnutí
Použijme efekt přeškrtnutí na text v buňce. Upravíme styl písma buňky.
```csharp
// ExStart:SetStrikeout
// Nastavení efektu přeškrtnutí písma
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
Nastavením `IsStrikeout` na hodnotu true, dáváte Excelu pokyn, aby vizuálně přeškrtl text ve vybrané buňce – podobně jako když vizuálně vyznačíte něco v seznamu.
## Krok 10: Použití stylu na buňku
Po úpravě stylu je nutné jej znovu použít na buňku, aby se změny projevily.
```csharp
// Použití stylu na buňku
cell.SetStyle(style);
```
Ten/Ta/To `SetStyle` Metoda aktualizuje buňku novým stylem, který nyní zahrnuje formátování přeškrtnutých textů.
## Krok 11: Uložte soubor Excel
Konečně je čas uložit sešit do zadaného adresáře. V tomto příkladu ukládáme soubor s názvem `book1.out.xls`.
```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Ten/Ta/To `Save` Metoda zapíše sešit na disk ve formátu aplikace Excel 97-2003. V případě potřeby můžete zadat jiné formáty.
## Závěr
Vytvoření efektu přeškrtnutí textu v Excelu pomocí Aspose.Cells pro .NET je jednoduchý proces, když si ho rozeberete krok za krokem. Dodržováním tohoto návodu nyní získáte dovednosti, jak vylepšit své tabulky vizuálními pomůckami, díky nimž budou vaše data nejen informativní, ale i vizuálně poutavá.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro správu souborů aplikace Excel v aplikacích .NET, která umožňuje programově vytvářet, manipulovat a převádět dokumenty aplikace Excel.
### Mohu používat Aspose.Cells zdarma?
Ano, můžete jej používat zdarma během zkušební doby. Bezplatná zkušební verze je k dispozici na adrese [Bezplatná zkušební verze Aspose.Cells](https://releases.aspose.com/).
### Jak si mohu zakoupit Aspose.Cells?
Licenci pro Aspose.Cells si můžete zakoupit prostřednictvím jejich webových stránek. [Koupit Aspose.Cells](https://purchase.aspose.com/buy).
### Jsou k dispozici příklady použití Aspose.Cells?
Ano, v tomto odkazu najdete spoustu příkladů a úryvků kódu. [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/).
### Kde mohu získat podporu pro Aspose.Cells?
Podporu a pomoc komunity můžete získat od [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}