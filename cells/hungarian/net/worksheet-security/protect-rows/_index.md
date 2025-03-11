---
title: Védje a sorokat a munkalapon az Aspose.Cells használatával
linktitle: Védje a sorokat a munkalapon az Aspose.Cells használatával
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan védheti meg Excel-munkalapok sorait az Aspose.Cells for .NET használatával. Biztosítsa adatait sorszintű védelemmel, és megakadályozza a véletlen módosításokat.
weight: 18
url: /hu/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Védje a sorokat a munkalapon az Aspose.Cells használatával

## Bevezetés
Az Excel fájlokkal programozott munkavégzés gyakran olyan feladat, amely nemcsak adatkezelést, hanem adatvédelmet is igényel. Függetlenül attól, hogy meg kell védenie az érzékeny adatokat, vagy meg kell akadályoznia a véletlen szerkesztést, a munkalapok sorainak védelme kulcsfontosságú lépés lehet. Ebben az oktatóanyagban megtudjuk, hogyan védhetjük meg az Excel-munkalap egyes sorait az Aspose.Cells for .NET használatával. Végigsétálunk minden szükséges lépésen, a környezet előkészítésétől a védelmi funkciók egyszerű, könnyen követhető megvalósításáig.
## Előfeltételek
Mielőtt elkezdené védeni a sorokat a munkalapon, néhány dolgot meg kell tennie:
1.  Aspose.Cells for .NET: Győződjön meg arról, hogy az Aspose.Cells for .NET telepítve van a fejlesztői gépén. Ha még nem tette meg, egyszerűen letöltheti a webhelyről[Aspose Cells letöltési oldal](https://releases.aspose.com/cells/net/).
2. Visual Studio vagy bármilyen .NET IDE: A megoldás megvalósításához be kell állítani egy fejlesztői környezetet. A Visual Studio nagyszerű lehetőség, de bármely .NET-kompatibilis IDE működik.
3. Alapvető C# ismeretek: A C# programozás alapjainak megértése segít követni az oktatóanyagot, és az igényeinek megfelelően módosítani a példakódot.
4.  Aspose.Cells API dokumentáció: Ismerkedjen meg a[Aspose.Cells a .NET dokumentációhoz](https://reference.aspose.com/cells/net/) hogy áttekintést kapjunk a könyvtárban használt osztálystruktúráról és metódusokról.
Ha minden készen áll az előfeltételekkel, azonnal belevághatunk a megvalósításba.
## Csomagok importálása
A kezdéshez importálnia kell a szükséges csomagokat. Ezek a könyvtárak kulcsfontosságúak az Excel-fájlokkal való interakcióhoz a C#-projektben.
```csharp
using System.IO;
using Aspose.Cells;
```
Miután importálta a szükséges csomagokat, elkezdheti a kódolást. 
Most bontsuk le a folyamatot kisebb lépésekre, hogy rendkívül könnyen követhető legyen. Minden lépés a megvalósítás egy meghatározott részére összpontosít, biztosítva, hogy gyorsan megértse és alkalmazza. 
## 1. lépés: Hozzon létre egy új munkafüzetet és munkalapot
Mielőtt bármilyen védelmi beállítást alkalmazna, létre kell hoznia egy új munkafüzetet, és ki kell választania azt a munkalapot, amellyel dolgozni szeretne. Ez lesz az Ön munkadokumentuma.
```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
// Hozzon létre könyvtárat, ha még nincs jelen.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Hozzon létre egy új munkafüzetet.
Workbook wb = new Workbook();
// Hozzon létre egy munkalap objektumot, és szerezze be az első lapot.
Worksheet sheet = wb.Worksheets[0];
```
Ebben a példában egy új munkafüzetet hozunk létre egyetlen munkalappal (ez az alapértelmezett beállítás, amikor új munkafüzetet hoz létre az Aspose.Cells használatával). Ezután megragadjuk a munkafüzet első munkalapját, amely a sorvédelem célpontja lesz.
## 2. lépés: Stílus és StyleFlag objektumok meghatározása
A következő lépés a stílus és a stílusjelző objektumok meghatározása. Ezekkel az objektumokkal módosíthatja a cella tulajdonságait, például azt, hogy zárolva van-e vagy feloldva.
```csharp
// Határozza meg a stílusobjektumot.
Style style;
// Határozza meg a styleflag objektumot.
StyleFlag flag;
```
Ezeket az objektumokat a későbbi lépésekben fogja használni a cellatulajdonságok testreszabásához és a munkalapon való alkalmazásához.
## 3. lépés: Oldja fel a munkalap összes oszlopát
Alapértelmezés szerint az Excel munkalap minden cellája zárolva van. Amikor azonban véd egy munkalapot, a zárolt állapot érvényesül. Annak biztosítása érdekében, hogy csak bizonyos sorok vagy cellák legyenek védettek, először feloldhatja az összes oszlop zárolását. Ez a lépés elengedhetetlen, ha csak bizonyos sorokat szeretne védeni.
```csharp
// Lapozzon át a munkalap összes oszlopán, és oldja fel őket.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 Ebben a kódban végigpörgetjük a munkalap mind a 256 oszlopát (az Excel munkalapok legfeljebb 256 oszlopot tartalmaznak, indexelve 0-tól 255-ig), és beállítjuk`IsLocked` tulajdonát`false`. Ez a művelet biztosítja, hogy minden oszlop feloldva legyen, de bizonyos sorokat később is zárolunk.
## 4. lépés: Zárja le az első sort
Miután feloldotta az oszlopok zárolását, a következő lépés a védeni kívánt sorok zárolása. Ebben a példában az első sort zároljuk. Ez biztosítja, hogy a felhasználók ne módosíthassák, amíg a többi sor zárolva marad.
```csharp
//Szerezze meg az első sor stílusát.
style = sheet.Cells.Rows[0].Style;
// Zárd be.
style.IsLocked = true;
//Példányosítsa a zászlót.
flag = new StyleFlag();
// Állítsa be a zár beállítását.
flag.Locked = true;
// Alkalmazza a stílust az első sorra.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Itt elérjük az első sor stílusát, és beállítjuk`IsLocked` tulajdonát`true` . Ezt követően használjuk a`ApplyRowStyle()` módszerrel alkalmazhatja a zárolási stílust a teljes sorra. Ezt a lépést megismételheti a többi védeni kívánt sor zárolásához.
## 5. lépés: Védje meg a lapot
Most, hogy feloldottuk és zároltuk a szükséges sorokat, ideje megvédeni a munkalapot. A védelem biztosítja, hogy senki ne módosíthassa a zárolt sorokat vagy cellákat, hacsak el nem távolítja a védelmi jelszót (ha van).
```csharp
// Védje a lapot.
sheet.Protect(ProtectionType.All);
```
 Ebben a lépésben a teljes lapra védelmet alkalmazunk`ProtectionType.All`. Ez a fajta védelem azt jelenti, hogy a lap minden aspektusa védett, beleértve a zárolt sorokat és cellákat is. Ezt a védelmet szükség esetén különböző védelmi típusok megadásával is testreszabhatja.
## 6. lépés: Mentse el a munkafüzetet
Végül el kell mentenünk a munkafüzetet a szükséges stílusok és védelem alkalmazása után. A munkafüzet különféle formátumokban menthető, például Excel 97-2003, Excel 2010 stb.
```csharp
// Mentse el az Excel fájlt.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Ez a kódsor Excel 97-2003 formátumban menti a munkafüzetet az alkalmazott módosításokkal. Igényei szerint módosíthatja a fájlformátumot, ha több közül választhat`SaveFormat` opciók.
## Következtetés
És megvan! Sikeresen megtanulta, hogyan védheti meg a munkalap sorait az Aspose.Cells for .NET használatával. A fenti lépések követésével szükség szerint feloldhatja vagy zárolhatja a sorokat vagy oszlopokat, és védelmet alkalmazhat az adatok integritásának biztosítása érdekében.
## GYIK
### Hogyan védhetek több sort egyszerre?  
 Több soron is átléphet, és mindegyikre külön-külön alkalmazhatja a zárolási stílust. Egyszerűen cserélje ki`0` a zárolni kívánt sorindexszel.
### Beállíthatok jelszót a lapvédelemhez?  
 Igen! Jelszót adhat át a`sheet.Protect()` módszer a jelszavas védelem érvényesítésére.
### Feloldhatom a cellák zárolását a teljes oszlopok helyett?  
Igen! Az oszlopok feloldása helyett az egyes cellák zárolását a stílustulajdonságok módosításával oldhatja fel.
### Mi történik, ha megpróbálok szerkeszteni egy védett sort?  
Ha egy sor védett, az Excel megakadályozza a zárolt cellák szerkesztését, hacsak nem szünteti meg a munkalap védelmét.
### Egymás után védhetek bizonyos tartományokat?  
 Igen! Egyes tartományokat sorban zárolhat a beállításával`IsLocked` tulajdonság a tartományon belüli meghatározott cellákhoz.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
