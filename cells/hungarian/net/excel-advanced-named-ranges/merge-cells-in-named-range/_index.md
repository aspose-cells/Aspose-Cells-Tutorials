---
title: Cellák egyesítése az Excel elnevezett tartományában
linktitle: Cellák egyesítése az Excel elnevezett tartományában
second_title: Aspose.Cells .NET Excel Processing API
description: Ebben a lépésenkénti oktatóanyagban megtudhatja, hogyan egyesíthet cellákat egy elnevezett tartományban az Aspose.Cells for .NET használatával. Fedezze fel, hogyan formázhat, stílusozhat és automatizálhat Excel-jelentéseket.
weight: 11
url: /hu/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cellák egyesítése az Excel elnevezett tartományában

## Bevezetés

Amikor programozottan dolgozik Excel-fájlokkal, az egyik gyakori feladat a cellák összevonása egy elnevezett tartományon belül. Akár automatizálja a jelentéskészítést, akár irányítópultokat készít, akár egyszerűen csak nagy adatkészleteket kezel, a cellák összevonása elengedhetetlen technika. Ebben az oktatóanyagban megvizsgáljuk, hogyan egyesíthet cellákat egy elnevezett tartományban az Aspose.Cells for .NET használatával – egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy a Microsoft Excel telepítése nélkül kezeljék az Excel fájlokat.

## Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy készen áll a következőkre:

-  Aspose.Cells for .NET: Letöltheti a[Az Aspose.Cells kiadási oldala](https://releases.aspose.com/cells/net/).
- .NET Framework telepítve van a gépére.
- A C# alapvető ismerete: Az olyan fogalmak ismerete, mint az osztályok, módszerek és objektumok, segít.

## Csomagok importálása

Mielőtt belevágnánk a kódolásba, importálnia kell a szükséges névtereket. Ezek a névterek hozzáférést biztosítanak az Aspose.Cells könyvtár funkcióihoz.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Miután az előfeltételek és a csomagok nincsenek útban, térjünk át a szórakoztató részre: a kódolásra!

Az alábbiakban bemutatjuk, hogyan egyesítheti egy elnevezett tartományban lévő cellákat egy Excel-lapon az Aspose.Cells for .NET használatával.

## 1. lépés: Hozzon létre egy új munkafüzetet

Az első dolog, amire szükségünk van, egy munkafüzet. A munkafüzet az Excel kifejezésében egy Excel-fájl megfelelője. Hozzunk létre egyet.

```csharp
// Példányosítson egy új munkafüzetet.
Workbook wb1 = new Workbook();
```

Egy új munkafüzet inicializálásával egy üres Excel-fájl áll rendelkezésünkre, amely készen áll a manipulációra. Olyan, mintha egy üres vászonnal kezdenénk!

## 2. lépés: Nyissa meg az első munkalapot

Minden munkafüzet tartalmaz munkalapokat, és ebben az esetben az elsővel szeretnénk dolgozni. Fogjuk meg!

```csharp
// Szerezd meg az első munkalapot a munkafüzetben.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Gondoljon a munkalapra úgy, mint egy Excel-fájl egyes lapjaira, ahol a tényleges adatok találhatók. Alapértelmezés szerint a legelső lapot érjük el.

## 3. lépés: Hozzon létre egy cellatartományt

Most, hogy megvan a munkalapunk, ideje létrehozni egy tartományt. A tartomány egy cellatömbre utal, amely több sort és oszlopot is átfedhet.

```csharp
//Hozzon létre egy tartományt.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Itt a D6-tól az I12-ig terjedő cellákat választunk ki – ez a blokk több sort és oszlopot takar. Hamarosan összevonjuk ezt a választékot!

## 4. lépés: Nevezze el a tartományt

Egy tartomány elnevezése megkönnyíti a későbbi hivatkozást, különösen nagy adatkészletek kezelésekor.

```csharp
// Nevezze el a tartományt.
mrange.Name = "TestRange";
```

Ha ezt a tartományt "TestRange"-nek nevezzük el, akkor gyorsan lekérhetjük a kód későbbi részében, anélkül, hogy újra meg kellene adni a cellakoordinátákat.

## 5. lépés: Egyesítse a cellatartományt

Most pedig a varázslat – egyesítsük a sejteket az imént létrehozott tartományon belül!

```csharp
// Egyesítse a tartomány celláit.
mrange.Merge();
```

Ez a lépés az összes cellát D6-tól I12-ig egyetlen cellává egyesíti. Tökéletes olyan dolgokhoz, mint a címek vagy összefoglalók!

## 6. lépés: A megnevezett tartomány lekérése

A cellák egyesítése után érdemes lehet valamilyen formázást alkalmazni. Először vegyük elő a nevezett tartományunkat.

```csharp
// Szerezze meg a tartományt.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

A tartomány név szerinti lekérése lehetővé teszi további műveletek végrehajtását, például stílusok hozzáadását vagy adatok bevitelét.

## 7. lépés: Határozzon meg egy stílust az egyesített cellákhoz

Mit ér egy egyesített cella, ha nem néz ki csiszolt? Hozzon létre egy stílusobjektumot a szöveg igazításához, és alkalmazzon egy háttérszínt.

```csharp
// Stílusobjektum meghatározása.
Style style = wb1.CreateStyle();

// Állítsa be az igazítást.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Itt a szöveget vízszintesen és függőlegesen is középre igazítjuk, és világoskék (aqua) háttérszínt állítunk be. Stílusos, igaz?

## 8. lépés: Alkalmazza a stílust a tartományra

A stílus meghatározása után ideje alkalmazni az egyesített tartományra.

```csharp
// Hozzon létre egy StyleFlag objektumot.
StyleFlag flag = new StyleFlag();

// Állítsa be a relatív stílus attribútumot.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Alkalmazza a stílust a tartományra.
range1.ApplyStyle(style, flag);
```

 A`StyleFlag` megmondja az Aspose.Cells-nek, hogy mely stílustulajdonságokat kell alkalmazni – igazítást, árnyékolást stb. Ez részletesen szabályozza a stílus alkalmazásának módját.

## 9. lépés: Vigye be az adatokat az egyesített tartományba

Mit jelent a formázott tartomány tartalom nélkül? Adjunk hozzá egy kis szöveget.

```csharp
// Adatok bevitele a tartományba.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Ezzel az „Üdvözöljük az Aspose API-kban” szöveget egyesített tartományunk első cellájába helyezi. A cella egyesítésekor ez a szöveg a D6-tól I12-ig terjedő összes cellára kiterjed.

## 10. lépés: Mentse el az Excel fájlt

Végül mentsük el a munkafüzetet Excel fájlként.

```csharp
// Mentse el az Excel fájlt.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Itt a munkafüzet "outputMergeCellsInNamedRange.xlsx" néven kerül mentésre a megadott könyvtárba.

## Következtetés

És megvan! Sikeresen egyesítette a cellákat egy elnevezett tartományban, gyönyörű formázást alkalmazott, és még néhány adatot is bevitt – mindezt az Aspose.Cells for .NET segítségével. Akár a jelentések automatizálásán, akár az Excel-fájlok kezelésén dolgozik, akár csak új technikákat tanul, ez a lépésről lépésre ismertető útmutató megadja a szükséges alapot.

## GYIK

### Összevonhatok több nem összefüggő tartományt az Aspose.Cells-ben?  
Nem, csak az Aspose.Cells összefüggő celláit egyesítheti.

### Visszavonhatok egy összevonási műveletet programozottan?  
 Miután egyesítette a cellákat, a gombbal szüntetheti meg őket`UnMerge()` módszer az Aspose.Cells-ben.

### cellák egyesítése eltávolítja a bennük lévő adatokat?  
Ha az összevonás előtt van adat a cellákban, akkor a tartomány első cellájából származó adatokat megőrzi.

### Alkalmazhatok különböző stílusokat az egyesített tartományon belüli egyes cellákra?  
Nem, az egyesített tartomány egyetlen cellaként működik, így nem alkalmazhat különböző stílusokat az egyes cellákon belül.

### Hogyan érhetek el egy egyesített cellát egyesítés után?  
Egyesítés után továbbra is elérheti az egyesített cellát a bal felső sarokban található koordináták segítségével.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
