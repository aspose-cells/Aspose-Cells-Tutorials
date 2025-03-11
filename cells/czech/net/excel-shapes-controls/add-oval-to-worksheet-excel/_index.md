---
title: Přidejte Oval do listu v aplikaci Excel
linktitle: Přidejte Oval do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat ovál do listu aplikace Excel pomocí Aspose.Cells for .NET. Průvodce krok za krokem s podrobným vysvětlením kódů.
weight: 17
url: /cs/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte Oval do listu v aplikaci Excel

## Zavedení
Vytváření úžasných a interaktivních souborů aplikace Excel může zahrnovat více než jen čísla a vzorce. Tvary jako ovály mohou přidat vizuální přitažlivost nebo poskytnout funkční prvky ve vašich pracovních listech. V tomto tutoriálu prozkoumáme, jak pomocí Aspose.Cells for .NET přidat ovály do listu aplikace Excel programově. Ať už chcete přidat nějaký vkus nebo funkčnost, máme pro vás podrobného průvodce, který vše rozebere.
## Předpoklady
Než se ponoříte do kódu, musíte mít připraveno několik věcí:
1.  Aspose.Cells for .NET Library: Můžete si ji stáhnout z[zde](https://releases.aspose.com/cells/net/) nebo jej nainstalujte pomocí NuGet ve Visual Studiu.
2. Vývojové prostředí: AC# IDE jako Visual Studio.
3. Základní porozumění C#: Měli byste být obeznámeni se základními koncepty kódování v C#.
 Nezapomeňte také nastavit svůj projekt instalací knihovny Aspose.Cells for .NET. Pokud ještě nemáte licenci, můžete požádat o a[dočasná licence](https://purchase.aspose.com/temporary-license/) nebo použijte[zkušební verze zdarma](https://releases.aspose.com/) verze.
## Importujte balíčky
Před napsáním jakéhokoli kódu se ujistěte, že jste zahrnuli požadované jmenné prostory. Zde je fragment kódu C#, abyste se ujistili, že používáte správné knihovny:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Krok 1: Nastavte svůj adresář
Prvním krokem při přidávání oválu do listu aplikace Excel je určení, kam bude soubor aplikace Excel uložen. Definujme cestu k adresáři a před uložením naší práce se ujistěte, že adresář existuje.

Vytvoříme cestu k adresáři a ověříme, zda existuje. Pokud složka neexistuje, bude vytvořena.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento krok je zásadní, protože zajišťuje, že váš soubor bude uložen na správném místě a později nenarazíte na problémy s cestou k souboru.
## Krok 2: Inicializujte nový sešit
Dále musíme vytvořit nový sešit, do kterého přidáme naše oválné tvary. Sešit představuje soubor Excel a můžeme do něj přidávat obsah nebo tvary.

 V tomto kroku vytvoříme instanci nového`Workbook` objekt, který bude sloužit jako náš souborový kontejner Excel.
```csharp
// Vytvořte nový sešit.
Workbook excelbook = new Workbook();
```
## Krok 3: Přidejte první oválný tvar
Nyní přichází ta zábavná část – přidání oválného tvaru do listu. Tento ovál může představovat vizuální prvek, jako je tlačítko nebo zvýraznění. Začneme přidáním prvního oválného tvaru do prvního pracovního listu našeho sešitu.

 Zde používáme`Shapes.AddOval()` způsob vytvoření oválu na listu na konkrétním řádku a sloupci.
```csharp
// Přidejte oválný tvar.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 Parametry uvnitř`AddOval()` jsou následující:
- První dvě čísla představují řádek a sloupec pro levý horní roh oválu.
- Další dvě čísla představují výšku a šířku oválu.
## Krok 4: Nastavte umístění a styl oválu
 Jakmile je ovál vytvořen, můžeme nastavit jeho polohu, tloušťku čáry a styl čárky. The`Placement` vlastnost určuje, jak se ovál chová, když změníte velikost nebo přesunete buňky v listu.

Ovál děláme volně plovoucí a upravujeme jeho vzhled.
```csharp
// Nastavte umístění oválu.
oval1.Placement = PlacementType.FreeFloating;
// Nastavte tloušťku čáry.
oval1.Line.Weight = 1;
// Nastavte styl čárky oválu.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
To umožňuje oválu volně se pohybovat v rámci listu a jeho tloušťka čáry a styl jsou nastaveny pro vizuální konzistenci.
## Krok 5: Přidejte další oválný (kruhový) tvar
Proč se zastavit u jednoho? V tomto kroku přidáme další oválný tvar, tentokrát vytvoříme dokonalý kruh tím, že vytvoříme stejnou výšku a šířku.

Vytvoříme další ovál, umístíme jej na jiné místo a zajistíme, aby měl kruhový tvar nastavením stejné výšky a šířky.
```csharp
// Přidejte další oválný (kruhový) tvar.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Krok 6: Upravte druhý ovál
Stejně jako předtím upravíme umístění, váhu a styl čárky tohoto druhého oválu (nebo kruhu).

Podobné vlastnosti aplikujeme na druhý ovál, aby odpovídal stylu prvního.
```csharp
// Nastavte umístění oválu.
oval2.Placement = PlacementType.FreeFloating;
// Nastavte tloušťku čáry.
oval2.Line.Weight = 1;
// Nastavte styl čárky oválu.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Krok 7: Uložte sešit
Nakonec musíme sešit uložit s ovály, které jsme právě přidali. Uložením souboru zajistíte uložení všech našich změn.

Sešit uložíme do adresářové cesty, kterou jsme definovali dříve.
```csharp
// Uložte soubor aplikace Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
je to! Úspěšně jste přidali elipsy do listu aplikace Excel a uložili soubor.
## Závěr
Přidávání tvarů, jako jsou ovály, do listu aplikace Excel pomocí Aspose.Cells for .NET je nejen jednoduché, ale také zábavný způsob, jak vylepšit své tabulky o další vizuální prvky. Ať už pro účely návrhu nebo přidávání klikacích prvků, tvary mohou hrát významnou roli ve vzhledu a funkci vašich souborů Excel. Takže až budete příště pracovat na projektu, který vyžaduje interaktivní nebo vizuálně přitažlivé excelové listy, budete přesně vědět, jak přidat ty dokonalé ovály!
## FAQ
### Mohu pomocí Aspose.Cells pro .NET přidat další tvary, jako jsou obdélníky nebo čáry?
 Ano, pomocí tlačítka můžete přidávat různé tvary, jako jsou obdélníky, čáry a šipky`Shapes` kolekce v Aspose.Cells.
### Je možné po přidání změnit velikost oválů?
Absolutně! Po přidání oválů můžete upravit vlastnosti výšky a šířky.
### V jakých formátech souborů mohu uložit sešit kromě XLS?
Aspose.Cells podporuje různé formáty, jako je XLSX, CSV a PDF, mezi ostatními.
### Mohu upravit barvu obrysu oválu?
 Ano, můžete změnit barvu čáry oválu pomocí`Line.Color` vlastnictví.
### Je nutné mít licenci pro Aspose.Cells?
 I když můžete Aspose.Cells vyzkoušet s bezplatnou zkušební verzí, budete potřebovat a[licence](https://purchase.aspose.com/buy) pro dlouhodobé používání nebo pro přístup k pokročilým funkcím.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
