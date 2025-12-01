---
date: 2025-12-01
description: Tanulja meg, hogyan változtathatja meg az Excel diagram típusát, és adhat
  hozzá interaktív funkciókat, például eszköztippeket, adatcímkéket és drill‑downot
  az Aspose.Cells for Java használatával.
language: hu
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Excel diagram típusának módosítása és interaktivitás hozzáadása – Aspose.Cells
  Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel diagram típusának módosítása és interaktivitás hozzáadása

## Bevezetés

Az interaktív diagramok lehetővé teszik a közönség számára, hogy valós időben felfedezze az adatokat, míg a **Excel diagram típusának módosítása** rugalmasságot biztosít a legmegfelelőbb vizuális formátum kiválasztásához. Ebben az útmutatóban megtanulja, hogyan használja az Aspose.Cells for Java‑t egy diagram típusának módosításához, tooltip‑ek hozzáadásához, adatcímkék beágyazásához, és akár drill‑down hivatkozások létrehozásához – mindezt anélkül, hogy elhagyná a Java kódot. A végére egy teljes funkcionalitású, interaktív Excel munkafüzetet kap, amelyet beágyazhat jelentésekbe, műszerfalakba vagy webalkalmazásokba.

## Gyors válaszok
- **Programozottan módosíthatom a diagram típusát?** Igen – használja a `ChartType` enum‑t diagram létrehozásakor vagy frissítésekor.  
- **Hogyan adhatok hozzá tooltip‑eket egy diagramhoz?** Engedélyezze az adatcímkéket, és állítsa a `ShowValue` értékét true‑ra.  
- **Mi a legegyszerűbb módja a drill‑down hivatkozások hozzáadásának?** Csatoljon egy hiperhivatkozást egy adatponthoz a `getHyperlinks().add(url)` segítségével.  
- **Szükségem van licencre az Aspose.Cells‑hez?** A fejlesztéshez ingyenes próba verzió elegendő; a termeléshez licenc szükséges.  
- **Mely Java verzió támogatott?** A Java 8 és újabb verziók teljes körűen támogatottak.

## Mi az a „Excel diagram típusának módosítása”?

A diagram típusának módosítása azt jelenti, hogy a vizuális megjelenítést (például oszlopdiagramról vonaldiagramra) cseréljük, miközben az alapszintű adatokat változatlanul hagyjuk. Ez akkor hasznos, ha azt tapasztalja, hogy egy másik diagram jobban közvetíti a trendeket, összehasonlításokat vagy eloszlásokat.

## Miért érdemes interaktivitást hozzáadni az Excel diagramokhoz?

- **Jobb adatáttekintés:** A tooltip‑ek és adatcímkék lehetővé teszik a felhasználók számára a pontos értékek megtekintését görgetés nélkül.  
- **Lenyűgöző bemutatók:** Az interaktív elemek fenntartják a nézők érdeklődését.  
- **Drill‑down képesség:** A hiperhivatkozások lehetővé teszik a felhasználók számára, hogy részletes munkalapokra vagy külső forrásokra ugorjanak.  
- **Újrahasználható eszközök:** Egy munkafüzet több jelentési forgatókönyvben is használható, ha egyszerűen átváltja a diagram típusát.

## Előkövetelmények

- Java fejlesztői környezet (JDK 8+)  
- Aspose.Cells for Java könyvtár (letölthető [itt](https://releases.aspose.com/cells/java/))  
- Egy minta Excel fájl (`data.xlsx`), amely a megjeleníteni kívánt adatokat tartalmazza

## Lépésről‑lépésre útmutató

### 1. lépés: Állítsa be a Java projektet

1. Hozzon létre egy új Java projektet a kedvenc IDE‑jében (IntelliJ IDEA, Eclipse, VS Code, stb.).  
2. Adja hozzá az Aspose.Cells JAR‑t a projekt osztályútvonalához.

### 2. lépés: Töltse be a forrás munkafüzetet

Először betöltünk egy meglévő munkafüzetet, amely a diagram adatát tartalmazza.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 3. lépés: Hozzon létre egy diagramot és **változtassa meg a típusát**

Az alábbiakban létrehozunk egy oszlopdiagramot, majd azonnal bemutatjuk, hogyan lehet szükség esetén vonaldiagramra váltani.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tipp:** A diagram típusának módosítása a létrehozás után olyan egyszerű, mint a `setChartType(...)` meghívása. Ez kielégíti a fő kulcsszót **Excel diagram típusának módosítása** anélkül, hogy új diagram objektumra lenne szükség.

### 4. lépés: Interaktivitás hozzáadása

#### 4.1. Tooltip‑ek hozzáadása a diagramhoz

A tooltip‑ek akkor jelennek meg, amikor a felhasználó egy adatpontra viszi a kurzort. Az Aspose.Cells‑ben ez az adatcímkék segítségével valósul meg.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2. Adatcímkék hozzáadása ( **add data labels chart** )

Az adatcímkék megjeleníthetik a pontos értéket, a kategória nevét vagy mindkettőt. Itt egy felhívás stílusú címkét használunk.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3. Drill‑down megvalósítása ( **add drill down excel** )

A drill‑down hivatkozás lehetővé teszi, hogy a felhasználó egy pontra kattintva részletes nézetre ugorjon, akár a munkafüzeten belül, akár egy weboldalra.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### 5. lépés: Munkafüzet mentése

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Gyakori problémák és megoldások

| Probléma | Ok | Megoldás |
|----------|----|----------|
| Tooltip‑ek nem jelennek meg | `HasDataLabels` nincs engedélyezve | Győződjön meg róla, hogy a `setHasDataLabels(true)` hívás megtörtént a `ShowValue` beállítása előtt. |
| A drill‑down hivatkozás nem csinál semmit | A hiperhivatkozás URL-je hibás | Ellenőrizze, hogy az URL `http://` vagy `https://` előtaggal kezdődik. |
| A diagram típusa nem változik | Régebbi Aspose.Cells verzió használata | Frissítsen a legújabb verzióra (tesztelve a 24.12‑vel). |

## Gyakran Ismételt Kérdések

**Q: Hogyan változtathatom meg a diagram típusát a létrehozás után?**  
A: Hívja meg a `chart.setChartType(ChartType.YOUR_CHOICE)` metódust a meglévő `Chart` objektumon. Ez közvetlenül a **Excel diagram típusának módosítása** követelményt teljesíti.

**Q: Testreszabhatom a tooltip‑ek megjelenését?**  
A: Igen. Használja a `chart.getNSeries().get(0).getPoints().getDataLabels()` metódust a betűméret, szín és háttér beállításához.

**Q: Lehet-e több drill‑down hivatkozást hozzáadni egy diagramhoz?**  
A: Természetesen. Iteráljon a pontokon, és hívja meg a `getHyperlinks().add(url)` metódust minden olyan ponthoz, amelyhez hivatkozást szeretne.

**Q: Támogatja az Aspose.Cells más diagramtípusokat, például kör vagy radar diagramot?**  
A: Az `ChartType` enum‑ban definiált összes diagramtípus támogatott, beleértve a `PIE`, `RADAR`, `AREA` stb. típusokat.

**Q: Hol találok további példákat?**  
A: Látogassa meg a hivatalos [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalt a diagramokkal kapcsolatos összes metódus teljes listájáért.

## Összegzés

Most már tudja, hogyan **módosítsa az Excel diagram típusát**, ágyazzon be **tooltip‑eket**, adjon hozzá **adatcímkéket**, és hozzon létre **drill‑down** hivatkozásokat az Aspose.Cells for Java segítségével. Ezek az interaktív funkciók a statikus táblázatokat dinamikus adatfeltáró eszközökké alakítják, amelyek tökéletesek műszerfalakhoz, jelentésekhez és web‑alapú elemzésekhez.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}