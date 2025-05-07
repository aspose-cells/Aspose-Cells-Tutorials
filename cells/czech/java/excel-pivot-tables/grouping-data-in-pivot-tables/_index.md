---
"description": "Naučte se, jak vytvářet kontingenční tabulky v Excelu pomocí Aspose.Cells pro Javu. Automatizujte seskupování a analýzu dat pomocí příkladů zdrojového kódu."
"linktitle": "Seskupování dat v kontingenčních tabulkách"
"second_title": "Rozhraní API pro zpracování Excelu v Javě od Aspose.Cells"
"title": "Seskupování dat v kontingenčních tabulkách"
"url": "/cs/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Seskupování dat v kontingenčních tabulkách


Kontingenční tabulky jsou výkonným nástrojem pro analýzu a shrnování dat v tabulkách. Umožňují seskupovat a kategorizovat data a získávat tak cenné poznatky. V tomto článku se podíváme na to, jak efektivně seskupovat data v kontingenčních tabulkách pomocí Aspose.Cells pro Javu, a ukážeme si příklady zdrojového kódu.

## Zavedení

Kontingenční tabulky poskytují flexibilní způsob organizace a shrnutí dat z velkých datových sad. Umožňují vám vytvářet vlastní zobrazení dat seskupením do kategorií nebo hierarchií. To vám může pomoci snáze identifikovat trendy, vzory a odlehlé hodnoty v datech.

## Krok 1: Vytvořte kontingenční tabulku

Začněme vytvořením kontingenční tabulky pomocí Aspose.Cells pro Javu. Níže je uveden příklad, jak vytvořit kontingenční tabulku z ukázkového souboru aplikace Excel.

```java
// Načtěte soubor Excelu
Workbook workbook = new Workbook("sample.xlsx");

// Přístup k listu obsahujícímu data
Worksheet worksheet = workbook.getWorksheets().get(0);

// Zadejte rozsah dat
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Za předpokladu 20 řádků dat
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Za předpokladu 4 sloupců dat

// Vytvořte kontingenční tabulku na základě datového rozsahu
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Získání kontingenční tabulky podle indexu
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Přidání polí do řádků a sloupců
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Přidat hodnoty a použít agregaci
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Uložte upravený soubor aplikace Excel
workbook.save("output.xlsx");
```

## Krok 2: Seskupení dat

V Aspose.Cells pro Javu můžete seskupovat data v rámci kontingenční tabulky pomocí `PivotField` třída. Zde je příklad, jak seskupit pole v kontingenční tabulce:

```java
// Přístup k poli „Produkt“ v kontingenční tabulce
PivotField productField = pivotTable.getPivotFields().get("Product");

// Seskupte pole „Produkt“ podle určitého kritéria, např. podle počátečního písmene
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Uložte upravený soubor aplikace Excel se seskupenými daty
workbook.save("output_grouped.xlsx");
```

## Krok 3: Přizpůsobení seskupení

Nastavení seskupování si můžete dále přizpůsobit, například zadat intervaly seskupování podle data nebo vlastní pravidla seskupování. Zde je příklad přizpůsobení seskupování podle data:

```java
// Přístup k poli „Datum“ v kontingenční tabulce (za předpokladu, že se jedná o pole s datem)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Seskupit data podle měsíců
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Uložte upravený soubor aplikace Excel s vlastním seskupením dat
workbook.save("output_custom_grouping.xlsx");
```

## Závěr

Seskupování dat v kontingenčních tabulkách je cenná technika pro analýzu a shrnování dat v Excelu a Aspose.Cells pro Javu tento proces snadno automatizuje. S poskytnutými příklady zdrojového kódu můžete vytvářet kontingenční tabulky, přizpůsobovat seskupování a efektivně získávat přehled o svých datech.

## Často kladené otázky

### 1. K čemu slouží kontingenční tabulky v Excelu?

Kontingenční tabulky v Excelu se používají k shrnutí a analýze velkých datových sad. Umožňují vytvářet vlastní zobrazení dat, což usnadňuje identifikaci vzorců a trendů.

### 2. Jak mohu přizpůsobit seskupení dat v kontingenční tabulce?

Seskupení dat v kontingenční tabulce si můžete přizpůsobit pomocí `PivotField` třída v Aspose.Cells pro Javu. To umožňuje zadat kritéria seskupování, jako jsou intervaly založené na datu nebo vlastní pravidla.

### 3. Mohu automatizovat vytváření pivotních tabulek pomocí Aspose.Cells pro Javu?

Ano, vytváření kontingenčních tabulek v Excelu můžete automatizovat pomocí Aspose.Cells pro Javu, jak je ukázáno v uvedených příkladech zdrojového kódu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}