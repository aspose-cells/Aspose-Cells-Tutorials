---
"description": "Naučte se v tomto podrobném návodu krok za krokem, jak programově nastavit automatické formátování kontingenčních tabulek v Excelu pomocí Aspose.Cells pro .NET."
"linktitle": "Nastavení automatického formátu kontingenční tabulky programově v .NET"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nastavení automatického formátu kontingenční tabulky programově v .NET"
"url": "/cs/net/creating-and-configuring-pivot-tables/setting-auto-format/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení automatického formátu kontingenční tabulky programově v .NET

## Zavedení
Pokud jde o analýzu dat, pivotní tabulky v Excelu mohou být převratné. Umožňují dynamicky shrnout a analyzovat data, což vám pomáhá získat poznatky, které by bylo téměř nemožné extrahovat ručně. Co když ale chcete automatizovat proces formátování pivotních tabulek v .NET? Zde vám ukážu, jak programově nastavit automatický formát pivotní tabulky pomocí výkonné knihovny Aspose.Cells pro .NET.
V této příručce prozkoumáme základy, projdeme si předpoklady, importujeme potřebné balíčky a poté se ponoříme do podrobného tutoriálu, který vám pomůže formátovat kontingenční tabulky jako profesionál. Zní to dobře? Pojďme se do toho pustit!
## Předpoklady
Než začneme, ujistěte se, že máte vše, co potřebujete k zahájení:
1. Vývojové prostředí .NET: Ujistěte se, že máte funkční instanci Visual Studia (nebo jakékoli vývojové prostředí (IDE) s podporou .NET).
2. Knihovna Aspose.Cells: Pro bezproblémovou práci s excelovými soubory budete potřebovat nainstalovanou knihovnu Aspose.Cells. Pokud jste tak ještě neučinili, můžete si ji stáhnout z [stránka ke stažení](https://releases.aspose.com/cells/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět jednotlivým krokům.
4. Soubor Excel (šablona): Pro začátek budete potřebovat soubor šablony Excel, který bude v našem příkladu zpracován. Pro zjednodušení si můžete vytvořit vzorový soubor s názvem `Book1.xls`.
## Importovat balíčky
Abyste mohli ve svém projektu začít používat Aspose.Cells, budete muset importovat potřebné balíčky. Zde je návod, jak to nastavit ve svém .NET projektu:
### Vytvořit nový projekt
Začněte vytvořením nového projektu .NET ve vámi preferovaném IDE. 
### Přidat reference
Nezapomeňte přidat odkaz na knihovnu Aspose.Cells. Pokud jste si knihovnu stáhli, přidejte DLL soubory z extrakce. Pokud používáte NuGet, můžete jednoduše spustit:
```bash
Install-Package Aspose.Cells
```
### Importovat jmenné prostory
Nyní budete muset ve svém souboru s kódem importovat jmenný prostor Aspose.Cells. To můžete provést přidáním následujícího řádku na začátek souboru C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Po dokončení těchto kroků jste připraveni napsat kód!
Nyní si rozdělme kód, který jste poskytli, na podrobné kroky s vysvětlením, co každá část dělá. 
## Krok 1: Definujte adresář dokumentů
Nejprve je třeba nastavit cestu k adresáři s dokumenty, kde se nacházejí soubory aplikace Excel. V našem příkladu ji definujeme takto:
```csharp
string dataDir = "Your Document Directory";  // Upravte dle potřeby
```
Tento řádek vytvoří řetězcovou proměnnou `dataDir` který obsahuje cestu k vašim dokumentům. Nezapomeňte nahradit `"Your Document Directory"` se skutečnou cestou ve vašem systému.
## Krok 2: Načtěte soubor šablony
Dále budete chtít načíst existující sešit, který obsahuje vaši kontingenční tabulku:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Tento řádek inicializuje nový `Workbook` objekt načtením zadaného souboru aplikace Excel. Soubor by měl obsahovat alespoň jednu kontingenční tabulku, aby byly následující kroky účinné.
## Krok 3: Přístup k požadovanému pracovnímu listu
Určete, na kterém listu potřebujete pracovat pro přístup k kontingenční tabulce. V tomto případě si vezmeme pouze první:
```csharp
int pivotIndex = 0;  // Index kontingenční tabulky
Worksheet worksheet = workbook.Worksheets[0];
```
Zde, `worksheet` načte první list ze sešitu. Index kontingenční tabulky je nastaven na `0`, což znamená, že přistupujeme k první kontingenční tabulce v daném listu.
## Krok 4: Vyhledejte kontingenční tabulku
S připraveným pracovním listem je čas přistupovat k vaší kontingenční tabulce:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
Tím se inicializuje nový `PivotTable` objekt získáním pivotní tabulky na zadaném indexu z listu.
## Krok 5: Nastavení vlastnosti automatického formátování
A teď k té šťavnaté části: nastavení možností automatického formátování pro vaši kontingenční tabulku.
```csharp
pivotTable.IsAutoFormat = true; // Povolit automatické formátování
```
Tento řádek povoluje funkci automatického formátování kontingenční tabulky. Pokud je nastaveno na `true`, kontingenční tabulka se automaticky naformátuje na základě předdefinovaných stylů.
## Krok 6: Vyberte konkrétní typ automatického formátování
Také budeme chtít určit, jaký styl automatického formátování má kontingenční tabulka používat. Aspose.Cells nabízí různé formáty, ze kterých si můžeme vybrat. Zde je návod, jak ho nastavit:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
Tímto řádkem přiřadíme kontingenční tabulce specifický typ automatického formátu. `Report5` je to jen příklad jednoho stylu; můžete si vybrat z řady možností v závislosti na vašich potřebách. 
## Krok 7: Uložení sešitu
Nakonec nezapomeňte po provedení všech změn sešit uložit:
```csharp
workbook.Save(dataDir + "output.xls");
```
Tento řádek kódu uloží upravený sešit do nového souboru s názvem `output.xls` v zadaném adresáři. Nezapomeňte tento soubor zkontrolovat, abyste viděli svou krásně naformátovanou kontingenční tabulku!
## Závěr
Gratulujeme! Právě jste naprogramovali automatické formátování pivotní tabulky v Excelu pomocí Aspose.Cells v .NET. Tento proces vám nejen ušetří čas při přípravě sestav, ale také zajistí konzistenci vzhledu dat při každém spuštění. S pouhými několika řádky kódu můžete výrazně vylepšit své soubory v Excelu – stejně jako digitální kouzelník.
## Často kladené otázky
### Co je Aspose.Cells?
Aspose.Cells je výkonná knihovna .NET pro práci s excelovými soubory bez nutnosti instalace Microsoft Excelu.
### Mohu v sešitu formátovat více kontingenčních tabulek?
Ano, můžete v sešitu procházet více objektů kontingenční tabulky a formátovat je jeden po druhém.
### Je k dispozici bezplatná zkušební verze pro Aspose.Cells?
Rozhodně! Můžete začít s bezplatnou zkušební verzí, která je k dispozici. [zde](https://releases.aspose.com/).
### Co když moje kontingenční tabulka nemá správné formátování?
Ujistěte se, že je na kontingenční tabulku správně odkazováno a že existuje typ automatického formátování – jinak se může vrátit k výchozímu nastavení.
### Mohu tento proces automatizovat pomocí naplánovaných úloh?
Ano! Začleněním tohoto kódu do naplánované úlohy můžete pravidelně automatizovat generování a formátování sestav.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}