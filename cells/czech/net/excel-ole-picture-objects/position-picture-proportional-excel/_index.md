---
title: Umístěte obrázek (proporcionálně) v aplikaci Excel
linktitle: Umístěte obrázek (proporcionálně) v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak umístit obrázky proporcionálně v Excelu pomocí Aspose.Cells pro .NET. Udělejte ze svých tabulek vizuálně přitažlivější.
weight: 14
url: /cs/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Umístěte obrázek (proporcionálně) v aplikaci Excel

## Zavedení
Už vás nebaví ty pixelované obrázky, které se nikdy nevejdou přesně do vašich excelových tabulek? Představte si toto: máte krásné logo, které je třeba zobrazit na předním místě ve vašem listu Excelu, ale nakonec je zmáčknuté, natažené nebo špatně umístěné. To nikdo nechce! Dobře, držte se svých míst, protože dnes se naučíte, jak umístit obrázky proporcionálně v Excelu pomocí knihovny Aspose.Cells pro .NET. Tato výkonná knihovna umožňuje snadnou manipulaci se soubory aplikace Excel, ať už jde o vytváření sestav, analýzu dat nebo jen úpravu vašich prezentací. Pojďme se ponořit do toho nejnutnějšího dokonalého zarovnání obrázků!
## Předpoklady
Než se ponoříme do samotného kódování, je potřeba mít na svém počítači několik věcí:
1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio, protože poskytne pohodlné prostředí pro váš projekt .NET.
2.  Knihovna Aspose.Cells: Budete potřebovat knihovnu Aspose.Cells. Můžete si vyzkoušet bezplatnou zkušební verzi nebo ji zakoupit od[Aspose webové stránky](https://purchase.aspose.com/buy).
3. Základní znalost C#: Malá znalost programování v C# vám pomůže porozumět příkladům, o kterých budeme diskutovat.
4. Soubor obrázku: Připravte si obrázek (jako vaše logo), který chcete vložit do listu Excel.
Nyní, když máte vše na svém místě, pojďme se pustit do kódování!
## Importujte balíčky
Chcete-li začít používat Aspose.Cells ve svém projektu, musíte importovat konkrétní jmenné prostory. Postup:
### Vytvořit nový projekt
V sadě Visual Studio vytvořte nový projekt:
- Otevřete Visual Studio.
- Klikněte na „Vytvořit nový projekt“.
- Vyberte „Knihovna tříd (.NET Framework)“ nebo „Konzolová aplikace“ v závislosti na vašich preferencích.
### Nainstalujte Aspose.Cells
Balíček Aspose.Cells můžete přidat do svého projektu prostřednictvím NuGet. Zde je postup:
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a klikněte na „Instalovat“.
### Přidat pomocí direktiv
V horní části souboru kódu zahrňte následující direktivy:
```csharp
using System.IO;
using Aspose.Cells;
```
Tyto direktivy vám umožní přístup ke třídám, které budete potřebovat k manipulaci se soubory Excelu.
Nyní si to rozeberme do podrobných kroků, jak úspěšně umístit obrázek proporcionálně v Excelu.
## Krok 1: Nastavte svůj adresář
Nejprve se ujistěte, že máte určenou složku pro vaše dokumenty. Zde je návod, jak vytvořit adresář, pokud neexistuje:
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Tento úryvek vytvoří nový adresář (pokud neexistuje) pro ukládání souborů aplikace Excel. Stačí vyměnit`"Your Document Directory"` se skutečnou cestou, kam chcete soubory uložit.
## Krok 2: Vytvořte sešit
Dále vytvoříme nový sešit:
```csharp
Workbook workbook = new Workbook();
```
Tento řádek inicializuje nový objekt sešitu a poskytuje vám prázdné plátno, na kterém můžete pracovat.
## Krok 3: Přidejte nový list
Nyní, když máme náš sešit nastavený, přidáme do něj nový list:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Tím se přidá nový list a vrátí se index tohoto listu, který můžeme použít k pozdější manipulaci.
## Krok 4: Otevřete nový list
Chcete-li manipulovat s nově přidaným listem, musíte k němu získat přístup:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Teď,`worksheet` nám umožní přidat obsah a obrázky do tohoto konkrétního listu.
## Krok 5: Vložte obrázek
Nyní přichází ta vzrušující část! Pojďme přidat váš krásný obrázek. Nahradit`"logo.jpg"` s názvem vašeho obrázkového souboru:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Tento řádek přidá obrázek do buňky F6 (protože řádky a sloupce mají nulový index,`5` odkazuje na šestou buňku).
## Krok 6: Otevřete přidaný obrázek
Jakmile je obrázek vložen, můžete k němu přistupovat takto:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
To vám umožní manipulovat s vlastnostmi obrázku.
## Krok 7: Umístěte obrázek proporcionálně
Nyní umístěme obrázek proporcionálně:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Zde,`UpperDeltaX` a`UpperDeltaY` upravit polohu obrázku vzhledem k rozměrům buňky. Tyto hodnoty můžete upravit tak, aby byl váš obrázek správný.
## Krok 8: Uložte změny
Nakonec uložte sešit, abyste zachovali všechny změny:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Tento řádek uloží váš sešit jako`book1.out.xls` v určeném adresáři.
## Závěr
tady to máte! Právě jste se naučili, jak umístit obrázky proporcionálně v aplikaci Excel pomocí Aspose.Cells pro .NET. Nejde jen o vkládání obrázků; jde o to, aby ve vašich tabulkách vypadaly dokonale. Pamatujte: dobře umístěný obrázek může výrazně pozvednout vaši prezentaci dat.
Bavte se experimentováním s různými obrázky a umístěními a neváhejte se ponořit hlouběji do bohatých funkcí, které Aspose.Cells nabízí. Vaše excelové listy se chystají vážně změnit!
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která uživatelům umožňuje vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.
### Mohu používat Aspose.Cells zdarma?
 Ano, Aspose.Cells nabízí bezplatnou zkušební verzi, kterou si můžete stáhnout[zde](https://releases.aspose.com/).
### Kde najdu dokumentaci?
 Máte přístup ke komplexnímu[dokumentace](https://reference.aspose.com/cells/net/) pro Aspose.Cells.
### Podporuje Aspose.Cells všechny obrazové formáty?
Aspose.Cells podporuje různé formáty včetně JPEG, PNG, BMP, GIF a TIFF.
### Jak mohu získat podporu pro Aspose.Cells?
 V případě jakýchkoli dotazů neváhejte navštívit[fórum podpory](https://forum.aspose.com/c/cells/9)kde můžete klást své otázky.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
