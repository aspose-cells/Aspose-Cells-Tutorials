---
date: 2026-02-16
description: Tanulja meg, hogyan állítsa be a diagram adat tartományát, és hogyan
  hozzon létre vízesésdiagramot Java-ban az Aspose.Cells használatával. Lépésről‑lépésre
  útmutató az adat sorozat diagram hozzáadásához, testreszabásához és XLSX formátumba
  exportálásához.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Diagram adattartomány beállítása – Aspose.Cells for Java vízesés diagram
url: /hu/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vízárapály diagramok

## Bevezetés a vízárapály diagramokhoz az Aspose.Cells for Java használatával

Ebben az útmutatóban megtanulja, hogyan **állítsa be a diagram adatcímét** és hogyan hozzon létre egy **vízárapály diagramot** az Aspose.Cells for Java segítségével. A vízárapály diagramok alapvető eszközök az adatvizualizációban, mivel lehetővé teszik a pozitív és negatív értékek sorozatának kumulatív hatásának megtekintését. Legyen szó pénzügyi kimutatás, értékesítési teljesítmény‑jelentés vagy bármilyen más adat‑vezérelt elemzés elkészítéséről, egy vízárapály diagram a nyers számokat világos, cselekvőképes betekintéssé alakítja.

## Gyors válaszok
- **Mi az a vízárapály diagram?** Egy vizuális ábrázolás, amely megmutatja, hogyan növekszik vagy csökken egy kezdeti érték közbenső értékek sorozata által, végül egy végösszeggel zárulva.  
- **Melyik könyvtárat használjuk?** Aspose.Cells for Java.  
- **Szükségem van licencre?** Fejlesztéshez egy ingyenes próba verzió elegendő; termeléshez kereskedelmi licenc szükséges.  
- **Menthetem a fájlt XLSX formátumban?** Igen – használja a `workbook.save("FileName.xlsx")` parancsot.  
- **Alkalmas-e Java adatvizualizációra?** Teljes mértékben; az Aspose.Cells gazdag diagramkészítési funkciókat kínál Office telepítése nélkül.

## Mi az a vízárapály diagram?
A vízárapály diagram sorozatos pozitív és negatív hozzájárulásokat jelenít meg egy kiinduló értékhez képest, segítve megérteni, hogy az egyes komponensek hogyan befolyásolják a teljes eredményt.

## Miért használjuk az Aspose.Cells for Java‑t vízárapály diagram hozzáadásához?
- **Microsoft Excel nélkül** – diagramok generálása bármely szerveren vagy CI‑pipeline‑ban.  
- **Teljes formázási kontroll** – színek, adatcímkék és tengelyek programozott testreszabása.  
- **Több kimeneti formátum támogatása** – XLSX, PDF, HTML és még sok más.  
- **Magas teljesítmény** – nagy munkafüzetekhez és automatizált jelentéskészítéshez ideális.

## Előkövetelmények

Mielőtt a kódba merülnénk, győződjön meg róla, hogy az alábbiak rendelkezésre állnak:

- Aspose.Cells for Java: Telepítenie kell az Aspose.Cells for Java‑t. Letöltheti [innen](https://releases.aspose.com/cells/java/).

- Java fejlesztői környezet: Bizonyosodjon meg arról, hogy a Java telepítve van a rendszerén.

Most kezdjük el a vízárapály diagram lépésről‑lépésre történő létrehozását.

## Hogyan állítsuk be a diagram adatcímét egy vízárapály diagramhoz Java‑ban

### 1. lépés: Aspose.Cells importálása

```java
import com.aspose.cells.*;
```

Először importálni kell az Aspose.Cells könyvtárat a Java projektbe. Ez a könyvtár kiterjedt funkcionalitást biztosít Excel‑fájlok kezeléséhez, beleértve a diagramok létrehozását is.

### 2. lépés: Munkafüzet és munkalap inicializálása

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Hozzon létre egy új munkafüzetet, és adjon hozzá egy munkalapot. Ezt a munkalapot fogjuk használni az adatok bevitelére és a **diagram hozzáadására a munkalaphoz**.

### 3. lépés: Adatok bevitele

Most töltsük fel a munkalapot azokkal az adatokkal, amelyeket a vízárapály diagramon szeretnénk megjeleníteni.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

Ebben a példában az A oszlopban vannak a kategóriák, a B oszlopban pedig a hozzájuk tartozó értékek. A saját adathalmazával is helyettesítheti ezeket az adatokat.

### 4. lépés: Vízárapály diagram létrehozása

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Vízárapály diagramot adtunk a munkalaphoz, megadtuk az adat sorozatot és a kategória adatokat. Ez a kulcsfontosságú lépés, amely **vízárapály diagramot ad a laphoz**. Figyelje meg, hogy az `add` metódus a `"B2:B6"` tartományt használja – itt **állítjuk be a diagram adatcímét** a sorozathoz. A diagram megjelenését (színek, adatcímkék stb.) tovább testreszabhatja a `Chart` objektum tulajdonságainak módosításával.

### 5. lépés: Munkafüzet mentése

```java
workbook.save("WaterfallChart.xlsx");
```

Mentse a munkafüzetet egy fájlba. A példa az XLSX formátumot használja, de az Aspose.Cells lehetővé teszi **export excel pdf java**‑kompatibilis fájlok létrehozását is, például PDF, CSV és sok más formátum. Ez megfelel a **save workbook xlsx** követelménynek.

## Gyakori problémák és megoldások

- **A diagram üresen jelenik meg** – Ellenőrizze, hogy az adatcímek (`B2:B6` és `A2:A6`) megfelelnek a ténylegesen értékeket és kategóriákat tartalmazó celláknak.  
- **A negatív értékek nem jelennek meg helyesen** – Győződjön meg arról, hogy a sorozattípus `ChartType.WATERFALL`‑ra van állítva; más diagramtípusok másként kezelik a negatív értékeket.  
- **A fájl nem nyílik meg Excelben** – Bizonyosodjon meg róla, hogy a legújabb Aspose.Cells verziót (a legfrissebb kiadást) használja, és hogy a fájlkiterjesztés megfelel a formátumnak (`.xlsx` az Excelhez).

## Gyakran ismételt kérdések

### Hogyan testreszabhatom a vízárapály diagram megjelenését?

A diagram megjelenését testreszabhatja olyan tulajdonságok módosításával, mint a színek, adatcímkék és tengelycímkék. Részletes útmutatásért tekintse meg az Aspose.Cells dokumentációját.

### Létrehozhatok több vízárapály diagramot ugyanabban a munkalapban?

Igen, több vízárapály diagramot is létrehozhat ugyanabban a munkalapban, ha ugyanazokat a lépéseket követi különböző adatcímekkel.

### Az Aspose.Cells kompatibilis-e különböző Java fejlesztői környezetekkel?

Igen, az Aspose.Cells for Java kompatibilis különböző Java fejlesztői környezetekkel, beleértve az Eclipse‑et, az IntelliJ IDEA‑t és a NetBeans‑t.

### Hozzáadhatok további adat sorozatokat a vízárapály diagramomhoz?

Természetesen, további adat sorozatokat adhat a vízárapály diagramhoz, hogy összetett adathelyzeteket is hatékonyan ábrázoljon. Ez egy példa arra, hogyan **add data series chart** programozottan.

### Hol találok további forrásokat és példákat az Aspose.Cells for Java‑hoz?

Az Aspose.Cells for Java dokumentációját a [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) oldalon tekintheti meg, ahol részletes információk és kódrészletek állnak rendelkezésre.

## FAQ

**Q: Hogyan állíthatom be a diagram adatcímét egy pénzügyi vízárapály diagramhoz?**  
A: Használja a `add` metódust a diagram sorozatán, megadva a cellatartományt, amely tartalmazza az értékeket, például `"B2:B6"`.

**Q: Exportálhatom a munkafüzetet PDF‑be az XLSX helyett?**  
A: Igen, hívja meg a `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` parancsot, hogy **export excel pdf java**‑kompatibilis kimenetet kapjon.

**Q: Mi a teendő, ha több kategóriával szeretnék pénzügyi vízárapály diagramot létrehozni?**  
A: Bővítse az adatcímeket mind az értékek, mind a kategóriák oszlopában, majd ennek megfelelően frissítse a `add` és a `setCategoryData` hívásokat.

**Q: Van mód automatikusan formázni a pozitív és negatív oszlopokat?**  
A: Iterálhat a `Series` gyűjteményen, és a `FillFormat` színt a megfelelő érték előjelének megfelelően állíthatja be.

**Q: Támogatja-e az Aspose.Cells a diagramok dinamikus adatfrissítését?**  
A: Igen, a diagram létrehozása után módosíthatja a cellaértékeket; a diagram a munkafüzet mentésekor tükrözi a változásokat.

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}