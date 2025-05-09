---
"description": "Ismerje meg ebben a részletes útmutatóban, hogyan adhat hozzá ívvezérlőket csatlakozási pontokkal az Aspose.Cells for .NET használatával."
"linktitle": "Ívvezérlés hozzáadása csatlakozási pontokkal"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Ívvezérlés hozzáadása csatlakozási pontokkal"
"url": "/hu/net/excel-shapes-controls/add-arc-control-with-connection-points/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ívvezérlés hozzáadása csatlakozási pontokkal

## Bevezetés
Amikor vizuálisan lebilincselő Excel-jelentések létrehozásáról van szó, az illusztrációk létfontosságú szerepet játszanak. Akár pénzügyi jelentést, akár projektlebontást készít, az olyan alakzatok, mint az ívek, mélységet és érthetőséget adhatnak az adatprezentációhoz. Ma mélyrehatóan megvizsgáljuk, hogyan használható az Aspose.Cells for .NET ívvezérlők hozzáadásához csatlakozási pontokkal az Excel-munkafüzetekben. Tehát, ha valaha is elgondolkodott azon, hogyan dobhatja fel a táblázatait, vagy hogyan teheti éneklővé adatait, olvasson tovább!
## Előfeltételek
Mielőtt belevágnánk a kódolás izgalmába, győződjünk meg róla, hogy minden készen áll. Íme, amire szükséged van:
1. .NET Framework: Győződjön meg róla, hogy kompatibilis verzió van telepítve. Az Aspose.Cells több verzióval is működik, beleértve a .NET Core-t is.
2. Aspose.Cells .NET-hez: Le kell töltened és telepítened az Aspose.Cells könyvtárat. Könnyen letöltheted innen: [letöltési link](https://releases.aspose.com/cells/net/).
3. Egy jó IDE: A Visual Studio, minden .NET fejlesztő hűséges társa, segít gördülékenyebbé tenni a kódolási élményt.
4. C# alapismeretek: Ha ismered a C#-ot, ez az oktatóanyag simán fog menni.
5. Hozzáférés a dokumentumkönyvtárhoz: Tudd, hová fogod menteni az Excel-fájljaidat. Ez elengedhetetlen a kimenet hatékony rendszerezéséhez.
## Csomagok importálása
A következő lépés annak biztosítása, hogy a megfelelő csomagokat importáld a projektedbe. Az Aspose.Cells for .NET számos funkcióval rendelkezik, ezért egyszerűen fogjuk kezelni. Íme, amire szükséged lesz:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ezek a névterek hozzáférést biztosítanak az útmutatóban használt összes rajzolási és cellakezelési funkcióhoz.
## 1. lépés: Dokumentumkönyvtár beállítása
Először is hozzunk létre egy könyvtárat, ahová menteni fogjuk ezeket a vadonatúj Excel-fájlokat. Így csináljuk:
```csharp
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a kódrészlet ellenőrzi, hogy létezik-e a megadott mappa. Ha nem, akkor létrehoz egyet. Egyszerű, ugye? Mindig jó, ha van egy meghatározott hely a fájljaidnak, hogy elkerüljük a rendetlenséget.
## 2. lépés: Munkafüzet példányosítása
Most, hogy elkészült a könyvtárunk, hozzunk létre egy új Excel-munkafüzetet.
```csharp
Workbook excelbook = new Workbook();
```
Azzal, hogy felhívja a `Workbook` konstruktorral lényegében azt mondod: „Hé, kezdjünk egy új Excel-fájlt!” Ez lesz a vászon az összes alakzatod és adatod számára.
## 3. lépés: Az első ív alakzat hozzáadása
Itt kezdődik a móka! Adjuk hozzá az első ív alakzatunkat.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Ez a kódsor egy ív alakzatot ad hozzá az első munkalaphoz. A paraméterek az ív koordinátáit és a görbületét meghatározó szögeket adják meg. 
## 4. lépés: Az ív megjelenésének testreszabása
Egy üres ív olyan, mint egy festék nélküli vászon – kell hozzá egy kis csillogás!
### Ív kitöltési színének beállítása
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Ettől az ív egyszínű kék lesz. A színt bármilyen kívánt árnyalatra megváltoztathatod a cserével. `Color.Blue` egy másik színért.
### Ív elhelyezésének beállítása
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
A „FreeFloating” elhelyezés beállítása lehetővé teszi az ív számára, hogy a cellahatároktól függetlenül mozogjon, így rugalmasan pozicionálható.
### Vonalvastagság és stílus beállítása
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Itt határozhatod meg a vonal vastagságát és stílusát, így az hangsúlyosabb és vizuálisan vonzóbb lesz.
## 5. lépés: Újabb ív alakzat hozzáadása
Miért állnánk meg egynél? Adjunk hozzá egy másik ív alakzatot, hogy gazdagítsuk az Excel vizualizációnkat.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Az első ívhez hasonlóan ezt is más pozícióban adjuk hozzá – itt játszódik le a tervezés varázslata!
## 6. lépés: A második ív testreszabása
Adjunk a második ívnek is egy kis személyiséget!
### Ívvonal színének módosítása
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Egységes kék színt használunk, de bármikor keverheted és párosíthatod, hogy lásd, mi illik a legjobban a dizájnodhoz!
### Az első ívhez hasonló tulajdonságok beállítása
Ügyeljen arra, hogy megismételje ezeket az esztétikai döntéseket:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Itt egyszerűen csak arról gondoskodsz, hogy a második ív illeszkedjen az elsőhöz, így egységes megjelenést teremtve a munkalapon.
## 7. lépés: Mentse el a munkafüzetét
Egyetlen remekmű sem teljes mentés nélkül, igaz? Ideje kiírni az íveket egy Excel fájlba.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Ez a sor elmenti az újonnan létrehozott íveket egy "book1.out.xls" nevű Excel fájlba a megadott könyvtárban.
## Következtetés
Gratulálunk! Most elsajátítottad az ívvezérlők csatlakozási pontokkal való hozzáadásának alapjait az Excel-táblázataidban az Aspose.Cells for .NET használatával. Ez a funkció nemcsak széppé teszi a táblázataidat, hanem a komplex adatokat is könnyebben emészthetővé teheti. Akár tapasztalt fejlesztő vagy, akár most kezded, ezek a vizuális elemek a jelentéseidet unalmasból grandiózussá varázsolhatják.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET könyvtár, amely lehetővé teszi a fejlesztők számára, hogy programozottan hozzanak létre és manipuláljanak Excel fájlokat.
### Ingyenesen használhatom az Aspose.Cells-t?
Igen! Ingyenes próbaverziót is kipróbálhat. Látogasson el ide. [ezt a linket](https://releases.aspose.com/) hogy elkezdje.
### Hogyan adhatok hozzá más alakzatokat az íveken kívül?
Az Aspose.Cells.Drawing névtérben elérhető különböző osztályokat használhatod különféle alakzatok, például téglalapok, körök és egyebek hozzáadásához.
### Milyen típusú fájlokat hozhatok létre az Aspose.Cells segítségével?
Különböző Excel formátumokat hozhat létre és kezelhet, beleértve az XLS, XLSX, CSV és egyebeket.
### Elérhető technikai támogatás az Aspose.Cells-hez?
Természetesen! Hozzáférhetsz a [Aspose támogatói fórum](https://forum.aspose.com/c/cells/9) segítségért.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}