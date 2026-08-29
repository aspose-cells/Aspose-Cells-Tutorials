---
category: general
date: 2026-08-17
description: Ismerje meg, hogyan hozhat létre duplikált részletező munkalapokat az
  Aspose.Cells for Java segítségével, és engedélyezheti a duplikált munkalapneveket
  a SmartMarkerProcessor használatával.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: hu
lastmod: 2026-08-17
og_description: Készíts duplikált részletező lapokat az Aspose.Cells for Java-ban,
  és engedélyezd a duplikált lapneveket. Kövesd ezt a teljes útmutatót az azonnali
  eredményekért.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Részletes munkalapok másolása az Aspose.Cells for Java-ban – lépésről lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hogyan hozhatunk létre duplikált részletes munkalapokat az Aspose.Cells for
  Java-ban
url: /hu/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre duplikált részletező munkalapokat az Aspose.Cells for Java-ban

Ha **duplikált részletező munkalapokat** kell létrehoznia egy Excel munkafüzetben, az Aspose.Cells for Java egyszerűvé teszi ezt. Ez az útmutató pontosan bemutatja, hogyan engedélyezhetők a duplikált munkalapnevek a SmartMarkerProcessor használatával részletező munkalapok generálásakor, így olyan munkafüzetet hozhat létre, amely több, ugyanazt a nevet viselő munkalapot tartalmaz.

Látni fog egy teljes, futtatható példát, a konfigurációs lehetőségek részletes bontását, valamint tippeket a gyakori szélhelyzetek kezeléséhez, mint a névütközések és nagy adatkészletek. Külső hivatkozásokra nincs szükség – minden, amire szüksége van, a lentebb lévő kódban megtalálható.

## Előkövetelmények

* Java Development Kit (JDK) 8 vagy újabb.
* Maven vagy Gradle a függőségek kezeléséhez.
* Aspose.Cells for Java könyvtár (23.9 vagy újabb verzió). Adja hozzá a következő Maven függőséget a `pom.xml` fájlhoz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Egy mester sablon munkafüzet (`master_template.xlsx`), amely Smart Marker régiót tartalmaz a részletező adatokhoz.

## A megoldás áttekintése

A megoldás négy logikai lépést követ:

1. Töltse be a mester sablon munkafüzetet.
2. Állítsa be a `SmartMarkerProcessor`-t, hogy **engedélyezze a duplikált munkalapneveket**.
3. Dolgozza fel a munkafüzetet úgy, hogy minden adatcsoporthoz új részletező munkalap jöjjön létre.
4. Mentse el a keletkezett munkafüzetet, amely most már duplikált részletező munkalapokat tartalmaz.

Minden lépés részletesen van kifejtve alább, és a teljes forrásfájl a útmutató végén megtalálható.

## 1. lépés: A mester sablon munkafüzet betöltése

Az első művelet egy `Workbook` példányt hoz létre, amely a sablonfájlt képviseli. A sablonnak tartalmaznia kell egy Smart Marker helyőrzőt (pl. `&=DetailData`), amely megmondja a processzornak, hová szúrja be az adatokat.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Miért fontos:** A sablon betöltése elkülöníti a elrendezést és a formázást az adatgenerálási logikától, ami tiszta kódot eredményez, és megkönnyíti ugyanazon sablon újrahasználatát különböző adatcsoportokhoz.

## 2. lépés: A SmartMarkerProcessor beállítása a duplikált munkalapnevek engedélyezéséhez

Alapértelmezés szerint az Aspose.Cells egyedi munkalapneveket generál a részletező munkalapok létrehozásakor. A **duplikált munkalapnevek** engedélyezéséhez állítsa be a `DetailSheetNewName` opciót egy állandó értékre. A processzor minden generált munkalapnál ezt a nevet fogja újrahasználni.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Miért fontos:** A `DetailSheetNewName` beállítása azt mondja a motornak, hogy minden részletező munkalap ugyanazt a nevet használja, ami közvetlenül teljesíti a **duplikált munkalapnevek** engedélyezésének követelményét. Ez a megközelítés akkor hasznos, ha a downstream eszközök a munkalapokat a pozíciójuk alapján azonosítják, nem pedig a nevük szerint.

## 3. lépés: A munkafüzet feldolgozása a részletező munkalapok generálásához

A konfiguráció után hívja meg a `process` metódust a munkafüzeten. A processzor beolvassa a Smart Marker régiót, minden adatcsoporthoz új munkalapot hoz létre, és feltölti a megfelelő sorokkal.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Miért fontos:** A `process` hívás végzi a nehéz munkát – a Smart Marker-ek elemzését, a sablon munkalap klónozását és az adatok beszúrását. Mivel a `DetailSheetNewName` opció már be van állítva, minden új munkalap ugyanazt a nevet kapja, ami duplikált munkalapneveket eredményez a végleges fájlban.

## 4. lépés: A keletkezett munkafüzet mentése

Végül írja a módosított munkafüzetet egy új fájlba. A kimeneti fájl annyi “DetailSheet” fület tartalmaz majd, ahány adatcsoport van.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Miért fontos:** A fájl mentése befejezi a processzor által végzett módosításokat. A keletkezett munkafüzet megnyitható a Microsoft Excel, a LibreOffice vagy bármely más, XLSX formátumot támogató táblázatkezelő alkalmazásban.

## Teljes forráskód

Az összes elemet összevonva itt található a teljes program, amelyet másolhat, beilleszthet és futtathat:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Várt kimenet

Amikor megnyitja a `duplicate_detail.xlsx` fájlt, több, **DetailSheet** nevű fület fog látni. Minden fül a sablonban egy adott Smart Marker csoporthoz tartozó adatkészletet tartalmaz. A mester sablon elrendezése, formázása és képletei minden duplikált munkalapon megmaradnak.

## Gyakori problémák kezelése

| Probléma | Magyarázat | Megoldás |
|----------|------------|----------|
| Excel figyelmeztetést jelenít meg a duplikált munkalapnevekről | Az Excel engedélyezi a duplikált neveket, de a fájl megnyitásakor figyelmeztetést jeleníthet meg. | A figyelmeztetés ártalmatlan; a munkafüzet helyesen működik. Ha el szeretné kerülni a figyelmeztetést, a feldolgozás után nevezze át a munkalapokat a `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);` kóddal. |
| Nagy adatcsoportok magas memóriahasználatot okoznak | Minden duplikált munkalap a sablon teljes másolatát hozza létre, ami RAM-ot fogyaszthat. | Engedélyezze a streaming módot a `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` hívással a sablon betöltése előtt. |
| Smart Marker régió nem található | A processzor nem találja a `&=DetailData` helyet a sablonban. | Ellenőrizze, hogy a helyőrző szintaxisa megfelel-e az adatforrásnak, és hogy a sablon munkalap nincs elrejtve. |

## Profi tipp: a duplikált elnevezési séma testreszabása

Ha egy kiszámítható elnevezési mintára van szüksége, miközben továbbra is engedélyezi a duplikációkat, kombináljon egy alapnevet egy indexszel:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

A `{0}` helyőrzőt a munkalap indexe helyettesíti, így olyan nevek jönnek létre, mint `DetailSheet_1`, `DetailSheet_2` stb. Ez továbbra is megfelel a **duplikált munkalapnevek** követelményének, mivel az alapnév állandó marad.

## Következő lépések

Most, hogy **duplikált részletező munkalapokat** tud létrehozni, a következő témákat érdemes felfedezni:

* **Részletező munkalapok feltöltése képekkel** – használjon `Picture` objektumokat logók vagy diagramok beágyazásához.
* **Feltételes formázás alkalmazása** – adjon `FormatCondition` szabályokat a sorok értékek alapján való kiemeléshez.
* **Exportálás PDF-be** – hívja a `workbook.save("output.pdf", SaveFormat.PDF);` metódust a duplikált munkalapok PDF változatának létrehozásához.

Ezek a kiterjesztések mind a bemutatott Smart Marker munkafolyamaton alapulnak, lehetővé téve, hogy magabiztosan automatizálja a komplex Excel jelentéskészítési feladatokat.

---

*Megtanulta, hogyan hozhat létre duplikált részletező munkalapokat az Aspose.Cells for Java-ban, és hogyan engedélyezheti a duplikált munkalapneveket a SmartMarkerProcessor segítségével. Alkalmazza a kódot, igazítsa a sablont, és integrálja a technikát jelentéskészítő folyamatába.*

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Excel munkalapok létrehozása és elérése, PDF könyvjelzők hozzáadása az Aspose.Cells for Java használatával](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Excel munkalapok létrehozása és elérése, PDF könyvjelzők hozzáadása Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Excel munkalapok létrehozása és elérése, PDF könyvjelzők hozzáadása Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}