---
title: Mentse a munkafüzetet szöveges CSV formátumba
linktitle: Mentse a munkafüzetet szöveges CSV formátumba
second_title: Aspose.Cells .NET Excel Processing API
description: Ebben a .NET-fejlesztők számára készült átfogó, lépésről lépésre szóló oktatóanyagban megtudhatja, hogyan konvertálhat könnyedén Excel-munkafüzeteket CSV formátumba az Aspose.Cells segítségével.
weight: 17
url: /hu/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mentse a munkafüzetet szöveges CSV formátumba

## Bevezetés
Az adatok kezelésekor a választott formátum valóban meghatározhatja, hogy milyen könnyen tud velük dolgozni. A táblázatos adatok kezelésének leggyakoribb formátumai közé tartozik a CSV (vesszővel elválasztott értékek). Ha Ön Excel-fájlokkal dolgozó fejlesztő, és a munkafüzeteket CSV-formátumba kell konvertálnia, az Aspose.Cells for .NET egy fantasztikus könyvtár, amely leegyszerűsíti ezt a feladatot. Ebben az oktatóanyagban lebontjuk az Excel-munkafüzet zökkenőmentes szöveges CSV-formátumba konvertálásához szükséges lépéseket.
## Előfeltételek
Mielőtt belemerülnénk, győződjön meg arról, hogy minden a helyén van a kezdéshez:
1. Alapszintű C# és .NET ismerete: Mivel C#-ban fogunk kódot írni, elengedhetetlen a nyelv és a .NET keretrendszer ismerete.
2. Aspose.Cells Library: Győződjön meg arról, hogy az Aspose.Cells for .NET könyvtár telepítve van a fejlesztői környezetében. Letöltheti[itt](https://releases.aspose.com/cells/net/).
3. Visual Studio vagy bármilyen C# IDE: A kód írásához és végrehajtásához integrált fejlesztői környezetre (IDE) lesz szüksége. A Visual Studio népszerű választás.
4. Excel-munkafüzet: készítsen egy példa Excel-munkafüzetet (pl. "book1.xls"), amely tartalmaz néhány adatot az átalakítás teszteléséhez.
## Csomagok importálása
Most, hogy az előfeltételeinket lefedtük, a folyamat első lépése a szükséges csomagok importálása. A C# projektben a következő névteret kell szerepeltetnie a kódfájl tetején:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ezek a névterek hozzáférést biztosítanak az Excel-fájlok kezeléséhez és a memóriafolyamok kezeléséhez szükséges osztályokhoz és módszerekhez.
## 1. lépés: Határozza meg a Dokumentumkönyvtár elérési útját
Folyamatunk első lépéseként meghatározzuk, hogy hol tároljuk a dokumentumainkat (Excel-munkafüzeteket). Ez elengedhetetlen, mivel lehetővé teszi programunknak, hogy tudja, hol találja a feldolgozandó fájlokat. 
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```
 Mindenképpen cserélje ki`"Your Document Directory"` a tényleges elérési úttal, ahol a "book1.xls" fájl található. Ez lehet egy könyvtár a számítógépen, vagy egy kiszolgáló elérési útja.
## 2. lépés: Töltse be a forrásmunkafüzetet
Ezután be kell töltenünk az Excel-munkafüzetet, amelyet CSV formátumba konvertálunk.
```csharp
// Töltse be a forrásmunkafüzetet
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 A`Workbook` osztály az Aspose.Cells könyvtárból lehetővé teszi az Excel-munkafüzetek kezelését és elérését. A fájl elérési útjának átadásával betöltjük a megadott munkafüzetet feldolgozásra.
## 3. lépés: Inicializáljon egy bájttömböt a munkafüzet adataihoz
Mielőtt elkezdené konvertálni a munkafüzetet CSV formátumba, inicializálnunk kell egy üres bájttömböt, amely végül a munkalap összes adatát tartalmazza.
```csharp
// 0 bájtos tömb
byte[] workbookData = new byte[0];
```
Ez a bájttömb egyesíti az egyes munkalapok adatait egyetlen struktúrába, amelyet később kiírhatunk egy fájlba.
## 4. lépés: Állítsa be a szöveges mentési beállításokat
Most állítsuk be a szövegformátum mentésére vonatkozó beállításokat. Választhat egyéni határolókat, vagy ragaszkodhat a tabulátorokhoz.
```csharp
// Szövegmentési lehetőségek. Bármilyen típusú elválasztót használhat
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Tabulátor beállítása elválasztóként
```
 Ebben a példában egy tabulátor karaktert használunk elválasztóként. Cserélheted`'\t'` tetszőleges karakterrel, például vesszővel (`,`), attól függően, hogy hogyan szeretné formázni a CSV-t.
## 5. lépés: Ismételje meg az egyes munkalapokat
 Ezután a munkafüzetben lévő összes munkalapot ismételgetjük, és mindegyiket elmentjük a sajátunkba`workbookData` tömböt, de először ki kell választani, hogy melyik munkalapon dolgozzon.
```csharp
// Másolja az egyes munkalapadatokat szöveges formátumban a munkafüzet adattömbébe
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Mentse el az aktív munkalapot szöveges formátumba
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 A ciklus végigfut a munkafüzet minden munkalapján.`ActiveSheetIndex` úgy van beállítva, hogy a cikluson keresztül minden alkalommal az aktuális munkalapot mentsük. Az eredmények a memóriába kerülnek a a`MemoryStream`.
## 6. lépés: A munkalap adatainak lekérése
 Miután elmentett egy munkalapot a memóriafolyamba, a következő lépés az adatok lekérése és hozzáfűzése a`workbookData` sor.
```csharp
    // Mentse el a munkalap adatait egy adattömbbe
    ms.Position = 0; // A memóriafolyam pozíciójának visszaállítása
    byte[] sheetData = ms.ToArray(); // Szerezd meg a bájttömböt
```
`ms.Position = 0;` visszaállítja az írás utáni olvasási pozíciót. Akkor használjuk`ToArray()` a memóriafolyamot a munkalap adatait tároló bájttömbbé alakítani.
## 7. lépés: A munkalapadatok egyesítése
 Most egyesítjük az egyes munkalapok adatait egyetlen egybe`workbookData` korábban inicializált tömb.
```csharp
    // Kombinálja ezeket a munkalapadatokat munkafüzet-adattömbbe
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Létrehozunk egy új tömböt, amely elég nagy ahhoz, hogy a meglévő munkafüzetadatokat és az új munkalapadatokat is tárolja. Ezután a meglévő és az új adatokat ebbe a kombinált tömbbe másoljuk későbbi felhasználás céljából.
## 8. lépés: Mentse el a munkafüzet teljes adatait fájlba
 Végül az összes adattal együtt a mi`workbookData` tömböt, elmenthetjük ezt a tömböt egy megadott fájl elérési útra.
```csharp
//Mentse el a munkafüzet teljes adatait fájlba
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` veszi a kombinált bájttömböt, és egy "out.txt" nevű szövegfájlba írja a megadott könyvtárba.
## Következtetés
És megvan! Sikeresen konvertált egy Excel-munkafüzetet CSV-formátumba az Aspose.Cells for .NET használatával. Ez a folyamat nemcsak hatékony, hanem lehetővé teszi az Excel-adatok egyszerű kezelését további elemzés vagy jelentéskészítés céljából. Mostantól automatizálhatja adatfeldolgozási feladatait, vagy akár nagyobb alkalmazásokba is integrálhatja ezt a funkciót.
## GYIK
### Használhatok különböző határolókat a CSV-fájlhoz?
 Igen, megváltoztathatod a`opts.Separator` bármely kívánt karakterhez, például vesszőhöz vagy pipához.
### Az Aspose.Cells ingyenesen használható?
 Az Aspose.Cells nem ingyenes, de ingyenes próbaverziót kaphat[itt](https://releases.aspose.com/).
### Milyen típusú formátumokba menthetek a CSV-n kívül?
Az Aspose.Cells lehetővé teszi a mentést többféle formátumba, beleértve az XLSX-et, PDF-t és még sok mást.
### Feldolgozhatok nagy Excel-fájlokat az Aspose.Cells segítségével?
Igen, az Aspose.Cells a nagy fájlok hatékony kezelésére készült, de a teljesítmény a rendszererőforrásoktól függhet.
### Hol találok részletesebb dokumentációt?
Átfogó dokumentációt és példákat találhat rajtuk[referencia webhely](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
