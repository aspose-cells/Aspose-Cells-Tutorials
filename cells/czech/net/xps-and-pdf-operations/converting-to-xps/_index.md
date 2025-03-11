---
title: Převod na XPS v .NET
linktitle: Převod na XPS v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se převádět soubory aplikace Excel do formátu XPS pomocí Aspose.Cells for .NET v několika jednoduchých krocích s praktickými příklady kódu.
weight: 10
url: /cs/net/xps-and-pdf-operations/converting-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod na XPS v .NET

## Zavedení
Pokud jde o převod souborů aplikace Excel do formátu XPS, můžete se cítit trochu mimo, zvláště pokud jste ve světě programování nováčkem nebo se teprve ponoříte do vývoje .NET. Ale nebojte se! V této příručce rozebereme proces pomocí Aspose.Cells pro .NET jako profesionál. Až přečtete, budete nejen jasně rozumět tomu, jak to udělat, ale také získáte praktické poznatky, které mohou zlepšit vaše kódovací dovednosti. Takže, pojďme začít!
## Předpoklady
Než se ponoříte do hlubin konverze, ujistěte se, že máte vše, co potřebujete. Zde je to, co budete potřebovat:
1. Visual Studio: Toto je IDE, kde budete psát svůj kód. Ujistěte se, že jej máte nainstalovaný.
2.  Knihovna Aspose.Cells: Tuto knihovnu potřebujete k efektivnímu zpracování souborů aplikace Excel. Můžete si jej stáhnout z[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost .NET: Znalost C# nebo VB.NET vám pomůže lépe porozumět našim příkladům.
4. Soubor aplikace Excel: Připravte si ve svém pracovním adresáři vzorový soubor aplikace Excel (pro tento tutoriál použijeme „Book1.xls“).

## Importujte balíčky
Nyní, když jsme probrali předpoklady, přejděme k importu potřebných balíčků. Import správných jmenných prostorů je zásadní, protože říká kompilátoru, kde najde třídy a metody, které budeme používat.
### Nastavte svůj projekt
První věci jako první! Otevřete Visual Studio a vytvořte nový projekt. Vyberte si konzolovou aplikaci, protože je přímočará a perfektní pro tento druh úkolu.
### Přidejte Aspose.Cells do svého projektu
Chcete-li začít s Aspose.Cells, musíte přidat knihovnu. Postup:
1. Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Klikněte na „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.Cells“ a klikněte na „Instalovat“.
### Importujte požadované jmenné prostory
Na začátku souboru C# budete muset importovat Aspose.Cells. To zahrnuje přidání následujících pomocí direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Pojďme si rozebrat proces převodu souboru Excel do formátu XPS do jednoduchých, zvládnutelných kroků. 
## Krok 1: Definujte svůj adresář dokumentů
Zde zadáte cestu, kde jsou umístěny vaše soubory Excel. To je zásadní, protože kód bude muset vědět, kde najde soubory.
```csharp
string dataDir = "Your Document Directory"; // Nezapomeňte nahradit svou skutečnou cestou
```
## Krok 2: Otevřete soubor aplikace Excel
Nyní načtěte soubor aplikace Excel do objektu Aspose Workbook. Tato akce umožní vašemu programu přístup k datům v tomto souboru aplikace Excel.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Zde vytváříme novou instanci`Workbook` třídy a načtení do ní "Kniha1.xls".
## Krok 3: Otevřete první pracovní list
Dále musíme získat pracovní list, na kterém chceme pracovat. Protože používáme první list, náš kód bude vypadat takto:
```csharp
Worksheet sheet = workbook.Worksheets[0]; // Přístup k prvnímu pracovnímu listu
```
Tento řádek kódu umožňuje přístup k prvnímu listu pro další příkazy.
## Krok 4: Nakonfigurujte možnosti obrázku a tisku
 Nyní musíme definovat, jak chceme vykreslit náš výstup. To zahrnuje vytvoření instance`ImageOrPrintOptions` a nastavení požadovaného výstupního formátu.
```csharp
Aspose.Cells.Rendering.ImageOrPrintOptions options = new Aspose.Cells.Rendering.ImageOrPrintOptions();
options.SaveFormat = SaveFormat.Xps; // Nastavení výstupního formátu na XPS
```
Tento krok říká Aspose, že chceme převést obsah aplikace Excel do formátu XPS.
## Krok 5: Vykreslete list
nastavenými možnostmi je čas vykreslit konkrétní list:
```csharp
Aspose.Cells.Rendering.SheetRender sr = new Aspose.Cells.Rendering.SheetRender(sheet, options);
sr.ToImage(0, dataDir + "out_printingxps.out.xps");
```
 Zde jsme vytvořili a`SheetRender` objekt, který se stará o proces vykreslování. Metoda`ToImage` zpracuje skutečný převod a uloží vykreslený výstup jako "out_printingxps.out.xps".
## Krok 6: Exportujte celý sešit do XPS
Pokud chcete převést celý sešit namísto pouze jednoho listu, můžete provést tento další krok:
```csharp
WorkbookRender wr = new WorkbookRender(workbook, options);
wr.ToImage(dataDir + "out_whole_printingxps.out.xps");
```
Tento fragment kódu umožňuje exportovat celý sešit najednou, což je efektivní, pokud máte k převodu více listů.
## Závěr
Gratuluji! Úspěšně jste převedli soubor aplikace Excel do formátu XPS pomocí knihovny Aspose.Cells v .NET. Může se to zdát jako mnoho kroků, ale každý z nich hraje v tomto procesu zásadní roli. S těmito znalostmi jste dobře vybaveni pro práci se soubory Excel ve vašich aplikacích a jejich optimalizaci pro různé formáty. Takže až se vás příště někdo zeptá, jak převést ty otravné tabulky, budete přesně vědět, co máte dělat!
## FAQ
### Co je formát XPS?
XPS (XML Paper Specification) je pevný formát dokumentu, který zachovává rozložení a vzhled dokumentů.
### Musím si koupit Aspose.Cells, abych je mohl používat?
 Můžete vyzkoušet bezplatnou zkušební verzi Aspose.Cells k dispozici[zde](https://releases.aspose.com/). Poté budete možná muset zakoupit licenci pro plnou funkčnost.
### Mohu převést více souborů aplikace Excel najednou?
Ano, kód můžete přizpůsobit tak, aby procházel více soubory v adresáři a pro každý soubor použít stejnou konverzní logiku.
### Co když potřebuji převést pouze konkrétní listy?
 Můžete zadat index listu, který chcete v`SheetRender` objekt, jak je znázorněno v našich krocích.
### Kde najdu více informací o Aspose.Cells?
 Můžete prozkoumat[dokumentace](https://reference.aspose.com/cells/net/) pro pokročilejší funkce a možnosti dostupné s knihovnou.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
