---
title: Vezérelje a külső erőforrásokat az Excelből PDF-be az Aspose.Cells-ben
linktitle: Vezérelje a külső erőforrásokat az Excelből PDF-be az Aspose.Cells-ben
second_title: Aspose.Cells .NET Excel Processing API
description: Fedezze fel, hogyan vezérelheti a külső erőforrásokat az Excelben PDF-be az Aspose.Cells for .NET használatával a könnyen követhető útmutatónk segítségével.
weight: 12
url: /hu/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vezérelje a külső erőforrásokat az Excelből PDF-be az Aspose.Cells-ben

## Bevezetés
A mai digitális korban gyakori feladat az Excel-táblázatok PDF dokumentumokká konvertálása. Legyen szó jelentések, pénzügyi adatok vagy prezentációs anyagok készítéséről, biztosítani szeretné, hogy PDF-fájljai pontosan úgy nézzenek ki, ahogyan azt szeretné. Az Aspose.Cells for .NET egy robusztus könyvtár, amely lehetővé teszi ennek az átalakítási folyamatnak a legapróbb részletéig történő irányítását, különösen az Excel-fájlokat kísérő külső erőforrások, például képek kezelésekor. Ebben az útmutatóban azt mutatjuk be, hogyan irányítható a külső erőforrások az Aspose.Cells segítségével az Excelből PDF-be átalakítási folyamat során. Fogja meg tehát kedvenc italát, és kezdjük is!
## Előfeltételek
Mielőtt belevágnánk a zűrzavarba, győződjünk meg arról, hogy minden megvan, ami a gördüléshez szükséges. Íme egy gyors ellenőrző lista:
1. Visual Studio vagy bármely .NET-kompatibilis IDE: Szüksége lesz egy környezetre a kód írásához és teszteléséhez.
2.  Aspose.Cells for .NET: Ha még nem telepítette, menjen a következőhöz[Aspose letöltések](https://releases.aspose.com/cells/net/) oldalt, és töltse le a legújabb verziót.
3. Alapvető C# ismerete: Hasznos lesz a C# programozási nyelv ismerete. Ha nem biztos a fogalomban, ne habozzon utánanézni.
4. Minta Excel-fájl: Készítsen Excel-fájlt bármilyen külső erőforrással, amelyet konvertálni szeretne. Használhatja a mellékelt „samplePdfSaveOptions_StreamProvider.xlsx” mintafájlt.
5. Képfájl tesztelésre: Ez külső erőforrásként lesz használva az átalakítás során. A "newPdfSaveOptions_StreamProvider.png" képfájl jó helyőrző.
## Csomagok importálása
dolgok elindításához importálnia kell a szükséges névtereket az Aspose.Cells könyvtárból. Ez kulcsfontosságú a funkcióinak eléréséhez. Ügyeljen arra, hogy a fájl tetején található direktívák használatával adja hozzá a következőket:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Ezek a csomagok biztosítják az összes alapvető osztályt és metódust, amelyre a feladatok elvégzéséhez szüksége lesz.
## 1. lépés: Hozd létre a Stream Provider osztályodat
 Az első feladat egy adatfolyam-szolgáltató osztály létrehozása, amely megvalósítja a`IStreamProvider` felület. Ez az osztály lehetővé teszi a külső erőforrások betöltésének szabályozását.
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
        // Olvassa be az új képet egy memóriafolyamban, és rendelje hozzá a Stream tulajdonsághoz
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Ebben az osztályban:
- CloseStream: Ez a metódus a folyam bezárásakor kerül meghívásra. Egyelőre csak egy hibakeresési üzenetet írunk a követéshez.
-  InitStream: Itt kezdődik a varázslat. Itt beolvassa a külső képfájlt bájttömbként, átalakítja memóriafolyammá, és hozzárendeli a`options.Stream` ingatlan.
## 2. lépés: Állítsa be a forrás- és kimeneti könyvtárakat
Most, hogy az adatfolyam-szolgáltató készen áll, ideje meghatározni, hol található az Excel-fájl, és hova szeretné menteni a PDF-fájlt.
```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";
// Kimeneti könyvtár
string outputDir = "Your Document Directory";
```
 Egyszerűen cserélje ki`"Your Document Directory"` a tényleges elérési úttal a számítógépen, ahol a fájlok találhatók. A fájlok rendszerezése kulcsfontosságú!
## 3. lépés: Töltse be az Excel fájlt
Ezután töltse be azt az Excel-fájlt, amelyből létre kívánja hozni a PDF-fájlt.
```csharp
// Töltse be a külső képeket tartalmazó Excel forrásfájlt
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Használjuk a`Workbook` osztályt az Aspose.Cellsből, amely az Ön Excel-fájlját képviseli. A fájl különféle külső forrásokat, például képeket tartalmazhat, amelyeket az átalakítás során vezérelni szeretne.
## 4. lépés: Állítsa be a PDF mentési beállításokat
Mielőtt a munkafüzetet PDF formátumban menti, adja meg, hogyan szeretné menteni. Ezeket a beállításokat igényei szerint módosíthatja.
```csharp
// Adja meg a Pdf mentési beállításokat – Stream Provider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Mentse el az egyes lapot egy új oldalra
```
 Itt egy új példányt hozunk létre`PdfSaveOptions` , amely lehetővé teszi a PDF formátumának testreszabását. A`OnePagePerSheet`Az opció praktikus annak biztosítására, hogy minden Excel-lap külön oldalt kapjon a végső PDF-ben.
## 5. lépés: Jelölje ki az adatfolyam-szolgáltatót
A beállított PDF-beállítások esetén meg kell mondania az Aspose-nak, hogy az egyéni adatfolyam-szolgáltatót használja külső erőforrásokhoz.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Ez a vonal köti össze`Workbook` példa a`MyStreamProvider` korábban létrehozott osztályt. Ez azt jelenti, hogy valahányszor külső erőforrásokkal találkozik az átalakítás során, a szolgáltató a megadott módon kezeli azokat.
## 6. lépés: Mentse el a munkafüzetet PDF formátumban
Ha mindent beállított, végre eljött az ideje, hogy PDF-ként mentse az Excel-munkafüzetet.
```csharp
// Mentse el a munkafüzetet PDF-be
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Felhívva a`Save` metódussal a munkafüzet objektumon, és átadja a kimeneti könyvtárat a PDF-beállításokkal együtt, akkor az Excel-fájlt gyönyörűen formázott PDF-fájllá konvertálja.
## 7. lépés: Erősítse meg a sikeres végrehajtást
A dolgok lezárásaként mindig jó megerősíteni, hogy a folyamat sikeres volt!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
sikerüzenet kinyomtatása a konzolra segít folyamatosan tájékoztatni a művelet állapotáról. Jó szokás, hogy ezeket az apró megerősítéseket belefoglalja a kódjába.
## Következtetés
Megvan! Ha követi ezeket az egyszerű lépéseket, az Aspose.Cells segítségével szakszerűen szabályozhatja a külső erőforrások kezelését az Excel PDF-be konvertálása során. Ez azt jelenti, hogy a dokumentumok most már pontosan tartalmazhatnak képeket és egyéb külső elemeket, így minden alkalommal csiszolt végterméket biztosítanak.
## GYIK
### Mi az Aspose.Cells?  
Az Aspose.Cells egy hatékony könyvtár .NET-fejlesztők számára, amely lehetővé teszi Excel-fájlok létrehozását, kezelését, konvertálását és renderelését különféle formátumokban.
### Hogyan tölthetem le az Aspose.Cells-t?  
 Letöltheti az Aspose.Cells legújabb verzióját a[Letöltési link](https://releases.aspose.com/cells/net/).
### Kipróbálhatom az Aspose.Cells-t ingyen?  
 Igen! Ingyenes próbaverziót kaphat, ha felkeresi a[Ingyenes próbaoldal](https://releases.aspose.com/).
### Hol találok támogatást az Aspose.Cells számára?  
 Bármilyen támogatással kapcsolatos kérdés esetén keresse fel a[Aspose támogatási fórum](https://forum.aspose.com/c/cells/9).
### Hogyan szerezhetek ideiglenes licencet az Aspose.Cells számára?  
 Ideiglenes jogosítványt igényelhet[itt](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
