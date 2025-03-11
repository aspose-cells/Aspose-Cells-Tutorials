---
title: Adja hozzá a kombinált mezőt az Excel munkalapjához
linktitle: Adja hozzá a kombinált mezőt az Excel munkalapjához
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat programozottan kombinált mezőt egy Excel-munkalaphoz az Aspose.Cells for .NET használatával. Ez a lépésről lépésre végigvezeti Önt minden részleten.
weight: 21
url: /hu/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adja hozzá a kombinált mezőt az Excel munkalapjához

## Bevezetés
Interaktív Excel-táblázatok létrehozása nagymértékben javíthatja a felhasználói élményt, különösen akkor, ha űrlapelemeket, például kombinált dobozokat ad hozzá. A kombinált mezők lehetővé teszik a felhasználók számára, hogy egy előre meghatározott listából válasszon opciókat, megkönnyítve és hatékonyabbá téve az adatbevitelt. Az Aspose.Cells for .NET segítségével programozottan hozhat létre kombinált mezőket Excel-lapokon anélkül, hogy közvetlenül az Excelt használná. Ez a hatékony könyvtár lehetővé teszi a fejlesztők számára, hogy különféle módokon kezeljék az Excel fájlokat, beleértve az űrlapvezérlők automatizálásának lehetőségét is.
Ebben az oktatóanyagban végigvezetjük a kombinált mező hozzáadásának folyamatán az Excel munkalapjaihoz az Aspose.Cells for .NET használatával. Ha dinamikus, felhasználóbarát táblázatokat szeretne készíteni, ez az útmutató segít az indulásban.
## Előfeltételek
Mielőtt belemerülnénk a kódba, győződjön meg arról, hogy mindennel rendelkezik, amire szüksége van:
- Aspose.Cells for .NET: Töltse le és telepítse az Aspose.Cells for .NET könyvtárat a[letöltési oldal](https://releases.aspose.com/cells/net/).
- .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a számítógépen. Az Aspose.Cells által támogatott bármely verzió működik.
- Fejlesztési környezet: Használjon olyan IDE-t, mint a Visual Studio a projekt kezeléséhez és a kód írásához.
-  Aspose Licenc: Kiértékelési módban licenc nélkül is dolgozhat, de a teljes verzióhoz licencet kell kérnie. Szerezzen be a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) ha szükséges.
## Csomagok importálása
A kezdéshez importálnia kell a szükséges névtereket a projektbe. Íme, amire szüksége van:
```csharp
using System.IO;
using Aspose.Cells;
```
Ezek elengedhetetlenek az Excel-fájlokkal való interakcióhoz és az űrlapelemek, például a munkafüzet kombinált mezőinek kezeléséhez.
Bontsuk le a kombinált mező hozzáadásának folyamatát több egyszerű lépésre a könnyebb érthetőség érdekében.
## 1. lépés: Állítsa be a dokumentumkönyvtárat
Az első lépés az, hogy hozzon létre egy könyvtárat, ahová az Excel fájlokat menti. Létrehozhat egy új mappát, ha még nem létezik.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Megadja azt a helyet, ahová a kimeneti fájl mentésre kerül.
- System.IO.Directory.Exists: Ellenőrzi, hogy a könyvtár létezik-e már.
- System.IO.Directory.CreateDirectory: Létrehozza a könyvtárat, ha hiányzik.
## 2. lépés: Hozzon létre egy új munkafüzetet
Most hozzon létre egy új Excel-munkafüzetet, amelyhez hozzáadja a kombinált mezőt.

```csharp
// Hozzon létre egy új munkafüzetet.
Workbook workbook = new Workbook();
```

- Munkafüzet-munkafüzet: Inicializálja a Munkafüzet osztály új példányát, amely egy Excel-fájlt képvisel.
## 3. lépés: Szerezze be a munkalapot és a cellákat
Ezután nyissa meg az első munkalapot a munkafüzetből, és kérje le a cellagyűjteményt, amelybe adatokat fog bevinni.

```csharp
// Szerezd meg az első munkalapot.
Worksheet sheet = workbook.Worksheets[0];
// Szerezze be a munkalap cellagyűjteményét.
Cells cells = sheet.Cells;
```

- Munkalap lap: lekéri az első munkalapot a munkafüzetből.
- Cellák cellák: Lekéri a cellák gyűjteményét a munkalapról.
## 4. lépés: Adja meg a Combo Box értékeit
Most néhány értéket kell beírnunk a cellákba. Ezek az értékek a kombinált doboz opcióiként fognak szolgálni.

```csharp
// Adjon meg egy értéket.
cells["B3"].PutValue("Employee:");
// Állítsa félkövérre.
cells["B3"].GetStyle().Font.IsBold = true;
// Adjon meg néhány értéket, amelyek a kombinált doboz beviteli tartományát jelölik.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- sejteket["B3"].PutValue: A B3 cellába helyezi az "Employee" címkét.
- Font.IsBold = true: A szöveget félkövérre állítja, hogy kiemelkedjen.
- Beviteli tartomány: Több alkalmazotti azonosítót ír be az A2-A7 cellákba. Ezek a legördülő listában jelennek meg.
## 5. lépés: Adja hozzá a kombinált mezőt a munkalaphoz
A következő lépés a kombinált vezérlőelem hozzáadása a munkalaphoz. Ezzel a kombinált mezővel a felhasználók kiválaszthatják a korábban megadott alkalmazotti azonosítók egyikét.

```csharp
// Új kombinált mező hozzáadása.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Új kombinált mezőt ad a munkalaphoz. A számok (2, 0, 2, 0, 22, 100) a kombinált doboz helyzetét és méreteit jelzik.
## 6. lépés: Kapcsolja össze a kombinált dobozt egy cellával, és állítsa be a beviteli tartományt
Ahhoz, hogy a kombinált doboz működőképes legyen, egy adott cellához kell kapcsolnunk, és meg kell határoznunk a cellák tartományát, ahonnan a beállításokat lekéri.

```csharp
// Állítsa be a csatolt cellát.
comboBox.LinkedCell = "A1";
// Állítsa be a beviteli tartományt.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: A kombinált mező kijelölését az A1 cellához kapcsolja. Ebben a cellában fog megjelenni a kombinált mezőből kiválasztott érték.
- InputRange: Meghatározza a cellatartományt (A2:A7), amely tartalmazza azokat az értékeket, amelyek feltöltik a kombinált mező beállításait.
## 7. lépés: A kombinált doboz megjelenésének testreszabása
Tovább szabhatja a kombinált mezőt a legördülő sorok számának megadásával és a 3D árnyékolás engedélyezésével a jobb esztétikai megjelenés érdekében.

```csharp
// készlet sz. a kombinált mező listarészében megjelenő listasorok közül.
comboBox.DropDownLines = 5;
// Állítsa be a kombinált mezőt 3D árnyékolással.
comboBox.Shadow = true;
```

- DropDownLines: Azt szabályozza, hogy egyszerre hány opció legyen látható a kombinált mező legördülő menüjében.
- Árnyék: 3D-s árnyékolási effektust ad a kombinált dobozhoz.
## 8. lépés: Oszlopok automatikus illesztése és a munkafüzet mentése
Végül illesszük be automatikusan az oszlopokat a tiszta elrendezés érdekében, és mentsük el a munkafüzetet.

```csharp
// Oszlopok automatikus illeszkedése
sheet.AutoFitColumns();
// Menti a fájlt.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Automatikusan beállítja az oszlopszélességet, hogy illeszkedjen a tartalomhoz.
- Mentés: A munkafüzetet Excel-fájlként menti a megadott könyvtárba.

## Következtetés
kombinált mező hozzáadása az Excel-munkalapokhoz az Aspose.Cells for .NET használatával egyszerű folyamat, amely nagymértékben javítja az adatbeviteli rugalmasságot. Az űrlapvezérlők programozott létrehozásával könnyedén készíthet interaktív táblázatokat. Ez az oktatóanyag bemutatja, hogyan adhat hozzá kombinált mezőt, hogyan kapcsolhatja össze egy cellával, és hogyan konfigurálhatja a beviteli tartományát, mindezt az Aspose.Cells használatával.
 Az Aspose.Cells funkciók széles skáláját kínálja az Excel-fájlok kezeléséhez, így ideális választás a táblázatkezelési feladatokat automatizálni kívánó fejlesztők számára. Próbáld ki a[ingyenes próbaverzió](https://releases.aspose.com/).
## GYIK
### Használhatom az Aspose.Cells programot Excel telepítése nélkül?
Igen, az Aspose.Cells az Exceltől függetlenül működik, és nem szükséges az Excel telepítése.
### Hogyan kérhetek licencet az Aspose.Cellsben?
 Az engedélyt azáltal kérheti, hogy megszerzi[itt](https://purchase.aspose.com/buy) és hív`License.SetLicense()` a kódodban.
### Milyen formátumokat támogat az Aspose.Cells a fájlok mentéséhez?
Az Aspose.Cells támogatja a fájlok többféle formátumban, például XLSX, XLS, CSV, PDF stb.
### Korlátozott a hozzáadható kombinált dobozok száma?
Nem, nincs szigorú korlát; annyi kombinált mezőt adhat hozzá, amennyit a projekt megkövetel.
### Hogyan kaphatok támogatást az Aspose.Cells-hez?
 Támogatást kaphat a[Aspose fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
