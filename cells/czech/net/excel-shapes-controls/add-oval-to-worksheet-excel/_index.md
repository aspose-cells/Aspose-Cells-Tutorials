---
"description": "Naučte se, jak přidat ovál do listu aplikace Excel pomocí Aspose.Cells pro .NET. Podrobný návod s podrobným vysvětlením kódu."
"linktitle": "Přidání oválu do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání oválu do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání oválu do listu v Excelu

## Zavedení
Vytváření úžasných a interaktivních souborů Excelu může zahrnovat více než jen čísla a vzorce. Tvary jako ovály mohou vašim listům dodat vizuální atraktivitu nebo poskytnout funkční prvky. V tomto tutoriálu se podíváme na to, jak pomocí Aspose.Cells for .NET programově přidat ovály do listu Excelu. Ať už chcete dodat listu trochu šmrncu nebo funkčnosti, máme pro vás podrobný návod, který vše rozebírá.
## Předpoklady
Než se ponoříme do kódu, je třeba mít připraveno několik věcí:
1. Knihovna Aspose.Cells pro .NET: Můžete si ji stáhnout z [zde](https://releases.aspose.com/cells/net/) nebo jej nainstalujte pomocí NuGetu ve Visual Studiu.
2. Vývojové prostředí: AC# IDE, jako je Visual Studio.
3. Základní znalost C#: Měli byste být obeznámeni se základními koncepty kódování v C#.
Nezapomeňte také nastavit svůj projekt instalací knihovny Aspose.Cells pro .NET. Pokud ještě nemáte licenci, můžete o ni požádat. [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo použijte [bezplatná zkušební verze](https://releases.aspose.com/) verze.
## Importovat balíčky
Než začnete psát jakýkoli kód, ujistěte se, že jste zahrnuli požadované jmenné prostory. Zde je úryvek kódu C#, abyste se ujistili, že používáte správné knihovny:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Krok 1: Nastavení adresáře
Prvním krokem při přidání oválu do excelového listu je určení místa, kam bude váš excelový soubor uložen. Před uložením práce si definujme cestu k adresáři a ujistěme se, že adresář existuje.

Vytvoříme cestu k adresáři a ověříme, zda existuje. Pokud složka neexistuje, bude vytvořena.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento krok je klíčový, protože zajišťuje, že váš soubor bude uložen na správném místě a později se nesetkáte s problémy s cestou k souboru.
## Krok 2: Inicializace nového sešitu
Dále musíme vytvořit nový sešit, do kterého přidáme oválné tvary. Sešit představuje soubor aplikace Excel a můžeme do něj přidávat obsah nebo tvary.

V tomto kroku vytvoříme novou instanci `Workbook` objekt, který bude sloužit jako náš kontejner pro excelové soubory.
```csharp
// Vytvořte instanci nového sešitu.
Workbook excelbook = new Workbook();
```
## Krok 3: Přidejte první oválný tvar
A teď přichází ta zábavná část – přidání oválného tvaru do pracovního listu. Tento ovál může představovat vizuální prvek, jako je tlačítko nebo zvýraznění. Začneme přidáním prvního oválného tvaru do prvního pracovního listu našeho sešitu.

Zde používáme `Shapes.AddOval()` metoda pro vytvoření oválu na listu v určitém řádku a sloupci.
```csharp
// Přidejte oválný tvar.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Parametry uvnitř `AddOval()` jsou následující:
- První dvě čísla představují řádek a sloupec pro levý horní roh oválu.
- Další dvě čísla představují výšku a šířku oválu.
## Krok 4: Nastavení umístění a stylu oválu
Jakmile je ovál vytvořen, můžeme nastavit jeho polohu, tloušťku čáry a styl čar. `Placement` Vlastnost určuje, jak se ovál chová při změně velikosti nebo přesunutí buněk v listu.

Ovál necháme volně se vznášet a upravíme jeho vzhled.
```csharp
// Nastavte umístění oválu.
oval1.Placement = PlacementType.FreeFloating;
// Nastavte tloušťku čáry.
oval1.Line.Weight = 1;
// Nastavte styl čárkování oválu.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Díky tomu se ovál může volně pohybovat v rámci listu a jeho tloušťka a styl čáry jsou nastaveny pro vizuální konzistenci.
## Krok 5: Přidejte další oválný (kruhový) tvar
Proč se zastavit u jednoho? V tomto kroku přidáme další oválný tvar, tentokrát vytvoříme dokonalý kruh tak, že výšku a šířku nastavíme stejně.

Vytvoříme další ovál, umístíme ho na jiné místo a zajistíme, aby měl kruhový tvar nastavením stejné výšky a šířky.
```csharp
// Přidejte další oválný (kruhový) tvar.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Krok 6: Stylizujte druhý ovál
Stejně jako předtím upravíme umístění, tloušťku a styl čárkování tohoto druhého oválu (nebo kruhu).

Na druhý ovál aplikujeme podobné vlastnosti, aby odpovídal stylu prvního.
```csharp
// Nastavte umístění oválu.
oval2.Placement = PlacementType.FreeFloating;
// Nastavte tloušťku čáry.
oval2.Line.Weight = 1;
// Nastavte styl čárkování oválu.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Krok 7: Uložení sešitu
Nakonec musíme uložit sešit s právě přidanými ovály. Uložení souboru zajistí, že se všechny naše změny uloží.

Sešit uložíme do adresáře, který jsme definovali dříve.
```csharp
// Uložte soubor Excelu.
excelbook.Save(dataDir + "book1.out.xls");
```
A to je vše! Úspěšně jste přidali ovály do listu aplikace Excel a uložili soubor.
## Závěr
Přidávání tvarů, jako jsou ovály, do excelového listu pomocí Aspose.Cells pro .NET je nejen jednoduché, ale také zábavný způsob, jak vylepšit vaše tabulky o další vizuální prvky. Ať už jde o designové účely nebo přidání klikatelných prvků, tvary mohou hrát významnou roli v tom, jak vaše excelové soubory vypadají a fungují. Takže až budete příště pracovat na projektu, který vyžaduje interaktivní nebo vizuálně atraktivní excelové listy, budete přesně vědět, jak tyto dokonalé ovály přidat!
## Často kladené otázky
### Mohu pomocí Aspose.Cells pro .NET přidat další tvary, jako jsou obdélníky nebo čáry?
Ano, můžete přidat různé tvary, jako jsou obdélníky, čáry a šipky, pomocí `Shapes` kolekce v Aspose.Cells.
### Je možné po přidání oválů změnit jejich velikost?
Rozhodně! Po přidání oválů můžete upravit jejich výšku a šířku.
### V jakých formátech souborů kromě XLS mohu sešit uložit?
Aspose.Cells podporuje více formátů, jako například XLSX, CSV a PDF.
### Mohu upravit barvu obrysu oválu?
Ano, barvu čáry oválu můžete změnit pomocí `Line.Color` vlastnictví.
### Je nutné mít licenci pro Aspose.Cells?
I když si můžete Aspose.Cells vyzkoušet s bezplatnou zkušební verzí, budete potřebovat [licence](https://purchase.aspose.com/buy) pro dlouhodobé používání nebo pro přístup k pokročilým funkcím.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}