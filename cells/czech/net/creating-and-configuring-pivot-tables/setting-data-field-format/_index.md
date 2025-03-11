---
title: Nastavení formátu datového pole programově v .NET
linktitle: Nastavení formátu datového pole programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Hlavní nastavení formátů datových polí v kontingenčních tabulkách pomocí Aspose.Cells for .NET s tímto podrobným výukovým programem. Vylepšete formátování dat v Excelu.
weight: 19
url: /cs/net/creating-and-configuring-pivot-tables/setting-data-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení formátu datového pole programově v .NET

## Zavedení
Pokud se ponoříte do manipulace se soubory Excelu pomocí .NET, pravděpodobně jste se setkali s datovými sadami, které vyžadují nějaké efektní formátování. Jedním z běžných požadavků je nastavit datová pole, zejména v kontingenčních tabulkách, způsobem, který zajistí, že vaše data budou nejen srozumitelná, ale také vizuálně přitažlivá a přehledná. S Aspose.Cells pro .NET může být tento úkol hračkou. V tomto tutoriálu doslova rozebereme, jak programově nastavit formáty datových polí v .NET krok za krokem, zpochybníme skličující složitosti a uděláme vše stravitelné!
## Předpoklady
Než se vydáme na tuto cestu, ujistěte se, že máte vše vyřešeno. Zde je rychlý kontrolní seznam toho, co potřebujete:
1. Visual Studio: Protože kdo by neměl rád dobré integrované vývojové prostředí (IDE)?
2.  Aspose.Cells for .NET Library: Můžete si ji snadno stáhnout z[Stránka Aspose Releases](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Pokud rozumíte základům programovacího jazyka, můžete začít!
### Proč Aspose.Cells?
Aspose.Cells for .NET je výkonná knihovna speciálně navržená pro správu operací se soubory aplikace Excel. Umožňuje vám snadno číst, psát, manipulovat a převádět soubory Excel. Představte si, že byste mohli programově vytvářet sestavy, kontingenční tabulky nebo dokonce grafy, aniž byste se museli ponořit do uživatelského rozhraní Excelu – zní to jako kouzlo, že?
## Importujte balíčky
Nyní, když máme všechny předpoklady nastavené, pojďme se vrhnout na další kroky. Začněte importem potřebných balíčků. Zde je návod, jak je můžete uvést do provozu:
### Vytvořit nový projekt
Otevřete Visual Studio a vytvořte nový projekt C#. Vyberte šablonu konzolové aplikace, protože my budeme provádět backendové zpracování.
### Přidejte odkaz do Aspose.Cells
1. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte „Spravovat balíčky NuGet“.
3. V části Procházet vyhledejte „Aspose.Cells“.
4. Nainstalujte knihovnu. Po instalaci jste připraveni k importu!
### Importujte požadované jmenné prostory
V horní části souboru kódu C# přidejte následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
To vám umožní přístup k funkcím nabízeným Aspose.Cells.

Dobře, teď se dostáváme k tomu podstatnému z našeho programu. Budeme pracovat s existujícím souborem Excel — pro účely tohoto tutoriálu jej pojmenujme „Book1.xls“.
## Krok 1: Definujte svůj datový adresář
Nejprve musíte svému programu sdělit, kde najde tento vzácný soubor Excel.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory"; // Nezapomeňte to změnit na svou skutečnou cestu!
```
## Krok 2: Načtěte sešit
Načtení sešitu je podobné jako otevření knihy před jejím čtením. Postup je následující:
```csharp
// Načtěte soubor šablony
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Ujistěte se, že Book1.xls sedí pěkně v určeném adresáři, jinak můžete narazit na pár škytavek!
## Krok 3: Otevřete první pracovní list
Nyní, když máme náš sešit, dáme si do rukou první pracovní list (jako obálku naší knihy):
```csharp
// Získejte první pracovní list
Worksheet worksheet = workbook.Worksheets[0]; // Index začíná na 0!
```
## Krok 4: Otevřete kontingenční tabulku
S pracovním listem, který máme v rukou, je čas najít kontingenční tabulku, se kterou potřebujeme pracovat.
```csharp
int pivotindex = 0; // Za předpokladu, že chcete první kontingenční tabulku
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
## Krok 5: Získejte datová pole
Nyní, když jsme v kontingenční tabulce, vytáhneme datová pole. Představte si to jako jít do knihovny a načíst konkrétní knihy (nebo datová pole).
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.DataFields;
```
## Krok 6: Přístup k prvnímu datovému poli
Z kolekce polí můžeme přistupovat k prvnímu. Je to jako vybrat z police první knihu ke čtení.
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0]; // Získejte první datové pole
```
## Krok 7: Nastavte formát zobrazení dat
Dále nastavíme formát zobrazení dat kontingenčního pole. Zde můžete začít zobrazovat smysluplné vizuální prvky – například procenta:
```csharp
// Nastavení formátu zobrazení dat
pivotField.DataDisplayFormat = Aspose.Cells.Pivot.PivotFieldDataDisplayFormat.PercentageOf;
```
## Krok 8: Nastavte základní pole a základní položku
Každé pivotní pole může být svázáno s jiným polem jako základní reference. Pojďme to nastavit:
```csharp
//Nastavení základního pole
pivotField.BaseFieldIndex = 1; // Použijte vhodný index pro základní pole
// Nastavení základní položky
pivotField.BaseItemPosition = Aspose.Cells.Pivot.PivotItemPosition.Next; // Vyberte další položku
```
## Krok 9: Nastavte formát čísla
Když to vezmeme o krok dále, upravíme formát čísel. Je to podobné jako rozhodování o tom, jak chcete čísla zobrazovat – pojďme je udělat úhledně!
```csharp
// Nastavení formátu čísel
pivotField.Number = 10; // Podle potřeby použijte index formátu
```
## Krok 10: Uložte soubor Excel
Vše nastaveno a hotovo! Je čas uložit změny. Váš sešit nyní bude odrážet všechny mocné změny, které jste právě provedli.
```csharp
// Uložení souboru Excel
workbook.Save(dataDir + "output.xls");
```
A tady to máte, lidi! Datová pole vaší kontingenční tabulky jsou nyní naformátována k dokonalosti!
## Závěr
Gratuluji! Právě jste prošli výukovým programem o programovém nastavení formátů datových polí v .NET pomocí Aspose.Cells. S každým krokem jsme odstranili vrstvy složitosti, což vám umožňuje dynamicky interagovat s Excelem, upravovat kontingenční tabulky a zobrazovat data v použitelných formátech. Pokračujte ve cvičení, prozkoumejte další funkce.
## FAQ
### Mohu použít Aspose.Cells k vytvoření souborů aplikace Excel od začátku?
Absolutně! Pomocí Aspose.Cells můžete od základu vytvářet a manipulovat se soubory aplikace Excel.
### Je k dispozici bezplatná zkušební verze?
 Ano! Můžete se podívat na[Bezplatná zkušební verze](https://releases.aspose.com/).
### Jaké formáty podporuje Aspose.Cells pro soubory Excel?
Podporuje různé formáty včetně XLS, XLSX, CSV a dalších.
### Musím za licenci platit?
 Máte několik možností! Licenci si můžete zakoupit na[Koupit stránku](https://purchase.aspose.com/buy) . Případně a[Dočasná licence](https://purchase.aspose.com/temporary-license/) je také k dispozici.
### Kde najdu podporu, když mám problémy?
 Podporu na nich najdete[Fórum podpory](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
