---
"description": "V tomto podrobném návodu se dozvíte, jak přidat ovládací prvky oblouku s body připojení pomocí Aspose.Cells pro .NET."
"linktitle": "Přidání ovládání oblouku s body připojení"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání ovládání oblouku s body připojení"
"url": "/cs/net/excel-shapes-controls/add-arc-control-with-connection-points/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání ovládání oblouku s body připojení

## Zavedení
Pokud jde o vytváření vizuálně poutavých excelových sestav, hrají ilustrace zásadní roli. Ať už vytváříte finanční sestavu nebo rozpis projektu, použití tvarů, jako jsou oblouky, může dodat vaší datové prezentaci hloubku a přehlednost. Dnes se podrobně ponoříme do toho, jak využít Aspose.Cells pro .NET k přidání obloukových ovládacích prvků s připojovacími body do excelových listů. Pokud jste se tedy někdy zamýšleli nad tím, jak oživit své tabulky nebo zvýraznit data, čtěte dál!
## Předpoklady
Než se pustíme do vzrušujícího programování, ujistěme se, že máte vše připravené. Zde je to, co budete potřebovat:
1. .NET Framework: Ujistěte se, že máte nainstalovanou kompatibilní verzi. Aspose.Cells funguje s více verzemi, včetně .NET Core.
2. Aspose.Cells pro .NET: Budete si muset stáhnout a nainstalovat knihovnu Aspose.Cells. Můžete si ji snadno stáhnout z [odkaz ke stažení](https://releases.aspose.com/cells/net/).
3. Dobré IDE: Visual Studio, věrný společník každého .NET vývojáře, vám pomůže zefektivnit programování.
4. Základní znalost C#: Pokud se v C# orientujete, shledáte tento tutoriál hračkou.
5. Přístup k adresáři dokumentů: Vědět, kam budete ukládat soubory aplikace Excel. Je to nezbytné pro efektivní organizaci výstupu.
## Importovat balíčky
Dalším krokem je zajistit, abyste do projektu importovali správné balíčky. Aspose.Cells pro .NET má různé funkce, takže to zjednodušíme. Zde je to, co budete muset zahrnout:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám poskytnou přístup ke všem funkcím kreslení a správy buněk, které budete v této příručce používat.
## Krok 1: Nastavení adresáře dokumentů
Nejdříve to nejdůležitější – vytvořme si adresář, kam budete ukládat ty nové, zářivé soubory aplikace Excel. Uděláme to takto:
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tato část kódu zkontroluje, zda zadaná složka existuje. Pokud ne, vytvoří ji. Jednoduché, že? Vždy je dobré mít pro soubory specifické místo, abyste se vyhnuli nepořádku.
## Krok 2: Vytvoření instance sešitu
Nyní, když máme adresář připravený, vytvořme nový sešit aplikace Excel.
```csharp
Workbook excelbook = new Workbook();
```
Zavoláním `Workbook` konstruktor v podstatě říkáte: „Hej, pojďme založit nový soubor aplikace Excel!“ Toto bude plátno pro všechny vaše tvary a data.
## Krok 3: Přidání prvního obloukového tvaru
A tady začíná ta zábava! Pojďme přidat náš první obloukový tvar.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Tento řádek kódu přidá do prvního listu oblouk. Parametry určují souřadnice oblouku a úhly, které definují jeho zakřivení. 
## Krok 4: Přizpůsobte vzhled oblouku
Prázdný oblouk je jako plátno bez barvy – potřebuje trochu šmrncu!
### Nastavení barvy výplně oblouku
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Díky tomu se oblouk zobrazí sytě modře. Barvu můžete změnit na libovolný odstín výměnou `Color.Blue` pro jinou barvu.
### Nastavení umístění oblouku
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Nastavení umístění na „FreeFloating“ umožňuje oblouku pohybovat se nezávisle na hranicích buněk, což vám poskytuje flexibilitu v umístění.
### Úprava tloušťky a stylu čáry
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde definujete tloušťku a styl čáry, čímž ji učiníte výraznější a vizuálně přitažlivější.
## Krok 5: Přidání dalšího obloukového tvaru
Proč se zastavit u jednoho? Pojďme přidat další obloukový tvar, který obohatí náš vizuál v Excelu.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Stejně jako první oblouk je i tento přidán na jiné pozici – právě zde se odehrává kouzlo designu!
## Krok 6: Přizpůsobení druhého oblouku
Dejme i našemu druhému oblouku trochu osobnosti!
### Změnit barvu obloukové čáry
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Držíme se konzistentní modré barvy, ale vždycky můžete kombinovat a najít to, co se k vašemu designu nejlépe hodí!
### Nastavení vlastností podobných prvnímu oblouku
Nezapomeňte tyto estetické volby zopakovat:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde jednoduše zajišťujete, aby druhý oblouk odpovídal prvnímu, a vytváříte tak soudržný vzhled v celém pracovním listu.
## Krok 7: Uložte si sešit
Žádné mistrovské dílo není kompletní bez uložení, že? Je čas zapsat vaše oblouky do souboru Excelu.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Tento řádek uloží nově vytvořené oblouky do souboru aplikace Excel s názvem „book1.out.xls“ ve vámi určeném adresáři.
## Závěr
Gratulujeme! Právě jste zvládli základy přidávání obloukových ovládacích prvků s napojovacími body do excelových listů pomocí Aspose.Cells pro .NET. Tato funkce nejen zkrášlí vaše tabulky, ale také usnadňuje vstřebávání složitých dat. Ať už jste zkušený vývojář, nebo teprve začínáte, tyto vizuální prvky dokáží proměnit vaše reporty z fádních na honosné.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům programově vytvářet a manipulovat s Excelovými soubory.
### Mohu používat Aspose.Cells zdarma?
Ano! Můžete si vyzkoušet bezplatnou zkušební verzi. Navštivte [tento odkaz](https://releases.aspose.com/) začít.
### Jak přidám jiné tvary než oblouky?
Můžete použít různé třídy dostupné v oboru názvů Aspose.Cells.Drawing k přidání různých tvarů, jako jsou obdélníky, kruhy a další.
### Jaké typy souborů mohu vytvořit pomocí Aspose.Cells?
Můžete vytvářet a manipulovat s různými formáty aplikace Excel, včetně XLS, XLSX, CSV a dalších.
### Je pro Aspose.Cells k dispozici technická podpora?
Rozhodně! Můžete přistupovat k [Fórum podpory Aspose](https://forum.aspose.com/c/cells/9) o pomoc.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}