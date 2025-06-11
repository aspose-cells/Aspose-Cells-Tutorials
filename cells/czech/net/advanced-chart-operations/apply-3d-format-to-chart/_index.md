---
"description": "Zjistěte, jak vytvářet úžasné 3D grafy v Excelu pomocí Aspose.Cells pro .NET. Postupujte podle našeho jednoduchého podrobného návodu."
"linktitle": "Použití 3D formátu na graf"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Použití 3D formátu na graf"
"url": "/cs/net/advanced-chart-operations/apply-3d-format-to-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Použití 3D formátu na graf

## Zavedení

době, kdy je vizualizace dat prvořadá, způsob, jakým prezentujeme naše data, jde nad rámec základních grafů a tabulek. S nástroji, jako je Aspose.Cells pro .NET, můžete vylepšit své datové prezentace ohromujícími 3D grafy, které nejen upoutají pozornost, ale také efektivně sdělí informace. Tato příručka vás provede kroky, jak pomocí Aspose.Cells použít 3D formát na graf a transformovat vaše nezpracovaná data do poutavého zobrazení.

## Předpoklady

Než se ponoříme do detailů použití 3D formátu na graf, ujistěte se, že máte vše, co potřebujete.

### Softwarové požadavky

- Visual Studio: Ujistěte se, že máte nainstalované Visual Studio pro práci s aplikacemi .NET.
- Aspose.Cells pro .NET: Pokud jste tak ještě neučinili, stáhněte si a nainstalujte Aspose.Cells z [zde](https://releases.aspose.com/cells/net/).

### Nastavení kódovacího prostředí

1. Vytvoření nového projektu .NET: Otevřete Visual Studio, vyberte „Vytvořit nový projekt“ a vyberte konzolovou aplikaci.
2. Referenční odkaz na Aspose.Cells: Prostřednictvím Správce balíčků NuGet přidejte Aspose.Cells vyhledáním nebo pomocí konzole Správce balíčků:

```bash
Install-Package Aspose.Cells
```

3. Nastavení výstupního adresáře: Určete výstupní adresář, kam budou uloženy vygenerované soubory – může to být stejně jednoduché jako vytvoření složky na ploše.

Nyní, když máte vše nastavené, je čas pustit se do kódu a vytvořit úžasné 3D grafy!

## Importovat balíčky

Pro začátek je potřeba importovat potřebné jmenné prostory. To vám pomůže získat přístup ke třídám a metodám poskytovaným Aspose.Cells. Zde je návod, jak to udělat:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Tato část rozdělí proces na zvládnutelné kroky a poskytne vám jasnou představu o každé fázi.

## Krok 1: Inicializace sešitu

Nejprve je třeba vytvořit instanci `Workbook` třída. Tento objekt bude sloužit jako základ pro váš dokument aplikace Excel.

```csharp
//Výstupní adresář
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
Zamysli se nad tím `Workbook` jako prázdné plátno – připravené k tomu, abyste ho naplnili barevnými daty a působivými vizualizacemi.

## Krok 2: Přejmenujte první pracovní list

Dále přejmenujeme první pracovní list. To nám poskytne jasno v tom, s jakými daty pracujeme.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Názvy by měly být intuitivní. V tomto případě to pojmenujeme „Datový list“, abychom věděli, kde se naše data nacházejí.

## Krok 3: Vytvoření dat pro graf

Nyní přidáme nějaká data do našeho „Datového listu“. Naplňme ho hodnotami, které bude náš graf používat.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Stejně jako recept závisí na ingrediencích, i efektivita vašeho grafu závisí na kvalitě a uspořádání vstupních dat.

## Krok 4: Nastavení nového pracovního listu s grafem

Je čas vytvořit nový pracovní list pro samotný graf. To vám pomůže udržet si přehlednost ve vizualizaci dat.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Považujte tento pracovní list za svou fázi – kde se odvíjí výkonnost vašich dat.

## Krok 5: Přidání grafu

Zde přidáme sloupcový graf do nově vytvořeného listu.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Definujeme prostor pro náš graf a určujeme jeho typ. Představte si to jako výběr typu rámečku pro vaši kresbu.

## Krok 6: Úprava vzhledu grafu

Nyní si přizpůsobme vzhled našeho grafu nastavením barev pozadí. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Čisté bílé pozadí často zvýrazní barvy vašich dat a zlepší jejich viditelnost.

## Krok 7: Přidání datové řady do grafu

Je čas naplnit náš graf daty. Přidáme datovou řadu z našeho „DataSheet“, abychom zajistili, že náš graf odráží potřebná data.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Je to analogické s tím, jak šéfkuchař připravuje jídlo s konkrétními ingrediencemi. Každý datový bod je důležitý!

## Krok 8: Přístup k datové řadě a její formátování

Nyní, když máme propojená data, pojďme si vzít datové řady a začít aplikovat některé 3D efekty.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Chystáme se dodat našemu pokrmu trochu šmrncu – berte to jako koření, které vylepší celkovou chuť.

## Krok 9: Použití 3D efektů zkosení

Dále přidáme efekt zkosení, abychom našemu grafu dodali rozměr.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Stejně jako sochař tvaruje kámen, i my vytváříme hloubku, která oživuje náš graf!

## Krok 10: Přizpůsobení materiálu povrchu a osvětlení

Rozzáříme náš graf! Upravíme materiál povrchu a nastavení osvětlení.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Správné osvětlení a materiál dokáží proměnit plochý objekt v poutavý vizuální prvek. Představte si filmovou kulisu s odborným osvětlením, které každou scénu vylepší.

## Krok 11: Dokončovací úpravy vzhledu série

Nyní dokončíme vzhled naší datové řady úpravou její barvy.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Správná barva může vyvolat určité pocity a reakce – kaštanová dodává nádech elegance a sofistikovanosti.

## Krok 12: Uložte si sešit

Konečně je čas uložit si své mistrovské dílo! Nezapomeňte zadat cílové umístění, kam ho chcete uložit.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Uložení vaší práce je jako umístění vašeho umění do galerie; je to okamžik, který si můžete vážit a sdílet.

## Závěr

Gratulujeme! Úspěšně jste vytvořili vizuálně atraktivní 3D graf pomocí Aspose.Cells pro .NET. Dodržením těchto kroků nyní máte k dispozici výkonný nástroj pro vylepšení prezentací dat, díky kterému budou nejen informativní, ale i vizuálně poutavé. Při zdokonalování grafů nezapomeňte, že každá vizualizace je příběh – udělejte ji poutavou, jasnou a působivou!

## Často kladené otázky

### Co je Aspose.Cells pro .NET?
Aspose.Cells pro .NET je výkonná knihovna, která umožňuje vývojářům programově manipulovat s dokumenty aplikace Excel, včetně vytváření grafů a diagramů.

### Mohu si v Aspose.Cells přizpůsobit typy grafů?
Ano! Aspose.Cells podporuje různé typy grafů, jako jsou sloupcové, čárové, koláčové a mnoho dalších, které lze snadno přizpůsobit.

### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
Rozhodně! Zkušební verzi si můžete stáhnout zdarma z [zde](https://releases.aspose.com/).

### Mohu na grafy použít i jiné efekty než 3D formáty?
Ano, můžete použít různé efekty, jako jsou stíny, přechody a různé styly, abyste vylepšili své grafy i mimo 3D.

### Kde najdu podporu pro Aspose.Cells?
Pro podporu můžete navštívit [Fórum Aspose](https://forum.aspose.com/c/cells/9) za pomoc a podporu komunity.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}