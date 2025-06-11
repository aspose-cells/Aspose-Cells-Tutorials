---
"description": "Tanulja meg az Excel pivot táblák kezelését az Aspose.Cells for .NET segítségével, beleértve az adatfrissítéseket, a kompatibilitási beállításokat és a cellaformázást."
"linktitle": "Excel fájlok kompatibilitásának programozott megadása .NET-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Excel fájlok kompatibilitásának programozott megadása .NET-ben"
"url": "/hu/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel fájlok kompatibilitásának programozott megadása .NET-ben

## Bevezetés

A mai adatvezérelt világban az Excel-fájlok programozott kezelése és manipulálása elengedhetetlenné vált sok fejlesztő számára. Ha .NET-ben dolgozol Excellel, az Aspose.Cells egy hatékony függvénytár, amely megkönnyíti az Excel-fájlok létrehozását, olvasását, módosítását és mentését. A függvénytár egyik fontos funkciója lehetővé teszi az Excel-fájlok kompatibilitásának programozott megadását. Ebben az oktatóanyagban megvizsgáljuk, hogyan lehet manipulálni az Excel-fájlokat, különös tekintettel az Aspose.Cells for .NET használatával történő kompatibilitáskezelésre. A végére megérted, hogyan állíthatod be az Excel-fájlok kompatibilitását, különösen a kimutatástáblák esetében, miközben frissíted és kezeled az adatokat.

## Előfeltételek

Mielőtt belevágnál a kódolási fázisba, győződj meg róla, hogy rendelkezel a következőkkel:

1. C# alapismeretek: Mivel C#-ban fogunk kódot írni, a nyelv ismerete segít jobban megérteni a bemutatót.
2. Aspose.Cells for .NET könyvtár: Letöltheti innen: [Aspose Cells kiadási oldal](https://releases.aspose.com/cells/net/)Ha még nem tette meg, először érdemes lehet ingyenes próbaverziót igénybe vennie, hogy felfedezhesse a funkcióit.
3. Visual Studio: Egy IDE, ahol hatékonyan írhatsz és tesztelhetsz C# kódot.
4. Minta Excel fájl: Győződjön meg róla, hogy van egy minta Excel fájlja, lehetőleg olyat, amely tartalmaz egy kimutatástáblát a demóhoz. Példánkban a következőt fogjuk használni: `sample-pivot-table.xlsx`.

Miután ezeket az előfeltételeket teljesítettük, kezdjük el a kódolási folyamatot.

## Csomagok importálása

Mielőtt elkezdenéd az alkalmazásod írását, a kódodba bele kell foglalnod a szükséges névtereket az Aspose.Cells könyvtár hatékony használatához. Íme, hogyan teheted meg.

### Aspose.Cells névtér importálása

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Ez a kódsor biztosítja, hogy az Aspose.Cells könyvtár összes osztályához és metódusához hozzáférhess.

Most pedig részletesen elemezzük a folyamatot, hogy minden világos és érthető legyen.

## 1. lépés: Állítsa be a címtárát

Először is állítsd be azt a könyvtárat, ahová az Excel-fájljaid kerülnek. Fontos, hogy a megfelelő fájlelérési utat add meg.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```

Itt cserélje ki `"Your Document Directory"` az Excel-fájlok tényleges elérési útjával. Itt kell lennie a minta pivot tábla fájlnak.

## 2. lépés: Töltse be a forrás Excel fájlt

Ezután be kell töltenünk a minta pivot táblázatot tartalmazó Excel fájlt. 

```csharp
// Minta pivot táblázatot tartalmazó forrás excel fájl betöltése
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

Ebben a lépésben létrehozunk egy példányt a `Workbook` osztály, amely betölti a megadott Excel fájlt. 

## 3. lépés: Hozzáférés a munkalapokhoz

Most, hogy a munkafüzet betöltődött, hozzá kell férnie a kimutatástábla adatait tartalmazó munkalaphoz.

```csharp
// Hozzáférés az első olyan munkalaphoz, amely kimutatástábla-adatokat tartalmaz
Worksheet dataSheet = wb.Worksheets[0];
```

Itt elérjük az első munkalapot, amelyen a pivot tábla található. Az Excel struktúrája alapján további munkalapokat is megadhat, vagy végiglépkedhet rajta.

## 4. lépés: Celladatok manipulálása

Következő lépésként módosítani fogsz néhány cellaértéket a munkalapon. 

### 4.1. lépés: Az A3 cella módosítása

Kezdjük az A3 cellához való hozzáféréssel és az értékének beállításával.

```csharp
// Hozzáférés az A3 cellához és az adatainak beállítása
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Ez a kódrészlet frissíti az A3 cellát a „FooBar” értékkel.

### 4.2. lépés: A B3 cella módosítása hosszú karakterlánccal

Most állítsunk be egy hosszú karakterláncot a B3 cellába, amely meghaladja az Excel szabványos karakterkorlátját.

```csharp
// Hozzáférés a B3 cellához, beállítja az adatait
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Ez a kód azért fontos, mert meghatározza az adatkorlátokkal kapcsolatos elvárásokat, különösen az Excel kompatibilitási beállításaival végzett munka során.

## 5. lépés: Ellenőrizze a B3 cella hosszát

Az is fontos, hogy megerősítsük a beírt karakterlánc hosszát.

```csharp
// B3 cella karakterláncának hosszának kinyomtatása
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Ez csak ellenőrzésre szolgál, hogy megtudjuk, hány karakter van a celládban.

## 6. lépés: Egyéb cellaértékek beállítása

Most további cellákat fogunk elérni, és beállítunk néhány értéket.

```csharp
// Hozzáférés a C3 cellához és az adatainak beállítása
cell = cells["C3"];
cell.PutValue("closed");

// Hozzáférés a D3 cellához és az adatainak beállítása
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Ezen kódrészletek mindegyike több további cellát frissít a munkalapon belül.

## 7. lépés: A kimutatástábla elérése

Ezután a második munkalapot fogod elérni, amely a kimutatástábla adatait tartalmazza.

```csharp
// Hozzáférés a második munkalaphoz, amely a pivot táblát tartalmazza
Worksheet pivotSheet = wb.Worksheets[1];

// Hozzáférés a pivot táblához
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Ez a kódrészlet lehetővé teszi a pivot tábla kompatibilitási beállításokhoz történő manipulálását.

## 8. lépés: Az Excel 2003 kompatibilitásának beállítása

Fontos beállítani, hogy a pivot tábla kompatibilis-e az Excel 2003-mal vagy sem. 

```csharp
// Az IsExcel2003Compatible tulajdonság a PivotTable frissítésekor jelzi, hogy a PivotTable kompatibilis-e az Excel2003-mal.
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Itt kezdődik az igazi átalakulás. A beállítással `IsExcel2003Compatible` hogy `true`frissítéskor a karakterek hosszát 255-re korlátozod.

## 9. lépés: Ellenőrizze a hosszúságot a kompatibilitási beállítás után

A kompatibilitás beállítása után nézzük meg, hogyan befolyásolja az adatokat.

```csharp
// Ellenőrizd a pivot munkalap B5 cellájának értékét.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Valószínűleg egy olyan kimenetet fog látni, amely megerősíti a csonkolás hatását, ha a kezdeti adatok meghaladják a 255 karaktert.

## 10. lépés: Kompatibilitási beállítások módosítása

Most módosítsuk a kompatibilitási beállítást, és ellenőrizzük újra.

```csharp
// Most állítsd az IsExcel2003Compatible tulajdonságot hamis értékre, majd frissítsd újra
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Ez lehetővé teszi, hogy az adatok az eredeti hosszukat tükrözzék a korábbi korlátozások nélkül.

## 11. lépés: Ellenőrizze újra a hosszt 

Ellenőrizzük, hogy az adatok most már pontosan tükrözik-e a valós hosszukat.

```csharp
// Most kinyomtatja a cellaadatok eredeti hosszát. Az adatokat most nem csonkolták.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Látnia kell, hogy a kimenet megerősíti a csonkolás eltávolítását.

## 12. lépés: A cellák formázása

vizuális élmény fokozása érdekében érdemes lehet formázni a cellákat. 

```csharp
// A B5 cella sormagasságának és oszlopszélességének beállítása, valamint a szöveg tördelése
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Ezek a kódsorok megkönnyítik az adatok olvashatóságát a cellaméretek módosításával és a szövegkörnyezet tördelésének engedélyezésével.

## 13. lépés: A munkafüzet mentése

Végül mentse el a munkafüzetet a végrehajtott módosításokkal.

```csharp
// Munkafüzet mentése xlsx formátumban
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

A megfelelő fájlformátum kiválasztása kulcsfontosságú az Excel fájlok mentésekor. `Xlsx` formátum széles körben használt és kompatibilis az Excel számos verziójával.

## Következtetés

Gratulálunk! Most már programozta az Excel fájlok kompatibilitási beállításait az Aspose.Cells for .NET használatával. Ez az oktatóanyag minden lépést felvázolt, a környezet beállításától a pivot táblák kompatibilitási beállításainak módosításáig. Ha valaha is dolgozott olyan adatokkal, amelyekhez speciális korlátozások vagy kompatibilitás szükséges, akkor ezt a készséget nem szeretné figyelmen kívül hagyni.

## GYIK

### Mi az Aspose.Cells?  
Az Aspose.Cells egy .NET könyvtár, amelyet úgy terveztek, hogy segítsen a fejlesztőknek zökkenőmentesen létrehozni, manipulálni és konvertálni az Excel fájlokat.

### Miért fontos az Excel kompatibilitás?  
Az Excel kompatibilitása elengedhetetlen annak biztosításához, hogy a fájlokat az Excel kívánt verzióiban lehessen megnyitni és használni, különösen akkor, ha olyan funkciókat vagy formátumokat tartalmaznak, amelyeket a korábbi verziók nem támogattak.

### Létrehozhatok programozottan pivot táblákat az Aspose.Cells segítségével?  
Igen, a pivot táblákat programozottan is létrehozhatja és módosíthatja az Aspose.Cells segítségével. A könyvtár különféle metódusokat kínál a pivot táblákhoz társított adatforrások, mezők és funkciók hozzáadására.

### Hogyan tudom ellenőrizni egy karakterlánc hosszát egy Excel cellában?  
Használhatod a `StringValue` egy tulajdona `Cell` objektumot a cella tartalmának lekéréséhez, majd a `.Length` tulajdonságot a karakterlánc hosszának megkereséséhez.

### Testreszabhatom a cellaformázást a sormagasságon és -szélességen túl is?  
Abszolút! Az Aspose.Cells kiterjedt cellaformázási lehetőségeket kínál. Módosíthatod a betűtípust, színeket, szegélyeket, számformátumokat és sok mást a... `Style` osztály.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}