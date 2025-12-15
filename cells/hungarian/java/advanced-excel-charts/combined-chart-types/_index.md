---
date: 2025-12-06
description: Tanulja meg, hogyan adjon hozzá adat sorozatokat, hozzon létre kombinált
  diagramtípusokat, mentse el a munkafüzetet Excel formátumban, és exportálja a diagramot
  PNG formátumba az Aspose.Cells for Java segítségével.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Adjon hozzá adat sorozatokat kombinált diagram létrehozásához az Aspose.Cells
  segítségével
url: /hu/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adatsorok hozzáadása kombinált diagram létrehozásához az Aspose.Cells használatával

Ebben az útmutatóban **adatsorokat** adsz hozzá egy Excel munkafüzethez, és megtanulod, hogyan **hozz létre kombinált diagram** típusokat az Aspose.Cells for Java segítségével. Lépésről lépésre végigvezetünk – a munkafüzet beállításától, az adatsorok hozzáadásán, a jelmagyarázat testreszabásán, egészen a **munkafüzet Excel** fájlok **mentéséig** és a **diagram PNG‑ként exportálásáig**. A végére egy használatra kész kombinált diagramod lesz, amelyet beágyazhatsz jelentésekbe vagy műszerfalakba.

## Gyors válaszok
- **Melyik könyvtár hoz létre kombinált diagramokat?** Aspose.Cells for Java  
- **Hogyan adhatok hozzá egy adatsort?** Használd a `chart.getNSeries().add(...)`  
- **Exportálhatom a diagramot képként?** Igen, a `chart.toImage(...)` (PNG) használatával  
- **Milyen fájlformátumban menthetjük a munkafüzetet?** Standard `.xlsx` (Excel)  
- **Szükség van licencre a termeléshez?** Egy érvényes Aspose.Cells licenc szükséges  

## Mi az **adatsor hozzáadása** az Aspose.Cells-ben?
Az adatsor hozzáadása megmondja a diagramnak, mely cellák tartalmazzák a megjeleníteni kívánt értékeket. Minden sor képviselhet egy vonalat, oszlopot vagy bármely más diagramtípust, és keverheted őket egy **kombinált diagram** létrehozásához.

## Miért hozunk létre **kombinált diagramot**?
A kombinált diagram lehetővé teszi, hogy különböző adatcsoportokat eltérő vizuális ábrázolással (pl. egy vonalsor egy oszlopsor felett) jeleníts meg egyetlen nézetben. Ez tökéletes a trendek összehasonlításához az összesítésekkel, a korrelációk kiemeléséhez, vagy gazdagabb betekintés nyújtásához egy kompakt formátumban.

## Előkövetelmények
- Java Development Kit (JDK) 8 vagy újabb  
- Aspose.Cells for Java könyvtár (letöltés az alábbi hivatkozásból)  
- Alapvető ismeretek a Java szintaxisról és az Excel koncepciókról  

## Kezdő lépések

Először töltsd le az Aspose.Cells for Java könyvtárat a hivatalos oldalról:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Miután a JAR-t hozzáadtad a projekted osztályútvonalához, elkezdheted felépíteni a diagramot.

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

### 4. lépés: Kombinált diagram objektum hozzáadása  
Először egy vonaldiagrammal kezdünk, majd később más sorokat adunk hozzá, hogy elérjük a **kombinált diagram** hatást.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adatok hozzáadása a diagramhoz

Mivel a diagramkonténer már létezik, adatokat kell betáplálnunk.

### 5. lépés: Az adat tartományok meghatározása és **adatsor hozzáadása**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tipp:** Az első paraméter (`"A1:A5"`) az első sor tartománya, a második (`"B1:B5"`) egy második sort hoz létre, amely az elsővel kombinálódik.

### 6. lépés: A kategória (X‑tengely) adat beállítása
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## A diagram testreszabása

Egy jó diagram mesél. Adjunk neki címet, tengelycímkéket és egyértelmű jelmagyarázatot.

### 7. lépés: Diagramcím és tengelycímkék beállítása
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 8. lépés: **Jelmagyarázat hozzáadása** a diagramhoz és a pozíciójának beállítása
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## A diagram mentése és exportálása

A testreszabás után **munkafüzet Excel** mentésre és egy kép generálására lesz szükséged.

### 9. lépés: A munkafüzet mentése Excel fájlként
```java
workbook.save("CombinedChart.xlsx");
```

### 10. lépés: A **diagram PNG‑ként** exportálása
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> A `chart.toImage` metódus **Excel diagram** képeket generál, amelyeket weboldalakon, jelentésekben vagy e‑mailben lehet használni.

## Gyakori problémák és hibaelhárítás

| Probléma | Megoldás |
|----------|----------|
| **Nincs adat** | Ellenőrizd, hogy a cellatartományok (`A1:A5`, `B1:B5`, `C1:C5`) valóban tartalmaznak adatot a diagram létrehozása előtt. |
| **A jelmagyarázat átfedi a diagramot** | Állítsd be a `chart.getLegend().setOverlay(false)` értéket, vagy helyezd a jelmagyarázatot más pozícióba (pl. `RIGHT`). |
| **A kép fájl üres** | Győződj meg róla, hogy a diagramnak legalább egy sorozata van, és a `chart.toImage` a teljes testreszabás után kerül meghívásra. |
| **Mentés kivételt dob** | Ellenőrizd, hogy írási jogosultságod van-e a célkönyvtárra, és hogy a fájl nincs-e megnyitva Excelben. |

## Gyakran feltett kérdések

**K: Hogyan telepíthetem az Aspose.Cells for Java-t?**  
V: Töltsd le a JAR-t a hivatalos oldalról, és add hozzá a projekted osztályútvonalához. A letöltési hivatkozás: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**K: Létrehozhatok más diagramtípusokat is a vonal és oszlop mellett?**  
V: Igen, az Aspose.Cells támogatja az oszlop, kör, szórt, terület és még sok más diagramtípust. Tekintsd meg az API dokumentációt a teljes listáért.

**K: Szükséges licenc a termeléshez?**  
V: Egy érvényes Aspose.Cells licenc szükséges a termelési környezethez. Ingyenes próba elérhető értékeléshez.

**K: Hogyan változtathatom meg az egyes sorozatok színét?**  
V: Használd a `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (vagy hasonló) metódust a sorozatok hozzáadása után.

**K: Hol találok további kódrészleteket?**  
V: Átfogó dokumentáció és további példák érhetők el az Aspose referencia oldalon: [here](https://reference.aspose.com/cells/java/).

---

**Utolsó frissítés:** 2025-12-06  
**Tesztelve a következővel:** Aspose.Cells for Java 24.12  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
