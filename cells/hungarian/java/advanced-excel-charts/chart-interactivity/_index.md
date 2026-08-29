---
date: 2026-08-21
description: Ismerje meg, hogyan adhat hozzá tooltip-eket, adatcímkéket, és módosíthatja
  a diagram típusát az Excel diagramokban az Aspose.Cells for Java használatával –
  lépésről‑lépésre útmutató interaktív példákkal.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Excel diagram típusának módosítása
og_description: Ismerje meg, hogyan adhat hozzá tooltip-eket, adatcímkéket, és módosíthatja
  a diagram típusát az Excel diagramokban az Aspose.Cells for Java használatával –
  lépésről‑lépésre útmutató interaktív példákkal.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Hogyan adjunk hozzá tooltip-eket és adatcímkéket az Excel diagramokhoz Java-ban
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Hogyan adjunk hozzá tooltip-eket és adatcímkéket az Excel diagramokhoz Java-ban
url: /hu/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adjon adatcímkéket az Excel diagramhoz és módosítsa a diagram típusát – Aspose.Cells Java

Az interaktív diagramok új szintre emelik az Excel jelentéseket, és **how to add tooltips** teszi az információt azonnal olvashatóvá. Ebben az oktatóanyagról megtanulja, hogyan **add data labels to Excel chart**, **change the chart type**, és interaktív Java megoldásokat hozhat létre az Aspose.Cells segítségével. Bemutatjuk továbbá, hogyan adhat hozzá tooltips-et és egy egyszerű drill‑down hiperhivatkozást, hogy a közönség mélyebben felfedezhesse az adatokat.

## Gyors válaszok
- **Melyik könyvtárat használnak?** Aspose.Cells for Java  
- **Módosíthatom a diagram típusát?** Igen – egyszerűen módosítsa a `ChartType` enumot a diagram létrehozásakor.  
- **Hogyan adhatok tooltips-et egy diagramhoz?** Használja az adatcímke API-t (`setHasDataLabels(true)`) és engedélyezze az érték megjelenítését.  
- **Támogatott a drill‑down?** Csatolhat hiperhivatkozásokat az adatpontokhoz az alapvető drill‑down viselkedéshez.  
- **Előfeltételek?** Java IDE, Aspose.Cells JAR, és egy Excel fájl mintaadatokkal.

## Mi az a how to add tooltips?
**How to add tooltips** arra a folyamatra utal, amely lehetővé teszi a hover‑over szöveg megjelenítését, ami egy adatpont értékét vagy egyéni információt mutat egy Excel diagramon. Az Aspose.Cells-ben ez a diagram adatcímke beállításain keresztül valósul meg. A tooltips segíti a felhasználókat gyorsan megérteni az adatokat anélkül, hogy a diagramot zsúfolná, és testreszabható betűtípus, szín és formátum szerint.

## Miért használjunk interaktív diagramokat az Aspose.Cells-szel?
Az Aspose.Cells támogatja a **50+ bemeneti és kimeneti formátumot** – beleértve az XLSX, CSV, PDF és HTML formátumokat – és képes **több mint 1 000 munkalappal** rendelkező munkafüzeteket feldolgozni anélkül, hogy a teljes fájlt a memóriába töltené, gyors, szerver‑oldali diagramgenerálást biztosítva vállalati jelentésekhez. Az interaktív diagramok lehetővé teszik hiperhivatkozások beágyazását, dinamikus adatfrissítéseket és exportálást web‑barát formátumokba, így ideálisak műszerfalakhoz és jelentési portálokhoz.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy a következőkkel rendelkezik:

- Java fejlesztői környezet (JDK 8+ ajánlott)  
- Aspose.Cells for Java könyvtár (letölthető a [Aspose.Cells for Java letöltési oldalról](https://releases.aspose.com/cells/java/))  
- Egy minta munkafüzet (`data.xlsx`), amely tartalmazza a megjeleníteni kívánt adatokat  

## 1. lépés: Java projekt beállítása

1. Hozzon létre egy új Java projektet a kedvenc IDE-jében (IntelliJ IDEA, Eclipse, stb.).  
2. Adja hozzá az Aspose.Cells JAR-t a projekt build útvonalához vagy Maven/Gradle függőségekhez.

## 2. lépés: adatok betöltése

A diagramokkal való munkához először egy memóriába betöltött munkafüzetre van szükség.

A `Workbook` osztály egy Excel fájlt képvisel, a `Worksheet` pedig egyetlen munkalapot a fájlon belül.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Hogyan változtassuk meg a diagram típusát az Aspose.Cells-ben?

Hozzon létre egy új diagramot a kívánt `ChartType` enummal; az Aspose.Cells nem módosítja egy meglévő diagram típusát helyben, ezért egy új diagramot kell hozzáadni a megfelelő típussal, és opcionálisan el kell távolítani a régit. Ez a megközelítés biztosítja, hogy minden sorozat és tengely helyesen újraépüljön az új vizuális megjelenítéshez.

## 3. lépés: diagram létrehozása (és típusának módosítása)

Bármilyen diagram típust választhat, amely megfelel az elemzésnek. Az alábbiakban egy **oszlopdiagramot** hozunk létre, de egyszerűen átválthat vonal-, kör- vagy sávdiagramra a `ChartType` enum módosításával.

`Chart` objektum metódusokat biztosít az adatok vizuális megjelenítésének konfigurálásához a munkalapon.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tipp:** A **change Excel chart type** módosításához cserélje le a `ChartType.COLUMN`-t `ChartType.LINE`, `ChartType.PIE` stb. értékekre.

## Hogyan adjunk tooltips-et egy Excel diagramhoz?

Töltse be a diagramot, engedélyezze az adatcímkéket, és állítsa be a `showValue` jelzőt. A tooltip ezután megjeleníti az alatta lévő cella értékét, amikor a felhasználó egy adatpontra húzza az egeret a megjelenített Excel fájlban vagy HTML nézetben. A tooltip betűtípusa, színe és háttérszíne is testreszabható a jelentés stílusához igazítva.

`DataLabel` osztály szabályozza az adatcímkék megjelenését és tartalmát, amelyek egyúttal tooltipként is működnek.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## 4. lépés: interaktivitás hozzáadása

### 4.1. Tooltips hozzáadása (add tooltips to chart)

A tooltips megjelenik, amikor a felhasználó egy adatpontra húzza az egeret. Az alábbi kód engedélyezi az adatcímkéket és megjeleníti az értéket tooltipként.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Adatcímkék hozzáadása – **add data labels to excel chart**

Az adatcímkék állandó vizuális jelzést biztosítanak a diagramon. Megjelenítheti őket felhívásokként a jobb olvashatóság érdekében.

`DataLabel` osztály szabályozza a címkék megjelenését minden sorozatnál. A `setHasDataLabels(true)` hívásával és a `setShowValue(true)` stb. tulajdonságok beállításával a numerikus értéket közvetlenül a diagramra ágyazza, így az azonnal látható anélkül, hogy interakcióra lenne szükség. További beállítások lehetővé teszik sorozatnevek, százalékok vagy egyéni szöveg megjelenítését a gazdagabb kontextusért.

> **Miért adjunk adatcímkéket?** Az adatcímkék közvetlenül a diagramra helyezése megszünteti a felhasználók számára a hover vagy a becslés szükségességét, javítva a jelentés átláthatóságát.

### 4.3. Drill‑down megvalósítása (hiperhivatkozás egy adatpontra)

Egy egyszerű mód a drill‑down képesség hozzáadására, ha egy adott ponthoz hiperhivatkozást csatol. A pontra kattintva egy részletes információkat tartalmazó weboldal nyílik meg.

`Hyperlink` osztály kattintható linket csatol egy diagram elemhez, lehetővé téve a drill‑down navigációt.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Hogyan adjunk adatcímkéket egy Excel diagramhoz?

`DataLabel` osztály szabályozza a címkék megjelenését minden sorozatnál. A `setHasDataLabels(true)` hívásával és a `setShowValue(true)` stb. tulajdonságok beállításával a numerikus értéket közvetlenül a diagramra ágyazza, így az azonnal látható anélkül, hogy interakcióra lenne szükség. További beállítások lehetővé teszik sorozatnevek, százalékok vagy egyéni szöveg megjelenítését a gazdagabb kontextusért.

## 5. lépés: munkafüzet mentése

A diagram konfigurálása után mentse a munkafüzetet, hogy az interaktív funkciók az output fájlban tárolódjanak.

`workbook.save` hívásával a módosított munkafüzet a kiválasztott formátumban kerül mentésre.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| **Tooltips nem jelenik meg** | Győződjön meg róla, hogy a `setHasDataLabels(true)` hívás megtörtént a `setShowValue(true)` beállítása előtt. |
| **Hyperlink nem kattintható** | Ellenőrizze, hogy a kimeneti formátum támogatja-e a hiperhivatkozásokat (pl. XLSX, nem CSV). |
| **Diagram típusa nem változik** | Ellenőrizze, hogy a diagram hozzáadásakor a megfelelő `ChartType` enumot módosította-e. |

## Gyakran feltett kérdések

**Q: Hogyan változtathatom meg a diagram típusát a létrehozás után?**  
A: Létre kell hoznia egy új diagramot a kívánt `ChartType`-tal. Az Aspose.Cells nem biztosít helyben történő típuskonverziót, ezért távolítsa el a régi diagramot és adjon hozzá egy újat.

**Q: Testreszabhatom a tooltips megjelenését?**  
A: Igen. Használja a `DataLabel` tulajdonságokat, mint például `setFontSize`, `setFontColor`, és `setBackgroundColor`, a tooltip szöveg stílusozásához.

**Q: Hogyan kezeljem a felhasználói interakciókat egy webalkalmazásban?**  
A: Exportálja a munkafüzetet HTML vagy XLSX fájlba, és használjon JavaScriptet a kliens oldalon a diagram elemeire történő kattintási események rögzítéséhez.

**Q: Hol találok további példákat és dokumentációt?**  
A: Látogassa meg a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oldalt a diagramokhoz kapcsolódó osztályok és metódusok teljes listájáért.

## Következtetés

Most már tudja, hogyan **add data labels to Excel chart**, **change Excel chart type**, **create interactive chart Java** megoldásokat hozhat létre, és gazdagíthatja őket tooltips-ekkel, adatcímkékkel és drill‑down hiperhivatkozásokkal az Aspose.Cells for Java segítségével. Ezek a fejlesztések sokkal vonzóbbá és átfogóbbá teszik az Excel jelentéseket a végfelhasználók számára.

---

**Utoljára frissítve:** 2026-08-21  
**Tesztelve a következővel:** Aspose.Cells for Java 24.12  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [Hogyan módosítsuk az Excel diagramokat és adatcímkéket az Aspose.Cells for Java használatával](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Excel diagram tengelycímkék kinyerése Aspose.Cells Java segítségével: átfogó útmutató](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Buborékdiagramok létrehozása Excelben az Aspose.Cells for Java használatával: lépésről‑lépésre útmutató](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}