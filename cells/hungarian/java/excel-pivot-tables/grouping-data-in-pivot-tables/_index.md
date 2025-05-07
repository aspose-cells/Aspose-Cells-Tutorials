---
"description": "Tanulja meg, hogyan hozhat létre pivot táblákat Excelben az Aspose.Cells for Java használatával. Automatizálja az adatcsoportosítást és -elemzést forráskódpéldákkal."
"linktitle": "Adatok csoportosítása kimutatástáblákban"
"second_title": "Aspose.Cells Java Excel feldolgozási API"
"title": "Adatok csoportosítása kimutatástáblákban"
"url": "/hu/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adatok csoportosítása kimutatástáblákban


A pivot táblázatok hatékony eszközök az adatok táblázatokban történő elemzéséhez és összegzéséhez. Lehetővé teszik az adatok csoportosítását és kategorizálását, hogy értékes információkat nyerjen. Ebben a cikkben azt vizsgáljuk meg, hogyan csoportosíthatja hatékonyan az adatokat a pivot táblázatokban az Aspose.Cells for Java használatával, forráskódpéldákkal együtt.

## Bevezetés

A pivot táblázatok rugalmas módot kínálnak a nagy adathalmazokból származó adatok rendszerezésére és összefoglalására. Lehetővé teszik az adatok egyéni nézeteinek létrehozását kategóriákba vagy hierarchiákba csoportosításával. Ez segíthet az adatok trendjeinek, mintázatainak és kiugró értékeinek könnyebb azonosításában.

## 1. lépés: Pivottábla létrehozása

Kezdjük egy pivot tábla létrehozásával az Aspose.Cells for Java használatával. Az alábbiakban egy példa látható arra, hogyan hozhat létre pivot táblát egy Excel mintafájlból.

```java
// Töltsd be az Excel fájlt
Workbook workbook = new Workbook("sample.xlsx");

// Hozzáférés az adatokat tartalmazó munkalaphoz
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adja meg az adattartományt
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // 20 sornyi adatot feltételezve
sourceData.startColumn = 0;
sourceData.endColumn = 3; // 4 oszlopnyi adatot feltételezve

// Hozz létre egy pivot táblát az adattartomány alapján
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Pivot tábla beolvasása index alapján
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Mezők hozzáadása sorokhoz és oszlopokhoz
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Értékek hozzáadása és összesítés alkalmazása
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Mentse el a módosított Excel fájlt
workbook.save("output.xlsx");
```

## 2. lépés: Adatok csoportosítása

Az Aspose.Cells for Java programban a pivot táblázaton belüli adatokat a következővel csoportosíthatja: `PivotField` osztály. Íme egy példa arra, hogyan csoportosíthat egy mezőt a pivot táblázatban:

```java
// Hozzáférés a „Termék” mezőhöz a pivot táblázatban
PivotField productField = pivotTable.getPivotFields().get("Product");

// Csoportosítsa a „Termék” mezőt egy adott kritérium szerint, pl. kezdőbetű szerint
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Mentse el a módosított Excel fájlt csoportosított adatokkal
workbook.save("output_grouped.xlsx");
```

## 3. lépés: Csoportosítás testreszabása

csoportosítási beállításokat tovább testreszabhatja, például dátumalapú csoportosítási intervallumokat vagy egyéni csoportosítási szabályokat adhat meg. Íme egy példa a dátumalapú csoportosítás testreszabására:

```java
// Nyissa meg a „Dátum” mezőt a pivot táblában (feltételezve, hogy dátummezőről van szó)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Dátumok csoportosítása hónapok szerint
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Mentse el a módosított Excel-fájlt egyéni dátumcsoportosítással
workbook.save("output_custom_grouping.xlsx");
```

## Következtetés

Az adatok csoportosítása pivot táblázatokban értékes technika az adatok Excelben történő elemzéséhez és összegzéséhez, és az Aspose.Cells for Java megkönnyíti ennek a folyamatnak az automatizálását. A megadott forráskódpéldákkal pivot táblázatokat hozhat létre, testreszabhatja a csoportosítást, és hatékonyan nyerhet elemzéseket az adataiból.

## GYIK

### 1. Mi a célja a pivot tábláknak az Excelben?

Az Excelben a pivot táblázatok nagy adathalmazok összefoglalására és elemzésére szolgálnak. Lehetővé teszik az adatok egyéni nézeteinek létrehozását, így könnyebben azonosíthatók a minták és trendek.

### 2. Hogyan szabhatom testre az adatok csoportosítását egy kimutatástáblázatban?

kimutatástáblázatban lévő adatok csoportosítását testreszabhatja a `PivotField` osztály az Aspose.Cells programban Java-ban. Ez lehetővé teszi csoportosítási feltételek megadását, például dátumalapú intervallumokat vagy egyéni szabályokat.

### 3. Automatizálhatom a pivot táblák létrehozását az Aspose.Cells for Java használatával?

Igen, automatizálhatja a pivot táblák létrehozását Excelben az Aspose.Cells for Java használatával, ahogy azt a megadott forráskód példák is mutatják.
{{< /blokkok/termékek/pf/oktatóanyag-oldal-szakasz >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}