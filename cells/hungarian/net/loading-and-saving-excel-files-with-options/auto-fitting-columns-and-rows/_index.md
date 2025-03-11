---
title: Oszlopok és sorok automatikus illesztése a HTML munkafüzetbe való betöltésekor
linktitle: Oszlopok és sorok automatikus illesztése a HTML munkafüzetbe való betöltésekor
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan illesztheti automatikusan az oszlopokat és sorokat, miközben betölti a HTML-t az Excelbe az Aspose.Cells for .NET segítségével. Lépésről lépésre útmutató mellékelve.
weight: 10
url: /hu/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Oszlopok és sorok automatikus illesztése a HTML munkafüzetbe való betöltésekor

## Bevezetés
Gondolkozott már azon, hogyan állíthatja be automatikusan az oszlop- és sorméretet, miközben HTML-tartalmat tölt be egy Excel-munkafüzetbe az Aspose.Cells for .NET segítségével? Nos, jó helyen jársz! Ebben az oktatóanyagban részletesen megvizsgáljuk, hogyan tölthet be egy HTML-táblázatot egy munkafüzetbe, és hogyan biztosíthatja, hogy az oszlopok és sorok automatikusan illeszkedjenek a tartalomhoz. Ha gyakran változó dinamikus adatokkal dolgozik, ez az útmutató a jól formázott Excel-lapok HTML-ből történő létrehozásához nyújt segítséget.
### Előfeltételek
Mielőtt belevágna a kódba, néhány dolgot be kell állítania a rendszeren. Ne aggódjon, ez egyszerű és egyértelmű!
1. Visual Studio telepítve: Szüksége lesz a Visual Studiora vagy bármely más .NET fejlesztői környezetre.
2.  Aspose.Cells for .NET: Megteheti[töltse le a legújabb verziót](https://releases.aspose.com/cells/net/) vagy használja a NuGet csomagkezelőt a telepítéshez.
3. .NET-keretrendszer: Győződjön meg arról, hogy telepítve van a .NET-keretrendszer 4.0-s vagy újabb verziója.
4. A C# alapvető ismerete: A C# ismeretekkel simábbá teheti ezt az oktatóanyagot.
5. HTML-táblaadatok: Készítsen néhány HTML-tartalmat (akár egy alaptáblázatot is), amelyet be szeretne tölteni az Excelbe.
## Csomagok importálása
Az első dolog az első – a kezdéshez importáljuk a szükséges névtereket. Íme egy egyszerű lista arról, hogy mit kell importálnia:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Ezekkel a csomagokkal kezelheti a munkafüzetet, kezelheti a HTML-adatokat, és zökkenőmentesen betöltheti azokat Excelbe.
Bontsuk fel ezt a folyamatot kezelhető darabokra, hogy könnyen követhessük. Ennek végére egy működő példája lesz az oszlopok és sorok automatikus illesztésére, miközben betölti a HTML-t egy munkafüzetbe az Aspose.Cells for .NET segítségével.
## 1. lépés: Állítsa be a dokumentumkönyvtárat
A fájlok egyszerű mentése és visszakeresése érdekében megadjuk a dokumentumok tárolási útvonalát. A könyvtár elérési útját lecserélheti saját mappa helyére.
```csharp
string dataDir = "Your Document Directory";
```
Ez a sor beállítja azt a könyvtárat, ahová az Excel-fájlok mentésre kerülnek. Ha több projekten dolgozik, fontos a fájlok megfelelő rendszerezése. Képzelje el ezt a projekt iratszekrényeként!
## 2. lépés: Hozzon létre HTML-adatokat karakterláncként
Ezután meghatározunk néhány alapvető HTML-tartalmat. A példa kedvéért egy egyszerű HTML-táblázatot fogunk használni. Testreszabhatja a projekt igényei szerint.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Itt egy nagyon egyszerű HTML karakterláncot határozunk meg. Tartalmaz egy táblázatot néhány sorból és oszlopból. Igényei szerint további sorokat vagy oszlopokat adhat hozzá. Tekintsd úgy, mint az alapanyagok elkészítését étkezés előtt!
## 3. lépés: Töltse be a HTML karakterláncot a MemoryStreambe
 Most, hogy a HTML-tartalom készen áll, a következő lépés az, hogy betöltjük a memóriába`MemoryStream`. Ez lehetővé teszi számunkra, hogy anélkül kezeljük a memóriában lévő HTML-tartalmat, hogy azt először lemezre mentenék.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 A HTML karakterlánc bájttömbbé alakításával és a`MemoryStream`, dolgozhatunk a memóriában lévő HTML adatokkal. Képzelje el ezt a lépést úgy, hogy az ételt egy edényben készíti el, mielőtt a sütőbe tenné!
## 4. lépés: A MemoryStream betöltése egy munkafüzetbe (automatikus illesztés nélkül)
 Miután megvan a HTML-tartalom a memóriában, betöltjük egy Aspose-ba`Workbook`Jelenleg még nem illesztjük automatikusan az oszlopokat és a sorokat. Ez a mi „előtte” forgatókönyvünk, hogy később összehasonlíthassuk az automatikusan beépített változattal.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
A munkafüzet betöltődik a HTML-tartalommal, de az oszlopok és sorok még nem illeszkednek automatikusan a szöveghez. Tekintse ezt úgy, mintha süteményt sütne, de elfelejtené ellenőrizni a hőmérsékletet – működik, de lehet, hogy nem tökéletes!
## 5. lépés: Adja meg a HTML-betöltési beállításokat az automatikus illeszkedés engedélyezésével
 Nos, itt a varázslat! Létrehozunk egy példányt`HtmlLoadOptions` és engedélyezze a`AutoFitColsAndRows` ingatlan. Ez biztosítja, hogy a HTML-tartalom betöltésekor az oszlopok és sorok igazodjanak a bennük lévő tartalomhoz.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Az opció beállításával azt utasítjuk az Aspose.Cells-re, hogy automatikusan átméretezze a sorokat és oszlopokat. Képzelje el ezt úgy, hogy a sütőt a tökéletes hőmérsékletre állítja be, hogy a sütemény megfelelően megkeljen!
## 6. lépés: Töltsön be HTML-t a munkafüzetbe automatikus illesztéssel
 Most újra betöltjük a HTML tartalmat, de ezúttal a`AutoFitColsAndRows`opció engedélyezve. Ezzel beállítja az oszlopok szélességét és a sorok magasságát a bennük lévő tartalom alapján.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Ez a lépés betölti a HTML-tartalmat egy új munkafüzetbe, és Excel-fájlként menti, de most az oszlopok és sorok automatikusan illeszkednek! Tekintsd ezt a tökéletesen sült süteménynek, ahol minden a megfelelő méretű.
## Következtetés
Ezeket az egyszerű lépéseket követve megtanulta, hogyan tölthet be HTML-tartalmat egy munkafüzetbe az Aspose.Cells for .NET használatával, és hogyan illesztheti automatikusan az oszlopokat és sorokat. Ez biztosítja, hogy Excel-lapjai mindig jól nézzenek ki, függetlenül attól, hogy milyen dinamikus a tartalom. Ez egy egyszerű, de hatékony funkció, amellyel rengeteg időt takaríthat meg az Excel-adatok formázása és rendszerezése során.
Most, hogy rendelkezik ezzel a tudással, kísérletezhet bonyolultabb HTML-tartalommal, stílust adhat hozzá, és akár teljes Excel-munkafüzeteket is készíthet weboldalakból!
## GYIK
### Használhatom ezt a módszert nagy HTML táblák betöltésére?
Igen, az Aspose.Cells hatékonyan kezeli a nagy HTML-táblázatokat, de az optimális teljesítmény érdekében ajánlatos az adatmérettel tesztelni.
### Alkalmazhatok bizonyos oszlopszélességeket és sormagasságokat manuálisan az automatikus illesztés után?
Teljesen! Az egyes oszlopokat és sorokat az automatikus illesztés funkció használata után is személyre szabhatja.
### Hogyan alakíthatom ki a táblázatot a HTML betöltése után?
A HTML betöltése után stílusokat alkalmazhat az Aspose.Cells kiterjedt stílusbeállításaival.
### Az Aspose.Cells for .NET kompatibilis a .NET-keretrendszer régebbi verzióival?
Igen, az Aspose.Cells for .NET támogatja a .NET Framework 4.0-s és újabb verzióit.
### A HTML-en kívül más típusú tartalmat is betölthetek az Excelbe az Aspose.Cells használatával?
Igen, az Aspose.Cells támogatja a különféle formátumok, például CSV, JSON és XML betöltését Excelbe.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
