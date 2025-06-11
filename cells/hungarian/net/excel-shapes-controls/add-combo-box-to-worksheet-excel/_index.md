---
"description": "Ismerje meg, hogyan adhat hozzá kombinált listát egy Excel-munkalaphoz programozott módon az Aspose.Cells for .NET használatával. Ez a lépésről lépésre szóló útmutató végigvezeti Önt minden részleten."
"linktitle": "Kombinált lista hozzáadása a munkalaphoz az Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Kombinált lista hozzáadása a munkalaphoz az Excelben"
"url": "/hu/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kombinált lista hozzáadása a munkalaphoz az Excelben

## Bevezetés
Az interaktív Excel-táblázatok létrehozása nagymértékben javíthatja a felhasználói élményt, különösen akkor, ha űrlapelemeket, például kombinált listákat ad hozzá. A kombinált listák lehetővé teszik a felhasználók számára, hogy egy előre definiált listából válasszanak opciókat, így egyszerűbbé és hatékonyabbá téve az adatbevitelt. Az Aspose.Cells for .NET segítségével programozottan hozhat létre kombinált listákat Excel-táblázatokban anélkül, hogy közvetlenül az Excelt használná. Ez a hatékony függvénytár lehetővé teszi a fejlesztők számára, hogy az Excel-fájlokat különféle módokon manipulálják, beleértve az űrlapvezérlők automatizálását is.
Ebben az oktatóanyagban végigvezetünk azon, hogyan adhatsz hozzá kombinált listát egy munkalaphoz Excelben az Aspose.Cells for .NET használatával. Ha dinamikus, felhasználóbarát táblázatokat szeretnél készíteni, ez az útmutató segít az indulásban.
## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjünk meg róla, hogy minden szükséges dolog megvan:
- Aspose.Cells .NET-hez: Töltse le és telepítse az Aspose.Cells .NET-hez könyvtárat a következő helyről: [letöltési oldal](https://releases.aspose.com/cells/net/).
- .NET-keretrendszer: Győződjön meg róla, hogy a .NET-keretrendszer telepítve van a gépén. Az Aspose.Cells által támogatott bármely verzió működni fog.
- Fejlesztői környezet: Használjon egy IDE-t, például a Visual Studio-t a projekt kezeléséhez és a kód írásához.
- Aspose licenc: Kiértékelési módban licenc nélkül is dolgozhatsz, de a teljes verzióhoz licencet kell igényelned. Szerezz be egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) ha szükséges.
## Csomagok importálása
A kezdéshez importálnia kell a szükséges névtereket a projektjébe. Íme, amire szüksége van:
```csharp
using System.IO;
using Aspose.Cells;
```
Ezek elengedhetetlenek az Excel-fájlokkal való interakcióhoz és az űrlapelemek, például a munkafüzet kombinált listájának kezeléséhez.
Bontsuk le a kombinált lista hozzáadásának folyamatát több egyszerű lépésre a könnyebb megértés érdekében.
## 1. lépés: A dokumentumkönyvtár beállítása
Az első lépés egy könyvtár létrehozása, ahová az Excel-fájlokat menteni fogja. Létrehozhat egy új mappát, ha még nem létezik.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Megadja a kimeneti fájl mentési helyét.
- System.IO.Directory.Exists: Ellenőrzi, hogy a könyvtár már létezik-e.
- System.IO.Directory.CreateDirectory: Létrehozza a hiányzó könyvtárat.
## 2. lépés: Új munkafüzet létrehozása
Most hozzon létre egy új Excel-munkafüzetet, ahová fel fogja venni a kombinált listát.

```csharp
// Hozz létre egy új munkafüzetet.
Workbook workbook = new Workbook();
```

- Munkafüzet munkafüzet: Inicializálja a Workbook osztály egy új példányát, amely egy Excel-fájlt jelöl.
## 3. lépés: Szerezd meg a munkalapot és a cellákat
Ezután nyissa meg a munkafüzet első munkalapját, és keresse meg a cellagyűjteményt, ahová adatokat fog beírni.

```csharp
// Szerezd meg az első munkalapot.
Worksheet sheet = workbook.Worksheets[0];
// Szerezd meg a munkalap celláinak gyűjteményét.
Cells cells = sheet.Cells;
```

- Munkalap: Kiválasztja az első munkalapot a munkafüzetből.
- Cells cells: A munkalap celláinak gyűjteményét adja vissza.
## 4. lépés: Értékek bevitele a kombinált listába
Most be kell írnunk néhány értéket a cellákba. Ezek az értékek opcióként szolgálnak majd a kombinált listában.

```csharp
// Adjon meg egy értéket.
cells["B3"].PutValue("Employee:");
// Állítsd be félkövér betűtípussal.
cells["B3"].GetStyle().Font.IsBold = true;
// Adjon meg néhány értéket, amelyek a kombinált lista beviteli tartományát jelölik.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: Az "Alkalmazott" címkét a B3 cellába helyezi.
- Font.IsBold = true: A szöveget félkövérre állítja, hogy kiemelkedjen.
- Beviteli tartomány: Több alkalmazotti azonosítót ad meg az A2-től A7-ig terjedő cellákban. Ezek megjelennek a kombinált lista legördülő menüjében.
## 5. lépés: A kombinált lista hozzáadása a munkalaphoz
A következő lépés a kombinált lista vezérlőelemének hozzáadása a munkalaphoz. Ez a kombinált lista lehetővé teszi a felhasználók számára, hogy kiválasszák a korábban megadott alkalmazotti azonosítók egyikét.

```csharp
// Új kombinált lista hozzáadása.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Új kombinált listát ad hozzá a munkalaphoz. A számok (2, 0, 2, 0, 22, 100) a kombinált lista helyét és méreteit jelölik.
## 6. lépés: Kombinált lista csatolása egy cellához és a beviteli tartomány beállítása
Ahhoz, hogy a kombinált lista működőképes legyen, össze kell kapcsolnunk egy adott cellával, és meg kell határoznunk azt a cellatartományt, amelyből a beállításokat kérni fogja.

```csharp
// Állítsa be a csatolt cellát.
comboBox.LinkedCell = "A1";
// Állítsa be a beviteli tartományt.
comboBox.InputRange = "A2:A7";
```

- KapcsoltCella: A kombinált listában kijelölt értéket az A1 cellához csatolja. A kombinált listából kiválasztott érték ebben a cellában fog megjelenni.
- Beviteli tartomány: Meghatározza a cellatartományt (A2:A7), amely a kombinált lista beállításait kitöltő értékeket tartalmazza.
## 7. lépés: A kombinált lista megjelenésének testreszabása
A kombinált listát tovább testreszabhatja a legördülő sorok számának megadásával és a 3D árnyékolás engedélyezésével a jobb esztétika érdekében.

```csharp
// Állítsa be a kombinált lista lista részében megjelenített lista sorok számát.
comboBox.DropDownLines = 5;
// Állítsa be a kombinált listát térhatású árnyékolással.
comboBox.Shadow = true;
```

- DropDownLines: Azt szabályozza, hogy egyszerre hány lehetőség legyen látható a kombinált lista legördülő menüjében.
- Árnyék: 3D árnyékolási effektust ad a kombinált listához.
## 8. lépés: Oszlopok automatikus illesztése és a munkafüzet mentése
Végül igazítsuk automatikusan az oszlopokat a tiszta elrendezés érdekében, és mentsük el a munkafüzetet.

```csharp
// Oszlopok automatikus illesztése
sheet.AutoFitColumns();
// Menti a fájlt.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Automatikusan beállítja az oszlopszélességet a tartalomhoz igazítva.
- Mentés: A munkafüzetet Excel-fájlként menti a megadott könyvtárba.

## Következtetés
Kombinált lista hozzáadása az Excel-munkafüzetekhez az Aspose.Cells for .NET használatával egy egyszerű folyamat, amely jelentősen javítja az adatbevitel rugalmasságát. Űrlapvezérlők programozott létrehozásával könnyedén készíthet interaktív táblázatokat. Ez az oktatóanyag bemutatta, hogyan adhat hozzá kombinált listát, hogyan csatolhatja azt egy cellához, és hogyan konfigurálhatja a beviteli tartományát, mindezt az Aspose.Cells használatával.
Az Aspose.Cells számos funkciót kínál az Excel fájlok kezeléséhez, így ideális választás azoknak a fejlesztőknek, akik automatizálni szeretnék a táblázatkezelési feladatokat. Próbálja ki egy... [ingyenes próba](https://releases.aspose.com/).
## GYIK
### Használhatom az Aspose.Cells-t Excel telepítése nélkül?
Igen, az Aspose.Cells az Exceltől függetlenül működik, és nem igényli az Excel telepítését.
### Hogyan igényelhetek licencet az Aspose.Cells-ben?
licencet úgy igényelheti, hogy megszerzi azt a következő helyről: [itt](https://purchase.aspose.com/buy) és hívás `License.SetLicense()` a kódodban.
### Milyen formátumokat támogat az Aspose.Cells a fájlok mentéséhez?
Az Aspose.Cells támogatja a fájlok mentését többféle formátumban, például XLSX, XLS, CSV, PDF és egyebekben.
### Van-e korlátozás a hozzáadható kombinált listák számára?
Nem, nincs szigorú korlátozás; annyi kombinált listát adhatsz hozzá, amennyit a projekted megkövetel.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
Támogatást kaphatsz a [Aspose fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}