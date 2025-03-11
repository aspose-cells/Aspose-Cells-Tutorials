---
title: Nastavit výchozí písmo pro možnosti uložení PDF
linktitle: Nastavit výchozí písmo pro možnosti uložení PDF
second_title: Aspose.Cells .NET Excel Processing API
description: Zjistěte, jak nastavit výchozí písma pro možnosti uložení PDF pomocí Aspose.Cells pro .NET, abyste zajistili, že vaše dokumenty budou pokaždé vypadat dokonale.
weight: 11
url: /cs/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit výchozí písmo pro možnosti uložení PDF

## Zavedení
Pokud jde o generování zpráv, faktur nebo jakýchkoli jiných dokumentů ve formátu PDF, je prvořadé zajistit, aby váš obsah vypadal správně. Písma hrají zásadní roli při zachování vizuální přitažlivosti a čitelnosti vašich dokumentů. Co se však stane, když písmo, které jste použili v souboru aplikace Excel, není k dispozici v systému, ve kterém generujete PDF? To je místo, kde se Aspose.Cells for .NET hodí. Tato výkonná knihovna vám umožňuje nastavit výchozí písma pro možnosti ukládání PDF, čímž zajistíte, že vaše dokumenty budou vypadat profesionálně a konzistentně, bez ohledu na to, kde jsou otevřeny.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
1. Visual Studio: K psaní a spouštění kódu budete potřebovat vývojové prostředí, jako je Visual Studio.
2.  Aspose.Cells for .NET: Nejnovější verzi si můžete stáhnout z[tento odkaz](https://releases.aspose.com/cells/net/). Případně jej můžete nainstalovat přes NuGet Package Manager ve Visual Studiu.
3. Základní znalost C#: Pochopení základů C# vám pomůže sledovat příklady kódu.
4. Vzorový soubor Excel: Připravte si vzorový soubor Excel k testování. Můžete si vytvořit jedno s různými fonty a styly, abyste viděli, jak Aspose.Cells zpracovává chybějící fonty.
## Importujte balíčky
Než budete moci použít Aspose.Cells ve svém projektu, musíte importovat potřebné balíčky. Jak na to:
1. Otevřete svůj projekt: Spusťte Visual Studio a otevřete svůj stávající projekt nebo vytvořte nový.
2. Přidat odkazy: Klikněte pravým tlačítkem na svůj projekt v Průzkumníku řešení a vyberte „Spravovat balíčky NuGet“.
3. Instalace Aspose.Cells: Vyhledejte „Aspose.Cells“ a klikněte na tlačítko „Instalovat“.
4. Přidat pomocí direktiv: V horní části souboru C# uveďte následující jmenné prostory:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Krok 1: Nastavte své adresáře
Před prací se soubory je důležité definovat zdrojový a výstupní adresář. To usnadní nalezení vstupního souboru aplikace Excel a uložení vygenerovaných výstupních souborů.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` se skutečnou cestou k vašim adresářům.
## Krok 2: Otevřete soubor aplikace Excel
 Nyní, když máme nastavené adresáře, otevřeme soubor Excel, se kterým chcete pracovat. The`Workbook` třída v Aspose.Cells se používá k načtení dokumentu aplikace Excel.
```csharp
// Otevřete soubor aplikace Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Nezapomeňte nahradit název souboru skutečným názvem souboru.
## Krok 3: Nastavte možnosti vykreslování obrázků
Dále musíme nakonfigurovat možnosti vykreslování pro převod našeho listu Excel do formátu obrázku. Vytvoříme instanci`ImageOrPrintOptions`, určující typ obrázku a výchozí písmo.
```csharp
// Vykreslování do formátu souboru PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 V tomto fragmentu kódu nastavíme`CheckWorkbookDefaultFont` majetek do`false`, což znamená, že pokud některá písma chybí, použije se místo toho zadané výchozí písmo („Times New Roman“).
## Krok 4: Vykreslete list jako obrázek
 Nyní vykreslíme první list sešitu jako obrázek PNG. Použijeme`SheetRender` třídy, aby se to podařilo.
```csharp
// Vykreslete první list na obrázek
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Krok 5: Změňte typ obrázku a vykreslení na TIFF
 Pokud chcete vykreslit stejný list do jiného formátu obrázku, jako je TIFF, můžete jednoduše změnit`ImageType` vlastnost a opakujte proces vykreslování.
```csharp
// Nastavte na formát TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Krok 6: Nakonfigurujte možnosti uložení PDF
 Dále nastavíme možnosti uložení PDF. Vytvoříme instanci`PdfSaveOptions`nastavte výchozí písmo a zadejte, že chceme zkontrolovat chybějící písma.
```csharp
// Konfigurace možností uložení PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Krok 7: Uložte sešit jako PDF
S nakonfigurovanými možnostmi ukládání je čas uložit náš excelový sešit jako soubor PDF. 
```csharp
// Uložte sešit do PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Krok 8: Potvrďte provedení
Nakonec je dobré dát uživateli vědět, že proces byl úspěšně dokončen. Toho lze dosáhnout pomocí jednoduché konzolové zprávy.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Závěr
Aspose.Cells poskytuje flexibilní a robustní způsob manipulace se soubory Excel, což vývojářům usnadňuje vytváření vizuálně přitažlivých dokumentů, které si zachovávají své formátování. Ať už pracujete na sestavách, finančních dokumentech nebo jakékoli jiné formě prezentace dat, kontrola nad vykreslováním písem může výrazně zlepšit kvalitu vašeho výstupu.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům manipulovat se soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel. Podporuje různé formáty souborů a nabízí bohaté funkce pro práci s tabulkami.
### Jak mohu nastavit výchozí písmo pro soubory Excel?
 Výchozí písmo můžete nastavit pomocí`PdfSaveOptions` třídy a zadejte požadovaný název písma. Tím je zajištěno, že i když nějaké písmo chybí, váš dokument použije výchozí písmo, které jste zadali.
### Mohu převést soubory Excel do jiných formátů než PDF?
Absolutně! Aspose.Cells umožňuje převádět soubory aplikace Excel do různých formátů, včetně obrázků (PNG, TIFF), HTML, CSV a dalších.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je komerční produkt, ale můžete si ho vyzkoušet zdarma s omezenou zkušební verzí. Pro plnou funkčnost si budete muset zakoupit licenci.
### Kde najdu podporu pro Aspose.Cells?
 Podporu pro Aspose.Cells najdete na stránce[Aspose fórum](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a sdílet poznatky s ostatními uživateli a vývojáři.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
