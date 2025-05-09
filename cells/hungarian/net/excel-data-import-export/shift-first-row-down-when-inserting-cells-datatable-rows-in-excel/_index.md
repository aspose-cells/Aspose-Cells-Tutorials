---
"description": "Tanuld meg, hogyan szúrhatsz be DataTable sorokat Excelben anélkül, hogy az első sort lejjebb tolnád az Aspose.Cells for .NET segítségével. Lépésről lépésre útmutató a könnyed automatizáláshoz."
"linktitle": "Az első sor eltolása lefelé az adattábla sorainak beszúrásakor Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Az első sor eltolása lefelé az adattábla sorainak beszúrásakor Excelben"
"url": "/hu/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Az első sor eltolása lefelé az adattábla sorainak beszúrásakor Excelben

## Bevezetés

Elege van abból, hogy manuálisan kell sorokat tolni, amikor új adatokat illeszt be az Excel-táblázatokba? Nos, szerencséje van! Ebben a cikkben részletesebben is bemutatjuk, hogyan automatizálhatja ezt a folyamatot az Aspose.Cells for .NET segítségével. A bemutató végére nemcsak azt tanulja meg, hogyan kell adattáblákkal dolgozni Excelben, hanem azt is, hogyan szabhatja testre az importálási beállításokat, hogy jobban megfeleljenek az igényeinek. Hidd el, ez sok időt és energiát takaríthat meg Önnek! Szóval, igyon egy csésze kávét, és kezdjük is!

## Előfeltételek

Mielőtt belevágnánk a kódolásba, győződjünk meg róla, hogy mindent beállítottunk:

1. Visual Studio: Győződjön meg róla, hogy telepítve van a Visual Studio (a 2017-es vagy újabb verziónak megfelelően működnie kell).
2. Aspose.Cells .NET-hez: Szükséged lesz az Aspose.Cells könyvtárra. Ha még nem tetted meg, letöltheted. [itt](https://releases.aspose.com/cells/net/).
3. C# és Excel alapismeretek: A C# programozás és az Excel működésének alapvető ismerete minden bizonnyal segíteni fog abban, hogy hatékonyabban kövesd a feladatokat.

Érdemes kéznél tartani egy minta Excel fájlt is. Ebben az útmutatóban egy úgynevezett mintát fogunk használni. `sampleImportTableOptionsShiftFirstRowDown.xlsx`Létrehozhatod ezt a fájlt, vagy kereshetsz egy az igényeidnek megfelelő sablont.

## Csomagok importálása

Mielőtt belevágnánk a kódolásba, ellenőriznünk kell, hogy importáltuk-e a szükséges csomagokat. A C# projektedben a következő névtereket használd:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Ezek a csomagok elengedhetetlenek a munkafüzet, a munkalap és a táblázatok használatához.

## 1. lépés: A projekt beállítása

### Új C# projekt létrehozása

Kezdésként hozz létre egy új C# konzolalkalmazást a Visual Studioban. Adj a projektednek egy megfelelő nevet, például „ExcelDataImport”.

### Aspose.Cells NuGet csomag hozzáadása

Az Aspose.Cells csomag hozzáadásához kattintson jobb gombbal a projektre a Megoldáskezelőben, válassza a NuGet csomagok kezelése lehetőséget, és keressen rá az „Aspose.Cells” kifejezésre. Telepítse a csomagot, hogy biztosan hozzáférhessen az összes szükséges funkcióhoz.

## 2. lépés: Az adattábla definiálása

Következőként implementáljuk a `ICellsDataTable` felületet egy olyan osztály létrehozásához, amely az importálandó adatokat biztosítja. Így strukturálhatja a `CellsDataTable` osztály:

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

Itt definiáljuk az oszlopneveket és az egyes oszlopok adatait, ami megkönnyíti az importált táblázat szerkezetét.

## 3. lépés: Az ICellsDataTable interfész tagjainak megvalósítása

A `CellsDataTable` osztályban meg kell valósítani a tagjait `ICellsDataTable` felület. Íme a szükséges implementáció:

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

Az osztálynak ez a része az adatlekéréssel, a sorok és oszlopok számának meghatározásával, valamint az aktuális indexállapot kezelésével foglalkozik.

## 4. lépés: Írd meg a fő függvényt

Most pedig hozzuk létre a `Run` metódus a teljes táblaimportálási folyamat összehangolására:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 5. lépés: Importálási beállítások megadása

Az importálási viselkedés szabályozásához létre kell hoznia egy példányt a következőből: `ImportTableOptions` és ennek megfelelően állítsuk be a tulajdonságokat. Konkrétan azt szeretnénk beállítani, hogy `ShiftFirstRowDown` hogy `false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Nem akarjuk az első sort lejjebb tolni.
```

## 6. lépés: Importálja az adattáblát

Most importálhatjuk az adatokat a mi `CellsDataTable` a munkalapba.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Ez a parancs közvetlenül beszúrja az adattáblát a megadott sortól és oszloptól kezdve.

## 7. lépés: A munkafüzet mentése

Végül a módosított munkafüzetet visszamentjük egy fájlba:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Következtetés

És íme! Megtanultad, hogyan szúrhatsz be DataTable sorokat egy Excel-táblázatba az első sor áthelyezése nélkül az Aspose.Cells for .NET használatával. Ez a folyamat nemcsak az Excelen belüli adatkezelést egyszerűsíti, hanem az alkalmazás teljesítményét is javítja egy jellemzően nehézkes feladat automatizálásával. Ezzel a tudással az eszköztáradban jobban felkészülhetsz az Excel automatizálási feladatainak kezelésére, így időt és energiát takaríthatsz meg.

## GYIK

### Mi az Aspose.Cells .NET-hez?
Az Aspose.Cells for .NET egy programozási könyvtár, amely lehetővé teszi a fejlesztők számára Excel-fájlok létrehozását, kezelését és konvertálását .NET-alkalmazásokban.

### Szükségem van licencre az Aspose.Cells használatához?
Igen, érvényes licencre lesz szükséged a teljes funkciók használatához. Azonban ingyenes próbaverzió áll rendelkezésre a kezdeti teszteléshez.

### Használhatom az Aspose.Cells-t webes alkalmazásokban?
Abszolút! Az Aspose.Cells tökéletes .NET-ben fejlesztett asztali, webes és felhőalapú alkalmazásokhoz.

### Milyen típusú Excel fájlokat hozhatok létre az Aspose.Cells segítségével?
Számos Excel fájlformátumot hozhat létre, többek között XLSX, XLS, CSV és egyebeket.

### Hol kaphatok támogatást az Aspose.Cells-hez?
Kérdéseket tehet fel vagy segítséget kérhet a [Aspose fórumok](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}