---
category: general
date: 2026-08-20
description: Tanulja meg, hogyan exportálhat diagramot docx‑be, és hogyan konvertálhat
  Excel munkafüzetet docx‑be az Aspose.Cells Java‑val. Lépésről‑lépésre útmutató teljes
  kóddal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: hu
lastmod: 2026-08-20
og_description: Exportálja a diagramot docx formátumba, és konvertálja az Excel munkafüzetet
  docx-re az Aspose.Cells for Java segítségével. Kövesse ezt a teljes, futtatható
  útmutatót.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Diagram exportálása docx-be az Aspose.Cells segítségével – Java útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Hogyan exportáljunk diagramot docx-be Excelből az Aspose.Cells for Java használatával
url: /hu/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagram exportálása DOCX-be Excel munkafüzetből Java használatával

Ha közvetlenül egy Excel fájlból **export chart to docx**-t szeretne, ez az útmutató egy kész‑a‑futtatásra megoldást mutat be. A útmutató végére megtudja, hogyan **convert Excel workbook to docx**-t hajthat végre úgy, hogy a szerkeszthető diagramot megőrzi, így a létrehozott Word dokumentum módosítható a pontosság elvesztése nélkül.

Diagramok exportálása gyakori, amikor jelentéseket generál, amelyek a táblázatkezelő számításokat gazdag Word elrendezésekkel kombinálják. Az Aspose.Cells for Java egyszerűvé teszi a konverziót, és az API lehetővé teszi, hogy a diagram szerkeszthető maradjon – nincs szükség statikus képre.

## Mit fed le ez az útmutató

* Létező, diagramot tartalmazó munkafüzet betöltése.  
* `ImageOrPrintOptions` konfigurálása a DOCX formátum célzásához.  
* `ExportEditableCharts` jelző engedélyezése (elérhető a 25.10-es verziótól).  
* A munkafüzet mentése DOCX fájlként, amely megőrzi a szerkeszthető diagramot.  

Külső eszközök nem szükségesek az Aspose.Cells JAR-on kívül. A kód Java 8+ és bármely friss Aspose.Cells verzióval működik.

## Előkövetelmények

| Követelmény | Miért fontos |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | `setExportEditableCharts` funkció ebben a kiadásban került bevezetésre. |
| **Java Development Kit (JDK) 8 or newer** | Biztosítja a futtatókörnyezetet a példa lefordításához és futtatásához. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | A diagram az az objektum, amelyet a DOCX-be exportálunk. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Megkönnyíti a függőségek kezelését és a futtatást. |

A legújabb Aspose.Cells JAR letölthető az [Aspose weboldaláról](https://products.aspose.com/cells/java/).

## 1. lépés: A projekt beállítása és az Aspose.Cells függőség hozzáadása

Ha Maven-t használ, adja hozzá a következő függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Gradle-hez adja hozzá:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** Használja azt a pontos verziót, amely bevezette a `ExportEditableCharts`-t (25.10) vagy bármely újabb kiadást. A régebbi verziók figyelmen kívül hagyják a jelzőt, és statikus képet hoznak létre helyette.

## 2. lépés: A diagramot tartalmazó munkafüzet betöltése

A `Workbook` osztály képviseli az egész Excel fájlt. Betöltése egy soros művelet:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Miért fontos:** A munkafüzetnek teljesen be kell töltenie, mielőtt bármilyen exportálási beállítást alkalmazna. Ha a fájl útvonala helytelen, az Aspose.Cells `FileNotFoundException`-t dob.

## 3. lépés: Kép/nyomtatási beállítások konfigurálása DOCX kimenethez

`ImageOrPrintOptions` szabályozza, hogyan kerül renderelésre a munkafüzet. A mentési formátum `DOCX`-re állítása azt mondja az Aspose.Cells-nek, hogy Word dokumentumot készítsen kép helyett.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Itt módosíthatja az oldal méretét, DPI-t vagy a képminőséget, de ezek opcionálisak a diagram exportálásához.

## 4. lépés: Szerkeszthető diagramok exportálásának engedélyezése

A 25.10-es verziótól kezdve az Aspose.Cells beágyazhat diagramokat natív Word diagramobjektumként. Ez teljesen szerkeszthetővé teszi őket a Microsoft Wordben.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Külön eset:** Ha ezt a jelzőt `false`-ra állítja (vagy kihagyja), a diagram statikus képként lesz renderelve. `true`-t csak akkor használja, ha a célközönségnek a konverzió után szerkesztenie kell a diagramot.

## 5. lépés: A munkafüzet mentése DOCX fájlként

Végül hívja meg a `Workbook.save`-t a konfigurált beállításokkal:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Amikor a program befejeződik, nyissa meg a `ChartEditable.docx`-et a Microsoft Wordben. Látnia kell az eredeti diagramot, és ha jobb‑kattint rá, a **Edit Data** opció elérhető lesz – ez megerősíti, hogy a diagram valóban szerkeszthető.

## Teljes, futtatható példa

Az alábbiakban a teljes forrásfájl található. Másolja be az IDE-jébe, cserélje le a `YOUR_DIRECTORY`-t egy abszolút vagy relatív útvonalra, és futtassa.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Várható kimenet**

* A megadott könyvtárban egy `ChartEditable.docx` nevű fájl.  
* A fájl Wordben való megnyitása megmutatja a diagramot pontosan úgy, ahogy az Excelben megjelent, és duplakattintással szerkesztheti az adat sorozatot.

## Gyakori buktatók és hogyan kerülhetők el

| Tünet | Ok | Megoldás |
|---------|-------|-----|
| A Word **statikus képet** mutat a szerkeszthető diagram helyett | `setExportEditableCharts` nincs meghívva vagy a 25.10-nél alacsonyabb verzió használata | Győződjön meg róla, hogy a jelző `true` értékre van állítva, és az Aspose.Cells 25.10 vagy újabb verziót használ. |
| A generált DOCX **üres** | Helytelen fájlútvonal a forrás munkafüzethez vagy nem elegő jogosultság | Ellenőrizze a munkafüzet útvonalát, és hogy az alkalmazásnak van-e olvasási/írási hozzáférése. |
| A diagram elrendezése **torzult** | Az Excel oldalméretezése (pl. rejtett sorok/oszlopok) eltér a Word alapértelmezett beállításaitól | `ImageOrPrintOptions` módosítása (pl. `setOnePagePerSheet(true)`) a méretezés szabályozásához. |
| **Teljesítmény** romlik nagy munkafüzeteknél | Sok diagram vagy nagy adat halmaz exportálása | Csak a szükséges munkalapok exportálása vagy a `setSheetIndex` használata a feldolgozás korlátozásához. |

## A megoldás kibővítése

* **Több diagram:** Iteráljon az összes munkalapon, és hívja meg a `worksheet.getCharts()`-t, hogy minden diagramot egyenként exportáljon.  
* **Egyedi DOCX stílus:** Mentés után használja az Aspose.Words-ot fejlécek, láblécek vagy stílusok alkalmazásához a generált dokumentumban.  
* **Kötegelt konverzió:** A kódot egy ciklusba ágyazza, amely egy `.xlsx` fájlokból álló könyvtárat dolgoz fel, minden fájlhoz DOCX-et készít.  

## Következtetés

Most már rendelkezik egy megbízható módszerrel a **export chart to docx** és a **convert Excel workbook to docx** végrehajtására, miközben a diagram teljes szerkeszthetőségét megőrzi. A kulcsfontosságú lépések a munkafüzet betöltése, a `ImageOrPrintOptions` DOCX-re konfigurálása, az `ExportEditableCharts` engedélyezése és az eredmény mentése.

Kísérletezzen további beállításokkal – például oldal margók beállításával vagy a munkafüzet képleteinek beágyazásával – hogy a kimenetet a jelentéskészítési folyamatához igazítsa. Amikor programozottan kell Word jelentéseket generálni Excel adatokból, ez a megközelítés tiszta, karbantartható megoldást nyújt.

--- 

*Készen áll a kipróbálásra? Klónozza a példát, frissítse a fájl útvonalakat, és futtassa a programot. Ha bármilyen problémába ütközik, tekintse meg az Aspose.Cells for Java dokumentációt, vagy fedezze fel az alábbi kapcsolódó témákat.*

### Kapcsolódó témák, amelyeket érdemes felfedezni

* **convert excel workbook to pdf** – PDF jelentések generálása ugyanabból a munkafüzetből.  
* **Aspose.Cells chart formatting** – színek, jelölők és tengelyek testreszabása exportálás előtt.  
* **Embedding images in DOCX with Aspose.Words** – diagramok kombinálása más Word tartalommal.  

Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}