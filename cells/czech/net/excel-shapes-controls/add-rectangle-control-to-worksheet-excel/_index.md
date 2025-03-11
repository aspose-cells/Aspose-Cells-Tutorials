---
title: Přidejte ovládací prvek obdélníku do listu v aplikaci Excel
linktitle: Přidejte ovládací prvek obdélníku do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat ovládací prvek obdélníku do listu aplikace Excel pomocí Aspose.Cells for .NET, pomocí podrobného průvodce krok za krokem.
weight: 25
url: /cs/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte ovládací prvek obdélníku do listu v aplikaci Excel

## Zavedení
Pokud jde o automatizaci úloh aplikace Excel, Aspose.Cells for .NET je výkonný nástroj, který vám může pomoci dosáhnout různých cílů, z nichž jedním je přidávání tvarů, jako jsou obdélníky, do vašich listů. V této příručce prozkoumáme, jak přidat ovládací prvek obdélníku do listu aplikace Excel pomocí Aspose.Cells pro .NET. Na konci budete moci vytvořit, přizpůsobit a uložit list s vloženým ovládacím prvkem obdélníku.
Než se ale ponoříme, promluvme si o předpokladech.
## Předpoklady
Chcete-li pokračovat v tomto tutoriálu, ujistěte se, že máte splněny následující předpoklady:
1.  Knihovna Aspose.Cells for .NET: Pokud jste to ještě neudělali,[stáhnout knihovnu](https://releases.aspose.com/cells/net/) nebo jej nainstalujte pomocí NuGet ve Visual Studiu.
2. .NET Framework: Na vašem počítači musíte mít nastavené vývojové prostředí .NET.
3. Základní znalost C#: Přestože vás provedeme krok za krokem, základní znalost C# a objektově orientovaného programování je výhodná.
4.  Licence: Použití Aspose.Cells ve zkušebním režimu funguje dobře pro základní úkoly, ale pro plnou funkčnost zvažte získání a[dočasná licence](https://purchase.aspose.com/temporary-license/)nebo koupíte od[zde](https://purchase.aspose.com/buy).
Nyní se pojďme ponořit do kódu!
## Importujte balíčky
Chcete-li začít s Aspose.Cells, ujistěte se, že jste do svého projektu importovali potřebné jmenné prostory. Tyto importy umožní přístup k různým třídám a metodám, které potřebujete pro interakci se soubory aplikace Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto řádky zajišťují, že váš projekt může komunikovat s adresáři souborů (`System.IO`), sešity Excel (`Aspose.Cells`) a kresba tvaru (`Aspose.Cells.Drawing`).
Nyní si tento proces rozdělíme do jednoduchých kroků, abyste jej mohli snadno sledovat a replikovat ve svých vlastních projektech.
## Krok 1: Nastavení cesty k adresáři
První věc, kterou musíte udělat, je definovat adresář, do kterého bude váš soubor Excel uložen. Tento krok zajistí, že váš projekt ví, kde vytvořit a uložit výstupní soubor.
### Definování datového adresáře
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Zde zadáte cestu k adresáři, kam bude soubor Excel uložen. Můžete vyměnit`"Your Document Directory"` se skutečnou cestou na vašem počítači, nebo dynamicky vytvořte složku, pokud neexistuje.
### Kontrola a vytvoření adresáře
```csharp
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento blok kontroluje, zda adresář existuje. Pokud ne, vytvoří jeden. Představte si to, jako byste měli kartotéku připravenou před uložením jakýchkoli dokumentů.
## Krok 2: Vytvoření nového sešitu
 V tomto kroku vytvoříte nový excelový sešit pomocí`Aspose.Cells.Workbook` třída. To bude sloužit jako kontejner pro váš pracovní list a tvary.
```csharp
// Vytvořte nový sešit.
Workbook excelbook = new Workbook();
```
 Zavoláním na`Workbook` konstruktoru, nyní máte prázdný excelový sešit připravený k přizpůsobení.
## Krok 3: Přidání obdélníkového ovládacího prvku
Tady se děje kouzlo. Do prvního listu sešitu přidáte tvar obdélníku.
```csharp
// Přidejte ovládací prvek obdélník.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Pojďme si to rozebrat:
- `excelbook.Worksheets[0]`: Tím se dostanete k prvnímu listu ve vašem sešitu.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Tím se do listu přidá tvar obdélníku. Parametry zde definují pozici (řádek a sloupec), stejně jako šířku a výšku obdélníku.
## Krok 4: Přizpůsobení obdélníku
Pouhé přidání obdélníku nestačí – budete si ho chtít přizpůsobit. V tomto kroku nastavíme umístění, tloušťku čáry a styl čárky obdélníku.
### Nastavení umístění
```csharp
// Nastavte umístění obdélníku.
rectangle.Placement = PlacementType.FreeFloating;
```
To určuje, že obdélník je volně plovoucí, což znamená, že nebude vázán rozměry buňky.
### Nastavení tloušťky čáry
```csharp
// Nastavte tloušťku čáry.
rectangle.Line.Weight = 4;
```
Zde nastavíme tloušťku čáry obdélníku na 4 body. Čím vyšší číslo, tím tlustší čára.
### Nastavení stylu pomlčky
```csharp
// Nastavte styl čárky obdélníku.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Tato čára nastaví styl čárky okraje obdélníku na plný. Můžete experimentovat s různými styly jako`Dash` nebo`Dot` v závislosti na vašich požadavcích.
## Krok 5: Uložení sešitu
Po přidání a přizpůsobení obdélníku je posledním krokem uložení sešitu do určeného adresáře.
```csharp
// Uložte soubor aplikace Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
 Tím se sešit uloží jako soubor`.xls` soubor ve složce, kterou jste definovali dříve. Formát souboru můžete upravit změnou přípony, např`.xlsx` pokud dáváte přednost novějšímu formátu Excel.
## Závěr
tady to máte! Přidání ovládacího prvku obdélníku do listu aplikace Excel pomocí Aspose.Cells for .NET je jednoduchý proces, jakmile jej rozeberete krok za krokem. Ať už potřebujete přidat tvary pro vizuální přitažlivost, zvýraznit části dat nebo přizpůsobit své sestavy, Aspose.Cells vám poskytuje flexibilitu, abyste tak učinili programově.
Tato příručka by vás měla vybavit všemi znalostmi, které potřebujete, abyste mohli začít přidávat tvary, jako jsou obdélníky, do listů aplikace Excel pomocí Aspose.Cells. Nyní je čas experimentovat a zjistit, čeho dalšího můžete dosáhnout s touto výkonnou knihovnou!
## FAQ
### Mohu pomocí Aspose.Cells pro .NET přidat další tvary, jako jsou kruhy nebo čáry?  
Ano, Aspose.Cells umožňuje přidávat různé tvary, včetně kruhů, čar, šipek a dalších.
### Jaké další vlastnosti mohu nastavit pro ovládací prvek obdélník?  
Můžete přizpůsobit barvu výplně, barvu čáry, průhlednost a dokonce přidat text do obdélníku.
### Je Aspose.Cells kompatibilní s .NET Core?  
Ano, Aspose.Cells podporuje .NET Core, stejně jako .NET Framework a další platformy založené na .NET.
### Mohu umístit obdélník vzhledem ke konkrétní buňce?  
 Ano, obdélník můžete umístit do konkrétních řádků a sloupců nebo použít`PlacementType` kontrolovat, jak je ukotven.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?  
 Ano, můžete získat a[zkušební verze zdarma](https://releases.aspose.com/) z webové stránky, abyste si před nákupem vyzkoušeli funkce knihovny.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
