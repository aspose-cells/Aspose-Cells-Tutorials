---
title: Worksheet to Image Conversion in .NET
linktitle: Worksheet to Image Conversion in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak převést excelové listy na obrázky v .NET pomocí Aspose.Cells s naším průvodcem krok za krokem. Zefektivněte vizualizaci dat.
weight: 11
url: /cs/net/image-and-chart-operations/worksheet-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Worksheet to Image Conversion in .NET

## Zavedení
Pokud jde o manipulaci se soubory Excel v .NET, Aspose.Cells vyniká jako spolehlivá a robustní knihovna. Jedním z častých úkolů, se kterými se můžete setkat, je převod listu aplikace Excel na obrázek. Tento podrobný průvodce vás celým procesem provede, ať už chcete zobrazit list na webové stránce, zahrnout jej do sestavy nebo data jednoduše sdílet vizuálně. Nakonec budete vybaveni vším, co potřebujete k bezproblémovému převodu pracovních listů na obrázky. Pojďme se tedy ponořit!
## Předpoklady
Než zahájíme konverzi, je nezbytné se ujistit, že máte vše správně nastaveno. Zde jsou předpoklady, které budete potřebovat:
1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Je to IDE, které vám pomůže hladce provozovat vaše .NET projekty.
2.  Aspose.Cells for .NET Library: Musíte získat tuto knihovnu. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/) nebo začít s a[zkušební verze zdarma](https://releases.aspose.com/).
3. Základní znalost C#: Výhodou bude znalost programování v C#, protože naše příklady a vysvětlení budou psány v tomto jazyce.
4.  Ukázkový soubor Excel: Pro demonstraci vytvořte nebo stáhněte soubor Excel. Uložit jako`MyTestBook1.xls` ve vašem projektovém adresáři.
5. Základní porozumění projektům .NET: Vědět, jak vytvořit jednoduchý projekt .NET, to usnadní, ale nebojte se – provedeme vás jednotlivými kroky.
## Importujte balíčky
Prvním krokem na naší cestě je import potřebných balíčků Aspose.Cells do našeho projektu. To je nezbytné, protože nám to umožňuje využívat všechny funkce, které Aspose.Cells nabízí.
## Krok 1: Vytvořte nový projekt 
Chcete-li věci začít, vytvořte nový projekt .NET ve Visual Studiu:
- Otevřete Visual Studio.
- Klikněte na „Vytvořit nový projekt“.
- Vyberte „Console App (.NET Framework)“ nebo „Console App (.NET Core)“ v závislosti na vašich preferencích.
- Pojmenujte svůj projekt (např. WorksheetToImage) a klikněte na „Vytvořit“.
## Krok 2: Přidejte odkaz Aspose.Cells
Nyní, když máme náš projekt, musíme přidat Aspose.Cells:
- Klepněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte nejnovější verzi.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
Jste připraveni na kódovací část!

Nyní si krok za krokem rozeberme skutečný proces převodu. Budeme používat jednoduchý program v jazyce C#, který otevře soubor aplikace Excel, převede list na obrázek a uloží tento obrázek do určeného adresáře.
## Krok 3: Nastavení prostředí
Nejprve nastavte své prostředí definováním cesty k adresáři dokumentů:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Zde definujeme proměnnou tzv`dataDir` která obsahuje cestu k adresáři, kde budou uloženy naše soubory. Nahradit`"Your Document Directory"` se skutečnou cestou ve vašem systému (např. "C:\\MyFiles\\").
## Krok 4: Otevřete sešit aplikace Excel
 Dále otevřeme soubor Excel pomocí`Workbook` třída z Aspose.Cells:
```csharp
// Otevřete soubor šablony Excel.
Workbook book = new Workbook(dataDir + "MyTestBook1.xls");
```
 V tomto kroku vytvoříme instanci`Workbook` třídy a předejte cestu k našemu souboru Excel. To nám umožňuje programově interagovat s obsahem souboru.
## Krok 5: Přístup k listu
Nyní, když máme sešit otevřený, přistupme k prvnímu listu:
```csharp
// Získejte první pracovní list.
Worksheet sheet = book.Worksheets[0];
```
 Zde načteme první pracovní list (index`0` ze sešitu. Pole Aspose.Cells mají nulový index, což znamená, že první list je`0`.
## Krok 6: Definujte možnosti obrázku nebo tisku
 Než obrázek vykreslíme, musíme určit, jak chceme, aby vypadal pomocí`ImageOrPrintOptions`:
```csharp
// Definujte ImageOrPrintOptions
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
// Určete formát obrázku
imgOptions.ImageType = Drawing.ImageType.Jpeg;
// Bude vykreslena pouze jedna stránka pro celý list
imgOptions.OnePagePerSheet = true;
```
 V tomto kroku vytvoříme instanci`ImageOrPrintOptions` . Určíme, že chceme výstup uložit jako obrázek JPEG a nastavíme`OnePagePerSheet` na`true` abyste zajistili zachycení celého listu v jednom snímku.
## Krok 7: Vykreslení listu
S nastavenými možnostmi nyní můžeme vykreslit list:
```csharp
// Vykreslete list s ohledem na zadané možnosti obrázku/tisku
SheetRender sr = new SheetRender(sheet, imgOptions);
// Vykreslete obrázek pro list
Bitmap bitmap = sr.ToImage(0);
```
 The`SheetRender` class pomáhá vykreslit list do bitmapového obrázku. voláme`ToImage(0)` vykreslit nultou stránku (náš první list) do bitmapy.
## Krok 8: Uložení obrázku
Po vykreslení musíme obrázek uložit do určeného adresáře:
```csharp
//Uložte soubor obrázku s určením formátu obrázku.
bitmap.Save(dataDir + "SheetImage.out.jpg");
```
 Zde uložíme bitmapový obrázek, který jsme vygenerovali. Tento řádek zapíše obrázek do`dataDir` umístění s názvem souboru`SheetImage.out.jpg`.
## Krok 9: Oznámení o dokončení
Aby bylo zajištěno dokončení procesu, přidejte jednoduchou zprávu konzoly:
```csharp
// Zobrazit výsledek, aby uživatel věděl, že zpracování skončilo.
System.Console.WriteLine("Conversion to Image(s) completed.");
```
Na tomto řádku se zobrazí potvrzovací zpráva do konzole, která uživateli dává vědět, že převod byl úspěšný.
## Závěr
A tady to máte! V několika jednoduchých krocích jste se naučili, jak převést excelový list na obrázek pomocí Aspose.Cells for .NET. Tento proces je nejen rychlý, ale také výkonný a umožňuje vám snadno vytvářet vizuální reprezentace vašich tabulkových dat.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům vytvářet, manipulovat, převádět a zpracovávat soubory Excelu programově.
### Mohu používat Aspose.Cells zdarma?
 Ano, můžete začít používat Aspose.Cells stažením bezplatné zkušební verze z jejich[webové stránky](https://releases.aspose.com/).
### Jaké formáty obrázků podporuje Aspose.Cells pro export?
Aspose.Cells podporuje různé formáty obrázků, včetně JPEG, PNG, BMP a GIF.
### Kde najdu další podporu pro Aspose.Cells?
 Můžete vstoupit na fórum podpory pro Aspose.Cells[zde](https://forum.aspose.com/c/cells/9).
### Jak získám dočasnou licenci pro Aspose.Cells?
 Dočasnou licenci lze získat návštěvou jejich[dočasná licenční stránka](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
