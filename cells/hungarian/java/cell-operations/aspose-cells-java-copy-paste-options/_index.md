---
date: '2026-10-28'
description: Ismerje meg, hogyan illesszünk be értékeket az Aspose.Cells másolás és
  beillesztés opcióival Java-ban, lépésről‑lépésre kód, Maven függőség beállítása
  és licencelési tippek segítségével.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Ismerje meg, hogyan illesszünk be értékeket az Aspose.Cells másolás
  és beillesztés opcióival Java-ban, lépésről‑lépésre kód, Maven függőség beállítása
  és licencelési tippek segítségével.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Hogyan illesszünk be értékeket az Aspose.Cells másolás és beillesztés opcióival
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Hogyan illesszünk be értékeket az Aspose.Cells másolás és beillesztés opcióival
url: /hu/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan illesszünk be értékeket az Aspose.Cells másolás és beillesztés beállításaival

Automating Excel reporting in Java means you can generate, consolidate, and format workbooks without ever opening Excel manually. With **Aspose.Cells** you get full control over formulas, hidden rows, and cell values, so your reports stay accurate and lightweight. In this tutorial you’ll learn how to use **CopyOptions.ReferToDestinationSheet** to keep formulas correct and **PasteOptions** to paste only the visible values you need.

## Gyors válaszok
- **Mi a `CopyOptions.ReferToDestinationSheet` feladata?** Átírja a képleteket, hogy a másolási művelet után a cél munkalapra mutassanak.  
- **Hogyan illeszthetek be csak látható cellákat?** Hívja a `PasteOptions.setOnlyVisibleCells(true)`-t a `PasteType.VALUES`-szal együtt.  
- **Melyik könyvtárverzió szükséges?** Aspose.Cells 25.3 vagy újabb.  
- **Szükségem van licencre a termeléshez?** Igen – egy állandó vagy ideiglenes licenc eltávolítja a kiértékelési korlátokat.  
- **Használhatok Maven-t vagy Gradle-t?** Mindkettő támogatott; lásd az alábbi függőségi példákat.

## Mi az a „Excel jelentés automatizálása”?
Az Excel jelentés automatizálása azt jelenti, hogy programozott módon generál és frissít Excel munkafüzeteket, lehetővé téve jelentések létrehozását, egyesítését és formázását manuális másolás‑beillesztés nélkül, ami csökkenti a hibákat és órákat takarít meg az ismétlődő munkában. Ez a megközelítés ideális ütemezett kötegelt feladatokhoz, adat‑vezérelt műszerfalakhoz és pénzügyi konszolidációs folyamatokhoz.

## Miért használjuk a CopyOptions és PasteOptions osztályokat a jelentéskészítéshez?
Ez a két osztály lehetővé teszi, hogy a képlet hivatkozásokat érintetlenül tartsa másolás közben **és** csak a szűrés vagy sorok elrejtése után látható cellákat vonja ki. Együtt használva csökkentik az átvitt adatmennyiséget akár 80 %-kal tipikus szűrt‑táblázat esetekben, és garantálják, hogy a képletek helyesen számoljanak a cél munkalapon.

## Előfeltételek
- Java 8 vagy újabb.  
- Maven vagy Gradle a függőségkezeléshez.  
- Aspose.Cells 25.3+ (próba, ideiglenes vagy állandó licenc).  

## Aspose.Cells beállítása Java-hoz

Add the library to your project with one of the following:

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
- **Ingyenes próba** – teljes funkciókészlet kiértékeléshez.  
- **Ideiglenes licenc** – eltávolítja a próba korlátait a tesztelés során.  
- **Állandó licenc** – ajánlott termelési feladatokhoz.

Initialize Aspose.Cells in your Java code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Lépésről‑lépésre útmutató

### 1. copyOptions a referToDestinationSheet használatával

#### Áttekintés
`CopyOptions` az Aspose.Cells konfigurációs objektuma, amely szabályozza, hogyan kezelődnek a képletek és cellahivatkozások másolási művelet során. A `CopyOptions.ReferToDestinationSheet` `true` értékre állítása átírja a képlet hivatkozásokat, hogy a másolás után az új munkalapra mutassanak.

#### 1. lépés: munkafüzet és munkalapok inicializálása  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 2. lépés: copyOptions konfigurálása  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### 3. lépés: másolási művelet végrehajtása  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Miért fontos*: Azok a képletek, amelyek eredetileg a `Sheet1`-re hivatkoztak, most helyesen a `DestSheet`-re fognak hivatkozni, így az automatizált jelentései megbízhatóak maradnak.

**Hibaelhárítási tipp**: Ha a képletek még mindig a régi munkalapra hivatkoznak, győződjön meg róla, hogy a `setReferToDestinationSheet(true)` **a másolás előtt** van meghívva.

### 2. pasteOptions csak a látható cellák értékeinek beillesztéséhez

#### Áttekintés
`PasteOptions` az Aspose.Cells beállítási objektuma, amely meghatározza, mi kerül beillesztésre. A `PasteType.VALUES` és az `onlyVisibleCells=true` használatával csak a megjelenített értékek másolódnak, a rejtett sorok/oszlopok és a formázás figyelmen kívül marad.

#### 1. lépés: munkafüzet és munkalapok inicializálása  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 2. lépés: pasteOptions konfigurálása  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### 3. lépés: beillesztési művelet végrehajtása  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Miért fontos*: Ideális szűrt adatok kinyeréséhez vagy tiszta jelentések generálásához rejtett sorok vagy formázási zaj nélkül.

**Hibaelhárítási tipp**: Ellenőrizze, hogy a sorok/oszlopok valóban rejtve vannak-e az Excelben a másolás előtt; ellenkező esetben belekerülnek.

## Gyakorlati alkalmazások
1. **Pénzügyi konszolidáció** – havi munkalapok egyesítése egy fő munkafüzetbe, miközben minden képlet pontos marad.  
2. **Szűrt adat export** – csak a látható sorok kinyerése egy szűrt táblázatból egy összegző munkalapra.  
3. **Ütemezett jelentéskészítés** – automatizált éjszakai Excel jelentés létrehozása pontos cellaértékekkel és helyes hivatkozásokkal.

## Teljesítménybeli megfontolások
- **Munkafüzetek felszabadítása** a munka befejezésekor (`wb.dispose();`) a natív erőforrások felszabadításához.  
- **Kötegelt műveletek** – több másolás/beillesztés hívás csoportosítása a terhelés csökkentéséhez.  
- **Memória figyelése** – nagy munkafüzetekhez megnövelt heap (`-Xmx2g`) lehet szükséges.  
- Az Aspose.Cells támogat **50+ bemeneti és kimeneti formátumot**, és képes **akár 2 millió sor** tartalmazó munkafüzetek feldolgozására anélkül, hogy az egész fájlt memóriába töltené, magas áteresztőképességű teljesítményt nyújtva vállalati feladatokhoz.

## Gyakran ismételt kérdések

**Q: Mire használják a `CopyOptions.ReferToDestinationSheet`-t?**  
A: Átírja a képlet hivatkozásokat, hogy a másolás után a cél munkalapra mutassanak, biztosítva, hogy a jelentés képletei helyesek maradjanak.

**Q: Hogyan illeszthetek be csak látható cellákat?**  
A: Állítsa be a `PasteOptions.setOnlyVisibleCells(true)`-t és válassza a `PasteType.VALUES`-t.

**Q: Használhatom az Aspose.Cells-t licenc vásárlása nélkül?**  
A: Igen, ingyenes próba vagy ideiglenes licenc elérhető kiértékeléshez, de termeléshez állandó licenc szükséges.

**Q: Miért hibásak még mindig egyes hivatkozások a másolás után?**  
A: Ellenőrizze, hogy a `ReferToDestinationSheet` **a másolás előtt** legyen engedélyezve, és hogy a forrás képletek ne tartalmazzanak külső munkafüzet hivatkozásokat.

**Q: Milyen memória‑kezelési legjobb gyakorlatokat kövessek?**  
A: Szabadítsa fel a `Workbook` objektumokat a munka befejezésekor, dolgozzon nagy fájlokkal darabokban, és figyelje a JVM heap használatát.

**Q: Lehet-e egy műveletben kombinálni a CopyOptions és PasteOptions használatát?**  
A: Igen, láncolhatja őket úgy, hogy először a `CopyOptions`-szal másol, majd a `PasteOptions`-t alkalmazza a cél tartományra.

## Források
- **Dokumentáció**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Letöltés**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Vásárlás**: [Vásároljon Aspose.Cells](https://purchase.aspose.com/buy)  
- **Ingyenes próba**: [Aspose.Cells ingyenes próba](https://releases.aspose.com/cells/java/)  
- **Ideiglenes licenc**: [Ideiglenes licenc igénylése](https://purchase.aspose.com/temporary-license/)  
- **Támogatási fórum**: [Aspose támogatás](https://forum.aspose.com/c/cells)

---

**Utolsó frissítés:** 2026-10-28  
**Tesztelve:** Aspose.Cells 25.3 for Java  
**Szerző:** Aspose

## Kapcsolódó oktatóanyagok

- [Excel fájl olvasása Java – Munkafüzet cellaműveletek mestersége Aspose.Cells használatával](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Adatok hozzáadása cellához Excelben Aspose.Cells for Java használatával](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Excel cella sor és oszlop indexek konvertálása Aspose.Cells Java-val](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}