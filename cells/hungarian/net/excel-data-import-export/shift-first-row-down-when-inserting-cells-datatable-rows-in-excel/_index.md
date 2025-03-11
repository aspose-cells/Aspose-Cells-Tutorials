---
title: Az első sor eltolása lefelé DataTable sorok beszúrásakor az Excelben
linktitle: Az első sor eltolása lefelé DataTable sorok beszúrásakor az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Tanulja meg a DataTable sorok beszúrását az Excelben anélkül, hogy az első sort lefelé tolná az Aspose.Cells for .NET segítségével. Lépésről lépésre útmutató a könnyű automatizáláshoz.
weight: 11
url: /hu/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az első sor eltolása lefelé DataTable sorok beszúrásakor az Excelben

## Bevezetés

Belefáradt a sorok manuális eltolásába, amikor új adatokat szúr be Excel-táblázataiba? Nos, szerencséd van! Ebben a cikkben bemutatjuk, hogyan automatizálható ez a folyamat az Aspose.Cells for .NET használatával. Ennek az oktatóanyagnak a végére nemcsak az Excel adattáblázatainak kezelését tanulja meg, hanem azt is, hogyan szabhatja testre az importálási beállításokat, hogy jobban megfeleljenek az Ön igényeinek. Bízz bennem; ezzel sok időt és fáradságot takaríthat meg! Szóval, igyál egy csésze kávét, és kezdjük!

## Előfeltételek

Mielőtt belevágnánk a kódolásba, győződjön meg arról, hogy mindent beállított:

1. Visual Studio: Győződjön meg arról, hogy telepítve van a Visual Studio (a 2017-es vagy újabb verzióinak jól kell működnie).
2.  Aspose.Cells for .NET: rendelkeznie kell az Aspose.Cells könyvtárral. Ha még nem tette meg, letöltheti[itt](https://releases.aspose.com/cells/net/).
3. A C# és az Excel alapvető ismerete: A C# programozás és az Excel működésének alapvető ismerete minden bizonnyal segít a hatékonyabb követésben.

 Szüksége lesz egy minta Excel-fájlra is. Ebben az útmutatóban egy mintát fogunk használni`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Létrehozhatja ezt a fájlt, vagy megtalálhatja az igényeinek megfelelő sablont.

## Csomagok importálása

Mielőtt belemerülnénk a kódolásba, meg kell győződnünk arról, hogy importáljuk a szükséges csomagokat. A C# projektben vegye fel a következő névtereket:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ezek a csomagok elengedhetetlenek a munkafüzettel, munkalappal és táblázatokkal való munkához.

## 1. lépés: Állítsa be projektjét

### Hozzon létre egy új C# projektet

Kezdje egy új C# konzolalkalmazás létrehozásával a Visual Studióban. Adjon megfelelő nevet a projektnek, például „ExcelDataImport”.

### Adja hozzá az Aspose.Cells NuGet csomagot

Az Aspose.Cells csomag hozzáadásához kattintson a jobb gombbal a projektre a Solution Explorerben, válassza a Manage NuGet Packages lehetőséget, és keresse meg az „Aspose.Cells” kifejezést. Telepítse a csomagot, hogy biztosan hozzáférjen az összes szükséges funkcióhoz.

## 2. lépés: Határozza meg az adattáblázatot

 Ezt követően megvalósítjuk a`ICellsDataTable` interfész az importálandó adatokat biztosító osztály létrehozásához. Így strukturálhatja a`CellsDataTable` osztály:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Más tagok megvalósítása ...
}
```

Itt minden oszlophoz meghatározzuk az oszlopneveket és az adatokat, ami megkönnyíti az importált táblázatunk szerkezetét.

## 3. lépés: Az ICellsDataTable Interface Members implementálása

 Azon belül`CellsDataTable` osztályban, meg kell valósítani a tagjait a`ICellsDataTable` felület. Íme a szükséges megvalósítás:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Az osztály ezen része kezeli az adatlekérést, meghatározza, hogy hány sor és oszlop legyen, és kezeli az aktuális indexállapotot.

## 4. lépés: Írja be a fő függvényt

 Most pedig hozzuk létre a`Run`módszer a teljes táblázat importálási folyamatának megszervezéséhez:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 5. lépés: Állítsa be az importálási beállításokat

 Az importálási viselkedés szabályozásához létre kell hoznia egy példányt`ImportTableOptions` és ennek megfelelően állítsa be a tulajdonságokat. Pontosabban szeretnénk beállítani`ShiftFirstRowDown` hogy`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Nem akarjuk lefelé tolni az első sort
```

## 6. lépés: Importálja a DataTable-t

 Most már importálhatjuk az adatokat a sajátunkból`CellsDataTable` a munkalapba.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Ez a parancs közvetlenül beszúrja az adattáblázatot a megadott sortól és oszloptól kezdve.

## 7. lépés: Mentse el a munkafüzetet

Végül a módosított munkafüzetet visszamentjük egy fájlba:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Következtetés

És megvan! Az Aspose.Cells for .NET segítségével megtanulta, hogyan lehet DataTable sorokat beszúrni egy Excel-lapba az első sor áthelyezése nélkül. Ez a folyamat nemcsak egyszerűsíti az adatok kezelését az Excelben, hanem az alkalmazás teljesítményét is növeli azáltal, hogy automatizál egy tipikusan nehézkes feladatot. Az eszköztárban található ismeretekkel jobban felkészült az Excel automatizálási feladatainak kezelésére, így időt és erőfeszítést takarít meg.

## GYIK

### Mi az Aspose.Cells a .NET számára?
Az Aspose.Cells for .NET egy programkönyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok létrehozását, kezelését és konvertálását .NET-alkalmazásokban.

### Szükségem van engedélyre az Aspose.Cells használatához?
Igen, a teljes funkciók használatához érvényes licencre lesz szüksége. A kezdeti teszteléshez azonban ingyenes próbaverzió áll rendelkezésre.

### Használhatom az Aspose.Cells-t webes alkalmazásokban?
Teljesen! Az Aspose.Cells tökéletes a .NET-ben fejlesztett asztali, webes és felhőalapú alkalmazásokhoz.

### Milyen típusú Excel-fájlokat hozhatok létre az Aspose.Cells segítségével?
Számos Excel fájlformátumot hozhat létre, beleértve az XLSX, XLS, CSV és egyebeket.

### Hol kaphatok támogatást az Aspose.Cells-hez?
 Kérdéseket tehet fel, vagy segítséget találhat a[Aspose fórumok](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
