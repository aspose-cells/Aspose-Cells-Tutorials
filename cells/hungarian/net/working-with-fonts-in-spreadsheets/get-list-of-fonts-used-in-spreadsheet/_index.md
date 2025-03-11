---
title: Szerezze meg a táblázatban használt betűtípusok listáját
linktitle: Szerezze meg a táblázatban használt betűtípusok listáját
second_title: Aspose.Cells .NET Excel Processing API
description: Ezzel a könnyen követhető oktatóanyaggal megtudhatja, hogyan kérhet le és listázhat le betűtípusokat Excel-táblázatokból az Aspose.Cells for .NET segítségével.
weight: 10
url: /hu/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szerezze meg a táblázatban használt betűtípusok listáját

## Bevezetés
Előfordult már, hogy egy Excel-táblázatot görgetett, és azon töprengett, hogy milyen betűtípusokat használtak a különböző celláiban? Talán találkozott már egy régi dokumentummal, és szeretné tudni, milyen tipográfiai döntéseket hoztak? Nos, szerencséd van! Az Aspose.Cells for .NET segítségével olyan, mintha egy eszköztárral rendelkezne, amely lehetővé teszi a táblázatokban rejtett betűtípustitkok átvizsgálását és feltárását. Ebben az útmutatóban végigvezetjük, hogyan lehet egyszerűen lekérni az Excel-fájlban használt összes betűtípus listáját. Kapcsold be, és merüljünk el a táblázatok világában!
## Előfeltételek
Mielőtt belevágnánk a kódba, van néhány dolog, amit meg kell tennie a kezdéshez. Ne aggódj, ez nagyon egyszerű. Íme egy ellenőrző lista, amire szüksége van:
1. Visual Studio: Győződjön meg arról, hogy a Visual Studio egyik verziója telepítve van a gépen. Ide írjuk a kódunkat.
2. Aspose.Cells for .NET: Az Aspose.Cells könyvtárnak rendelkezésre kell állnia. Ha még nem töltötte le, letöltheti a[telek](https://releases.aspose.com/cells/net/).
3. Alapvető C# ismerete: A C# programozás egy kis megértése biztosan segít abban, hogy könnyen eligazodjon a kódban.
4. Minta Excel-fájl: A munkavégzéshez szüksége lesz egy minta Excel-fájlra, például a „sampleGetFonts.xlsx”-re. Itt alkalmazzuk a betűtípus-feltárásunkat.
Ha mindent összerakott, készen áll a kódolásra!
## Csomagok importálása
A dolgok elindításához importáljuk a szükséges névtereket. A .NET-ben a csomagok importálása olyan, mintha a megfelelő vendégeket hívná meg a buliba – nélkülük a dolgok nem működnek zökkenőmentesen.
A következőképpen importálhatja az Aspose.Cells fájlt:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Ezzel az egyszerű vonallal meghívjuk az Aspose.Cells alapvető funkcióit projektünkbe. Most pedig térjünk át a munkafüzet betöltésére.
## 1. lépés: Állítsa be a dokumentumkönyvtárat
Először is – mielőtt belemerülnénk a kódba, be kell állítania a dokumentumkönyvtár elérési útját. Itt található az Excel-fájl. 
```csharp
string dataDir = "Your Document Directory";
```
A „Saját dokumentumkönyvtár” helyére az Excel-fájl tényleges elérési útja lép. Gondolja ezt úgy, mintha azt mondaná a programnak: „Hé, itt rejtettem el az Excel fájlomat; menj és nézd meg!”
## 2. lépés: Töltse be a Forrás munkafüzetet
 Ideje betölteni az Excel fájlt. Új példányt hozunk létre a`Workbook` osztályt, és adja meg a fájl elérési útját. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Mi történik itt? Alapvetően megnyitjuk a táblázatunkat. A`Workbook` osztály lehetővé teszi számunkra, hogy kapcsolatba lépjünk az Excel fájl tartalmával. 
## 3. lépés: Töltse le az összes betűtípust
 Most jön a varázslatos pillanat – tulajdonképpen visszakeressük a betűtípusokat! A`GetFonts()` módszer az arany jegyünk.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Itt megkérjük a munkafüzetet, hogy ossza meg a benne használt összes betűtípust. A`fnts` tömb fogja tartani a kincseinket.
## 4. lépés: Nyomtassa ki a betűtípusokat
Végül vegyük ezeket a betűtípusokat és nyomtassuk ki őket. Ez segít ellenőrizni, hogy mit találtunk.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Ez a ciklus a mi minden betűtípuson keresztül fut`fnts` tömböt, egyenként kiadva őket a konzolra. Ez olyan, mintha megmutatná az összes remek tipográfiai lehetőséget az Excel-fájlban!
## Következtetés
És megvan! Néhány sornyi kóddal sikeresen lekérte és kinyomtatta az Excel-táblázatban használt betűtípusok listáját az Aspose.Cells for .NET segítségével. Ez nem csak a betűtípusokról szól; ez a dokumentumok finomságainak megértése, a prezentációk tökéletesítése és a táblázatok tipográfiai művészetének elsajátítása. Legyen szó fejlesztőről vagy valakiről, aki egyszerűen csak szeret az Excellel bütykölni, ez a kis részlet megváltoztathatja a játékot. 
## GYIK
### Az Aspose.Cells programot külön kell telepítenem?
Igen, le kell töltenie és hivatkoznia kell a könyvtárra a projektben. 
### Használhatom az Aspose.Cells-t más formátumokhoz?
Teljesen! Az Aspose.Cells többféle Excel formátummal működik, mint például az XLSX, XLS és CSV.
### Van ingyenes próbaverzió?
 Igen, megragadhat egy ingyenes próbaverziót a webhelyen[letöltési link](https://releases.aspose.com/).
### Hogyan kaphatok műszaki támogatást?
 Ha segítségre van szüksége, a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9) nagyszerű erőforrás.
### Az Aspose.Cells kompatibilis a .NET Core-al?
Igen, az Aspose.Cells a .NET Core projektekkel is kompatibilis.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
