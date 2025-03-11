---
title: Najděte maximální počet řádků a sloupců podporovaných formáty XLS a XLSX
linktitle: Najděte maximální počet řádků a sloupců podporovaných formáty XLS a XLSX
second_title: Aspose.Cells .NET Excel Processing API
description: Objevte maximální počet řádků a sloupců podporovaných formáty XLS a XLSX pomocí Aspose.Cells pro .NET. Maximalizujte správu dat v Excelu pomocí tohoto komplexního kurzu.
weight: 11
url: /cs/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Najděte maximální počet řádků a sloupců podporovaných formáty XLS a XLSX

## Zavedení
Ve světě Excelu může být správa velkých datových sad náročným úkolem, zejména pokud jde o manipulaci s maximálním počtem řádků a sloupců podporovaných různými formáty souborů. Tento tutoriál vás provede procesem nalezení maximálního počtu řádků a sloupců podporovaných formáty XLS a XLSX pomocí knihovny Aspose.Cells for .NET. Na konci tohoto článku budete mít ucelenou představu o tom, jak využít tento výkonný nástroj k efektivnímu zpracování úloh souvisejících s Excelem.
## Předpoklady
Než se pustíme do výukového programu, ujistěte se, že máte splněny následující předpoklady:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) nebo[.NET Core](https://dotnet.microsoft.com/en-us/download) nainstalovaný ve vašem systému.
2. [Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/) knihovnu staženou a odkazovanou ve vašem projektu.
 Pokud jste tak ještě neučinili, můžete si stáhnout knihovnu Aspose.Cells for .NET z webu[webové stránky](https://releases.aspose.com/cells/net/) nebo jej nainstalujte přes[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importujte balíčky
Chcete-li začít, budete muset importovat potřebné balíčky z knihovny Aspose.Cells for .NET. Přidejte následující pomocí příkazů v horní části souboru C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Krok 1: Najděte maximální počet řádků a sloupců podporovaných formátem XLS
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
1. Vytiskněte zprávu o tom, že pracujeme s formátem XLS.
2.  Vytvořte nový`Workbook` instance pomocí`FileFormatType.Excel97To2003` enum, který představuje formát XLS.
3.  Získejte maximální počet řádků a sloupců podporovaných formátem XLS pomocí`Workbook.Settings.MaxRow` a`Workbook.Settings.MaxColumn`vlastnosti, resp. K těmto hodnotám přidáme 1, abychom získali skutečný maximální počet řádků a sloupců (protože jsou založeny na nule).
4. Vytiskněte maximální počet řádků a sloupců do konzoly.
## Krok 2: Najděte maximální počet řádků a sloupců podporovaných formátem XLSX
Dále se podívejme na maximální počet řádků a sloupců podporovaných formátem XLSX (Excel 2007 a novější).
```csharp
// Vytiskněte zprávu o formátu XLSX.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Vytvořte sešit ve formátu XLSX.
wb = new Workbook(FileFormatType.Xlsx);
// Vytiskněte maximální počet řádků a sloupců podporovaných formátem XLSX.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
V tomto kroku:
1. Vytiskněte zprávu o tom, že pracujeme s formátem XLSX.
2.  Vytvořte nový`Workbook` instance pomocí`FileFormatType.Xlsx` enum, který představuje formát XLSX.
3.  Získejte maximální počet řádků a sloupců podporovaných formátem XLSX pomocí`Workbook.Settings.MaxRow` a`Workbook.Settings.MaxColumn`vlastnosti, resp. K těmto hodnotám přidáme 1, abychom získali skutečný maximální počet řádků a sloupců (protože jsou založeny na nule).
4. Vytiskněte maximální počet řádků a sloupců do konzoly.
## Krok 3: Zobrazte zprávu o úspěchu
Nakonec zobrazme zprávu o úspěchu, která indikuje, že příklad "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" byl úspěšně proveden.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Tento krok jednoduše vytiskne zprávu o úspěchu do konzole.
## Závěr
tomto tutoriálu jste se naučili, jak používat knihovnu Aspose.Cells for .NET k nalezení maximálního počtu řádků a sloupců podporovaných formáty souborů XLS a XLSX. Když pochopíte omezení těchto formátů, můžete lépe plánovat a spravovat své projekty založené na Excelu a zajistit, aby vaše data odpovídala podporovaným rozsahům.
## FAQ
### Jaký je maximální počet řádků podporovaných formátem XLS?
Maximální počet řádků podporovaných formátem XLS (Excel 97-2003) je 65 536.
### Jaký je maximální počet sloupců podporovaných formátem XLS?
Maximální počet sloupců podporovaných formátem XLS (Excel 97-2003) je 256.
### Jaký je maximální počet řádků podporovaných formátem XLSX?
Maximální počet řádků podporovaných formátem XLSX (Excel 2007 a novější) je 1 048 576.
### Jaký je maximální počet sloupců podporovaných formátem XLSX?
Maximální počet sloupců podporovaných formátem XLSX (Excel 2007 a novější) je 16 384.
### Mohu použít knihovnu Aspose.Cells for .NET pro práci s jinými formáty souborů aplikace Excel?
 Ano, knihovna Aspose.Cells for .NET podporuje širokou škálu formátů souborů Excel, včetně XLS, XLSX, ODS a dalších. Můžete prozkoumat[dokumentace](https://reference.aspose.com/cells/net/) se dozvíte o dostupných funkcích a funkcích.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
