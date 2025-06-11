---
"description": "Naučte se, jak proporcionálně umisťovat obrázky v Excelu pomocí Aspose.Cells pro .NET. Udělejte si tabulky vizuálně atraktivnějšími."
"linktitle": "Pozice obrázku (proporcionální) v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Pozice obrázku (proporcionální) v Excelu"
"url": "/cs/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pozice obrázku (proporcionální) v Excelu

## Zavedení
Už vás nebaví ty pixelované obrázky, které se do excelových tabulek nikdy nevejdou tak akorát? Představte si to: máte krásné logo, které by mělo být v excelovém listu prominentně zobrazeno, ale nakonec je zmačkané, roztažené nebo špatně umístěné. To nikdo nechce! Tak se držte, protože dnes se naučíte, jak proporcionálně umisťovat obrázky v Excelu pomocí knihovny Aspose.Cells pro .NET. Tato výkonná knihovna usnadňuje manipulaci s excelovými soubory, ať už jde o reporting, analýzu dat nebo jen o vylepšení prezentací. Pojďme se ponořit do detailů dokonalého zarovnání obrázků!
## Předpoklady
Než se pustíme do samotného kódování, je třeba mít na svém počítači nastaveno několik věcí:
1. Visual Studio: Ujistěte se, že máte nainstalované Visual Studio, protože vám poskytne pohodlné prostředí pro váš .NET projekt.
2. Knihovna Aspose.Cells: Budete potřebovat knihovnu Aspose.Cells. Můžete si ji zdarma stáhnout nebo zakoupit na [Webové stránky Aspose](https://purchase.aspose.com/buy).
3. Základní znalost C#: Trocha znalosti programování v C# vám hodně pomůže porozumět příkladům, které budeme probírat.
4. Soubor s obrázkem: Mějte připravený obrázek (například logo), který chcete vložit do excelového listu.
Teď, když máte vše připravené, pojďme se pustit do kódování!
## Importovat balíčky
Chcete-li začít používat Aspose.Cells ve svém projektu, musíte importovat specifické jmenné prostory. Zde je návod, jak to udělat:
### Vytvořit nový projekt
Ve Visual Studiu vytvořte nový projekt:
- Otevřete Visual Studio.
- Klikněte na „Vytvořit nový projekt“.
- Zvolte „Knihovna tříd (.NET Framework)“ nebo „Konzolová aplikace“ podle vašich preferencí.
### Instalace Aspose.Cells
Balíček Aspose.Cells můžete do svého projektu přidat pomocí NuGetu. Postupujte takto:
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a klikněte na „Instalovat“.
### Přidat pomocí direktiv
V horní části souboru s kódem uveďte následující direktivy:
```csharp
using System.IO;
using Aspose.Cells;
```
Tyto direktivy vám poskytnou přístup ke třídám, které budete potřebovat k manipulaci s excelovými soubory.
Nyní si to rozeberme do podrobných kroků, jak úspěšně proporcionálně umístit obrázek v Excelu.
## Krok 1: Nastavení adresáře
Nejdříve se ujistěte, že máte vyhrazenou složku pro své dokumenty. Zde je návod, jak vytvořit složku, pokud neexistuje:
```csharp
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento úryvek kódu vytvoří nový adresář (pokud neexistuje) pro uložení souborů aplikace Excel. Stačí nahradit `"Your Document Directory"` se skutečnou cestou, kam chcete soubory uložit.
## Krok 2: Vytvoření instance sešitu
Dále si vytvořme nový sešit:
```csharp
Workbook workbook = new Workbook();
```
Tento řádek inicializuje nový objekt sešitu a poskytuje vám prázdné plátno pro práci.
## Krok 3: Přidání nového pracovního listu
Nyní, když máme sešit nastavený, přidejme do něj nový list:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Tím se přidá nový list a vrátí se index tohoto listu, který můžeme později použít k jeho úpravě.
## Krok 4: Přístup k novému pracovnímu listu
Pro manipulaci s nově přidaným listem je potřeba k němu přistupovat:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Teď, `worksheet` nám umožní přidat obsah a obrázky do daného listu.
## Krok 5: Vložení obrázku
A teď přichází ta vzrušující část! Pojďme přidat váš krásný obrázek. Nahraďte ho. `"logo.jpg"` s názvem vašeho obrazového souboru:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Tento řádek přidá obrázek do buňky F6 (protože řádky a sloupce mají nulový index, `5` odkazuje na šestou buňku).
## Krok 6: Přístup k přidanému obrázku
Jakmile je obrázek vložen, můžete k němu přistupovat takto:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
To vám umožní manipulovat s vlastnostmi obrázku.
## Krok 7: Proporcionální umístění obrázku
Nyní umístěme obrázek proporcionálně:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Zde, `UpperDeltaX` a `UpperDeltaY` Upravte polohu obrázku vzhledem k rozměrům buňky. Tyto hodnoty můžete upravit tak, aby váš obrázek byl přesně takový, jaký je.
## Krok 8: Uložte změny
Nakonec uložte sešit, abyste zachovali všechny změny:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Tento řádek uloží váš sešit jako `book1.out.xls` v určeném adresáři.
## Závěr
A tady to máte! Právě jste se naučili, jak proporcionálně umisťovat obrázky v Excelu pomocí Aspose.Cells pro .NET. Nejde jen o vkládání obrázků; jde o to, aby v tabulkách vypadaly perfektně. Jen nezapomeňte: dobře umístěný obrázek může výrazně vylepšit prezentaci vašich dat.
Bavte se experimentováním s různými obrázky a umístěními a neváhejte se hlouběji ponořit do bohatých funkcí, které Aspose.Cells nabízí. Vaše excelovské listy se brzy dočkají pořádné proměny!
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna pro .NET, která umožňuje uživatelům vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.
### Mohu používat Aspose.Cells zdarma?
Ano, Aspose.Cells nabízí bezplatnou zkušební verzi, kterou si můžete stáhnout. [zde](https://releases.aspose.com/).
### Kde najdu dokumentaci?
Můžete získat přístup ke komplexnímu [dokumentace](https://reference.aspose.com/cells/net/) pro Aspose.Cells.
### Podporuje Aspose.Cells všechny obrazové formáty?
Aspose.Cells podporuje různé formáty včetně JPEG, PNG, BMP, GIF a TIFF.
### Jak mohu získat podporu pro Aspose.Cells?
V případě jakýchkoli dotazů neváhejte navštívit [fórum podpory](https://forum.aspose.com/c/cells/9) kde můžete položit své otázky.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}