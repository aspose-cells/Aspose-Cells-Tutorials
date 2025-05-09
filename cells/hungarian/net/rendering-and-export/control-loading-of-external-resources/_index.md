---
"description": "Fedezze fel, hogyan kezelheti a külső erőforrásokat az Excel PDF-be konvertálása során az Aspose.Cells for .NET használatával könnyen követhető útmutatónkkal."
"linktitle": "Külső erőforrások vezérlése Excelben PDF-be konvertálása Aspose.Cells-ben"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Külső erőforrások vezérlése Excelben PDF-be konvertálása Aspose.Cells-ben"
"url": "/hu/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Külső erőforrások vezérlése Excelben PDF-be konvertálása Aspose.Cells-ben

## Bevezetés
A mai digitális korban az Excel-táblázatok PDF-dokumentumokká konvertálása gyakori feladat. Akár jelentéseket, pénzügyi adatokat vagy prezentációs anyagokat készít, biztosítani szeretné, hogy a PDF-fájlok pontosan úgy nézzenek ki, ahogyan szeretné. Az Aspose.Cells for .NET egy robusztus könyvtár, amely lehetővé teszi a konvertálási folyamat legapróbb részleteinek szabályozását, különösen az Excel-fájlokat kísérő külső erőforrások, például képek kezelésekor. Ebben az útmutatóban elmerülünk abban, hogyan szabályozhatja a külső erőforrásokat az Excel PDF-vé konvertálási folyamata során az Aspose.Cells segítségével. Tehát, fogja meg kedvenc italát, és kezdjük is!
## Előfeltételek
Mielőtt belevágnánk a lényegbe, győződjünk meg róla, hogy minden megvan, amire szükséged van a kezdéshez. Íme egy gyors ellenőrzőlista:
1. Visual Studio vagy bármilyen .NET-kompatibilis IDE: Szükséged lesz egy környezetre a kódod írásához és teszteléséhez.
2. Aspose.Cells .NET-hez: Ha még nem telepítetted, látogass el a következő oldalra: [Aspose letöltések](https://releases.aspose.com/cells/net/) oldalt, és töltsd le a legújabb verziót.
3. C# alapismeretek: A C# programozási nyelv ismerete hasznos lesz. Ha bizonytalan vagy valamelyik koncepcióban, ne habozz utánanézni.
4. Minta Excel-fájl: Készítsen elő egy Excel-fájlt, amely tartalmazza a konvertálni kívánt külső erőforrásokat. Használhatja a mellékelt "samplePdfSaveOptions_StreamProvider.xlsx" mintafájlt.
5. Egy képfájl teszteléshez: Ez külső erőforrásként lesz használva a konvertálás során. A "newPdfSaveOptions_StreamProvider.png" képfájl jó helykitöltő.
## Csomagok importálása
kezdéshez importálnod kell a szükséges névtereket az Aspose.Cells könyvtárból. Ez elengedhetetlen a funkcióinak eléréséhez. Ügyelj arra, hogy a fájl elejére add hozzá a következő direktívákat:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Ezek a csomagok minden alapvető osztályt és metódust biztosítanak, amire szükséged lesz a feladataid elvégzéséhez.
## 1. lépés: Hozza létre a streamszolgáltató osztályát
Az első teendő egy olyan stream szolgáltató osztály létrehozása, amely megvalósítja a következőt: `IStreamProvider` interfész. Ez az osztály lehetővé teszi a külső erőforrások betöltésének szabályozását.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Olvassa be az új képet egy memóriafolyamból, és rendelje hozzá a Stream tulajdonsághoz.
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Ebben az osztályban:
- CloseStream: Ez a metódus akkor kerül meghívásra, amikor a stream lezárul. Egyelőre csak egy hibakeresési üzenetet írunk a követéshez.
- InitStream: Itt kezdődik a varázslat. Itt bájttömbként olvasod be a külső képfájlt, memóriafolyammá alakítod, és hozzárendeled a `options.Stream` ingatlan.
## 2. lépés: Forrás- és kimeneti könyvtárak beállítása
Most, hogy a streamelési szolgáltatód készen áll, itt az ideje meghatározni, hogy hol található az Excel-fájlod, és hová szeretnéd menteni a PDF-et.
```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
Egyszerűen cserélje ki `"Your Document Directory"` a számítógépeden található tényleges elérési úttal. A fájlok rendszerezése kulcsfontosságú!
## 3. lépés: Töltse be az Excel-fájlt
Ezután betöltöd azt az Excel fájlt, amelyből a PDF-et létre szeretnéd hozni.
```csharp
// Külső képeket tartalmazó forrás Excel fájl betöltése
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Mi használjuk a `Workbook` osztály az Aspose.Cells fájlból, amely az Excel-fájlodat jelöli. A fájl tartalmazhat különféle külső erőforrásokat, például képeket, amelyeket a konvertálás során vezérelni szeretnél.
## 4. lépés: PDF mentési beállítások megadása
Mielőtt PDF formátumban mentené a munkafüzetet, adja meg, hogyan szeretné menteni. Ezeket a beállításokat az igényeinek megfelelően módosíthatja.
```csharp
// PDF mentési beállítások megadása – Stream szolgáltató
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Minden munkalap mentése új oldalra
```
Itt létrehozunk egy új példányt a következőből: `PdfSaveOptions`amely lehetővé teszi a PDF formátumának testreszabását. `OnePagePerSheet` Ez a beállítás hasznos annak biztosítására, hogy minden Excel-lap külön oldalt kapjon a végső PDF-ben.
## 5. lépés: A streamszolgáltató hozzárendelése
Miután beállítottad a PDF-beállításaidat, meg kell mondanod az Aspose-nak, hogy a külső forrásokhoz az egyéni streamszolgáltatódat használja.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Ez a vonal összeköti Önt `Workbook` például a `MyStreamProvider` korábban létrehozott osztály. Ez azt jelenti, hogy amikor a konvertálás során külső erőforrásokba ütközik, a szolgáltató a megadott módon fogja kezelni azokat.
## 6. lépés: Mentse el a munkafüzetet PDF formátumban
Miután minden készen állt, végre itt az ideje, hogy PDF formátumban mentse az Excel-munkafüzetet.
```csharp
// Munkafüzet mentése PDF formátumban
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Azzal, hogy felhívja a `Save` metódust a munkafüzet objektumon, és átadja a kimeneti könyvtárat a PDF-beállításokkal együtt, akkor az Excel-fájlt egy szépen formázott PDF-vé alakítja.
## 7. lépés: A sikeres végrehajtás megerősítése
Összefoglalva, mindig jó érzés megerősíteni, hogy a folyamat sikeres volt!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
konzolra kiírt sikerüzenet segít tájékozódni a művelet állapotáról. Jó szokás, ha ezeket a kis visszaigazolásokat beilleszted a kódodba.
## Következtetés
Íme, itt van! Ezeket az egyszerű lépéseket követve szakértőként szabályozhatod, hogy a külső erőforrások hogyan kezelődnek az Excelből PDF-be konvertálás során az Aspose.Cells segítségével. Ez azt jelenti, hogy a dokumentumaid mostantól pontosan tartalmazhatnak képeket és más külső elemeket, így minden alkalommal kifinomult végeredményt biztosítva.
## GYIK
### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony függvénykönyvtár .NET fejlesztők számára, amely lehetővé teszi Excel fájlok létrehozását, kezelését, konvertálását és renderelését különböző formátumokban.
### Hogyan tölthetem le az Aspose.Cells fájlt?  
Az Aspose.Cells legújabb verzióját letöltheted innen: [Letöltési link](https://releases.aspose.com/cells/net/).
### Kipróbálhatom ingyen az Aspose.Cells-t?  
Igen! Ingyenes próbaverziót kaphatsz, ha ellátogatsz a következő oldalra: [Ingyenes próbaoldal](https://releases.aspose.com/).
### Hol találok támogatást az Aspose.Cells-hez?  
Bármilyen támogatással kapcsolatos kérdés esetén látogassa meg a következőt: [Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).
### Hogyan szerezhetek ideiglenes licencet az Aspose.Cells-hez?  
Ideiglenes jogosítványt lehet igényelni [itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}