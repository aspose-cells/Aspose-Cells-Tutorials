---
title: Hozzon létre PDF diagramot a kívánt oldalmérettel
linktitle: Hozzon létre PDF diagramot a kívánt oldalmérettel
second_title: Aspose.Cells .NET Excel Processing API
description: Hozzon létre egy PDF-fájlt az Excel diagramjával az Aspose.Cells for .NET segítségével. Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan.
weight: 12
url: /hu/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hozzon létre PDF diagramot a kívánt oldalmérettel

## Bevezetés

A vizuálisan tetszetős és informatív diagramok készítése elengedhetetlen az adatok megjelenítéséhez különböző területeken. Legyen szó értékesítési adatokról, teljesítménymutatókról vagy bármilyen más információról, a kiváló minőségű diagramok készítésének képessége mélységet és egyértelműséget ad az eredményeknek. Ha .NET-alkalmazásokkal dolgozik, az Aspose.Cells egy olyan hatékony könyvtár, amely az Excel-dokumentumok kezelését és a diagramok létrehozását gyerekjáték. Ebben az oktatóanyagban végigvezetjük Önt a kívánt oldalméretű Excel-fájlból PDF-fájl létrehozásának folyamatán.

## Előfeltételek

Mielőtt belemerülne a kódba, meg kell felelnie néhány előfeltételnek a zavartalan élmény érdekében:

### C# és .NET alapszintű ismerete

Szüksége lesz a C# programozás és a .NET keretrendszer alapvető ismereteire. Ez segít megérteni a kód szerkezetét, amellyel ebben az útmutatóban találkozni fog.

### Aspose.Cells for .NET

Győződjön meg arról, hogy az Aspose.Cells for .NET telepítve van. Minden részletet megtalálsz a[Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/). 

### Fejlesztési környezet

 Állítsa be a fejlesztői környezetet. Ez lehet a Visual Studio vagy bármely más C#-t támogató IDE. Töltse le és telepítse az Aspose.Cells könyvtárat a[letöltési oldal](https://releases.aspose.com/cells/net/).

### Minta Excel fájl

Szüksége lesz egy minta Excel-fájlra, amely legalább egy diagramot tartalmaz. Létrehozhat egy mintafájlt, vagy letölthet egyet az oktatóanyagban való használatra.

## Csomagok importálása

Az Aspose.Cells használatának megkezdéséhez importálnia kell a szükséges névtereket a C# alkalmazásba. Íme, hogyan kell ezt megtenni:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Ezek a névterek hozzáférést biztosítanak az Excel-munkafüzetek és tartalmuk kezeléséhez szükséges osztályokhoz és metódusokhoz.

Most, hogy minden előfeltételt megoldottunk, bontsuk le a folyamatot részletes lépésekre.

## 1. lépés: Állítsa be a kimeneti és forráskönyvtárakat

Kezdésként meg kell határoznia, hogy a kimeneti PDF hova kerüljön mentésre, és hol található a forrás Excel-dokumentum.

```csharp
//Kimeneti könyvtár
string outputDir = "Your Output Directory";

//Forrás könyvtár
string sourceDir = "Your Document Directory";
```

Ügyeljen arra, hogy a "Saját kimeneti könyvtár" és a "Dokumentumkönyvtár" helyére cserélje ki a rendszer tényleges elérési útját. Ez határozza meg, hogy az Aspose hova mentse a létrehozott PDF-fájlt, és hol találja meg az Excel-fájlt.

## 2. lépés: Töltse be az Excel mintafájlt

Ezután be kell töltenie a diagramot tartalmazó Excel-fájlt. Íme, hogyan:

```csharp
//Töltse be a diagramot tartalmazó Excel mintafájlt.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 A`Workbook` osztály központi szerepet játszik az Excel dokumentummal való interakcióban. Győződjön meg arról, hogy az elérési út helyesen mutat az Excel-fájlra – egy hiba megakadályozza a kód többi részének végrehajtását.

## 3. lépés: Nyissa meg az első munkalapot

A munkafüzet betöltése után a következő lépés a kívánt diagramot tartalmazó munkalap elérése.

```csharp
//Az első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```

 Az Aspose.Cells-ben a munkalapok nullától kezdve indexelve vannak, tehát`Worksheets[0]` az első lapra vonatkozik.

## 4. lépés: Nyissa meg az első diagramot

Most pedig nyissa meg a PDF-be exportálni kívánt diagramot. Ez a lépés feltételezi, hogy a munkalap legalább egy diagramot tartalmaz.

```csharp
//Hozzáférés az első diagramhoz a munkalapon belül.
Chart ch = ws.Charts[0];
```

Ez ismét eléri a munkalap első diagramját; győződjön meg arról, hogy a munkalap szerkezete megfelel ennek a megközelítésnek.

## 5. lépés: Hozzon létre PDF-et a kívánt oldalmérettel

Végül itt az ideje elkészíteni a PDF-et a diagramból egy megadott oldalmérettel. Íme a varázslatos kódsor, amely mindent megtesz:

```csharp
//Készítsen pdf grafikont a kívánt oldalmérettel.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

Ebben a kódban:
- A PDF a korábban megadott kimeneti könyvtárba kerül mentésre.
-  A számok`7, 7` a kívánt oldalméret szélességét és magasságát jelzik.
- A PageLayoutAlignmentType.Center biztosítja, hogy a diagram az oldal közepén legyen.

## 6. lépés: Megerősítő üzenet

Ha szeretné tudatni magát (és másokkal), hogy minden gördülékenyen ment, írjon egy megerősítő üzenetet a kód végére:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Ez az üzenet jelenik meg a konzol ablakában, amint a folyamat befejeződött, jelezve, hogy a PDF-fájl gond nélkül elkészült.

## Következtetés

Gratulálok! Most tanulta meg, hogyan használhatja az Aspose.Cells for .NET-et PDF-fájl létrehozásához egy Excel-fájlban található diagramból. Ez a nagy teljesítményű könyvtár leegyszerűsíti az Excel-dokumentumok kezelésének és az adatok vizuális megjelenítésének folyamatát, így órákat takarít meg a kézi formázástól. Feltétlenül fedezze fel az Aspose.Cells által a PDF-generáláson túlmenően kínált egyéb funkciók sokaságát – soha nem tudhatja, mi javíthatja tovább projektjeit!

## GYIK

### Mire használható az Aspose.Cells for .NET?  
Az Aspose.Cells for .NET Excel-dokumentumok létrehozására, szerkesztésére és konvertálására szolgál programozottan .NET-alkalmazásokban.

### Használhatom ingyenesen az Aspose.Cells-t?  
 Igen, az Aspose.Cells a[ingyenes próbaverzió](https://releases.aspose.com/) értékelési célokra.

### Van mód a próbaidőszak meghosszabbítására a kezdeti időszakon túl?  
 Jelentkezni lehet a[ideiglenes engedély](https://purchase.aspose.com/temporary-license/) kiterjesztett tesztelésre.

### Mi a teendő, ha problémákba ütközöm, vagy kérdéseim vannak?  
 Segítséget kérhet az Aspose közösségtől[támogatási fórum](https://forum.aspose.com/c/cells/9).

### Hogyan vásárolhatom meg az Aspose.Cells-t?  
 Az Aspose.Cells-t megvásárolhatja a[vásárlási oldal](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
