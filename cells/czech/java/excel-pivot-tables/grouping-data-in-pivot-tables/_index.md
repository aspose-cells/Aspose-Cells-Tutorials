---
title: Seskupování dat v kontingenčních tabulkách
linktitle: Seskupování dat v kontingenčních tabulkách
second_title: Aspose.Cells Java Excel Processing API
description: Naučte se vytvářet kontingenční tabulky v Excelu pomocí Aspose.Cells for Java. Automatizujte seskupování a analýzu dat pomocí příkladů zdrojového kódu.
weight: 14
url: /cs/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Seskupování dat v kontingenčních tabulkách


Kontingenční tabulky jsou mocným nástrojem pro analýzu a sumarizaci dat v tabulkách. Umožňují vám seskupovat a kategorizovat data, abyste získali cenné poznatky. V tomto článku prozkoumáme, jak efektivně seskupovat data v kontingenčních tabulkách pomocí Aspose.Cells for Java, spolu s příklady zdrojového kódu.

## Zavedení

Kontingenční tabulky poskytují flexibilní způsob, jak organizovat a sumarizovat data z velkých datových sad. Umožňují vám vytvářet vlastní pohledy na vaše data jejich seskupováním do kategorií nebo hierarchií. To vám může pomoci snáze identifikovat trendy, vzory a odlehlé hodnoty ve vašich datech.

## Krok 1: Vytvořte kontingenční tabulku

Začněme vytvořením kontingenční tabulky pomocí Aspose.Cells for Java. Níže je uveden příklad, jak vytvořit kontingenční tabulku z ukázkového souboru aplikace Excel.

```java
// Načtěte soubor Excel
Workbook workbook = new Workbook("sample.xlsx");

// Vstupte do listu obsahujícího data
Worksheet worksheet = workbook.getWorksheets().get(0);

// Zadejte rozsah dat
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Předpokládejme 20 řádků dat
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Předpokládejme 4 sloupce dat

// Vytvořte kontingenční tabulku na základě rozsahu dat
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Získejte kontingenční tabulku podle indexu
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Přidejte pole do řádků a sloupců
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Přidejte hodnoty a použijte agregaci
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Uložte upravený soubor aplikace Excel
workbook.save("output.xlsx");
```

## Krok 2: Seskupení dat

 V Aspose.Cells for Java můžete seskupit data v rámci kontingenční tabulky pomocí`PivotField` třída. Zde je příklad, jak seskupit pole v kontingenční tabulce:

```java
// Otevřete pole „Produkt“ v kontingenční tabulce
PivotField productField = pivotTable.getPivotFields().get("Product");

//Seskupte pole "Produkt" podle konkrétního kritéria, např. podle počátečního písmene
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Uložte upravený soubor Excel se seskupenými daty
workbook.save("output_grouped.xlsx");
```

## Krok 3: Přizpůsobte seskupování

Nastavení seskupování můžete dále upravit, například zadat intervaly seskupování na základě data nebo vlastní pravidla seskupování. Zde je příklad přizpůsobení seskupování podle data:

```java
// Přístup k poli "Datum" v kontingenční tabulce (za předpokladu, že se jedná o pole data)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Seskupte data podle měsíců
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Uložte upravený soubor Excel s vlastním seskupením podle data
workbook.save("output_custom_grouping.xlsx");
```

## Závěr

Seskupování dat v kontingenčních tabulkách je cenná technika pro analýzu a sumarizaci dat v Excelu a Aspose.Cells for Java usnadňuje automatizaci tohoto procesu. S poskytnutými příklady zdrojového kódu můžete vytvářet kontingenční tabulky, přizpůsobovat seskupování a efektivně získávat přehledy z vašich dat.

## Nejčastější dotazy

### 1. K čemu slouží kontingenční tabulky v Excelu?

Kontingenční tabulky v Excelu se používají k shrnutí a analýze velkých datových sad. Umožňují vám vytvářet vlastní pohledy na vaše data, což usnadňuje identifikaci vzorců a trendů.

### 2. Jak mohu přizpůsobit seskupování dat v kontingenční tabulce?

 Seskupení dat v kontingenční tabulce můžete přizpůsobit pomocí`PivotField` třídy v Aspose.Cells for Java. To vám umožní určit kritéria seskupení, jako jsou intervaly založené na datu nebo vlastní pravidla.

### 3. Mohu automatizovat vytváření kontingenčních tabulek pomocí Aspose.Cells for Java?

Ano, můžete automatizovat vytváření kontingenčních tabulek v Excelu pomocí Aspose.Cells for Java, jak je ukázáno v poskytnutých příkladech zdrojového kódu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
