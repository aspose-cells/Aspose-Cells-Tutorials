---
category: general
date: 2026-08-20
description: Tanulja meg, hogyan exportálhatja az Excelt TXT formátumba, miközben
  korlátozza a tizedesjegyek számát, megőrizve a jelentős számjegyeket, és Java-val
  TXT-ként menti a munkafüzetet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: hu
lastmod: 2026-08-20
og_description: Exportálja az Excelt TXT-be az Aspose.Cells segítségével. Ez az útmutató
  bemutatja, hogyan korlátozhatja a tizedesjegyek számát, megőrizheti a jelentős számjegyeket,
  és mentheti a munkafüzetet TXT formátumban Java-ban.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Excel exportálása TXT-be Java-ban – a tizedesjegyek és a jelentős számjegyek
  szabályozása
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Hogyan exportáljunk Excel-t TXT-be az Aspose.Cells segítségével, és szabályozzuk
  a tizedes pontosságot
url: /hu/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk Excel-t TXT-be az Aspose.Cells segítségével, és szabályozzuk a tizedesjegyek pontosságát

Ha **Excel-t TXT-be szeretnél exportálni**, és biztosítani akarod, hogy a kimenet egy meghatározott számú tizedesjegyet tartalmazzon, ez az útmutató teljes megoldást nyújt. Megmutatjuk, hogyan korlátozhatod a tizedesjegyek számát, hogyan őrizheted meg a jelentős számjegyeket, és hogyan **mentheted a munkafüzetet TXT-ként** az Aspose.Cells Java könyvtár segítségével.

A tutorial lépésről lépésre bemutatja egy munkafüzet létrehozását, egy nagy pontosságú érték beillesztését, a TXT mentési beállítások konfigurálását, valamint a fájl lemezre írását. A végére képes leszel olyan szövegfájlt generálni, amely pontosan a kívánt pontosságot tartalmazza, manuális utófeldolgozás nélkül.

## Amire szükséged lesz

- Java 17 (vagy bármely támogatott JDK)
- Aspose.Cells for Java 23.10 vagy újabb
- IDE vagy build eszköz (Maven/Gradle) a függőségek kezeléséhez
- Írási jogosultság a kimeneti könyvtárban

## 1. lépés: Munkafüzet létrehozása és az első munkalap elérése

A munkafüzet létrehozása az első lépés, amikor **Excel-t TXT-be szeretnél exportálni**. A `Workbook` osztály képviseli az egész Excel-fájlt, a `Worksheet` pedig hozzáférést biztosít a cellákhoz.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Miért fontos*: A munkafüzet objektum tartalmazza az összes adatot, stílust és metaadatot. Egy friss munkafüzet használata garantálja, hogy rejtett formázások ne befolyásolják a szöveg exportálását.

## 2. lépés: Numerikus érték hozzáadása és a tizedesjegyek korlátozása

Illessz be egy számot, amely sok tizedesjegyet tartalmaz, hogy bemutathasd, hogyan **korlátozhatod a tizedesjegyek számát** exportálás közben.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Miért fontos*: Az Excel a teljes pontosságot tárolja, de exportáláskor előfordulhat, hogy le kell vágni vagy kerekíteni kell az értéket. A `limit decimal places` beállítás ezt automatikusan kezeli.

## 3. lépés: TXT mentési beállítások konfigurálása a jelentős számjegyek megtartásához

Az Aspose.Cells biztosítja a `TxtSaveOptions` osztályt. A `significantDigits` beállítása azt mondja az exportálónak, hogy csak a szükséges számú jelentős számjegyet tartsa meg, a vezető nullákat figyelmen kívül hagyva.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Miért fontos*: A **keep significant digits** opció biztosítja, hogy a kimeneti fájl előre meghatározott pontosságot tartalmazzon, ami elengedhetetlen azoknak a downstream rendszereknek, amelyek fix szélességű numerikus formátumot várnak.

## 4. lépés: Munkafüzet mentése TXT-ként

Végül írd a munkafüzetet egy szövegfájlba. A `save` metódus figyelembe veszi a korábban beállított opciókat, így a kapott fájl a korlátozott tizedesjegy-reprezentációt tartalmazza.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Miért fontos*: A **save workbook as txt** a megfelelő `TxtSaveOptions` használatával garantálja, hogy az exportált fájl megfeleljen a korábban beállított pontossági korlátozásoknak.

### Várható tartalom a `SignificantDigits.txt` fájlban

```
0.00012346
```

Az érték öt jelentős számjegyet (`12346`) mutat a kerekítés után, a vezető nullák pedig a TXT formátum szerint megmaradnak.

## Variációk és szélsőséges esetek

| Forgatókönyv | Módosítás |
|--------------|-----------|
| **Eltérő számú jelentős számjegy** | Hívd meg a `txtOptions.setSignificantDigits(n)` metódust, ahol az `n` 1‑15 között van. |
| **Tartomány exportálása a teljes lap helyett** | Használd a `txtOptions.setExportRange("A1:B10")` beállítást mentés előtt. |
| **Oszlopelválasztók megőrzése** | Állítsd be a `txtOptions.setSeparator('\t')` értéket tab‑elválasztott kimenethez. |
| **Nagy munkalapok** | Növeld a `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` értékét, hogy elkerüld a `OutOfMemoryError` hibát. |

## Gyakori buktatók és profi tippek

- **Ne keverd össze a jelentős számjegyeket a tizedesjegyekkel**. A vezető nullák nem számítanak jelentősnek; használj `setSignificantDigits`-et a valódi pontossághoz, és `setDecimalPlaces`-t, ha a tizedesvessző után fix számú jegyet szeretnél.
- **Mindig adj meg abszolút kimeneti útvonalat** IDE-ből futtatáskor, hogy elkerüld a jogosultsági hibákat.
- **Ellenőrizd a generált fájlt** egyszerű `java.nio.file.Files.readAllLines(Paths.get(outputPath))` hívással, hogy biztosan megfeleljen a várakozásoknak, mielőtt downstream folyamatokba továbbadnád.

## Teljes forráskód referenciaként

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

A program futtatása `SignificantDigits.txt` fájlt hoz létre, amely egyetlen sort tartalmaz: `0.00012346`, demonstrálva, hogy a **export excel to txt** folyamat egyaránt tiszteletben tartja a **limit decimal places** és a **keep significant digits** követelményeket.

## Következtetés

Most már tudod, hogyan **exportálj Excel-t TXT-be** az Aspose.Cells for Java segítségével, miközben szabályozod a numerikus pontosságot. A `TxtSaveOptions` konfigurálásával **korlátozhatod a tizedesjegyek számát**, **megtarthatod a jelentős számjegyeket**, és megbízhatóan **mentheted a munkafüzetet txt-ként** további utófeldolgozás nélkül.

További lépések:

- Több munkalap exportálása külön TXT fájlokba (`save workbook as txt` egyenként laponként)
- `setSeparator` használata CSV‑kompatibilis kimenet létrehozásához
- Tömeges konverziók automatizálása nagy adathalmazok esetén

Nyugodtan kísérletezz különböző számjegyszámokkal és elválasztókkal, hogy pontosan a projekted igényeinek megfelelő eredményt kapd. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd az API további funkcióit, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java \| Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}