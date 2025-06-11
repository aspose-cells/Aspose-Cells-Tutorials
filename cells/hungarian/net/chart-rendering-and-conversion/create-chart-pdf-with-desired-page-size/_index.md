---
"description": "Hozz létre egy PDF-et az Excel-diagramoddal az Aspose.Cells for .NET használatával. Tanuld meg, hogyan kell ezt tenni ebből a lépésről lépésre szóló útmutatóból."
"linktitle": "Diagram PDF létrehozása a kívánt oldalmérettel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Diagram PDF létrehozása a kívánt oldalmérettel"
"url": "/hu/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagram PDF létrehozása a kívánt oldalmérettel

## Bevezetés

A vizuálisan vonzó és informatív diagramok készítése elengedhetetlen az adatok ábrázolásához számos területen. Akár értékesítési adatokkal, teljesítménymutatókkal vagy bármilyen más típusú információval foglalkozik, a kiváló minőségű diagramok készítésének képessége mélységet és egyértelműséget biztosít az eredményekhez. Ha .NET alkalmazásokkal dolgozik, az Aspose.Cells egy hatékony könyvtár, amely megkönnyíti az Excel dokumentumok kezelését és a diagramok létrehozását. Ebben az oktatóanyagban végigvezetjük Önt egy diagram PDF-fájljának létrehozásának folyamatán egy Excel fájlból a kívánt oldalméretben.

## Előfeltételek

Mielőtt belemerülnénk a kódba, van néhány előfeltétel, amit teljesítened kell a zökkenőmentes élmény érdekében:

### C# és .NET alapismeretek

Szükséged lesz a C# programozás és a .NET keretrendszer alapvető ismeretére. Ez segít megérteni a kézikönyvben található kód szerkezetét.

### Aspose.Cells .NET-hez

Győződjön meg róla, hogy telepítve van az Aspose.Cells for .NET. Az összes részletet megtalálja a következő címen: [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/). 

### Fejlesztői környezet

Állítsa be a fejlesztői környezetét. Ez lehet Visual Studio vagy bármilyen más C#-t támogató IDE. Töltse le és telepítse az Aspose.Cells könyvtárat a következő helyről: [letöltési oldal](https://releases.aspose.com/cells/net/).

### Minta Excel-fájl

Szükséged lesz egy minta Excel-fájlra, amely legalább egy diagramot tartalmaz. Létrehozhatsz egy mintafájlt, vagy letölthetsz egyet, hogy használhasd ezt az oktatóanyagot.

## Csomagok importálása

Az Aspose.Cells használatának megkezdéséhez importálnia kell a szükséges névtereket a C# alkalmazásába. Ezt a következőképpen teheti meg:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Ezek a névterek hozzáférést biztosítanak az Excel-munkafüzetek és azok tartalmának kezeléséhez szükséges osztályokhoz és metódusokhoz.

Most, hogy minden előfeltételt tisztáztunk, bontsuk le a folyamatot részletes lépésekre.

## 1. lépés: Kimeneti és forráskönyvtárak beállítása

Először is meg kell határoznia, hogy hová kerüljön a kimeneti PDF, és hol legyen a forrás Excel dokumentum.

```csharp
//Kimeneti könyvtár
string outputDir = "Your Output Directory";

//Forráskönyvtár
string sourceDir = "Your Document Directory";
```

Ügyelj arra, hogy a „Kimeneti könyvtár” és a „Dokumentumkönyvtár” helyére a rendszereden található tényleges elérési utakat írd be. Ez határozza meg, hogy az Aspose hová menti a létrehozott PDF-et, és hol fogja megtalálni az Excel-fájlt.

## 2. lépés: Töltse be a minta Excel-fájlt

Ezután be kell töltenie a diagramot tartalmazó Excel-fájlt. Így teheti meg:

```csharp
//Töltsd be a diagramot tartalmazó minta Excel fájlt.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

A `Workbook` Az osztály központi szerepet játszik az Excel-dokumentummal való interakcióban. Győződjön meg arról, hogy az elérési út helyesen az Excel-fájlra mutat – egy itt fellépő hiba megakadályozza a kód többi részének végrehajtását.

## 3. lépés: Az első munkalap elérése

Miután a munkafüzet betöltődött, a következő lépés a kívánt diagramot tartalmazó munkalap elérése.

```csharp
//Első munkalap elérése.
Worksheet ws = wb.Worksheets[0];
```

Az Aspose.Cells fájlban a munkalapok nullától kezdődően indexelődnek, tehát `Worksheets[0]` az első lapra utal.

## 4. lépés: Az első diagram elérése

Most pedig nézzük meg a PDF-be exportálni kívánt diagramot. Ez a lépés feltételezi, hogy a munkalap legalább egy diagramot tartalmaz.

```csharp
//Hozzáférés az első diagramhoz a munkalapon belül.
Chart ch = ws.Charts[0];
```

Ez ismét a munkalap első diagramjához fér hozzá; győződjön meg arról, hogy a munkalap szerkezete megfelel ennek a megközelítésnek.

## 5. lépés: PDF létrehozása a kívánt oldalmérettel

Végül itt az ideje, hogy a diagramból PDF-et készítsünk a megadott oldalmérettel. Íme a varázslatos kódsor, ami mindezt elvégzi:

```csharp
//Hozz létre egy PDF-diagramot a kívánt oldalméretben.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

Ebben a kódban:
- A PDF fájl a korábban megadott kimeneti könyvtárba lesz mentve.
- A számok `7, 7` a kívánt oldalméret szélességét és magasságát jelölik.
- A PageLayoutAlignmentType.Center biztosítja, hogy a diagram az oldal közepére legyen igazítva.

## 6. lépés: Megerősítő üzenet

Hogy tudasd magaddal (és másokkal) a sikert, illessz be egy megerősítő üzenetet a kódod végére:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Ez az üzenet jelenik meg a konzolablakban, amint a folyamat befejeződött, jelezve, hogy a PDF fájl gond nélkül létrejött.

## Következtetés

Gratulálunk! Most megtanultad, hogyan használhatod az Aspose.Cells for .NET-et PDF létrehozásához egy Excel-fájlban található diagramból. Ez a hatékony könyvtár leegyszerűsíti az Excel-dokumentumok kezelésének és az adatok vizuális ábrázolásának folyamatát, így órákig tartó manuális formázást takaríthatsz meg. Feltétlenül fedezd fel az Aspose.Cells számos egyéb funkcióját is, amelyeket a PDF-generáláson túl kínál – soha nem tudhatod, mi javíthatja tovább a projektjeidet!

## GYIK

### Mire használják az Aspose.Cells for .NET-et?  
Az Aspose.Cells for .NET az Excel dokumentumok programozott létrehozására, szerkesztésére és konvertálására szolgál .NET alkalmazásokban.

### Ingyenesen használhatom az Aspose.Cells-t?  
Igen, az Aspose.Cells kínál egy [ingyenes próba](https://releases.aspose.com/) értékelési célokra.

### Van mód arra, hogy a próbaidőszakomat meghosszabbítsam a kezdeti időszakon túl?  
Pályázatot tehet egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) hosszabb teszteléshez.

### Mi van, ha problémákba ütközöm vagy kérdéseim vannak?  
Segítséget kérhetsz az Aspose közösségtől a következő címen: [támogató fórum](https://forum.aspose.com/c/cells/9).

### Hogyan vásárolhatom meg az Aspose.Cells-t?  
Az Aspose.Cells-t a következő helyről vásárolhatod meg: [vásárlási oldal](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}