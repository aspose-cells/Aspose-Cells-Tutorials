---
"description": "Naučte se, jak převést excelové listy na obrázky v .NET pomocí Aspose.Cells s naším podrobným návodem. Zjednodušte si vizualizaci dat."
"linktitle": "Převod pracovního listu na obrázek v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Převod pracovního listu na obrázek v .NET"
"url": "/cs/net/image-and-chart-operations/worksheet-to-image-conversion/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Převod pracovního listu na obrázek v .NET

## Zavedení
Pokud jde o manipulaci s excelovými soubory v .NET, Aspose.Cells vyniká jako spolehlivá a robustní knihovna. Jedním z častých úkolů, se kterými se můžete setkat, je převod excelového listu do obrázku. Ať už chcete list zobrazit na webové stránce, zahrnout ho do sestavy nebo jednoduše vizuálně sdílet data, tento podrobný návod vás provede celým procesem. Nakonec budete vybaveni vším, co potřebujete k bezproblémovému převodu listů do obrázků. Tak se do toho pustíme!
## Předpoklady
Než začneme s konverzí, je nezbytné se ujistit, že máte vše správně nastavené. Zde jsou předpoklady, které budete potřebovat:
1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Je to vývojové prostředí (IDE), které vám pomůže hladce spouštět vaše .NET projekty.
2. Knihovna Aspose.Cells pro .NET: Tuto knihovnu si musíte pořídit. Můžete [stáhněte si to zde](https://releases.aspose.com/cells/net/) nebo začněte s [bezplatná zkušební verze](https://releases.aspose.com/).
3. Základní znalost C#: Znalost programování v C# bude přínosem, protože naše příklady a vysvětlení budou napsány v tomto jazyce.
4. Ukázkový soubor aplikace Excel: Pro demonstraci si vytvořte nebo stáhněte soubor aplikace Excel. Uložte jej jako `MyTestBook1.xls` ve vašem adresáři projektu.
5. Základní znalost projektů .NET: Znalost vytvoření jednoduchého projektu .NET vám to usnadní, ale nebojte se – provedeme vás jednotlivými kroky.
## Importovat balíčky
Prvním krokem na naší cestě je import potřebných balíčků Aspose.Cells do našeho projektu. To je nezbytné, protože nám to umožní využívat všechny funkce, které Aspose.Cells nabízí.
## Krok 1: Vytvořte nový projekt 
Pro začátek vytvořte nový .NET projekt ve Visual Studiu:
- Otevřete Visual Studio.
- Klikněte na „Vytvořit nový projekt“.
- Vyberte možnost „Konzolová aplikace (.NET Framework)“ nebo „Konzolová aplikace (.NET Core)“ podle vašich preferencí.
- Pojmenujte svůj projekt (např. WorksheetToImage) a klikněte na tlačítko „Vytvořit“.
## Krok 2: Přidání odkazu na Aspose.Cells
Nyní, když máme náš projekt, musíme přidat Aspose.Cells:
- Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
- Vyberte možnost „Spravovat balíčky NuGet“.
- Vyhledejte „Aspose.Cells“ a nainstalujte nejnovější verzi.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
Jste připraveni na kódování!

Nyní si krok za krokem rozebereme samotný proces převodu. Použijeme jednoduchý program v C#, který otevře soubor aplikace Excel, převede pracovní list na obrázek a uloží tento obrázek do zadaného adresáře.
## Krok 3: Nastavení prostředí
Nejprve si nastavte prostředí definováním cesty k adresáři s dokumenty:
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Zde definujeme proměnnou s názvem `dataDir` , který obsahuje cestu k adresáři, kde budou uloženy naše soubory. Nahraďte `"Your Document Directory"` with the actual path on your system (e.g., "C:\\MyFiles\\").
## Krok 4: Otevřete sešit aplikace Excel
Dále otevřeme soubor Excel pomocí `Workbook` třída z Aspose.Cells:
```csharp
// Otevřete šablonu souboru aplikace Excel.
Workbook book = new Workbook(dataDir + "MyTestBook1.xls");
```
V tomto kroku vytvoříme instanci `Workbook` třídu a předáme cestu k našemu souboru aplikace Excel. To nám umožní programově interagovat s obsahem souboru.
## Krok 5: Přístup k pracovnímu listu
Nyní, když máme otevřený sešit, pojďme se podívat na první list:
```csharp
// Vezměte si první pracovní list.
Worksheet sheet = book.Worksheets[0];
```
Zde načteme první pracovní list (index `0`) ze sešitu. Pole Aspose.Cells mají nulový index, což znamená, že první list je `0`.
## Krok 6: Definování možností obrázku nebo tisku
Než obrázek vykreslíme, musíme si nejprve určit, jak má vypadat, a to pomocí `ImageOrPrintOptions`:
```csharp
// Definovat možnosti obrázku nebo tisku
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
// Zadejte formát obrázku
imgOptions.ImageType = Drawing.ImageType.Jpeg;
// Zobrazí se pouze jedna stránka z celého listu.
imgOptions.OnePagePerSheet = true;
```
V tomto kroku vytvoříme instanci `ImageOrPrintOptions`Určíme, že chceme výstup uložit jako obrázek JPEG a nastavíme `OnePagePerSheet` na `true` aby se zajistilo, že celý list bude zachycen na jednom snímku.
## Krok 7: Vykreslení pracovního listu
S nastavenými možnostmi nyní můžeme vykreslit pracovní list:
```csharp
// Vykreslení listu s ohledem na zadané možnosti obrázku/tisku
SheetRender sr = new SheetRender(sheet, imgOptions);
// Vykreslení obrázku pro list
Bitmap bitmap = sr.ToImage(0);
```
Ten/Ta/To `SheetRender` třída pomáhá vykreslit pracovní list do bitmapového obrázku. Voláme `ToImage(0)` vykreslit nultou stránku (náš první list) do bitmapy.
## Krok 8: Uložení obrázku
Po vykreslení musíme obrázek uložit do zadaného adresáře:
```csharp
// Uložte soubor s obrázkem s uvedením jeho formátu.
bitmap.Save(dataDir + "SheetImage.out.jpg");
```
Zde ukládáme vygenerovaný bitmapový obrázek. Tento řádek zapíše obrázek do `dataDir` umístění s názvem souboru `SheetImage.out.jpg`.
## Krok 9: Oznámení o dokončení
Abychom zajistili dokončení procesu, přidejme jednoduchou konzolovou zprávu:
```csharp
// Zobrazit výsledek, aby uživatel věděl, že zpracování je dokončeno.
System.Console.WriteLine("Conversion to Image(s) completed.");
```
Tento řádek vypíše do konzole potvrzovací zprávu, která uživatele informuje o úspěšném provedení konverze.
## Závěr
A máte to! V několika jednoduchých krocích jste se naučili, jak převést list aplikace Excel na obrázek pomocí nástroje Aspose.Cells pro .NET. Tento proces je nejen rychlý, ale také výkonný a umožňuje vám bez námahy vytvářet vizuální reprezentace dat z tabulky.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je knihovna .NET, která umožňuje vývojářům programově vytvářet, manipulovat, převádět a zpracovávat soubory aplikace Excel.
### Mohu používat Aspose.Cells zdarma?
Ano, Aspose.Cells můžete začít používat stažením bezplatné zkušební verze z jejich [webové stránky](https://releases.aspose.com/).
### Jaké obrazové formáty Aspose.Cells podporuje pro export?
Aspose.Cells podporuje různé obrazové formáty, včetně JPEG, PNG, BMP a GIF.
### Kde najdu další podporu pro Aspose.Cells?
Můžete se připojit k fóru podpory pro Aspose.Cells [zde](https://forum.aspose.com/c/cells/9).
### Jak získám dočasnou licenci pro Aspose.Cells?
Dočasné povolení lze získat návštěvou jejich [stránka s dočasnou licencí](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}