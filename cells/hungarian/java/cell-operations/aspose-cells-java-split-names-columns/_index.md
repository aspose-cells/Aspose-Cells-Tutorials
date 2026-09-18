---
date: '2026-03-15'
description: Tanulja meg, hogyan lehet a neveket külön oszlopokra bontani, és az Aspose.Cells
  Java használatával xlsx munkafüzetet menteni egy lépésről‑lépésre útmutatóban.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Nevek felosztása oszlopokra
url: /hu/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mesteri szintű **aspose cells java**: Nevek oszlopokra bontása

Üdvözöljük átfogó **aspose cells java** oktatóanyagainkban. Ebben az útmutatóban megtanulja, **hogyan bontson szét neveket**, amelyek egyetlen Excel oszlopban vannak tárolva, két külön oszlopba – keresztnév és vezetéknév – a hatékony szöveg‑oszlopokra bontás funkcióval. Akár egy névjegyzék tisztításáról, egy CRM import előkészítéséről, vagy egyszerűen csak egy gyors módjáról van szó a táblázatok átalakításának, ez az oktatóanyag pontosan megmutatja, hogyan **save workbook xlsx** a transzformáció után.

## Quick Answers
- **Mi a tutorial tartalma?** Teljes név karakterláncok bontása keresztnév és vezetéknév oszlopokra az Aspose.Cells for Java segítségével.  
- **Melyik könyvtárverziót használja?** A legújabb stabil kiadás (2026 állapot szerint).  
- **Szükségem van licencre?** Egy ingyenes próba a fejlesztéshez működik; a termeléshez kereskedelmi licenc szükséges.  
- **Használhatok más elválasztókat?** Igen – csak módosítsa a `TxtLoadOptions`‑ban a szeparátort.  
- **Az eredmény .xlsx fájl lesz?** Természetesen, a munkafüzet XLSX formátumban kerül mentésre.

## Mi az **aspose cells java**?
**Aspose.Cells java** egy nagy teljesítményű Java API, amely lehetővé teszi a fejlesztők számára, hogy Excel fájlokat hozzanak létre, módosítsanak, konvertáljanak és megjelenítsenek a Microsoft Office nélkül. Támogatja az összes főbb Excel formátumot, és fejlett funkciókat kínál, mint például képletek, diagramok és adatkezelés.

## Why use **aspose cells java** for splitting names?
- **Zero‑install**: Bármely szerver‑oldali Java környezetben működik.  
- **Sebesség**: Nagy táblázatokat gyorsabban kezel, mint a natív Excel interop.  
- **Pontosság**: Teljes ellenőrzés az elválasztók, oszloptartományok és kimeneti formátumok felett.  
- **Megbízhatóság**: Nincs COM vagy Office függőség, így ideális felhő- vagy konténer környezetben.

## Előfeltételek
- Java Development Kit (JDK) 8 vagy újabb.  
- IDE, például IntelliJ IDEA vagy Eclipse (opcionális, de ajánlott).  
- Maven vagy Gradle a függőségkezeléshez.  

### Maven beállítás
Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle beállítás
Add the library to your `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tipp:** Használjon ideiglenes licencet az Aspose portálról a teljes funkcionalitás feloldásához fejlesztés közben.

## Lépésről‑lépésre megvalósítás

### 1. lépés: Hozzon létre egy munkafüzetet és érje el az első munkalapot
Először importálja a fő osztályokat, és hozza létre az új munkafüzetet. Ez egy tiszta Excel fájlt biztosít, amely készen áll az adatok beszúrására.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### 2. lépés: Töltse fel a munkalapot mintanévekkel
Ezután adjon néhány teljes név karakterláncot az **A** oszlopba. Valós projektben ezeket adatbázisból vagy CSV fájlból olvasná be.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### 3. lépés: Állítsa be a Text Load Options‑t az oszlopok bontásához
A `TxtLoadOptions` osztály megmondja az Aspose.Cells‑nek, hogyan értelmezze a szöveget. Itt szóközt (`' '`) használunk elválasztóként.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### 4. lépés: Bontsa szét a szöveget két oszlopra
Most hívja meg a `textToColumns()`‑t azon cellatartományon, amely a neveket tartalmazza. A `(0, 0, 5, opts)` paraméterek azt jelentik, *kezdje a 0‑s sorban, 0‑s oszlopban, dolgozzon fel 5 sort, a most definiált beállításokkal*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Ez a hívás után az A oszlop a keresztneveket, a B oszlop pedig a vezetékneveket tartalmazza.

### 5. lépés: Mentse a munkafüzetet XLSX fájlként
Végül írja a módosított munkafüzetet a lemezre. A `SaveFormat` enum biztosítja, hogy a fájl a modern XLSX formátumban legyen tárolva.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Miért fontos:** A **save workbook xlsx** használatával garantálja a kompatibilitást a legújabb Excel, Google Sheets és egyéb táblázatkezelő eszközök verzióival.

## Gyakorlati alkalmazások
- **Adattisztítás:** Gyorsan szétválasztja az összefűzött mezőket, mielőtt elemzési csővezetékekbe töltené.  
- **CRM integráció:** Átalakítja a lapos névjegyzéket egy strukturált táblává az importáláshoz.  
- **HR rendszerek:** Szétválasztja a munkavállalók teljes nevét a bérszámfejtés vagy juttatások feldolgozása céljából.

## Teljesítménybeli szempontok
1. **Kötegelt frissítések:** Használja a `ws.getCells().setRowHeight()` vagy hasonló kötegelt módszereket a terhelés csökkentéséhez.  
2. **Memóriakezelés:** Hívja a `wb.calculateFormula()`‑t csak szükség esetén, és gyorsan szabadítsa fel a nagy objektumokat.  
3. **Garbage Collection:** Futtassa a JVM-et megfelelő heap beállításokkal (`-Xmx2g` nagy fájlokhoz), hogy elkerülje az OutOfMemory hibákat.

## Gyakori problémák és megoldások

| Probléma | Megoldás |
|-------|----------|
| **A nevek középső kezdőbetűt tartalmaznak** (pl. “John A. Doe”) | Állítsa be az elválasztót, vagy utólag dolgozza fel a második oszlopot a vezetéknév kinyeréséhez. |
| **Váratlanul üres cellák** | Ellenőrizze, hogy a forrás tartomány (`textToColumns` paraméterek) megegyezik-e a tényleges adat sorokkal. |
| **Licenc nem található** | Helyezze az ideiglenes licencfájlt (`Aspose.Cells.lic`) a projekt gyökerébe, vagy állítsa be a licencet programkódból. |

## Gyakran feltett kérdések

**Q: Mi az Aspose.Cells Java?**  
A: Egy hatékony könyvtár, amely lehetővé teszi, hogy Java‑ban programozottan hozzon létre, módosítson és konvertáljon Excel fájlokat.

**Q: Tudok oszlopokat bontani más elválasztókkal, mint a szóköz?**  
A: Igen, testreszabhatja a `TxtLoadOptions` szeparátort az adatainak megfelelően.

**Q: Hogyan kezeljek nagy adathalmazokat az Aspose.Cells‑szel?**  
A: Optimalizálja a teljesítményt a memória kezelésével és a munkafüzet műveletek minimalizálásával, ahogy fentebb leírtuk.

**Q: Van elérhető támogatás, ha problémáim adódnak?**  
A: Látogassa meg az [Aspose Forum](https://forum.aspose.com/c/cells/9) közösségi segítségért, vagy vegye fel közvetlenül a kapcsolatot az Aspose támogatási csapattal.

**Q: Milyen formátumokba tudja az Aspose.Cells menteni a munkafüzeteket?**  
A: Széles körű Excel fájlformátumot támogat, beleértve az XLSX, XLS, CSV és egyebeket.

## Erőforrások

- **Dokumentáció**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Letöltés**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Vásárlás**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Ingyenes próba**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Ideiglenes licenc**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Boldog kódolást, és élvezze az **aspose cells java** teljes erejének kihasználását projektjeiben!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Utoljára frissítve:** 2026-03-15  
**Tesztelve ezzel:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose