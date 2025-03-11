---
title: Szövegmező-vezérlő hozzáadása a diagramhoz
linktitle: Szövegmező-vezérlő hozzáadása a diagramhoz
second_title: Aspose.Cells .NET Excel Processing API
description: Ismerje meg, hogyan adhat szövegdobozt az Excel diagramjaihoz az Aspose.Cells for .NET használatával. Fokozza az adatok megjelenítését erőfeszítés nélkül.
weight: 12
url: /hu/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szövegmező-vezérlő hozzáadása a diagramhoz

## Bevezetés

A dinamikus és tetszetős diagramok Excelben készítése fantasztikus módja az adatok hatékony ábrázolásának. Az egyik remek funkció, amelyet használhat, egy TextBox hozzáadása a diagramhoz. Az Aspose.Cells for .NET segítségével ez a feladat egyszerűvé és szórakoztatóvá válik! Ebben az útmutatóban lépésről lépésre végigvezetjük a TextBox diagramba való integrálásának folyamatán. Akár tapasztalt fejlesztő, akár most kezdő, ez az oktatóanyag minden olyan eszközt megad, amelyre szüksége van Excel-diagramjainak javításához. Szóval, készen állsz a merülésre?

## Előfeltételek

Mielőtt belevágnánk a kódolásba, van néhány dolog, amit a helyén kell tartani:

- C# alapvető ismerete: Hasznos lesz a C# programozás alapvető ismerete. Ne aggódj; nem kell szakértőnek lenni, csak kényelmesen eligazodni a szintaxisban.
-  Telepített Aspose.Cells Library: Győződjön meg arról, hogy telepítve van az Aspose.Cells for .NET könyvtár. Letöltheti innen[itt](https://releases.aspose.com/cells/net/) ha még nem tetted meg.
- Visual Studio: Alapvető fontosságú a Visual Studio vagy bármely olyan IDE ismerete, amelyet a .NET keretrendszerhez szeretne használni.
- Meglévő Excel-fájl: Ebben a példában egy "sampleAddingTextBoxControlInChart.xls" nevű meglévő Excel-fájllal fogunk dolgozni. Létrehozhat egyet, vagy letölthet egy mintát.

Most, hogy minden a helyén van, térjünk rá a kódolási részre!

## Csomagok importálása

Először is importálnunk kell a szükséges Aspose.Cells névtereket a C# projektünkbe. Ezt egyszerűen megteheti, ha a következő sorokat helyezi el a kódfájl tetején:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## 1. lépés: Határozza meg a forrás- és kimeneti könyvtárait

Mielőtt elkezdené dolgozni az Excel fájllal, fontos meghatározni, hogy hol található a bemeneti fájl, és hova szeretné menteni a kimeneti fájlt. Ez segít a projekt szervezettségében.

```csharp
// Forrás könyvtár
string sourceDir = "Your Document Directory";

// Kimeneti könyvtár
string outputDir = "Your Output Directory";
```
 Cserélje ki`"Your Document Directory"` és`"Your Output Directory"` a rendszer tényleges elérési útjaival.

## 2. lépés: Nyissa meg a meglévő Excel-fájlt

Ezután meg kell nyitnunk azt az Excel fájlt, amely a módosítani kívánt diagramot tartalmazza. Ez lehetővé teszi számunkra a diagram lekérését és a módosítások végrehajtását.

```csharp
// Nyissa meg a meglévő fájlt.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Ez a sor inicializál egy új munkafüzet objektumot a megadott fájlunkkal.

## 3. lépés: Nyissa meg a diagramot a munkalapon

Mivel az Excel diagramjai egy munkalapon belül vannak tárolva, először el kell érnünk a munkalapot, majd be kell szereznünk a kívánt diagramot. Ebben a példában az első munkalap első diagramját fogjuk elérni.

```csharp
// Szerezze be a tervezői diagramot az első lapon.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Az index értékének módosításával különböző munkalapokat vagy diagramokat választhat ki, ha a fájlban több van.

## 4. lépés: Adjon hozzá egy új szövegmezőt a diagramhoz

Most készen állunk a TextBox hozzáadására. Helyét és méretét a létrehozáskor adjuk meg.

```csharp
// Adjon hozzá egy új szövegmezőt a diagramhoz.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Ebben a parancsban a paraméterek határozzák meg a TextBox helyét (x, y) és méretét (szélesség, magasság) a diagramban. Módosítsa ezeket az értékeket sajátos elrendezési igényei szerint.

## 5. lépés: Állítsa be a TextBox szövegét

Ha a TextBox a helyére került, ideje megtölteni tartalommal. Bármilyen szöveget hozzáadhat a diagramhoz, amelyet szükségesnek tart.

```csharp
// Töltse ki a szöveget.
textbox0.Text = "Sales By Region";
```
Nyugodtan cserélje le az „Értékesítés régiónként” szöveget bármilyen, az adataira vonatkozó szöveggel.

## 6. lépés: Állítsa be a TextBox tulajdonságait

Most tegyük jól a TextBox-unkat! Testreszabhatja a különféle tulajdonságokat, például a betűtípus színét, méretét és stílusát.

```csharp
// Állítsa be a betűtípus színét.
textbox0.Font.Color = Color.Maroon; // Váltson a kívánt színre

// Állítsa a betűtípust félkövérre.
textbox0.Font.IsBold = true;

// Állítsa be a betűméretet.
textbox0.Font.Size = 14;

// A font attribútumot állítsa dőltre.
textbox0.Font.IsItalic = true;
```

Ezen sorok mindegyike módosítja a szöveg megjelenését a TextBoxban, javítva a láthatóságot és a vonzerőt.

## 7. lépés: Formázza meg a szövegdoboz megjelenését

A TextBox hátterének és szegélyének formázása is elengedhetetlen. Ez kiemeli a diagramon.

```csharp
// Szerezze meg a szövegdoboz kitöltési formátumát.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Szerezze be a szövegdoboz sorformátumának típusát.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Állítsa be a vonalvastagságot.
lineformat.Weight = 2;

// Állítsa a vonal stílusát tömörre.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Ezekkel az opciókkal beállíthatja a TextBox háttérkitöltését és testreszabhatja a keretét.

## 8. lépés: Mentse el a módosított Excel-fájlt

Az utolsó lépés az elvégzett módosítások mentése egy új Excel-fájlba. Ez biztosítja, hogy az eredeti fájl érintetlen maradjon.

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Cserélje ki`"outputAddingTextBoxControlInChart.xls"` a kívánt fájlnévvel.

## Következtetés

Gratulálok! Sikeresen hozzáadott egy TextBox vezérlőt egy diagramhoz az Aspose.Cells for .NET használatával. Ez az egyszerű, de hatékony változtatás informatívabbá és látványosabbá teheti diagramjait. Az adatok megjelenítése kulcsfontosságú a hatékony kommunikációhoz, és az olyan eszközökkel, mint az Aspose, minimális erőfeszítéssel javíthatja ezt a prezentációt.

## GYIK

### Mi az Aspose.Cells a .NET számára?
Az Aspose.Cells for .NET egy hatékony könyvtár Excel-fájlok létrehozásához, kezeléséhez és konvertálásához anélkül, hogy a Microsoft Excelre kellene hagyatkoznia.

### Hozzáadhatok több szövegdobozt egyetlen diagramhoz?
Igen! Annyi TextBoxot adhat hozzá, amennyire szüksége van, ha megismétli a TextBox létrehozási lépéseit különböző pozíciókkal.

### Az Aspose.Cells ingyenesen használható?
Az Aspose.Cells egy fizetős könyvtár, de ingyenes próbaverziót is letölthet a webhelyről[itt](https://releases.aspose.com/).

### Hol találok további dokumentációt az Aspose.Cells-ről?
 Hozzáférhet az átfogó dokumentációhoz[itt](https://reference.aspose.com/cells/net/).

### Hogyan kaphatok támogatást, ha problémákba ütközöm?
 Az Aspose támogatási fórumán keresztül kérhet segítséget[itt](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
