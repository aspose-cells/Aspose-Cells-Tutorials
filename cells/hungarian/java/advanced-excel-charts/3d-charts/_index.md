---
date: 2026-08-21
description: Ismerje meg, hogyan exportálhat chart-et képként, és hozhat létre 3D
  pie chart-okat Java-ban az Aspose.Cells segítségével. Generáljon 3D bar chart-okat,
  adjon hozzá 3D chart-okat az Excelhez, és mentse a munkafüzeteket XLSX formátumban.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: 3D pie chart létrehozása Java-ban
og_description: Exportáljon chart-et képként, és készítsen 3D pie chart-okat Java-ban
  az Aspose.Cells használatával. Lépésről lépésre útmutató a 3D bar és pie chart-ok
  generálásához, testreszabásához, valamint a munkafüzetek XLSX formátumban történő
  mentéséhez.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Export chart as image and create 3D pie chart in Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Hogyan exportáljunk chart-et képként, és hozzunk létre 3D pie chart-ot Java-ban
url: /hu/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 3D kördiagram létrehozása Java

## Bevezetés a 3D diagramokba

Az Aspose.Cells for Java egy erőteljes Java API Excel fájlok kezelésére, és egyszerűvé teszi a **3D kördiagram** projektek, valamint a klasszikus 3‑D oszlopdiagramok létrehozását. Ebben az oktatóanyagról pontosan megmutatjuk, hogyan **exportálhatja a diagramot képként**, hogyan generáljon egy 3‑D oszlopdiagramot, hogyan alkalmazza ugyanazt a megközelítést egy 3‑D kördiagramra, hogyan testreszabja a megjelenést, és végül hogyan **adjon 3d diagram excel** fájlokat a jelentéseihez. Akár pénzügyi műszerfalat, értékesítési teljesítmény‑lapot vagy tudományos adatok vizualizációját építi, az alábbi lépések szilárd alapot nyújtanak.

## Gyors válaszok
- **Milyen könyvtárra van szükségem?** Aspose.Cells for Java (legújabb verzió)  
- **Generálhatok 3D oszlopdiagramot?** Igen – használja a `ChartType.BAR_3_D` értéket  
- **Szükség van licencre?** Egy érvényes licenc eltávolítja a kiértékelési korlátokat  
- **Mely Excel verziók támogatottak?** Minden fő verzió 2003‑tól 2023‑ig  
- **Lehet a diagramot képként exportálni?** Igen – hívja a `chart.toImage()` metódust a diagram létrehozása után  

## Mi a 3D diagram?
A 3D diagramok mélységet adnak a hagyományos 2D vizualizációknak, segítve a nézőket a többdimenziós kapcsolatok intuitív megértésében. Különösen hasznosak, ha több kategóriát kell egymás mellett összehasonlítani, miközben egyértelmű vizuális hierarchiát tartanak fenn. A harmadik dimenzió hozzáadásával ezek a diagramok kiemelhetik a nagyságrendi különbségeket, amelyek lapos ábrázolásban kevésbé nyilvánvalóak, ezáltal a komplex adatokat könnyebben értelmezhetővé téve az üzleti érintettek számára.

## Miért használja az Aspose.Cells for Java‑t 3D oszlopdiagram generálásához?
Az Aspose.Cells for Java több mint 150 beépített diagramtípust és több mint 100 Excel‑függvényt támogat, így egy teljes körű motor áll rendelkezésre, amely minden Excel‑verzióval (2003‑tól 2023‑ig) működik Microsoft Office nélkül. Ez azt jelenti, hogy **3d bar chart** objektumokat programozottan hozhat létre előre látható eredményekkel és minimális terheléssel.

## Az Aspose.Cells for Java beállítása

### Letöltés és telepítés
Az Aspose.Cells for Java könyvtárat letöltheti a hivatalos weboldalról. Kövesse a megadott Maven/Gradle útmutatót, vagy adja hozzá a JAR‑t közvetlenül a projekt osztályútvonalához.

### Licenc inicializálása
A `License` osztályt használják az Aspose.Cells licenc alkalmazásához és a teljes funkcionalitás feloldásához.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Alap 3D diagram létrehozása

### Szükséges könyvtárak importálása
Először hozza be a szükséges osztályokat:  
```java
import com.aspose.cells.*;
```

### Munkafüzet inicializálása
Hozzon létre egy új munkafüzetet, amely a diagramot fogja tartalmazni:  
```java
Workbook workbook = new Workbook();
```

### Adatok hozzáadása a diagramhoz
Töltse fel a munkalapot mintaadatokkal, amelyeket a diagram felhasznál:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Hogyan generáljunk 3D oszlopdiagramot Java‑ban
Egy 3D oszlopdiagram létrehozásához adjon egy diagramobjektumot a munkalaphoz, állítsa be a típusát `ChartType.BAR_3_D`‑re, majd kössön adat sorozatokat a megfelelő cellákhoz. A diagram megjelenésének beállítása után renderelheti vagy exportálhatja igény szerint.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Diagram mentése fájlba
Végül írja a munkafüzetet (amely már tartalmazza a 3‑D diagramot) a lemezre. Ez **save workbook xlsx** a szabványos Excel formátumban:  
```java
workbook.save("3D_Chart.xlsx");
```

## Hogyan hozzunk létre 3D kördiagramot az Aspose.Cells for Java‑val
Ha kördiagram‑stílusú vizualizációra van szüksége, a munkafolyamat majdnem azonos – csak a `ChartType` enum változik. Cserélje le a `ChartType.BAR_3_D`‑t `ChartType.PIE_3_D`‑re a diagram hozzáadásakor, és irányítsa a sorozatot ugyanarra az adat tartományra. A diagram létrehozása után beállíthat egy leíró címet, módosíthatja a szelet színeit, és exportálhatja az eredményt képként. Ez a megközelítés lehetővé teszi, hogy ugyanazt az adat‑előkészítő kódot újrahasználja, miközben más vizuális perspektívát kínál.

## Hogyan exportáljuk a diagramot képként Java‑ban
A `Chart` objektum `toImage` metódusa a diagramot képfájlba menti. Bármely 3D diagramot egyetlen hívással exportálhat raster képpé: `chart.toImage("myChart.png", ImageFormat.getPng())`. Ez a metódus a diagramot pontosan úgy rendereli, ahogy az Excelben megjelenik, megőrizve a 3‑D mélységet, színeket és jelmagyarázatokat, és a megadott fájlútra írja ki. Használjon PNG‑t veszteségmentes minőséghez, vagy JPEG‑t kisebb fájlméretekhez, ha a képet webes jelentésekbe ágyazza be.

## A 3D diagramok különböző típusai
Az Aspose.Cells for Java többféle 3D diagramot támogat, amelyeket **add 3d chart excel** fájlokkal használhat:

- **Oszlopdiagramok** – ideálisak kategóriák összehasonlításához.  
- **Kördiagramok** – arányos hozzájárulásokat mutatnak (beleértve a 3D kördiagramot).  
- **Vonaldiagramok** – trendeket ábrázolnak időben.  
- **Területdiagramok** – a változás nagyságát hangsúlyozzák.

A `ChartType` enumot a fenti típusok bármelyikére átállíthatja, miközben ugyanazt a létrehozási mintát követi.

## Haladó diagram testreszabás

### Címek és címkék hozzáadása
Adjon a diagramnak kontextust egy leíró cím és tengelycímkék beállításával.

### Színek és stílusok beállítása
Használja a `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` metódust a vállalati arculathoz való igazításhoz.

### Diagram tengelyek kezelése
Finomhangolja a tengely skálákat, intervallumokat és jelölőket a jobb olvashatóság érdekében.

### Jelmagyarázatok hozzáadása
Engedélyezze a jelmagyarázatokat a `chart.getLegend().setVisible(true)` hívással, hogy a nézők azonosíthassák az egyes adat sorozatokat.

### Diagramok exportálása képként
Amikor statikus képre van szükség webes jelentéshez, hívja a `chart.toImage("chart.png", ImageFormat.getPng())` metódust. Ez teljesíti a **convert chart png** felhasználási esetet anélkül, hogy elhagyná a munkafüzetet.

## Adatintegráció
Az Aspose.Cells for Java adatokat tud lekérni adatbázisokból, CSV‑fájlokból vagy élő API‑kból. Egyszerűen töltse fel a munkalap celláit a lekért adatokkal, mielőtt a tartományt a diagramhoz csatolná. Ez dinamikussá és naprakésszé teszi a **add 3d chart excel** munkafolyamatot.

## Összegzés
Ebben az útmutatóban végigvezettük, hogyan **create 3d pie chart** és **create 3d bar chart** projekteket indíttól a végéig – a könyvtár beállítása, adatok hozzáadása, 3‑D oszlopdiagram generálása, ugyanazon lépések alkalmazása 3‑D kördiagramra, és fejlett stílusok alkalmazása. Az Aspose.Cells for Java egy megbízható, verzió‑független módot biztosít a gazdag 3‑D vizualizációk közvetlen beágyazására Excel munkafüzetekbe, és akár **export chart as image** is használható műszerfalak vagy jelentések számára.

## Gyakran ismételt kérdések

**Q: Hogyan adhatok hozzá több adat sorozatot egy 3D diagramhoz?**  
A: Használja a `chart.getNSeries().add()` metódust minden sorozattartományhoz, és győződjön meg róla, hogy a diagram típusa 3‑D marad (pl. `ChartType.BAR_3_D` vagy `ChartType.PIE_3_D`).

**Q: Exportálhatom a Aspose.Cells for Java‑val létrehozott 3D diagramokat más formátumokba?**  
A: Igen, a diagramot mentheti PNG, JPEG vagy PDF formátumban a megfelelő `chart.toImage()` túlterhelés vagy a `workbook.save()` kép‑ vagy PDF‑formátummal, ezzel kielégítve a **convert chart png** követelményt.

**Q: Lehet interaktív 3D diagramokat készíteni az Aspose.Cells for Java‑val?**  
A: Az Aspose.Cells statikus Excel diagramokra fókuszál. Interaktív web‑alapú 3‑D vizualizációkhoz fontolja meg az Excel adatokat JavaScript könyvtárakkal, például a Three.js‑szel való kombinálását.

**Q: Automatizálhatom a diagramok adatainak frissítését?**  
A: Természetesen. Programozottan töltse be az új adatokat a munkalapra, és frissítse a diagram tartományát; a munkafüzet következő megnyitásakor a diagram a frissített értékeket mutatja.

**Q: Hol találok további forrásokat és dokumentációt az Aspose.Cells for Java‑hoz?**  
A: Átfogó dokumentációt és forrásokat az Aspose.Cells for Java‑hoz a következő weboldalon talál: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Utolsó frissítés:** 2026-08-21  
**Tesztelve a következővel:** Aspose.Cells for Java 24.12 (legújabb)  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [Kördiagramok létrehozása Excelben Aspose.Cells for Java használatával: Átfogó útmutató](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Excel diagram létrehozása megjegyzésekkel](/cells/java/advanced-excel-charts/chart-annotations/)
- [Adatcímkék hozzáadása Excel diagramhoz Aspose.Cells Java-val](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}