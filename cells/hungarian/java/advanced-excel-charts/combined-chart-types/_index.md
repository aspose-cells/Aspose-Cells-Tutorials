---
date: 2026-02-14
description: Tanulja meg, hogyan exportálja a diagramot PNG formátumba, adjon hozzá
  adat sorozatot, kombináljon vonal‑oszlop diagramot, mentse a munkafüzetet XLSX formátumban,
  és adjon hozzá jelmagyarázatot a diagramhoz az Aspose.Cells for Java segítségével.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Diagram exportálása PNG-be és adat sorozat hozzáadása kombinált diagramhoz
url: /hu/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

 content.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagram exportálása PNG formátumba és adat sorozat hozzáadása kombinált diagramhoz

Ebben az oktatóanyagról **adat sorozatot adsz hozzá** egy Excel munkafüzethez, **összekapcsolod a vonal- és oszlopdiagram** elemeket, és megtanulod, hogyan **exportálod a diagramot PNG‑be** az Aspose.Cells for Java használatával. Lépésről lépésre végigvezetünk – a munkafüzet beállításától, a diagram hozzáadásán a munkalaphoz, a jelmagyarázat testreszabásáig, egészen a **munkafüzet mentéséig xlsx‑ként** és a diagram PNG képének előállításáig. A végére egy kész, használatra kész kombinált diagramod lesz, amelyet beágyazhatsz jelentésekbe vagy műszerfalakba.

## Gyors válaszok
- **Melyik könyvtár hoz létre kombinált diagramokat?** Aspose.Cells for Java  
- **Hogyan adhatok hozzá adat sorozatot?** Use `chart.getNSeries().add(...)`  
- **Hogyan exportálhatom a diagramot png‑be?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **Milyen fájlformátumban menthetem a munkafüzetet?** Standard `.xlsx` (save workbook as xlsx)  
- **Szükségem van licencre a termeléshez?** A valid Aspose.Cells license is required  

## Mi az **export chart to PNG** az Aspose.Cells‑ben?
A diagram PNG‑be exportálása egy raszteres képet hoz létre az Excel diagramról, amely weboldalakon, jelentésekben vagy e‑mailben jeleníthető meg az Excel alkalmazás nélkül.

## Miért hozunk létre **kombinált vonal‑oszlop diagramot**?
A kombinált diagram lehetővé teszi, hogy különböző adatcsoportokat eltérő vizuális ábrázolással (pl. egy vonal sorozat egy oszlop sorozat felett) egyetlen nézetben jelenítsünk meg. Ez tökéletes a trendek összehasonlításához az összesítésekkel, a korrelációk kiemeléséhez, vagy gazdagabb betekintés nyújtásához kompakt formátumban.

## Előkövetelmények
- Java Development Kit (JDK) 8 vagy újabb  
- Aspose.Cells for Java könyvtár (letöltés az alábbi hivatkozásból)  
- Alapvető ismeretek a Java szintaxisról és az Excel koncepciókról  

## Kezdés

Először töltse le az Aspose.Cells for Java könyvtárat a hivatalos oldalról:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Miután a JAR-t hozzáadta a projekt osztályútvonalához, elkezdheti a diagram felépítését.

### 1. lépés: Aspose.Cells osztályok importálása
```java
import com.aspose.cells.*;
```

### 2. lépés: Új munkafüzet létrehozása
```java
Workbook workbook = new Workbook();
```

### 3. lépés: Az első munkalap elérése
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 4. lépés: Kombinált diagram objektum hozzáadása a munkalaphoz  
Először egy vonaldiagrammal kezdünk, majd később egy oszlopsorozatot adunk hozzá, hogy elérjük a **kombinált vonal‑oszlop diagram** hatást.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adatok hozzáadása a diagramhoz

Miután a diagram konténer létezik, adatokat kell betáplálnunk.

### 5. lépés: Az adat tartományok meghatározása és **adat sorozat hozzáadása**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tipp:** Az első paraméter (`"A1:A5"`) az első sorozat tartománya, a második (`"B1:B5"`) egy második sorozatot hoz létre, amely az elsővel kombinálódik.

### 6. lépés: A kategória (X‑tengely) adat beállítása
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## A diagram testreszabása

Egy jó diagram történetet mesél. Adjunk neki címet, tengelycímkéket és egyértelmű jelmagyarázatot.

### 7. lépés: **Diagram tengelycímkék beállítása** és cím
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 8. lépés: **Jelmagyarázat hozzáadása a diagramhoz** és a pozíciójának módosítása
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## A diagram mentése és exportálása

A testreszabás után szeretné **menteni a munkafüzetet xlsx‑ként** és képet is előállítani.

### 9. lépés: A munkafüzet mentése Excel fájlként (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### 10. lépés: **Diagram exportálása PNG‑be**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> A `chart.toImage` metódus **excel diagram** képeket generál, amelyeket weboldalakon, jelentésekben vagy e‑mailben lehet használni.

## Gyakori problémák és hibaelhárítás

| Issue | Solution |
|-------|----------|
| **Nincs adat** | Ellenőrizze, hogy a cellatartományok (`A1:A5`, `B1:B5`, `C1:C5`) valóban tartalmaznak adatot a diagram létrehozása előtt. |
| **A jelmagyarázat átfedi a diagramot** | Állítsa be a `chart.getLegend().setOverlay(false)` értéket, vagy mozgassa a jelmagyarázatot más pozícióba (pl. `RIGHT`). |
| **A kép fájl üres** | Győződjön meg róla, hogy a diagramnak legalább egy sorozata van, és a `chart.toImage` a teljes testreszabás után kerül meghívásra. |
| **Mentés közben kivétel keletkezik** | Ellenőrizze, hogy van írási jogosultsága a célkönyvtárban, és a fájl nincs megnyitva Excelben. |

## Gyakran ismételt kérdések

**Q: Hogyan telepítem az Aspose.Cells for Java‑t?**  
A: Töltse le a JAR‑t a hivatalos oldalról, és adja hozzá a projekt osztályútvonalához. A letöltési hivatkozás: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Készíthetek más diagramtípusokat is a vonal és oszlop mellett?**  
A: Igen, az Aspose.Cells támogatja az oszlop, kör, szórt, terület és sok más diagramtípust. Tekintse meg az API dokumentációt a teljes listáért.

**Q: Szükséges licenc a termelési használathoz?**  
A: Érvényes Aspose.Cells licenc szükséges a termelési telepítésekhez. Ingyenes próba elérhető értékeléshez.

**Q: Hogyan változtathatom meg az egyes sorozatok színeit?**  
A: Használja a `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (vagy hasonló) metódust a sorozatok hozzáadása után.

**Q: Hol találok további kódrészleteket?**  
A: Átfogó dokumentáció és további példák érhetők el az Aspose referencia oldalon: [here](https://reference.aspose.com/cells/java/).

---

**Utoljára frissítve:** 2026-02-14  
**Tesztelve:** Aspose.Cells for Java legújabb verzióval  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}