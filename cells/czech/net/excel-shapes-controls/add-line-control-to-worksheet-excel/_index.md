---
"description": "V tomto komplexním tutoriálu se naučíte přidávat a upravovat ovládací prvky čar v listech aplikace Excel pomocí Aspose.Cells pro .NET."
"linktitle": "Přidání ovládacího prvku řádku do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidání ovládacího prvku řádku do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-line-control-to-worksheet-excel/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání ovládacího prvku řádku do listu v Excelu

## Zavedení
Excelovské tabulky nejsou jen o řádcích a sloupcích dat; jsou také plátnem pro vizualizaci. Přidání ovládacích prvků čáry může vylepšit způsob, jakým jsou informace v listech reprezentovány, a učinit vztahy a trendy mnohem jasnějšími. Představujeme Aspose.Cells pro .NET, výkonnou knihovnu, která zjednodušuje proces programového vytváření a manipulace s excelovými soubory. V této příručce vás provedeme kroky pro přidání ovládacích prvků čáry do listu pomocí Aspose.Cells. Pokud jste připraveni posunout své znalosti Excelu na vyšší úroveň, pojďme se do toho pustit!
## Předpoklady
Než začnete přidávat řádky do listů aplikace Excel, budete potřebovat následující:
1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Pokud ne, můžete si ho stáhnout z [webové stránky](https://visualstudio.microsoft.com/).
2. Aspose.Cells pro .NET: Na tuto knihovnu je nutné odkazovat ve vašem projektu. Podrobnou dokumentaci naleznete [zde](https://reference.aspose.com/cells/net/) a stáhněte si knihovnu [zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže porozumět kódu, který budeme probírat.
4. Prostředí Windows: Protože Aspose.Cells je navržen pro aplikace .NET, je preferováno prostředí Windows.
## Importovat balíčky
Než začneme přidávat řádky do vašeho excelového listu, nastavme si naše kódovací prostředí. Zde je návod, jak importovat požadovaný balíček Aspose.Cells do vašeho projektu.
### Vytvořit nový projekt
- Otevřete Visual Studio.
- Vytvořte nový projekt konzolové aplikace. Můžete ho pojmenovat libovolně – pro přehlednost třeba „ExcelLineDemo“.
### Instalace Aspose.Cells
- Přejděte do Správce balíčků NuGet ve Visual Studiu (`Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`).
- Hledat `Aspose.Cells` a nainstalujte jej. Tato akce přidá do vašeho projektu potřebné knihovny.
### Importovat jmenný prostor
Na začátek hlavního souboru programu přidejte následující direktivu using, která zpřístupní Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Díky tomu nyní můžete používat všechny funkce z knihovny Aspose.Cells bez nutnosti jejich předponování.
Nyní, když jsme si vše nastavili, je čas přidat do našeho pracovního listu několik řádků. Projdeme si každý krok podrobně.
## Krok 1: Nastavení adresáře dokumentů
Než začnete pracovat se souborem aplikace Excel, musíte si určit, kam bude uložen. Postupujte takto:
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
```
Nahradit `"Your Document Directory"` s platnou cestou v systému, kam chcete uložit výstupní soubor.
## Krok 2: Vytvořte adresář
Je dobrým zvykem zajistit, aby adresář existoval. Pokud ne, můžete ho vytvořit pomocí následujícího kódu:
```csharp
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento úryvek kódu zkontroluje, zda zadaný adresář existuje, a pokud ne, vytvoří ho. Je to jako když si před túrou zkontrolujete batoh – chcete se ujistit, že máte vše potřebné!
## Krok 3: Vytvoření instance nového sešitu
Nyní si vytvořme nový sešit aplikace Excel. Toto je plátno, na kterém budete kreslit čáry.
```csharp
// Vytvořte instanci nového sešitu.
Workbook workbook = new Workbook();
```
Vytvoření nové instance `Workbook` vám poskytne nový, prázdný soubor aplikace Excel, se kterým můžete pracovat.
## Krok 4: Přístup k prvnímu pracovnímu listu
Každý sešit má alespoň jeden list a pro naše řádky použijeme ten první.
```csharp
// Vezměte si první pracovní list v knize.
Worksheet worksheet = workbook.Worksheets[0];
```
Zde vybíráme první pracovní list přístupem k němu prostřednictvím `Worksheets` sbírka `Workbook`.
## Krok 5: Přidejte první řádek
Začněme přidávat čáry. První čára bude stylově plná.
```csharp
// Přidejte do pracovního listu nový řádek.
Aspose.Cells.Drawing.LineShape line1 = worksheet.Shapes.AddLine(5, 0, 1, 0, 0, 250);
```
V tomto prohlášení:
- `AddLine` Metoda přidá čáru začínající na souřadnicích `(5, 0)` a končící v `(1, 0)` sahající do výšky `250`.
- Souřadnice `(5, 0)` představují počáteční pozici na pracovním listu, zatímco `(1, 0, 0, 250)` označuje koncovou vzdálenost.
## Krok 6: Nastavení vlastností čáry
Nyní si čáru trochu přizpůsobíme – nastavíme styl a umístění čárkování.
```csharp
// Nastavení stylu čáry čárkování
line1.Line.DashStyle = MsoLineDashStyle.Solid;
// Nastavte umístění.
line1.Placement = PlacementType.FreeFloating;
```
Zde říkáme řádku, aby zůstal na jednom místě bez ohledu na změny ve struktuře listu, a to pomocí `PlacementType.FreeFloating`.
## Krok 7: Přidání dalších řádků
Přidejme druhý řádek s jiným stylem, s použitím čárkovaného stylu.
```csharp
// Přidejte do pracovního listu další řádek.
Aspose.Cells.Drawing.LineShape line2 = worksheet.Shapes.AddLine(7, 0, 1, 0, 85, 250);
// Nastavte styl čárkované čáry.
line2.Line.DashStyle = MsoLineDashStyle.DashLongDash;
// Nastavte tloušťku čáry.
line2.Line.Weight = 4;
// Nastavte umístění.
line2.Placement = PlacementType.FreeFloating;
```
Všimněte si, jak jsme upravili umístění a změnili styl pomlčky na `DashLongDash`Vlastnost weight umožňuje ovládat tloušťku čáry.
## Krok 8: Přidejte třetí řádek
Ještě jedna čára! Dokončíme kresbu plnou čarou.
```csharp
// Doplňte třetí řádek do pracovního listu.
Aspose.Cells.Drawing.LineShape line3 = worksheet.Shapes.AddLine(13, 0, 1, 0, 0, 250);
```
Opět nastavíme jeho vlastnosti podobně, jako jsme nastavovali předchozí řádky.
## Krok 9: Skrýt mřížku
Aby naše kresba vypadala čistěji, skryjme mřížku listu.
```csharp
// prvním listu zrušte viditelnost mřížky.
workbook.Worksheets[0].IsGridlinesVisible = false;
```
Skrytí mřížky pomáhá uživatelům lépe se soustředit na čáry, které jste skutečně přidali, podobně jako malíř vyčistí oblast kolem plátna, aby se vyhnul rušivým elementům.
## Krok 10: Uložení sešitu
Nakonec si uložme pracovní sešit, aby naše tvrdá práce nepřišla nazmar!
```csharp
// Uložte soubor Excelu.
workbook.Save(dataDir + "book1.out.xls");
```
Výstupní soubor můžete pojmenovat libovolně – stačí se ujistit, že končí na `.xls` nebo jinou podporovanou příponu souboru Excelu.
## Závěr
Gratulujeme! Úspěšně jste se naučili, jak přidat ovládací prvky řádků do listu aplikace Excel pomocí knihovny Aspose.Cells pro .NET. S několika řádky kódu můžete výrazně vylepšit své soubory aplikace Excel a nabídnout vizuální reprezentaci dat, která vám pomůže efektivněji sdělovat poznatky. Ať už chcete vytvářet sestavy, prezentace nebo analytické nástroje, zvládnutí knihoven, jako je Aspose.Cells, vám může značně zjednodušit a zefektivnit pracovní postup.
## Často kladené otázky
### Co je Aspose.Cells pro .NET?
Aspose.Cells pro .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel bez nutnosti používat Microsoft Excel.
### Mohu přidat jiné tvary než čáry?
Ano, Aspose.Cells nabízí různé tvary, jako jsou obdélníky, elipsy a další. Můžete je snadno vytvořit pomocí podobných metod.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je placená knihovna, ale můžete začít s [bezplatná zkušební verze](https://releases.aspose.com/) prozkoumat jeho vlastnosti.
### Mohu si přizpůsobit barvy čar?
Rozhodně! Vlastnosti barev čar můžete nastavit pomocí parametrů čar. `LineColor` vlastnictví.
### Kde mohu požádat o technickou podporu?
Podporu můžete získat od [Fórum Aspose](https://forum.aspose.com/c/cells/9) kde členové komunity a týmu Aspose pomáhají uživatelům.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}