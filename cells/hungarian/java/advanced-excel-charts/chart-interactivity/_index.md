---
date: 2025-12-04
description: Tanulja meg, hogyan hozhat létre interaktív diagramot Java-ban az Aspose.Cells
  használatával, hogyan adhat hozzá tooltip-eket a diagramhoz, és hogyan készíthet
  drill‑down diagramot a gazdagabb adatmegjelenítés érdekében.
language: hu
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Interaktív diagram létrehozása Java-val az Aspose.Cells segítségével
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Interaktív diagram létrehozása Java-ban

## Bevezetés

Az interaktív diagramok lehetővé teszik a felhasználók számára, hogy felfedezzék az adatpontokat, részleteket lássanak hover‑rel, és akár mélyebb adatkészletekbe is belemerüljenek – mindezt anélkül, hogy elhagynák a táblázatot. Ebben az útmutatóban megtanulod, **hogyan hozhatsz létre interaktív diagram Java** alkalmazásokat az Aspose.Cells segítségével. Végigvezetünk a tooltip‑ek, adatcímkék hozzáadásán és egy drill‑down élmény megvalósításán, hogy diagramjaid még vonzóbbak és informatívabbak legyenek.

## Gyors válaszok
- **Melyik könyvtárat használja?** Aspose.Cells for Java  
- **Hozzáadhatok tooltip‑eket a diagramhoz?** Igen, a NSeries adatcímke API‑val  
- **Támogatja a drill‑down‑ot?** Igen, adatpontokhoz hiperhivatkozásokat csatolva  
- **Milyen fájlformátumot állít elő?** Standard XLSX munkafüzet beágyazott diagramokkal  
- **Szükség van licencre?** Egy ingyenes próba a kiértékeléshez elegendő; termeléshez kereskedelmi licenc szükséges  

## Előfeltételek

Mielőtt belemerülnél, győződj meg róla, hogy rendelkezel:

- Java fejlesztői környezettel (JDK 8+ ajánlott)  
- Aspose.Cells for Java könyvtárral (töltsd le a hivatalos [Aspose kiadási oldalról](https://releases.aspose.com/cells/java/))  
- Egy **data.xlsx** nevű minta Excel fájllal, amely a megjeleníteni kívánt adatokat tartalmazza  

## 1. lépés: Java projekt beállítása

1. Hozz létre egy új Java projektet a kedvenc IDE‑dben (IntelliJ IDEA, Eclipse, VS Code, stb.).  
2. Add hozzá az Aspose.Cells JAR‑t a projekt classpath‑jához – akár a `libs` mappába helyezve, akár Maven/Gradle függőségként.

## 2. lépés: Adatok betöltése

Az interaktív diagram felépítéséhez először egy munkalapra van szükség adatként. Az alábbi kódrészlet megnyit egy meglévő munkafüzetet, és lekéri az első munkalapot.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tipp:** Győződj meg róla, hogy a diagramhoz szánt adat-tartomány folytonos; az Aspose.Cells automatikusan felismeri a tartományt, amikor a sorozatot kötöd.

## 3. lépés: Diagram létrehozása

Most egy oszlopdiagramot hozunk létre, és elhelyezzük a munkalapon. A `ChartType.COLUMN` értéket bármely más típusra (pl. `ChartType.LINE`) cserélheted, ha más vizuális stílust szeretnél.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Miért fontos:** A diagram programozott létrehozása teljes kontrollt ad a méret, pozíció és adatforrás felett, ami elengedhetetlen az interaktív élmények építéséhez.

## 4. lépés: Interaktivitás hozzáadása

### Hogyan adjunk tooltip‑eket a diagramhoz

A tooltip‑ek (vagy adatcímkék, amelyek az értékeket mutatják) lehetővé teszik a felhasználók számára, hogy azonnal lássák az egyes oszlopok mögötti pontos számot. Az alábbi kód engedélyezi az adatcímkéket és beállítja, hogy az értéket jelenítsék meg.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Hogyan adjunk adatcímkéket (callout‑ok)

Ha a címkéket felhívásként (callout) szeretnéd megjeleníteni a sima szöveg helyett, állítsd be a `ShowLabelAsDataCallout` tulajdonságot.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Hogyan adjunk drill‑down diagramot

A drill‑down lehetővé teszi, hogy a felhasználó egy adatpontra kattintva egy kapcsolódó részletes nézetre ugorjon – ezt általában hiperhivatkozással valósítják meg. Az alábbiakban egy URL‑t csatolunk a sorozat első pontjához.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Gyakori hibaforrás:** Ne felejtsd el a hiperhivatkozás célját egy olyan oldalra mutatni, amely képes megjeleníteni a részletes adatokat (pl. webes jelentés vagy egy másik Excel lap). Ellenkező esetben a kattintás egy hibás linkhez vezet.

## 5. lépés: Munkafüzet mentése

A diagram konfigurálása után mentsd el a munkafüzetet. A keletkezett fájl tartalmazza az interaktív diagramot, amely megnyitható Excelben vagy bármely kompatibilis megjelenítőben.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Összegzés

Ebben az útmutatóban megtanultad, **hogyan hozhatsz létre interaktív diagram Java** megoldásokat az Aspose.Cells segítségével, a következő témák lefedésével:

- Adatok betöltése meglévő munkafüzetből  
- Oszlopdiagram programozott létrehozása  
- Tooltip‑ek és callout adatcímkék hozzáadása  
- Drill‑down funkció megvalósítása hiperhivatkozásokkal  
- A végleges munkafüzet mentése  

Ezek a technikák a statikus táblázatokat dinamikus, felhasználóbarát műszerfalakká alakítják, amelyek növelik az adatok megértését és a döntéshozatalt.

## Gyakran ismételt kérdések

**K: Hogyan változtathatom meg a diagram típusát?**  
V: Módosítsd a `ChartType` enum‑ot az `add` metódusban (pl. `ChartType.LINE` egy vonaldiagramhoz).

**K: Testreszabhatom a tooltip‑ek megjelenését?**  
V: Igen, a `DataLabels` objektumon keresztül állíthatod a betűméretet, színt, háttérszínt és egyéb stílus tulajdonságokat.

**K: Hogyan kezelem a diagram interaktivitását egy webalkalmazásban?**  
V: Exportáld a munkafüzetet XLSX‑be, majd használj egy JavaScript diagramkönyvtárat (pl. Highcharts) az adatok kliensoldali megjelenítéséhez, vagy ágyazd be az Excel fájlt egy Office Web Viewer‑be, amely támogatja a hiperhivatkozásokat.

**K: Hol találok további példákat?**  
V: Látogasd meg a hivatalos [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalt a diagramokhoz kapcsolódó osztályok és metódusok teljes listájáért.

**K: Szükség van licencre a termeléshez?**  
V: Igen, a kereskedelmi licenc kötelező a telepítéshez; egy ingyenes értékelő licenc elérhető teszteléshez.

---

**Utolsó frissítés:** 2025-12-04  
**Tesztelt verzió:** Aspose.Cells for Java 24.12 (a írás időpontjában legújabb)  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}