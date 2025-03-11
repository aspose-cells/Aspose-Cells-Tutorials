---
title: Přidejte ovládání oblouku pomocí spojovacích bodů
linktitle: Přidejte ovládání oblouku pomocí spojovacích bodů
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném průvodci zjistíte, jak přidat ovládací prvky oblouku se spojovacími body pomocí Aspose.Cells for .NET.
weight: 27
url: /cs/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte ovládání oblouku pomocí spojovacích bodů

## Zavedení
Pokud jde o vytváření vizuálně poutavých sestav Excel, hrají důležitou roli ilustrace. Ať už vytváříte finanční zprávu nebo členění projektu, použití tvarů, jako jsou oblouky, může vaší prezentaci dat přidat hloubku a jasnost. Dnes se ponoříme hluboko do toho, jak využít Aspose.Cells pro .NET k přidání ovládacích prvků oblouku se spojovacími body do vašich listů aplikace Excel. Takže, pokud jste někdy přemýšleli, jak okořenit své tabulky nebo rozezpívat data, čtěte dál!
## Předpoklady
Než se vrhneme do vzrušení z kódování, ujistíme se, že máte vše připraveno. Zde je to, co potřebujete:
1. .NET Framework: Ujistěte se, že máte nainstalovanou kompatibilní verzi. Aspose.Cells pracuje s více verzemi, včetně .NET Core.
2.  Aspose.Cells for .NET: Budete si muset stáhnout a nainstalovat knihovnu Aspose.Cells. Můžete jej snadno uchopit z[odkaz ke stažení](https://releases.aspose.com/cells/net/).
3. Dobré IDE: Visual Studio, věrný společník každého vývojáře .NET, vám pomůže zefektivnit práci s kódováním.
4. Základní znalost C#: Pokud se v C# vyznáte, zjistíte, že tento tutoriál je bezproblémový.
5. Přístup k adresáři dokumentů: Zjistěte, kam budete ukládat soubory Excel. Je to nezbytné pro efektivní organizaci výstupu.
## Importujte balíčky
Dalším krokem je zajistit, abyste do svého projektu importovali správné balíčky. Aspose.Cells for .NET má různé funkce, takže to zjednodušíme. Zde je to, co budete muset zahrnout:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám umožní přístup ke všem funkcím kreslení a funkcím správy buněk, které budete používat v této příručce.
## Krok 1: Nastavte adresář dokumentů
Za prvé – založme adresář, kam budete ukládat ty zbrusu nové excelové soubory. Uděláme to takto:
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento kousek kódu zkontroluje, zda zadaná složka existuje. Pokud ne, vytvoří jeden. Jednoduché, že? Vždy je dobré mít pro své soubory konkrétní místo, abyste se vyhnuli nepořádku.
## Krok 2: Vytvořte sešit
Nyní, když máme náš adresář připravený, vytvoříme nový excelový sešit.
```csharp
Workbook excelbook = new Workbook();
```
 Zavoláním na`Workbook` konstruktoru, v podstatě říkáte: "Hej, začněme nový soubor Excel!" Toto bude plátno pro všechny vaše tvary a data.
## Krok 3: Přidání tvaru prvního oblouku
Tady začíná zábava! Přidáme náš první tvar oblouku.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Tento řádek kódu přidá do prvního listu tvar oblouku. Parametry určují souřadnice oblouku a úhly, které definují jeho zakřivení. 
## Krok 4: Přizpůsobte vzhled oblouku
Tvar prázdného oblouku je jako plátno bez barvy – chce to trochu vkusu!
### Nastavte barvu výplně oblouku
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Díky tomu bude oblouk celý modrý. Barvu můžete změnit na jakýkoli odstín, který se vám líbí, výměnou`Color.Blue` pro jinou barvu.
### Nastavte umístění oblouku
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Nastavení umístění na "FreeFloating" umožňuje oblouku se pohybovat nezávisle na hranicích buněk, což vám dává flexibilitu v umístění.
### Upravte tloušťku a styl čáry
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde definujete váhu a styl linky, díky čemuž bude výraznější a vizuálně přitažlivější.
## Krok 5: Přidání dalšího tvaru oblouku
Proč se zastavit u jednoho? Pojďme přidat další tvar oblouku, který obohatí náš vizuál Excelu.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Stejně jako první oblouk je i tento přidán na jiné pozici – zde se odehrává kouzlo designu!
## Krok 6: Přizpůsobte druhý oblouk
Dejme našemu druhému oblouku také nějakou osobitost!
### Změnit barvu čáry oblouku
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Udržujeme ji v souladu s modrou barvou, ale vždy ji můžete kombinovat, abyste zjistili, co se nejlépe hodí k vašemu designu!
### Nastavení vlastností podobně jako u prvního oblouku
Ujistěte se, že replikujete tyto estetické volby:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Zde jednoduše zajistíte, aby se druhý oblouk shodoval s prvním, čímž vytvoříte soudržný vzhled celého listu.
## Krok 7: Uložte sešit
Žádné mistrovské dílo není úplné, aniž by bylo zachráněno, že? Je čas zapsat své oblouky do souboru aplikace Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Tento řádek uloží vaše nově vytvořené oblouky do souboru aplikace Excel s názvem „book1.out.xls“ ve vámi určeném adresáři.
## Závěr
Gratuluji! Právě jste zvládli základy přidávání ovládacích prvků oblouku se spojovacími body do listů aplikace Excel pomocí Aspose.Cells pro .NET. Tato funkce nejen zkrášlí vaše tabulky, ale může také usnadnit trávení složitých dat. Ať už jste zkušený vývojář nebo teprve začínáte, tyto vizuální prvky dokážou přeměnit vaše sestavy z nevýrazných na velkolepé.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům programově vytvářet soubory Excelu a manipulovat s nimi.
### Mohu používat Aspose.Cells zdarma?
 Ano! Můžete vyzkoušet bezplatnou zkušební verzi. Návštěva[tento odkaz](https://releases.aspose.com/) začít.
### Jak přidám další tvary kromě oblouků?
přidání různých tvarů, jako jsou obdélníky, kruhy a další, můžete použít různé třídy dostupné v oboru názvů Aspose.Cells.Drawing.
### Jaký typ souborů mohu vytvořit pomocí Aspose.Cells?
Můžete vytvářet a manipulovat s různými formáty Excelu včetně XLS, XLSX, CSV a dalších.
### Je pro Aspose.Cells k dispozici technická podpora?
 Absolutně! Můžete přistupovat k[Aspose fórum podpory](https://forum.aspose.com/c/cells/9) o pomoc.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
