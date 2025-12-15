---
date: 2025-12-10
description: Ismerje meg, hogyan hozhat létre vízesés diagramot Java-ban az Aspose.Cells
  használatával. Lépésről lépésre útmutató a diagram munkalapra való hozzáadásához,
  testreszabásához és a munkafüzet XLSX formátumban való mentéséhez.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Hogyan készítsünk vízesés diagramot az Aspose.Cells for Java segítségével
url: /hu/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vízárapló diagramok

## Bevezetés a vízárapló diagramokhoz az Aspose.Cells for Java használatával

Ebben az oktatóanyagban megtanulja, hogyan **hozzon létre vízárapló diagramot** az Aspose.Cells for Java segítségével. A vízárapló diagramok alapvető eszközök az adatvizualizációban, mivel lehetővé teszik a pozitív és negatív értékek sorozatának kumulatív hatásának megtekintését. Legyen szó pénzügyi kimutatás, értékesítési teljesítmény jelentés vagy bármilyen más adat‑vezérelt elemzés elkészítéséről, a vízárapló diagram nyers számokat átlátható, cselekvésre ösztönző betekintéssé alakít.

## Gyors válaszok
- **Mi az a vízárapló diagram?** Egy vizuális ábrázolás, amely megmutatja, hogyan növekszik és csökken egy kezdeti érték egy sor közbenső érték hatására, végül egy végösszeggel.  
- **Melyik könyvtárat használjuk?** Aspose.Cells for Java.  
- **Szükségem van licencre?** A ingyenes próba verzió fejlesztéshez elegendő; a termeléshez kereskedelmi licenc szükséges.  
- **Menthetem a fájlt XLSX formátumban?** Igen – használja a `workbook.save("FileName.xlsx")` parancsot.  
- **Alkalmas-e Java adatvizualizációra?** Teljesen; az Aspose.Cells gazdag diagramkészítési funkciókat biztosít Office telepítése nélkül.

## Mi az a vízárapló diagram?
A vízárapló diagram sorozatos pozitív és negatív hozzájárulásokat jelenít meg egy kiinduló értékhez, segítve megérteni, hogyan befolyásolja az egyes komponensek az összesített eredményt.

## Miért használjuk az Aspose.Cells for Java‑t vízárapló diagram hozzáadásához?
- **Microsoft Excel nem szükséges** – diagramok generálása bármely szerveren vagy CI pipeline‑ban.  
- **Teljes formázási irányítás** – színek, adatcímkék és tengelyek programozottan testreszabhatók.  
- **Több kimeneti formátumot támogat** – XLSX, PDF, HTML és egyebek.  
- **Magas teljesítmény** – ideális nagy munkafüzetekhez és automatizált jelentésekhez.

## Előfeltételek

Mielőtt belevágna a kódba, győződjön meg róla, hogy a következő előfeltételek teljesülnek:

- Aspose.Cells for Java: Telepítenie kell az Aspose.Cells for Java‑t. Letöltheti innen: [here](https://releases.aspose.com/cells/java/).

- Java fejlesztői környezet: Győződjön meg róla, hogy a Java telepítve van a rendszerén.

Most kezdjünk is el lépésről lépésre létrehozni a vízárapló diagramot.

## Hogyan hozzunk létre vízárapló diagramot Java‑ban

### 1. lépés: Aspose.Cells importálása

```java
import com.aspose.cells.*;
```

Először importálnia kell az Aspose.Cells könyvtárat a Java projektjébe. Ez a könyvtár kiterjedt funkcionalitást nyújt Excel fájlok kezeléséhez, beleértve a diagramkészítést is.

### 2. lépés: Munkafüzet és munkalap inicializálása

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Hozzon létre egy új munkafüzetet, és adjon hozzá egy munkalapot. Ezt a munkalapot fogjuk használni az adataink bevitelére és a **diagram munkalapra való hozzáadására**.

### 3. lépés: Adatok bevitele

Most töltsük fel a munkalapot azokkal az adatokkal, amelyeket a vízárapló diagramon szeretnénk megjeleníteni.

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

Ebben a példában az A oszlopban vannak a kategóriák, a B oszlopban pedig a hozzájuk tartozó értékek. A saját adatkészletével helyettesítheti ezeket.

### 4. lépés: Vízárapló diagram létrehozása

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Hozzáadtunk egy vízárapló diagramot a munkalaphoz, megadtuk az adat sorozatot és a kategória adatokat. Ez a kulcsfontosságú lépés, amely **vízárapló diagramot ad hozzá** a laphoz. A diagram megjelenését (színek, adatcímkék stb.) tovább testreszabhatja a `Chart` objektum tulajdonságainak használatával.

### 5. lépés: Munkafüzet mentése

```java
workbook.save("WaterfallChart.xlsx");
```

Mentse a munkafüzetet egy fájlba. A példa az XLSX formátumot használja, de az Aspose.Cells lehetővé teszi a PDF, CSV és számos egyéb formátumba történő exportálást is. Ez megfelel a **save workbook xlsx** követelménynek.

## Gyakori problémák és megoldások

- **A diagram üresnek jelenik meg** – Ellenőrizze, hogy az adat tartomány hivatkozások (`B2:B6` és `A2:A6`) megegyeznek a ténylegesen értékeket és kategóriákat tartalmazó cellákkal.  
- **A negatív értékek nem jelennek meg helyesen** – Győződjön meg arról, hogy a sorozat típusa `ChartType.WATERFALL`‑ra van állítva; más diagramtípusok másként kezelik a negatív értékeket.  
- **A fájl nem nyílik meg Excelben** – Ellenőrizze, hogy a legújabb Aspose.Cells verziót használja (a legfrissebb kiadást), és hogy a fájlkiterjesztés megfelel a formátumnak (`.xlsx` az Excelhez).

## Gyakran feltett kérdések

### Hogyan testreszabhatom a vízárapló diagram megjelenését?

A vízárapló diagram megjelenését testreszabhatja olyan tulajdonságok módosításával, mint a színek, adatcímkék és tengelycímkék. Részletes útmutatásért tekintse meg az Aspose.Cells dokumentációt.

### Létrehozhatok több vízárapló diagramot ugyanabban a munkalapban?

Igen, több vízárapló diagramot is létrehozhat ugyanabban a munkalapban, ha a különböző adat tartományokkal ugyanazokat a lépéseket követi.

### Kompatibilis‑e az Aspose.Cells különböző Java fejlesztői környezetekkel?

Igen, az Aspose.Cells for Java kompatibilis különböző Java fejlesztői környezetekkel, beleértve az Eclipse‑et, az IntelliJ IDEA‑t és a NetBeans‑t.

### Hozzáadhatok további adat sorozatokat a vízárapló diagramomhoz?

Természetesen, további adat sorozatokat adhat hozzá a vízárapló diagramhoz, hogy hatékonyan ábrázolja a komplex adathelyzeteket.

### Hol találok további forrásokat és példákat az Aspose.Cells for Java‑hoz?

A részletes információkért és kódpéldákért böngészheti az Aspose.Cells for Java dokumentációját a [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) oldalon.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}