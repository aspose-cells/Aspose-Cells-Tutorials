---
"description": "V tomto podrobném tutoriálu se naučíte, jak přidat ovládací prvek Spinner do listu aplikace Excel pomocí Aspose.Cells pro .NET."
"linktitle": "Přidání ovládacího prvku Spinner do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání ovládacího prvku Spinner do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání ovládacího prvku Spinner do listu v Excelu

## Zavedení
Pokud se ponořujete do světa automatizace Excelu pomocí .NET, pravděpodobně jste narazili na potřebu interaktivnějších ovládacích prvků ve vašich tabulkách. Jedním z takových ovládacích prvků je Spinner, který uživatelům umožňuje snadno zvyšovat nebo snižovat hodnotu. V tomto tutoriálu se podíváme na to, jak přidat ovládací prvek Spinner do listu Excelu pomocí Aspose.Cells pro .NET. Rozdělíme to do srozumitelných kroků, abyste mohli plynule sledovat. 
## Předpoklady
Než se pustíme do kódu, ujistěme se, že máte vše nastavené pro hladký chod:
1. Aspose.Cells pro .NET: Ujistěte se, že máte knihovnu Aspose.Cells. Pokud ji ještě nemáte nainstalovanou, můžete si stáhnout nejnovější verzi z [odkaz ke stažení](https://releases.aspose.com/cells/net/).
2. Visual Studio: Měli byste mít funkční instalaci Visual Studia nebo jiného preferovaného vývojového prostředí .NET.
3. Základní znalost C#: Znalost programování v C# vám pomůže snadno porozumět úryvkům kódu. Pokud s programováním teprve začínáte, nebojte se! Provedu vás každou částí.
## Importovat balíčky
Chcete-li ve svém projektu použít Aspose.Cells, musíte importovat potřebné jmenné prostory. Zde je návod, jak si můžete nastavit prostředí:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám umožňují přístup k základním funkcím Aspose.Cells, včetně manipulace se sešitem a možností kreslení tvarů, jako je například Spinner.
Nyní, když jsme si probrali předpoklady a importovali potřebné balíčky, pojďme se ponořit do podrobného návodu. Každý krok je navržen tak, aby byl jasný a stručný, abyste ho mohli snadno implementovat.
## Krok 1: Nastavení adresáře projektu
Než začnete s kódováním, je dobrým zvykem uspořádat si soubory. Vytvořme si adresář pro naše excelovské soubory.
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Zde zadáme cestu k adresáři s našimi dokumenty. Pokud adresář neexistuje, vytvoříme ho. Tím zajistíme, že všechny naše vygenerované soubory budou mít určené domovské umístění.
## Krok 2: Vytvořte nový sešit
Nyní je čas vytvořit sešit aplikace Excel, kam přidáme ovládací prvek Spinner.
```csharp
// Vytvořte instanci nového sešitu.
Workbook excelbook = new Workbook();
```
Ten/Ta/To `Workbook` Třída představuje soubor aplikace Excel. Jejím vytvořením instance vytvoříme nový sešit připravený k úpravám.
## Krok 3: Přístup k prvnímu pracovnímu listu
Náš Spinner přidáme na první list v sešitu.
```csharp
// Vezměte si první pracovní list.
Worksheet worksheet = excelbook.Worksheets[0];
```
Tento řádek přistupuje k prvnímu listu (index 0) z našeho sešitu. Můžete mít více listů, ale v tomto příkladu to zjednodušíme.
## Krok 4: Práce s buňkami
Dále si pojďme popracovat s buňkami v našem listu. Nastavíme si nějaké hodnoty a styly.
```csharp
// Získejte buňky pracovního listu.
Cells cells = worksheet.Cells;
// Vložte řetězcovou hodnotu do buňky A1.
cells["A1"].PutValue("Select Value:");
// Nastavte barvu písma buňky.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Nastavte tučné písmo textu.
cells["A1"].GetStyle().Font.IsBold = true;
// Vložte hodnotu do buňky A2.
cells["A2"].PutValue(0);
```
Zde vyplníme buňku A1 výzvou, použijeme červenou barvu a text zvýrazníme tučně. Buňku A2 také nastavíme na počáteční hodnotu 0, která bude propojena s naším číselníkem.
## Krok 5: Stylizace buňky A2
Dále aplikujme na buňku A2 nějaké styly, aby byla vizuálně atraktivnější.
```csharp
// Nastavte barvu stínování na černou s plným pozadím.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Nastavte barvu písma buňky.
cells["A2"].GetStyle().Font.Color = Color.White;
// Nastavte tučné písmo textu.
cells["A2"].GetStyle().Font.IsBold = true;
```
Do buňky A2 přidáme černé pozadí s plným vzorem a nastavíme barvu písma na bílou. Tento kontrast ji na listu zvýrazní.
## Krok 6: Přidání ovládacího prvku Spinner
Nyní jsme připraveni přidat ovládací prvek Spinner do našeho listu.
```csharp
// Přidejte ovládací prvek číselníku.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Tento řádek přidá do listu ovládací prvek Spinner. Parametry určují polohu a velikost Spinneru (řádek, sloupec, šířka, výška).
## Krok 7: Konfigurace vlastností rotačního ovladače
Pojďme si přizpůsobit chování Spinneru našim potřebám.
```csharp
// Nastavte typ umístění spinneru.
spinner.Placement = PlacementType.FreeFloating;
// Nastavte propojenou buňku pro ovládací prvek.
spinner.LinkedCell = "A2";
// Nastavte maximální hodnotu.
spinner.Max = 10;
// Nastavte minimální hodnotu.
spinner.Min = 0;
// Nastavte změnu přírůstku pro ovládací prvek.
spinner.IncrementalChange = 2;
// Nastavte 3D stínování.
spinner.Shadow = true;
```
Zde nastavujeme vlastnosti prvku Spinner. Propojíme ho s buňkou A2, což mu umožní ovládat hodnotu, která se v něm zobrazuje. Minimální a maximální hodnota definují rozsah, ve kterém může prvk Spinner pracovat, zatímco inkrementální změna určuje, o kolik se hodnota mění s každým kliknutím. Přidání 3D stínování mu dodá elegantní vzhled.
## Krok 8: Uložte soubor Excel
Nakonec si uložme náš excelový sešit s číselníkem.
```csharp
// Uložte soubor Excelu.
excelbook.Save(dataDir + "book1.out.xls");
```
Tento příkaz uloží sešit do zadaného adresáře. Název souboru můžete podle potřeby změnit.
## Závěr
A tady to máte! Úspěšně jste přidali ovládací prvek Spinner do listu aplikace Excel pomocí Aspose.Cells pro .NET. Tento interaktivní prvek vylepšuje uživatelský zážitek tím, že umožňuje rychlé úpravy hodnot. Ať už vytváříte dynamický nástroj pro tvorbu sestav nebo formulář pro zadávání dat, ovládací prvek Spinner může být cenným doplňkem. 
## Často kladené otázky
### Co je ovládací prvek Spinner v Excelu?
Ovládací prvek Spinner umožňuje uživatelům snadno zvyšovat nebo snižovat číselnou hodnotu a poskytuje intuitivní způsob provádění výběru.
### Mohu si přizpůsobit vzhled Spinneru?
Ano, můžete upravit jeho velikost, polohu a dokonce i 3D stínování pro elegantnější vzhled.
### Potřebuji licenci k používání Aspose.Cells?
Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro produkční použití je vyžadována placená licence. Podívejte se na [možnosti nákupu](https://purchase.aspose.com/buy).
### Jak mohu získat pomoc s Aspose.Cells?
Pro podporu navštivte [Fórum Aspose](https://forum.aspose.com/c/cells/9) kde můžete klást otázky a hledat odpovědi.
### Je možné přidat více Spinnerů do stejného listu?
Rozhodně! Můžete přidat libovolný počet spinnerů podle potřeby podle stejných kroků pro každý ovládací prvek.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}