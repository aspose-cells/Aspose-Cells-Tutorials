---
title: Převod grafu na obrázek v .NET
linktitle: Převod grafu na obrázek v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak převést grafy na obrázky v .NET pomocí Aspose.Cells, pomocí tohoto podrobného průvodce. Snadno převádějte grafy Excel na vysoce kvalitní obrázky.
weight: 10
url: /cs/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod grafu na obrázek v .NET

## Zavedení
Převod grafu z Excelu na obrázek může být zásadním požadavkem při vytváření systémů sestav nebo sdílení vizuálních reprezentací dat. Naštěstí s Aspose.Cells pro .NET je tento proces snadný jako facka! Ať už generujete sestavy nebo jednoduše převádíte grafy Excel na obrázky pro lepší zobrazení, tento průvodce vás provede procesem krok za krokem.
## Předpoklady
Než začneme, ujistěte se, že máte vše na svém místě, abyste mohli postupovat podle tohoto návodu.
### Aspose.Cells pro knihovnu .NET
Nejprve si budete muset stáhnout a odkazovat na knihovnu Aspose.Cells for .NET ve vašem projektu. Nejnovější verzi si můžete stáhnout zde:
- [Stáhněte si Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/)
### .NET prostředí
Ujistěte se, že máte na svém systému nainstalovaný .NET framework. Ke spuštění tohoto příkladu můžete použít Visual Studio nebo jakékoli jiné vývojové prostředí .NET.
### Nastavení licence (volitelné)
 Ačkoli můžete Aspose.Cells používat s bezplatnou zkušební verzí, pro úplnou funkčnost bez omezení zvažte žádost o[dočasná licence](https://purchase.aspose.com/temporary-license/) nebo si jeden kupte od[zde](https://purchase.aspose.com/buy).

## Importujte balíčky
Abychom to nastartovali, importujme potřebné jmenné prostory pro práci s knihovnou Aspose.Cells. To nám umožní manipulovat s excelovými soubory a generovat obrázky.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Před zahájením kódovací části se ujistěte, že máte tyto balíčky připraveny.

Nyní si rozeberme proces převodu grafu na obrázek do jednoduchých kroků.
## Krok 1: Nastavte adresář projektu
Potřebujete místo pro ukládání vygenerovaných obrázků, že? Nejprve si vytvoříme adresář, kam se budou ukládat výstupní obrázky.

Začneme tím, že definujeme cestu pro náš adresář dokumentů a zajistíme, že složka existuje. Pokud ne, vytvoříme jeden.
```csharp
// Definujte adresář pro ukládání obrázků
string dataDir = "Your Document Directory";
//Zkontrolujte, zda adresář existuje
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Tímto krokem jste připraveni vygenerovat a uložit obrázky grafu do tohoto adresáře.
## Krok 2: Vytvořte nový sešit
Zde vytvoříme instanci objektu Workbook. To bude představovat náš soubor Excel, do kterého bude graf vložen.

Sešit je jako soubor aplikace Excel, který obsahuje listy. Vytvořením nového sešitu začínáme znovu s prázdným souborem Excel.
```csharp
// Vytvořte nový objekt sešitu
Workbook workbook = new Workbook();
```
## Krok 3: Přidejte nový list
Každý soubor aplikace Excel má listy (nebo karty). Pojďme přidat jeden do našeho sešitu.

Přidání nového listu je nezbytné, protože do tohoto listu vložíme naše data a grafy. Jakmile je list přidán, získáme jeho referenci.
```csharp
// Přidejte do sešitu nový list
int sheetIndex = workbook.Worksheets.Add();
// Načtěte nově přidaný list
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Krok 4: Vyplňte list daty
Abychom vytvořili smysluplný graf, potřebujeme nějaká data, že? Vyplňte několik buněk vzorovými hodnotami.

Doplníme data do konkrétních buněk na listu. Tato data budou později použita k vytvoření našeho grafu.
```csharp
// Přidejte ukázková data do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Krok 5: Přidejte graf do listu
Nyní vytvoříme sloupcový graf, který vizualizuje data, která jsme právě přidali.

Určíme typ grafu (sloupcový graf) a definujeme jeho velikost a polohu v rámci listu.
```csharp
// Přidejte do listu sloupcový graf
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Krok 6: Definujte zdroj dat grafu
Zde je kouzlo: propojení grafu s daty v listu!

Graf propojíme s údaji ve sloupcích A1 až B3. To říká grafu, odkud data čerpat.
```csharp
// Propojte graf s daty v rozsahu A1 až B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Krok 7: Převeďte graf na obrázek
Okamžik pravdy: převedeme tento graf na obrázkový soubor!

 Zde používáme`ToImage` způsob převodu grafu do formátu obrázku podle vašeho výběru. V tomto případě jej převádíme do formátu EMF (Enhanced Metafile).
```csharp
// Převeďte graf na obrázek a uložte jej do adresáře
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
A je to! Váš graf byl nyní uložen jako obrázek. Čas se poplácat po zádech.
## Krok 8: Zobrazte zprávu o úspěchu
Abychom to uzavřeli, zobrazme zprávu potvrzující vygenerování obrázku.
```csharp
// Zobrazte zprávu označující úspěch
System.Console.WriteLine("Image generated successfully.");
```
## Závěr
Výložník! Jak snadné je převést graf z Excelu na obrázek pomocí Aspose.Cells for .NET. Tento proces nejen zjednodušuje prezentaci dat, ale také zvyšuje flexibilitu sestav nebo řídicích panelů, kde jsou obrázky preferovány před vloženými grafy.
Podle kroků uvedených v této příručce můžete nyní převést jakýkoli graf aplikace Excel na obrázek, což vám umožní bezproblémově integrovat vizuální data do různých aplikací.
## FAQ
### Mohu pomocí této metody převést různé typy grafů?
Ano, můžete převést jakýkoli typ grafu podporovaný Aspose.Cells včetně koláčových grafů, sloupcových grafů, spojnicových grafů a dalších!
### Je možné změnit formát obrázku?
 Absolutně! I když jsme v tomto příkladu použili EMF, můžete změnit formát obrázku na PNG, JPEG, BMP a další jednoduše úpravou`ImageFormat` parametr.
### Podporuje Aspose.Cells obrázky ve vysokém rozlišení?
Ano, Aspose.Cells umožňuje ovládat rozlišení a nastavení kvality obrázku při exportu grafů do obrázků.
### Mohu převést více grafů na obrázky najednou?
Ano, můžete procházet více grafy v sešitu a všechny je převést na obrázky pomocí několika řádků kódu.
### Existuje nějaký limit na počet grafů, které mohu převést?
Aspose.Cells neukládá žádné vlastní omezení, ale zpracování velkého množství dat může záviset na paměti a výkonových možnostech vašeho systému.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
