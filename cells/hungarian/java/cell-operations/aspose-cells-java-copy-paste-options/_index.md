---
date: '2026-02-22'
description: Tanulja meg, hogyan automatizálhatja az Excel-jelentéseket az Aspose.Cells
  Java-val, a CopyOptions és PasteOptions használatával, hogy a képletek pontosak
  maradjanak, és csak a látható értékeket illessze be.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Excel jelentések automatizálása – A CopyOptions és PasteOptions mesteri használata
  Java-ban az Aspose.Cells segítségével
url: /hu/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizálja az Excel jelentéskészítést az Aspose.Cells segítségével: CopyOptions és PasteOptions Java-ban

Szeretne **automatikusan Excel jelentéseket** készíteni Java-val? Az Aspose.Cells segítségével programozottan másolhat, beilleszthet és módosíthat képleteket, így a jelentések pontosak maradnak, és csak a szükséges adatokat továbbítja. Ebben az útmutatóban két alapvető funkciót mutatunk be – **CopyOptions.ReferToDestinationSheet** és **PasteOptions** – amelyek lehetővé teszik a képletreferenciák megőrzését és csak a látható cellák értékeinek beillesztését.

## Gyors válaszok
- **Mit csinál a `CopyOptions.ReferToDestinationSheet`?** Átírja a képleteket, hogy a céllapra mutassanak másoláskor.  
- **Hogyan illeszthetek be csak látható cellákat?** Állítsa be a `PasteOptions.setOnlyVisibleCells(true)` értéket `PasteType.VALUES` használatával.  
- **Melyik könyvtárverzió szükséges?** Aspose.Cells 25.3 vagy újabb.  
- **Szükség van licencre a termeléshez?** Igen, egy állandó vagy ideiglenes licenc eltávolítja a kiértékelési korlátokat.  
- **Használhatok Maven‑t vagy Gradle‑t?** Mindkettő támogatott; lásd az alábbi függőség‑példákat.

## Mi az a „automatikus Excel jelentéskészítés”?
Az automatikus Excel jelentéskészítés azt jelenti, hogy programozottan generál, konszolidál és formáz Excel munkafüzeteket, ezzel kiküszöbölve a kézi másol‑beillesztés lépéseit és csökkentve a hibákat. Az Aspose.Cells gazdag API‑t biztosít, amely lehetővé teszi a Java fejlesztők számára a táblázatok nagymértékű manipulálását.

## Miért használjuk a CopyOptions‑t és a PasteOptions‑t jelentéskészítéshez?
- **A képletek integritásának megőrzése** adatmozgatáskor a lapok között.  
- **Rejtett sorok/oszlopok kizárása** a jelentések tisztasága és fókuszáltsága érdekében.  
- **Teljesítmény növelése** csak a szükséges adatok másolásával, a teljes tartomány helyett.

## Előfeltételek
- Java 8 vagy újabb.  
- Maven vagy Gradle a függőségkezeléshez.  
- Aspose.Cells 25.3+ (próba, ideiglenes vagy állandó licenc).  

## Aspose.Cells beállítása Java‑hoz

Adja hozzá a könyvtárat a projektjéhez az alábbiak egyikével:

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Licenc beszerzése
- **Ingyenes próba** – Teljes funkcionalitás kiértékeléshez.  
- **Ideiglenes licenc** – Eltávolítja a próba korlátozásait tesztelés közben.  
- **Állandó licenc** – Ajánlott termelési környezetben.

Az Aspose.Cells inicializálása Java‑kódban:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Lépés‑ről‑lépésre útmutató

### 1. CopyOptions a ReferToDestinationSheet beállítással

#### Áttekintés
A `CopyOptions.ReferToDestinationSheet` **true** értékre állítása átírja a képletreferenciákat, hogy a másolás után az új lapra mutassanak.

#### 1. lépés: Workbook és Worksheet inicializálása
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 2. lépés: CopyOptions konfigurálása
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### 3. lépés: Másolási művelet végrehajtása
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Miért fontos*: Azok a képletek, amelyek eredetileg a `Sheet1`‑re hivatkoztak, most helyesen a `DestSheet`‑re fognak mutatni, így az automatizált jelentések megbízhatóak maradnak.

**Hibaelhárítási tipp**: Ha a képletek még mindig a régi lapra mutatnak, ellenőrizze, hogy a `setReferToDestinationSheet(true)` **a másolás előtt** lett‑e meghívva.

### 2. PasteOptions csak látható cellák értékeinek beillesztéséhez

#### Áttekintés
A `PasteOptions` lehetővé teszi, hogy meghatározza, mi kerüljön beillesztésre. A `PasteType.VALUES` és az `onlyVisibleCells=true` kombinációja csak a megjelenített értékeket másolja, figyelmen kívül hagyva a rejtett sorokat/oszlopokat és a formázást.

#### 1. lépés: Workbook és Worksheet inicializálása
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 2. lépés: PasteOptions konfigurálása
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### 3. lépés: Beillesztési művelet végrehajtása
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Miért fontos*: Ideális szűrt adatok kinyeréséhez vagy tiszta jelentések generálásához rejtett sorok és formázási „zaj” nélkül.

**Hibaelhárítási tipp**: Győződjön meg arról, hogy a sorok/oszlopok valóban rejtve vannak‑e Excelben a másolás előtt; ellenkező esetben belekerülnek a másolásba.

## Gyakorlati alkalmazások
1. **Pénzügyi konszolidáció** – Havi lapok egyesítése egy fő munkafüzetbe, miközben minden képlet pontos marad.  
2. **Szűrt adatok exportálása** – Csak a látható sorok átvétele egy szűrt táblázatból egy összegző lapra.  
3. **Ütemezett jelentéskészítés** – Éjszakánkénti Excel jelentés automatikus generálása pontos cellaértékekkel és helyes hivatkozásokkal.

## Teljesítmény‑szempontok
- **Workbook‑ok felszabadítása** a munka befejezésekor (`wb.dispose();`) a natív erőforrások felszabadításához.  
- **Kötegelt műveletek** – Több másolás/beillesztés egyesítése a terhelés csökkentése érdekében.  
- **Memóriafigyelés** – Nagy munkafüzetek esetén növelni kell a heap‑et (`-Xmx2g`).

## Gyakran Ismételt Kérdések

**Q1: Mire szolgál a `CopyOptions.ReferToDestinationSheet`?**  
A: Átírja a képletreferenciákat, hogy a másolás után a céllapra mutassanak, ezáltal a jelentésképletek helyesek maradnak.

**Q2: Hogyan illeszthetek be csak látható cellákat?**  
A: Állítsa be a `PasteOptions.setOnlyVisibleCells(true)` értéket, és válassza a `PasteType.VALUES`‑t.

**Q3: Használhatom az Aspose.Cells‑t licenc vásárlása nélkül?**  
A: Igen, elérhető ingyenes próba vagy ideiglenes licenc kiértékeléshez, de termelési környezetben állandó licenc szükséges.

**Q4: Miért maradnak néhány hivatkozás hibásan a másolás után?**  
A: Ellenőrizze, hogy a `ReferToDestinationSheet` **a másolás előtt** legyen engedélyezve, és hogy a forrásképletek ne tartalmazzanak külső munkafüzet‑hivatkozásokat.

**Q5: Milyen memória‑kezelési legjobb gyakorlatokat kövessek?**  
A: Szabadítsa fel a `Workbook` objektumokat a munka befejezésekor, dolgozzon nagy fájlokkal darabokban, és figyelje a JVM heap‑használatot.

**Q6: Lehet-e egy műveletben kombinálni a CopyOptions‑t és a PasteOptions‑t?**  
A: Igen, először másoljon `CopyOptions`‑szel, majd alkalmazza a `PasteOptions`‑t a cél‑tartományra.

## Források
- **Dokumentáció**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Letöltés**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Megvásárlás**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Ingyenes próba**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Ideiglenes licenc**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Támogatási fórum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Utoljára frissítve:** 2026-02-22  
**Tesztelt verzió:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose