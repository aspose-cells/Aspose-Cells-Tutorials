---
category: general
date: 2026-11-25
description: Excel munkafüzet létrehozása Java kódrészlet példával az Aspose.Cells
  okos jelölők segítségével, amely JSON tömböket egyetlen értékként köt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: hu
lastmod: 2026-11-25
og_description: Készítsen Excel munkafüzetet Java-val az Aspose.Cells segítségével,
  hogy könnyedén exportálja a JSON tömböket egyedi cellákba. Kövesse a lépésről‑lépésre
  útmutatót.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Excel munkafüzet létrehozása Java – Aspose.Cells okos marker útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan hozzunk létre Excel munkafüzetet Java-val az Aspose.Cells jelölőkkel
url: /hu/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Excel munkafüzetet Java-val Aspose.Cells jelölőkkel

Ha **create Excel workbook Java** kódra van szükséged, amely egy JSON tömböt egyetlen cellába ír, ez a tutorial pontosan megmutatja, hogyan. Az Aspose.Cells okos jelölőkkel egy egész tömböt egy értékként kezelhetsz, elkerülve a manuális ciklusokat és a cellán‑kénti írásokat.

Megtanulod, hogyan állíts be egy munkafüzetet, definiálj egy okos jelölőt, kötöd a `Map` adatforrást, amely egy JSON‑szerű tömböt tartalmaz, és végül mented a fájlt. A példa Java 17+, Maven és az ingyenes Aspose.Cells for Java próbaverzió könyvtárral működik.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Képernyőkép egy Java-ban Aspose.Cells okos jelölőkkel létrehozott Excel munkafüzetről"}

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|----------------|
| Java 17 vagy újabb | A legújabb nyelvi funkciók és biztonsági frissítések |
| Maven 3.6+ | Egyszerűsíti a függőségkezelést |
| Aspose.Cells for Java (v23.12 vagy újabb) | Biztosítja a mintában használt `Workbook`, `Worksheet` és smart‑marker API‑kat |
| Alapvető Java gyűjtemények ismerete | Létrehozni fogsz egy `Map<String, Object>`-et, amely adatforrásként szolgál |

Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Excel workbook Java létrehozása – teljes példa

Az alábbi program egy **teljes, futtatható** megoldás. Másold egy `ExcelSmartMarkerDemo.java` nevű fájlba, fordítsd le, és futtasd.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Mit csinál a kód

1. **Új munkafüzetet hoz létre** – a `new Workbook()` egy memóriában lévő Excel fájlt ad egy alapértelmezett lappal.  
2. **Okos jelölőt helyez el az A1 cellában** – a `{{jsonArray:ArrayAsSingle}}` azt mondja az Aspose.Cells-nek, hogy cserélje le a jelölőt a *teljes* tömbre, vesszőkkel összefűzve.  
3. **Létrehozza a `Map` adatforrást** – a `"jsonArray"` kulcs megegyezik a jelölő nevével; az érték egy `String[]`.  
4. **Meghívja a `setSmartMarkerData`-t** – ez összekapcsolja a map-et a jelölővel és végrehajtja a cserét.  
5. **Mentés a fájlba** – a `workbook.save(...)` a `JsonSingleValue.xlsx` fájlt írja a lemezre.

Amikor megnyitod a generált Excel fájlt, az **A1** cella tartalma:

```
One, Two, Three
```

A tömb egyetlen, vesszővel elválasztott karakterláncként jelenik meg a `ArrayAsSingle` opció miatt.

---

## Aspose.Cells okos jelölő használata JSON adatok kötéséhez

Az Aspose.Cells okos jelölők hatékony módja a komplex objektumok (beleértve a JSON‑szerű struktúrákat) közvetlenül a munkalapokra leképezésének. A `{{fieldName:Option}}` szintaxis nagyon hasonlít egy sablonmotorra:

* **fieldName** – a kulcs az adatforrásodban (`Map`, POJO vagy `DataTable`).  
* **Option** – szabályozza, hogyan kezeljék a gyűjteményeket. Az `ArrayAsSingle` az egész gyűjteményt egy értékként kezeli; más opciók, mint az `Array`, a tömböt sorokra bontanák.  

**Miért használjunk okos jelölőt a ciklus helyett?**  
A ciklus manuális cellacím-számításokat, hibára hajlamos indexelést és extra kódot igényel a formázáshoz. Az okos jelölők lehetővé teszik deklaratív helyőrzők írását, rövid Java kódot, és a könyvtár kezeli a elrendezés részleteit.

---

## Java Map adatforrás beállítása

A `Map<String, Object>` a legegyszerűbb adatkonténer az Aspose.Cells számára:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*A kulcs (`jsonArray`) pontosan meg kell egyezzen a jelölő nevével.*  
Használhatsz `List<String>`-et, egy egyedi POJO-t, vagy akár egy beágyazott `Map`-et is összetettebb JSON struktúrákhoz. Az Aspose.Cells automatikusan bejárja az objektum gráfot.

**Tipp:** Ha másként szeretnéd formázni az összefűzött karakterláncot (pl. pontosvesszőkkel), előfeldolgozhatod a tömböt Java-ban, mielőtt a map-hez rendelnéd:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## A munkafüzet mentése és a kimenet ellenőrzése

```java
workbook.save("JsonSingleValue.xlsx");
```

A `save` metódus számos formátumot támogat (`.xlsx`, `.xls`, `.csv`, `.pdf`). Ebben a tutorialban az alapértelmezett Excel Open XML formátumot használjuk.

**Ellenőrzési lépések**

1. Nyisd meg a `JsonSingleValue.xlsx` fájlt Microsoft Excel, LibreOffice Calc vagy Google Sheets programban.  
2. Győződj meg róla, hogy az **A1** cella `One, Two, Three` értéket tartalmaz.  
3. Ellenőrizd, hogy nem került hozzá extra sor vagy oszlop – az okos jelölő helyben cserélte ki.  

Ha a cella a nyers jelölő szöveget (`{{jsonArray:ArrayAsSingle}}`) mutatja, ellenőrizd, hogy:

* A jelölő neve pontosan megegyezik a map kulcsával (kis‑nagybetű érzékeny).  
* A `setSmartMarkerData` **a** jelölő elhelyezése **után** van meghívva.  
* Az Aspose.Cells verzió támogatja az `ArrayAsSingle` opciót (elérhető v20.3-tól).

---

## Gyakori variációk és szélhelyzetek

| Szituáció | Módosítás |
|----------|------------|
| **Eltérő elválasztó** | Használd az `ArrayAsSingle`-t egy egyedi összefűzéssel Java-ban (lásd a fenti tippet). |
| **Több tömb egy lapon** | Helyezz el további jelölőket, például `{{anotherArray:ArrayAsSingle}}` más cellákban, és adj hozzá megfelelő bejegyzéseket a map-hez. |
| **Beágyazott JSON objektumok** | Adj meg egy beágyazott `Map<String, Object>`-et; hivatkozz a mezőkre pont jelöléssel (`{{parent.child}}`). |
| **Nagy adathalmazok** | Több ezer sor esetén inkább az `Array` opciót használd, hogy az Aspose.Cells automatikusan bővítse a sorokat, ami |

## Mit érdemes következőként megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}