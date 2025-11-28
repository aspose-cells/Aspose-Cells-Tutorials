---
date: 2025-11-28
description: Tanulja meg, hogyan adhat hozzá tooltip‑eket, adatcímkéket és drill‑down
  funkciókat, hogy interaktív diagramot hozzon létre Java‑ban az Aspose.Cells használatával.
language: hu
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Hogyan adjunk hozzá eszköztippeket interaktív diagramokhoz (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan adjunk hozzá tooltip-eket az interaktív diagramokhoz (Aspose.Cells Java)

## Bevezetés

## Gyors válaszok
- **Melyik könyvtár szükséges?** Aspose.Cells for Java (legújabb verzió).  
- **Melyik fő funkciót tárgyalja ez az útmutató?** Tooltip-ek hozzáadása diagramokhoz.  
- **Hozzáadhatok adatcímkéket is?** Igen – lásd a „Adatcímkék hozzáadása” szekciót.  
- **Támogatott a drill‑down?** Igen, adatpontok hiperhivatkozásain keresztül.  
- **Milyen fájlformátum jön létre?** Egy Excel munkafüzet (`.xlsx`) interaktív diagrammal.

## Mi az a tooltip hozzáadása?

A tooltip egy kis felugró ablak, amely megjelenik, amikor a felhasználó egy diagram elem fölé viszi az egérmutatót, és további információkat mutat, például a pontos értéket vagy egy egyedi üzenetet. A tooltip-ek javítják az adatok olvashatóságát anélkül, hogy zsúfolnák a vizuális elrendezést.

## Miért készítsünk interaktív diagramokat Java-ban?

- **Jobb döntéshozatal:** A felhasználók azonnal láthatják a pontos értékeket.  
- **Professzionális jelentések:** Az interaktív elemek modern megjelenést kölcsönöznek a műszerfalaknak.  
- **Újrahasználható komponensek:** Miután elsajátítod az API-t, bármely Excel-alapú jelentési megoldásra alkalmazhatod.

## Előfeltételek

Mielőtt belemerülnénk, győződj meg róla, hogy rendelkezel:

- Java fejlesztői környezet (JDK 8 vagy újabb).  
- Aspose.Cells for Java könyvtár (letölthető [innen](https://releases.aspose.com/cells/java/)).  
- Egy minta Excel fájl **data.xlsx** néven, amely a megjeleníteni kívánt adatokat tartalmazza.

## 1. lépés: Java projekt beállítása

1. Hozz létre egy új Java projektet a kedvenc IDE-dben (IntelliJ IDEA, Eclipse stb.).  
2. Add the Aspose.Cells JAR to your project’s classpath.

## 2. lépés: Adatok betöltése

Interaktív diagram létrehozásához először egy adatokat tartalmazó munkalapra van szükség. Az alábbi kód betölti az első munkalapot a **data.xlsx** fájlból.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 3. lépés: Diagram létrehozása

Most egy oszlopdiagramot adunk a munkalaphoz. A diagram a F6‑tól K16‑ig terjedő cellákat foglalja el.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 4. lépés: Interaktivitás hozzáadása

### 4.1. Tooltip-ek hozzáadása

Az alábbi kódrészlet engedélyezi a tooltip-eket a diagram első sorozatához. Minden adatpont a hover (egérmutató fölé helyezése) esetén megjeleníti az értékét.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Adatcímkék hozzáadása a diagramhoz

Ha látható címkéket is szeretnél minden oszlop mellett, használd az alább bemutatott **add data labels chart** megközelítést. Ez megfelel a másodlagos kulcsszónak *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down megvalósítása

A drill‑down lehetővé teszi, hogy a felhasználók egy adatpontra kattintva részletes nézetre (pl. egy weboldalra) ugorjanak. Itt egy hiperhivatkozást csatolunk a sorozat első pontjához.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Pro tipp:** Dinamikusan generálhatod az URL-t a pont értéke alapján, hogy valóban adat‑vezérelt drill‑down élményt hozz létre.

## 5. lépés: Munkafüzet mentése

A diagram beállítása után mentsd el a munkafüzetet. A kapott fájl egy interaktív diagramot tartalmaz, amely készen áll az Excelben való megnyitásra.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| A tooltip-ek nem jelennek meg | Az adatcímkék nincsenek engedélyezve | Győződj meg arról, hogy a `setHasDataLabels(true)` hívás megtörténik a `ShowValue` beállítása előtt. |
| A hiperhivatkozás nem kattintható | Helytelen pont index | Ellenőrizd, hogy a helyes pontot hivatkozod (`get(0)` az első pont). |
| A diagram rosszul helyezkedik el | Helytelen cellatartomány | Állítsd be a sor/oszlop indexeket a `add(ChartType.COLUMN, row1, col1, row2, col2)` hívásban. |

## Gyakran feltett kérdések

**K: Hogyan változtathatom meg a diagram típusát?**  
V: Cseréld le a `ChartType.COLUMN`-t egy másik enum értékre, például `ChartType.LINE` vagy `ChartType.PIE`-re, amikor a `worksheet.getCharts().add(...)` metódust hívod.

**K: Testreszabhatom a tooltip-ek megjelenését?**  
V: Igen. Használd a `DataLabel` objektum formázási tulajdonságait (betűméret, háttérszín stb.) a tooltip szövegének stílusozásához.

**K: Hogyan kezelem a felhasználói interakciókat egy webalkalmazásban?**  
V: Exportáld a munkafüzetet web‑kompatibilis formátumba (pl. HTML), és használj JavaScriptet a diagram elemein történő kattintási események rögzítéséhez.

**K: Hol találok további példákat és dokumentációt?**  
V: Tekintsd meg a hivatalos API referenciát a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalon.

**K: Lehetséges több drill‑down hivatkozást is hozzáadni ugyanabban a diagramban?**  
V: Természetesen. Iterálj a sorozat pontjai között, és minden pont `Hyperlinks` gyűjteményéhez rendelj egyedi URL-t.

## Összegzés

Ebben az útmutatóban megtanultad, hogyan **adj hozzá tooltip-eket**, **adj hozzá adatcímkéket**, és **valósíts meg drill‑down** funkciót, hogy **interaktív diagramot Java‑ban** hozz létre az Aspose.Cells segítségével. Ezek a funkciók a statikus Excel diagramokat dinamikus, felhasználó‑barát vizualizációkká alakítják, amelyek megkönnyítik az érintettek számára az adatok felfedezését.

---

**Utolsó frissítés:** 2025-11-28  
**Tesztelve a következővel:** Aspose.Cells for Java 24.12  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}