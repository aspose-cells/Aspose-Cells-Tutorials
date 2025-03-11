---
title: Přidat Spinner Control do listu v Excelu
linktitle: Přidat Spinner Control do listu v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném návodu se dozvíte, jak přidat ovládací prvek Spinner do listu aplikace Excel pomocí Aspose.Cells for .NET.
weight: 23
url: /cs/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat Spinner Control do listu v Excelu

## Zavedení
Pokud se noříte do světa automatizace Excelu pomocí .NET, pravděpodobně jste narazili na potřebu interaktivnějších ovládacích prvků v tabulkách. Jedním z takových ovládacích prvků je Spinner, který umožňuje uživatelům snadno zvyšovat nebo snižovat hodnotu. V tomto tutoriálu prozkoumáme, jak přidat ovládací prvek Spinner do listu aplikace Excel pomocí Aspose.Cells pro .NET. Rozdělíme to na stravitelné kroky, abyste mohli plynule pokračovat. 
## Předpoklady
Než se pustíme do kódu, ujistěte se, že máte vše nastaveno pro hladký průběh:
1.  Aspose.Cells for .NET: Ujistěte se, že máte knihovnu Aspose.Cells. Pokud jste jej ještě nenainstalovali, můžete si stáhnout nejnovější verzi z[odkaz ke stažení](https://releases.aspose.com/cells/net/).
2. Visual Studio: Měli byste mít funkční instalaci sady Visual Studio nebo jakéhokoli jiného .NET IDE, které dáváte přednost.
3. Základní znalost C#: Znalost programování v C# vám pomůže snadno porozumět úryvkům kódu. Pokud právě začínáte, nebojte se! Provedu vás každou částí.
## Importujte balíčky
Chcete-li ve svém projektu použít Aspose.Cells, musíte importovat potřebné jmenné prostory. Prostředí můžete nastavit takto:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto jmenné prostory vám umožňují přístup k základním funkcím Aspose.Cells, včetně manipulace se sešitem a možností kreslení pro tvary, jako je Spinner.
Nyní, když jsme pokryli předpoklady a importovali potřebné balíčky, pojďme se ponořit do podrobného průvodce. Každý krok je navržen tak, aby byl jasný a stručný, abyste jej mohli snadno implementovat.
## Krok 1: Nastavte adresář projektu
Než začnete kódovat, je dobré si soubory uspořádat. Vytvořme adresář pro naše soubory Excel.
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Zde specifikujeme cestu pro náš adresář dokumentů. Pokud adresář neexistuje, vytvoříme jej. To zajišťuje, že všechny naše vygenerované soubory mají určený domov.
## Krok 2: Vytvořte nový sešit
Nyní je čas vytvořit sešit aplikace Excel, kam přidáme ovládací prvek Spinner.
```csharp
// Vytvořte nový sešit.
Workbook excelbook = new Workbook();
```
 The`Workbook` třída představuje soubor Excel. Jeho instancí vytvoříme nový sešit připravený k úpravám.
## Krok 3: Otevřete první pracovní list
Náš Spinner přidáme do prvního listu v sešitu.
```csharp
// Získejte první pracovní list.
Worksheet worksheet = excelbook.Worksheets[0];
```
Tento řádek přistupuje k prvnímu listu (index 0) z našeho sešitu. Můžete mít více listů, ale pro tento příklad to uděláme jednoduše.
## Krok 4: Práce s buňkami
Dále pracujme s buňkami v našem listu. Nastavíme nějaké hodnoty a styly.
```csharp
// Získejte buňky listu.
Cells cells = worksheet.Cells;
// Zadejte hodnotu řetězce do buňky A1.
cells["A1"].PutValue("Select Value:");
// Nastavte barvu písma buňky.
cells["A1"].GetStyle().Font.Color = Color.Red;
// Nastavte text písma tučně.
cells["A1"].GetStyle().Font.IsBold = true;
// Zadejte hodnotu do buňky A2.
cells["A2"].PutValue(0);
```
Zde vyplníme buňku A1 výzvou, použijeme červenou barvu a text uděláme tučným. Nastavíme také buňku A2 na počáteční hodnotu 0, která bude propojena s naším Spinnerem.
## Krok 5: Upravte styl buňky A2
Dále použijeme některé styly na buňku A2, aby byla vizuálně přitažlivější.
```csharp
// Nastavte barvu stínování na černou s plným pozadím.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// Nastavte barvu písma buňky.
cells["A2"].GetStyle().Font.Color = Color.White;
// Nastavte text písma tučně.
cells["A2"].GetStyle().Font.IsBold = true;
```
Do buňky A2 přidáváme černé pozadí s plným vzorem a nastavujeme barvu písma na bílou. Díky tomuto kontrastu vynikne na pracovním listu.
## Krok 6: Přidejte ovladač Spinner
Nyní jsme připraveni přidat ovládací prvek Spinner do našeho listu.
```csharp
// Přidejte ovládací prvek spinneru.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
Tento řádek přidá do listu ovládací prvek Spinner. Parametry určují polohu a velikost Spinneru (řádek, sloupec, šířka, výška).
## Krok 7: Nakonfigurujte vlastnosti Spinner
Přizpůsobme si chování Spinneru tak, aby vyhovovalo našim potřebám.
```csharp
// Nastavte typ umístění spinneru.
spinner.Placement = PlacementType.FreeFloating;
// Nastavte propojenou buňku pro ovládací prvek.
spinner.LinkedCell = "A2";
// Nastavte maximální hodnotu.
spinner.Max = 10;
//Nastavte minimální hodnotu.
spinner.Min = 0;
// Nastavte změnu přírůstku pro ovládací prvek.
spinner.IncrementalChange = 2;
// Nastavte 3D stínování.
spinner.Shadow = true;
```
Zde nastavíme vlastnosti Spinneru. Propojíme ji s buňkou A2 a umožníme jí ovládat hodnotu tam zobrazenou. Minimální a maximální hodnoty definují rozsah, ve kterém může Spinner pracovat, zatímco přírůstková změna určuje, jak moc se hodnota změní s každým kliknutím. Přidáním 3-D stínování získá leštěný vzhled.
## Krok 8: Uložte soubor Excel
Nakonec si uložme náš excelový sešit s přiloženým Spinnerem.
```csharp
// Uložte soubor aplikace Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
Tento příkaz uloží sešit do zadaného adresáře. Název souboru můžete podle potřeby změnit.
## Závěr
tady to máte! Úspěšně jste přidali ovládací prvek Spinner do listu aplikace Excel pomocí Aspose.Cells pro .NET. Tento interaktivní prvek zlepšuje uživatelskou zkušenost tím, že umožňuje rychlé úpravy hodnot. Ať už vytváříte nástroj pro dynamické vytváření sestav nebo formulář pro zadávání dat, ovládací prvek Spinner může být cenným doplňkem. 
## FAQ
### Co je ovládací prvek Spinner v Excelu?
Ovládací prvek Spinner umožňuje uživatelům snadno zvyšovat nebo snižovat číselnou hodnotu a poskytuje intuitivní způsob výběru.
### Mohu přizpůsobit vzhled Spinneru?
Ano, můžete upravit jeho velikost, polohu a dokonce i jeho 3D stínování pro uhlazenější vzhled.
### Potřebuji licenci k používání Aspose.Cells?
 Aspose.Cells nabízí bezplatnou zkušební verzi, ale pro produkční použití je vyžadována placená licence. Podívejte se na[koupit opce](https://purchase.aspose.com/buy).
### Jak mohu získat pomoc s Aspose.Cells?
 Pro podporu navštivte[Aspose fórum](https://forum.aspose.com/c/cells/9) kde můžete klást otázky a hledat odpovědi.
### Je možné přidat více spinnerů do stejného listu?
Absolutně! Pomocí stejných kroků pro každý ovládací prvek můžete přidat tolik Spinnerů, kolik potřebujete.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
