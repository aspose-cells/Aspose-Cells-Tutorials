---
"date": "2025-04-08"
"description": "Ismerje meg, hogyan használhatja az Aspose.Cells for Java programot szövegdobozok hozzáadásához és sorköz beállításához Excel-munkafüzetekben. Dobja fel munkafüzet-bemutatóit formázott szövegalakzatokkal."
"title": "Szövegdoboz hozzáadása és sorköz beállítása Excelben az Aspose.Cells for Java használatával"
"url": "/hu/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Szövegdoboz hozzáadása és sorköz beállítása Excelben az Aspose.Cells for Java használatával

## Bevezetés

A dinamikus Excel-jelentések létrehozása gyakran egyéni szövegformázást igényel, például meghatározott sorközű szövegdobozok hozzáadását. Az Aspose.Cells for Java segítségével ez egyszerűvé és hatékonnyá válik. Ez az oktatóanyag végigvezeti Önt azon, hogyan javíthatja munkafüzet-bemutatóit az Aspose.Cells for Java segítségével formázott szövegalakzatok hozzáadásához.

Az útmutató végére megtanulod, hogyan:
- Új Excel-munkafüzet létrehozása és a munkalapjainak elérése
- Szövegdoboz alakzat hozzáadása egy munkalaphoz
- Egyéni sorköz beállítása szövegalakzaton belül
- Mentse el formázott munkafüzetét XLSX formátumban

Kezdjük a környezet beállításával.

### Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy a következőkkel rendelkezik:
- Java fejlesztőkészlet (JDK) telepítve a gépeden
- IDE vagy szerkesztő Java kód írásához
- Maven vagy Gradle build rendszer, amely a függőségek kezelésére van konfigurálva

Előnyt jelent a Java programozás alapjainak ismerete és az Excel fájlszerkezetek ismerete.

## Az Aspose.Cells beállítása Java-hoz

Az Aspose.Cells függvényt is vedd be a projekted függőségkezelésébe Maven vagy Gradle használatával:

**Szakértő**

Adja hozzá a következő függőségi blokkot a `pom.xml` fájl:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Vedd bele ezt a `build.gradle` fájl:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Ezután szerezzen be egy Aspose.Cells licencet egy ingyenes próbaverzió kiválasztásával, ideiglenes licenc igénylésével vagy teljes licenc megvásárlásával.

### Az Aspose.Cells inicializálása

Miután a könyvtár bekerült a projektbe, inicializálja azt a Java alkalmazásban:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Workbook egy példányának inicializálása (egy Excel-fájlt jelöl)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Megvalósítási útmutató

### Munkafüzet és Access-munkalap létrehozása

Kezdésként hozzon létre egy új Excel-munkafüzetet, és nyissa meg annak első munkalapját. Ide fogja hozzáadni a szövegdobozt.

#### Áttekintés

Egy új munkafüzet létrehozása egy üres lapot biztosít, amelyhez szükség szerint adatokat, alakzatokat és formázásokat fűzhet hozzá.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Szövegdoboz hozzáadása a munkalaphoz

Ezután adjon hozzá egy szövegdoboz alakzatot a kiválasztott munkalaphoz. Ez az alakzat bármilyen szükséges szöveget tartalmazhat.

#### Áttekintés

A szövegdobozok sokoldalú eszközök egyéni szövegek, például jegyzetek vagy utasítások közvetlen Excel-táblázatba való beillesztésére.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Szövegdoboz alakzat hozzáadása a munkalaphoz
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Szöveg beállítása alakzatban

Miután elkészült a szövegdoboz, állítsd be a tartalmát, és formázd meg a benne lévő szöveget.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Szövegdoboz alakzat hozzáadása a munkalaphoz
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Szöveges tartalom beállítása az alakzaton belül
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Hozzáférés szövegbekezdésekhez az alakzatban

A szövegdobozon belüli egyes bekezdésekhez hozzáférhet, hogy speciális formázást alkalmazzon.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Szövegdoboz alakzat hozzáadása a munkalaphoz
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Szöveges tartalom beállítása az alakzaton belül
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // A második bekezdés elérése az alakzatban
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Bekezdés sorközének beállítása

A sorköz testreszabása javíthatja az olvashatóságot. Így állíthatja be:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Szövegdoboz alakzat hozzáadása a munkalaphoz
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Szöveges tartalom beállítása az alakzaton belül
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // A második bekezdés elérése az alakzatban
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Sorköz beállítása 20 pontra
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // A bekezdés előtti és utáni térköz konfigurálása
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Munkafüzet mentése

Végül mentse el a munkafüzetet az újonnan hozzáadott és formázott szövegmezővel.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Új munkafüzet létrehozása (Excel-fájl)
        Workbook workbook = new Workbook();
        
        // Hozzáférés az első munkalaphoz
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Szövegdoboz alakzat hozzáadása a munkalaphoz
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Szöveges tartalom beállítása az alakzaton belül
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // A második bekezdés elérése az alakzatban
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Sorköz beállítása 20 pontra
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // A bekezdés előtti és utáni térköz konfigurálása
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // A munkafüzet mentése
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Következtetés

Sikeresen megtanultad, hogyan adhatsz hozzá szövegdobozt és állíthatsz be sorközt egy Excel-munkafüzetben az Aspose.Cells for Java használatával. Ezáltal fejlesztheted a dinamikus, vizuálisan vonzó jelentések létrehozásának képességét.

## Kulcsszóajánlások
- "Aspose.Cells Java-hoz"
- "Szövegdoboz hozzáadása Excelben"
- "Sorköz beállítása Excelben"
- "Stílusos szöveggel ellátott Excel-munkafüzet"
- „Java és Aspose.Cells”


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}