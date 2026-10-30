---
category: general
date: 2026-08-20
description: Hozzon létre munkalapok intelligens jelölőket Java-ban az Aspose.Cells
  használatával, és szabályozza a részletes lapok elnevezését a SmartMarkerOptions
  segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: hu
lastmod: 2026-08-20
og_description: Hozzon létre okos jelölőket munkalapokhoz Java-ban az Aspose.Cells
  segítségével. Ismerje meg, hogyan nevezheti el dinamikusan a részletes munkalapokat
  a SmartMarkerOptions használatával.
og_image_alt: create worksheets smart markers example diagram
og_title: Munkalapok létrehozása intelligens jelölőkkel – Java útmutató az Aspose.Cells
  használatához
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Hogyan hozhatunk létre munkalapok intelligens jelölőit az Aspose.Cells használatával
url: /hu/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre munkalapok okos jelölőket az Aspose.Cells segítségével

Ha Java munkafüzetben **okos jelölőket szeretne létrehozni a munkalapokon**, ez az útmutató pontos lépéseket mutat be, hogyan teheti ezt meg az Aspose.Cells segítségével. Megmutatjuk, hogyan konfigurálja a `SmartMarkerOptions`-t, hogy minden részletlap egyedi, előre meghatározott nevet kapjon.

Excel jelentések generálása, amelyek egy mester‑részlet sablont bővítenek, gyakori igény a pénzügyi, készletkezelő és jelentési rendszerekben. Az okos jelölők használata megszünteti a manuális lapmásolást, és lehetővé teszi, hogy az adatokra koncentráljon ahelyett, hogy a háttérfolyamatokkal foglalkozna.

## Amit megtanul

* Hogyan töltsön be egy mester munkafüzetet, amely okos jelölőket tartalmaz.  
* Hogyan állítsa be a `SmartMarkerOptions`-t a generált részletlapok elnevezésének szabályozásához.  
* Hogyan adjon meg egy `DataTable`-t mintaként, és alkalmazza azt az okos jelölőkre.  
* Hogyan mentse az eredményt úgy, hogy minden részletmunkalap egyedi nevet kapjon, elkerülve a duplikált lapneveket.

**Előfeltételek**  
* Java 17 vagy újabb (a kód JDK 8+‑vel is fordítható).  
* Aspose.Cells for Java 23.9 vagy újabb – a könyvtár biztosítja a `Workbook`, `SmartMarkerOptions` és a kapcsolódó osztályokat.  
* Egy IDE, például IntelliJ IDEA, Eclipse vagy VS Code.

A továbbiakban felbukkanó fogalmak közé tartozik a **Aspose.Cells Java**, a **smart marker options**, és a **duplicate sheet names** kezelése, amikor a sablon bővül.

## Munkalapok okos jelölőinek létrehozása – lépésről‑lépésre útmutató

Az alábbi szakaszok a folyamatot különálló, újrahasználható lépésekre bontják. Minden lépés tartalmaz egy kódrészletet, magyarázatot arra, hogy miért fontos, valamint gyakorlati tippeket a gyakori hibák elkerüléséhez.

### 1. lépés: Maven projekt beállítása és az Aspose.Cells hozzáadása

Create a new Maven module (or Gradle project) and add the Aspose.Cells dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Miért fontos ez a lépés** – A könyvtár biztosítja a `Workbook` osztályt, amely Excel fájlokat olvas és ír, valamint az okos‑jelölő motorját, amely automatikusan kibővíti a sablont. A megfelelő függőség hiányában a fordító nem tudja feloldani a később használt API hívásokat.

> **Pro tipp:** Ha vállalati proxy mögött dolgozik, konfigurálja a Maven `settings.xml`‑t, hogy biztonságosan töltse le az Aspose tárolót.

### 2. lépés: Load the master workbook that contains smart markers

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Miért fontos ez a lépés** – A mester munkafüzet meghatározza a elrendezést, képleteket és a helyőrző címkéket (`«SmartMarker»`), amelyeket a motor helyettesít. A fájl egyszeri betöltése alacsony memóriahasználatot biztosít, és lehetővé teszi ugyanazon munkafüzet újrahasználatát több adatcsoporthoz.

### 3. lépés: Configure SmartMarkerOptions for custom detail sheet names

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Miért fontos ez a lépés** – Alapértelmezés szerint az Aspose.Cells általános nevekkel hoz létre részletlapokat, például „DetailSheet”. Ha a sablon sok sorra bővül, ezek a nevek ütköznek, ami **duplicate sheet names** hibához és futásidejű kivételhez vezet. A `"DetailSheet_{0}"` minta garantálja, hogy minden sor egyedi nevet kap, megoldva a duplikációt.

### 4. lépés: Build a DataTable that matches the smart marker fields

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Miért fontos ez a lépés** – A `DataTable` biztosítja a tényleges értékeket, amelyek helyettesítik az okos jelölő helyőrzőket. Az oszlopneveknek meg kell egyezniük a sablonban lévő jelölő nevekkel; ellenkező esetben a motor csendben kihagyja a helyettesítést.

> **Gyakori hiba:** Olyan oszlopnév használata, amely eltér a kis‑ és nagybetűkben (pl. „id” vs „Id”), hiányzó adatot eredményez a generált lapokon.

### 5. lépés: Apply the data to the smart markers with the naming options

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Miért fontos ez a lépés** – Az `apply` metódus elindítja az okos‑jelölő motort. Beolvassa minden sort, a `SmartMarkerOptions`‑ből származó névmintával új részletlapot hoz létre, és feltölti a sort tartalmazó adatokkal. Ez az egyetlen hívás helyettesíti a tucatnyi sor manuális lapklónozást és cella kitöltést.

### 6. lépés: Save the workbook and verify the result

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Végrehajtás után nyissa meg a `MasterDetailDuplicatedNames.xlsx` fájlt. A következőket kell látnia:

* Az eredeti mesterlap változatlan.  
* Két új munkalap, `DetailSheet_1` és `DetailSheet_2` néven.  
* Minden részletlap a `DataTable` megfelelő sorának értékeit tartalmazza.

**Miért fontos ez a lépés** – A munkafüzet mentése befejezi az okos‑jelölő kibővítést. A fájl most már elküldhető downstream rendszereknek, e‑mailhez csatolható, vagy Excelben megnyitható további elemzés céljából.

## Szélsőséges esetek és változatok kezelése

### Több mesterlap

Ha a sablon több mint egy mesterlapot tartalmaz, iteráljon minden lap okos jelölőin:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Egyedi elnevezés a sorindexen túl

Bármely adatoszlopot beágyazhat a lap nevébe helyőrzők használatával, például `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Győződjön meg arról, hogy a `OrderId` oszlop létezik a megadott `DataTable`‑ben.

### Túl hosszú lapnevek megakadályozása

Az Excel a lapneveket 31 karakterre korlátozza. Ha az elnevezési mintája meghaladhatja ezt a határt, csonkolja vagy hash-elje az értéket:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Ezután a generált nevet a `StringUtils.abbreviate`‑el dolgozza fel, mielőtt átadná az Aspose‑nak.

## Teljesen futtatható példa

Az alábbiakban a teljes forrásfájl található, amelyet másolhat, módosíthatja az elérési útvonalakat, és közvetlenül futtathat:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Várt kimenet**

* `MasterDetailDuplicatedNames.xlsx` tartalmazza:

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Mastering Aspose.Cells Java: Utilize Smart Markers for Dynamic Data in Worksheets](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Create Dynamic Charts with Smart Markers in Aspose.Cells for Java | Step-by-Step Guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}