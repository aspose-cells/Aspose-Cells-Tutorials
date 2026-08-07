---
date: '2026-02-22'
description: Ismerje meg, hogyan változtathatja meg az Excel dátumrendszerét 1904-re
  az Aspose.Cells for Java segítségével, állítsa be az Excel dátumformátumot, és konvertálja
  hatékonyan az Excel 1904-es rendszerét.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Az Excel dátumrendszerének 1904-re módosítása az Aspose.Cells Java segítségével
url: /hu/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

 any missed items: The heading "## Set Excel date programmatically (secondary keyword)" we translated to Hungarian but keep parentheses. Good.

Also "## Convert Excel 1904 system back to 1900 (secondary keyword)" done.

Make sure to keep blockquote > note.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel dátumrendszer módosítása 1904-re az Aspose.Cells Java segítségével

A történelmi adatok kezelése Excelben kihívást jelenthet, mivel az Excel két különböző dátumrendszert támogat. **Ebben az útmutatóban megtanulja, hogyan változtassa meg az Excel dátumrendszerét 1904-es formátumra az Aspose.Cells for Java használatával**, ami egyszerűvé teszi az örökölt dátumok kezelését. Lépésről lépésre bemutatjuk a munkafüzet inicializálását, a 1904-es dátumrendszer engedélyezését és a módosítás mentését.

## Gyors válaszok
- **Mi a 1904-es dátumrendszer funkciója?** A napok számolását 1904. január 1‑től kezdi, így minden dátumot 1462 nappal eltol a alapértelmezett 1900-as rendszerhez képest.  
- **Miért használja az Aspose.Cells‑t a dátumrendszer módosításához?** Egyszerű API-t biztosít, amely Excel telepítése nélkül működik, és nagy fájlok támogatásával.  
- **Mely Java verziók támogatottak?** JDK 8 vagy újabb.  
- **Szükségem van licencre?** Egy ingyenes próbaidőszak elegendő az értékeléshez; a licenc eltávolítja a használati korlátokat.  
- **Vissza tudok konvertálni a 1900-as rendszerre később?** Igen, csak állítsa be a `setDate1904(false)` értéket.

## Mi az a 1904-es dátumrendszer az Excelben?
A 1904-es dátumrendszert eredetileg az Excel korai Macintosh verziói használták. A napok számolását 1904. január 1‑től kezdi, ami hasznos a régi táblázatokkal és egyes pénzügyi modellekkel való kompatibilitáshoz.

## Miért módosítsa az Excel dátumrendszert az Aspose.Cells segítségével?
- **Keresztplatformos kompatibilitás** – működik Windows, Linux és macOS rendszereken.  
- **Excel telepítése nem szükséges** – ideális szerveroldali feldolgozáshoz.  
- **Magas teljesítmény** – nagy munkafüzetek kezelése minimális memóriahasználattal.  

## Előkövetelmények
- Java Development Kit (JDK) 8 vagy újabb.  
- Maven vagy Gradle a függőségkezeléshez.  
- Alapvető Java programozási ismeretek.  

## Aspose.Cells for Java beállítása

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

## Excel dátumrendszer módosítása Aspose.Cells Java használatával

Az alábbi lépésről‑lépésre útmutató valóban **módosítja az Excel dátumrendszert**. Minden lépés rövid magyarázatot tartalmaz, majd a szükséges pontos kódot.

### 1. lépés: A munkafüzet inicializálása és betöltése
Először hozzon létre egy `Workbook` példányt, amely az Ön meglévő Excel fájljára mutat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 2. lépés: A 1904-es dátumrendszer engedélyezése
Használja a munkafüzet beállításait a dátumrendszer átváltásához.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tipp:** Később is meghívhatja a `setDate1904(false)` metódust, ha vissza szeretné állítani.

### 3. lépés: A módosított munkafüzet mentése
Végül írja a változtatásokat egy új fájlba (vagy felülírja az eredetit).

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

> **Megjegyzés:** A fenti kód a `tWorkbook` osztálynevet használja, ahogyan eredetileg megadták. Győződjön meg róla, hogy ez a gépelési hiba megfelel a projekt elnevezési konvencióinak, vagy szükség esetén javítsa `Workbook`-ra.

## Excel dátum programozott beállítása (másodlagos kulcsszó)
Ha a rendszer módosítása után egyedi cellaértékeket kell módosítania, használhatja a `Cells.get(i, j).putValue(Date)` metódust, ahol a dátumot az aktív dátumrendszer szerint értelmezi.

## Excel 1904-es rendszer visszaállítása 1900-ra (másodlagos kulcsszó)
A visszaállításhoz egyszerűen hívja meg:

```java
workbook.getSettings().setDate1904(false);
```

Ezután mentse újra a munkafüzetet.

## Gyakorlati alkalmazások
1. **Adatarchiválás** – Örökölt időbélyegek megőrzése régi Mac‑alapú táblázatok migrálásakor.  
2. **Keresztplatformos jelentéskészítés** – Olyan jelentések létrehozása, amelyek Windows és macOS rendszeren egyaránt megnyithatók dátumeltérések nélkül.  
3. **Pénzügyi modellezés** – Dátumszámítások összehangolása azzal a régi pénzügyi modellel, amely a 1904-es rendszert várja.  

## Teljesítménybeli megfontolások
- Korlátozza a munkafüzet műveleteket egyetlen munkamenetben a memóriahasználat alacsonyan tartása érdekében.  
- Használja a Java szemétgyűjtésének finomhangolását nagyon nagy fájlok esetén.  

## Gyakran ismételt kérdések

**Q: Mi a különbség a 1900 és a 1904-es dátumrendszerek között?**  
A: A 1900-as rendszer 1900. január 1‑től indul, míg a 1904-es rendszer 1904. január 1‑től, így minden dátum 1462 nappal eltolódik.

**Q: Meg tudom változtatni egy jelenleg Excelben nyitott munkafüzet dátumrendszerét?**  
A: Igen, de előbb be kell zárni a fájlt az Excelben; különben a mentés sikertelen lesz.

**Q: Szükségem van licencre a `setDate1904` használatához?**  
A: A metódus működik az ingyenes próbaidőszakban, de egy teljes licenc eltávolítja a tesztelési korlátokat.

**Q: Lehetséges csak egyetlen munkalap dátumrendszerét módosítani?**  
A: Nem, a dátumrendszer a munkafüzet szintű beállítás, amely minden munkalapra érvényes.

**Q: Hogyan ellenőrizhetem, hogy a dátumrendszer módosult?**  
A: Nyissa meg a mentett fájlt Excelben, lépjen a **File → Options → Advanced** menüpontra, és jelölje be a **"Use 1904 date system"** (1904-es dátumrendszer használata) jelölőnégyzetet.

## Következtetés
Most már tudja, hogyan **módosítsa az Excel dátumrendszert** 1904-re az Aspose.Cells for Java segítségével, hogyan állítsa be az Excel dátumformátumokat, és hogyan állítsa vissza szükség esetén. Illessze be ezeket a kódrészleteket az adatfeldolgozó csővezetékekbe, hogy biztosítsa a dátumkompatibilitást a különböző platformok között.

---

**Utolsó frissítés:** 2026-02-22  
**Tesztelt verzió:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose  

**Dokumentáció:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
**Letöltés:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
**Licenc vásárlása:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
**Ingyenes próba:** [Start Free Trial](https://releases.aspose.com/cells/java/)  
**Ideiglenes licenc:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)  
**Támogatási fórum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}