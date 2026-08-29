---
category: general
date: 2026-08-14
description: Tartomány másolása munkafüzetek között Java-val az Aspose.Cells használatával.
  Tanulja meg, hogyan másoljon pivot tábla munkafüzetet, exportáljon képet PowerPointba,
  és távolítsa el az AutoFilter-t az Excel táblázatból.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: hu
lastmod: 2026-08-14
og_description: Tartomány másolása munkafüzetek között Java-ban. Ez az útmutató bemutatja,
  hogyan másoljunk pivot tábla munkafüzetet, exportáljunk képet PowerPointba, és hogyan
  távolítsuk el az AutoFilter-t az Excel táblázatból.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Tartomány másolása munkafüzetek között Java-ban – teljes Aspose.Cells útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Tartomány másolása munkafüzetek között Java‑ban – lépésről‑lépésre útmutató
url: /hu/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tartomány másolása munkafüzetek között Java-ban – lépésről‑lépésre útmutató

Ha Java-ban **copy range between workbooks**-t kell végrehajtani, az Aspose.Cells tiszta API-t biztosít, amely kezeli az összetett objektumokat, például a pivot táblákat és képeket. Ez az útmutató bemutatja, hogyan **copy pivot table workbook**, **export picture to PowerPoint**, és **remove AutoFilter from Excel table**, miközben a kód könnyen olvasható és karbantartható marad.

Megtanulja, hogyan:

* Betölteni egy forrás munkafüzetet és meghatározni a forrás tartományt.  
* Létrehozni egy cél munkafüzetet és másolni a tartományt úgy, hogy a pivot tábla érintetlen maradjon.  
* Exportálni a munkalap első képét szerkeszthető PowerPoint objektumként.  
* Eltávolítani egy AutoFilter-t az első Excel táblázatból.  
* Betölteni egy munkafüzetet `SmartMarkerOptions`-szel, hogy a JSON tömböket egyetlen cellaértékként kezelje.

A példa az Aspose.Cells 23.10 for Java-t használja, de a koncepciók korábbi verziókra is alkalmazhatók.

---

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|----------------|
| Java 17 vagy újabb | Az újabb Aspose.Cells futtatókörnyezet által megkövetelt. |
| Aspose.Cells for Java (Maven artefakt `com.aspose:aspose-cells`) | Biztosítja a kódban használt `Workbook`, `Worksheet`, `Range` és kapcsolódó osztályokat. |
| Egy forrás Excel fájl (`src.xlsx`), amely pivot táblát, képet és AutoFilter-rel rendelkező táblázatot tartalmaz. | Az útmutató ezekkel az objektumokkal dolgozik, hogy bemutassa az egyes funkciókat. |

Adja hozzá a Maven függőséget a `pom.xml`-hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Tartomány másolása munkafüzetek között – forrás és cél betöltése

Az első lépés a forrás munkafüzet megnyitása, a másolni kívánt adatokat tartalmazó tartomány kiválasztása, és egy üres cél munkafüzet létrehozása.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Why this matters:** A `Range.copy` használatával az Aspose.Cells nem csak a nyers cellaértékeket másolja, hanem az alatta lévő pivot gyorsítótárat is, így a pivot tábla a cél munkafüzetben is működőképes marad.

---

## Pivot tábla munkafüzet másolása a tartomány másolása közben

Most másolja a meghatározott tartományt a forrás munkafüzetből a cél munkafüzetbe. A pivot tábla automatikusan megmarad, mivel a tartomány tartalmazza a pivot gyorsítótárat.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Result:** A `destination.xlsx` megnyitása ugyanazt a pivot tábla elrendezést mutatja, mint a `src.xlsx`. Nem szükséges további kód a pivot gyorsítótár újjáépítéséhez.

---

## Kép exportálása PowerPointba

Az Aspose.Cells megjelölhet egy képet, hogy exportálja szerkeszthető PowerPoint objektumként. A következő kód kiválasztja a cél munkalap első képét és beállítja az export jelzőt.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **What you see:** A `destination.pptx` PowerPointban történő megnyitása a képet natív alakzatként jeleníti meg, amelyet szerkeszthet, átméretezhet vagy animálhat.

---

## AutoFilter eltávolítása Excel táblázatból

Ha a forrás munkalap AutoFilter-rel rendelkező táblázatot tartalmaz, a másolás után érdemes törölni azt. Az alábbi kód hozzáfér az első táblázathoz és eltávolítja a szűrőt.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effect:** A táblázat a munkafüzetben marad, de a legördülő szűrő nyilak eltűnnek, így tiszta adatnézetet kap.

---

## Munkafüzet betöltése SmartMarker beállításokkal – JSON tömbök kezelése egyetlen cellaként

Amikor JSON-ból generál jelentést, az Aspose.Cells egy teljes tömböt egyetlen cellaértékként kezelhet. Ez hasznos, ha JSON karakterláncokat szeretne egy sablonba beágyazni anélkül, hogy több cellára bontaná őket.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Why you might use this:** Ha a JSON terhelés egy tömböt tartalmaz, amelyet egyetlen cellában JSON karakterláncként kell megjeleníteni, a `setArrayAsSingle(true)` megakadályozza, hogy az Aspose.Cells a tömböt külön sorokra vagy oszlopokra bontsa.

![Tartomány másolása munkafüzetek között Java-ban – Aspose.Cells kódpélda](copy-range-workbooks.png)

*Kép alternatív szöveg:* **Copy range between workbooks in Java – Aspose.Cells code example** (egyezik az elsődleges kulcsszóval).

---

## Várható kimenet

| Fájl neve                | Tartalma |
|--------------------------|----------|
| `destination.xlsx`       | Másolt tartomány működő pivot táblával. |
| `destination.pptx`       | Exportált kép szerkeszthető PowerPoint alakzatként. |
| `final_output.xlsx`      | Táblázat AutoFilter nyilak nélkül. |
| `template_filled.xlsx`   | JSON tömb egyetlen cellaértékként tárolva. |

Nyissa meg minden fájlt a megfelelő alkalmazásban (Excel vagy PowerPoint), hogy ellenőrizze, a műveletek sikeresek voltak-e.

---

## Következtetés

Most már tudja, hogyan **copy range between workbooks**-t hajtson végre Java-ban az Aspose.Cells használatával, miközben megőrzi a pivot táblát, exportál egy képet PowerPointba, és eltávolít egy AutoFilter-t egy Excel táblázatból. Ugyanez a minta kiterjeszthető bármely Excel tartomány új munkafüzetbe másolására, SmartMarker JSON tömbök kezelésére, vagy további átalakítások láncolására.

A következő lépések, amelyeket érdemes felfedezni:

* **Copy Excel range to new workbook** több munkalappal.  
* Használja a **export picture to PowerPoint**-t kötegelt képkinyeréshez.  
* Alkalmazza a **remove autofilter from excel table**-t nagyobb jelentéscsővezetékekben.  
* Kombinálja ezeket a technikákat az Aspose.Slides-szel a teljes Excel‑to‑PowerPoint automatizáláshoz.

Nyugodtan kísérletezzen különböző tartománycímekkel, több pivot táblával vagy egyedi képformátumokkal. Az Aspose.Cells API programozási rugalmasságra lett tervezve, így a bemutatott mintákat bármilyen vállalati Excel automatizálási forgatókönyvhöz testre szabhatja.

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Képek másolása munkalapok között Excelben az Aspose.Cells for Java használatával: Átfogó útmutató](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Oldalbeállítások másolása munkalapok között Excelben az Aspose.Cells Java használatával](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel munkalapok másolása munkafüzetek között](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}