---
"description": "Tanulja meg, hogyan adhat meg dokumentumtulajdonságokat, például verziót, szerzőt és címet egy Excel-fájlban programozottan az Aspose.Cells for .NET használatával lépésről lépésre bemutatott utasításokkal."
"linktitle": "Excel fájl dokumentumverziójának programozott megadása .NET-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Excel fájl dokumentumverziójának programozott megadása .NET-ben"
"url": "/hu/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel fájl dokumentumverziójának programozott megadása .NET-ben

## Bevezetés
Az Aspose.Cells for .NET egy hatékony függvénykönyvtár, amely lehetővé teszi a fejlesztők számára, hogy könnyedén, programozottan manipulálják az Excel-fájlokat. Akár a nulláról szeretnél Excel-fájlokat létrehozni, akár meglévőket módosítani, az Aspose.Cells átfogó API-t kínál a céljaid eléréséhez. Az egyik ilyen funkció a dokumentumtulajdonságok, például a verzió, a szerző vagy a cím megadása. Ez az oktatóanyag bemutatja, hogyan adhatod meg programozott módon egy Excel-fájl dokumentumverzióját az Aspose.Cells for .NET használatával.
## Előfeltételek
Mielőtt belemerülnénk a részletekbe, győződjünk meg róla, hogy mindent megtalál, amire szüksége van ehhez az oktatóanyaghoz:
1. Aspose.Cells .NET-hez: Letöltheti a legújabb verziót [itt](https://releases.aspose.com/cells/net/)Ha még nem vásárolt licencet, választhat egyet. [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) hogy felfedezhesd a funkciókat.
2. .NET fejlesztői környezet: Használhatja a Visual Studio-t vagy bármilyen .NET-kompatibilis IDE-t.
3. C# alapismeretek: A C# programozás ismerete megkönnyíti a haladást.
## Csomagok importálása
Mielőtt elkezdenéd a kódolást, importálnod kell a szükséges névtereket az Aspose.Cells könyvtárból. Ez hozzáférést biztosít az Excel fájlok kezeléséhez szükséges osztályokhoz és metódusokhoz.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ez a két névtér elengedhetetlen lesz a munkafüzettel és annak beépített dokumentumtulajdonságaival való interakcióhoz.
Most bontsuk le a dokumentumtulajdonságok megadásának folyamatát egy Excel-fájlban, beleértve a verziót, a címet és a szerzőt.
## 1. lépés: A munkafüzet objektum inicializálása
Az első lépés egy új példány létrehozása a `Workbook` objektum. Ez az objektum a teljes Excel-fájlt jelöli, amellyel dolgozni fog.
```csharp
Workbook wb = new Workbook();
```
A `Workbook` Az osztály egy Excel fájl reprezentációját biztosítja. Létrehozásával egy üres Excel munkafüzetet hozunk létre, amelyet manipulálhatunk.
## 2. lépés: Beépített dokumentumtulajdonságok elérése
Az Aspose.Cells beépített dokumentumtulajdonságokat kínál, amelyek olyan mezőket tartalmaznak, mint a cím, a szerző és a dokumentum verziója. Ezeket a tulajdonságokat a következőn keresztül érheti el: `BuiltInDocumentProperties` gyűjtemény.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
A `BuiltInDocumentPropertyCollection` Az osztály hozzáférést biztosít a beépített dokumentumtulajdonságok gyűjteményéhez, például a címhez, a szerzőhöz és a dokumentumhoz jellemzően kapcsolódó egyéb metaadatokhoz.
## 3. lépés: Állítsa be az Excel-dokumentum címét
Ezután beállítjuk az Excel-dokumentum címét. Ez a metaadat segít a fájl későbbi azonosításában és kezelésében.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
cím megadása fontos a dokumentum rendszerezéséhez. Ez a metaadat a fájl tulajdonságai között látható, és külső rendszerek felhasználhatják a dokumentum hatékonyabb katalogizálására vagy azonosítására.
## 4. lépés: Adja meg a szerzőt
A dokumentum szerzője is megadható, hogy tükrözze, ki hozta létre vagy módosította a fájlt.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Ez a lépés segít a dokumentum létrehozójához rendelni, további metaadatokat biztosítva a dokumentumkezeléshez vagy az együttműködési forgatókönyvekhez.
## 5. lépés: Adja meg a dokumentum verzióját
Az oktatóanyag egyik legfontosabb tulajdonsága a dokumentum verziója. Ebben a lépésben megadhatja a dokumentum verzióját, ami hasznos olyan környezetekben, ahol verziókövetésre van szükség.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
A dokumentum verziójának beállítása egyértelművé teszi, hogy a dokumentum vagy könyvtár melyik verzióját használták a fájl létrehozásához. Ez különösen fontos azokban a környezetekben, ahol nyomon kell követni a fájlverziókat vagy a különböző könyvtárverziókkal való kompatibilitást.
## 6. lépés: Mentse el az Excel-fájlt
Végül elmentheted az Excel fájlt az összes beállított tulajdonsággal. Az Aspose.Cells lehetővé teszi a fájl különböző formátumokban történő mentését, de ebben a példában a következőnél maradunk: `.xlsx` formátum.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
A `Save` metódussal mentheti a fájlt a megadott könyvtárba. Itt Excel-fájlként mentjük el a `.xlsx` formátum. Szükség esetén az Aspose.Cells olyan formátumokat is támogat, mint a `.xls`, `.csv`, és `.pdf`, rugalmasságot biztosítva a projekt igényei alapján.
## Következtetés
Ebben az oktatóanyagban bemutattuk, hogyan adhatjuk meg a dokumentum tulajdonságait, különösen a dokumentum verzióját, egy Excel-fájlban az Aspose.Cells for .NET használatával. Az Aspose.Cells egy rendkívül rugalmas és hatékony eszköz, amely lehetővé teszi az Excel-fájlok programozott kezelését, így nagyszerű eszköz minden táblázatokkal dolgozó .NET-fejlesztő számára.
## GYIK
### Módosíthatok más beépített tulajdonságokat az Aspose.Cells használatával?  
Igen, módosíthatja a többi beépített tulajdonságot, például a tárgyat, a kulcsszavakat és a megjegyzéseket.
### Milyen fájlformátumokat támogat az Aspose.Cells?  
Az Aspose.Cells számos formátumot támogat, beleértve a következőket: `.xls`, `.xlsx`, `.csv`, `.pdf`, és még sok más.
### Szükségem van licencre az Aspose.Cells for .NET használatához?  
Az Aspose.Cells-t a következővel fedezheted fel: [ingyenes próba](https://releases.aspose.com/) vagy jelentkezzen egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) hosszabb teszteléshez.
### Használhatom az Aspose.Cells-t egy webes alkalmazásban?  
Igen, az Aspose.Cells asztali és webes alkalmazásokban is használható. Rendkívül sokoldalú, és jól integrálható a .NET webes keretrendszerekkel.
### Hol kaphatok támogatást az Aspose.Cells-hez?  
Közösségi és támogatási lehetőségekhez férhetsz hozzá a következőn keresztül: [Aspose.Cells támogatói fórum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}