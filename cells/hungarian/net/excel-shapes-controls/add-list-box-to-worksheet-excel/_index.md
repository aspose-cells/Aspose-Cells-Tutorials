---
"description": "Tanuld meg, hogyan adhatsz hozzá listát egy Excel-munkalaphoz az Aspose.Cells for .NET segítségével. Kövesd az egyszerű, lépésről lépésre haladó útmutatónkat, és tedd interaktívvá Excel-munkalapjaidat."
"linktitle": "Lista hozzáadása a munkalaphoz az Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Lista hozzáadása a munkalaphoz az Excelben"
"url": "/hu/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lista hozzáadása a munkalaphoz az Excelben

## Bevezetés
Interaktív elemek, például listák hozzáadása az Excel-munkafüzetekhez jelentősen javíthatja az adatkezelést és a megjelenítést. Akár interaktív űrlapot, akár egyéni adatbeviteli eszközt hoz létre, felbecsülhetetlen értékű a felhasználói bevitel listákkal történő vezérlésének lehetősége. Az Aspose.Cells for .NET hatékony módszert kínál ezeknek a vezérlőknek az Excel-fájlokban való hozzáadására és kezelésére. Ebben az útmutatóban végigvezetjük Önt egy lista munkalaphoz való hozzáadásának folyamatán az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belevágnál a kódolásba, győződj meg róla, hogy a következő eszközök és források a rendelkezésedre állnak:
- Aspose.Cells .NET könyvtárhoz: Letöltheti innen: [Aspose.Cells .NET letöltési oldal](https://releases.aspose.com/cells/net/).
- Fejlesztői környezet: Bármely .NET fejlesztést támogató IDE, például a Visual Studio.
- .NET-keretrendszer: Győződjön meg arról, hogy a projekt a .NET-keretrendszer egy támogatott verzióját célozza meg.
Fontolja meg azt is, hogy szerezzen be egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) ha korlátozás nélkül szeretnéd felfedezni az összes funkciót.
## Csomagok importálása
Mielőtt elkezdenéd, győződj meg róla, hogy importáltad a szükséges Aspose.Cells névtereket. Így teheted ezt meg:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Ebben az oktatóanyagban több egyszerű lépésre bontjuk a listamező hozzáadásának folyamatát. Kövesd gondosan az egyes lépéseket, hogy minden a várt módon működjön.
## 1. lépés: A dokumentumkönyvtár beállítása
Mielőtt bármilyen Excel-fájlt létrehozna, meg kell adnia egy helyet, ahová mentheti azt. A könyvtár beállításának módja:
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ebben a lépésben meghatározod, hogy hol tárolja a fájlodat. A kód ellenőrzi, hogy létezik-e a könyvtár, és ha nem, akkor létrehoz egyet. Ez biztosítja, hogy később ne kerülj szembe a „fájl nem található” hibákkal.
## 2. lépés: Új munkafüzet létrehozása és az első munkalap elérése
Ezután létrehozunk egy új munkafüzetet, és megnyitjuk az első munkalapot, ahová felvesszük a listánkat.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook workbook = new Workbook();
// Szerezd meg az első munkalapot.
Worksheet sheet = workbook.Worksheets[0];
```
A munkafüzet lényegében egy Excel-fájl. Itt egy új munkafüzetet hozunk létre, és megnyitjuk az első munkalapot, ahová a listánkat helyezzük. Gondoljon erre úgy, mintha egy üres vászon lenne, ahová a vezérlőket fogjuk festeni.
## 3. lépés: Adatok bevitele a listamezőbe
Mielőtt hozzáadnánk a listát, ki kell töltenünk néhány adatot, amelyekre a lista hivatkozni fog.
```csharp
// Szerezd meg a munkalap celláinak gyűjteményét.
Cells cells = sheet.Cells;
// Adjon meg egy értéket a címkéhez.
cells["B3"].PutValue("Choose Dept:");
// Állítsd a címkét félkövérre.
cells["B3"].GetStyle().Font.IsBold = true;
// Adja meg a lista értékeit.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Itt szöveget adunk a munkalaphoz. A „Choose Dept:” felirat a B3 cellában található, félkövér betűtípussal. Az A oszlopba olyan értékeket illesztünk be, amelyek a lista beviteli tartományaként szolgálnak majd, és a különböző részlegeket jelképezik. A felhasználók ebből a beviteli tartományból választhatnak, amikor a listamezővel interakcióba lépnek.
## 4. lépés: Lista hozzáadása a munkalaphoz
Most, hogy beállítottuk az adatokat, adjuk hozzá magát a listamező vezérlőelemet.
```csharp
// Új lista hozzáadása.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Ez a kód hozzáadja a listát a munkalaphoz. A paraméterek határozzák meg a lista helyét és méretét. A lista a 2. sor 0. oszlopában található, 122 szélességgel és 100 magassággal. Ezek a koordináták és a méret határozzák meg, hogy a lista hol fog megjelenni a munkalapon.
## 5. lépés: Lista tulajdonságainak beállítása
Ezután beállítjuk a listamező különböző tulajdonságait, hogy az teljesen működőképes legyen.
```csharp
// Állítsa be az elhelyezés típusát.
listBox.Placement = PlacementType.FreeFloating;
// Állítsa be a csatolt cellát.
listBox.LinkedCell = "A1";
// Állítsa be a beviteli tartományt.
listBox.InputRange = "A2:A7";
// Állítsa be a kijelölés típusát.
listBox.SelectionType = SelectionType.Single;
// Állítsa be a listamezőt térhatású árnyékolással.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Ez a tulajdonság biztosítja, hogy a lista a helyén maradjon, függetlenül attól, hogy hogyan módosul a munkalap.
- LinkedCell: Ez beállít egy cellát (jelen esetben az A1-et), ahol a listából kiválasztott érték megjelenik.
- InputRange: Ez határozza meg a listának, hogy hol keresse a lehetőségek listáját (A2-től A7-ig, amelyeket korábban beállítottunk).
- SelectionType.Single: Ez a felhasználót arra korlátozza, hogy csak egyetlen elemet válasszon ki a listából.
- Árnyék: Az árnyékeffektus háromdimenziósabb megjelenést kölcsönöz a listának, így vizuálisan vonzóbbá teszi azt.
## 6. lépés: Mentse el az Excel-fájlt
Végül mentsük el a munkafüzetünket a listával együtt.
```csharp
// Mentse el a munkafüzetet.
workbook.Save(dataDir + "book1.out.xls");
```
Ez a kódsor a korábban létrehozott könyvtárba menti a munkafüzetet. A fájl neve "book1.out.xls", de bármilyen nevet választhat, amely illik a projekthez.
## Következtetés
És íme! Sikeresen hozzáadtál egy listát egy Excel munkalaphoz az Aspose.Cells for .NET segítségével. Mindössze néhány sornyi kóddal létrehoztunk egy teljes funkcionalitású listát, így a munkalap interaktívabb és dinamikusabb lett. Ez az oktatóanyag szilárd alapot nyújt ahhoz, hogy felfedezd az Aspose.Cells for .NET egyéb vezérlőit és funkcióit. Kísérletezz tovább, és hamarosan elsajátítod a könyvtár hatalmas funkcionalitását!
## GYIK
### Engedélyezhetek több kijelölést a listában?  
Igen, megváltoztathatja a `SelectionType` hogy `SelectionType.Multi` hogy több kijelölés is lehetséges legyen.
### Meg lehet változtatni a lista megjelenését?  
Abszolút! Az Aspose.Cells lehetővé teszi a listadoboz megjelenésének testreszabását, beleértve a méretét, betűtípusát és akár a színét is.
### Mi van, ha később el kell távolítanom a listát?  
A listát elérheti és eltávolíthatja a `Shapes` gyűjtemény felhasználásával `sheet.Shapes.RemoveAt(index)`.
### Összekapcsolhatom a listát egy másik cellával?  
Igen, egyszerűen változtasd meg a `LinkedCell` tulajdonságot bármely más cellába, ahol a kiválasztott értéket meg szeretné jeleníteni.
### Hogyan adhatok hozzá további elemeket a listához?  
Egyszerűen frissítse a beviteli tartományt további értékek beszúrásával a megadott cellákba, és a lista automatikusan frissül.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}