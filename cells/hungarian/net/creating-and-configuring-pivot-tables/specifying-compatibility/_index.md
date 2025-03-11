---
title: Adja meg az Excel-fájl programozott kompatibilitását .NET-ben
linktitle: Adja meg az Excel-fájl programozott kompatibilitását .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg az Excel pivot tábláinak kezelését az Aspose.Cells for .NET segítségével, beleértve az adatfrissítéseket, a kompatibilitási beállításokat és a cellaformázást.
weight: 23
url: /hu/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adja meg az Excel-fájl programozott kompatibilitását .NET-ben

## Bevezetés

mai adatközpontú világban az Excel-fájlok programozott kezelése és kezelése sok fejlesztő számára elengedhetetlenné vált. Ha Excellel dolgozik .NET-ben, az Aspose.Cells egy hatékony könyvtár, amely megkönnyíti az Excel-fájlok létrehozását, olvasását, módosítását és mentését. A könyvtár egyik fontos funkciója lehetővé teszi az Excel-fájlok kompatibilitásának programozott megadását. Ebben az oktatóanyagban megvizsgáljuk, hogyan lehet kezelni az Excel-fájlokat, különös tekintettel a kompatibilitás kezelésére az Aspose.Cells for .NET használatával. A végére megérti, hogyan állíthatja be az Excel-fájlok kompatibilitását, különösen a pivot táblák esetében, miközben frissíti és kezeli az adatokat.

## Előfeltételek

Mielőtt belevágna a kódolási fázisba, győződjön meg arról, hogy rendelkezik a következőkkel:

1. Alapvető C# ismerete: Mivel a kódot C#-ban fogjuk írni, a nyelv ismerete segít jobban megérteni az oktatóanyagot.
2.  Aspose.Cells for .NET könyvtár: Letöltheti a[Az Aspose Cells kiadási oldala](https://releases.aspose.com/cells/net/)Ha még nem tette meg, fontolja meg az ingyenes próbaverzió beszerzését, hogy először fedezze fel a funkcióit.
3. Visual Studio: Egy IDE, ahol hatékonyan írhatja és tesztelheti C# kódját.
4.  Minta Excel-fájl: Győződjön meg arról, hogy rendelkezik egy minta Excel-fájllal, lehetőleg olyannal, amely tartalmaz egy pivot táblát a bemutatóhoz. Példánkban használni fogjuk`sample-pivot-table.xlsx`.

Ha ezekkel az előfeltételekkel rendelkezik, kezdjük el a kódolási folyamatot.

## Csomagok importálása

Mielőtt elkezdené írni az alkalmazást, bele kell foglalnia a szükséges névtereket a kódba, hogy hatékonyan tudja használni az Aspose.Cells könyvtárat. Íme, hogyan kell csinálni.

### Importálja az Aspose.Cells névteret

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Ez a kódsor biztosítja, hogy az Aspose.Cells könyvtár összes osztályához és metódusához hozzáférjen.

Most pedig részletezzük a folyamatot, hogy minden világos és érthető legyen.

## 1. lépés: Állítsa be a címtárat

Először is állítsa be azt a könyvtárat, amelyben az Excel-fájlok találhatók. Fontos a megfelelő fájl elérési út megadása.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```

 Tessék, cserélje ki`"Your Document Directory"`az Excel-fájlok tényleges elérési útjával. Itt kell lennie a minta pivot tábla fájljának.

## 2. lépés: Töltse be az Excel forrásfájlt

Ezután be kell töltenünk a minta pivot táblát tartalmazó Excel fájlt. 

```csharp
// Töltse be a minta kimutatástáblázatot tartalmazó Excel forrásfájlt
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 Ebben a lépésben létrehozzuk a`Workbook` osztály, amely betölti a megadott Excel fájlt. 

## 3. lépés: Nyissa meg a munkalapokat

Most, hogy a munkafüzet betöltődött, el kell érnie a kimutatástábla adatait tartalmazó munkalapot.

```csharp
// Hozzáférés az első munkalaphoz, amely kimutatástáblázat adatait tartalmazza
Worksheet dataSheet = wb.Worksheets[0];
```

Itt elérjük az első munkalapot, ahol a pivot tábla található. Az Excel-struktúra alapján más munkalapokat is megkereshet vagy megadhat.

## 4. lépés: A cellaadatok manipulálása

Ezután módosítani kell néhány cellaértéket a munkalapon. 

### 4.1. lépés: Módosítsa az A3 cellát

Kezdjük azzal, hogy elérjük az A3 cellát, és beállítjuk az értékét.

```csharp
// Hozzáférés az A3 cellához, és beállíthatja az adatait
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Ez a kódrészlet frissíti az A3 cellát a „FooBar” értékkel.

### 4.2. lépés: Módosítsa a B3 cellát hosszú karakterlánccal

Most állítsunk be egy hosszú karakterláncot a B3 cellába, amely meghaladja az Excel szabványos karakterkorlátait.

```csharp
// Hozzáférés a B3 cellához, beállítja az adatait
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Ez a kód azért fontos, mert meghatározza az adatkorlátokkal kapcsolatos elvárásait, különösen akkor, ha az Excel kompatibilitási beállításaival dolgozik.

## 5. lépés: Ellenőrizze a B3 cella hosszát

Szintén elengedhetetlen a beírt karakterlánc hosszának megerősítése.

```csharp
// Nyomtassa ki a B3 cella hosszát
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Ez csak az ellenőrzésre szolgál, hogy megmutassa, hány karaktert tartalmaz a cella.

## 6. lépés: Állítsa be a többi cellaértéket

Most több cellát fogunk elérni, és beállítunk néhány értéket.

```csharp
// Hozzáférés a C3 cellához, és beállíthatja annak adatait
cell = cells["C3"];
cell.PutValue("closed");

// Hozzáférés a D3 cellához, és beállíthatja annak adatait
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Ezen kódrészletek mindegyike több további cellát frissít a munkalapon.

## 7. lépés: Nyissa meg a Pivot Table-t

Ezután elérheti a második munkalapot, amely a pivot tábla adatait tartalmazza.

```csharp
//Nyissa meg a kimutatástáblázatot tartalmazó második munkalapot
Worksheet pivotSheet = wb.Worksheets[1];

// Hozzáférés a pivot táblához
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Ez a kódrészlet lehetővé teszi a pivot tábla módosítását a kompatibilitási beállításokhoz.

## 8. lépés: Állítsa be az Excel 2003 kompatibilitását

Kulcsfontosságú annak beállítása, hogy a kimutatás kompatibilis-e az Excel 2003-mal vagy sem. 

```csharp
// Az IsExcel2003Compatible tulajdonság megmondja, hogy a PivotTable kompatibilis-e az Excel2003-mal, miközben frissíti a kimutatást
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 Itt kezdődik az igazi átalakulás. Beállítás által`IsExcel2003Compatible` hogy`true`, frissítéskor a karakterhosszt 255-re korlátozza.

## 9. lépés: Ellenőrizze a hosszt a kompatibilitási beállítás után

A kompatibilitás beállítása után nézzük meg, hogyan hat az adatokra.

```csharp
// Ellenőrizze a kimutatáslap B5 cellájának értékét.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Valószínűleg megjelenik egy olyan kimenet, amely megerősíti a csonkítási hatást, ha a kezdeti adat meghaladja a 255 karaktert.

## 10. lépés: A kompatibilitási beállítás módosítása

Most változtassuk meg a kompatibilitási beállításokat, és ellenőrizzük újra.

```csharp
//Most állítsa az IsExcel2003Compatible tulajdonságot false értékre, majd frissítse újra
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Ez lehetővé teszi az adatok eredeti hosszának tükrözését a korábbi korlátozások nélkül.

## 11. lépés: Ellenőrizze újra a hosszt 

Ellenőrizzük, hogy az adatok most pontosan tükrözik a valós hosszukat.

```csharp
// Most kinyomtatja a cellaadatok eredeti hosszát. Az adatok most nem lettek csonkolva.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Látnia kell, hogy a kimenet megerősíti a csonkítás eltávolítását.

## 12. lépés: Formázza meg a cellákat

A vizuális élmény fokozása érdekében érdemes lehet formázni a cellákat. 

```csharp
// Állítsa be a B5 cella sormagasságát és oszlopszélességét, és tördelje a szöveget is
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Ezek a kódsorok megkönnyítik az adatok olvashatóságát a cellaméretek módosításával és a szöveg tördelésének engedélyezésével.

## 13. lépés: Mentse el a munkafüzetet

Végül mentse el a munkafüzetet az elvégzett változtatásokkal.

```csharp
// Mentse a munkafüzetet xlsx formátumban
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 A megfelelő fájlformátum kiválasztása kulcsfontosságú az Excel fájlok mentésekor. A`Xlsx`formátumot széles körben használják, és számos Excel-verzióval kompatibilis.

## Következtetés

Gratulálok! Az Aspose.Cells for .NET segítségével most beprogramozta az Excel fájlkompatibilitási beállításait. Ez az oktatóanyag felvázolta az egyes lépéseket, a környezet beállításától a pivot táblák kompatibilitási beállításainak módosításáig. Ha valaha is olyan adatokkal dolgozott, amelyek meghatározott korlátozásokat vagy kompatibilitást igényeltek, ez egy olyan képesség, amelyet nem szeretne figyelmen kívül hagyni.

## GYIK

### Mi az Aspose.Cells?  
Az Aspose.Cells egy .NET-könyvtár, amelyet arra terveztek, hogy segítse a fejlesztőket Excel-fájlok zökkenőmentes létrehozásában, kezelésében és konvertálásában.

### Miért fontos az Excel kompatibilitás?  
Az Excel-kompatibilitás kulcsfontosságú annak biztosításához, hogy a fájlok megnyithatók és használhatók legyenek az Excel tervezett verzióiban, különösen akkor, ha olyan funkciókat vagy formátumokat tartalmaznak, amelyeket a korábbi verziók nem támogatnak.

### Létrehozhatok-e programozottan kimutatástáblákat az Aspose.Cells segítségével?  
Igen, az Aspose.Cells használatával programozottan is létrehozhat és manipulálhat kimutatástáblázatokat. A könyvtár különféle módszereket kínál a kimutatástáblákhoz társított adatforrások, mezők és szolgáltatások hozzáadásához.

### Hogyan ellenőrizhetem egy karakterlánc hosszát egy Excel cellában?  
Használhatja a`StringValue` tulajdona a`Cell` objektumot a cella tartalmának lekéréséhez, majd hívja meg a`.Length` tulajdonságot, hogy megtudja a karakterlánc hosszát.

### Testreszabhatom a cella formázását a sor magasságán és szélességén túl?  
 Teljesen! Az Aspose.Cells kiterjedt cellaformázást tesz lehetővé. Megváltoztathatja a betűstílusokat, színeket, szegélyeket, számformátumokat és még sok minden mást a segítségével`Style` osztály.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
