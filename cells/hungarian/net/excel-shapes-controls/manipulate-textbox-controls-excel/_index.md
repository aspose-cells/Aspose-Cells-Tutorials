---
title: Szövegdoboz-vezérlők kezelése az Excelben
linktitle: Szövegdoboz-vezérlők kezelése az Excelben
second_title: Aspose.Cells .NET Excel Processing API
description: Ezzel a könnyen követhető, lépésről lépésre bemutató oktatóanyaggal megtudhatja, hogyan kezelheti az Excel szövegdobozait az Aspose.Cells for .NET segítségével.
weight: 15
url: /hu/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szövegdoboz-vezérlők kezelése az Excelben

## Bevezetés
Ha valaha is dolgozott Excellel, valószínűleg találkozott már azokkal a kis szövegdobozokkal, amelyek segítségével lebegő szöveget adhat hozzá a táblázatokhoz. De mi van akkor, ha programozottan kell manipulálnia ezeket a szövegdobozokat? Itt jön jól az Aspose.Cells for .NET. Segítségével könnyedén elérheti és módosíthatja a szövegdobozokat, így tökéletes a feladatok automatizálásához vagy a jelentések testreszabásához. Ebben az oktatóanyagban végigvezetjük a szövegdobozok Excelben az Aspose.Cells for .NET segítségével történő kezelésének folyamatán.
## Előfeltételek
Mielőtt belemerülne a tényleges kódba, győződjön meg arról, hogy mindent megfelelően beállított:
1.  Aspose.Cells for .NET: Le kell töltenie az Aspose.Cells for .NET könyvtárat. A letöltési linket megtalálod[itt](https://releases.aspose.com/cells/net/).
2. .NET fejlesztői környezet: Bármely IDE, amely támogatja a .NET-et, például a Visual Studio, működik.
3. Alapvető C# ismerete: Ez az oktatóanyag feltételezi, hogy ismeri az alapvető C# szintaxist és az Excel munkafüzetek szerkezetét.
4.  Excel-fájl: Egy létező Excel-fájl szövegmezőkkel (ezt fogjuk használni`book1.xls`ebben a példában).
5.  Aspose License: Ha nem használja az ingyenes próbaverziót, akkor szüksége lesz rá[vétel](https://purchase.aspose.com/buy) engedélyt vagy szerezzen a[ideiglenes](https://purchase.aspose.com/temporary-license/).
Most pedig merüljünk el a lépésekben!
## Csomagok importálása
Mielőtt az Excel-munkafüzeteket és szövegdobozokat az Aspose.Cells segítségével kezelné, importálnia kell a szükséges névtereket. Íme a kódrészlet, amelyet a C# fájl tetején fog használni:
```csharp
using System.IO;
using Aspose.Cells;
```
Ezek a csomagok hozzáférést biztosítanak a munkafüzet-kezeléshez, a munkalapokhoz és a rajzobjektumokhoz (például szövegdobozokhoz).
Most, hogy mindent beállítottunk, bontsuk le a szövegdobozok kezelésének folyamatát könnyen követhető lépésekre.
## 1. lépés: Állítsa be a munkafüzet-könyvtárat
 Az első lépés az, hogy adja meg, hogy az Excel-fájlok hol legyenek a rendszeren. Cserélnie kell a helyőrzőt`Your Document Directory` a fájl tényleges elérési útjával. Ez az útvonal a`dataDir` változó a könnyű hivatkozás érdekében a kódban.
```csharp
string dataDir = "Your Document Directory";
```
Ez lehetővé teszi a program számára, hogy tudja, hol találja a bemeneti Excel fájlt (`book1.xls`), és hová kell menteni a kimeneti fájlt.
## 2. lépés: Nyissa meg az Excel fájlt
Ezután be kell töltenie a meglévő Excel-fájlt az Aspose.Cells munkafüzet objektumba. Ez a munkafüzet az Excel-adatok tárolójaként működik, hozzáférést biztosítva a munkalapokhoz és a rajzobjektumokhoz (például szövegdobozokhoz).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 A`Workbook` Az Aspose.Cells osztály betölti a megadott Excel fájlt a könyvtárából. Ha a fájl nem létezik a megadott könyvtárban, akkor kivételt dob, ezért ellenőrizze, hogy az elérési út helyes-e.
## 3. lépés: Nyissa meg az első munkalapot
Most, hogy betöltötte a munkafüzetet, hozzáférhet a munkalapjaihoz. Ebben a példában a munkafüzet első munkalapját érjük el, amely a 0 indexen van tárolva.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 A`Worksheets` tulajdonság hozzáférést biztosít a munkafüzet összes lapjához. Itt csak az első lapra vagyunk kíváncsiak, de a megfelelő index megadásával bármelyik lappal dolgozhat.
## 4. lépés: Szerezze be az első szövegdoboz-objektumot
Az Excel-munkalap szövegdobozai rajzobjektumnak minősülnek. Az Aspose.Cells.Drawing.TextBox osztály tulajdonságokat és módszereket biztosít ezek kezeléséhez. A munkalap első szövegdobozának eléréséhez egyszerűen tekintse meg a`TextBoxes` gyűjtés index szerint.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Ez lekéri az első szövegdoboz-objektumot a`TextBoxes` gyűjtemény. Ha a munkalapon nincs szövegdoboz az indexnél, akkor kivételt dob, ezért mindig győződjön meg arról, hogy az index érvényes.
## 5. lépés: Szöveg lekérése az első szövegmezőből
 A szövegmező elérése után a benne lévő szöveget kibonthatja a`.Text` ingatlan.
```csharp
string text0 = textbox0.Text;
```
 Ez rögzíti a szöveget az első szövegmezőből a`text0` húr. Most már megjelenítheti, módosíthatja vagy feldolgozhatja az alkalmazásban.
## 6. lépés: Nyissa meg a második szövegdoboz-objektumot
Több szövegdoboz kezeléséhez továbbiakat is lekérhetünk a munkalapról. Itt a második szövegmezőt az elsőhöz hasonló módon érjük el:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Ismét elérjük a második szövegdobozt az 1-es index használatával`TextBoxes`gyűjtemény.
## 7. lépés: Szöveg lekérése a második szövegmezőből
Csakúgy, mint az első szövegmezőnél, a második szövegdobozból is lekérheti a szöveget, és egy karakterláncban tárolhatja:
```csharp
string text1 = textbox1.Text;
```
Ez rögzíti az aktuális szöveget a második szövegmezőből.
## 8. lépés: Módosítsa a szöveget a második szövegmezőben
 Most tegyük fel, hogy módosítani szeretné a szöveget a második szövegmezőben. Ezt egyszerűen megteheti, ha új karakterláncot rendel hozzá a`.Text` a szövegdoboz objektum tulajdonsága.
```csharp
textbox1.Text = "This is an alternative text";
```
Ez megváltoztatja a második szövegmezőben lévő szöveget az új tartalomra. Ide bármilyen szöveget beszúrhat igényei szerint.
## 9. lépés: Mentse el a frissített Excel-fájlt
 Végül a szövegmezők módosítása után ideje elmenteni a változtatásokat. Az Aspose.Cells lehetővé teszi a módosított munkafüzet mentését a`.Save()` módszer. Megadhat új fájlnevet, vagy felülírhatja a meglévő fájlt.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Ezzel elmenti a módosított Excel-fájlt a kijelölt kimeneti útvonalra. Most, amikor megnyitja az Excel fájlt, látni fogja a szövegmezőkön végzett módosításokat.
## Következtetés
És megvan! Most tanulta meg, hogyan lehet szövegdobozokat kezelni az Excelben az Aspose.Cells for .NET használatával. Legyen szó a jelentéskészítés automatizálásáról, az Excel-táblázatok testreszabásáról vagy a dinamikus tartalom létrehozásáról, az Aspose.Cells megkönnyíti az Excel-fájlok minden aspektusának programozott vezérlését. A szöveg kibontásától és módosításától a frissített fájlok mentéséig ez a könyvtár hatékony eszköz az Excellel .NET-környezetekben dolgozó fejlesztők számára.
## GYIK
### A szövegdobozokon kívül más rajzobjektumokat is kezelhetek az Aspose.Cells segítségével?
Igen, az Aspose.Cells lehetővé teszi más rajzobjektumok, például alakzatok, diagramok és képek kezelését.
### Mi történik, ha megpróbálok hozzáférni egy nem létező szövegdobozhoz?
 Ha a szövegdoboz indexe a tartományon kívül esik, egy`IndexOutOfRangeException` dobják majd.
### Hozzáadhatok új szövegdobozokat egy Excel-munkalaphoz az Aspose.Cells segítségével?
 Igen, az Aspose.Cells lehetővé teszi új szövegmezők hozzáadását a`AddTextBox` módszer.
### Szükségem van engedélyre az Aspose.Cells használatához?
 Igen, licencet kell vásárolnia, de az Aspose is kínál a[ingyenes próbaverzió](https://releases.aspose.com/).
### Használhatom az Aspose.Cells-t a C#-on kívül más programozási nyelvekkel is?
Igen, az Aspose.Cells bármely .NET által támogatott nyelvvel használható, például a VB.NET-tel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
