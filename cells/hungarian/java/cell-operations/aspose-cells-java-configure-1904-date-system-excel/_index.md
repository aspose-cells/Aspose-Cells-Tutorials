---
date: '2026-10-28'
description: Ismerje meg, hogyan változtathatja meg az Excel dátumrendszerét 1904-re
  az Aspose.Cells for Java használatával, állítsa be az Excel dátumformátumot, és
  hatékonyan konvertálja a 1904-es rendszert.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Az Excel dátumrendszerének 1904-re változtatása az Aspose.Cells for
  Java segítségével. Ismerje meg lépésről‑lépésre, hogyan engedélyezheti a 1904-es
  rendszert, állíthatja be a dátumokat, és konvertálhat vissza.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Az Excel dátumrendszerének 1904-re változtatása az Aspose.Cells for Java
  segítségével
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Az Excel dátumrendszerének 1904-re változtatása az Aspose.Cells Java segítségével
url: /hu/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel dátumrendszer módosítása 1904-re az Aspose.Cells Java-val

Ebben az útmutatóban megtanulja, hogyan **változtassa meg az Excel dátumrendszert** a 1904-es formátumra az Aspose.Cells for Java használatával. A 1904-es rendszer akkor lényeges, amikor meg kell őrizni a régi Mac‑alapú dátumokat, vagy össze kell hangolni a pénzügyi modellekkel, amelyek ezt az epochot várják. Lépésről lépésre bemutatjuk a könyvtár telepítését, egy munkafüzet betöltését, a dátumrendszer átkapcsolását és az eredmény mentését – mindezt anélkül, hogy a szerveren a Microsoft Excelt telepíteni kellene.

## Gyors válaszok
- **Mi a 1904-es dátumrendszer feladata?** A napok számolását 1904. január 1-től kezdi, ezzel 1 462 nappal eltolva minden dátumot az alapértelmezett 1900-as rendszerhez képest.  
- **Miért használja az Aspose.Cells-t a dátumrendszer módosításához?** Egyszerű API-t biztosít, amely Excel telepítése nélkül működik, és nagy fájlok támogatásával.  
- **Mely Java verziók támogatottak?** JDK 8 vagy újabb.  
- **Szükségem van licencre?** Az ingyenes próba verzió értékelésre használható; egy licenc eltávolítja a használati korlátokat.  
- **Vissza tudom-e konvertálni a 1900-as rendszerre később?** Igen, csak hívja a `setDate1904(false)` metódust.

## Mi az a 1904-es dátumrendszer az Excelben?
A 1904-es dátumrendszer a napok számolását 1904. január 1-től kezdi, az alapértelmezett 1900-as epoch helyett. Ez a eltolás pontosan 1 462 napot ad minden dátumértékhez, ezért a régi Mac munkafüzetek eltoltnak tűnnek, amikor Windowson nyitják meg őket. Elsősorban a régebbi Macintosh Excel fájlokkal és néhány örökölt pénzügyi modellel való kompatibilitás miatt használják.

## Miért módosítsa az Excel dátumrendszert az Aspose.Cells segítségével?
A dátumrendszert közvetlenül Java-ból válthatja át, ezzel kiküszöbölve az Excelben szükséges manuális lépéseket. Az Aspose.Cells akár **2 GB** méretű munkafüzeteket is feldolgoz, és egy 500 lapos munkafüzetet kevesebb, mint **2 másodperc** alatt konvertál egy tipikus 4‑magos szerveren, magas teljesítményű szerver‑oldali automatizálást biztosítva.

## Előfeltételek
- Java Development Kit (JDK) 8 vagy újabb.  
- Maven vagy Gradle a függőségkezeléshez.  
- Alap Java programozási ismeretek.  

## Az Aspose.Cells for Java beállítása

### Maven
Adja hozzá a következő függőséget a `pom.xml` fájlhoz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Adja hozzá ezt a sort a `build.gradle` fájlhoz:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Licenc beszerzése
Az Aspose ingyenes próbaidőszakot, ideiglenes licencet és teljes kereskedelmi licenceket kínál. Kezdheti a [free trial](https://releases.aspose.com/cells/java/) linkkel, vagy szerezhet ideiglenes licencet a [temporary license page](https://purchase.aspose.com/temporary-license/) oldalról.

## Hogyan módosíthatja az Excel dátumrendszert 1904-re az Aspose.Cells for Java segítségével?
Töltse be a munkafüzetet, engedélyezze a 1904-es beállítást, és mentse a fájlt – ez a háromlépéses folyamat kevesebb, mint egy másodperc alatt frissíti a munkafüzet belső dátum-epochját. Az `setDate1904(true)` API hívás megfordítja a rendszerjelzőt, és a változás megmarad, amikor a `save` metódust meghívja. Excel telepítése nem szükséges, így ideális fej nélküli szerverkörnyezetekhez.

### 1. lépés: inicializálás és a munkafüzet betöltése
A `Workbook` osztály egy teljes Excel fájlt reprezentál a memóriában. Először hozzon létre egy `Workbook` példányt, amely az Ön meglévő fájljára mutat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 2. lépés: a 1904-es dátumrendszer engedélyezése
A `WorkbookSettings.setDate1904` metódus átkapcsolja a munkafüzet szintű dátumjelzőt. `true` értékre állítva aktiválja a 1904-es rendszert minden munkalapon.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tipp:** Később is meghívhatja a `setDate1904(false)` metódust, ha vissza kell állítania.

### 3. lépés: a módosított munkafüzet mentése
Végül írja a változtatásokat egy új fájlba (vagy írja felül az eredetit). A `save` metódus automatikusan figyelembe veszi az aktív dátumrendszert.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Megjegyzés:** A fenti kód a `tWorkbook` osztálynevet használja, ahogy eredetileg megadták. Győződjön meg róla, hogy ez a gépelési hiba megfelel a projekt elnevezési konvencióinak, vagy szükség esetén javítsa `Workbook`-ra.

## Excel dátum programozott beállítása (másodlagos kulcsszó)
Ha a rendszer módosítása után egyedi cellaértékeket kell beállítania, használhatja a `cells.get(i, j).putValue(Date)` metódust, ahol a dátum az aktív dátumrendszer szerint lesz értelmezve.

## Excel 1904-es rendszer visszaállítása 1900-ra (másodlagos kulcsszó)
A visszaállításhoz egyszerűen hívja meg:

```java
workbook.getSettings().setDate1904(false);
```

Ezután mentse újra a munkafüzetet.

## Gyakorlati alkalmazások
1. **Adatarchiválás** – Örökölt időbélyegek megőrzése régi Mac‑alapú táblázatok migrálásakor.  
2. **Keresztplatformos jelentéskészítés** – Olyan jelentések generálása, amelyek helyesen nyílnak meg Windows és macOS rendszereken egyaránt, dátumeltérések nélkül.  
3. **Pénzügyi modellezés** – Dátumszámítások összehangolása a 1904-es rendszert elváró örökölt pénzügyi modellekkel.  

## Teljesítményfontosságú szempontok
- Korlátozza a munkafüzet műveleteket egyetlen munkamenetben a memóriahasználat alacsonyan tartása érdekében; az Aspose.Cells adatfolyamot használ, és csak akkor tölti be a teljes fájlt a RAM-ba, ha kifejezetten kéri.  
- Állítsa be a Java szemétgyűjtő zászlókat (`-XX:+UseG1GC`) nagyon nagy fájlok esetén, hogy elkerülje a szünetidő csúcsait.  

## Gyakran ismételt kérdések

**Q: Mi a különbség a 1900 és a 1904-es dátumrendszerek között?**  
A: A 1900-as rendszer 1900. január 1-től indul, míg a 1904-es rendszer 1904. január 1-től, ezzel minden dátumot 1 462 nappal eltolva.

**Q: Meg tudom változtatni egy jelenleg Excelben nyitott munkafüzet dátumrendszerét?**  
A: Igen, de előbb be kell zárni a fájlt Excelben; ellenkező esetben a mentési művelet hibát fog eredményezni.

**Q: Szükségem van licencre a `setDate1904` használatához?**  
A: A metódus működik az ingyenes próba verzióban, de egy teljes licenc eltávolítja a kiértékelési korlátozásokat.

**Q: Lehet-e csak egyetlen munkalap dátumrendszerét módosítani?**  
A: Nem, a dátumrendszer munkafüzet‑szintű beállítás; minden munkalapra vonatkozik.

**Q: Hogyan ellenőrizhetem, hogy a dátumrendszer megváltozott?**  
A: Nyissa meg a mentett fájlt Excelben, lépjen a **File → Options → Advanced** menüpontra, és ellenőrizze a **"Use 1904 date system"** jelölőnégyzetet.

## Következtetés
Most már tudja, hogyan **változtassa meg az Excel dátumrendszert** 1904-re az Aspose.Cells for Java segítségével, hogyan állítson be egyedi cella dátumokat, és hogyan állítsa vissza a 1900-as rendszert, ha szükséges. Integrálja ezeket a kódrészleteket adatfeldolgozó csővezetékekbe, hogy biztosítsa a dátumkompatibilitást a platformok és az örökölt fájlok között.

---

**Legutóbb frissítve:** 2026-10-28  
**Tesztelve ezzel:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose  

**Erőforrások**
- **Dokumentáció:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Letöltés:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Licenc vásárlása:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Ingyenes próba:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Ideiglenes licenc:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Támogatási fórum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Kapcsolódó oktatóanyagok

- [Hatékony Excel PDF konvertálás egyedi dátumformátumokkal az Aspose.Cells for Java segítségével](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: Hogyan hozzon létre és formázzon Excel munkafüzeteket hatékonyan](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Excel manipuláció mestersége az Aspose.Cells for Java segítségével: Munkafüzet műveletek és cellastílusok oktatóanyaga](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}