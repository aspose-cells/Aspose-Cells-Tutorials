---
title: Másolja az adatokat a munkafüzeten belül az Aspose.Cells segítségével
linktitle: Másolja az adatokat a munkafüzeten belül az Aspose.Cells segítségével
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan másolhat hatékonyan adatokat egy Excel-munkafüzetben az Aspose.Cells for .NET segítségével lépésenkénti útmutatóval, kódmintákkal és hasznos tippekkel.
weight: 12
url: /hu/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Másolja az adatokat a munkafüzeten belül az Aspose.Cells segítségével

## Bevezetés
Az Excel-munkafüzeteken belüli adatok kezelése számos alkalmazás alapvető része. Képzelje el, hogy van egy sablonja vagy egy lapja, amely fontos adatokkal van megtöltve, és azt szeretné lemásolni ugyanabban a munkafüzetben további felhasználás céljából. Itt ragyog az Aspose.Cells for .NET! Ebben az útmutatóban végigvezetjük Önt, hogyan másolhat adatokat ugyanabban a munkafüzetben az Aspose.Cells használatával, egy barátságos és világos, lépésről lépésre bemutatott oktatóanyag segítségével.
## Előfeltételek
Mielőtt belevágnánk a kódolásba, győződjünk meg arról, hogy mindennel rendelkezünk, ami a feladat elvégzéséhez szükséges:
1.  Aspose.Cells for .NET Library – Töltse le a legújabb verziót innen[Aspose.Cells for .NET letöltési oldal](https://releases.aspose.com/cells/net/).
2. Fejlesztői környezet – Szüksége lesz egy .NET-kompatibilis IDE-re, például a Visual Studiora.
3.  Licenc – Az Aspose.Cells ingyenes próbaverziója vagy megvásárolt licenc használata. Kaphat ideiglenes engedélyt[itt](https://purchase.aspose.com/temporary-license/) vagy fedezze fel a vásárlási lehetőségeket[itt](https://purchase.aspose.com/buy).
## Csomagok importálása
Kódjában importálnia kell az Aspose.Cells fájlt az osztályok és metódusok használatához:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Merüljünk el a kódban! Az Aspose.Cells for .NET segítségével egy munkafüzetben lévő adatok másolásának feladatát könnyen követhető lépésekre bontjuk.
## 1. lépés: Állítsa be a címtár elérési útjait
Mielőtt elkezdené kezelni a munkafüzetet, határozzuk meg, hol találhatók a fájljaink, és hová szeretnénk menteni a kimenetet. A címtár elérési útjának beállítása rendszerezi a dolgokat.
```csharp
// Állítsa be a dokumentumok könyvtárának elérési útját.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Tessék, cserélje ki`"Your Document Directory"` a munkafüzet tárolásának tényleges elérési útjával. Ez az elérési út változó megkönnyíti a bemeneti és kimeneti fájlokra való hivatkozást.
## 2. lépés: Nyissa meg a meglévő Excel-fájlt
Excel-fájllal való munkavégzéshez be kell töltenünk az Aspose.Cells munkafüzet-objektumába. Ez a lépés megnyitja azt a fájlt, amelyből adatokat szeretne másolni.
```csharp
// Nyisson meg egy meglévő Excel-fájlt.
Workbook wb = new Workbook(inputPath);
```
 Ezzel a mi`Workbook` objektum`wb` most már készen áll a tartalmával való interakcióra`book1.xls`.
## 3. lépés: Nyissa meg a Munkalapgyűjteményt
 Most, hogy a munkafüzet meg van nyitva, hozzáférünk a munkalapgyűjteményéhez. A`WorksheetCollection` osztály segít több lappal dolgozni a munkafüzeten belül.
```csharp
// Hozzon létre egy munkalap-objektumot, amely a munkafüzet összes lapjára hivatkozik.
WorksheetCollection sheets = wb.Worksheets;
```
 Itt,`sheets` lehetővé teszi számunkra a munkafüzet minden egyes lapjának kezelését, beleértve egy meglévő lap másolatának hozzáadását.
## 4. lépés: Másolja az adatokat egy új lapra
Feladatunk fő része egy lap tartalmának másolása egy új lapra ugyanazon a munkafüzeten belül. Ebben a példában az „1. munkalap” adatait egy új munkalapra másoljuk.
```csharp
// Másolja az adatokat az „1. lapról” egy új munkalapra a munkafüzetben.
sheets.AddCopy("Sheet1");
```
 A`AddCopy`metódus létrehozza a megadott lap pontos másolatát, hozzáfűzve azt a munkafüzethez. Itt lemásoljuk az „1. munkalapot”. Megadhatja bármely másolni kívánt munkalap nevét.
## 5. lépés: Mentse el a munkafüzetet az új lappal
A munkalap másolása után mentse el a munkafüzetet új néven vagy új helyre a változtatások megőrzése érdekében.
```csharp
// Mentse el a munkafüzetet a másolt adatokkal.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Ez a sor másként menti a módosított munkafüzetet`CopyWithinWorkbook_out.xls` a megadott könyvtárban.
## Következtetés
És megvan! Az adatok munkafüzeten belüli másolása az Aspose.Cells for .NET használatával gyerekjáték. Az Aspose.Cells egyszerűvé teszi az Excel-fájlok kezelését, és lehetővé teszi az összetett adatkezelési feladatok egyszerű elvégzését. Függetlenül attól, hogy sablonhasználathoz, biztonsági mentésekhez vagy új verziók létrehozásához lapokat kell másolnia, az általunk tárgyalt lépések segítenek elérni céljait.
 Ha többet szeretne felfedezni, nézze meg a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) a fejlett funkciókhoz és képességekhez.
## GYIK
### Másolhatok több lapot egyszerre?
Az Aspose.Cells nem támogatja több munkalap másolását egyetlen híváson belül, de a többszörözni kívánt lapokon át lehet lépni, és egyenként másolhatja őket.
### Átnevezhetem a másolt lapot?
 Igen, a lap másolása után átnevezheti a használatával`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Az Aspose.Cells kompatibilis a .NET Core-al?
Teljesen! Az Aspose.Cells támogatja a .NET Framework és a .NET Core környezeteket is.
### Hogyan kezelhetem a formázást lapok másolása közben?
 A`AddCopy` módszer megőrzi az összes tartalmat és formázást, így a másolt munkalap az eredetihez hasonlóan fog kinézni.
### Mi a teendő, ha egy lapot egy másik munkafüzetbe akarok másolni?
Használhatja a`Copy` módszer egy másik munkafüzetre való hivatkozással, mint pl`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
