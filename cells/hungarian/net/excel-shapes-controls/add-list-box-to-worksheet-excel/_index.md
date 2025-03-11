---
title: Listadoboz hozzáadása az Excel munkalapjához
linktitle: Listadoboz hozzáadása az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat hozzá listamezőt egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Kövesse egyszerű, lépésenkénti útmutatónkat, és tegye interaktívvá Excel-lapjait.
weight: 20
url: /hu/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Listadoboz hozzáadása az Excel munkalapjához

## Bevezetés
Interaktív elemek, például listamezők hozzáadása az Excel-munkalapokhoz jelentősen javíthatja az adatkezelést és a megjelenítést. Akár interaktív űrlapot, akár egyéni adatbeviteli eszközt hoz létre, a felhasználói bevitel listamezővel történő szabályozásának lehetősége felbecsülhetetlen értékű. Az Aspose.Cells for .NET hatékony módot biztosít ezeknek a vezérlőknek az Excel-fájlokba való hozzáadására és kezelésére. Ebben az útmutatóban végigvezetjük a listadoboz munkalapokhoz való hozzáadásának folyamatán az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belevágna a kódolásba, győződjön meg arról, hogy a következő eszközökkel és erőforrásokkal rendelkezik:
-  Aspose.Cells for .NET Library: Letöltheti a[Aspose.Cells for .NET letöltési oldal](https://releases.aspose.com/cells/net/).
- Fejlesztői környezet: Bármely IDE, amely támogatja a .NET fejlesztést, például a Visual Studio.
- .NET-keretrendszer: Győződjön meg arról, hogy projektje a .NET-keretrendszer támogatott verzióját célozza meg.
 Ezenkívül fontolja meg a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) ha az összes funkciót korlátozás nélkül szeretné felfedezni.
## Csomagok importálása
Mielőtt elkezdené, győződjön meg arról, hogy importálta a szükséges Aspose.Cells névtereket. Ezt a következőképpen teheti meg:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Ebben az oktatóanyagban a listamező hozzáadásának folyamatát több egyszerű lépésre bontjuk. Gondosan kövesse az egyes lépéseket, hogy minden a várt módon működjön.
## 1. lépés: A dokumentumkönyvtár beállítása
Mielőtt bármilyen Excel-fájlt hozna létre, meg kell adnia egy helyet a mentéshez. A következőképpen állíthatja be a könyvtárat:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ebben a lépésben meg kell határoznia, hogy a fájl hol kerüljön tárolásra. A kód ellenőrzi, hogy létezik-e a könyvtár, és ha nem, akkor létrehoz egyet. Ez biztosítja, hogy a későbbiekben ne kerüljön bele a "fájl nem található" hibaüzenetbe.
## 2. lépés: Hozzon létre egy új munkafüzetet, és nyissa meg az első munkalapot
Ezután létrehozunk egy új munkafüzetet, és elérjük az első munkalapot, amelyhez hozzáadjuk a listánkat.
```csharp
// Hozzon létre egy új munkafüzetet.
Workbook workbook = new Workbook();
// Szerezd meg az első munkalapot.
Worksheet sheet = workbook.Worksheets[0];
```
A munkafüzet lényegében az Ön Excel-fájlja. Itt egy új munkafüzetet hozunk létre, és elérjük az első munkalapot, ahol elhelyezzük a listamezőnket. Gondoljon erre úgy, mint egy üres vászon létrehozására, amelyen a vezérlőket festeni fogja.
## 3. lépés: Adatok bevitele a listadobozhoz
Mielőtt hozzáadnánk a listamezőt, fel kell töltenünk néhány adatot, amelyekre a listamező hivatkozni fog.
```csharp
// Szerezze be a munkalap cellagyűjteményét.
Cells cells = sheet.Cells;
// Adjon meg egy értéket a címke számára.
cells["B3"].PutValue("Choose Dept:");
// Állítsa félkövérre a címkét.
cells["B3"].GetStyle().Font.IsBold = true;
// Adja meg a listamező értékeit.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Itt egy kis szöveget adunk a munkalaphoz. A "Choose Dept:" címke a B3 cellába kerül, a betűtípus pedig félkövérre van állítva. Az A oszlopba olyan értékeket szúrunk be, amelyek a listamező beviteli tartományaként szolgálnak, és különböző részlegeket képviselnek. Ebből a beviteli tartományból választhatnak a felhasználók a listamezővel való interakció során.
## 4. lépés: Adja hozzá a listadobozt a munkalaphoz
Most, hogy beállítottuk az adatokat, adjuk hozzá magát a listadoboz-vezérlőt.
```csharp
// Új listamező hozzáadása.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Ez a kód hozzáadja a listamezőt a munkalaphoz. A paraméterek határozzák meg a listamező helyét és méretét. A listamező a 2. sor 0. oszlopában található, szélessége 122, magassága 100. Ezek azok a koordináták és méretek, amelyek meghatározzák, hogy a listamező hol jelenjen meg a munkalapon.
## 5. lépés: Állítsa be a List Box tulajdonságait
Ezután különböző tulajdonságokat állítunk be a listamezőhöz, hogy teljesen működőképes legyen.
```csharp
// Állítsa be az elhelyezés típusát.
listBox.Placement = PlacementType.FreeFloating;
// Állítsa be a csatolt cellát.
listBox.LinkedCell = "A1";
// Állítsa be a beviteli tartományt.
listBox.InputRange = "A2:A7";
// Állítsa be a kiválasztási típust.
listBox.SelectionType = SelectionType.Single;
// Állítsa be a listamezőt 3D árnyékolással.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Ez a tulajdonság biztosítja, hogy a listamező a munkalap módosításától függetlenül a helyén maradjon.
- LinkedCell: Beállít egy cellát (ebben az esetben az A1-et), ahol a listából kiválasztott érték jelenik meg.
- InputRange: Ez megmondja a listamezőnek, hogy hol keresse az opciók listáját (A2-tól A7-ig, amit korábban beállítottunk).
- SelectionType.Single: Ez korlátozza a felhasználót, hogy csak egy elemet válasszon ki a listából.
- Árnyék: Az árnyékhatás háromdimenziósabb megjelenést kölcsönöz a listamezőnek, így vizuálisan is vonzó.
## 6. lépés: Mentse el az Excel fájlt
Végül mentsük el a munkafüzetünket a listával együtt.
```csharp
// Mentse el a munkafüzetet.
workbook.Save(dataDir + "book1.out.xls");
```
Ez a kódsor a munkafüzetet a korábban beállított könyvtárba menti. A fájl neve "book1.out.xls", de bármilyen nevet választhat, amely megfelel a projektnek.
## Következtetés
És megvan! Sikeresen hozzáadott egy listamezőt egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Néhány sornyi kóddal létrehoztunk egy teljesen működőképes listadobozt, amely interaktívabbá és dinamikusabbá tette a munkalapot. Ez az oktatóanyag szilárd alapot biztosít az Aspose.Cells for .NET egyéb vezérlőinek és funkcióinak felfedezéséhez. Folytasd a kísérletezést, és hamarosan elsajátítod a könyvtár hatalmas funkcióit!
## GYIK
### Engedélyezhetek több kijelölést a listamezőben?  
 Igen, megváltoztathatod a`SelectionType` hogy`SelectionType.Multi` több kijelölés engedélyezése.
### Módosíthatom a listamező megjelenését?  
Teljesen! Az Aspose.Cells lehetővé teszi a listamező kinézetének testreszabását, beleértve annak méretét, betűtípusát és színét is.
### Mi a teendő, ha később el kell távolítanom a listamezőt?  
 A listamezőt elérheti és eltávolíthatja a`Shapes` gyűjtés segítségével`sheet.Shapes.RemoveAt(index)`.
### Kapcsolhatom a listamezőt egy másik cellához?  
 Igen, egyszerűen változtassa meg a`LinkedCell` tulajdonság bármely másik cellába, ahol meg szeretné jeleníteni a kiválasztott értéket.
### Hogyan adhatok hozzá további elemeket a listamezőhöz?  
Csak frissítse a beviteli tartományt több érték beszúrásával a megadott cellákba, és a listamező automatikusan frissül.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
