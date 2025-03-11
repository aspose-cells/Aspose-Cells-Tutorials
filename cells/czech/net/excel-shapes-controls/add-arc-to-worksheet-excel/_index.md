---
title: Přidat Arc do listu v Excelu
linktitle: Přidat Arc do listu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se přidávat oblouky do listů aplikace Excel pomocí Aspose.Cells pro .NET. Postupujte podle našeho podrobného průvodce pro vylepšení návrhů tabulek.
weight: 16
url: /cs/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat Arc do listu v Excelu

## Zavedení
Vytváření vizuálně přitažlivých excelových tabulek je pro prezentaci dat zásadní a knihovna Aspose.Cells poskytuje vývojářům robustní nástroje pro splnění tohoto úkolu. Jednou zajímavou funkcí, kterou byste mohli chtít začlenit do svých dokumentů aplikace Excel, je možnost přidávat tvary, jako jsou oblouky. V tomto tutoriálu si krok za krokem projdeme, jak přidat oblouky do listu aplikace Excel pomocí Aspose.Cells for .NET. Na konci tohoto článku se nejen naučíte přidávat oblouky, ale také získáte přehled o správě tvarů obecně.
## Předpoklady
Než se ponoříme do složitosti přidávání oblouků do vašeho listu, je nezbytné zajistit, abyste měli několik věcí na svém místě. Zde jsou předpoklady, které budete potřebovat, abyste mohli začít:
1. Visual Studio: Budete muset mít na svém počítači nainstalované Visual Studio, protože jako náš programovací jazyk budeme používat C#.
2. .NET Framework: Ujistěte se, že máte nainstalované rozhraní .NET Framework nebo .NET Core. Aspose.Cells podporuje obojí.
3. Aspose.Cells for .NET: Musíte mít knihovnu Aspose.Cells. Můžete si jej stáhnout z[Aspose.Cells ke stažení](https://releases.aspose.com/cells/net/) strana.
4. Základní porozumění C#: Znalost C# vám pomůže bez větších problémů sledovat úryvky kódu.
## Importujte balíčky
Chcete-li začít pracovat s Aspose.Cells ve vašem projektu, musíte importovat potřebné balíčky. Jak na to:
### Vytvořit nový projekt
- Otevřete Visual Studio.
- Zvolte „Vytvořit nový projekt“.
- Vyberte šablonu, která pracuje s .NET (jako konzolová aplikace).
  
### Přidejte odkazy Aspose.Cells
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte jej.
Nyní jste připraveni začít kódovat přidání oblouku.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Zde je podrobný rozpis kódu, který ukazuje, jak přidat oblouky do listu v aplikaci Excel.
## Krok 1: Nastavení adresáře
Prvním krokem je nastavení adresáře, kam budete soubor Excelu ukládat. To pomáhá snadno spravovat vaše výstupní soubory.
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
V tomto fragmentu kódu zadáváme cestu k adresáři dokumentů. Také zkontrolujeme, zda adresář existuje; pokud ne, vytvoříme ho. To vytváří základy pro náš výstup.
## Krok 2: Vytvořte sešit
Dále vytvoříme novou instanci sešitu.
```csharp
// Vytvořte nový sešit.
Workbook excelbook = new Workbook();
```
Tento řádek vytvoří nový sešit aplikace Excel. Představte si to jako prázdné plátno, kam můžeme přidávat tvary, data a další.
## Krok 3: Přidejte tvar prvního oblouku
Nyní do listu přidáme náš první tvar oblouku.
```csharp
// Přidejte tvar oblouku.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Zde přidáváme oblouk do prvního listu. Parametry definují polohu a velikost oblouku:`(left, top, width, height, startAngle, endAngle)`. Je to jako nakreslit výseč kruhu!
## Krok 4: Přizpůsobte první oblouk
Po přidání oblouku možná budete chtít upravit jeho vzhled.
```csharp
// Nastavte barvu tvaru výplně
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Nastavte umístění oblouku.
arc1.Placement = PlacementType.FreeFloating;           
// Nastavte tloušťku čáry.
arc1.Line.Weight = 1;      
// Nastavte styl čárky oblouku.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
V této sekci přizpůsobujeme oblouk. Nastavíme jeho typ výplně na plnou barvu (v tomto případě modrou), definujeme způsob jeho umístění, určíme tloušťku čáry a zvolíme styl čárky. V podstatě oblékáme náš oblouk tak, aby byl vizuálně přitažlivý!
## Krok 5: Přidejte druhý tvar oblouku
Přidejme další tvar oblouku, abychom poskytli více kontextu.
```csharp
// Přidejte další tvar oblouku.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Podobně jako u prvního oblouku přidáváme na stejný list druhý oblouk. Souřadnice jsou zde trochu posunuté, aby to bylo umístěno jinak.
## Krok 6: Přizpůsobte druhý oblouk
Stejně jako jsme to udělali s prvním obloukem, přizpůsobíme i druhý.
```csharp
// Nastavte barvu čáry
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Nastavte umístění oblouku.
arc2.Placement = PlacementType.FreeFloating;          
// Nastavte tloušťku čáry.
arc2.Line.Weight = 1;           
// Nastavte styl čárky oblouku.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde dáváme druhému oblouku stejný styl jako prvnímu. Můžete změnit barvu nebo styl podle potřeby pro jedinečnost nebo tematické účely.
## Krok 7: Uložte sešit
Konečně je čas uložit nově vytvořený sešit s oblouky.
```csharp
// Uložte soubor aplikace Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Tento řádek funguje jako stisknutí tlačítka Uložit. Ukládáme naši práci do určeného umístění s určeným názvem souboru. Nezapomeňte zkontrolovat svůj adresář, abyste viděli své mistrovské dílo ve formátu Excel!
## Závěr
tomto tutoriálu jsme prozkoumali proces přidávání obloukových tvarů do listu aplikace Excel pomocí Aspose.Cells pro .NET. Prostřednictvím jednoduchého průvodce krok za krokem jste se naučili, jak vytvořit nový sešit, přidat oblouky, upravit jejich vzhled a uložit dokument. Tato funkce nejen zvyšuje vizuální přitažlivost vašich tabulek, ale také činí vaše datové prezentace informativnější. Ať už vytváříte grafy, sestavy nebo jen experimentujete, použití tvarů, jako jsou oblouky, může dodat vašim projektům kreativní nádech.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel programově bez potřeby aplikace Microsoft Excel.
### Musím nainstalovat Microsoft Excel, abych mohl používat Aspose.Cells?
Ne, Aspose.Cells je zcela nezávislý a nevyžaduje instalaci aplikace Microsoft Excel.
### Mohu vyzkoušet Aspose.Cells zdarma?
 Ano, můžete vyzkoušet Aspose.Cells pomocí jejich[Bezplatná zkušební verze](https://releases.aspose.com/).
### Jaké programovací jazyky Aspose.Cells podporuje?
Aspose.Cells podporuje více jazyků, včetně C#, VB.NET a dalších.
### Kde mohu získat podporu pro Aspose.Cells?
 Podporu můžete získat prostřednictvím[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
