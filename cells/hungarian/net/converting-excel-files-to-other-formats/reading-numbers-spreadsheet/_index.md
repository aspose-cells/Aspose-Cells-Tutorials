---
title: Számtáblázat programozott olvasása .NET-ben
linktitle: Számtáblázat programozott olvasása .NET-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Ebben a részletes oktatóanyagban megtudhatja, hogyan olvassa el a Numbers-táblázatokat, és hogyan konvertálja azokat PDF-be az Aspose.Cells for .NET segítségével.
weight: 18
url: /hu/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Számtáblázat programozott olvasása .NET-ben

## Bevezetés
A mai digitális világban az adatkezelés létfontosságú készség, a táblázatok pedig az adatszervezés élvonalában állnak. De mi van akkor, ha egy Numbers-táblázattal – az Apple Numbers alkalmazásával létrehozott fájlokkal – kell dolgoznia .NET használatával? Ne aggódj; nem vagy egyedül! Ebben az oktatóanyagban a Numbers-táblázat programozott olvasásának folyamatát mutatjuk be az Aspose.Cells for .NET segítségével. Megtanulja, hogyan tölthet be egy Numbers-fájlt, és hogyan alakíthatja át PDF-be.
## Előfeltételek
Mielőtt elkezdenénk, néhány dolgot meg kell tennie:
1. Aspose.Cells for .NET: Győződjön meg arról, hogy telepítve van az Aspose.Cells könyvtár. Letöltheti[itt](https://releases.aspose.com/cells/net/).
2. Visual Studio: Javasoljuk, hogy a Visual Studio (vagy bármely más .NET-kompatibilis IDE) telepítve legyen a gépen.
3. Alapvető C# ismerete: A C# programozás egy kis ismerete segít a zökkenőmentes követésben.
4. Az Ön dokumentumkönyvtára: Szüksége lesz egy könyvtárra, ahol a Numbers-fájlt tárolja, valamint egy helyet a konvertált PDF mentéséhez.
Ha ezeket az előfeltételeket teljesítette, minden készen áll a kezdésre!
## Csomagok importálása
Először is importálnunk kell a szükséges csomagokat a C# projektünkbe. Ez döntő lépés, mert lehetővé teszi számunkra, hogy kihasználjuk az Aspose.Cells könyvtár által biztosított funkciókat.
1. Nyissa meg C#-projektjét a Visual Studióban.
2. Hivatkozás hozzáadása az Aspose.Cells könyvtárhoz:
   - Ha NuGetet használ, egyszerűen futtassa a következő parancsot a Package Manager konzolon:
```
 Install-Package Aspose.Cells
 ```
3. Importálja a szükséges névtereket a kódba:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Most, hogy importáltuk a szükséges csomagokat, folytassuk a Numbers-táblázat olvasásának lépésenkénti útmutatóját.
## 1. lépés: Adja meg a forrás- és kimeneti könyvtárakat
Ebben a lépésben beállítjuk azokat a könyvtárakat, ahol a forrás Numbers fájl található, és ahová menteni szeretné a kimeneti PDF-fájlt.
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory"; // Frissítse ezt a tényleges könyvtárra
// Kimeneti könyvtár
string outputDir = "Your Document Directory"; // Frissítse ezt a tényleges könyvtárra
```
 Itt két karakterlánc-változót definiálunk,`sourceDir` és`outputDir` , a bemeneti és kimeneti fájlok helyének megadásához. Ügyeljen arra, hogy cserélje ki`"Your Document Directory"` a rendszer tényleges elérési útjaival.
## 2. lépés: Állítsa be a betöltési beállításokat a számformátumhoz
Ezután megadjuk a betöltési beállításokat a Numbers-táblázat olvasásához. Ez a lépés elengedhetetlen, mivel megmondja az Aspose-nak, hogyan kell értelmezni a Numbers fájlt.
```csharp
// Adja meg a terhelési beállításokat; be akarjuk tölteni a Számok táblázatot
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Létrehozunk a`LoadOptions` objektumot, és adja meg a formátumot mint`LoadFormat.Numbers`. Ez jelzi az Aspose.Cells könyvtárnak, hogy egy Numbers fájllal dolgozunk. 
## 3. lépés: Töltse be a Számtáblázatot egy munkafüzetbe
Most itt az ideje, hogy betöltse a tényleges Numbers táblázatot a`Workbook` objektum.
```csharp
// Töltse be a Számok táblázatot a munkafüzetbe a fenti betöltési beállításokkal
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Példányosítjuk a`Workbook` objektumot, és adja át a Numbers fájl elérési útját a betöltési opcióinkkal együtt. Győződjön meg arról, hogy a fájlnév (`sampleNumbersByAppleInc.numbers`) megegyezik a Numbers fájl tényleges nevével.
## 4. lépés: Mentse el a munkafüzetet PDF formátumban
A Numbers fájl sikeres betöltése után a következő lépés az, hogy más formátumban – különösen PDF-ben – mentse.
```csharp
// Mentse el a munkafüzetet PDF formátumba
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Itt hívjuk a`Save` módszer a`Workbook` objektumot, megadva a kimeneti fájl elérési útját és a menteni kívánt formátumot. Ebben az esetben PDF formátumban mentjük el. Győződjön meg arról, hogy a kimeneti fájl neve (`outputNumbersByAppleInc.pdf`) egyedi, és nem ír felül egyetlen meglévő fájlt sem.
## 5. lépés: Erősítse meg a sikert
Végül adjunk hozzá egy üzenetet, amely megerősíti, hogy műveletünk sikeres volt.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Ez a kódsor sikeres üzenetet nyomtat a konzolra, ha minden készen van. Mindig jó visszajelzést kapni, igaz?
## Következtetés
És megvan! Sikeresen elolvasott egy Numbers-táblázatot, és PDF-be konvertálta az Aspose.Cells for .NET segítségével. Ez a nagy teljesítményű könyvtár lehetővé teszi a táblázatok könnyed kezelését, így az adatkezelési feladatokat könnyedén elvégezheti. Függetlenül attól, hogy alkalmazásokat fejleszt, vagy egyszerűen csak hatékonyabban kell kezelnie a táblázatokat, az Aspose.Cells egy fantasztikus eszköz az eszköztárban.
## GYIK
### Milyen típusú fájlokat tud olvasni az Aspose.Cells?  
Az Aspose.Cells számos fájlformátumot képes olvasni, beleértve az XLS-, XLSX-, CSV- és Numbers-fájlokat. 
### Szerkeszthetem a Numbers fájlokat az Aspose.Cells használatával?  
Igen, az Aspose.Cells segítségével olvashat, kezelhet és menthet Numbers-fájlokat.
### Az Aspose.Cells ingyenesen használható?  
 Az Aspose.Cells ingyenes próbaverziót kínál, de a hosszabb használathoz licencre lesz szüksége. Ellenőrizze az árat[itt](https://purchase.aspose.com/buy).
### Mi a teendő, ha hibát észlelek egy Numbers-fájl betöltése közben?  
 Győződjön meg arról, hogy a megfelelő betöltési beállításokat használja, és hogy a fájl elérési útja pontos. További támogatásért keresse fel a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).
### Hogyan szerezhetek ideiglenes licencet az Aspose.Cells számára?  
 Ideiglenes jogosítványt igényelhet[itt](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
