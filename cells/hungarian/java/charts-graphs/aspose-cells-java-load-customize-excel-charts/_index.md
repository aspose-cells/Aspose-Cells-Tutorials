---
date: '2026-06-12'
description: Ismerje meg, hogyan exportálhat diagramot PNG formátumba az Aspose.Cells
  Java segítségével, hogyan generálhat diagramképeket, hogyan renderelhet Excel-diagramokat
  PNG-ként, és hogyan testreszabhatja a megjelenítéseket hatékonyan.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: Diagram exportálása PNG formátumba az Aspose.Cells Java használatával
url: /hu/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagram exportálása PNG formátumba az Aspose.Cells Java használatával

## Bevezetés

Diagramot PNG-be exportálni gyakori igény, amikor vizuális adatokat kell beágyazni jelentésekbe, prezentációkba vagy weboldalakra. Az **Aspose.Cells for Java** segítségével betölthet egy meglévő Excel munkafüzetet, frissítheti a diagram adatokat, alkalmazhat globalizációs beállításokat, és a diagramot közvetlenül magas‑minőségű PNG képként renderelheti – mindezt anélkül, hogy a Microsoft Excel telepítve lenne. Ebben az útmutatóban megtudja, hogyan **export chart to PNG**, programozottan generálhat diagramképeket, és testreszabhatja a kimenetet a globális közönség számára.

## Gyors válaszok
- **Hogyan exportálhatok egy diagramot PNG-be?** Töltsd be a munkafüzetet, férj hozzá a diagramhoz, és hívd meg a `chart.toImage()` metódust úgy, hogy a `ImageOrPrintOptions` PNG‑re legyen beállítva.  
- **Melyik könyvtár támogatja a Java diagramkép generálást?** Az Aspose.Cells for Java teljes API‑t biztosít az Excel diagramok képként történő rendereléséhez.  
- **Szükségem van licencre a PNG exportáláshoz?** Az ingyenes próbaverzió működik, de egy kereskedelmi licenc eltávolítja a kiértékelési korlátokat.  
- **Testreszabhatom‑e a számformátumokat globálisan?** Igen, a renderelés előtt használd a `Workbook.getSettings().setGlobalizationSettings()` metódust.  
- **Csak PNG a formátum?** Nem, a képformátum beállításának módosításával JPEG, BMP vagy TIFF formátumba is renderelhet.

## Mi az Aspose.Cells for Java?
`Aspose.Cells for Java` egy **Java‑alapú táblázatkezelő könyvtár**, amely lehetővé teszi a fejlesztők számára, hogy Microsoft Office nélkül hozzanak létre, módosítsanak, konvertáljanak és rendereljenek Excel fájlokat. Több mint 50 fájlformátumot támogat, több ezer soros munkafüzeteket kezel, és tipikus szerverhardveren egy másodpercnél gyorsabban képekké renderelheti a diagramokat.

## Miért exportáljunk diagramot PNG-be az Aspose.Cells segítségével?
A diagramok PNG‑be exportálása az Aspose.Cells segítségével magas teljesítményt, alacsony memóriahasználatot és formátum sokoldalúságot biztosít, miközben megszünteti a Microsoft Excel szükségességét. A könyvtár egy másodpercnél gyorsabban rendereli a diagramokat, szerény heap használatot tart fenn, és támogatja a PNG, JPEG, BMP és TIFF formátumokat, így ideális webes, nyomtatási és többplatformos telepítésekhez.

## Előfeltételek

- **Aspose.Cells for Java** v25.3 (vagy újabb).  
- **JDK 8+** telepítve a fejlesztői gépen.  
- **IDE**, például IntelliJ IDEA vagy Eclipse.  
- **Maven vagy Gradle** a függőségkezeléshez.  

### Szükséges könyvtárak és függőségek

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Környezet beállítása

1. Ellenőrizd, hogy a **JDK 8** vagy újabb szerepel a `PATH` környezeti változóban.  
2. Nyisd meg a kedvenc IDE‑det, és hozz létre egy új Maven/Gradle Java projektet.  
3. Add hozzá az Aspose.Cells függőséget a fenti kódrészletekkel.  

### Licenc beszerzése

Az Aspose.Cells ingyenes próbaverziót kínál funkciói kipróbálásához:

- [Ingyenes próbaverzió letöltése](https://releases.aspose.com/cells/java/)  
- Éles környezetben használathoz vásárolj licencet a [Aspose.Cells vásárlása](https://purchase.aspose.com/buy) oldalon.  
- Ideiglenes licenc kérhető a hosszabb teszteléshez.

## Az Aspose.Cells for Java beállítása

Miután a környezet készen áll, inicializáld az Aspose.Cells‑et a projektedben:

1. Add hozzá a Maven vagy Gradle függőséget, ahogy korábban bemutattuk.  
2. Helyezd el a licencfájlt (`Aspose.Cells.lic`) a projekt resources mappájába.  
3. Töltsd be a licencet futásidőben:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## Megvalósítási útmutató

Áttekintünk három alapvető forgatókönyvet: diagram betöltése és frissítése, globalizációs beállítások testreszabása, valamint a diagram PNG‑be renderelése.

### Hogyan exportáljunk diagramot PNG-be az Aspose.Cells Java segítségével?

Az Aspose.Cells for Java használatával diagram PNG‑be exportálásához először töltsd be a munkafüzetet a `Workbook` osztállyal, majd szerezd meg a kívánt `Chart` objektumot a megfelelő munkalapról. Állítsd be az `ImageOrPrintOptions`‑t PNG képként, és végül hívd meg a `chart.toImage(outputStream, options)` metódust. Az eredményül kapott stream egy magas minőségű PNG‑t tartalmaz, amelyet elmenthetsz vagy közvetlenül elküldhetsz a kliensnek.

### Diagram betöltése és frissítése Excel fájlból

**Overview**: Betöltesz egy meglévő munkafüzetet, biztosítod, hogy a diagram a legfrissebb adatokat tükrözze, és előkészíted a rendereléshez.

#### 1. A munkafüzet betöltése  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*Definition anchor*: A `Workbook` osztály egy teljes Excel fájlt reprezentál a memóriában, hozzáférést biztosít a munkalapokhoz, diagramokhoz és cellákhoz.

#### 2. A munkalap és a diagram elérése  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*Definition anchor*: A `Worksheet` objektum sor/oszlop hozzáférést biztosít, míg a `Chart` objektum a diagram‑specifikus tulajdonságokat tartalmazza.

#### 3. A diagram frissítése  
```java
chart.calculate();
```  
`calculate()` meghívása arra kényszeríti a diagramot, hogy újraszámolja sorozatait a módosult forrásadatok alapján, biztosítva a vizuális pontosságot.

### Diagramok globalizációs beállításainak testreszabása

**Overview**: A dátum, idő és számformátumok beállítása a regionális konvenciókhoz a renderelés előtt.

#### 1. A munkafüzet betöltése  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. Egyéni globalizációs beállítások megadása  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
Megadhatsz helyspecifikus mintákat, például `"dd-MMM-yyyy"` dátumokhoz vagy `"#,##0.00"` számokhoz, biztosítva, hogy az exportált PNG megfeleljen a helyi szabványoknak.

### Diagram renderelése képpé

**Overview**: A frissített diagram PNG fájlba konvertálása, amely prezentációkban, PDF‑ekben vagy weboldalakon használható.

#### 1. A munkafüzet betöltése és a diagram elérése  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. Renderelés képpé  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
A `toImage()` metódus a diagramot egy `java.io.OutputStream`‑be írja. Az `ImageOrPrintOptions.setImageFormat(ImageFormat.png)` beállításával egy tiszta PNG fájlt kapsz.

## Gyakorlati alkalmazások

- **Üzleti jelentések** – PNG diagramok beágyazása PDF vagy Word dokumentumokba a stakeholder‑ek számára.  
- **Adat Dashboardok** – A diagramokat valós időben frissíti, amikor új adatok érkeznek, majd PNG‑be rendereli a gyors webes szállításhoz.  
- **Globális megfelelőség** – Helyspecifikus szám‑ és dátumformátumok alkalmazása a regionális szabályozási követelményeknek való megfeleléshez.

## Teljesítmény szempontok

- **Memory Management**: Nagy fájlok esetén használd a `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` beállítást.  
- **Selective Refresh**: Hívd meg a `chart.calculate()`‑t csak azoknál a diagramoknál, amelyek forrásadatai megváltoztak.  
- **Thread Safety**: Hozz létre egy külön `Workbook` példányt szálanként a versenyhelyzetek elkerülése érdekében.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|----------|----------|
| Licenc nem található | Ellenőrizd az `Aspose.Cells.lic` útvonalát, és győződj meg róla, hogy a classpath‑on van. |
| A PNG kimenet üres | Győződj meg róla, hogy a diagram nincs elrejtve, és a renderelés előtt meghívtad a `calculate()`‑t. |
| Lassú renderelés nagy fájlok esetén | Engedélyezd a `MemorySetting.MEMORY_PREFERENCE` beállítást, és csak a szükséges munkalapot rendereld. |

## Gyakran feltett kérdések

**Q:** Hogyan oldjam meg a licenc aktiválási problémákat?  
A: Helyezd a `Aspose.Cells.lic` fájlt a resources mappába, és töltsd be a `License license = new License(); license.setLicense("Aspose.Cells.lic");` kóddal.

**Q:** Használhatom‑e az Aspose.Cells for Java‑t webalkalmazásban?  
A: Igen, zökkenőmentesen integrálható a Spring Boot, Jakarta EE vagy bármely servlet konténerrel.

**Q:** Mik a gyakori hibák a diagramok frissítésekor?  
A: Ha a `calculate()` meghívása előtt nem frissíted a forrásadatokat, elavult vizuális megjelenéshez vezet.

**Q:** Hogyan kezeljem hatékonyan a nagy Excel fájlokat?  
A: Használd a `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` beállítást, és dolgozz a munkalapokkal stream‑ekben.

**Q:** Milyen képformátumok támogatottak a diagramok rendereléséhez?  
A: A PNG, JPEG, BMP és TIFF teljes mértékben támogatott; a veszteség‑mentes minőségért válaszd a PNG‑t.

## Források

- **Dokumentáció**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **Letöltések**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **Vásárlás és licencelés**: [Aspose.Cells vásárlása](https://purchase.aspose.com/buy)  
- **Ingyenes próbaverzió**: [Aspose.Cells ingyenes próbaverzió letöltése](https://releases.aspose.com/cells/java/)  
- **Ideiglenes licenc**: [Ideiglenes licenc kérése](https://purchase.aspose.com/temporary-license/)  
- **Támogatás és fórumok**: [Aspose támogatási fórum](https://forum.aspose.com/c/cells/9)

Ezeknek a lépéseknek az elsajátításával megbízhatóan **export chart to PNG** tudsz végrehajtani, és magas minőségű vizualizációkat integrálhatsz bármely Java‑alapú megoldásba.

---

**Utoljára frissítve:** 2026-06-12  
**Tesztelve ezzel:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Kapcsolódó oktatóanyagok

- [Hogyan exportáljunk Excel diagramokat SVG formátumba az Aspose.Cells Java használatával a méretezhető vektorgrafikához](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Excel diagramok exportálása PDF‑be az Aspose.Cells for Java használatával: Egyedi oldalméretek útmutatója](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Hogyan testreszabjuk az Excel diagramokat témaszínekkel az Aspose.Cells Java használatával](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```