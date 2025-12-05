---
date: 2025-12-05
description: Tanulja meg, hogyan adjon hozzá adatcímkéket a diagramhoz, és hogyan
  hozzon létre interaktív diagramot Java-ban az Aspose.Cells használatával. Adjon
  hozzá tooltippeket, adatcímkéket és drill‑down funkciót.
language: hu
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Adjon hozzá adatcímkéket a diagramhoz interaktivitással az Aspose.Cells Java-ban
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adatcímkék hozzáadása diagramhoz interaktivitással az Aspose.Cells Java-ban

Az interaktív diagramok lehetővé teszik a felhasználók számára, hogy valós időben felfedezzék az adatokat. Ebben az útmutatóban **adatcímkék diagram** funkciókat – tooltip‑eket, adatcímkéket és drill‑down műveleteket – adunk hozzá az Aspose.Cells for Java segítségével. A végén egy kifinomult, interaktív diagramot kapunk, amely az összetett adatokat azonnal érthetővé teszi.

## Gyors válaszok
- **Melyik könyvtárra van szükségem?** Aspose.Cells for Java  
- **Hozzáadhatok tooltip‑eket egy Excel diagramhoz?** Igen – a API adatcímke‑beállításaival.  
- **Mely diagramtípusok támogatják az interaktivitást?** A legtöbb beépített típus (oszlop, vonal, kör, stb.).  
- **Szükség van licencre a termeléshez?** Érvényes Aspose.Cells licenc szükséges.  
- **Mennyi időt vesz igénybe a megvalósítás?** Körülbelül 10–15 perc egy alap diagramhoz.

## Mi az a „adatcímkék hozzáadása diagram”?
Az *adatcímkék hozzáadása diagram* egy olyan diagram, ahol minden adatpont közvetlenül a vizuális elemre helyezett címkét (értéket, nevet vagy egyéni szöveget) jelenít meg. Ez megkönnyíti a nézők számára a pontos értékek leolvasását anélkül, hogy a kurzort mozgatniuk vagy külön legendát keresniük kellene.

## Miért érdemes interaktív diagram‑Java megoldásokat készíteni?
Az interaktivitás beágyazása – tooltip‑ek, kattintható pontok, drill‑down hivatkozások – a statikus táblázatokat felfedező irányítópultokká alakítja. A felhasználók:
- Gyorsan azonosíthatják a kiugró értékeket.  
- Egyetlen kattintással mélyebb adatrétegeket érhetnek el.  
- Javíthatják a döntéshozatali sebességet, mivel nincs szükség külön jelentésekre.

## Előfeltételek

Mielőtt belevágnánk, győződjön meg róla, hogy rendelkezik:

- Java fejlesztői környezettel (JDK 8+ ajánlott).  
- Aspose.Cells for Java könyvtárral (letölthető innen: [here](https://releases.aspose.com/cells/java/)).  

## 1. lépés: Java projekt beállítása

1. Hozzon létre egy új Java projektet a kedvenc IDE‑jében (IntelliJ, Eclipse, VS Code, stb.).  
2. Adja hozzá az Aspose.Cells for Java JAR‑t a projekt osztályútvonalához.

## 2. lépés: Adatok betöltése

Az interaktív diagram felépítéséhez először adatokat kell betölteni egy munkalapra. Az alábbi kódrészlet egy meglévő **data.xlsx** munkafüzetet tölt be.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 3. lépés: Diagram létrehozása

Most egy oszlopdiagramot hozunk létre, és elhelyezzük a munkalapon. Nyugodtan cserélje le a `ChartType.COLUMN`‑t egy másik típusra, ha úgy kívánja.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 4. lépés: Interaktivitás hozzáadása – az „adatcímkék hozzáadása diagram” magja

### 4.1. Tooltip‑ek hozzáadása (add tooltips excel chart)

A tooltip‑ek akkor jelennek meg, amikor a felhasználó egy adatpontra viszi a kurzort. Az alábbi kód engedélyezi őket az adatcímkék bekapcsolásával és az érték megjelenítésével.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Adatcímkék hozzáadása (add data labels chart)

Az adatcímkék a vizuális szöveg, amely minden pont mellett megjelenik. Ez a részlet a diagramot úgy konfigurálja, hogy felhívó (callout) címkéket jelenítsen meg a sima értékek helyett.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down megvalósítása (create interactive chart java)

A drill‑down lehetővé teszi, hogy a felhasználó egy pontra kattintva részletes nézetre ugorjon. Itt egy hiperhivatkozást csatolunk az első adatponthoz; ezt bármely más pontra megismételheti.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 5. lépés: Munkafüzet mentése

A diagram beállítása után mentse a munkafüzetet egy új fájlba, hogy megnyithassa Excelben és tesztelhesse az interaktivitást.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Gyakori problémák és tippek

| Probléma | Megoldás |
|----------|----------|
| **Tooltip‑ek nem jelennek meg** | Győződjön meg róla, hogy a `setHasDataLabels(true)` metódust a `ShowValue` beállítása előtt hívja meg. |
| **A hiperhivatkozás nem kattintható** | Ellenőrizze, hogy az URL helyesen van‑formázva, és hogy az Excel biztonsági beállításai engedélyezik a külső hivatkozásokat. |
| **Diagramtípus-eltérés** | Egyes diagramtípusok (pl. radar) korlátozott címke‑támogatással rendelkeznek – válasszon kompatibilis típust, például oszlop vagy vonal. |
| **Teljesítménycsökkenés nagy adathalmazoknál** | Korlátozza a címkékkel megjelenített pontok számát; kevésbé kritikus soroknál használja a `setShowValue(false)` beállítást. |

## Gyakran ismételt kérdések

**K: Hogyan változtathatom meg a diagram típusát?**  
V: Módosítsa a `ChartType` enum értékét a diagram létrehozásakor (például `ChartType.LINE` egy vonaldiagramhoz).

**K: Testreszabhatom a tooltip‑ek megjelenését?**  
V: Igen – a `DataLabel` objektum betűtípusát, háttérszínét és szegélytulajdonságait használva formázhatja a tooltip‑eket.

**K: Hogyan kezelem a felhasználói interakciókat egy webalkalmazásban?**  
V: Exportálja a munkafüzetet HTML‑oldalra, vagy használja az Aspose.Cells Cloud‑t a diagram rendereléséhez, majd JavaScript‑kel ragadja meg a kattintási eseményeket.

**K: Hol találok további példákat és dokumentációt?**  
V: Látogassa meg a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalt a diagramokhoz kapcsolódó osztályok és metódusok teljes listájáért.

## Összegzés

Ebben az útmutatóban bemutattuk, hogyan adhatunk hozzá **adatcímkék diagram** funkciókat, és hogyan hozhatunk létre **interaktív diagram Java** megoldást az Aspose.Cells segítségével. Tooltip‑ek, adat‑hívások és drill‑down hiperhivatkozások hozzáadásával egy statikus Excel diagramot dinamikus adat‑felfedező eszközzé alakítunk, amely növeli a betekintést és a használhatóságot.

---

**Utolsó frissítés:** 2025-12-05  
**Tesztelt verzió:** Aspose.Cells for Java 24.12  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}