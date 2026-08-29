---
date: '2026-04-11'
description: Tanulja meg, hogyan jelenítheti meg az Aspose Cells verzióját, hogyan
  tölthet be Excel munkafüzetet Java‑ban, és hogyan kezelheti a diagram‑enumokat az
  Aspose.Cells‑szel. Kövesse a lépésről‑lépésre példákat.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: 'Megjelenítés: Aspose Cells verzió és diagram enum kezelés Java-ban'
url: /hu/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells verzió megjelenítése és diagram enum kezelése Java-ban

## Bevezetés

Ha szükséged van **Aspose Cells verzió megjelenítésére**, Excel munkafüzet betöltésére Java-ban, és diagram enumokkal való munkára, jó helyen jársz. Ebben az útmutatóban lépésről‑lépésre végigvezetünk a szükséges teendőkön, hogy integráld az Aspose.Cells for Java‑t a projektjeidbe, kinyerd a diagram adatait, és egész szám alapú enumokat olvasható szöveggé alakítsd. A végére egy stabil, termelés‑kész megoldást kapsz, amelyet közvetlenül beilleszthetsz a kódodba.

**Mit fogsz megtanulni**
- Hogyan jelenítsd meg az Aspose.Cells verzióját.
- Hogyan **tölts be Excel munkafüzetet Java‑ban** és érj el diagram adatokat.
- Hogyan konvertáld az egész számú enum értékeket a megfelelő sztringekre.
- Hogyan olvasd ki egy diagram pont X és Y értéktípusait.

Kezdjünk is!

## Gyors válaszok
- **Hogyan ellenőrizhetem az Aspose.Cells verzióját?** Hívd meg a `CellsHelper.getVersion()` metódust, és írd ki az eredményt.  
- **Melyik Maven koordináta adja hozzá az Aspose.Cells‑t?** `com.aspose:aspose-cells:25.3`.  
- **Betölthetek Excel munkafüzetet Java‑ban?** Igen — használd a `new Workbook(filePath)` kifejezést.  
- **Hogyan konvertálódnak az enum értékek?** Tárolj egy `HashMap<Integer, String>`‑et, és keresd meg az egész szám kulcsot.  
- **Melyik metódus írja ki az X/Y értéktípusokat?** `pnt.getXValueType()` és `pnt.getYValueType()`.

## Mi az a „display Aspose Cells version”?
A kifejezés a könyvtár futási időben elérhető verziószövegének lekérdezését jelenti. A pontos verzió ismerete segít a hibakeresésben, a kompatibilitás biztosításában és abban, hogy a licenc a megfelelő kiadásra vonatkozik.

## Miért fontos a verzió megjelenítése és az Excel munkafüzet betöltése Java‑ban?
- **Hibakeresés** – Megerősíti, hogy a helyes könyvtár van a classpath‑on.  
- **Megfelelőség** – Egyszerűen ellenőrizhető, hogy licencelt verziót használsz.  
- **Automatizálás** – Lehetővé teszi, hogy a szkriptek a könyvtár különböző kiadásaihoz alkalmazkodjanak manuális beavatkozás nélkül.  

## Előkövetelmények

### Szükséges könyvtárak és függőségek
- **Aspose.Cells for Java** – a fő könyvtár Excel kezeléshez.  
- **Java Development Kit (JDK)** – 8‑as vagy újabb verzió.

### Környezet beállítása
- A kedvenc IDE‑d (IntelliJ IDEA, Eclipse, NetBeans).  
- Build eszköz: Maven **vagy** Gradle (az alábbiakban leírtak).

### Szükséges ismeretek
- Alap Java programozás.  
- Az Excel alapfogalmainak (munkalapok, diagramok) ismerete előny, de nem kötelező.

## Aspose.Cells for Java beállítása

### Maven használata
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle használata
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Licenc beszerzési lépések
- **Ingyenes próba**: Töltsd le a [Aspose kiadási oldaláról](https://releases.aspose.com/cells/java/).  
- **Ideiglenes licenc**: Szerezz rövid távú licencet a [Aspose ideiglenes licenc oldalán](https://purchase.aspose.com/temporary-license/).  
- **Megvásárlás**: Hosszú távú projektekhez vásárolj licencet a [Aspose vásárlási oldalon](https://purchase.aspose.com/buy).

### Alap inicializálás és beállítás
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## Implementációs útmutató

### Hogyan jelenítsd meg az Aspose Cells verzióját
**Áttekintés** – Gyorsan ellenőrizd a könyvtár verzióját futás közben.

#### 1. lépés: Szükséges csomagok importálása
```java
import com.aspose.cells.*;
```

#### 2. lépés: Osztály és `main` metódus létrehozása
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### Magyarázat
- A `CellsHelper.getVersion()` visszaadja az Aspose.Cells DLL pontos verziószövegét, amelyet az alkalmazásod használ.

### Hogyan konvertáld az egész számú enumokat sztring enumokra
**Áttekintés** – Alakítsd át a numerikus enum értékeket (pl. `CellValueType.IS_NUMERIC`) olvasható szöveggé.

#### 1. lépés: HashMap beállítása a konverzióhoz
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 2. lépés: Enum érték konvertálása és kiírása
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### Magyarázat
- A `cvTypes` térkép összekapcsolja a numerikus konstansokat egy ember által olvasható címkével.

### Hogyan tölts be Excel munkafüzetet Java‑ban és érj el diagram adatokat
**Áttekintés** – Nyiss meg egy meglévő munkafüzetet, keresd meg a diagramot, és biztosítsd, hogy az adatok naprakészek legyenek.

#### 1. lépés: Szükséges csomagok importálása
```java
import com.aspose.cells.*;
```

#### 2. lépés: Munkafüzet betöltése és munkalap elérése
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### Magyarázat
- A `new Workbook(filePath)` betölti a fájlt a memóriába.  
- A `ch.calculate()` kényszeríti a diagramot, hogy újraszámolja a képleteket, így a kiolvasott adatok aktuálisak lesznek.

### Hogyan olvasd ki és írd ki egy diagram pont X és Y értéktípusait
**Áttekintés** – Szerezd meg egy adott pont X és Y értékeinek adattípusát.

#### 1. lépés: Enum konverziós HashMap beállítása (újrahasználva az előzőből)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 2. lépés: Diagram pont elérése és értéktípusok kiírása
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### Magyarázat
- A `pnt.getXValueType()` / `pnt.getYValueType()` egész számú konstansokat ad vissza, amelyek jelzik, hogy az érték numerikus, sztring, dátum stb.  
- A `cvTypes` térkép ezeket az egész számokat olvasható szöveggé alakítja.

## Gyakorlati alkalmazások
1. **Pénzügyi jelentéskészítés** – Automatikusan generálj diagramokat ellenőrzött adattípusokkal audit‑célra.  
2. **Adatvizualizációs irányítópultok** – Húzd be a diagram pontokat egyedi UI komponensekbe.  
3. **Automatizált tesztelés** – Ellenőrizd, hogy a diagram sorozatok a várt adattípusokat tartalmazzák.  
4. **Üzleti intelligencia** – A diagram metaadatokat továbbítsd downstream elemzési csővezetékekbe.  
5. **Egyedi jelentéskészítő eszközök** – Építs testreszabott jelentésmotorokat, amelyek pontos enum kezelést igényelnek.

## Teljesítménybeli megfontolások
- **Csak a szükséges lapok betöltése** – Használd a `Workbook.getWorksheets().get(index)`‑et a minden lap betöltése helyett nagy fájlok esetén.  
- **Objektumok gyors felszabadítása** – A feldolgozás után állítsd a munkafüzet referenciáit `null`‑ra a szemétgyűjtés segítéséhez.  
- **Kötegelt fájlfeldolgozás** – Sok munkafüzet esetén dolgozz kötegekben, hogy a memóriahasználat kiszámítható maradjon.

## Gyakori problémák és megoldások
- **Licenc nem található** – Győződj meg róla, hogy a licencfájl útvonala helyes, és a fájl szerepel a build kimenetében.  
- **Diagram nem számolt** – Mindig hívd meg a `chart.calculate()`‑t a pontértékek olvasása előtt.  
- **Helytelen enum leképezés** – Ellenőrizd, hogy minden releváns `CellValueType` konstans fel van-e véve a `HashMap`‑be.  

## Gyakran feltett kérdések

**K: Használhatom ezt a kódot Aspose.Cells 24.x‑el?**  
V: Igen, a verzió lekérdezés, munkafüzet betöltés és diagram pont elérés API‑ja stabil maradt a legújabb kiadásokban.

**K: Mi van, ha a diagram dátumértékeket tartalmaz?**  
V: Add hozzá a `CellValueType.IS_DATE_TIME`‑t a `cvTypes` térképhez, és térképezd le a `"IsDateTime"` szövegre.

**K: Szükségem van licencre a próba használatához?**  
V: Teljes funkcionalitáshoz próba‑licenc szükséges; licenc nélkül a generált fájlokon vízjelek jelennek meg.

**K: Hogyan kezelem a több munkalapot?**  
V: Iterálj a `wb.getWorksheets()`‑en, és dolgozd fel minden megtalált `Chart` objektumot.

**K: Van mód a diagram adat exportálására CSV‑be?**  
V: Igen — a sorozat értékeket a `chart.getNSeries().get(i).getValues()`‑el nyerheted ki, majd a szokásos Java I/O‑val írhatsz CSV‑t.

---

**Utoljára frissítve:** 2026-04-11  
**Tesztelve:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}