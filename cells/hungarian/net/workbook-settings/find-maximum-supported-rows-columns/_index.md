---
title: Keresse meg az XLS és XLSX formátumok által támogatott maximális sorokat és oszlopokat
linktitle: Keresse meg az XLS és XLSX formátumok által támogatott maximális sorokat és oszlopokat
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel az XLS és XLSX formátumok által támogatott maximális sorokat és oszlopokat az Aspose.Cells for .NET segítségével. Maximalizálja Excel adatkezelését ezzel az átfogó oktatóanyaggal.
weight: 11
url: /hu/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Keresse meg az XLS és XLSX formátumok által támogatott maximális sorokat és oszlopokat

## Bevezetés
Az Excel világában a nagy adatkészletek kezelése ijesztő feladat lehet, különösen, ha a különböző fájlformátumok által támogatott maximális számú sor és oszlop kezeléséről van szó. Ez az oktatóanyag végigvezeti Önt az XLS és XLSX formátumok által támogatott maximális sorok és oszlopok megtalálásán az Aspose.Cells for .NET könyvtár használatával. A cikk végére átfogóan megérti, hogyan használhatja ezt a hatékony eszközt az Excel-lel kapcsolatos feladatok hatékony kezelésére.
## Előfeltételek
Mielőtt belevágnánk az oktatóanyagba, győződjön meg arról, hogy a következő előfeltételek teljesülnek:
1. [.NET-keretrendszer](https://dotnet.microsoft.com/en-us/download) vagy[.NET Core](https://dotnet.microsoft.com/en-us/download) telepítve van a rendszerére.
2. [Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) letöltött és a projektben hivatkozott könyvtár.
 Ha még nem tette meg, letöltheti az Aspose.Cells for .NET könyvtárat a[weboldal](https://releases.aspose.com/cells/net/) vagy telepítse keresztül[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Csomagok importálása
A kezdéshez importálnia kell a szükséges csomagokat az Aspose.Cells for .NET könyvtárból. Adja hozzá a következőket utasításokkal a C# fájl tetején:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 1. lépés: Keresse meg az XLS formátum által támogatott maximális sorokat és oszlopokat
Kezdjük az XLS (Excel 97-2003) formátum által támogatott maximális sorok és oszlopok feltárásával.
```csharp
// Nyomtasson üzenetet az XLS formátumról.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Hozzon létre munkafüzetet XLS formátumban.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Nyomtassa ki az XLS formátum által támogatott maximális sorokat és oszlopokat.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
Ebben a lépésben mi:
1. Nyomtasson ki egy üzenetet, jelezve, hogy az XLS formátummal dolgozunk.
2.  Hozzon létre egy újat`Workbook` például a`FileFormatType.Excel97To2003` enum, amely az XLS formátumot képviseli.
3.  Az XLS formátum által támogatott maximális sorok és oszlopok lekérése a`Workbook.Settings.MaxRow` és`Workbook.Settings.MaxColumn`tulajdonságait, ill. Ezekhez az értékekhez 1-et adunk, hogy megkapjuk a tényleges maximális sor- és oszlopszámot (mivel ezek nulla alapúak).
4. Nyomtassa ki a maximális sorokat és oszlopokat a konzolra.
## 2. lépés: Keresse meg az XLSX formátum által támogatott maximális sorokat és oszlopokat
Ezután vizsgáljuk meg az XLSX (Excel 2007 és újabb) formátum által támogatott maximális sorokat és oszlopokat.
```csharp
// Nyomtasson üzenetet az XLSX formátumról.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Hozzon létre munkafüzetet XLSX formátumban.
wb = new Workbook(FileFormatType.Xlsx);
// Nyomtassa ki az XLSX formátum által támogatott maximális sorokat és oszlopokat.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
Ebben a lépésben mi:
1. Nyomtasson ki egy üzenetet, jelezve, hogy az XLSX formátummal dolgozunk.
2.  Hozzon létre egy újat`Workbook` például a`FileFormatType.Xlsx` enum, amely az XLSX formátumot képviseli.
3.  Az XLSX formátum által támogatott maximális sorok és oszlopok lekérése a`Workbook.Settings.MaxRow` és`Workbook.Settings.MaxColumn`tulajdonságait, ill. Ezekhez az értékekhez 1-et adunk, hogy megkapjuk a tényleges maximális sor- és oszlopszámot (mivel ezek nulla alapúak).
4. Nyomtassa ki a maximális sorokat és oszlopokat a konzolra.
## 3. lépés: Jelenítsen meg egy sikerüzenetet
Végül jelenítsünk meg egy sikerüzenetet, jelezve, hogy a „FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats” példa sikeresen lefutott.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Ez a lépés egyszerűen sikeres üzenetet nyomtat a konzolra.
## Következtetés
Ebben az oktatóanyagban megtanulta, hogyan használhatja az Aspose.Cells for .NET könyvtárat az XLS és XLSX fájlformátumok által támogatott maximális sorok és oszlopok megkeresésére. Ha megérti ezeknek a formátumoknak a korlátait, jobban megtervezheti és kezelheti Excel-alapú projektjeit, biztosítva, hogy adatai beleférjenek a támogatott tartományokba.
## GYIK
### Mekkora az XLS formátum által támogatott sorok maximális száma?
Az XLS (Excel 97-2003) formátum által támogatott sorok maximális száma 65 536.
### Mennyi az XLS formátum által támogatott oszlopok maximális száma?
Az XLS (Excel 97-2003) formátum által támogatott oszlopok maximális száma 256.
### Mekkora az XLSX formátum által támogatott sorok maximális száma?
Az XLSX (Excel 2007 és újabb) formátum által támogatott sorok maximális száma 1 048 576.
### Mennyi az XLSX formátum által támogatott oszlopok maximális száma?
Az XLSX (Excel 2007 és újabb) formátum által támogatott oszlopok maximális száma 16 384.
### Használhatom az Aspose.Cells for .NET könyvtárat más Excel fájlformátumokkal való együttműködéshez?
 Igen, az Aspose.Cells for .NET könyvtár az Excel fájlformátumok széles skáláját támogatja, beleértve az XLS-t, XLSX-et, ODS-t és még sok mást. Feltárhatod a[dokumentáció](https://reference.aspose.com/cells/net/) hogy megismerje az elérhető funkciókat és funkciókat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
