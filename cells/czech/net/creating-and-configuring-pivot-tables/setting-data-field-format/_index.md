---
"description": "Zvládněte nastavení formátů datových polí v kontingenčních tabulkách pomocí Aspose.Cells pro .NET s tímto podrobným návodem. Vylepšete formátování dat v Excelu."
"linktitle": "Programové nastavení formátu datových polí v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Programové nastavení formátu datových polí v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/setting-data-field-format/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programové nastavení formátu datových polí v .NET

## Zavedení
Pokud se pouštíte do manipulace s excelovými soubory v .NET, pravděpodobně jste se setkali s datovými sadami, které vyžadují trochu složitějšího formátování. Jedním z běžných požadavků je nastavení datových polí, zejména v kontingenčních tabulkách, takovým způsobem, aby vaše data byla nejen srozumitelná, ale také vizuálně přitažlivá a přehledná. S Aspose.Cells pro .NET může být tento úkol hračka. V tomto tutoriálu si doslova krok za krokem rozebereme, jak programově nastavit formáty datových polí v .NET, a zvládneme tak složité úkoly a zároveň je uděláme stravitelnými!
## Předpoklady
Než se na tuto cestu vydáme, ujistěme se, že máte vše vyřešeno. Zde je stručný kontrolní seznam toho, co budete potřebovat:
1. Visual Studio: Protože kdo by nemiloval dobré integrované vývojové prostředí (IDE)?
2. Knihovna Aspose.Cells pro .NET: Můžete si ji snadno stáhnout z [Stránka s vydáními Aspose](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Pokud rozumíte základům programovacího jazyka, můžete začít!
### Proč Aspose.Cells?
Aspose.Cells pro .NET je výkonná knihovna speciálně navržená pro správu operací s Excelovými soubory. Umožňuje vám snadno číst, zapisovat, manipulovat s Excelovými soubory a převádět je. Představte si, že byste mohli programově vytvářet sestavy, kontingenční tabulky nebo dokonce grafy, aniž byste se museli hrabat v uživatelském rozhraní Excelu – zní to jako kouzlo, že?
## Importovat balíčky
Nyní, když máme všechny předpoklady nastavené, pojďme se ponořit do dalších kroků. Začněte importem potřebných balíčků. Zde je návod, jak je spustit:
### Vytvořit nový projekt
Otevřete Visual Studio a vytvořte nový projekt v C#. Vyberte šablonu konzolové aplikace, protože budeme provádět backendové zpracování.
### Přidat odkaz na Aspose.Cells
1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. V sekci Procházet vyhledejte „Aspose.Cells“.
4. Nainstalujte knihovnu. Po instalaci můžete začít s importem!
### Importujte požadované jmenné prostory
V horní části souboru kódu C# přidejte následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Tím získáte přístup k funkcím, které nabízí Aspose.Cells.

Dobře, teď se dostáváme k podstatě našeho programu. Budeme pracovat s existujícím souborem aplikace Excel – pro účely tohoto tutoriálu ho pojmenujeme „Book1.xls“.
## Krok 1: Definujte svůj datový adresář
V první řadě musíte programu sdělit, kde má najít ten drahocenný soubor aplikace Excel.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory"; // Nezapomeňte to změnit na svou skutečnou cestu!
```
## Krok 2: Načtení sešitu
Načtení sešitu je podobné jako otevření knihy před jejím přečtením. Postupujte takto:
```csharp
// Načíst soubor šablony
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Ujistěte se, že soubor Book1.xls je správně umístěn v zadaném adresáři, jinak můžete narazit na pár problémů!
## Krok 3: Přístup k prvnímu pracovnímu listu
Teď, když máme pracovní sešit, pojďme se pustit do prvního pracovního listu (jako obálky naší knihy):
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0]; // Index začíná na 0!
```
## Krok 4: Přístup k kontingenční tabulce
S pracovním listem v rukou je čas najít kontingenční tabulku, se kterou budeme pracovat.
```csharp
int pivotindex = 0; // Za předpokladu, že chcete první pivotní tabulku
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
## Krok 5: Získejte datová pole
Teď, když jsme v kontingenční tabulce, pojďme vytáhnout datová pole. Představte si to, jako byste šli do knihovny a vyhledali konkrétní knihy (nebo datová pole).
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.DataFields;
```
## Krok 6: Přístup k prvnímu datovému poli
Z kolekce polí můžeme přistupovat k prvnímu. Je to jako vybrat si první knihu z police, kterou si přečteme.
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0]; // Získat první datové pole
```
## Krok 7: Nastavení formátu zobrazení dat
Dále nastavíme formát zobrazení dat v pivotním poli. Zde můžete začít zobrazovat smysluplné vizuály – například procenta:
```csharp
// Nastavení formátu zobrazení dat
pivotField.DataDisplayFormat = Aspose.Cells.Pivot.PivotFieldDataDisplayFormat.PercentageOf;
```
## Krok 8: Nastavení základního pole a základní položky
Každé pivotní pole lze propojit s jiným polem jako základní referencí. Nastavme to:
```csharp
// Nastavení základního pole
pivotField.BaseFieldIndex = 1; // Použijte vhodný index pro základní pole
// Nastavení základní položky
pivotField.BaseItemPosition = Aspose.Cells.Pivot.PivotItemPosition.Next; // Vyberte další položku
```
## Krok 9: Nastavení formátu čísla
Půjdeme o krok dál a upravme formát čísel. Je to podobné jako rozhodování o tom, jak chcete, aby se čísla zobrazovala – udělejme je úhledné!
```csharp
// Nastavení formátu čísla
pivotField.Number = 10; // Použijte index formátu podle potřeby
```
## Krok 10: Uložte soubor Excel
Hotovo! Čas uložit změny. Váš sešit nyní bude odrážet všechny důležité změny, které jste právě provedli.
```csharp
// Uložení souboru aplikace Excel
workbook.Save(dataDir + "output.xls");
```
A tady to máte, přátelé! Datová pole vaší kontingenční tabulky jsou nyní naformátována k dokonalosti!
## Závěr
Gratulujeme! Právě jste úspěšně zvládli tutoriál o programovém nastavování formátů datových polí v .NET pomocí Aspose.Cells. S každým krokem jsme odstraňovali vrstvy složitosti, což vám umožňuje dynamicky interagovat s Excelem, upravovat kontingenční tabulky a zobrazovat data v akčních formátech. Pokračujte v procvičování a prozkoumejte další funkce.
## Často kladené otázky
### Mohu použít Aspose.Cells k vytvoření souborů aplikace Excel od nuly?
Rozhodně! S Aspose.Cells můžete vytvářet a manipulovat s excelovými soubory od základů.
### Je k dispozici bezplatná zkušební verze?
Ano! Můžete se podívat na [Bezplatná zkušební verze](https://releases.aspose.com/).
### Jaké formáty souborů Excelu podporuje Aspose.Cells?
Podporuje různé formáty včetně XLS, XLSX, CSV a dalších.
### Musím platit za licenci?
Máte několik možností! Licenci si můžete zakoupit na [Koupit stránku](https://purchase.aspose.com/buy)Alternativně, a [Dočasná licence](https://purchase.aspose.com/temporary-license/) je také k dispozici.
### Kde mohu najít podporu, pokud mám problémy?
Podporu u nich najdete [Fórum podpory](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}