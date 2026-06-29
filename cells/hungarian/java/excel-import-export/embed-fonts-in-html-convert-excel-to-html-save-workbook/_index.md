---
category: general
date: 2026-06-27
description: Ágyazz be betűtípusokat HTML-be, amikor Excel-t HTML-re konvertálsz.
  Tanulja meg, hogyan menthet egy munkafüzetet HTML-ként beágyazott betűtípusokkal
  egyszerű Java kóddal.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: hu
og_description: Betűkészletek beágyazása HTML-be Excel HTML-re konvertálása közben.
  Ez az útmutató bemutatja, hogyan lehet a munkafüzetet HTML-ként menteni a betűkészletek
  beágyazásával Java használatával.
og_title: Betűk beágyazása HTML-ben – Excel konvertálása HTML-re és a munkafüzet mentése
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Betűtípusok beágyazása HTML-be – Excel konvertálása HTML-re és a munkafüzet
  mentése
url: /hu/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Betűtípusok beágyazása HTML-ben – Excel konvertálása HTML-re és munkafüzet mentése

Valaha is szükséged volt **betűtípusok beágyazására HTML-ben**, amikor *Excel-t konvertálsz HTML-re*? Lehet, hogy egy jelentési portált építesz, és az alapértelmezett webes betűtípusok egyszerűen nem elegendőek. A jó hír, hogy nem kell lemondanod az unalmas, általános megjelenésről – az Aspose.Cells lehetővé teszi, hogy a táblázatban használt pontos betűkészleteket közvetlenül a generált HTML fájlba csomagold.

Ebben az útmutatóban egy teljes, azonnal futtatható Java példán keresztül mutatjuk be, hogyan **mentheted a munkafüzetet HTML‑ként** betűtípusok beágyazásával, miért lehet ez hasznos, és néhány gyakori buktatót is kiemelünk. A végére egy önálló HTML oldalad lesz, amely pontosan úgy néz ki, mint az eredeti Excel‑lap, hiányzó karakterek és külső CSS problémák nélkül.

## Mit fogsz megtanulni

- Hogyan tölts be egy meglévő Excel munkafüzetet (vagy hozz létre egy újat) Java‑ban.  
- Hogyan konfiguráld a `HtmlSaveOptions`‑t, hogy a munkafüzet betűtípusait közvetlenül beágyazza a HTML kimenetbe.  
- Hogyan hívd meg a `Workbook.save`‑t, hogy a fájl **HTML‑ként beágyazott betűtípusokkal** kerüljön mentésre.  
- Tippek nagy betűtípusfájlok kezeléséhez, egyedi betűtípus könyvtárakhoz, és a gyakori hibák elhárításához.

> **Előfeltétel:** Szükséged van az Aspose.Cells for Java (legújabb verzió) a classpath‑odon, valamint egy Java 8+ futtatókörnyezetre. Más harmadik féltől származó könyvtár nem szükséges.

---

## 1. lépés: A projekt beállítása és a szükséges osztályok importálása

Mielőtt a kódba merülnénk, győződjünk meg róla, hogy a fejlesztői környezet készen áll. Ha Maven‑t használsz, add hozzá az Aspose.Cells függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Ha inkább Gradle‑t használsz, az ekvivalens:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Pro tip:** Tartsd naprakészen a könyvtárat. Az új kiadások gyakran javítják a betűtípuskezelést és csökkentik a beágyazott adatok méretét.

Most importáljuk a szükséges osztályokat:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Ezek az importok hozzáférést biztosítanak a munkafüzet modellhez, a HTML export beállításokhoz és néhány segédosztályhoz.

---

## 2. lépés: Az Excel munkafüzet betöltése (vagy létrehozása)

Betölthetsz egy meglévő `.xlsx` fájlt, vagy létrehozhatsz egy munkafüzetet a helyben. Bemutatásképpen tegyük fel, hogy a projekt `resources` mappájában van egy `Sample.xlsx` nevű fájl.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Ha nincs forrásfájlod, gyorsan generálhatsz egy munkafüzetet:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Miért fontos:** Amikor betűtípusokat ágyazol be, az Aspose.Cells a munkafüzetben használt pontos betűdefiníciókat nyeri ki. Ha a munkafüzet egyedi betűtípusokat tartalmaz, azok az HTML‑ben is megjelennek, garantálva a vizuális hűséget.

---

## 3. lépés: HtmlSaveOptions konfigurálása a betűtípusok beágyazásához

Ez a tutorial szíve. Alapértelmezés szerint a `HtmlSaveOptions` CSS‑t ír, amely a rendszer betűtípusaira hivatkozik. Ennek megváltoztatásához engedélyezzük a `setEmbedFonts(true)` kapcsolót.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Mit csinálnak a beállítások

| Beállítás | Alapértelmezett | Hatás módosításkor |
|-----------|-----------------|--------------------|
| `setEmbedFonts(true)` | `false` | Beágyazza a teljes betűfájlokat (általában Base64‑kódolt data URI‑ként) a generált HTML‑be. |
| `setSubsetFonts(true)` | `false` | A beágyazott betűtípust csak a ténylegesen használt karakterekre szűkíti, drámaian csökkentve a fájlméretet. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Kiválaszthatod, hogy csak bizonyos betűtípusokat ágyazz be, ha licencelési korlátaid vannak. |

> **Edge case:** Ha a munkafüzet olyan betűtípust használ, amely nincs telepítve a szerveren, az Aspose.Cells egy alapértelmezett rendszerbetűtípusra vált. A meglepetések elkerülése érdekében győződj meg róla, hogy minden egyedi betűtípus elérhető a Java futtatókörnyezet betűtárban, vagy regisztráld őket manuálisan a `FontConfig`‑on keresztül.

---

## 4. lépés: A munkafüzet mentése HTML‑ként beágyazott betűtípusokkal

Miután a beállítások készen állnak, egyszerűen meghívjuk a `save`‑t. Az eredmény egyetlen `.html` fájl lesz, amely a munkafüzet adatait **és** a betűtípusfájlokat közvetlenül a markupba kódolva tartalmazza.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Amikor megnyitod a `page.html`‑t bármely modern böngészőben, az oldal pontosan ugyanazzal a tipográfiával jelenik meg, mint az Excel‑ben – külső betűtípusfájlok nélkül, hiányzó karakterek nélkül.

---

## 5. lépés: Az eredmény ellenőrzése és a kimenet megértése

Nyisd meg a generált HTML‑fájlt egy böngészőben (Chrome, Firefox, Edge – bármelyik megfelel). A munkalapnak hűen kell megjelenni. A betűtípusok valódi beágyazásának ellenőrzéséhez:

1. Jobb‑kattintás a lapon → „View Page Source”.  
2. Keresd meg az `@font-face`‑t. Találsz egy CSS‑szabályt, amely egy `src: url(data:font/ttf;base64,…)` sort tartalmaz – ez a Base64‑kódolt betűtípus adat.

Ha ezt látod, a **betűtípusok beágyazása HTML‑be** lépés sikeres volt.

### Gyakori kérdések

- **„Miért nagyobb a HTML‑fájl, mint vártam?”**  
  A teljes betűfájlok beágyazása több száz kilobájtot is hozzáadhat. Használd a `setSubsetFonts(true)`‑t a méret csökkentéséhez, vagy csak a szükséges lapokat konvertáld.

- **„Beágyazhatok csak egy meghatározott betűtípust?”**  
  Igen. Állítsd be a `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)`‑t, majd add meg a betűtípus neveket a `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`‑val.

- **„Mi van, ha a betűtípus licencelt és nem ágyazható be?”**  
  Kapcsold ki a kapcsolót (`setEmbedFonts(false)`) és biztosíts web‑biztonságos helyettesítőt CSS‑ben, vagy tedd közzé a betűtípust egy CDN‑en, ahol van engedélyed.

---

## 6. lépés: Nagy munkafüzetek kezelése és teljesítmény tippek

A betűtípusok beágyazása jól működik közepes méretű táblázatoknál, de egy tucatnyi egyedi betűtípust tartalmazó munkafüzet könnyen felrobbanthatja a HTML méretét. Íme néhány teljesítmény‑orientált ajánlás:

- **Subset fonts** (már bemutatva) a csak használt glifek megtartásához.  
- **Export only needed worksheets** a `htmlOpts.setExportActiveWorksheetOnly(true)` használatával.  
- **Compress the HTML** a generálás után (pl. gzip a szerveren) a hálózati késleltetés csökkentéséhez.  
- **Cache the generated HTML** ha ugyanazt az Excel‑fájlt gyakran kérik.

---

## 7. lépés: Következő lépések – Alapvető exporton túl

Miután elsajátítottad a **betűtípusok beágyazását HTML‑be**, érdemes felfedezni a kapcsolódó lehetőségeket:

- **Convert Excel to HTML with images** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Generate PDF instead of HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Create responsive HTML** a `htmlOpts.setExportActiveWorksheetOnly` és `htmlOpts.setExportGridLines` finomhangolásával.  

Mindezek a funkciók ugyanazt a mintát követik: konfiguráld a `*SaveOptions` objektumot, állítsd be a megfelelő kapcsolókat, és hívd meg a `Workbook.save`‑t.

---

## Összegzés

Most megtanultad, hogyan **ágyazz betűtípusokat HTML‑be**, miközben **Excel‑t konvertálsz HTML‑re** és **munkafüzetet mentesz HTML‑ként** az Aspose.Cells for Java segítségével. A kulcsfontosságú lépések:

1. Töltsd be vagy hozd létre a munkafüzetet.  
2. Hozd létre a `HtmlSaveOptions`‑t és engedélyezd a `setEmbedFonts(true)`‑t.  
3. Hívd meg a `Workbook.save`‑t a beállításokkal.

Az eredmény egyetlen, hordozható HTML fájl, amely pontosan úgy néz ki, mint az eredeti táblázat – hiányzó betűtípusok, extra CSS fájlok és a kliens gépén telepített betűtípusok függősége nélkül.

Nyugodtan kísérletezz a betűtípus‑szubszettel, a szelektív beágyazással, vagy akár a szerver‑oldali gyorsítótárazással nagy forgalmú környezetekben. Ha bármilyen furcsaságba ütközöl (például váratlanul nagy fájlok vagy hiányzó glifek), nézd át a bemutatott opcionális beállításokat és igazítsd őket.

Jó kódolást, és élvezd a pixel‑tökéletes HTML‑t, amelyet most közvetlenül a Java alkalmazásaidból szolgálhatsz ki!

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen cikkben bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy további API‑funkciókat saját projektjeidben is könnyedén elsajátíthasd.

- [Convert Excel to HTML in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel to HTML Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Export Excel to HTML using IStreamProvider & Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}