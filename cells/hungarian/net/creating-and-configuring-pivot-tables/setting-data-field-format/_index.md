---
title: Az adatmező formátumának programozott beállítása .NET-ben
linktitle: Az adatmező formátumának programozott beállítása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Az Aspose.Cells for .NET segítségével az adatmező-formátumok főbeállítása pivot táblákban ezzel a lépésről lépésre bemutatott oktatóanyaggal. Javítsa az Excel adatformázást.
weight: 19
url: /hu/net/creating-and-configuring-pivot-tables/setting-data-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az adatmező formátumának programozott beállítása .NET-ben

## Bevezetés
Ha az Excel-fájlok .NET használatával történő manipulációiba merül, akkor valószínűleg olyan adatkészletekkel kereszteződött az útja, amelyek különleges formázást igényelnek. Az egyik általános követelmény, hogy az adatmezőket, különösen a kimutatástáblákban, úgy állítsa be, hogy az adatok ne csak érthetőek legyenek, hanem vizuálisan is vonzóak és áttekinthetőek legyenek. Az Aspose.Cells for .NET segítségével ez a feladat gyerekjáték lehet. Ebben az oktatóanyagban szó szerint lebontjuk, hogyan állíthat be programozott adatmező-formátumokat a .NET-ben lépésről lépésre, kihívást jelent az ijesztő bonyolultságokkal, és mindezt emészthetővé téve!
## Előfeltételek
Mielőtt nekivágnánk ennek az utazásnak, gondoskodjunk arról, hogy minden rendben legyen. Íme egy gyors ellenőrző lista arról, hogy mire van szüksége:
1. Visual Studio: Mert ki nem szereti a jó integrált fejlesztői környezetet (IDE)?
2.  Aspose.Cells for .NET Library: Könnyen letöltheti a[Aspose Releases oldal](https://releases.aspose.com/cells/net/).
3. C# alapismeretek: Ha érted a programozási nyelv alapjait, akkor készen állsz!
### Miért az Aspose.Cells?
Az Aspose.Cells for .NET egy hatékony könyvtár, amelyet kifejezetten az Excel fájlműveleteinek kezelésére terveztek. Segítségével könnyedén olvashat, írhat, kezelhet és konvertálhat Excel fájlokat. Képzelje el, hogy képes programozottan jelentéseket, pivot táblákat vagy akár diagramokat készíteni anélkül, hogy bele kellene ásnia magát az Excel felhasználói felületébe – varázslatosnak hangzik, igaz?
## Csomagok importálása
Most, hogy minden előfeltételünk megvan, ugorjunk bele a következő lépésekbe. Kezdje a szükséges csomagok importálásával. A következőképpen állíthatja be ezeket:
### Hozzon létre egy új projektet
Nyissa meg a Visual Studio-t, és hozzon létre egy új C#-projektet. Válasszon egy konzolalkalmazássablont, mivel mi fogjuk végezni a háttérfeldolgozást.
### Adja hozzá az Aspose.Cells hivatkozást
1. Kattintson a jobb gombbal a projektre a Solution Explorerben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. A Tallózás részben keressen rá az „Aspose.Cells” kifejezésre.
4. Telepítse a könyvtárat. A telepítés után készen áll az importálásra!
### Importálja a szükséges névtereket
A C#-kódfájl tetején adja hozzá a következő névtereket:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Ez hozzáférést biztosít az Aspose.Cells által kínált funkciókhoz.

Rendben, most elérkeztünk a programunk lényegéhez. Egy meglévő Excel-fájllal fogunk dolgozni – nevezzük el "Book1.xls"-nek az oktatóanyag kedvéért.
## 1. lépés: Határozza meg az adattárat
Először is meg kell mondania a programnak, hogy hol találja ezt az értékes Excel-fájlt.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory"; // Mindenképpen változtassa meg ezt a tényleges útvonalra!
```
## 2. lépés: Töltse be a munkafüzetet
A munkafüzet betöltése olyan, mintha kinyitnánk egy könyvet, mielőtt elolvasnánk. Íme, hogyan kell csinálni:
```csharp
// Töltsön be egy sablonfájlt
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Győződjön meg arról, hogy a Book1.xls jól ül a megadott könyvtárban, különben néhány akadozásba ütközhet!
## 3. lépés: Nyissa meg az első munkalapot
Most, hogy megvan a munkafüzetünk, tegyük a kezünkbe az első munkalapot (például könyvünk borítóját):
```csharp
// Szerezd meg az első munkalapot
Worksheet worksheet = workbook.Worksheets[0]; // Az index 0-ról indul!
```
## 4. lépés: Nyissa meg a Pivot Table-t
A munkalap a kezünkben van, itt az ideje, hogy megkeressük azt a pivot táblát, amellyel dolgoznunk kell.
```csharp
int pivotindex = 0; // Feltéve, hogy az első pivot táblát szeretné
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
## 5. lépés: Szerezze be az adatmezőket
Most, hogy a pivot táblában vagyunk, húzzuk ki az adatmezőket. Gondolja ezt úgy, hogy bemegy egy könyvtárba, és bizonyos könyveket (vagy adatmezőket) hoz le.
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.DataFields;
```
## 6. lépés: Nyissa meg az első adatmezőt
A mezők gyűjteményéből az elsőt érhetjük el. Ez olyan, mintha az első könyvet venné le a polcról, hogy elolvassa.
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0]; // Szerezze meg az első adatmezőt
```
## 7. lépés: Állítsa be az adatmegjelenítési formátumot
Következő lépésként állítsuk be a pivot mező adatmegjelenítési formátumát. Itt kezdheti meg az értelmes látványelemek – például százalékok – megjelenítését:
```csharp
// Az adatok megjelenítési formátumának beállítása
pivotField.DataDisplayFormat = Aspose.Cells.Pivot.PivotFieldDataDisplayFormat.PercentageOf;
```
## 8. lépés: Állítsa be az alapmezőt és az alapelemet
Minden pivot mező egy másik mezőhöz köthető alaphivatkozásként. Állítsuk be:
```csharp
//Az alapmező beállítása
pivotField.BaseFieldIndex = 1; // Használjon megfelelő indexet az alapmezőhöz
// Az alapelem beállítása
pivotField.BaseItemPosition = Aspose.Cells.Pivot.PivotItemPosition.Next; // Válassza ki a következő elemet
```
## 9. lépés: Állítsa be a számformátumot
Egy lépéssel tovább lépve állítsuk be a számformátumot. Ez olyan, mintha eldöntené, hogyan jelenítse meg a számokat – tegyük őket ügyessé!
```csharp
// Számformátum beállítása
pivotField.Number = 10; // Szükség szerint használja a formátumindexet
```
## 10. lépés: Mentse el az Excel fájlt
Minden kész és kész! Ideje menteni a változtatásokat. A munkafüzeted most tükrözni fogja az összes hatalmas változtatást, amit most végrehajtott.
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "output.xls");
```
És itt van, emberek! A kimutatástáblázat adatmezői most már tökéletesre formázva vannak!
## Következtetés
Gratulálok! Éppen most végezte el az adatmező-formátumok programozott beállítását .NET-ben az Aspose.Cells használatával. Minden egyes lépéssel visszahúztuk a komplexitás rétegeit, lehetővé téve, hogy dinamikusan kommunikáljon az Excellel, módosítsa a pivot táblákat, és megjelenítse az adatokat használható formátumban. Folytassa a gyakorlást, fedezzen fel további funkciókat.
## GYIK
### Használhatom az Aspose.Cells-t Excel-fájlok létrehozására a semmiből?
Teljesen! Az Aspose.Cells segítségével az alapoktól kezdve létrehozhat és kezelhet Excel-fájlokat.
### Van ingyenes próbaverzió?
 Igen! Megnézheti a[Ingyenes próbaverzió](https://releases.aspose.com/).
### Milyen formátumokat támogat az Aspose.Cells az Excel-fájlokhoz?
Különféle formátumokat támogat, beleértve az XLS-t, XLSX-et, CSV-t és még sok mást.
### Fizetnem kell az engedélyért?
 Van egy-két lehetőséged! Licenc vásárolható a[Vásárlás oldal](https://purchase.aspose.com/buy) . Alternatív megoldásként a[Ideiglenes jogosítvány](https://purchase.aspose.com/temporary-license/) is elérhető.
### Hol találok támogatást, ha problémáim vannak?
 Támogatást találhatsz náluk[Támogatási fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
