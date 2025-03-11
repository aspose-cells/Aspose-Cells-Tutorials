---
title: Osztott ablaktáblák munkalap
linktitle: Osztott ablaktáblák munkalap
second_title: Aspose.Cells for .NET API Reference
description: lépésenkénti útmutatónkból megtudhatja, hogyan oszthat fel munkalappaneleket az Aspose.Cells for .NET-ben. Ezzel az egyszerű oktatóanyaggal javíthatja az Excel-fájlok navigációját.
weight: 130
url: /hu/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Osztott ablaktáblák munkalap

## Bevezetés

Készen áll egy Excel-munkalap ablaktábláinak felosztására az Aspose.Cells for .NET segítségével? Képzelje el ezt: van egy gigantikus Excel-lapja, és belefáradt abba, hogy állandóan visszagörgessen a fejlécekhez, csak hogy emlékezzen, melyik oszloppal dolgozik. Írja be az "Osztott ablaktáblák" lehetőséget. Ez a praktikus funkció lehetővé teszi a munkalap egy részének lefagyasztását, ami sokkal könnyebbé teszi a navigációt. Függetlenül attól, hogy pénzügyi adatokkal, készletkezeléssel vagy hatalmas adatkészletekkel dolgozik, az ablaktáblák felosztása tízszeresére növelheti a termelékenységet. 

## Előfeltételek

Mielőtt elkezdenénk az ablaktáblák felosztását, mint egy táblázatkezelő varázsló, végezzük el a megfelelő beállítást. Íme, amire szüksége lesz:

-  Aspose.Cells for .NET: Győződjön meg arról, hogy letöltötte és telepítette. Ha még nem, fogd meg[itt](https://releases.aspose.com/cells/net/).
- .NET-keretrendszer: Ez az útmutató feltételezi, hogy Ön .NET-környezetben dolgozik.
- Excel-munkafüzet: Egy Excel-mintafájlt használunk a funkció működésének bemutatására.
-  Ideiglenes vagy teljes licenc: Aspose.Cells licenc szükséges. Ha csak kipróbálod, szerezd be a[ingyenes ideiglenes licenc](https://purchase.aspose.com/temporary-license/) hogy elkerüljük az értékelési korlátokat.

## Csomagok importálása

Mielőtt belemerülnénk a kódba, először importáljuk a szükséges névtereket. Az Aspose.Cells-ben nem igazán tudsz semmit tenni ezek nélkül.

```csharp
using System.IO;
using Aspose.Cells;
```

Most, hogy a lényeges dolgokkal foglalkoztunk, térjünk át az izgalmas részre – az ablaktáblák felosztására!

## 1. lépés: Példányosítson munkafüzetet

 Ennek a folyamatnak az első lépése az a`Workbook` objektumot, amely a módosítani kívánt Excel-fájlt fogja képviselni. Ebben az esetben egy fájlt egy könyvtárból töltünk be. Ez az Ön vászna, az Excel-lap, amelyen varázsolhatja.

Mielőtt felosztanánk az ablaktáblákat, szükségünk van egy munkafüzetre, amellyel dolgozhatunk! Ez a lépés ugyanolyan fontos, mint kinyitni egy könyvet, mielőtt elkezdi olvasni.

```csharp
// A dokumentumok könyvtárának elérési útja
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Hozzon létre egy új munkafüzetet, és nyisson meg egy sablonfájlt
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 A fenti kódban cserélje ki`"YOUR DOCUMENT DIRECTORY"` az Excel-fájl tényleges elérési útjával. A`Workbook`osztály betölti az Excel fájlt a memóriába.

## 2. lépés: Állítsa be az aktív cellát

 A munkafüzet betöltése után ideje beállítani az aktív cellát. Az Excel kifejezésében az aktív cella az aktuálisan kijelölt vagy fókuszban lévő cella. Ebben az oktatóanyagban cellát választunk ki`A20` az első munkalapon.

Az aktív cella beállítása kulcsfontosságú, mert az ablaktábla felosztása ettől az aktív cellától kezdődik. Ez olyan, mintha kiválasztaná, hol készítse el az első szeletet egy pizzában – válassza ki a szeletet!

```csharp
// Állítsa be az aktív cellát
book.Worksheets[0].ActiveCell = "A20";
```

 Ez a kódrészlet teszi`A20` az aktív sejt. Ez azért fontos, mert a felosztás ezen a ponton történik, ugyanúgy, mint ahogy az Excelben történő navigáció gyakran egy adott cella köré összpontosul.

## 3. lépés: Ossza fel a munkalapot

Most, hogy az aktív cella be van állítva, térjünk át a szórakoztató részre – a munkalap felosztására! Ebben a lépésben történik a varázslat. A könnyebb megtekintés és navigáció érdekében a munkalapot több panelre is feloszthatja.

Ez az egész oktatóanyag magja. A munkalap felosztásával külön ablaktáblákat hoz létre, amelyek lehetővé teszik az Excel munkalap különböző szakaszainak görgetését anélkül, hogy szem elől tévesztené a fejléceket vagy más fontos területeket.

```csharp
// A munkalap ablak felosztása
book.Worksheets[0].Split();
```

 A`Split()` módszerrel, akkor azt mondod az Aspose.Cells-nek, hogy ossza fel a munkalapot az aktív cellában (`A20` ebben az esetben). Ettől a ponttól kezdve az Excel egy felosztást hoz létre a lapon, amely elválasztja az ablaktáblákat, hogy önállóan navigálhasson.

## 4. lépés: Mentse el a munkafüzetet

Az ablaktáblák felosztása után már csak el kell mentenie a munkáját. Ez az utolsó lépés biztosítja, hogy a változtatások a megadott kimeneti fájlba kerüljenek.

Mit ér a kemény munkád, ha nem mented meg? A mentés biztosítja, hogy a gyönyörűen hasított üvegtáblák sértetlenek maradnak a későbbi használatra.

```csharp
// Mentse el az Excel fájlt
book.Save(dataDir + "output.xls");
```

 Itt, a`Save()` metódus menti a munkafüzetet az újonnan felosztott ablaktáblákkal egy kimeneti Excel-fájlba. Az Ön által végrehajtott változtatások készen állnak az Ön – vagy bárki más – használatra.

## Következtetés

És megvan! Most tanulta meg, hogyan oszthat fel ablaktáblákat egy Excel-munkalapon az Aspose.Cells for .NET segítségével. Nincs több végtelen görgetés vagy adatok elvesztése. Ezzel a módszerrel a nagy Excel-fájlok kezelése sokkal kevésbé nyomasztó és sokkal hatékonyabb. Az ablaktáblák felosztásának lehetőségével most nyomon követheti a kritikus adatpontokat, miközben összetett táblázatokkal dolgozik.

## GYIK

### Feloszthatok kettőnél több ablaktáblát?  
 Igen, a munkalapot több panelre is feloszthatja, ha különböző aktív cellákat ad meg, és meghívja a`Split()` módszer.

### Mi a különbség a hasító és a fagyasztó ablaktáblák között?  
Az ablaktáblák felosztása lehetővé teszi, hogy mindkét panelen egymástól függetlenül görgessen. Az ablaktáblák rögzítése zárolja a fejléceket vagy bizonyos sorokat/oszlopokat, így görgetés közben láthatóak maradnak.

### Eltávolíthatom a hasadást az alkalmazás után?  
Igen, eltávolíthatja a felosztást a munkafüzet bezárásával és újranyitásával, vagy programozott alaphelyzetbe állításával.

### felosztási ablaktáblák ugyanúgy működnek a különböző Excel fájlformátumoknál (XLS, XLSX)?  
 Igen, a`Split()` A módszer XLS és XLSX formátumok esetén is működik.

### Használhatom az Aspose.Cells-t licenc nélkül?  
 Igen, de ez korlátokkal jár. A teljes élmény érdekében a legjobb, ha a[ideiglenes](https://purchase.aspose.com/temporary-license/) vagy[fizetett licenc](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
