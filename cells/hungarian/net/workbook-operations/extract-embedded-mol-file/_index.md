---
title: A beágyazott Mol fájl kibontása a munkafüzetből
linktitle: A beágyazott Mol fájl kibontása a munkafüzetből
second_title: Aspose.Cells .NET Excel Processing API
description: Ebből a részletes, lépésenkénti oktatóanyagból megtudhatja, hogyan bonthat ki beágyazott MOL-fájlokat Excel-munkafüzetekből az Aspose.Cells for .NET használatával.
weight: 18
url: /hu/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# A beágyazott Mol fájl kibontása a munkafüzetből

## Bevezetés
Amikor az Excel-munkafüzeteken belüli adatkezelésről van szó, néha különféle beágyazott objektumokkal találkozhat, amelyek nem szabványos formátumúak. Az egyik ilyen formátum a MOL (Molecular Structure File), amelyet a kémiában általában a molekuláris információk ábrázolására használnak. Ha ezeket a MOL-fájlokat egy Excel-munkafüzetből szeretné kibontani az Aspose.Cells for .NET segítségével, akkor a megfelelő útmutatóhoz jutott. Ebben a cikkben lépésről lépésre végigvezetjük a folyamaton, miközben az egyes részeket tisztázzuk.
## Előfeltételek
Mielőtt belemerülne a kódba, elengedhetetlen, hogy rendelkezzen a szükséges készségekkel és eszközökkel. Íme, amire szüksége lesz:
1. A .NET programozás alapjai: Ismernie kell a C#-t és a .NET keretrendszert.
2.  Aspose.Cells for .NET: Győződjön meg arról, hogy rendelkezik az Aspose.Cells könyvtárral. Tudod[töltse le itt](https://releases.aspose.com/cells/net/).
3. IDE: Használhatja a Visual Studio-t vagy bármely más .NET-kompatibilis IDE-t.
4. Excel munkafüzet beágyazott MOL fájlokkal: Ehhez az oktatóanyaghoz szüksége van egy MOL objektumokat tartalmazó Excel fájlra. Létrehozhat saját vagy bármilyen mintafájlt.
## Csomagok importálása
A kezdéshez importálnia kell a szükséges névtereket a projektbe. Ez döntő fontosságú az Aspose.Cells funkciók eléréséhez. A következőképpen teheti meg:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Ezek a névterek lehetővé teszik a munkafüzetek kezelését, a munkalapok elérését és általában a fájlokkal való munkát.
Most, hogy az előfeltételeinket rendeztük, merüljünk el a kódban, és ismerjük meg a beágyazott MOL-fájlok Excel-munkafüzetből való kibontásának minden lépését. 
## 1. lépés: A címtárak beállítása
Az első lépés annak meghatározása, hogy a forrásdokumentum hol található, és hova szeretné menteni a kibontott MOL fájlokat. Állítsuk be ezeket a könyvtárakat.
```csharp
string SourceDir = "Your Document Directory"; // Cserélje ki a könyvtár elérési útját
string outputDir = "Your Document Directory"; // Cserélje ki a kimeneti útvonalra
```
 Tessék, te cseréld ki`"Your Document Directory"` tényleges könyvtárak elérési útjával. Fontos, hogy mind a forrás-, mind a kimeneti könyvtár elérhető legyen az alkalmazás számára.
## 2. lépés: A munkafüzet betöltése
Miután beállította a könyvtárakat, a következő feladat az Excel munkafüzet betöltése. Tegyük meg most.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Példányt készítünk a`Workbook` osztályt, és átadjuk az elérési utat a nevű Excel fájlunkhoz`EmbeddedMolSample.xlsx`. Ez a lépés inicializálja a munkafüzetet, lehetővé téve a tartalom elérését.
## 3. lépés: Munkalapok ismétlése
Most, hogy a munkafüzet betöltődött, végig kell lépnie a munkafüzeten belül minden munkalapon. Ez lehetővé teszi, hogy minden lapon megvizsgáljon beágyazott objektumokat.

```csharp
var index = 1; // Kibontott MOL fájlok elnevezésére szolgál
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // A további kinyerési logika ide tartozik
}
```

 Itt az a`foreach` hurok segítségével navigálhat a munkalapokon. Minden munkalaphoz hozzáférhet a`OleObjects` gyűjtemény, amely az összes beágyazott objektumot tartalmazza.
## 4. lépés: MOL fájlok kibontása
Most jön a kritikus rész – a MOL fájlok kibontása az OLE objektumokból. Ehhez egy másik ciklusra van szükség a munkalap hurkon belül.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Minden egyes talált OLE objektumhoz új fájlt hoz létre a kimeneti könyvtárban. A`ObjectData` tulajdona a`OleObject` tárolja a beágyazott objektum adatait, amelyeket egy újonnan létrehozott fájlba ír a segítségével`FileStream`. A fájl elnevezése sorrendben történik (`OleObject1.mol`, `OleObject2.mol` stb.) alapján a`index` változó.
## 5. lépés: A folyamat befejezésének megerősítése
Végül, miután az összes MOL-fájlt kicsomagolta, célszerű tájékoztatni a felhasználót a folyamat sikeres befejezéséről.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Ez a sor egyszerűen egy üzenetet nyomtat a konzolnak, amely tudatja, hogy a kicsomagolás sikeres volt. Ez egy kellemes érintés a felhasználói visszajelzésekhez.
## Következtetés
És megvan! Sikeresen kibontotta a beágyazott MOL fájlokat egy Excel-munkafüzetből az Aspose.Cells for .NET segítségével. Ez a folyamat néhány alapvető lépést foglal magában, biztosítva a beágyazott objektumok kezelésének strukturált megközelítését. Akár tudományos kutatással, akár kémiai elemzéssel foglalkozik, vagy egyszerűen csak összetett adatkészletekkel foglalkozik, az ilyen fájltípusok kinyerése és manipulálása jelentősen megváltoztathatja az információkezelés módját. 
## GYIK
### A MOL-on kívül más fájltípusokat is ki lehet bontani az Excelből?
Igen, számos más beágyazott fájltípust is kibonthat hasonló technikákkal.
### Az Aspose.Cells ingyenesen használható?
 Az Aspose.Cells egy kereskedelmi könyvtár, de megteheti[próbáld ki ingyenesen korlátozott ideig](https://releases.aspose.com/).
### Ez a módszer minden Excel verzióval működik?
Igen, amennyiben a fájlformátumot az Aspose.Cells támogatja.
### Automatizálhatom ezt a kivonási folyamatot?
Teljesen! Automatizálhatja ezt a folyamatot, ha elhelyezi a kódot egy ütemezett feladatba vagy egy parancsfájlba.
### Hol találok további dokumentációt az Aspose.Cells-ről?
 Megnézheti a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) további részletekért és példákért.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
