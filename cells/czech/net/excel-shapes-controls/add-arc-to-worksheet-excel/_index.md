---
"description": "Naučte se přidávat oblouky do excelových listů pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného návodu a vylepšete návrhy svých tabulek."
"linktitle": "Přidání oblouku do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání oblouku do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání oblouku do listu v Excelu

## Zavedení
Vytváření vizuálně atraktivních tabulek v Excelu je pro prezentaci dat klíčové a knihovna Aspose.Cells poskytuje vývojářům robustní nástroje k provedení tohoto úkolu. Jednou zajímavou funkcí, kterou byste mohli chtít začlenit do svých dokumentů v Excelu, je možnost přidávat tvary, například oblouky. V tomto tutoriálu si krok za krokem ukážeme, jak přidat oblouky do listu v Excelu pomocí Aspose.Cells pro .NET. Na konci tohoto článku se nejen naučíte, jak přidávat oblouky, ale také získáte přehled o správě tvarů obecně.
## Předpoklady
Než se ponoříme do složitostí přidávání oblouků do pracovního listu, je nezbytné se ujistit, že máte připraveno několik věcí. Zde jsou předpoklady, které budete potřebovat k zahájení:
1. Visual Studio: Budete muset mít na počítači nainstalované Visual Studio, protože budeme používat C# jako programovací jazyk.
2. .NET Framework: Ujistěte se, že máte nainstalovaný .NET Framework nebo .NET Core. Aspose.Cells podporuje oba.
3. Aspose.Cells pro .NET: Musíte mít knihovnu Aspose.Cells. Můžete si ji stáhnout z [Soubory ke stažení Aspose.Cells](https://releases.aspose.com/cells/net/) strana.
4. Základní znalost jazyka C#: Znalost jazyka C# vám pomůže sledovat úryvky kódu bez větších potíží.
## Importovat balíčky
Abyste mohli ve svém projektu začít pracovat s Aspose.Cells, musíte importovat potřebné balíčky. Postupujte takto:
### Vytvořit nový projekt
- Otevřete Visual Studio.
- Vyberte možnost „Vytvořit nový projekt“.
- Vyberte šablonu, která funguje s .NET (například konzolová aplikace).
  
### Přidat odkazy na Aspose.Cells
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte jej.
Nyní jste připraveni začít kódovat sčítání oblouku.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Zde je podrobný rozpis kódu, který ukazuje, jak přidat oblouky do listu v Excelu.
## Krok 1: Nastavení adresáře
Prvním krokem je nastavení adresáře, kam uložíte soubor Excel. To vám pomůže snadno spravovat výstupní soubory.
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
V tomto úryvku kódu určíme cestu k adresáři s dokumenty. Také zkontrolujeme, zda adresář existuje; pokud ne, vytvoříme ho. Tím se vytvoří základ pro náš výstup.
## Krok 2: Vytvoření instance sešitu
Dále si vytvořme novou instanci sešitu.
```csharp
// Vytvořte instanci nového sešitu.
Workbook excelbook = new Workbook();
```
Tento řádek vytvoří nový sešit aplikace Excel. Představte si ho jako prázdné plátno, kam můžeme přidávat tvary, data a další prvky.
## Krok 3: Přidání prvního obloukového tvaru
Nyní přidejme do pracovního listu náš první obloukový tvar.
```csharp
// Přidejte obloukový tvar.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Zde přidáváme oblouk do prvního listu. Parametry definují polohu a velikost oblouku: `(left, top, width, height, startAngle, endAngle)`Je to jako vykreslovat segment kruhu!
## Krok 4: Přizpůsobení prvního oblouku
Po přidání oblouku můžete chtít upravit jeho vzhled.
```csharp
// Nastavení barvy výplně tvaru
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Nastavte umístění oblouku.
arc1.Placement = PlacementType.FreeFloating;           
// Nastavte tloušťku čáry.
arc1.Line.Weight = 1;      
// Nastavte styl čárkování oblouku.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
V této části upravíme oblouk. Nastavíme typ výplně na plnou barvu (v tomto případě modrou), definujeme způsob umístění, určíme tloušťku čáry a zvolíme styl čar. V podstatě upravíme náš oblouk tak, aby byl vizuálně přitažlivý!
## Krok 5: Přidání druhého obloukového tvaru
Přidejme další obloukový tvar pro lepší kontext.
```csharp
// Přidejte další obloukový tvar.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Podobně jako u prvního oblouku přidáváme na stejný list druhý oblouk. Souřadnice jsou zde trochu posunuty, aby se umístil jinak.
## Krok 6: Přizpůsobení druhého oblouku
Stejně jako u prvního oblouku, upravíme i ten druhý.
```csharp
// Nastavení barvy čáry
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Nastavte umístění oblouku.
arc2.Placement = PlacementType.FreeFloating;          
// Nastavte tloušťku čáry.
arc2.Line.Weight = 1;           
// Nastavte styl čárkování oblouku.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde dáváme druhému oblouku stejný styl jako prvnímu. Barvu nebo styl můžete změnit dle libosti pro jedinečnost nebo tematické účely.
## Krok 7: Uložení sešitu
Konečně je čas uložit nově vytvořený sešit s oblouky.
```csharp
// Uložte soubor Excelu.
excelbook.Save(dataDir + "book1.out.xls");
```
Tento řádek funguje jako stisknutí tlačítka pro uložení. Ukládáme naši práci do zadaného umístění s určeným názvem souboru. Nezapomeňte zkontrolovat adresář, abyste viděli své mistrovské dílo ve formátu Excel!
## Závěr
tomto tutoriálu jsme prozkoumali proces přidávání obloukových tvarů do listu aplikace Excel pomocí Aspose.Cells pro .NET. Prostřednictvím jednoduchého podrobného návodu jste se naučili, jak vytvořit nový sešit, přidat oblouky, přizpůsobit jejich vzhled a uložit dokument. Tato funkce nejen vylepšuje vizuální atraktivitu vašich tabulek, ale také činí vaše prezentace dat informativnějšími. Ať už vytváříte grafy, zprávy nebo jen experimentujete, použití tvarů, jako jsou oblouky, může vašim projektům dodat kreativní nádech.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti používat Microsoft Excel.
### Musím si pro použití Aspose.Cells nainstalovat Microsoft Excel?
Ne, Aspose.Cells je zcela nezávislý a nevyžaduje instalaci aplikace Microsoft Excel.
### Mohu si Aspose.Cells vyzkoušet zdarma?
Ano, můžete vyzkoušet Aspose.Cells pomocí jejich [Bezplatná zkušební verze](https://releases.aspose.com/).
### Jaké programovací jazyky podporuje Aspose.Cells?
Aspose.Cells podporuje více jazyků, včetně C#, VB.NET a dalších.
### Kde mohu získat podporu pro Aspose.Cells?
Podporu můžete získat prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}