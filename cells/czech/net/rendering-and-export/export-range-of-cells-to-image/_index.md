---
title: Exportujte rozsah buněk do obrázku pomocí Aspose.Cells
linktitle: Exportujte rozsah buněk do obrázku pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Pomocí tohoto podrobného průvodce můžete snadno exportovat rozsahy buněk Excelu do obrázků pomocí Aspose.Cells for .NET. Vylepšete své reportování a prezentace.
weight: 14
url: /cs/net/rendering-and-export/export-range-of-cells-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportujte rozsah buněk do obrázku pomocí Aspose.Cells

## Zavedení
Při práci se soubory aplikace Excel může být neuvěřitelně užitečná schopnost převádět konkrétní rozsahy buněk na obrázky. Představte si, že potřebujete sdílet kritickou část vaší tabulky, aniž byste museli posílat celý dokument – zde vstupuje do hry Aspose.Cells for .NET! V této příručce vás krok za krokem provedeme exportem řady buněk do obrázku, čímž zajistíme, že pochopíte každou část procesu bez jakýchkoli technických překážek.
## Předpoklady
Než se pustíte do výukového programu, existuje několik předpokladů, abyste se ujistili, že máte vše správně nastaveno:
1. Visual Studio: Ujistěte se, že máte v systému nainstalované Visual Studio.
2.  Aspose.Cells for .NET: Stáhněte si tuto knihovnu z[Aspose stránky](https://releases.aspose.com/cells/net/). Můžete také zahájit bezplatnou zkušební verzi, pokud si přejete prozkoumat její možnosti předtím, než se zapojíte.
3. Základní znalost C#: Znalost C# a frameworku .NET vám pomůže lépe porozumět kódu.
4.  Ukázkový soubor Excel: V tomto tutoriálu použijeme soubor s názvem`sampleExportRangeOfCellsInWorksheetToImage.xlsx`. Pro účely testování můžete vytvořit jednoduchý soubor Excel.
Nyní, když máme pokryty předpoklady, pojďme rovnou do kódu!
## Importujte balíčky
Pro začátek musíme importovat základní jmenné prostory. Jak na to:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Tyto balíčky nám umožní pracovat se sešity, listy a spravovat vykreslování našich rozsahů buněk.
## Krok 1: Nastavte cesty k adresáři
Nastavení adresářů se může zdát všední, ale je velmi důležité. Tento krok zajistí, že váš program ví, kde najít soubory a kam uložit exportované obrázky.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"`se skutečnou cestou, kde jsou umístěny vaše soubory. Může to být cesta na místním disku nebo síťový adresář.
## Krok 2: Vytvořte sešit ze zdrojového souboru
 Dalším krokem je vytvoření a`Workbook` objekt, který slouží jako váš vstupní bod do souboru Excel.
```csharp
// Vytvořte sešit ze zdrojového souboru.
Workbook workbook = new Workbook(sourceDir + "sampleExportRangeOfCellsInWorksheetToImage.xlsx");
```
 Zde vytvoříme nový`Workbook` předání úplné cesty k souboru Excel, se kterým chcete pracovat. Tento krok otevře soubor a připraví jej pro manipulaci.
## Krok 3: Otevřete první pracovní list
Jakmile máme náš sešit, potřebujeme získat přístup k listu obsahujícímu data, která chceme exportovat.
```csharp
// Otevřete první pracovní list
Worksheet worksheet = workbook.Worksheets[0];
```
 The`Worksheets` kolekce je indexovaná 0, což znamená`Worksheets[0]` nám dává první list. Pokud chcete jiný list, můžete index upravit.
## Krok 4: Nastavte oblast tisku
Dále musíme definovat oblast, kterou chceme exportovat jako obrázek. To se provádí nastavením oblasti tisku na listu.
```csharp
// Nastavte oblast tisku s požadovaným rozsahem
worksheet.PageSetup.PrintArea = "D8:G16";
```
tomto případě určujeme, že chceme exportovat buňky z D8 do G16. Upravte tyto odkazy na buňky na základě dat, která chcete zachytit.
## Krok 5: Nakonfigurujte okraje
Ujistěte se, že náš exportovaný obrázek neobsahuje žádné zbytečné mezery. Všechny okraje nastavíme na nulu.
```csharp
// Nastavte všechny okraje na 0
worksheet.PageSetup.LeftMargin = 0;
worksheet.PageSetup.RightMargin = 0;
worksheet.PageSetup.TopMargin = 0;
worksheet.PageSetup.BottomMargin = 0;
```
Tento krok je zásadní pro to, aby výsledný obrázek perfektně seděl, aniž by kolem něj byl nějaký nepořádek.
## Krok 6: Nastavte možnosti obrázku
Dále nastavíme možnosti, jak se bude obrázek vykreslovat. To zahrnuje specifikaci rozlišení a typu obrázku.
```csharp
// Nastavte možnost OnePagePerSheet jako true
ImageOrPrintOptions options = new ImageOrPrintOptions();
options.OnePagePerSheet = true;
options.ImageType = ImageType.Jpeg;
options.HorizontalResolution = 200;
options.VerticalResolution = 200;
```
Zde uvádíme, že chceme, aby byl obrázek ve formátu JPEG s rozlišením 200 DPI. Neváhejte a upravte DPI podle svých potřeb.
## Krok 7: Vykreslení listu na obrázek
Nyní přichází ta vzrušující část: vlastně vykreslení listu na obrázek!
```csharp
// Udělejte si obrázek svého pracovního listu
SheetRender sr = new SheetRender(worksheet, options);
sr.ToImage(0, outputDir + "outputExportRangeOfCellsInWorksheetToImage.jpg");
```
 Vytváříme a`SheetRender` instance a volání`ToImage`vygenerovat obrázek z první stránky zadaného listu. Obrázek se uloží do výstupního adresáře se zadaným názvem souboru.
## Krok 8: Potvrďte provedení
Nakonec je vždy dobré po dokončení operace poskytnout zpětnou vazbu, takže vytiskneme zprávu do konzole.
```csharp
Console.WriteLine("ExportRangeOfCellsInWorksheetToImage executed successfully.\r\n");
```
Tento krok je zásadní pro potvrzení úspěchu operace, zejména při spouštění kódu v konzolové aplikaci.
## Závěr
A tady to máte – váš podrobný průvodce pro export řady buněk do obrázku pomocí Aspose.Cells for .NET! Tato výkonná knihovna vám umožňuje bezproblémově manipulovat a pracovat se soubory aplikace Excel a nyní víte, jak zachytit tyto důležité buňky jako obrázky. Ať už jde o reportování, prezentace nebo prostě sdílení konkrétních dat, tato metoda je neuvěřitelně šikovná a efektivní. 
## FAQ
### Mohu změnit formát obrázku?
 Ano! Můžete nastavit`ImageType` vlastnost pro podporu dalších formátů, jako je PNG nebo BMP.
### Co když chci exportovat více rozsahů?
Budete muset opakovat kroky vykreslování pro každý rozsah, který chcete exportovat.
### Existuje omezení velikosti rozsahu, který mohu exportovat?
Zatímco Aspose.Cells je poměrně robustní, extrémně velké rozsahy mohou ovlivnit výkon. Nejlepší je testovat v rozumných mezích.
### Mohu tento proces automatizovat?
Absolutně! Tento kód můžete integrovat do větších aplikací nebo skriptů a automatizovat tak své úkoly v Excelu.
### Kde mohu získat další podporu?
 Pro další pomoc navštivte[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
