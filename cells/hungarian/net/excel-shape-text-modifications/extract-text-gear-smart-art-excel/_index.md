---
"description": "Tanuld meg, hogyan kinyerhetsz szöveget fogaskerék típusú SmartArt-ábrákból Excelben az Aspose.Cells for .NET használatával. Lépésről lépésre útmutató és kódpélda is mellékelve."
"linktitle": "Szöveg kinyerése a Gear Type Smart Artból Excelben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Szöveg kinyerése a Gear Type Smart Artból Excelben"
"url": "/hu/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése a Gear Type Smart Artból Excelben

## Bevezetés
Az Excel használata során előfordulhat, hogy olyan SmartArt grafikákkal találkozunk, amelyek segítenek vizuálisan vonzó módon közvetíteni az üzeneteket. Ezen grafikák közül a fogaskerék típusú SmartArt a kedvenc a hierarchikus és irányított folyamatai miatt, amelyet gyakran használnak a projektmenedzsmentben vagy a rendszermodellezésben. De mi van akkor, ha programozottan kell szöveget kinyerni ezekből az alakzatokból? Itt jön jól az Aspose.Cells for .NET! Ebben a blogbejegyzésben lépésről lépésre bemutatjuk, hogyan lehet szöveget kinyerni fogaskerék típusú SmartArt alakzatokból Excelben az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belevágnánk, van néhány alapvető előfeltétel, aminek teljesülnie kell. Ne aggódj, egyszerű, és én végigvezetlek rajta.
### .NET környezet
Győződjön meg róla, hogy van beállítva egy .NET fejlesztői környezet a számítógépén. Ez lehet a Visual Studio vagy bármilyen más választott IDE, amely támogatja a .NET fejlesztést.
### Aspose.Cells .NET-hez
Ezután telepítened kell az Aspose.Cells könyvtárat. Ez az az erőmű, amely lehetővé teszi az Excel fájlok zökkenőmentes kezelését. Letöltheted innen: [Aspose Kiadások oldal](https://releases.aspose.com/cells/net/)Ha először szeretnéd felfedezni, használd ki a [ingyenes próba](https://releases.aspose.com/).
### C# alapismeretek
A C# programozás alapvető ismereteire van szükséged ehhez az oktatóanyaghoz. Ha még új vagy, ne aggódj – a lépéseket a lehető legkezdőbarátabb módon tervezem meg.
### Minta Excel-fájl
Ehhez az oktatóanyaghoz szükséged lesz egy minta Excel fájlra is, amely fogaskerék típusú SmartArt alakzatokat tartalmaz. Könnyen létrehozhatsz egyet, vagy találhatsz egy sablont online. Csak győződj meg róla, hogy a SmartArt legalább egy fogaskerék típusú alakzatot tartalmaz.
## Csomagok importálása
A kódolás megkezdéséhez importálnia kell a szükséges csomagokat. Így teheti meg:
### Új projekt létrehozása
1. Nyisd meg a .NET IDE-t.
2. Hozz létre egy új projektet. Például válaszd a „Konzolalkalmazás” lehetőséget a .NET beállítások alatt.
3. Adj nevet a projektednek, és állítsd be a kívánt keretrendszert. 
### Referenciák hozzáadása
Az Aspose.Cells használatához hozzá kell adnia a könyvtárhivatkozásokat a projekthez:
1. Kattintson jobb gombbal a projekt nevére a Megoldáskezelőben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresd meg az „Aspose.Cells” fájlt, és telepítsd.
Telepítés után máris készen állsz a kódolásra!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Most pedig bontsuk le a szöveg kinyeréséhez használt kódot. Lépésről lépésre fogjuk megtenni.
## 1. lépés: A forráskönyvtár beállítása
Kezd azzal, hogy meghatározzuk azt a könyvtárat, ahol az Excel fájl található:
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";
```
Mindenképpen cserélje ki `"Your Document Directory"` az Excel-fájl tényleges elérési útjával.
## 2. lépés: Töltse be az Excel-munkafüzetet
Ezután betöltjük az Excel munkafüzetet. Így férhetünk hozzá a tartalmához:
```csharp
// Fogaskerék típusú Smart Art alakzatot tartalmazó minta Excel fájl betöltése.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Ez a rész betölti a minta Excel-munkafüzetet.
## 3. lépés: Az első munkalap elérése
Most, hogy betöltöttük a munkafüzetet, nyissuk meg az első munkalapot, ahol a SmartArt-ábra található:
```csharp
// Első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```
Ez visszaállítja az első munkalapot a további szerkesztéshez.
## 4. lépés: Az első alakzat elérése
Ezután el kell érnünk a munkalapunk első alakzatát. Ezzel navigálhatunk a SmartArt-grafikák között:
```csharp
// Első alakzat elérése.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Itt az első alakzatra koncentrálunk, amelyről feltételezzük, hogy a szükséges SmartArt-ábra.
## 5. lépés: A csoport alakjának meghatározása
Miután megvan az alakzat, itt az ideje, hogy megkapjuk a SmartArt-ábrázolásunk eredményét:
```csharp
// Szerezd meg a fogaskerék típusú intelligens művészeti alakzat eredményét csoportos alakzat formájában.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Ez csoportosított alakzatként kéri le a fogaskerék típusú SmartArt-ábrát.
## 6. lépés: Egyedi alakzatok kinyerése
Most pedig vonjuk ki az SmartArt-ábránkat alkotó egyes alakzatokat:
```csharp
// Szerezd meg a csoportos alakzatból álló egyedi alakzatok listáját.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Ez a tömb fogja tartalmazni az összes egyedi alakzatot, amelyeken végig kell mennünk.
## 7. lépés: Szöveg kinyerése és nyomtatása
Végül végigpörgethetjük a shapes tömbünket, és kinyerhetjük a szöveget bármely fogaskerék típusú alakzatból:
```csharp
// Kinyerd a fogaskerék típusú alakzatok szövegét, és nyomtasd ki őket a konzolon.
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
Végül érdemes lehet hozzáadni egy megerősítő üzenetet, miután a folyamat sikeresen befejeződött:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Ezzel a kinyerés befejeződött, és a szöveges kimenetnek látnia kell a konzolon!
## Következtetés
Gratulálunk! Most megtanultad, hogyan lehet szöveget kinyerni fogaskerék-szerű SmartArt alakzatokból Excelben az Aspose.Cells for .NET segítségével. Ez a praktikus technika utat nyit a vizuális adatábrázoláson alapuló jelentések vagy dokumentációk automatizálása előtt. Akár tapasztalt fejlesztő vagy, akár most kezded, az információk SmartArt-ból történő vezérlése és kinyerése egyszerűsítheti a munkafolyamatodat és hatékonyabbá teheti. Ne felejtsd el megismerni a részletes útmutatót. [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) további képességekért.
## GYIK
### Mi az Aspose.Cells?
Az Aspose.Cells egy .NET könyvtár, amely lehetővé teszi a fejlesztők számára az Excel fájlok egyszerű létrehozását és kezelését.
### Használhatom az Aspose.Cells-t más programozási nyelvekkel?
Igen! Az Aspose.Cells több programozási nyelven is elérhető, beleértve a Java és a Python nyelvet is.
### Meg kell vásárolnom az Aspose.Cells for .NET-et?
Az Aspose.Cells ingyenes próbaverziót kínál, de a hosszabb használathoz vásárlás szükséges. A vásárlási lehetőségeket itt találja. [itt](https://purchase.aspose.com/buy).
### Van elérhető támogatás az Aspose.Cells felhasználók számára?
Természetesen! Közösségi támogatást találhatsz a következő helyen: [Aspose.Cells fórum](https://forum.aspose.com/c/cells/9).
### Ki tudok más SmartArt-típusokat is kinyerni ezzel a módszerrel?
Igen, apró módosításokkal kinyerhet szöveget különféle SmartArt-alakzatokból a kód feltételeinek módosításával.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}