---
date: 2026-02-09
description: Tanulja meg, hogyan adhat hozzá adatcímkéket az Excel-diagramhoz, és
  hogyan változtathatja meg a diagram típusát az Aspose.Cells for Java segítségével,
  valamint a tooltip‑eket és a drill‑down interaktivitást.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Adjon adatcímkéket az Excel-diagramhoz az Aspose.Cells Java segítségével
url: /hu/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

 a diagram típusát – Aspose.Cells Java"

Next paragraph: "Interactive charts give your Excel reports a new level ...". Translate.

We need to translate all textual content.

I'll produce Hungarian translation.

Be careful with bold markup **.

Also bullet lists.

Tables: translate Issue and Solution headings? Keep as is? Should translate content but keep header names maybe translate "Issue" to "Probléma", "Solution" to "Megoldás". But must preserve table structure. We'll translate both.

Also FAQ questions and answers.

Let's craft.

Also note "Quick Answers" heading.

Ok.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adjon hozzá adatcímkéket az Excel-diagramhoz és változtassa meg a diagram típusát – Aspose.Cells Java

Az interaktív diagramok új szintre emelik az Excel‑jelentéseket, és az **adatcímkék hozzáadása az Excel-diagramhoz** az információt azonnal olvashatóvá teszi. Ebben az útmutatóban megtanulja, hogyan **adjon hozzá adatcímkéket az Excel-diagramhoz**, hogyan változtassa meg a diagram típusát, valamint hogyan hozzon létre interaktív Java‑megoldásokat az Aspose.Cells segítségével. Megmutatjuk, hogyan adhat hozzá tooltip‑eket és egy egyszerű drill‑down hiperhivatkozást, hogy a közönség mélyebben felfedezhesse az adatokat.

## Gyors válaszok
- **Melyik könyvtárat használja?** Aspose.Cells for Java  
- **Megváltoztathatom a diagram típusát?** Igen – egyszerűen módosítsa a `ChartType` enum‑t a diagram létrehozásakor.  
- **Hogyan adhatok tooltip‑eket egy diagramhoz?** Használja az adatcímke API‑t (`setHasDataLabels(true)`) és engedélyezze az érték megjelenítését.  
- **Támogatott a drill‑down?** Hiperhivatkozásokat csatolhat adatpontokhoz az alapvető drill‑down viselkedéshez.  
- **Előfeltételek?** Java IDE, Aspose.Cells JAR, és egy Excel‑fájl mintaadatokkal.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy a következőkkel rendelkezik:

- Java fejlesztői környezet (JDK 8+ ajánlott)  
- Aspose.Cells for Java könyvtár (letölthető [innen](https://releases.aspose.com/cells/java/))  
- Egy minta munkafüzet (`data.xlsx`) a megjeleníteni kívánt adatokkal  

## 1. lépés: Java projekt beállítása

1. Hozzon létre egy új Java projektet a kedvenc IDE‑jében (IntelliJ IDEA, Eclipse, stb.).  
2. Adja hozzá az Aspose.Cells JAR‑t a projekt build‑path‑jához vagy Maven/Gradle függőségekhez.

## 2. lépés: Adatok betöltése

A diagramok használatához először be kell tölteni egy munkafüzetet a memóriába.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 3. lépés: Diagram létrehozása (és a típus módosítása)

Bármely olyan diagramtípust választhat, amely megfelel az elemzésnek. Az alábbiakban egy **oszlopdiagramot** hozunk létre, de könnyedén átválthat vonal-, kör- vagy sávdiagramra a `ChartType` enum módosításával.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** Az **Excel-diagram típusának megváltoztatásához** cserélje le a `ChartType.COLUMN` értéket `ChartType.LINE`, `ChartType.PIE` stb. értékekre.

## 4. lépés: Interaktivitás hozzáadása

### 4.1. Tooltip‑ek hozzáadása (Add Tooltips to Chart)

A tooltip‑ek akkor jelennek meg, amikor a felhasználó az egérrel egy adatpontra húz. Az alábbi kód engedélyezi az adatcímkéket és a értéket tooltip‑ként jeleníti meg.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Adatcímkék hozzáadása – **add data labels to excel chart**

Az adatcímkék állandó vizuális jelzést biztosítanak a diagramon. Megjelenítheti őket felhívásokként a jobb olvashatóság érdekében.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Miért érdemes adatcímkéket hozzáadni?** Az adatcímkék közvetlenül a diagramon való elhelyezése megszünteti a felhasználók számára a hover‑el vagy a becslés szükségességét, ezáltal javítva a jelentés átláthatóságát.

### 4.3. Drill‑Down megvalósítása (Hiperhivatkozás egy adatpontra)

Egy egyszerű módja a drill‑down képesség hozzáadásának, ha hiperhivatkozást csatol egy adott ponthoz. A pontra kattintva egy weboldal nyílik meg, amely részletes információkat tartalmaz.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 5. lépés: Munkafüzet mentése

A diagram konfigurálása után mentse a munkafüzetet, hogy az interaktív funkciók az output fájlban is megmaradjanak.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **A tooltip‑ek nem jelennek meg** | Győződjön meg róla, hogy a `setHasDataLabels(true)` hívás a `setShowValue(true)` konfigurálása előtt történik. |
| **A hiperhivatkozás nem kattintható** | Ellenőrizze, hogy a kimeneti formátum támogatja a hiperhivatkozásokat (pl. XLSX, nem CSV). |
| **A diagram típusa nem változik** | Ellenőrizze, hogy a diagram hozzáadásakor a megfelelő `ChartType` enum‑t módosította. |

## Gyakran feltett kérdések

**K: Hogyan változtathatom meg a diagram típusát a létrehozás után?**  
V: Új diagramot kell létrehoznia a kívánt `ChartType` értékkel. Az Aspose.Cells nem biztosít helyben történő típuskonverziót, ezért távolítsa el a régi diagramot és adjon hozzá egy újat.

**K: Testreszabhatom a tooltip‑ek megjelenését?**  
V: Igen. Használja a `DataLabel` tulajdonságait, például `setFontSize`, `setFontColor` és `setBackgroundColor` a tooltip‑szöveg stílusának beállításához.

**K: Hogyan kezelem a felhasználói interakciókat egy webalkalmazásban?**  
V: Exportálja a munkafüzetet HTML vagy XLSX formátumba, és használjon JavaScript‑et az ügyféloldalon a diagramelemekre történő kattintási események rögzítéséhez.

**K: Hol találok további példákat és dokumentációt?**  
V: Látogassa meg az [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalt a diagramokkal kapcsolatos osztályok és metódusok teljes listájáért.

## Összegzés

Most már tudja, hogyan **adjon hozzá adatcímkéket az Excel-diagramhoz**, **változtassa meg az Excel-diagram típusát**, **hozzon létre interaktív Java‑diagrammegoldásokat**, és gazdagítsa őket tooltip‑ekkel, adatcímkékkel és drill‑down hiperhivatkozásokkal az Aspose.Cells for Java segítségével. Ezek a fejlesztések sokkal vonzóbbá és informatívabbá teszik az Excel‑jelentéseket a végfelhasználók számára.

---

**Utolsó frissítés:** 2026-02-09  
**Tesztelt verzió:** Aspose.Cells for Java 24.12  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}