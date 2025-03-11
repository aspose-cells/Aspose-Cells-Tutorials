---
title: Beépített számformátumok használata az Excel programban programozottan
linktitle: Beépített számformátumok használata az Excel programban programozottan
second_title: Aspose.Cells .NET Excel Processing API
description: Automatizálja a számformázást az Excelben az Aspose.Cells for .NET használatával. Ismerje meg a dátum-, százalék- és pénznemformátumok programozott alkalmazásának módját.
weight: 10
url: /hu/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Beépített számformátumok használata az Excel programban programozottan

## Bevezetés
Ebben az oktatóanyagban végigvezetjük, hogyan használhatja a beépített számformátumokat az Excelben az Aspose.Cells for .NET használatával. A környezet beállításától a különböző formátumok, például dátumok, százalékok és pénznemek alkalmazásáig mindenre kiterjedünk. Akár tapasztalt profi, akár csak belemerül a .NET-ökoszisztémába, ez az útmutató segít az Excel-cellák gyors formázására.
## Előfeltételek
Búvárkodás előtt győződjön meg arról, hogy rendelkezik az alábbiakkal:
-  Aspose.Cells for .NET könyvtár telepítve. Tudod[töltse le itt](https://releases.aspose.com/cells/net/).
- C# és alapvető .NET programozási ismeretek.
- Visual Studio vagy bármely, a gépére telepített .NET IDE.
-  Érvényes Aspose jogosítvány ill[ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
- .NET-keretrendszer telepítve (4.0-s vagy újabb verzió).
  
Ha a fentiek közül bármelyik hiányzik, kövesse a mellékelt hivatkozásokat az összes beállításához. Kész? Ugorjunk a mókás részbe!
## Csomagok importálása
Mielőtt elkezdené az oktatóanyagot, feltétlenül importálja az Aspose.Cells for .NET-hez szükséges névtereket:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Miután ezeket importálta, készen áll az Excel-fájlok programozott kezelésére. Most pedig merüljünk el a lépésről lépésre szóló útmutatóban!
## 1. lépés: Az Excel-munkafüzet létrehozása vagy elérése
Ebben a lépésben új munkafüzetet hoz létre. Tekintsd ezt úgy, mint egy új Excel-fájl megnyitását, kivéve, hogy ezt kódon keresztül csinálod!
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Munkafüzet objektum példányosítása
Workbook workbook = new Workbook();
```
 Itt egyszerűen létrehozunk egy újat`Workbook` objektum. Ez Excel-fájlként működik, készen áll az adatok manipulálására. Meglévő fájlt is betölthet az elérési út megadásával.
## 2. lépés: Nyissa meg a munkalapot
Az Excel-munkafüzetek több munkalapot is tartalmazhatnak. Ebben a lépésben elérjük a munkafüzet első munkalapját:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Most elérjük a munkafüzet első munkalapját. Ha további lapokat kell kezelnie, hivatkozhat rájuk indexük vagy nevük használatával.
## 3. lépés: Adjon hozzá adatokat a cellákhoz
Kezdjük el néhány adat hozzáadását bizonyos cellákhoz. Először beszúrjuk az aktuális rendszerdátumot az "A1" cellába:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Ez a sor beszúrja az aktuális dátumot az A1 cellába. Nagyon klassz, igaz? Képzeld el, hogy ezt manuálisan csinálod több száz cellánál – rémálom lenne. Most pedig térjünk át a formázásra!
## 4. lépés: Dátum formázása az "A1" cellában
Ezután formázza a dátumot egy olvashatóbb formátumban, például "október 15-24". Itt ragyog igazán az Aspose.Cells:
1. A cella stílusának lekérése:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Itt az A1 cella stílusát ragadjuk meg. Tekintsd ezt úgy, mintha megragadnád a cella "divatját", mielőtt bármilyen módosítást végeznél.
2. Állítsa be a dátumformátumot:
```csharp
style.Number = 15;
```
 Beállítása a`Number` tulajdonság a 15-re alkalmazza a kívánt dátumformátumot. Ez egy beépített számformátumú kód a dátumok "d-hh-éé" formátumú megjelenítéséhez.
3. Alkalmazza a stílust a cellára:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Ez a sor alkalmazza a stílusmódosításokat a cellára. Mostantól az alapértelmezett dátumformátum helyett valami sokkal felhasználóbarátabbat fog látni, például „15-október 24.”.
## 5. lépés: Százalék hozzáadása és formázása az "A2" cellában
Térjünk át a százalékok formázására. Képzelje el, hogy be szeretne szúrni egy értéket, és százalékban szeretné megjeleníteni. Ebben a lépésben hozzáadunk egy számértéket az "A2" cellához, és százalékos formában formázzuk:
1. Numerikus érték beszúrása:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Ezzel beszúrja a 20-as számot az A2 cellába. Lehet, hogy azt gondolja: "Ez csak egy sima szám – hogyan alakítsam át százalékra?" Nos, mindjárt eljutunk odáig.
2. Töltse le a stílust, és állítsa be a százalékos formátumot:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formázás százalékban
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Itt hozzáadjuk a 2546-ot az A3 cellához. Ezután ezt a számot úgy formázzuk, hogy pénznemként jelenjen meg.
2. Töltse le a stílust és állítsa be a pénznemformátumot:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formátum pénznemként
worksheet.Cells["A3"].SetStyle(style);
```
 Beállítása a`Number` A 6-os tulajdonság a pénznemformátumot alkalmazza. Most az A3 cellában lévő érték "2546,00" lesz, vesszővel és két tizedesjegygel kiegészítve.
## 7. lépés: Mentse el az Excel fájlt
Most, hogy alkalmaztuk az összes formázási varázslatot, ideje elmenteni a fájlt:
```csharp
// Az Excel fájl mentése
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 Ez a sor az Excel fájlt Excel 97-2003 formátumban menti. Meg tudod változtatni a`SaveFormat`hogy megfeleljen az Ön igényeinek. És éppen így, Ön programozottan hozott létre és formázott egy Excel-fájlt!
## Következtetés
Gratulálok! Sikeresen megtanulta az Aspose.Cells for .NET használatát, amellyel beépített számformátumokat alkalmazhat egy Excel-fájl celláiban. A dátumoktól a százalékokig és a pénznemekig lefedtük az Excel adatfeldolgozás leggyakoribb formázási igényeit. Mostantól a cellák kézi formázása helyett automatizálhatja a teljes folyamatot, így időt takaríthat meg és csökkenti a hibákat.
## GYIK
### Alkalmazhatok egyéni számformátumokat az Aspose.Cells for .NET használatával?
 Igen! A beépített formátumok mellett az Aspose.Cells támogatja az egyéni számformátumokat is. A segítségével nagyon specifikus formátumokat hozhat létre`Custom` ingatlan a`Style` osztály.
### Hogyan formázhatok egy cellát pénznemként egy adott szimbólummal?
 Egy adott pénznemszimbólum alkalmazásához egyéni formázást használhat a`Style.Custom` ingatlan.
### Formázhatok teljes sorokat vagy oszlopokat?
 Teljesen! A stílusokat egész sorokra vagy oszlopokra alkalmazhatja a`Rows` vagy`Columns`gyűjtemények a`Worksheet` objektum.
### Hogyan formázhatok egyszerre több cellát?
Használhatja a`Range` objektumot több cella kijelöléséhez és stílusok alkalmazásához egyszerre.
### Az Aspose.Cells használatához telepíteni kell a Microsoft Excelt?
Nem, az Aspose.Cells a Microsoft Exceltől függetlenül működik, így nincs szükség az Excel telepítésére a gépére.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
