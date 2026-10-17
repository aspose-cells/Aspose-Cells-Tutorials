---
date: '2026-10-17'
description: Tanulja meg, hogyan állíthatja be az Excel diagram adatcímkéinek alakját
  Java-ban az Aspose.Cells használatával. Ez az útmutató megmutatja, hogyan módosíthatja
  az Excel diagram címkéit gyorsan és hatékonyan.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Tanulja meg, hogyan állíthatja be az Excel diagram adatcímkéinek alakját
  Java-ban az Aspose.Cells használatával. Ez a lépésről‑lépésre útmutató segít gyorsan
  módosítani az Excel diagram címkéit.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Hogyan állítsuk be az Excel diagram adatcímkéinek alakját Java-ban
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Hogyan állítsuk be az Excel diagram adatcímkéinek alakját Java-ban
url: /hu/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Az Aspose.Cells használatával a diagram testreszabásának elsajátítása Java-ban: adatcímke alakzatok módosítása

## Bevezetés

Az Excel-diagramok vizuális vonzerejének növelése kulcsfontosságú jelentések vagy irányítópultok készítésekor, különösen Java használata esetén. Az Aspose.Cells – egy erőteljes könyvtár táblázatkezeléshez és manipulációhoz – segítségével **hogyan állítsuk be az alakzatot** a diagram adatcímkéin néhány kódsorral. Ez az oktatóanyag végigvezeti a diagram adatcímkéinek alakzatának módosításán az Aspose.Cells for Java használatával. A végére megtanulod, hogyan:

- Hozzáférj és módosítsd a diagram adatcímkéit
- Egyedi alakzatokat állíts be az adatcímkékhez
- Elmentsd a változtatásokat a munkafüzetben

## Gyors válaszok
- **Mi az elsődleges osztály az Excel fájlok kezeléséhez?** `Workbook` egy teljes Excel-fájlt képvisel a memóriában.  
- **Melyik metódus állítja be a címke alakzatát?** `setShapeType(DataLabelShapeType shape)` egy `DataLabel` objektumon.  
- **Szükségem van licencre a fejlesztéshez?** Egy ingyenes ideiglenes licenc elegendő értékeléshez; a teljes licenc a termeléshez kötelező.  
- **Alkalmazhatom az alakzatot több sorozatra?** Igen – iterálj minden sorozaton és hívd meg a `setShapeType` metódust.  
- **Ez a megközelítés kompatibilis nagy munkafüzetekkel?** Az Aspose.Cells több‑száz oldalas munkafüzeteket dolgoz fel anélkül, hogy az egész fájlt a memóriába töltené.

## Mi a **how to set shape**?
A **how to set shape** kifejezés a diagram adatcímkéjének vizuális körvonalának konfigurálását jelenti, például egy egyszerű téglalap átalakítását felhívásra vagy ellipszisre. Az alakzat módosítása javítja az olvashatóságot és kiemeli a kulcsfontosságú adatpontokat. A megfelelő alakzat kiválasztásával a címke kitűnhet, csoportosíthatja a kapcsolódó pontokat, vagy megfelelhet a vállalati arculati irányelveknek, ezáltal növelve a diagram általános érthetőségét.

## Miért használjuk az Aspose.Cells-et a diagramcímke testreszabásához?
Az Aspose.Cells **50+ bemeneti és kimeneti formátumot** támogat – köztük XLSX, CSV, ODS és PDF – és képes **akár 1 millió sor** tartalmazó munkafüzetek manipulálására anélkül, hogy a memória kimerülne. API-ja lehetővé teszi a diagramok programozott módosítását, kiküszöbölve a manuális Excel-szerkesztést és biztosítva a konzisztens stílusokat az automatizált jelentésekben.

## Előfeltételek

- **Aspose.Cells for Java Library**: A 25.3 vagy újabb verzió szükséges.  
- **Java Development Environment**: JDK telepítve a gépeden.  
- **IDE Setup**: Használj olyan IDE-t, mint az IntelliJ IDEA vagy az Eclipse a kód írásához és futtatásához.

### Szükséges könyvtárak és függőségek

Maven felhasználók számára a következő függőséget kell felvenni a `pom.xml`‑be:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gradle felhasználók a következőt adják hozzá a `build.gradle` fájlhoz:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Licenc beszerzése

Az Aspose.Cells ingyenes próbaverzió licencet kínál, amelyet a [Aspose temporary license page](https://purchase.aspose.com/temporary-license/) oldalról szerezhetsz be. Ez korlátozások nélkül biztosítja a teljes funkcionalitást egy korlátozott időtartamra.

## Az Aspose.Cells beállítása Java-hoz

Miután a környezet készen áll, állítsuk be az Aspose.Cells-et. Íme a kezdő lépések:

### Telepítési lépések

1. **Könyvtár letöltése**: Használd a Maven‑t vagy a Gradle‑t, ahogy fent látható.  
2. **Licenc konfigurálása**:  
   - A `License` osztály alkalmazza az Aspose.Cells licencfájlt a teljes funkcionalitás engedélyezéséhez.  
   - Töltsd le és alkalmazd az ideiglenes licencet a következő kódrészlettel a `Workbook` objektum inicializálása után:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Alapvető inicializálás**: Hozz létre egy `Workbook` példányt az Excel‑fájlok kezelésének megkezdéséhez.

## Hogyan állítsuk be az adatcímkék alakzatát egy diagramon?

Töltsd be a munkafüzetet, keresd meg a cél diagramot, és alkalmazd a kívánt alakzatot az adatcímkékre. Az alábbi közvetlen lépések kevesebb, mint egy perc alatt elvégezhetők.

### Lépésről‑lépésre útmutató

#### 1. lépés: töltsd be a munkafüzetet

A `Workbook` osztály az Aspose.Cells felső‑szintű objektuma, amely egyetlen Excel‑fájlt képvisel a memóriában. Használd a `new Workbook("input.xlsx")` szintaxist a módosítandó fájl betöltéséhez.

#### 2. lépés: a diagram elérése

A `Worksheet` egy munkafüzeten belüli egyetlen lapot képvisel.  
`Worksheet ws = workbook.getWorksheets().get(0);` lekéri az első munkalapot.  
A `Chart` egy objektum, amely egy munkalapon beágyazott diagramot jelöl.  
`Chart chart = ws.getCharts().get(0);` megszerzi az első diagramot azon a lapon.

#### 3. lépés: sorozatok lekérése és adatcímkék módosítása

A `Series` egy diagramon megjelenített adatcsaládot jelöl.  
Minden `Series` objektum tartalmaz egy `DataLabel` gyűjteményt.  
A `DataLabel` szabályozza egy sorozat adatcímkéjének megjelenését.  
A `DataLabelShapeType` felsorolja az adatcímkék lehetséges alakzatait.  
Hívd meg a `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` metódust az alakzat beállításához. Az enum tucatnyi lehetőséget kínál, például `RECTANGLE`, `CLOUD` és `WEDGE_ELLIPSE_CALLOUT`.

#### 4. lépés: mentsd el a munkafüzetet

Az alakzat alkalmazása után hívd meg a `workbook.save("output.xlsx");` metódust a változtatások lemezre írásához.

## Hibaelhárítási tippek

- **Fájlútvonal problémák**: Ellenőrizd, hogy az útvonal abszolút vagy a projekt munkakönyvtárához relatív‑e.  
- **Könyvtárverzió eltérés**: Győződj meg róla, hogy az Aspose.Cells 25.3 vagy újabb verzióját használod; a régebbi verziók nem tartalmazzák a `setShapeType` metódust.  
- **Nem támogatott diagramtípusok**: Egyes régi diagramtípusok (pl. radar) nem teszik elérhetővé az adatcímke‑alakzat tulajdonságait; válts támogatott típusra, mint például oszlop vagy vonal.

## Gyakorlati alkalmazások

1. **Pénzügyi jelentés** – Kiemeld a kulcsfontosságú profitmargin‑okat felhívás‑stílusú címkékkel.  
2. **Oktatási anyag** – Használj felhő‑alakú címkéket, hogy felhívd a figyelmet a fontos adatpontokra az oktatási anyagokban.  
3. **Marketing‑analitika** – Alkalmazz egyedi alakzatokat a kampányteljesítmény‑mutatók megkülönböztetéséhez a műszerfalakon.

Az Aspose.Cells integrálása adatcsővezetékekkel vagy CRM‑rendszerekkel lehetővé teszi a teljesen formázott jelentések automatikus generálását, csökkentve a manuális munkát és biztosítva a márka‑konzisztens vizuális megjelenést.

## Teljesítmény szempontok

Nagy Excel‑fájlok kezelésekor:

- **Memóriahasználat optimalizálása**: Hívd meg a `workbook.dispose();` metódust a mentés után a natív erőforrások azonnali felszabadításához.  
- **Kötegelt feldolgozás**: A diagramokat csoportokban dolgozd fel egyenkénti helyett, hogy minimalizáld az objektum‑létrehozási terhelést.  
- **Hatékony adatkezelés**: Kerüld a nehéz számításokat olyan ciklusokban, amelyek több ezer sort iterálnak; számold ki az értékeket előre.

## Összegzés

Most már tudod, **hogyan állítsuk be az alakzatot** az Excel‑diagram adatcímkéin Java‑ban az Aspose.Cells segítségével. Ez a lehetőség nem csak a diagram esztétikáját javítja, hanem a felhasználók adatmegértését is növeli. Fedezz fel további testreszabási lehetőségeket – például címke‑színek, betűtípusok és vezetővonalak – a vizualizációk további finomításához.

Bármilyen kérdés vagy segítség esetén tekintsd meg az [Aspose support forum](https://forum.aspose.com/c/cells/9) oldalt.

## Gyakran ismételt kérdések

**K: Hogyan változtathatom meg egyszerre több adatcímke alakzatát?**  
V: Iterálj végig a diagram minden sorozatán, és hívd meg a `setShapeType` metódust a sorozat `DataLabel` objektumán.

**K: Kezelheti az Aspose.Cells for Java nagy Excel‑fájlokat hatékonyan?**  
V: Igen. Megfelelő memória‑kezeléssel a könyvtár több százezer soros munkafüzeteket dolgoz fel anélkül, hogy az egész fájlt a memóriába töltené.

**K: Milyen gyakori problémák merülnek fel az Aspose.Cells beállításakor?**  
V: Hiányzó Maven‑függőségek, elavult könyvtárverzió vagy érvénytelen licencfájl a tipikus akadályok.

**K: Van mód visszaállítani az adatcímke alakzatát az alapértelmezettre?**  
V: Állítsd be a shape‑típusra a `DataLabelShapeType.DEFAULT` értéket a kiinduló megjelenés visszaállításához.

**K: Hogyan alkalmazhatom ezt a testreszabást több diagramra egy munkafüzetben?**  
V: Iterálj a `ws.getCharts()` gyűjteményen, és alkalmazd ugyanazt a `setShapeType` logikát minden diagram sorozatgyűjteményére.

## Források

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase a License](https://purchase.aspose.com/buy)
- [Free Trial License](https://releases.aspose.com/cells/java/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)

---  

**Last Updated:** 2026-10-17  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Kapcsolódó oktatóanyagok

- [Modify Excel Chart Data Labels Using Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [How to Resize Labels in Excel Charts with Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Add Labels to Excel Charts with Aspose Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}