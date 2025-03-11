---
title: Az Excel fájl dokumentumverziójának programozott megadása .NET-ben
linktitle: Az Excel fájl dokumentumverziójának programozott megadása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhatja meg a dokumentum tulajdonságait, például a verziót, a szerzőt és a címet egy Excel-fájlban programozottan az Aspose.Cells for .NET használatával lépésről lépésre.
weight: 12
url: /hu/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az Excel fájl dokumentumverziójának programozott megadása .NET-ben

## Bevezetés
Az Aspose.Cells for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára az Excel-fájlok egyszerű programozását. Akár a semmiből szeretne Excel-fájlokat létrehozni, akár a meglévőket módosítani, az Aspose.Cells átfogó API-t kínál céljainak eléréséhez. Az egyik ilyen funkció a dokumentum tulajdonságainak megadása, például a verzió, a szerző vagy a cím. Ez az oktatóanyag végigvezeti Önt, hogyan adhatja meg programozottan egy Excel-fájl dokumentumverzióját az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belemerülnénk a részletekbe, győződjünk meg arról, hogy mindennel rendelkezünk, ami ehhez az oktatóanyaghoz szükséges:
1. Aspose.Cells for .NET: Letöltheti a legújabb verziót[itt](https://releases.aspose.com/cells/net/) . Ha még nem vásárolt licencet, választhat a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) a funkciók felfedezéséhez.
2. .NET fejlesztői környezet: Használhatja a Visual Studio-t vagy bármely .NET-kompatibilis IDE-t.
3. Alapvető C# ismerete: A C# programozás megértése megkönnyíti a követést.
## Csomagok importálása
A kódolás megkezdése előtt importálnia kell a szükséges névtereket az Aspose.Cells könyvtárból. Ez hozzáférést biztosít az Excel-fájlok kezeléséhez szükséges osztályokhoz és metódusokhoz.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ez a két névtér elengedhetetlen lesz a munkafüzettel és a beépített dokumentumtulajdonságokkal való interakcióhoz.
Most bontsuk le a dokumentum tulajdonságainak Excel-fájlban történő megadásának folyamatát, beleértve a verziót, a címet és a szerzőt.
## 1. lépés: Inicializálja a munkafüzet objektumot
 Az első lépés egy új példány létrehozása a`Workbook` objektum. Ez az objektum képviseli a teljes Excel-fájlt, amellyel dolgozni fog.
```csharp
Workbook wb = new Workbook();
```
 A`Workbook`osztály egy Excel-fájl reprezentációját biztosítja. Példányosításával egy üres Excel munkafüzetet hozunk létre, amelyet kezelhetünk.
## 2. lépés: Nyissa meg a beépített dokumentum tulajdonságait
 Az Aspose.Cells beépített dokumentumtulajdonságokat kínál, amelyek olyan mezőket tartalmaznak, mint a cím, a szerző és a dokumentum verziója. Ezeket a tulajdonságokat a következőn keresztül érheti el`BuiltInDocumentProperties`gyűjtemény.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 A`BuiltInDocumentPropertyCollection` osztály hozzáférést biztosít a beépített dokumentumtulajdonságok gyűjteményéhez, például a címhez, a szerzőhöz és a dokumentumhoz jellemzően társított egyéb metaadatokhoz.
## 3. lépés: Állítsa be az Excel-dokumentum címét
Ezután beállítjuk az Excel dokumentum címét. Ezek a metaadatok segítenek a fájl későbbi azonosításában és kezelésében.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
A cím beállítása fontos a dokumentumrendezés szempontjából. Ezek a metaadatok a fájltulajdonságokban láthatók, és külső rendszerek felhasználhatják a dokumentum hatékonyabb katalogizálására vagy azonosítására.
## 4. lépés: Adja meg a szerzőt
A dokumentum szerzője is megadható, hogy tükrözze, ki hozta létre vagy módosította a fájlt.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Ez a lépés segít a dokumentum hozzárendelésében a készítőhöz, és további metaadatokat biztosít a dokumentumkezeléshez vagy az együttműködési forgatókönyvekhez.
## 5. lépés: Adja meg a dokumentum verzióját
Az egyik legfontosabb tulajdonság, amellyel ebben az oktatóanyagban foglalkozunk, a dokumentum verziója. Ez a lépés lehetővé teszi a dokumentum verziójának megadását, ami akkor hasznos, ha olyan környezetben dolgozik, ahol verziókezelésre van szükség.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
A dokumentum verziójának beállítása egyértelművé teszi, hogy a dokumentum vagy könyvtár melyik verzióját használták a fájl létrehozásához. Ez különösen fontos olyan környezetekben, ahol nyomon kell követni a fájlok verzióit vagy a kompatibilitást a különböző könyvtárverziókkal.
## 6. lépés: Mentse el az Excel fájlt
 Végül elmentheti az Excel fájlt az összes beállított tulajdonsággal. Az Aspose.Cells lehetővé teszi a fájl különböző formátumokban történő mentését, de ebben a példában maradunk a`.xlsx` formátum.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 A`Save` módszerrel menti a fájlt a megadott könyvtárba. Itt Excel fájlként mentjük el a`.xlsx`formátum. Ha szükséges, az Aspose.Cells olyan formátumokat is támogat, mint pl`.xls`, `.csv` , és`.pdf`, amely rugalmasságot biztosít a projekt igényei alapján.
## Következtetés
Ebben az oktatóanyagban végigvezettük, hogyan adhatjuk meg a dokumentum tulajdonságait, különösen a dokumentum verzióját egy Excel-fájlban az Aspose.Cells for .NET használatával. Az Aspose.Cells egy rendkívül rugalmas és hatékony eszköz, amely lehetővé teszi az Excel-fájlok programozott kezelését, így nagyszerű eszköz a táblázatokkal dolgozó .NET-fejlesztők számára.
## GYIK
### Módosíthatok más beépített tulajdonságokat az Aspose.Cells használatával?  
Igen, módosíthatja az egyéb beépített tulajdonságokat, például a tárgyat, a kulcsszavakat és a megjegyzéseket.
### Milyen fájlformátumokat támogat az Aspose.Cells?  
 Az Aspose.Cells a formátumok széles skáláját támogatja, beleértve`.xls`, `.xlsx`, `.csv`, `.pdf`, és még sok más.
### Szükségem van licencre az Aspose.Cells for .NET használatához?  
 Az Aspose.Cells-t felfedezheti a[ingyenes próbaverzió](https://releases.aspose.com/) vagy jelentkezzen a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) kiterjesztett tesztelésre.
### Használhatom az Aspose.Cells-t webalkalmazásban?  
Igen, az Aspose.Cells asztali és webes alkalmazásokban is használható. Nagyon sokoldalú, és jól integrálható a .NET webes keretrendszerekkel.
### Hol kaphatok támogatást az Aspose.Cells-hez?  
 A közösséghez és a támogatáshoz a[Aspose.Cells támogatási fórum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
