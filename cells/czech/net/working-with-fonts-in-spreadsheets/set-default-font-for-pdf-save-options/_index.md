---
"description": "Naučte se, jak nastavit výchozí písma pro možnosti ukládání PDF pomocí Aspose.Cells pro .NET a zajistit, aby vaše dokumenty vypadaly pokaždé perfektně."
"linktitle": "Nastavení výchozího písma pro možnosti ukládání PDF"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nastavení výchozího písma pro možnosti ukládání PDF"
"url": "/cs/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení výchozího písma pro možnosti ukládání PDF

## Zavedení
Pokud jde o generování reportů, faktur nebo jakýchkoli jiných dokumentů ve formátu PDF, je prvořadé zajistit, aby váš obsah vypadal správně. Fonty hrají zásadní roli v udržení vizuální přitažlivosti a čitelnosti vašich dokumentů. Co se ale stane, když písmo, které jste použili v souboru Excel, není k dispozici v systému, ve kterém generujete PDF? A v tom případě se hodí Aspose.Cells pro .NET. Tato výkonná knihovna umožňuje nastavit výchozí fonty pro možnosti ukládání PDF, což zajišťuje, že vaše dokumenty budou vypadat profesionálně a konzistentně bez ohledu na to, kde jsou otevřeny.
## Předpoklady
Než začneme, ujistěte se, že máte následující:
1. Visual Studio: K napsání a spuštění kódu budete potřebovat vývojové prostředí, jako je Visual Studio.
2. Aspose.Cells pro .NET: Nejnovější verzi si můžete stáhnout z [tento odkaz](https://releases.aspose.com/cells/net/)Případně jej můžete nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu.
3. Základní znalost C#: Pochopení základů C# vám pomůže sledovat příklady kódu.
4. Ukázkový soubor Excel: Připravte si ukázkový soubor Excel k testování. Můžete si vytvořit soubor s různými fonty a styly, abyste viděli, jak Aspose.Cells zpracovává chybějící fonty.
## Importovat balíčky
Než budete moci ve svém projektu použít Aspose.Cells, musíte importovat potřebné balíčky. Zde je návod, jak to udělat:
1. Otevřete svůj projekt: Spusťte Visual Studio a otevřete stávající projekt nebo vytvořte nový.
2. Přidání odkazů: V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost „Spravovat balíčky NuGet“.
3. Instalace Aspose.Cells: Vyhledejte „Aspose.Cells“ a klikněte na tlačítko „Instalovat“.
4. Přidání použití direktiv: V horní části souboru C# uveďte následující jmenné prostory:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Krok 1: Nastavení adresářů
Před prací se soubory je důležité definovat zdrojový a výstupní adresář. To usnadní nalezení vstupního souboru Excel a uložení vygenerovaných výstupních souborů.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Výstupní adresář
string outputDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` se skutečnou cestou k vašim adresářům.
## Krok 2: Otevřete soubor Excel
Nyní, když máme nastavené adresáře, otevřeme soubor Excel, se kterým chcete pracovat. `Workbook` Třída v Aspose.Cells se používá k načtení dokumentu aplikace Excel.
```csharp
// Otevření souboru aplikace Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Nezapomeňte nahradit název souboru skutečným názvem souboru.
## Krok 3: Nastavení možností vykreslování obrázků
Dále musíme nakonfigurovat možnosti vykreslování pro převod našeho excelového listu do obrazového formátu. Vytvoříme instanci `ImageOrPrintOptions`, s určením typu obrázku a výchozího písma.
```csharp
// Vykreslování do formátu PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
V tomto úryvku kódu nastavíme `CheckWorkbookDefaultFont` majetek `false`což znamená, že pokud nějaké písmo chybí, použije se místo něj zadané výchozí písmo („Times New Roman“).
## Krok 4: Vykreslení listu jako obrázku
Nyní si vykreslíme první list sešitu jako obrázek PNG. Použijeme `SheetRender` třídu, aby toho dosáhla.
```csharp
// Vykreslení prvního listu do obrázku
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Krok 5: Změňte typ obrázku a vykreslení na TIFF
Pokud chcete stejný list vykreslit do jiného formátu obrázku, například TIFF, můžete jednoduše změnit `ImageType` vlastnost a opakujte proces vykreslování.
```csharp
// Nastaveno na formát TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Krok 6: Konfigurace možností ukládání PDF
Dále nastavíme možnosti ukládání PDF. Vytvoříme instanci `PdfSaveOptions`, nastavte výchozí písmo a určete, že chceme kontrolovat chybějící písma.
```csharp
// Konfigurace možností ukládání PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Krok 7: Uložte sešit jako PDF
Po nakonfigurování možností ukládání je čas uložit náš excelový sešit jako soubor PDF. 
```csharp
// Uložit sešit do PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Krok 8: Potvrzení provedení
Nakonec je dobrým zvykem informovat uživatele o úspěšném dokončení procesu. Toho lze dosáhnout pomocí jednoduché konzolové zprávy.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Závěr
Aspose.Cells nabízí flexibilní a robustní způsob, jak manipulovat s excelovými soubory, což vývojářům usnadňuje vytváření vizuálně přitažlivých dokumentů, které si zachovávají formátování. Ať už pracujete na reportech, finančních dokumentech nebo jakékoli jiné formě prezentace dat, kontrola nad vykreslováním písem může výrazně zlepšit kvalitu výstupu.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET, která umožňuje vývojářům manipulovat s excelovými soubory bez nutnosti instalace Microsoft Excelu. Podporuje různé formáty souborů a nabízí bohaté funkce pro práci s tabulkami.
### Jak mohu nastavit výchozí písmo pro soubory aplikace Excel?
Výchozí písmo můžete nastavit pomocí `PdfSaveOptions` třídu a zadejte požadovaný název písma. Tím zajistíte, že i když písmo chybí, dokument bude používat výchozí písmo, které jste zadali.
### Mohu převést soubory aplikace Excel do jiných formátů než PDF?
Rozhodně! Aspose.Cells umožňuje převádět soubory aplikace Excel do různých formátů, včetně obrázků (PNG, TIFF), HTML, CSV a dalších.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je komerční produkt, ale můžete si ho vyzkoušet zdarma s omezenou zkušební verzí. Pro plnou funkčnost si budete muset zakoupit licenci.
### Kde najdu podporu pro Aspose.Cells?
Podporu pro Aspose.Cells naleznete na adrese [Fórum Aspose](https://forum.aspose.com/c/cells/9), kde můžete klást otázky a sdílet své poznatky s ostatními uživateli a vývojáři.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}