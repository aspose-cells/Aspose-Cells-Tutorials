---
"description": "Naučte se, jak převádět grafy na obrázky v .NET pomocí Aspose.Cells s tímto podrobným návodem. Snadno převeďte grafy z Excelu na vysoce kvalitní obrázky."
"linktitle": "Převod grafu na obrázek v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Převod grafu na obrázek v .NET"
"url": "/cs/net/image-and-chart-operations/chart-to-image-conversion/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Převod grafu na obrázek v .NET

## Zavedení
Převod grafu z Excelu do obrázku může být klíčovým požadavkem při vytváření systémů pro tvorbu sestav nebo sdílení vizuálních reprezentací dat. Naštěstí je s Aspose.Cells pro .NET tento proces hračka! Ať už generujete sestavy nebo jednoduše převádíte grafy z Excelu do obrázků pro lepší zobrazení, tato příručka vás tímto procesem krok za krokem provede.
## Předpoklady
Než začneme, ujistěte se, že máte vše připravené, abyste mohli pokračovat v tomto tutoriálu.
### Knihovna Aspose.Cells pro .NET
Nejprve si budete muset stáhnout a ve svém projektu odkazovat na knihovnu Aspose.Cells pro .NET. Nejnovější verzi si můžete stáhnout zde:
- [Stáhnout Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/)
### Prostředí .NET
Ujistěte se, že máte v systému nainstalovaný framework .NET. Ke spuštění tohoto příkladu můžete použít Visual Studio nebo jakékoli jiné vývojové prostředí pro .NET.
### Nastavení licence (volitelné)
Ačkoli můžete Aspose.Cells používat s bezplatnou zkušební verzí, pro plnou funkčnost bez omezení zvažte žádost o... [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo si jeden zakoupit od [zde](https://purchase.aspose.com/buy).

## Importovat balíčky
Pro začátek importujme potřebné jmenné prostory pro práci s knihovnou Aspose.Cells. To nám umožní manipulovat s excelovými soubory a generovat obrázky.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Před zahájením kódování se ujistěte, že máte tyto balíčky připravené.

Nyní si rozeberme proces převodu grafu na obrázek do jednoduchých kroků.
## Krok 1: Nastavení adresáře projektu
Potřebujete místo, kam uložit vygenerované obrázky, že? Nejprve si vytvořme adresář, kam se budou ukládat výstupní obrázky.

Začneme definováním cesty k adresáři s dokumenty a ověřením, zda složka existuje. Pokud ne, vytvoříme ji.
```csharp
// Definujte adresář pro ukládání obrázků
string dataDir = "Your Document Directory";
// Zkontrolujte, zda adresář existuje
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
V tomto kroku jste připraveni generovat a ukládat obrázky grafů do tohoto adresáře.
## Krok 2: Vytvořte nový sešit
Zde vytvoříme instanci objektu Workbook. Ten bude reprezentovat náš excelový soubor, do kterého bude vložen graf.

Sešit je jako soubor aplikace Excel, který obsahuje listy. Vytvořením nového sešitu začínáme znovu s prázdným souborem aplikace Excel.
```csharp
// Vytvoření nového objektu sešitu
Workbook workbook = new Workbook();
```
## Krok 3: Přidání nového pracovního listu
Každý soubor aplikace Excel má listy (nebo záložky). Přidejme jeden do našeho sešitu.

Přidání nového listu je nezbytné, protože do něj budeme vkládat data a grafy. Jakmile je list přidán, načteme jeho referenci.
```csharp
// Přidání nového listu do sešitu
int sheetIndex = workbook.Worksheets.Add();
// Načíst nově přidaný list
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Krok 4: Naplnění pracovního listu daty
Abychom vytvořili smysluplný graf, potřebujeme nějaká data, že? Vyplňme několik buněk vzorovými hodnotami.

Do konkrétních buněk na listu přidáme data. Tato data později použijeme k vygenerování našeho grafu.
```csharp
// Přidání vzorových dat do buněk
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Krok 5: Přidání grafu do pracovního listu
Nyní si vytvořme sloupcový graf, který vizualizuje data, která jsme právě přidali.

Určíme typ grafu (sloupcový graf) a definujeme jeho velikost a umístění v rámci listu.
```csharp
// Přidání sloupcového grafu do listu
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Krok 6: Definování zdroje dat grafu
A tady se děje ta pravá magie: propojení grafu s daty v listu!

Graf propojíme s daty ve sloupcích A1 až B3. To grafu sdělí, odkud má data čerpat.
```csharp
// Propojte graf s daty v rozsahu A1 až B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Krok 7: Převeďte graf na obrázek
Okamžik pravdy: tento graf převedeme do obrazového souboru!

Zde používáme `ToImage` metoda pro převod grafu do obrazového formátu dle vašeho výběru. V tomto případě jej převádíme do formátu EMF (Enhanced Metafile).
```csharp
// Převeďte graf na obrázek a uložte jej do adresáře
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
A to je vše! Váš graf byl nyní uložen jako obrázek. Je čas se pochválit.
## Krok 8: Zobrazení zprávy o úspěchu
Abychom to shrnuli, zobrazíme zprávu potvrzující generování obrazu.
```csharp
// Zobrazit zprávu oznamující úspěch
System.Console.WriteLine("Image generated successfully.");
```
## Závěr
Bum! Tak snadné je převést graf z Excelu do obrázku pomocí Aspose.Cells pro .NET. Tento proces nejen zjednodušuje prezentaci dat, ale také zvyšuje flexibilitu sestav nebo dashboardů, kde se upřednostňují obrázky před vloženými grafy.
Dodržováním kroků popsaných v této příručce nyní můžete převést libovolný graf aplikace Excel na obrázek, což vám umožní bezproblémově integrovat vizuální data do různých aplikací.
## Často kladené otázky
### Mohu touto metodou převádět různé typy grafů?
Ano, můžete převést jakýkoli typ grafu podporovaný službou Aspose.Cells, včetně koláčových grafů, sloupcových grafů, spojnicových grafů a dalších!
### Je možné změnit formát obrázku?
Rozhodně! V tomto příkladu jsme sice použili EMF, ale formát obrázku můžete změnit na PNG, JPEG, BMP a další pouhou úpravou `ImageFormat` parametr.
### Podporuje Aspose.Cells obrázky s vysokým rozlišením?
Ano, Aspose.Cells umožňuje ovládat rozlišení a kvalitu obrazu při exportu grafů do obrázků.
### Mohu převést více grafů na obrázky najednou?
Ano, v sešitu můžete procházet více grafů a všechny je převést na obrázky pomocí několika řádků kódu.
### Existuje omezení počtu grafů, které mohu převést?
Aspose.Cells nemá žádná inherentní omezení, ale zpracování velkého množství dat může záviset na paměti a výkonu vašeho systému.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}