---
"description": "Tanuld meg, hogyan adhatsz hozzá szövegdobozt diagramokhoz Excelben az Aspose.Cells for .NET használatával. Fejleszd az adatvizualizációdat könnyedén."
"linktitle": "Szövegmező vezérlő hozzáadása a diagramhoz"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Szövegmező vezérlő hozzáadása a diagramhoz"
"url": "/hu/net/inserting-controls-in-charts/add-textbox-control-to-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szövegmező vezérlő hozzáadása a diagramhoz

## Bevezetés

dinamikus és vizuálisan vonzó diagramok létrehozása az Excelben fantasztikus módja az adatok hatékony ábrázolásának. Az egyik hasznos funkció, amit használhatsz, egy TextBox hozzáadása a diagramhoz. Az Aspose.Cells for .NET segítségével ez a feladat egyszerűvé és szórakoztatóvá válik! Ebben az útmutatóban lépésről lépésre végigvezetünk a TextBox diagramba való integrálásának folyamatán. Akár tapasztalt fejlesztő vagy, akár most kezded, ez az oktatóanyag minden szükséges eszközt megad az Excel-diagramjaid fejlesztéséhez. Szóval, készen állsz a belevágásra?

## Előfeltételek

Mielőtt belevágnánk a kódolásba, van néhány dolog, aminek a helyén kell lennie:

- C# alapismeretek: A C# programozás alapjainak ismerete hasznos lesz. Ne aggódj, nem kell szakértőnek lenned, elég, ha magabiztosan tudsz eligazodni a szintaxisban.
- Telepített Aspose.Cells könyvtár: Győződjön meg róla, hogy telepítve van az Aspose.Cells for .NET könyvtár. Letöltheti innen: [itt](https://releases.aspose.com/cells/net/) ha még nem tetted meg.
- Visual Studio: Elengedhetetlen a Visual Studio vagy bármely olyan IDE ismerete, amelyet a .NET keretrendszerhez használni szeretne.
- Egy meglévő Excel-fájl: Ebben a példában egy meglévő, „sampleAddingTextBoxControlInChart.xls” nevű Excel-fájllal fogunk dolgozni. Létrehozhat egyet, vagy letölthet egy mintát.

Most, hogy minden a helyén van, térjünk át a kódolásra!

## Csomagok importálása

Először is importálnunk kell a szükséges Aspose.Cells névtereket a C# projektünkbe. Ezt könnyen megteheted, ha a következő sorokat a kódfájl elejére illeszted:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## 1. lépés: A forrás- és kimeneti könyvtárak meghatározása

Mielőtt elkezdenénk dolgozni az Excel-fájllal, fontos meghatározni, hogy hol található a bemeneti fájl, és hová szeretnénk menteni a kimeneti fájlt. Ez segít a projekt rendszerezésében.

```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";

// Kimeneti könyvtár
string outputDir = "Your Output Directory";
```
Csere `"Your Document Directory"` és `"Your Output Directory"` a rendszeren található tényleges elérési utakkal.

## 2. lépés: Nyissa meg a meglévő Excel-fájlt

Ezután meg kell nyitnunk azt az Excel fájlt, amely a módosítani kívánt diagramot tartalmazza. Ez lehetővé teszi számunkra, hogy lekérjük a diagramot és módosításokat végezzünk.

```csharp
// Nyissa meg a meglévő fájlt.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Ez a sor inicializál egy új Workbook objektumot a megadott fájllal.

## 3. lépés: A diagram elérése a munkalapon

Mivel az Excelben a diagramok egy munkalapon belül tárolódnak, először a munkalapot kell elérnünk, majd a kívánt diagramot. Ebben a példában az első munkalap első diagramját fogjuk elérni.

```csharp
// Szerezd meg a tervezői táblázatot az első lapon.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Az indexérték módosításával kiválaszthat különböző munkalapokat vagy diagramokat, ha a fájlban több van.

## 4. lépés: Új szövegmező hozzáadása a diagramhoz

Most már készen állunk a szövegdoboz hozzáadására. A létrehozáskor meg fogjuk adni a helyét és a méretét.

```csharp
// Adjon hozzá egy új szövegdobozt a diagramhoz.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Ebben a parancsban a paraméterek határozzák meg a TextBox helyét (x, y) és méretét (szélesség, magasság) a diagramon belül. Módosítsa ezeket az értékeket az elrendezési igényei alapján.

## 5. lépés: Állítsa be a szövegmező szövegét

Miután a szövegmező a helyén van, itt az ideje, hogy kitöltse tartalommal. Bármilyen szöveget hozzáadhat, amelyet szükségesnek tart a diagramhoz.

```csharp
// Töltsd ki a szöveget.
textbox0.Text = "Sales By Region";
```
A „Sales By Region” részt nyugodtan lecserélheti bármilyen, az adataihoz kapcsolódó szövegre.

## 6. lépés: A szövegdoboz tulajdonságainak módosítása

Most pedig tegyük széppé a TextBox-unkat! Testreszabhatod a különböző tulajdonságokat, például a betűszínt, -méretet és -stílust.

```csharp
// Állítsa be a betűszínt.
textbox0.Font.Color = Color.Maroon; // Váltsd át a kívánt színre

// Állítsd a betűtípust félkövérre.
textbox0.Font.IsBold = true;

// Állítsa be a betűméretet.
textbox0.Font.Size = 14;

// Állítsd a betűtípus attribútumát dőltre.
textbox0.Font.IsItalic = true;
```

Ezen sorok mindegyike módosítja a szöveg megjelenését a TextBox-ban, növelve a láthatóságot és a vonzerőt.

## 7. lépés: A szövegmező megjelenésének formázása

A TextBox hátterének és szegélyének formázása is elengedhetetlen. Ettől kiemelkedik a diagramon.

```csharp
// A szövegmező kitöltési formátumának lekérése.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Szerezd meg a szövegdoboz sorformátum-típusát.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Állítsa be a vonalvastagságot.
lineformat.Weight = 2;

// Állítsd a kötőjel stílusát tömörre.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Ezekkel a beállításokkal beállíthatja a szövegmező hátterének kitöltését és testreszabhatja a szegélyét.

## 8. lépés: Mentse el a módosított Excel-fájlt

Az utolsó lépés a módosítások mentése egy új Excel-fájlba. Ez biztosítja, hogy az eredeti fájl érintetlen maradjon.

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
Csere `"outputAddingTextBoxControlInChart.xls"` bármilyen fájlnévvel, amit csak szeretnél.

## Következtetés

Gratulálunk! Sikeresen hozzáadott egy TextBox vezérlőt egy diagramhoz az Aspose.Cells for .NET használatával. Ez az egyszerű, mégis hatékony módosítás informatívabbá és vizuálisan vonzóbbá teheti diagramjait. Az adatábrázolás kulcsfontosságú a hatékony kommunikációhoz, és olyan eszközökkel, mint az Aspose, minimális erőfeszítéssel javíthatja ezt a prezentációt.

## GYIK

### Mi az Aspose.Cells .NET-hez?
Az Aspose.Cells for .NET egy hatékony függvénytár Excel fájlok létrehozásához, kezeléséhez és konvertálásához anélkül, hogy a Microsoft Excelre kellene hagyatkozni.

### Hozzáadhatok több szövegdobozt egyetlen diagramhoz?
Igen! Annyi szövegdobozt adhatsz hozzá, amennyire szükséged van, ha a szövegdoboz létrehozási lépéseit különböző pozíciókban ismételgeted.

### Ingyenesen használható az Aspose.Cells?
Az Aspose.Cells egy fizetős könyvtár, de letölthet egy ingyenes próbaverziót innen: [itt](https://releases.aspose.com/).

### Hol találok további dokumentációt az Aspose.Cells-ről?
Átfogó dokumentációhoz férhet hozzá [itt](https://reference.aspose.com/cells/net/).

### Hogyan kaphatok támogatást, ha problémákba ütközöm?
Segítséget kérhet az Aspose támogatási fórumán keresztül. [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}