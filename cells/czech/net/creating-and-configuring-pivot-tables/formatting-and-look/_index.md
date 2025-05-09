---
"description": "Vylepšete si pivotové tabulky v Excelu pomocí Aspose.Cells pro .NET. Naučte se bez námahy formátovat, upravovat a automatizovat prezentaci dat."
"linktitle": "Programové formátování a vzhled kontingenčních tabulek v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové formátování a vzhled kontingenčních tabulek v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/formatting-and-look/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové formátování a vzhled kontingenčních tabulek v .NET

## Zavedení
Kontingenční tabulky jsou fantastické nástroje v Excelu, které uživatelům umožňují shrnovat a analyzovat složité datové sady. Dokážou transformovat běžná data do vizuálně atraktivních a informativních sestav, což uživatelům umožňuje rychle získat potřebné informace. V tomto tutoriálu se podíváme na to, jak manipulovat se styly kontingenčních tabulek pomocí Aspose.Cells pro .NET, což vám umožní bez námahy automatizovat a přizpůsobovat sestavy v Excelu. Jste připraveni zlepšit své dovednosti v prezentaci dat? Pojďme se do toho pustit!
## Předpoklady
Než se na tuto cestu vydáme, je třeba mít připraveno několik základních věcí:
1. Visual Studio: Toto bude naše hlavní prostředí pro kódování a testování.
2. Aspose.Cells pro .NET: Ujistěte se, že máte tuto knihovnu nainstalovanou. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže snadno se orientovat.
4. Soubor aplikace Excel: Budete potřebovat existující soubor aplikace Excel, který obsahuje kontingenční tabulku. Pokud ji nemáte, můžete si jednoduchou vytvořit pomocí aplikace Microsoft Excel.
Jakmile máte vše nastavené, pojďme k importu potřebných balíčků!
## Importovat balíčky
Abychom mohli začít, musíme importovat požadované knihovny do našeho projektu v C#. Zde je návod, jak to udělat:
### Vytvoření nového projektu v C#
Nejprve otevřete Visual Studio a vytvořte nový projekt konzolové aplikace. To nám umožní snadno spustit náš kód.
### Přidat reference
Jakmile je váš projekt nastaven, budete muset přidat odkaz na knihovnu Aspose.Cells:
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte balíček.
Po dokončení jste připraveni importovat jmenný prostor Aspose.Cells. Níže je uveden kód pro import potřebných balíčků:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Nyní, když jsme importovali naše balíčky, se pojďme blíže podívat na to, jak manipulovat s formátováním kontingenční tabulky v Excelu.
## Krok 1: Nastavení adresáře dokumentů
Nejprve definujeme cestu k našemu souboru aplikace Excel. Zde je návod, jak to udělat:
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Nezapomeňte vyměnit `"Your Document Directory"` se skutečnou cestou, kde je uložen váš soubor Excel.
## Krok 2: Načtení sešitu
Dále musíme načíst váš existující soubor Excelu. V tomto kroku využijeme `Workbook` třída poskytovaná Aspose.Cells.
```csharp
// Načíst soubor šablony
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Když vyměníte `"Book1.xls"` s vaším skutečným názvem souboru, `workbook` Objekt bude nyní obsahovat data z aplikace Excel.
## Krok 3: Přístup k pracovnímu listu a kontingenční tabulce
Nyní si chceme stáhnout list a pivotní tabulku, se kterými budeme pracovat:
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
var pivot = workbook.Worksheets[0].PivotTables[0];
```
tomto případě používáme první list a první kontingenční tabulku. Pokud váš soubor aplikace Excel obsahuje více listů nebo kontingenčních tabulek, nezapomeňte odpovídajícím způsobem upravit hodnoty indexů.

Nyní, když máme přístup k pivotní tabulce, je čas ji vizuálně vylepšit! Můžeme nastavit styl a formátovat celou pivotní tabulku. Zde je postup:
## Krok 4: Nastavení stylu kontingenční tabulky
Použijme na naši kontingenční tabulku předdefinovaný styl:
```csharp
pivot.PivotTableStyleType = PivotTableStyleType.PivotTableStyleDark1;
```
Tento řádek kódu změní styl kontingenční tabulky na tmavý motiv. Můžete prozkoumat různé styly dostupné v knihovně Aspose.Cells a najít ten, který vyhovuje vašim potřebám.
## Krok 5: Úprava stylu kontingenční tabulky
Pro další úpravy si můžeme vytvořit vlastní styl. To je skvělé? Zde je návod, jak to udělat:
```csharp
Style style = workbook.CreateStyle();
style.Font.Name = "Arial Black";
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
```
V tomto úryvku:
- Jako písmo uvádíme „Arial Black“.
- Barva popředí je nastavena na žlutou.
- Vzor jsme nastavili na plný.
## Krok 6: Použití vlastního stylu na kontingenční tabulku
Nakonec aplikujme tento nově vytvořený styl k formátování celé kontingenční tabulky:
```csharp
pivot.FormatAll(style);
```
Tento řádek aplikuje váš vlastní styl na všechna data v kontingenční tabulce. Vaše tabulka by nyní měla vypadat fantasticky!
## Krok 7: Uložte změny
Jakmile dokončíte formátování kontingenční tabulky, nezapomeňte změny uložit. Zde je návod, jak dokument uložit:
```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "output.xls");
```
Nahradit `"output.xls"` s libovolným názvem pro nově naformátovaný soubor aplikace Excel. A voilà! Úspěšně jste naformátovali kontingenční tabulku pomocí Aspose.Cells pro .NET.
## Závěr
Stručně řečeno, vydali jsme se na cestu programově formátovat kontingenční tabulky v Excelu pomocí Aspose.Cells pro .NET. Začali jsme importem potřebných balíčků, načtením existujícího sešitu aplikace Excel, úpravou stylů kontingenčních tabulek a nakonec uložením formátovaného výstupu. Integrací těchto dovedností do vašeho pracovního postupu můžete automatizovat zdlouhavé úlohy formátování, které vás mohou stát drahocenný čas. Tak proč to nezkusit? Vyzkoušejte si to sami a posuňte své znalosti Excelu na vyšší úroveň!
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro manipulaci s excelovými soubory v .NET aplikacích, která umožňuje snadné provádění automatizovaných a programových úloh.
### Mohu si Aspose.Cells vyzkoušet zdarma?
Ano! Zkušební verzi zdarma můžete spustit kliknutím [zde](https://releases.aspose.com).
### Jaké typy stylů pivotních tabulek jsou k dispozici?
Aspose.Cells nabízí různé předdefinované styly, ke kterým lze přistupovat prostřednictvím `PivotTableStyleType`.
### Jak mohu v Excelu vytvořit kontingenční tabulku?
Kontingenční tabulku v Excelu můžete vytvořit pomocí karty „Vložit“ na panelu nástrojů a výběrem možnosti „Kontrolní tabulka“.
### Kde mohu získat podporu pro Aspose.Cells?
Pomoc můžete najít na fóru Aspose [zde](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}