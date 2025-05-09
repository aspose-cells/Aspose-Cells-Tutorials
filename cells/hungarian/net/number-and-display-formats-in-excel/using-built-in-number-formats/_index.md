---
"description": "Automatizálja a számformázást az Excelben az Aspose.Cells for .NET használatával. Ismerje meg, hogyan alkalmazhat programozottan dátum-, százalék- és pénznemformátumokat."
"linktitle": "Beépített számformátumok használata az Excelben programozottan"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Beépített számformátumok használata az Excelben programozottan"
"url": "/hu/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Beépített számformátumok használata az Excelben programozottan

## Bevezetés
Ebben az oktatóanyagban bemutatjuk, hogyan használhatod a beépített számformátumokat az Excelben az Aspose.Cells for .NET segítségével. Mindent lefedünk a környezet beállításától kezdve a különböző formátumok, például dátumok, százalékok és pénznemek alkalmazásáig. Akár tapasztalt profi vagy, akár csak most ismerkedsz a .NET ökoszisztémával, ezzel az útmutatóval gyerekjáték lesz formázni az Excel cellákat.
## Előfeltételek
Mielőtt belevágnál, győződj meg róla, hogy a következőkkel rendelkezel:
- Aspose.Cells for .NET könyvtár telepítve van. Megteheti [töltsd le itt](https://releases.aspose.com/cells/net/).
- C# és alapvető .NET programozási ismeretek.
- Visual Studio vagy bármilyen, a gépedre telepített .NET IDE.
- Érvényes Aspose licenc vagy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
- Telepített .NET keretrendszer (4.0-s vagy újabb verzió).
  
Ha a fentiek közül bármelyik hiányzik, kövesd a megadott linkeket a beállításhoz. Készen állsz? Kezdjük a mókás részt!
## Csomagok importálása
Mielőtt belekezdenénk az oktatóanyagba, importáljuk a szükséges névtereket az Aspose.Cells for .NET használatához:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Miután importáltad ezeket, máris elkezdheted programozottan kezelni az Excel-fájlokat. Most pedig lássuk a lépésről lépésre bemutatót!
## 1. lépés: Excel-munkafüzet létrehozása vagy elérése
Ebben a lépésben egy új munkafüzetet fogsz létrehozni. Gondolj erre úgy, mintha egy új Excel fájlt nyitnál meg, azzal a különbséggel, hogy kódon keresztül csinálod!
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozz létre egy könyvtárat, ha az még nem létezik.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Workbook objektum példányosítása
Workbook workbook = new Workbook();
```
Itt egyszerűen csak egy új példányt hozunk létre `Workbook` objektum. Ez az Ön Excel-fájljaként működik, készen áll az adatkezelésre. Egy meglévő fájlt is betölthet az elérési útjának megadásával.
## 2. lépés: A munkalap elérése
Az Excel-munkafüzetek több munkalapot is tartalmazhatnak. Ebben a lépésben a munkafüzet első munkalapját fogjuk elérni:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Most a munkafüzet első munkalapjához férünk hozzá. Ha további munkalapokat kell módosítania, hivatkozhat rájuk az indexük vagy a nevük használatával.
## 3. lépés: Adatok hozzáadása cellákhoz
Kezdjünk el adatokat hozzáadni bizonyos cellákhoz. Először is beillesztjük az aktuális rendszerdátumot az "A1" cellába:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Ez a sor beszúrja az aktuális dátumot az A1 cellába. Elég klassz, ugye? Képzeld el, hogy ezt manuálisan kell megtenned több száz cellán keresztül – rémálom lenne. Most pedig térjünk át a formázásra!
## 4. lépés: Dátum formázása az „A1” cellában
Ezután formázzuk a dátumot egy olvashatóbb formátumba, például „15-Okt-24”. Itt ragyog igazán az Aspose.Cells:
1. A cella stílusának lekérése:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Itt az A1 cella stílusát vesszük alapul. Gondoljon erre úgy, mintha a cella „stílusát” venné át, mielőtt bármilyen módosítást végezne.
2. Állítsa be a dátumformátumot:
```csharp
style.Number = 15;
```
A beállítás `Number` tulajdonság 15-re állítása a kívánt dátumformátumot alkalmazza. Ez egy beépített számformátum-kód a dátumok „n-hhh-éé” formátumban történő megjelenítéséhez.
3. Stílus alkalmazása a cellára:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Ez a sor alkalmazza a stílusmódosításokat a cellára. Most az alapértelmezett dátumformátum helyett valami sokkal felhasználóbarátabbat fog látni, például a „15-Okt-24.”-et.
## 5. lépés: Százalék hozzáadása és formázása az „A2” cellában
Térjünk át a százalékok formázására. Képzeljük el, hogy be szeretne szúrni egy értéket, és százalékként szeretné megjeleníteni. Ebben a lépésben egy numerikus értéket adunk az "A2" cellához, és százalékként formázzuk:
1. Numerikus érték beszúrása:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Ez a függvény a 20-as számot szúrja be az A2 cellába. Gondolhatja most: „Ez csak egy sima szám – hogyan alakítsam át százalékká?” Nos, mindjárt elérkezünk ehhez.
2. Stílus lekérése és százalékos formátum beállítása:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formátum százalékként
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Itt a 2546-ot adjuk hozzá az A3 cellához. Ezután formázzuk ezt a számot, hogy pénznemként jelenjen meg.
2. Stílus lekérése és pénznemformátum beállítása:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formátum pénznemként
worksheet.Cells["A3"].SetStyle(style);
```
A beállítás `Number` A 6-os értékű tulajdonság a pénznemformátumot alkalmazza. Az A3 cellában lévő érték most „2546,00” formában jelenik meg, vesszőkkel és két tizedesjegyre kiegészítve.
## 7. lépés: Mentse el az Excel-fájlt
Most, hogy minden formázási varázslatot alkalmaztunk, itt az ideje menteni a fájlt:
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Ez a sor Excel 97-2003 formátumban menti az Excel fájlt. A formátumot módosíthatja. `SaveFormat` az igényeidnek megfelelően. És ezzel máris létrehoztál és formáztál egy Excel fájlt programozottan!
## Következtetés
Gratulálunk! Sikeresen megtanultad, hogyan használhatod az Aspose.Cells for .NET programot beépített számformátumok alkalmazására egy Excel-fájl celláira. A dátumoktól a százalékokon át a pénznemekig áttekintettük az Excel adatfeldolgozás néhány leggyakoribb formázási igényét. Most a cellák manuális formázása helyett automatizálhatod a teljes folyamatot – így időt takaríthatsz meg és csökkentheted a hibákat.
## GYIK
### Alkalmazhatok egyéni számformátumokat az Aspose.Cells for .NET használatával?
Igen! A beépített formátumok mellett az Aspose.Cells egyéni számformátumokat is támogat. Nagyon specifikus formátumokat hozhat létre a `Custom` ingatlan a `Style` osztály.
### Hogyan formázhatok egy cellát pénznemként egy adott szimbólummal?
Egy adott pénznemszimbólum alkalmazásához egyéni formázást használhat a következő beállítással: `Style.Custom` ingatlan.
### Formázhatok teljes sorokat vagy oszlopokat?
Természetesen! Stílusokat alkalmazhatsz teljes sorokra vagy oszlopokra a `Rows` vagy `Columns` gyűjtemények a `Worksheet` objektum.
### Hogyan tudok egyszerre több cellát formázni?
Használhatod a `Range` objektummal több cellát kijelölhet, és egyszerre mindegyikre stílusokat alkalmazhat.
### Telepítenem kell a Microsoft Excelt az Aspose.Cells használatához?
Nem, az Aspose.Cells a Microsoft Exceltől függetlenül működik, így nincs szükség Excel telepítésére a gépeden.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}