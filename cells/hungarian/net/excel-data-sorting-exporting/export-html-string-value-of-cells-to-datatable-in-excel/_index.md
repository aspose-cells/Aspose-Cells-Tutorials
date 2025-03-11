---
title: Exportálja a cellák HTML karakterlánc-értékét az Excel adattáblázatába
linktitle: Exportálja a cellák HTML karakterlánc-értékét az Excel adattáblázatába
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan exportálhat HTML-karakterlánc-értékeket Excel-cellákból egy DataTable-ba az Aspose.Cells for .NET használatával egy egyszerű, lépésenkénti oktatóanyagban.
weight: 11
url: /hu/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportálja a cellák HTML karakterlánc-értékét az Excel adattáblázatába

## Bevezetés

Amikor Excel fájlokkal dolgozik .NET környezetben, előfordulhat, hogy információkat kell kivonnia a cellákból, nem csak egyszerű szövegként, hanem HTML-karakterláncként. Ez nagyon hasznos lehet, ha rich text adatokkal foglalkozik, vagy ha meg szeretné tartani a formázást. Ebben az útmutatóban végigvezetem, hogyan exportálhatja a cellák HTML-karakterlánc értékét egy adattáblába az Aspose.Cells for .NET segítségével. 

## Előfeltételek

Mielőtt belemerülne a kódba, győződjön meg arról, hogy minden a helyén van, amire szüksége van. Íme egy gyors ellenőrző lista:

1. Alapvető C# és .NET ismeretek: Mielőtt belevágna a kódolásba, győződjön meg arról, hogy ismeri a C# programozást és a .NET keretrendszer alapjait.
2.  Aspose.Cells for .NET: Ha még nem tette meg, telepítenie kell az Aspose.Cells for .NET programot. Ingyenes próbaverziót letölthet a webhelyről[itt](https://releases.aspose.com/).
3. Visual Studio vagy az Ön által választott IDE: Állítsa be a környezetét C# kód írására. A Visual Studio a szolgáltatások széles skálája és az egyszerű használat miatt ajánlott.
4. Minta Excel fájl: Szüksége lesz egy minta Excel fájlra (`sampleExportTableAsHtmlString.xlsx`) dolgozni. Győződjön meg arról, hogy egy elérhető könyvtárban található.
5. NuGet Package Manager: Győződjön meg arról, hogy rendelkezik hozzáféréssel a NuGet Package Managerhez a projektben az Aspose.Cells könyvtár egyszerű hozzáadásához.

Ha ezeket az előfeltételeket ellenőrizzük, piszkáljuk meg a kezünket egy kis kódolással!

## Csomagok importálása

Mielőtt elkezdhetnénk dolgozni az Aspose.Cells-szel, importálnunk kell a szükséges csomagokat. Ez általában magában foglalja az Aspose.Cells NuGet csomag hozzáadását a projekthez. Íme, hogyan kell csinálni:

### Nyissa meg a NuGet Package Managert

A Visual Studio alkalmazásban kattintson a jobb gombbal a projektre a Solution Explorerben, és válassza a NuGet-csomagok kezelése lehetőséget.

### Aspose.Cells keresése

 A NuGet Package Managerbe írja be`Aspose.Cells` a keresősávban.

### Telepítse a csomagot

Miután megtalálta az Aspose.Cells fájlt, kattintson a Telepítés gombra. Ez hozzáadja a könyvtárat a projekthez, és lehetővé teszi, hogy importálja a kódba.

### Importálja a névteret

Adja hozzá a következő direktívát a kódfájl tetejéhez:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Most, hogy mindent beállítottunk, merüljünk el a HTML-karakterlánc-értékek Excel-fájlból egy DataTable-be történő exportálásának lépésről lépésre történő folyamatába. 

## 1. lépés: Határozza meg a forráskönyvtárat

Kezdje azzal, hogy meghatározza azt a könyvtárat, ahol a minta Excel-fájlt tárolja. Ez kulcsfontosságú, mivel megmondja az alkalmazásnak, hogy hol találja a fájlt. Íme a kód ehhez:

```csharp
string sourceDir = "Your Document Directory";
```

 Mindenképpen cserélje ki`"Your Document Directory"` az Excel-fájl tényleges elérési útjával.

## 2. lépés: Töltse be az Excel mintafájlt

 A következő lépés az Excel munkafüzet betöltése. Használni fogja a`Workbook` osztályban az Aspose.Cells-től. Így töltheti be a fájlt:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Ez az egyszerű kódsor inicializálja a munkafüzetet, és betölti a megadott Excel-fájlt.

## 3. lépés: Nyissa meg az első munkalapot

A munkafüzet betöltése után el kell érnie azt a konkrét munkalapot, amely az Önt érdeklő adatokat tartalmazza. Általában az első munkalappal kell kezdenie:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Itt az első munkalappal (0. index) dolgozunk. Győződjön meg arról, hogy az adatok a megfelelő lapon szerepelnek.

## 4. lépés: Adja meg az exportálási táblázat beállításait

Az adatok exportálásának szabályozásához be kell állítania`ExportTableOptions`. Ebben az esetben biztosítani szeretné, hogy az oszlopnevek ne legyenek exportálva, és a cellaadatokat HTML-karakterláncként szeretné exportálni:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Ez a konfiguráció lehetővé teszi a cellaadatok gazdag formázásának megőrzését az exportálás során.

## 5. lépés: Cellák exportálása DataTable-be

 Most jön a döntő rész, amikor ténylegesen exportálja az adatokat. A`ExportDataTable` módszerrel behúzhatja az adatokat a munkalapról a`DataTable`. Ezt a következőképpen teheti meg:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Ez a kód a cellák egy meghatározott tartományát (a 0. sortól a 0. oszloptól a 3. sorig, a 3. oszlopig) egy DataTable-ba exportálja a korábban megadott beállításokkal.

## 6. lépés: Nyomtassa ki a HTML karakterlánc értékét

Végül nyomtassuk ki a HTML karakterlánc értékét a DataTable egy adott cellájából, hogy megnézzük, mit sikerült exportálnunk. Például, ha ki szeretné nyomtatni az értéket a harmadik sorból és a második oszlopból, tegye a következőket:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Ez a sor kiírja a kívánt HTML karakterláncot a DataTable-ból a konzolba. 

## Következtetés 

És megvan! Sikeresen exportálta a HTML karakterlánc-értékeket egy Excel-fájl celláiból egy DataTable-ba az Aspose.Cells for .NET segítségével. Ez a képesség nem csak az adatkezelési készségeket gazdagítja, hanem kibővíti a lehetőségeit is, amikor közvetlenül Excel-fájlokból formázott tartalmat kezel. 

## GYIK

### Használhatom az Aspose.Cells-t az Excelen kívül más fájlformátumokhoz is?  
Igen, az Aspose.Cells elsősorban az Excelhez való, de az Aspose más könyvtárakat is kínál különböző formátumokhoz.

### Szükségem van licencre az Aspose.Cellshez?  
 Igen, a termelési felhasználáshoz érvényes engedély szükséges. Kaphat ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/).

### Mi a teendő, ha az Excel fájlom képleteket tartalmaz? Rendesen exportálják?  
Igen, az Aspose.Cells képes kezelni a képleteket, és exportáláskor a rendszer a kapott értékekre értékeli ki őket.

### Lehetséges az exportálási beállítások módosítása?  
 Teljesen! Testreszabhatja`ExportTableOptions` hogy megfeleljen az Ön egyedi igényeinek.

### Hol találhatok részletesebb dokumentációt az Aspose.Cells-hez?  
 Részletes dokumentációt találhat[itt](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
