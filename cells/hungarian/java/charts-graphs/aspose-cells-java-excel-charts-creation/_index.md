---
date: '2026-04-08'
description: Ismerje meg, hogyan hozhat létre jelölőkkel ellátott vonaldiagramot az
  Aspose.Cells for Java segítségével, hogyan adja hozzá a diagramot a munkalaphoz,
  és hogyan testreszabhatja az Excel-diagramokat az automatizált jelentéskészítéshez.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Vonaldiagram létrehozása jelölőkkel az Aspose.Cells for Java használatával
url: /hu/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel diagramok létrehozása és formázása Aspose.Cells Java-val

## Bevezetés

A mai adat‑központú világban egy **line chart with markers** az egyik leghatékonyabb módja a trendek és kiugró értékek vizualizálásának. Akár automatizált jelentéseket, akár naponta frissülő irányítópultot építesz, egy vonaldiagram jelölőkkel programozott hozzáadása a munkalaphoz számtalan manuális lépést takarít meg. Ez az útmutató végigvezet az Aspose.Cells for Java használatán, hogy diagramokat hozz létre, formázz és exportálj, így az elemzésekre koncentrálhatsz a fáradságos Excel‑kezelés helyett.

**Mit fogsz megtanulni**
- Munkafüzet inicializálása és adatfeltöltés Aspose.Cells használatával.  
- **Hogyan adjunk hozzá egy line chart with markers diagramot egy munkalaphoz** és konfiguráljuk a megjelenését.  
- Sorozatok színeinek, jelölőinek és egyéb formázási beállításainak testreszabása.  
- Munkafüzet mentése Excel‑fájlként, amely tartalmazza a formázott diagramot.

## Gyors válaszok
- **Mi a fő osztály a kezdéshez?** `Workbook` egy új Excel‑fájlt inicializál.  
- **Melyik diagramtípus hoz létre egy line chart with markers diagramot?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Hogyan állíthatok be egyedi színeket a sorozat pontjaihoz?** Használd a `chart.getNSeries().setColorVaried(true)`‑t, és állítsd be a marker area színeket.  
- **Szükségem van licencre a teljes funkcionalitáshoz?** Igen, egy fizetett vagy ideiglenes Aspose.Cells licenc eltávolítja a kiértékelési korlátokat.  
- **Exportálhatom az eredményt XLSX‑ként?** Természetesen—`workbook.save("StyledChart.xlsx")` létrehoz egy XLSX fájlt.

## Előkövetelmények

Az Aspose.Cells for Java használatával történő diagramok létrehozása és formázása előtt győződj meg arról, hogy a következő beállítások megvannak:

### Szükséges könyvtárak
Add hozzá az Aspose.Cells-et függőségként a projektedhez. Íme az útmutató Maven és Gradle felhasználók számára:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Környezeti beállítási követelmények
- Java Development Kit (JDK) telepítve a rendszereden.  
- Integrált fejlesztőkörnyezet (IDE), például IntelliJ IDEA vagy Eclipse a kódoláshoz és teszteléshez.

### Tudás előkövetelmények
Egy alapvető Java programozási ismeret szükséges, valamint a Excel munkafüzetek és diagramkészítési koncepciók ismerete.

### Licenc beszerzése
Aspose.Cells egy kereskedelmi termék, amelyhez a teljes funkcionalitáshoz licenc szükséges. Ingyenes próbaverziót szerezhetsz a funkciók kiértékeléséhez, kérhetsz ideiglenes licencet a kiterjesztett teszteléshez, vagy megvásárolhatod a terméket hosszú távú használatra.

- **Ingyenes próba:** [Ingyenes próba letöltése](https://releases.aspose.com/cells/java/)  
- **Ideiglenes licenc:** [Ideiglenes licenc kérése](https://purchase.aspose.com/temporary-license/)  
- **Vásárlás:** [Aspose.Cells megvásárlása](https://purchase.aspose.com/buy)

## Aspose.Cells beállítása Java-hoz

Miután telepítetted a szükséges függőségeket, állítsd be a fejlesztői környezetet az Aspose.Cells használatához. Kezdjük a könyvtár importálásával és egy `Workbook` objektum inicializálásával a Java‑alkalmazásodban:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Implementációs útmutató

Ezen a részen a megvalósítást különálló funkciókra bontjuk: Munkafüzet inicializálása és adatfeltöltés, Diagram létrehozása és konfigurálása, Sorozat testreszabása, valamint Munkafüzet mentése.

### Funkció 1: Munkafüzet inicializálása és adatfeltöltés

**Áttekintés:** Ez a funkció egy új munkafüzet létrehozására, az első munkalap elérésére és a diagramkészítéshez szükséges adatok feltöltésére összpontosít.

#### 1. lépés: A Workbook inicializálása
Indíts egy `Workbook` objektum példányosításával:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 2. lépés: Oszlopcímek beállítása és adatok feltöltése
Határozd meg az oszlopfejléceket, és töltsd fel a sorokat mintaadatokkal:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funkció 2: Diagram létrehozása és konfigurálása

**Áttekintés:** Ez a funkció bemutatja, hogyan adjunk diagramot a munkafüzet munkalapjához, állítsuk be a stílusát, és konfiguráljuk az alapvető tulajdonságokat.

#### 3. lépés: Diagram hozzáadása a munkalaphoz
Adj hozzá egy line chart with markers diagramot:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funkció 3: Sorozat konfiguráció és testreszabás

**Áttekintés:** Növeld a diagramok vizuális vonzerejét a sorozati beállítások testreszabásával, például változatos színekkel és jelölő stílusokkal.

#### 4. lépés: Sorozati beállítások testreszabása
Konfiguráld a sorozati adatokat, alkalmazz egyedi formázást, és állítsd be a jelölőket:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funkció 4: Munkafüzet mentése

**Áttekintés:** Végül mentsd a munkafüzetet, hogy a változtatások megmaradjanak, és a diagram benne legyen az Excel‑fájlban.

#### 5. lépés: A munkafüzet mentése
Mentsd a munkafüzetet az újonnan létrehozott diagramokkal:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Gyakori problémák és hibaelhárítás
- **A diagram üresnek jelenik meg:** Ellenőrizd, hogy a `setXValues` és `setValues`‑ben használt cellatartományok helyesen hivatkoznak a feltöltött cellákra.  
- **A színek nem alkalmazódnak:** Győződj meg róla, hogy a `chart.getNSeries().setColorVaried(true)` hívás megtörténik az egyes sorozatok testreszabása előtt.  
- **Licenc hibák:** A próbaverzió licenc korlátozhatja a diagramok számát; telepíts teljes licencet a korlátozások eltávolításához.

## Gyakran Ismételt Kérdések

**K: Létrehozhatok más diagramtípusokat (pl. oszlop, kör) az Aspose.Cells‑szel?**  
V: Igen, az Aspose.Cells számos diagramtípust támogat; egyszerűen cseréld le a `ChartType.LINE_WITH_DATA_MARKERS`‑t a kívánt enum értékre.

**K: Szükséges bezárni a munkafüzetet vagy felszabadítani az erőforrásokat?**  
V: A `Workbook` osztály automatikusan kezeli az erőforrásokat, de hosszú futású alkalmazásokban meghívhatod a `workbook.dispose()`‑t a memória felszabadításához.

**K: Lehet több diagramot is hozzáadni ugyanahhoz a munkalaphoz?**  
V: Természetesen—hívd meg a `worksheet.getCharts().add(...)`‑t minden egyes diagramhoz, amelyet be szeretnél szúrni.

**K: Hogyan exportáljam a fájlt régebbi Excel formátumba (XLS)?**  
V: Használd a `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);` parancsot.

**K: A diagram megtartja a formázását, amikor Microsoft Excel‑ben nyitják meg?**  
V: Igen, az Aspose.Cells natív Excel diagramobjektumokat ír, így minden stílus, szín és jelölő pontosan úgy jelenik meg, ahogy definiáltad.

---

**Utoljára frissítve:** 2026-04-08  
**Tesztelve ezzel:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}