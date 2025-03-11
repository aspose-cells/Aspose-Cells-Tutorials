---
title: Přidejte Arrow Head do Shape v Excelu
linktitle: Přidejte Arrow Head do Shape v Excelu
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se přidávat šipky do obrazců v Excelu pomocí Aspose.Cells for .NET. Vylepšete své tabulky pomocí tohoto podrobného průvodce.
weight: 10
url: /cs/net/excel-shapes-controls/add-arrow-head-to-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte Arrow Head do Shape v Excelu

## Zavedení
Vytváření vizuálně poutavých excelových tabulek je zásadní, zejména při prezentaci dat jasným a informativním způsobem. Jedním ze způsobů, jak vylepšit takové prezentace, je přidání tvarů, jako jsou čáry se šipkami. Tato příručka vás provede přidáním šipek do tvarů v sešitu aplikace Excel pomocí Aspose.Cells for .NET. Ať už jste vývojář, který chce automatizovat sestavy, nebo prostě někdo, kdo má zájem vylepšit své excelové tabulky, tento článek vám poskytne potřebné informace.
## Předpoklady
Než se pustíte do výukového programu, ujistěte se, že máte vše připraveno. Zde je to, co potřebujete:
1. Základní znalost C# a .NET: Pochopení základů programování v C# vám pomůže procházet příklady kódu plynuleji.
2.  Aspose.Cells for .NET Library: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells. Můžete to získat z[stránka ke stažení](https://releases.aspose.com/cells/net/).
3. Vývojové prostředí: IDE jako Visual Studio pro spouštění a testování aplikací .NET.
4.  Bezplatná zkušební verze nebo licence: Pokud jste tak ještě neučinili, zvažte stažení a[zkušební verze zdarma](https://releases.aspose.com/) nebo získání a[dočasná licence](https://purchase.aspose.com/temporary-license/) pro Aspose.Cells.
5. Znalost Excelu: Znalost navigace v Excelu vám pomůže pochopit, jak tvary a čáry interagují s vašimi daty.
## Importujte balíčky
Chcete-li používat Aspose.Cells, budete muset do svého projektu C# importovat potřebné jmenné prostory. Můžete to provést přidáním následujícího řádku do horní části souboru kódu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Tyto obory názvů poskytují přístup k základním třídám a metodám potřebným pro manipulaci se soubory aplikace Excel a vytváření tvarů. 

Nyní si tento proces rozdělíme do jednoduchých, zvládnutelných kroků. 
## Krok 1: Nastavte své projektové prostředí
Nejprve otevřete své IDE (jako Visual Studio) a vytvořte nový projekt C#. Můžete si vybrat konzolovou aplikaci, protože nám to umožní spouštět kód přímo z terminálu.

Dále se ujistěte, že je ve vašem projektu odkazováno na Aspose.Cells. Pokud používáte NuGet, můžete jej snadno přidat prostřednictvím konzoly Správce balíčků pomocí následujícího příkazu:
```bash
Install-Package Aspose.Cells
```
## Krok 2: Definujte adresář dokumentů
Nyní je čas definovat, kde budou vaše dokumenty uloženy. Budete chtít vytvořit adresář, do kterého bude sešit uložen. Zde je návod, jak to udělat v kódu:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě není přítomen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
```
 Nezapomeňte změnit`"Your Document Directory"` na vhodnou cestu ve vašem systému, kde máte oprávnění k zápisu.
## Krok 3: Vytvořte sešit a pracovní list
### Vytvoření nového sešitu
Dále budete muset vytvořit sešit a přidat do něj list. Je to tak jednoduché:
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
```
### Přístup k prvnímu listu
Nyní si vezmeme první pracovní list, kam přidáme naše tvary.
```csharp
// Získejte první pracovní list v knize.
Worksheet worksheet = workbook.Worksheets[0];
```
## Krok 4: Přidejte tvar čáry
Nyní do našeho listu přidáme řádek:
```csharp
// Přidejte řádek do listu
Aspose.Cells.Drawing.LineShape line2 = worksheet.Shapes.AddLine(7, 0, 1, 0, 85, 250);
```
tomto příkladu vytváříme tvar čáry začínající na souřadnicích (7, 0) a končící na (85, 250). Tato čísla můžete upravit a přizpůsobit tak velikost a pozici čáry podle potřeby.
## Krok 5: Přizpůsobte čáru
Linku můžete učinit vizuálně přitažlivější změnou její barvy a hmotnosti. Zde je postup:
```csharp
// Nastavte barvu čáry
line2.Line.FillType = FillType.Solid;
line2.Line.SolidFill.Color = Color.Blue;
// Nastavte váhu vlasce.
line2.Line.Weight = 3;
```
V tomto případě jsme nastavili vlasec na plnou modrou výplň a váhu 3. Experimentujte s různými barvami a hmotnostmi, abyste zjistili, co vám vyhovuje!
## Krok 6: Upravte umístění čar
Dále je potřeba nastavit, jak se čára umístí do listu. Pro tento příklad to uděláme volně plovoucí:
```csharp
// Nastavte umístění.
line2.Placement = PlacementType.FreeFloating;
```
## Krok 7: Přidejte šipky
Zde je vzrušující část! Přidejme šipky na oba konce našeho řádku:
```csharp
// Nastavte šipky čar.
line2.Line.EndArrowheadWidth = MsoArrowheadWidth.Medium;
line2.Line.EndArrowheadStyle = MsoArrowheadStyle.Arrow;
line2.Line.EndArrowheadLength = MsoArrowheadLength.Medium;
line2.Line.BeginArrowheadStyle = MsoArrowheadStyle.ArrowDiamond;
line2.Line.BeginArrowheadLength = MsoArrowheadLength.Medium;
```
Tento kód nastavuje konec řádku tak, aby měl šipku střední šířky, zatímco začátek bude mít šipku ve stylu kosočtverce. Tyto vlastnosti můžete upravit na základě vašich preferencí návrhu.
## Krok 8: Udělejte mřížku neviditelnou
Někdy mohou mřížky bránit vizuální přitažlivosti grafu nebo tvaru. Chcete-li je vypnout, použijte následující řádek:
```csharp
// Udělejte mřížku neviditelnou v prvním listu.
workbook.Worksheets[0].IsGridlinesVisible = false;
```
## Krok 9: Uložte soubor Excel
Konečně je čas uložit svou práci:
```csharp
// Uložte soubor aplikace Excel.
workbook.Save(dataDir + "book1.out.xlsx");
```
 Ujistěte se, že název souboru končí příslušnou příponou souboru Excel, např`.xlsx` v tomto případě. 

## Závěr
Přidání šipek do tvarů v Excelu pomocí Aspose.Cells for .NET může výrazně zlepšit vizuální přitažlivost vašich tabulek. Pomocí několika řádků kódu můžete vytvářet profesionálně vypadající diagramy, které jasně sdělují informace. Ať už automatizujete sestavy nebo jednoduše vytváříte vizuální pomůcky, zvládnutí těchto technik nepochybně umožní vašim prezentacím vyniknout.
## FAQ
### Mohu změnit barvu hrotů šipek?
Ano, můžete upravit barvu čar a tvarů, včetně šipek, úpravou`SolidFill.Color` vlastnictví.
### Je Aspose.Cells zdarma k použití?
 Aspose.Cells je placený produkt, ale nabízí a[zkušební verze zdarma](https://releases.aspose.com/) které můžete použít k testování jeho funkcí.
### Musím nainstalovat nějaké další knihovny?
Ne, Aspose.Cells je samostatná knihovna. Ujistěte se, že na něj ve svém projektu odkazujete správně.
### Mohu vytvořit jiné tvary kromě čar?
Absolutně! Aspose.Cells podporuje různé tvary, včetně obdélníků, elips a dalších.
### Kde najdu další dokumentaci?
 Můžete najít komplexní dokumentaci o používání Aspose.Cells pro .NET[zde](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
