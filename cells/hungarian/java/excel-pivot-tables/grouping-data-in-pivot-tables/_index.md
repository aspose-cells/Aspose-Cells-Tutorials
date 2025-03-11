---
title: Adatok csoportosítása kimutatástáblákban
linktitle: Adatok csoportosítása kimutatástáblákban
second_title: Aspose.Cells Java Excel Processing API
description: Ismerje meg, hogyan hozhat létre pivot táblákat az Excelben az Aspose.Cells for Java használatával. Automatizálja az adatok csoportosítását és elemzését forráskód-példákkal.
weight: 14
url: /hu/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adatok csoportosítása kimutatástáblákban


A kimutatástáblák hatékony eszközt jelentenek az adatok táblázatokban történő elemzéséhez és összegzéséhez. Lehetővé teszik az adatok csoportosítását és kategorizálását, hogy értékes betekintést nyerhessenek. Ebben a cikkben bemutatjuk, hogyan lehet hatékonyan csoportosítani az adatokat pivot táblákban az Aspose.Cells for Java segítségével, valamint forráskód-példákat.

## Bevezetés

kimutatástáblák rugalmas módot kínálnak a nagy adatkészletekből származó adatok rendszerezésére és összegzésére. Lehetővé teszik az adatok egyéni nézeteinek létrehozását kategóriákba vagy hierarchiákba csoportosítva. Ezzel könnyebben azonosíthatja a trendeket, mintákat és kiugró értékeket az adatokban.

## 1. lépés: Hozzon létre egy kimutatástáblát

Kezdjük egy pivot tábla létrehozásával az Aspose.Cells for Java használatával. Az alábbiakban bemutatunk egy példát arra, hogyan hozhatunk létre kimutatási táblázatot egy minta Excel-fájlból.

```java
// Töltse be az Excel fájlt
Workbook workbook = new Workbook("sample.xlsx");

// Nyissa meg az adatokat tartalmazó munkalapot
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adja meg az adattartományt
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // 20 sornyi adatot feltételezve
sourceData.startColumn = 0;
sourceData.endColumn = 3; // 4 oszlopos adatot feltételezve

// Hozzon létre egy kimutatási táblát az adattartomány alapján
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Szerezze le a pivot táblát index szerint
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Mezők hozzáadása sorokhoz és oszlopokhoz
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Adjon hozzá értékeket és alkalmazza az összesítést
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Mentse el a módosított Excel fájlt
workbook.save("output.xlsx");
```

## 2. lépés: Csoportosítsa az adatokat

 Az Aspose.Cells for Java programban a pivot táblán belül csoportosíthatja az adatokat a segítségével`PivotField` osztály. Íme egy példa egy mező csoportosítására a kimutatástáblában:

```java
// Nyissa meg a „Termék” mezőt a kimutatásban
PivotField productField = pivotTable.getPivotFields().get("Product");

//Csoportosítsa a "Termék" mezőt egy adott kritérium szerint, pl. kezdőbetű szerint
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Mentse el a módosított Excel-fájlt csoportosított adatokkal
workbook.save("output_grouped.xlsx");
```

## 3. lépés: A csoportosítás testreszabása

Tovább szabhatja a csoportosítási beállításokat, például megadhatja a dátum alapú csoportosítási időközöket vagy egyéni csoportosítási szabályokat. Íme egy példa a dátum alapú csoportosítás testreszabására:

```java
// Hozzáférés a "Dátum" mezőhöz a kimutatásban (feltételezve, hogy ez egy dátum mező)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Csoportosítsa a dátumokat hónapok szerint
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Mentse el a módosított Excel-fájlt egyéni dátumcsoportosítással
workbook.save("output_custom_grouping.xlsx");
```

## Következtetés

Az adatok pivot táblákban történő csoportosítása értékes technika az adatok Excelben történő elemzéséhez és összegzéséhez, az Aspose.Cells for Java pedig megkönnyíti ennek a folyamatnak az automatizálását. A mellékelt forráskód-példákkal pivot táblákat hozhat létre, testreszabhatja a csoportosítást, és hatékonyan nyerhet betekintést az adatokból.

## GYIK

### 1. Mi a célja a pivot tábláknak az Excelben?

Az Excel kimutatásai nagy adatkészletek összegzésére és elemzésére szolgálnak. Lehetővé teszik az adatok egyéni nézeteinek létrehozását, megkönnyítve a minták és trendek azonosítását.

### 2. Hogyan szabhatom testre az adatok csoportosítását egy pivot táblában?

 Testreszabhatja az adatok csoportosítását egy pivot táblában a segítségével`PivotField` osztály az Aspose.Cells for Java-ban. Ez lehetővé teszi csoportosítási feltételek megadását, például dátumalapú intervallumokat vagy egyéni szabályokat.

### 3. Automatizálhatom a pivot táblák létrehozását az Aspose.Cells for Java használatával?

Igen, automatizálhatja a pivot táblák létrehozását az Excelben az Aspose.Cells for Java használatával, amint azt a forráskód példái bemutatják.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
