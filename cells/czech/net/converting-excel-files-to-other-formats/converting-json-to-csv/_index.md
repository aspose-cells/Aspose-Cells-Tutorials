---
title: Převod JSON na CSV programově v .NET
linktitle: Převod JSON na CSV programově v .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak převést JSON na CSV programově v .NET pomocí Aspose.Cells. Postupujte podle našeho podrobného průvodce, abyste zajistili bezproblémovou transformaci dat.
weight: 15
url: /cs/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod JSON na CSV programově v .NET

## Zavedení
dnešním digitálním světě se zpracování dat ve více formátech stalo samozřejmostí a JSON (JavaScript Object Notation) je jedním z nejpoužívanějších formátů pro výměnu dat. Co se ale stane, když potřebujete transformovat tento JSON do formátu, který je přístupnější pro analýzu, jako je CSV (Comma Separated Values)? Tento tutoriál vás provede procesem převodu JSON na CSV programově pomocí Aspose.Cells for .NET – snadno použitelného, ale výkonného rozhraní API pro manipulaci s tabulkami. 
## Předpoklady
Než se ponoříme do kódu, je nezbytné zajistit, abyste měli všechny potřebné komponenty a základní znalosti nástrojů, které budeme používat. Pojďme si nastínit, co potřebujete:
-  Aspose.Cells for .NET: Toto je primární knihovna, kterou použijeme pro převod JSON do CSV. Můžete[stáhněte si jej zde](https://releases.aspose.com/cells/net/).
- Visual Studio: K psaní a spouštění kódu .NET budete potřebovat integrované vývojové prostředí (IDE), jako je Visual Studio.
- .NET Framework: Ujistěte se, že máte nainstalované rozhraní .NET Framework. Aspose.Cells je kompatibilní s .NET Core i .NET Framework.
- Základní znalost C#: I když tato příručka rozebere každou část kódu, pomůže vám, pokud jste trochu obeznámeni s C#.
## Importujte balíčky
Chcete-li použít Aspose.Cells ve svém projektu .NET, musíte nejprve nainstalovat knihovnu. Můžete to udělat pomocí Správce balíčků NuGet:
1. Otevřete Visual Studio.
2. Přejděte na Nástroje > Správce balíčků NuGet > Spravovat balíčky NuGet pro řešení.
3. Vyhledejte Aspose.Cells a nainstalujte nejnovější verzi.
Po instalaci se ujistěte, že jste do kódu zahrnuli následující jmenné prostory:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Nyní, když je vše nastaveno, pojďme si kód rozebrat krok za krokem, abyste viděli, jak snadné je převést soubor JSON do CSV pomocí Aspose.Cells.
## Krok 1: Přečtěte si soubor JSON
 První věc, kterou musíme udělat, je načíst data JSON ze souboru. Budeme předpokládat, že již máte soubor JSON (říkejme tomu`SampleJson.json`) uložený v adresáři ve vašem systému.
Můžete použít`File.ReadAllText()` metoda v C# pro načtení obsahu souboru JSON do řetězce.
```csharp
// Zdrojový adresář
string sourceDir = "Your Document Directory";
// Přečtěte si soubor JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Tento krok je zásadní, protože ke spuštění procesu převodu potřebujete nezpracovaná data JSON. Tím, že jej čtete jako řetězec, jej připravujete ke zpracování Aspose.Cells.
## Krok 2: Vytvořte prázdný sešit
Aspose.Cells funguje především na sešitech (excelových souborech). Chcete-li začít importovat data JSON, musíte nejprve vytvořit prázdný sešit, kam budou tato data vložena.
```csharp
// Vytvořte prázdný sešit
Workbook workbook = new Workbook();
```
Zde inicializujete prázdný sešit, který bude nakonec obsahovat data ve formátu CSV. Představte si to jako vytvoření prázdné tabulky v Excelu, která bude brzy naplněna vašimi daty JSON.
## Krok 3: Přístup k buňkám v sešitu
 Nyní, když máme prázdný sešit, potřebujeme získat přístup k jeho buňkám. The`Cells` kolekce v Aspose.Cells představuje všechny buňky v listu, kam umístíte svá data JSON.
```csharp
// Získejte buňky
Cells cells = workbook.Worksheets[0].Cells;
```
Tento fragment kódu vybere první list (list na indexu 0) a získá jeho`Cells` sbírka. Tyto buňky jsou jako mřížka tabulky, do které budou přidána data.
## Krok 4: Nastavte JsonLayoutOptions
 Aspose.Cells poskytuje několik možností přizpůsobení, jak budou vaše data JSON importována. Zde definujeme`JsonLayoutOptions` určit, jak má Aspose zacházet s poli, číselnými daty a názvy objektů.
```csharp
// Nastavte JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Automaticky převádí hodnoty řetězce, které jsou číselné nebo datumové.
- ArrayAsTable: Zacházejte s poli v JSON jako s tabulkami v sešitu.
- IgnoreArrayTitle a IgnoreObjectTitle: Tyto možnosti ignorují názvy polí a objektů a zajišťují, že se importují pouze nezpracovaná data.
## Krok 5: Importujte data JSON
 Jakmile jsou možnosti rozvržení nastaveny, je čas přinést data JSON. The`JsonUtility.ImportData()` metoda zde dělá těžkou práci a vkládá data JSON do buněk sešitu.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Tato metoda vyžaduje několik parametrů:
- `str`Řetězec JSON, který jsme přečetli v kroku 1.
- `cells`: Kolekce buněk, do které budou data umístěna.
- `0, 0`: Toto jsou řádkové a sloupcové indexy označující, kde by měla data začínat (tj. levý horní roh).
- `importOptions`: Možnosti rozvržení, které jsme nastavili v kroku 4.
## Krok 6: Uložte sešit jako CSV
Nyní, když jsou data JSON v sešitu, můžeme sešit snadno uložit jako soubor CSV. CSV je jednoduchý, odlehčený formát pro ukládání tabulkových dat, díky čemuž je ideální pro analýzu dat.
```csharp
// Výstupní adresář
string outputDir = "Your Document Directory";
// Uložit sešit
workbook.Save(outputDir + @"SampleJson_out.csv");
```
V tomto kroku uložíme sešit jako soubor CSV. Zadáte cestu a název souboru (`SampleJson_out.csv`), kam bude CSV uložen.
## Krok 7: Potvrďte proces
Abychom zajistili, že vše fungovalo podle očekávání, můžeme vytisknout potvrzovací zprávu v konzole.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Jednoduchá zpráva o úspěchu pomáhá potvrdit, že proces proběhl hladce.
## Závěr
Převod JSON do CSV pomocí Aspose.Cells for .NET je přímočarý, ale výkonný proces. Pomocí několika řádků kódu můžete transformovat složitá data JSON do dostupnějšího formátu CSV. Ať už máte co do činění s poli, objekty nebo číselnými daty, Aspose.Cells usnadňuje konfiguraci procesu převodu tak, aby vyhovoval vašim potřebám.
## FAQ
### Dokáže Aspose.Cells zpracovat velké soubory JSON?
Ano, Aspose.Cells je navržen tak, aby efektivně zpracovával velké datové sady, takže je vhodný pro zpracování velkých souborů JSON bez problémů s výkonem.
### Jak mohu přizpůsobit výstup CSV?
 Výstup CSV můžete upravit úpravou`JsonLayoutOptions` nebo manipulace s formátováním sešitu před jeho uložením jako CSV.
### Existuje způsob, jak vyloučit určitá data z JSON během převodu?
Ano, vyladěním JSON nebo použitím vlastní logiky kódu před importem můžete vyloučit nebo odfiltrovat konkrétní datová pole.
### Podporuje Aspose.Cells jiné formáty souborů kromě CSV?
Absolutně! Aspose.Cells podporuje širokou škálu formátů včetně Excelu (XLS, XLSX), PDF, HTML a mnoha dalších.
### Jak mohu zdarma vyzkoušet Aspose.Cells?
 Můžete[stáhněte si bezplatnou zkušební verzi zde](https://releases.aspose.com/) k otestování všech funkcí před nákupem.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
