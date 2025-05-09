---
"description": "Naučte se, jak převést soubory Excelu do formátu XPS pomocí Aspose.Cells pro .NET v několika snadných krocích s praktickými příklady kódu."
"linktitle": "Převod do XPS v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Převod do XPS v .NET"
"url": "/cs/net/xps-and-pdf-operations/converting-to-xps/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Převod do XPS v .NET

## Zavedení
Pokud jde o převod souborů Excelu do formátu XPS, můžete se cítit trochu mimo své znalosti, zvláště pokud jste ve světě programování nováčkem nebo se teprve pouštíte do vývoje v .NET. Ale nebojte se! V této příručce si celý proces s využitím Aspose.Cells pro .NET rozebereme jako profesionál. Až dočtete, budete mít nejen jasnou představu o tom, jak na to, ale také získáte praktické poznatky, které vám mohou pomoci zlepšit vaše programátorské dovednosti. Tak pojďme na to!
## Předpoklady
Než se ponoříme do detailů konverze, ujistěme se, že máte vše, co potřebujete. Zde je to, co budete potřebovat:
1. Visual Studio: Toto je vývojové prostředí (IDE), kde budete psát kód. Ujistěte se, že ho máte nainstalované.
2. Knihovna Aspose.Cells: Tuto knihovnu potřebujete pro efektivní práci se soubory aplikace Excel. Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost .NET: Znalost C# nebo VB.NET vám pomůže lépe porozumět našim příkladům.
4. Soubor Excel: Mějte připravený vzorový soubor Excel (pro tento tutoriál použijeme „Book1.xls“) ve svém pracovním adresáři.

## Importovat balíčky
Nyní, když jsme si probrali předpoklady, pojďme k importu potřebných balíčků. Import správných jmenných prostorů je klíčový, protože kompilátoru říká, kde má najít třídy a metody, které budeme používat.
### Nastavení projektu
Nejdříve to nejdůležitější! Otevřete Visual Studio a vytvořte nový projekt. Vyberte konzolovou aplikaci, protože je přímočará a pro tento typ úkolu ideální.
### Přidejte Aspose.Cells do svého projektu
Abyste mohli začít s Aspose.Cells, musíte přidat knihovnu. Postupujte takto:
1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Klikněte na „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.Cells“ a klikněte na „Instalovat“.
### Importujte požadované jmenné prostory
Na začátek vašeho C# souboru budete muset importovat Aspose.Cells. To zahrnuje přidání následujících direktiv using:
```csharp
using System.IO;
using Aspose.Cells;
```
Pojďme si rozebrat proces převodu souboru aplikace Excel do formátu XPS na jednoduché a snadno zvládnutelné kroky. 
## Krok 1: Definujte adresář dokumentů
Zde zadáte cestu, kde se nacházejí vaše soubory aplikace Excel. To je zásadní, protože kód bude potřebovat vědět, kde soubory najít.
```csharp
string dataDir = "Your Document Directory"; // Nezapomeňte nahradit skutečnou cestou
```
## Krok 2: Otevřete soubor aplikace Excel
Nyní si načtěme váš soubor Excel do objektu Aspose Workbook. Tato akce umožní vašemu programu přístup k datům uvnitř tohoto souboru Excel.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Zde vytváříme novou instanci třídy `Workbook` třídu a načtení souboru „Book1.xls“ do ní.
## Krok 3: Přístup k prvnímu pracovnímu listu
Dále si musíme sehnat pracovní list, na kterém chceme pracovat. Protože používáme první pracovní list, bude náš kód vypadat takto:
```csharp
Worksheet sheet = workbook.Worksheets[0]; // Přístup k prvnímu listu
```
Tento řádek kódu vám umožňuje přístup k prvnímu listu pro další příkazy.
## Krok 4: Konfigurace možností obrázku a tisku
Nyní musíme definovat, jak chceme vykreslit náš výstup. To zahrnuje vytvoření instance třídy `ImageOrPrintOptions` a nastavení požadovaného výstupního formátu.
```csharp
Aspose.Cells.Rendering.ImageOrPrintOptions options = new Aspose.Cells.Rendering.ImageOrPrintOptions();
options.SaveFormat = SaveFormat.Xps; // Nastavení výstupního formátu na XPS
```
Tento krok sdělí Aspose, že chceme převést obsah aplikace Excel do formátu XPS.
## Krok 5: Vykreslení listu
Po nastavení možností je čas vykreslit konkrétní list:
```csharp
Aspose.Cells.Rendering.SheetRender sr = new Aspose.Cells.Rendering.SheetRender(sheet, options);
sr.ToImage(0, dataDir + "out_printingxps.out.xps");
```
Zde jsme vytvořili `SheetRender` objekt, který se stará o proces vykreslování. Metoda `ToImage` zpracovává samotnou konverzi a ukládá vykreslený výstup jako „out_printingxps.out.xps“.
## Krok 6: Export celého sešitu do formátu XPS
Pokud chcete převést celý sešit namísto pouze jednoho listu, můžete postupovat podle tohoto dalšího kroku:
```csharp
WorkbookRender wr = new WorkbookRender(workbook, options);
wr.ToImage(dataDir + "out_whole_printingxps.out.xps");
```
Tento úryvek kódu umožňuje exportovat celý sešit najednou, což je efektivní, pokud máte k převodu více listů.
## Závěr
Gratulujeme! Úspěšně jste převedli soubor aplikace Excel do formátu XPS pomocí knihovny Aspose.Cells v .NET. Může se to zdát jako spousta kroků, ale každý z nich hraje v tomto procesu zásadní roli. S těmito znalostmi jste dobře vybaveni pro práci s excelovými soubory ve vašich aplikacích a jejich optimalizaci pro různé formáty. Takže až se vás příště někdo zeptá, jak převést ty otravné tabulky, budete přesně vědět, co dělat!
## Často kladené otázky
### Co je formát XPS?
XPS (XML Paper Specification) je formát dokumentů s pevným formátem, který zachovává rozvržení a vzhled dokumentů.
### Musím si pro použití Aspose.Cells zakoupit?
Můžete si vyzkoušet bezplatnou zkušební verzi Aspose.Cells [zde](https://releases.aspose.com/)Poté si pro plnou funkčnost možná budete muset zakoupit licenci.
### Mohu převést více souborů aplikace Excel najednou?
Ano, kód můžete upravit tak, aby procházel více soubory v adresáři a pro každý soubor použil stejnou logiku převodu.
### Co když potřebuji převést pouze konkrétní listy?
Můžete zadat index požadovaného listu v `SheetRender` objekt, jak je znázorněno v našich krocích.
### Kde najdu více informací o Aspose.Cells?
Můžete prozkoumat [dokumentace](https://reference.aspose.com/cells/net/) pro pokročilejší funkce a možnosti dostupné v knihovně.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}