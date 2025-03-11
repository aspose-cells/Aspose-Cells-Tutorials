---
title: Adjon hozzá ívvezérlést csatlakozási pontokkal
linktitle: Adjon hozzá ívvezérlést csatlakozási pontokkal
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a részletes útmutatóból megtudhatja, hogyan adhat hozzá ívvezérlőket csatlakozási pontokkal az Aspose.Cells for .NET segítségével.
weight: 27
url: /hu/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adjon hozzá ívvezérlést csatlakozási pontokkal

## Bevezetés
Amikor vizuálisan vonzó Excel-jelentésekről van szó, az illusztrációk létfontosságú szerepet játszanak. Akár pénzügyi jelentést, akár projektlebontást készít, az olyan alakzatok, mint az ívek, használatával mélységet és tisztaságot adhat az adatok bemutatásához. Ma mélyrehatóan belemerülünk abba, hogyan használhatja az Aspose.Cells for .NET-et ívvezérlők hozzáadására csatlakozási pontokkal az Excel-munkalapokon. Tehát, ha valaha is azon töprengett, hogyan fűszerezheti táblázatait vagy énekelheti adatait, olvasson tovább!
## Előfeltételek
Mielőtt belevágnánk a kódolás izgalmába, győződjünk meg arról, hogy minden készen áll. Íme, amire szüksége van:
1. .NET-keretrendszer: Győződjön meg arról, hogy kompatibilis verziója van telepítve. Az Aspose.Cells többféle verzióval működik, beleértve a .NET Core-t is.
2.  Aspose.Cells for .NET: Le kell töltenie és telepítenie kell az Aspose.Cells könyvtárat. Könnyen megragadhatja a[letöltési link](https://releases.aspose.com/cells/net/).
3. Egy jó IDE: A Visual Studio, amely minden .NET-fejlesztő hűséges társa, segít a kódolási élmény egyszerűsítésében.
4. Alapvető C# ismerete: Ha jól ismeri a C#-t, akkor ezt az oktatóanyagot simán meg fogja találni.
5. Hozzáférés a dokumentumkönyvtárhoz: Tudja meg, hová fogja menteni az Excel fájlokat. Ez elengedhetetlen a kimenet hatékony megszervezéséhez.
## Csomagok importálása
A következő lépés annak biztosítása, hogy a megfelelő csomagokat importálja a projektbe. Az Aspose.Cells for .NET különféle funkciókkal rendelkezik, ezért az egyszerűséget megőrizzük. A következőket kell tartalmaznia:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Ezek a névterek hozzáférést biztosítanak az összes rajz- és cellakezelési funkcióhoz, amelyeket ebben az útmutatóban fog használni.
## 1. lépés: Állítsa be a dokumentumkönyvtárat
Először is – hozzunk létre egy könyvtárat, ahová elmentheti a fényes új Excel-fájlokat. Így csináljuk:
```csharp
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ez a kódrészlet ellenőrzi, hogy létezik-e a megadott mappa. Ha nem, akkor létrehoz egyet. Egyszerű, igaz? Mindig jó, ha van egy adott hely a fájljainak, hogy elkerülje a rendetlenséget.
## 2. lépés: Példányosítson munkafüzetet
Most, hogy készen van a könyvtárunk, hozzunk létre egy új Excel-munkafüzetet.
```csharp
Workbook excelbook = new Workbook();
```
 Felhívva a`Workbook` konstruktor, akkor lényegében azt mondod: „Hé, indítsunk egy új Excel-fájlt!” Ez lesz a vászon az összes alakzathoz és adathoz.
## 3. lépés: Az első ív alakzat hozzáadása
Itt kezdődik a móka! Adjuk hozzá az első ív alakzatunkat.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Ez a kódsor ív alakzatot ad az első munkalaphoz. A paraméterek megadják az ív koordinátáit és a görbületét meghatározó szögeket. 
## 4. lépés: Az ív megjelenésének testreszabása
Az üres ívforma olyan, mint egy vászon festék nélkül – kell hozzá egy kis érzék!
### Állítsa be az ívkitöltés színét
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Ez az ívet folyamatosan kékké teszi. A színt bármilyen árnyalatra módosíthatja, ha kicseréli`Color.Blue` másik színért.
### Állítsa be az ív elhelyezését
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Ha az elhelyezést "FreeFloating"-ra állítja, az ív a cellahatároktól függetlenül mozoghat, így rugalmasságot biztosít a pozicionálásban.
### Állítsa be a vonal súlyát és stílusát
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Itt határozhatja meg a vonal súlyát és stílusát, ezáltal feltűnőbbé és látványosabbá teszi azt.
## 5. lépés: Újabb ív alakzat hozzáadása
Miért álljunk meg egynél? Adjunk hozzá még egy ív alakzatot, hogy gazdagítsuk Excel vizualitásunkat.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Az első ívhez hasonlóan ez is egy másik helyen van hozzáadva – itt játszódik le a tervezés varázsa!
## 6. lépés: A második ív testreszabása
Adjunk személyességet a második ívünknek is!
### Változtassa meg az ívvonal színét
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Folyamatosan követjük a kék színt, de mindig keverheti és párosíthatja, hogy megtudja, mi illik a legjobban a dizájnjához!
### Állítsa be az első ívhez hasonló tulajdonságokat
Ügyeljen arra, hogy megismételje ezeket az esztétikai választásokat:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Itt egyszerűen gondoskodik arról, hogy a második ív megegyezzen az elsővel, így összefüggő megjelenést hoz létre a munkalapon.
## 7. lépés: Mentse el a munkafüzetet
Egyetlen remekmű sincs megmentés nélkül, igaz? Ideje beírni az íveket egy Excel-fájlba.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Ez a sor az újonnan létrehozott íveket egy "book1.out.xls" nevű Excel-fájlba menti a kijelölt könyvtárban.
## Következtetés
Gratulálok! Éppen most sajátította el az ívvezérlők csatlakozási pontokkal történő hozzáadásának alapjait az Excel-lapokon az Aspose.Cells for .NET segítségével. Ez a funkció nemcsak szépíti a táblázatokat, hanem az összetett adatokat is könnyebben megemésztheti. Akár tapasztalt fejlesztő, akár csak most kezdő, ezekkel a vizuális elemekkel a jelentéseket unalmasból nagyszerűvé alakíthatja.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy hatékony .NET-könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-fájlok programozott létrehozását és kezelését.
### Használhatom ingyenesen az Aspose.Cells-t?
 Igen! Kipróbálhat egy ingyenes próbaverziót. Látogatás[ezt a linket](https://releases.aspose.com/) kezdeni.
### Hogyan adhatok hozzá más alakzatokat az íveken kívül?
Az Aspose.Cells.Drawing névtérben elérhető különböző osztályokat használhatja különféle alakzatok, például téglalapok, körök és egyebek hozzáadásához.
### Milyen típusú fájlokat hozhatok létre az Aspose.Cells segítségével?
Különféle Excel-formátumokat hozhat létre és kezelhet, beleértve az XLS-t, az XLSX-et, a CSV-t stb.
### Elérhető technikai támogatás az Aspose.Cells számára?
 Teljesen! Hozzáférhet a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9) segítségért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
