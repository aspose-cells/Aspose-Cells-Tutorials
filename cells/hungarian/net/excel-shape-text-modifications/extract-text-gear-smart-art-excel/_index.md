---
title: Szöveg kibontása a Gear Type Smart Art programból az Excelben
linktitle: Szöveg kibontása a Gear Type Smart Art programból az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan bonthat ki szöveget fogaskerék-típusú SmartArtból az Excelben az Aspose.Cells for .NET használatával. Lépésről lépésre útmutató és kódpélda mellékelve.
weight: 10
url: /hu/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kibontása a Gear Type Smart Art programból az Excelben

## Bevezetés
Amikor Excellel dolgozik, találkozhat SmartArt grafikákkal, amelyek segítenek az üzenetek tetszetős közvetítésében. Ezen grafikák közül a fogaskerék-típusú SmartArt a kedvenc hierarchikus és irányított áramlásai miatt, amelyet gyakran használnak a projektmenedzsmentben vagy a rendszermodellezésben. De mi van akkor, ha programozottan kell szöveget kinyernie ezekből az alakzatokból? Itt jön jól az Aspose.Cells for .NET! Ebben a blogbejegyzésben lépésről lépésre bemutatjuk, hogyan vonhat ki szöveget fogaskerék-típusú SmartArt-alakzatokból az Excelben az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belemerülnénk, meg kell felelnie néhány alapvető előfeltételnek. Ne aggódj; egyszerű, és végigvezetem rajta.
### .NET környezet
Győződjön meg arról, hogy .NET fejlesztői környezet van beállítva a számítógépén. Ez lehet a Visual Studio vagy bármely tetszőleges IDE, amely támogatja a .NET fejlesztést.
### Aspose.Cells for .NET
 Ezután telepítenie kell az Aspose.Cells könyvtárat. Ez az erőmű, amely lehetővé teszi az Excel-fájlok zökkenőmentes kezelését. Letöltheti a[Aspose Releases oldal](https://releases.aspose.com/cells/net/) . Ha először szeretné felfedezni, használja ki a[ingyenes próbaverzió](https://releases.aspose.com/).
### C# alapismeretek
A C# programozás alapvető ismerete az, amit ehhez az oktatóanyaghoz követnie kell. Ha még nem ismeri, ne aggódjon – a lépéseket úgy fogom megtervezni, hogy azok a lehető legkezdőbarátabbak legyenek.
### Minta Excel fájl
Ehhez az oktatóanyaghoz egy minta Excel-fájlra is szüksége lesz, amely fogaskerék-típusú SmartArt-alakzatokat tartalmaz. Könnyen létrehozhat egyet, vagy kereshet sablont az interneten. Csak győződjön meg arról, hogy a SmartArt tartalmaz legalább egy fogaskerék típusú alakzatot.
## Csomagok importálása
A kódolás megkezdéséhez importálnia kell a szükséges csomagokat. Íme, hogyan kell csinálni:
### Hozzon létre egy új projektet
1. Nyissa meg a .NET IDE-jét.
2. Hozzon létre egy új projektet. Például válassza ki a „Konzolalkalmazás” lehetőséget a .NET beállításainál.
3. Adjon nevet a projektjének, és állítsa be a kívánt keretet. 
### Referenciák hozzáadása
Az Aspose.Cells használatához hozzá kell adnia a könyvtári hivatkozásokat a projekthez:
1. Kattintson a jobb gombbal a projekt nevére a Solution Explorerben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresse meg az "Aspose.Cells" kifejezést, és telepítse.
A telepítés után készen áll a kódolásra!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Most bontsuk fel a szöveg kibontásához használandó kódot. Ezt lépésről lépésre fogjuk megtenni.
## 1. lépés: Állítsa be a forráskönyvtárat
Kezdje azzal, hogy meghatározza azt a könyvtárat, amelyben az Excel fájl található:
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
```
 Mindenképpen cserélje ki`"Your Document Directory"` az Excel-fájl tényleges elérési útjával.
## 2. lépés: Töltse be az Excel-munkafüzetet
Ezután betöltjük az Excel munkafüzetet. Így érhetjük el a tartalmát:
```csharp
// Töltsön be egy minta Excel-fájlt, amely fogaskerék típusú smart art alakzatot tartalmaz.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Ez a darab betölti a minta Excel-munkafüzetet.
## 3. lépés: Nyissa meg az első munkalapot
Most, hogy betöltöttük a munkafüzetet, nyissuk meg az első munkalapot, ahol a SmartArt-unk létezik:
```csharp
// Az első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```
Ezzel lekéri az első munkalapot további manipuláció céljából.
## 4. lépés: Nyissa meg az első alakzatot
Ezután el kell érnünk az első alakzatot a munkalapunkon. Ezzel navigálhatunk a SmartArt grafikáink között:
```csharp
// Hozzáférés az első alakzathoz.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Itt az első alakzatra összpontosítunk, amelyről feltételezzük, hogy az a SmartArt, amelyre szükségünk van.
## 5. lépés: Szerezze meg a csoport alakját
Ha megvan az alakunk, itt az ideje, hogy megkapjuk a SmartArt ábrázolásunk eredményét:
```csharp
// Szerezze meg a fogaskerék típusú smart art alakzat eredményét csoportforma formájában.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Ez a fogaskerék-típusú SmartArt-ot csoportosított alakzatként kéri le.
## 6. lépés: Vonja ki az egyedi formákat
Most vegyük ki a SmartArt-ot alkotó egyedi alakzatokat:
```csharp
// Szerezze meg az egyéni alakzatok listáját, amely csoport alakzatokból áll.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Ez a tömb tartalmazza az összes egyedi alakzatot, amelyen át kell lépnünk.
## 7. lépés: Szöveg kibontása és nyomtatása
Végül végigpörgethetjük az alakzatok tömbjét, és kivonhatjuk a szöveget bármilyen fogaskerék típusú alakzatból:
```csharp
// Bontsa ki a fogaskerék típusú alakzatok szövegét, és nyomtassa ki őket a konzolra.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Ebben a ciklusban ellenőrizzük az alakzat típusát, és kinyomtatjuk a szöveget, ha fogaskerék típusú alakzatról van szó.
## 8. lépés: Végrehajtás megerősítése
Végül érdemes lehet egy megerősítő üzenetet hozzáadni a folyamat sikeres befejezése után:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Ezzel a kicsomagolás befejeződött, és látnia kell a szövegkimenetet a konzolban!
## Következtetés
 Gratulálok! Éppen most tanulta meg, hogyan bonthat ki szöveget fogaskerék-típusú SmartArt-alakzatokból az Excelben az Aspose.Cells for .NET használatával. Ez a praktikus technika lehetővé teszi a jelentések vagy dokumentációk automatizálását, amelyek a vizuális adatok megjelenítésére támaszkodnak. Akár tapasztalt fejlesztő, akár csak most kezdi, az információk ellenőrzése és kinyerése a SmartArtból leegyszerűsítheti a munkafolyamatot és hatékonyabbá teheti. Ne felejtse el megvizsgálni a részleteket[Aspose.Cells Documentation](https://reference.aspose.com/cells/net/) további képességekért.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET-könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-fájlok egyszerű létrehozását és kezelését.
### Használhatom az Aspose.Cells-t más nyelvekkel?
Igen! Az Aspose.Cells több programozási nyelven is elérhető, beleértve a Java-t és a Python-t.
### Meg kell vásárolnom az Aspose.Cells fájlt .NET-hez?
 Az Aspose.Cells ingyenes próbaverziót kínál, de a hosszabb használathoz vásárlás szükséges. Vásárlási lehetőségeket találhat[itt](https://purchase.aspose.com/buy).
### Van-e támogatás az Aspose.Cells felhasználók számára?
 Teljesen! A közösségi támogatást a[Aspose.Cells fórum](https://forum.aspose.com/c/cells/9).
### Kivonhatok más SmartArt-típusokat ezzel a módszerrel?
Igen, enyhe módosításokkal kivonhat szöveget a különböző SmartArt-alakzatokból a kód feltételeinek megváltoztatásával.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
