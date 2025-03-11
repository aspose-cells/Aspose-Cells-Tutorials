---
title: Přidat řádek řízení do listu v aplikaci Excel
linktitle: Přidat řádek řízení do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se přidávat a přizpůsobovat ovládací prvky čar v listech aplikace Excel pomocí Aspose.Cells for .NET v tomto komplexním kurzu.
weight: 26
url: /cs/net/excel-shapes-controls/add-line-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat řádek řízení do listu v aplikaci Excel

## Zavedení
Excelové tabulky nejsou jen o řádcích a sloupcích dat; jsou také plátnem pro vizualizaci. Přidání ovládacích prvků řádků může zlepšit způsob, jakým jsou informace reprezentovány ve vašich listech, čímž jsou vztahy a trendy mnohem jasnější. Vstupte do Aspose.Cells for .NET, výkonné knihovny, která zjednodušuje proces vytváření a manipulaci se soubory aplikace Excel programově. V této příručce vás provedeme kroky k přidání ovládacích prvků čar do listu pomocí Aspose.Cells. Pokud jste připraveni vylepšit svou hru Excel, pojďme se ponořit!
## Předpoklady
Než začnete přidávat řádky do svých excelových listů, budete potřebovat několik věcí:
1.  Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Pokud ne, můžete si jej stáhnout z[webové stránky](https://visualstudio.microsoft.com/).
2.  Aspose.Cells for .NET: Tato knihovna musí být uvedena ve vašem projektu. Můžete najít podrobnou dokumentaci[zde](https://reference.aspose.com/cells/net/) a stáhněte si knihovnu[zde](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže pochopit kód, na který se budeme dívat.
4. Prostředí Windows: Vzhledem k tomu, že Aspose.Cells je navržen pro aplikace .NET, je preferováno prostředí Windows.
## Importujte balíčky
Pojďme si nastavit naše kódovací prostředí, než začneme přidávat nějaké řádky do vašeho excelového listu. Zde je návod, jak importovat požadovaný balíček Aspose.Cells do vašeho projektu.
### Vytvořit nový projekt
- Otevřete Visual Studio.
- Vytvořte nový projekt aplikace konzoly. Můžete jej pojmenovat, jak chcete – pro přehlednost možná „ExcelLineDemo“.
### Nainstalujte Aspose.Cells
- Přejděte do Správce balíčků NuGet v sadě Visual Studio (`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`).
-  Hledat`Aspose.Cells` a nainstalujte jej. Tato akce přidá do vašeho projektu potřebné knihovny.
### Importujte jmenný prostor
V horní části hlavního souboru programu přidejte následující direktivu using, abyste zpřístupnili Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Tímto způsobem můžete nyní používat všechny funkce z knihovny Aspose.Cells, aniž byste jim přidávali předponu.
Nyní, když jsme nastavili, je čas přidat několik řádků do našeho listu. Projdeme si každý krok podrobně.
## Krok 1: Nastavte adresář dokumentů
Než začnete pracovat se souborem Excel, musíte definovat, kam se uloží. Postup je následující:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
```
 Nahradit`"Your Document Directory"` s platnou cestou ve vašem systému, kam chcete uložit výstupní soubor.
## Krok 2: Vytvořte adresář
Je dobrým zvykem zajistit, aby adresář existoval. Pokud tomu tak není, můžete jej vytvořit pomocí následujícího kódu:
```csharp
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tento fragment kódu zkontroluje, zda zadaný adresář existuje, a pokud ne, vytvoří jej. Je to jako zkontrolovat si batoh, než se vydáte na túru – chcete se ujistit, že máte vše, co potřebujete!
## Krok 3: Vytvořte nový sešit
Nyní vytvoříme nový excelový sešit. Toto je plátno, na které budete kreslit své čáry.
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```
 Vytvoření nové instance`Workbook` vám poskytne nový prázdný soubor Excel, se kterým můžete pracovat.
## Krok 4: Otevřete první pracovní list
Každý sešit má alespoň jeden list a ten první použijeme pro naše řádky.
```csharp
// Získejte první pracovní list v knize.
Worksheet worksheet = workbook.Worksheets[0];
```
Zde vybíráme první pracovní list přístupem přes`Worksheets` sbírka`Workbook`.
## Krok 5: Přidejte první řádek
Začněme přidávat nějaké řádky. První řádek bude stylově pevný.
```csharp
// Přidejte do listu nový řádek.
Aspose.Cells.Drawing.LineShape line1 = worksheet.Shapes.AddLine(5, 0, 1, 0, 0, 250);
```
V tomto prohlášení:
- `AddLine` metoda přidá řádek začínající na souřadnicích`(5, 0)` a končící v`(1, 0)` sahající do výšky`250`.
-  Souřadnice`(5, 0)` představují výchozí pozici na listu, zatímco`(1, 0, 0, 250)` označuje koncovou vzdálenost.
## Krok 6: Nastavte vlastnosti čáry
Nyní si linii trochu přizpůsobíme – nastavte její styl čárky a umístění.
```csharp
// Nastavte styl čárky
line1.Line.DashStyle = MsoLineDashStyle.Solid;
// Nastavte umístění.
line1.Placement = PlacementType.FreeFloating;
```
 Zde říkáme, aby řádek zůstal na jednom místě bez ohledu na změny ve struktuře listu pomocí použití`PlacementType.FreeFloating`.
## Krok 7: Přidejte další řádky
Pojďme přidat druhý řádek s jiným stylem, pomocí čárkovaného stylu.
```csharp
// Přidejte do listu další řádek.
Aspose.Cells.Drawing.LineShape line2 = worksheet.Shapes.AddLine(7, 0, 1, 0, 85, 250);
// Nastavte styl čárky.
line2.Line.DashStyle = MsoLineDashStyle.DashLongDash;
// Nastavte váhu vlasce.
line2.Line.Weight = 4;
// Nastavte umístění.
line2.Placement = PlacementType.FreeFloating;
```
 Všimněte si, jak jsme upravili umístění a změnili styl čárky na`DashLongDash`Vlastnost weight umožňuje ovládat tloušťku čáry.
## Krok 8: Přidejte třetí řádek
Ještě jeden řádek! K dokončení naší kresby přidáme plnou čáru.
```csharp
// Přidejte třetí řádek do listu.
Aspose.Cells.Drawing.LineShape line3 = worksheet.Shapes.AddLine(13, 0, 1, 0, 0, 250);
```
Jeho vlastnosti opět nakonfigurujeme podobně, jako jsme nastavili předchozí řádky.
## Krok 9: Skryjte mřížku
Aby naše kresba vypadala čistěji, skryjme mřížku listu.
```csharp
// Udělejte mřížku neviditelnou v prvním listu.
workbook.Worksheets[0].IsGridlinesVisible = false;
```
Skrytí čar mřížky pomůže uživatelům více se soustředit na skutečné čáry, které jste přidali, podobně jako když malíř vyčistí oblast kolem svého plátna, aby se vyhnul rozptylování.
## Krok 10: Uložte sešit
Nakonec si uložme sešit, aby naše dřina nepřišla nazmar!
```csharp
// Uložte soubor aplikace Excel.
workbook.Save(dataDir + "book1.out.xls");
```
 Výstupní soubor můžete pojmenovat, jak chcete – jen se ujistěte, že končí`.xls` nebo jinou podporovanou příponu souboru Excel.
## Závěr
Gratuluji! Úspěšně jste se naučili, jak přidat ovládací prvky řádku do listu aplikace Excel pomocí Aspose.Cells pro .NET. Pomocí několika řádků kódu můžete výrazně vylepšit své soubory Excel a nabídnout vizuální reprezentaci dat, která může pomoci efektivněji komunikovat statistiky. Ať už chcete vytvářet sestavy, prezentace nebo analytické nástroje, zvládnutí knihoven, jako je Aspose.Cells, může váš pracovní postup mnohem hladší a efektivnější.
## FAQ
### Co je Aspose.Cells pro .NET?
Aspose.Cells for .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět soubory aplikace Excel, aniž by museli používat aplikaci Microsoft Excel.
### Mohu přidat jiné tvary než čáry?
Ano, Aspose.Cells nabízí různé tvary, jako jsou obdélníky, elipsy a další. Můžete je snadno vytvořit pomocí podobných metod.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells je placená knihovna, ale můžete začít s a[zkušební verze zdarma](https://releases.aspose.com/) prozkoumat jeho vlastnosti.
### Mohu přizpůsobit barvy čar?
 Absolutně! Barevné vlastnosti čar můžete nastavit pomocí čar`LineColor` vlastnictví.
### Kde mohu požádat o technickou podporu?
 Můžete získat podporu od[Aspose fórum](https://forum.aspose.com/c/cells/9) kde uživatelům pomáhají členové komunity a členové týmu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
