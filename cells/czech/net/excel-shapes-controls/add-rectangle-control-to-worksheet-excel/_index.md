---
"description": "Naučte se, jak přidat ovládací prvek obdélník do listu aplikace Excel pomocí Aspose.Cells pro .NET s podrobným návodem krok za krokem."
"linktitle": "Přidání ovládacího prvku Obdélník do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání ovládacího prvku Obdélník do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání ovládacího prvku Obdélník do listu v Excelu

## Zavedení
Pokud jde o automatizaci úloh v Excelu, Aspose.Cells pro .NET je výkonný nástroj, který vám může pomoci dosáhnout řady cílů, jedním z nich je přidávání tvarů, jako jsou obdélníky, do vašich listů. V této příručce se podíváme na to, jak přidat ovládací prvek obdélník do listu Excelu pomocí Aspose.Cells pro .NET. Na konci budete schopni vytvořit, přizpůsobit a uložit list s vloženým ovládacím prvkem obdélník.
Ale než se do toho pustíme, pojďme si promluvit o předpokladech.
## Předpoklady
Abyste mohli pokračovat v tomto tutoriálu, ujistěte se, že máte splněny následující předpoklady:
1. Knihovna Aspose.Cells pro .NET: Pokud jste tak ještě neučinili, [stáhnout knihovnu](https://releases.aspose.com/cells/net/) nebo jej nainstalujte pomocí NuGetu ve Visual Studiu.
2. .NET Framework: Na svém počítači musíte mít nainstalované vývojové prostředí .NET.
3. Základní znalost C#: I když vás provedeme krok za krokem, základní znalost C# a objektově orientovaného programování je výhodou.
4. Licence: Použití Aspose.Cells v testovacím režimu funguje dobře pro základní úkoly, ale pro plnou funkčnost zvažte pořízení [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo si ho zakoupit od [zde](https://purchase.aspose.com/buy).
A teď se pojďme ponořit do kódu!
## Importovat balíčky
Abyste mohli začít s Aspose.Cells, ujistěte se, že jste do projektu importovali potřebné jmenné prostory. Tyto importy umožní přístup k různým třídám a metodám, které potřebujete k interakci se soubory aplikace Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto řádky zajišťují, že váš projekt může interagovat se soubory v adresářích (`System.IO`), sešity aplikace Excel (`Aspose.Cells`) a kreslení tvarů (`Aspose.Cells.Drawing`).
Nyní si celý proces rozdělme na jednoduché kroky, abyste je mohli snadno sledovat a replikovat ve svých vlastních projektech.
## Krok 1: Nastavení cesty k adresáři
První věc, kterou musíte udělat, je definovat adresář, kam bude uložen váš soubor Excel. Tento krok zajistí, že váš projekt bude vědět, kam má vytvořit a uložit výstupní soubor.
### Definování datového adresáře
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Zde zadáte cestu k adresáři, kam bude uložen soubor Excel. Můžete nahradit `"Your Document Directory"` se skutečnou cestou na vašem počítači nebo dynamicky vytvořit složku, pokud neexistuje.
### Kontrola a vytvoření adresáře
```csharp
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento blok kontroluje, zda adresář existuje. Pokud ne, vytvoří ho. Představte si to jako připravenou kartotéku před uložením jakýchkoli dokumentů.
## Krok 2: Vytvoření instance nového sešitu
V tomto kroku vytvoříte nový sešit aplikace Excel pomocí `Aspose.Cells.Workbook` třída. Toto bude sloužit jako kontejner pro váš pracovní list a tvary.
```csharp
// Vytvořte instanci nového sešitu.
Workbook excelbook = new Workbook();
```
Zavoláním `Workbook` konstruktor, nyní máte prázdný sešit aplikace Excel připravený k přizpůsobení.
## Krok 3: Přidání ovládacího prvku Obdélník
A tady se začne dít ta pravá magie. Na první list sešitu přidáte obdélníkový tvar.
```csharp
// Přidejte ovládací prvek obdélník.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Pojďme si to rozebrat:
- `excelbook.Worksheets[0]`Toto otevře první list v sešitu.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Toto přidá do listu obdélníkový tvar. Parametry zde definují polohu (řádek a sloupec) a také šířku a výšku obdélníku.
## Krok 4: Úpravy obdélníku
Pouhé přidání obdélníku nestačí – budete si ho chtít upravit. V tomto kroku nastavíme umístění, tloušťku čáry a styl čárkování obdélníku.
### Nastavení umístění
```csharp
// Nastavte umístění obdélníku.
rectangle.Placement = PlacementType.FreeFloating;
```
Toto určuje, že obdélník je volně plovoucí, což znamená, že nebude omezen rozměry buňky.
### Nastavení tloušťky čáry
```csharp
// Nastavte tloušťku čáry.
rectangle.Line.Weight = 4;
```
Zde nastavíme tloušťku čáry obdélníku na 4 body. Čím vyšší číslo, tím silnější čára.
### Nastavení stylu pomlčky
```csharp
// Nastavte styl čárkování obdélníku.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Tato čára nastaví styl čárkování okraje obdélníku na plný. Můžete experimentovat s různými styly, jako například `Dash` nebo `Dot` v závislosti na vašich požadavcích.
## Krok 5: Uložení sešitu
Jakmile je obdélník přidán a upraven, posledním krokem je uložení sešitu do zadaného adresáře.
```csharp
// Uložte soubor Excelu.
excelbook.Save(dataDir + "book1.out.xls");
```
Tím se sešit uloží jako `.xls` soubor ve složce, kterou jste dříve definovali. Formát souboru můžete upravit změnou přípony, například `.xlsx` pokud dáváte přednost novějšímu formátu Excelu.
## Závěr
A tady to máte! Přidání ovládacího prvku obdélník do listu aplikace Excel pomocí Aspose.Cells pro .NET je jednoduchý proces, jakmile si ho rozdělíte krok za krokem. Ať už potřebujete přidat tvary pro vizuální přitažlivost, zvýraznit části dat nebo přizpůsobit své sestavy, Aspose.Cells vám dává flexibilitu, jak to udělat programově.
Tato příručka by vám měla poskytnout všechny znalosti potřebné k tomu, abyste mohli začít s přidáváním tvarů, jako jsou obdélníky, do svých excelových listů pomocí Aspose.Cells. Nyní je čas experimentovat a zjistit, čeho dalšího můžete s touto výkonnou knihovnou dosáhnout!
## Často kladené otázky
### Mohu pomocí Aspose.Cells pro .NET přidat další tvary, jako jsou kruhy nebo čáry?  
Ano, Aspose.Cells umožňuje přidávat různé tvary, včetně kruhů, čar, šipek a dalších.
### Jaké další vlastnosti mohu nastavit pro ovládací prvek obdélník?  
Můžete si přizpůsobit barvu výplně, barvu čáry, průhlednost a dokonce i přidat text do obdélníku.
### Je Aspose.Cells kompatibilní s .NET Core?  
Ano, Aspose.Cells podporuje .NET Core, stejně jako .NET Framework a další platformy založené na .NET.
### Mohu umístit obdélník vzhledem ke konkrétní buňce?  
Ano, můžete umístit obdélník do určitých řádků a sloupců nebo použít `PlacementType` ovládat, jak je ukotveno.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?  
Ano, můžete získat [bezplatná zkušební verze](https://releases.aspose.com/) z webových stránek, abyste si před zakoupením vyzkoušeli funkce knihovny.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}