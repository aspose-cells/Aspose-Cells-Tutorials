---
"description": "Objevte maximální počet řádků a sloupců podporovaných formáty XLS a XLSX pomocí Aspose.Cells pro .NET. Maximalizujte správu dat v Excelu s tímto komplexním tutoriálem."
"linktitle": "Nalezení maximálního počtu řádků a sloupců podporovaných formáty XLS a XLSX"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Nalezení maximálního počtu řádků a sloupců podporovaných formáty XLS a XLSX"
"url": "/cs/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nalezení maximálního počtu řádků a sloupců podporovaných formáty XLS a XLSX

## Zavedení
Ve světě Excelu může být správa velkých datových sad náročným úkolem, zejména pokud jde o zpracování maximálního počtu řádků a sloupců podporovaných různými formáty souborů. Tento tutoriál vás provede procesem nalezení maximálního počtu řádků a sloupců podporovaných formáty XLS a XLSX pomocí knihovny Aspose.Cells pro .NET. Na konci tohoto článku budete mít komplexní představu o tom, jak tento výkonný nástroj využívat k efektivnímu zvládání úkolů souvisejících s Excelem.
## Předpoklady
Než se pustíme do tutoriálu, ujistěte se, že máte splněny následující předpoklady:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) nebo [.NET Core](https://dotnet.microsoft.com/en-us/download) nainstalovaný ve vašem systému.
2. [Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/) knihovna stažená a odkazovaná ve vašem projektu.
Pokud jste tak ještě neučinili, můžete si stáhnout knihovnu Aspose.Cells pro .NET z [webové stránky](https://releases.aspose.com/cells/net/) nebo si ho nainstalujte přes [NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importovat balíčky
Chcete-li začít, budete muset importovat potřebné balíčky z knihovny Aspose.Cells pro .NET. Na začátek souboru C# přidejte následující příkazy using:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Nalezení maximálního počtu řádků a sloupců podporovaných formátem XLS
Začněme prozkoumáním maximálního počtu řádků a sloupců podporovaných formátem XLS (Excel 97-2003).
```csharp
// Vytiskněte zprávu o formátu XLS.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Vytvořte sešit ve formátu XLS.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Vytiskněte maximální počet řádků a sloupců podporovaných formátem XLS.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
V tomto kroku:
1. Vytiskněte zprávu, která indikuje, že pracujeme s formátem XLS.
2. Vytvořit nový `Workbook` instance používající `FileFormatType.Excel97To2003` enum, který představuje formát XLS.
3. Načíst maximální počet řádků a sloupců podporovaných formátem XLS pomocí `Workbook.Settings.MaxRow` a `Workbook.Settings.MaxColumn` vlastnosti. K těmto hodnotám přičteme 1, abychom získali skutečný maximální počet řádků a sloupců (protože jsou založeny na nule).
4. Vypište maximální počet řádků a sloupců do konzole.
## Krok 2: Nalezení maximálního počtu řádků a sloupců podporovaných formátem XLSX
Dále se podívejme na maximální počet řádků a sloupců podporovaných formátem XLSX (Excel 2007 a novější).
```csharp
// Vytiskněte zprávu o formátu XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Vytvořte sešit ve formátu XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Vypíše maximální počet řádků a sloupců podporovaných formátem XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
V tomto kroku:
1. Vytiskněte zprávu, která indikuje, že pracujeme s formátem XLSX.
2. Vytvořit nový `Workbook` instance používající `FileFormatType.Xlsx` enum, který představuje formát XLSX.
3. Načíst maximální počet řádků a sloupců podporovaných formátem XLSX pomocí `Workbook.Settings.MaxRow` a `Workbook.Settings.MaxColumn` vlastnosti. K těmto hodnotám přičteme 1, abychom získali skutečný maximální počet řádků a sloupců (protože jsou založeny na nule).
4. Vypište maximální počet řádků a sloupců do konzole.
## Krok 3: Zobrazení zprávy o úspěchu
Nakonec si zobrazme zprávu o úspěchu, která indikuje, že příklad „FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats“ byl úspěšně spuštěn.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Tento krok jednoduše vypíše zprávu o úspěchu do konzole.
## Závěr
V tomto tutoriálu jste se naučili, jak pomocí knihovny Aspose.Cells pro .NET najít maximální počet řádků a sloupců podporovaných formáty souborů XLS a XLSX. Pochopením omezení těchto formátů můžete lépe plánovat a spravovat své projekty v Excelu a zajistit, aby se vaše data vešla do podporovaných rozsahů.
## Často kladené otázky
### Jaký je maximální počet řádků podporovaných formátem XLS?
Maximální počet řádků podporovaných formátem XLS (Excel 97-2003) je 65 536.
### Jaký je maximální počet sloupců podporovaných formátem XLS?
Maximální počet sloupců podporovaných formátem XLS (Excel 97-2003) je 256.
### Jaký je maximální počet řádků podporovaných formátem XLSX?
Maximální počet řádků podporovaných formátem XLSX (Excel 2007 a novější) je 1 048 576.
### Jaký je maximální počet sloupců podporovaných formátem XLSX?
Maximální počet sloupců podporovaných formátem XLSX (Excel 2007 a novější) je 16 384.
### Mohu použít knihovnu Aspose.Cells pro .NET pro práci s jinými formáty souborů aplikace Excel?
Ano, knihovna Aspose.Cells pro .NET podporuje širokou škálu formátů souborů aplikace Excel, včetně XLS, XLSX, ODS a dalších. Můžete si prohlédnout [dokumentace](https://reference.aspose.com/cells/net/) seznámit se s dostupnými funkcemi a možnostmi.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}