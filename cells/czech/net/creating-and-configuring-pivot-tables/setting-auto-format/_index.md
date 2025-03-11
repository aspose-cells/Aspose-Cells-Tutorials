---
title: Nastavení automatického formátu kontingenční tabulky programově v .NET
linktitle: Nastavení automatického formátu kontingenční tabulky programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: V tomto podrobném podrobném kurzu se dozvíte, jak programově nastavit automatický formát pro kontingenční tabulky Excel pomocí Aspose.Cells for .NET.
weight: 18
url: /cs/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení automatického formátu kontingenční tabulky programově v .NET

## Zavedení
Pokud jde o analýzu dat, kontingenční tabulky v Excelu mohou změnit hru. Umožňují vám dynamicky shrnout a analyzovat data, což vám pomůže získat poznatky, které by bylo téměř nemožné extrahovat ručně. Ale co když chcete automatizovat proces formátování vašich kontingenčních tabulek v .NET? Zde vám ukážu, jak programově nastavit automatický formát kontingenční tabulky pomocí výkonné knihovny Aspose.Cells pro .NET.
této příručce prozkoumáme to podstatné, projdeme si předpoklady, naimportujeme potřebné balíčky a pak se ponoříme do podrobného tutoriálu, který vám pomůže formátovat kontingenční tabulky jako profesionál. Zní to dobře? Pojďme rovnou do toho!
## Předpoklady
Než začneme, ujistěte se, že máte vše, co potřebujete, abyste mohli začít:
1. Vývojové prostředí .NET: Ujistěte se, že máte funkční instanci sady Visual Studio (nebo jakékoli .NET podporující IDE).
2.  Knihovna Aspose.Cells: Chcete-li hladce pracovat se soubory aplikace Excel, budete potřebovat nainstalovanou knihovnu Aspose.Cells. Pokud jste to ještě neudělali, můžete si to vzít z[stránka ke stažení](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět jednotlivým krokům.
4.  Soubor Excel (šablona): Pro začátek budete potřebovat soubor šablony Excel, který bude zpracován v našem příkladu. Pro jednoduchost můžete vytvořit ukázkový soubor s názvem`Book1.xls`.
## Importujte balíčky
Abyste mohli začít používat Aspose.Cells ve svém projektu, budete muset importovat potřebné balíčky. Zde je návod, jak to můžete nastavit ve svém projektu .NET:
### Vytvořit nový projekt
Začněte vytvořením nového projektu .NET ve vámi preferovaném IDE. 
### Přidat reference
Nezapomeňte přidat odkaz na knihovnu Aspose.Cells. Pokud jste si knihovnu stáhli, přidejte knihovny DLL z extrakce. Pokud používáte NuGet, můžete jednoduše spustit:
```bash
Install-Package Aspose.Cells
```
### Importovat jmenné prostory
Nyní ve vašem souboru kódu budete muset importovat jmenný prostor Aspose.Cells. Můžete to udělat přidáním následujícího řádku do horní části souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Po dokončení těchto kroků jste připraveni napsat nějaký kód!
Nyní si rozeberme kód, který jste poskytli, do podrobných kroků s vysvětlením toho, co jednotlivé části dělají. 
## Krok 1: Definujte svůj adresář dokumentů
Chcete-li začít, musíte nastavit cestu k adresáři dokumentů, kde jsou umístěny soubory aplikace Excel. V našem příkladu to definujeme takto:
```csharp
string dataDir = "Your Document Directory";  // Upravte podle potřeby
```
 Tento řádek vytváří řetězcovou proměnnou`dataDir`který obsahuje cestu k souboru k vašim dokumentům. Nezapomeňte vyměnit`"Your Document Directory"` se skutečnou cestou ve vašem systému.
## Krok 2: Načtěte soubor šablony
Dále budete chtít načíst existující sešit, který obsahuje vaši kontingenční tabulku:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Tento řádek inicializuje nový`Workbook` objekt načtením zadaného souboru Excel. Aby byly následující kroky účinné, měl by soubor obsahovat alespoň jednu kontingenční tabulku.
## Krok 3: Otevřete požadovaný pracovní list
Určete, na kterém listu musíte pracovat, abyste získali přístup ke kontingenční tabulce. V tomto případě získáme pouze první:
```csharp
int pivotIndex = 0;  // Index kontingenční tabulky
Worksheet worksheet = workbook.Worksheets[0];
```
 Zde,`worksheet` načte první list ze sešitu. Index kontingenční tabulky je nastaven na`0`, což znamená, že přistupujeme k první kontingenční tabulce v tomto listu.
## Krok 4: Vyhledejte kontingenční tabulku
S připraveným listem je čas přistupovat k vaší kontingenční tabulce:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Tím se inicializuje nový`PivotTable` objekt získáním kontingenční tabulky na zadaném indexu z listu.
## Krok 5: Nastavte vlastnost automatického formátu
Nyní k šťavnaté části: nastavení možností automatického formátování pro vaši kontingenční tabulku.
```csharp
pivotTable.IsAutoFormat = true; // Povolit automatické formátování
```
 Tento řádek umožňuje funkci automatického formátování kontingenční tabulky. Při nastavení na`true`, kontingenční tabulka se automaticky naformátuje na základě předdefinovaných stylů.
## Krok 6: Vyberte konkrétní typ automatického formátu
Také budeme chtít určit, jaký styl automatického formátování by měla kontingenční tabulka používat. Aspose.Cells má různé formáty, ze kterých si můžeme vybrat. Postup nastavení:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Pomocí tohoto řádku přiřadíme kontingenční tabulce konkrétní typ automatického formátu.`Report5` je pouze příkladem jednoho stylu; můžete si vybrat z různých možností v závislosti na vašich potřebách. 
## Krok 7: Uložte sešit
Nakonec nezapomeňte po provedení všech změn sešit uložit:
```csharp
workbook.Save(dataDir + "output.xls");
```
 Tento řádek kódu uloží upravený sešit do nového souboru s názvem`output.xls` v zadaném adresáři. Nezapomeňte zkontrolovat tento soubor, abyste viděli svou krásně formátovanou kontingenční tabulku!
## Závěr
Gratuluji! Právě jste naprogramovali kontingenční tabulku Excelu do automatického formátu pomocí Aspose.Cells v .NET. Tento proces vám nejen šetří čas při přípravě sestav, ale také zajišťuje konzistentnost toho, jak vaše data vypadají při každém spuštění. Pomocí několika řádků kódu můžete výrazně vylepšit své soubory Excel – stejně jako digitální kouzelník.
## FAQ
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci se soubory aplikace Excel bez nutnosti instalace aplikace Microsoft Excel.
### Mohu naformátovat více kontingenčních tabulek v sešitu?
Ano, můžete procházet více objekty kontingenční tabulky v sešitu a formátovat je jeden po druhém.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
 Absolutně! Můžete začít s bezplatnou zkušební verzí, která je k dispozici[zde](https://releases.aspose.com/).
### Co když se moje kontingenční tabulka neformátuje správně?
Ujistěte se, že na kontingenční tabulku je správně odkazováno a že existuje typ automatického formátování – jinak se může vrátit zpět na výchozí nastavení.
### Mohu tento proces automatizovat pomocí naplánovaných úloh?
Ano! Začleněním tohoto kódu do naplánované úlohy můžete automatizovat generování a pravidelné formátování sestav.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
