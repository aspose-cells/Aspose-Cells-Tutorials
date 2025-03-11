---
title: Gegevens groeperen in draaitabellen
linktitle: Gegevens groeperen in draaitabellen
second_title: Aspose.Cells Java Excel-verwerkings-API
description: Leer hoe u draaitabellen in Excel maakt met Aspose.Cells voor Java. Automatiseer gegevensgroepering en -analyse met broncodevoorbeelden.
weight: 14
url: /nl/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gegevens groeperen in draaitabellen


Draaitabellen zijn een krachtig hulpmiddel voor het analyseren en samenvatten van gegevens in spreadsheets. Ze stellen u in staat om gegevens te groeperen en categoriseren om waardevolle inzichten te verkrijgen. In dit artikel onderzoeken we hoe u gegevens effectief kunt groeperen in draaitabellen met behulp van Aspose.Cells voor Java, samen met broncodevoorbeelden.

## Invoering

Draaitabellen bieden een flexibele manier om gegevens uit grote datasets te ordenen en samen te vatten. Ze stellen u in staat om aangepaste weergaven van uw gegevens te maken door deze te groeperen in categorieën of hiërarchieën. Dit kan u helpen trends, patronen en uitschieters in uw gegevens gemakkelijker te identificeren.

## Stap 1: Een draaitabel maken

Laten we beginnen met het maken van een draaitabel met Aspose.Cells voor Java. Hieronder ziet u een voorbeeld van hoe u een draaitabel maakt vanuit een voorbeeld-Excel-bestand.

```java
// Laad het Excel-bestand
Workbook workbook = new Workbook("sample.xlsx");

// Toegang tot het werkblad met de gegevens
Worksheet worksheet = workbook.getWorksheets().get(0);

// Geef het gegevensbereik op
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Uitgaande van 20 rijen met gegevens
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Uitgaande van 4 kolommen met gegevens

// Maak een draaitabel op basis van het gegevensbereik
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Haal de draaitabel op index op
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Velden toevoegen aan rijen en kolommen
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Waarden toevoegen en aggregatie toepassen
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Sla het gewijzigde Excel-bestand op
workbook.save("output.xlsx");
```

## Stap 2: Groepsgegevens

 In Aspose.Cells voor Java kunt u gegevens binnen de draaitabel groeperen met behulp van de`PivotField` klasse. Hier is een voorbeeld van hoe u een veld in de draaitabel kunt groeperen:

```java
// Toegang tot het veld 'Product' in de draaitabel
PivotField productField = pivotTable.getPivotFields().get("Product");

//Groepeer het veld 'Product' op basis van een specifiek criterium, bijvoorbeeld op basis van de beginletter
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Sla het gewijzigde Excel-bestand op met gegroepeerde gegevens
workbook.save("output_grouped.xlsx");
```

## Stap 3: Groepering aanpassen

U kunt de groeperingsinstellingen verder aanpassen, zoals het opgeven van op datum gebaseerde groeperingsintervallen of aangepaste groeperingsregels. Hier is een voorbeeld van het aanpassen van op datum gebaseerde groepering:

```java
// Toegang tot het veld 'Datum' in de draaitabel (ervan uitgaande dat het een datumveld is)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Groepeer data per maand
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Sla het gewijzigde Excel-bestand op met aangepaste datumgroepering
workbook.save("output_custom_grouping.xlsx");
```

## Conclusie

Gegevens groeperen in draaitabellen is een waardevolle techniek voor het analyseren en samenvatten van gegevens in Excel, en Aspose.Cells voor Java maakt het eenvoudig om dit proces te automatiseren. Met de meegeleverde broncodevoorbeelden kunt u draaitabellen maken, groeperingen aanpassen en efficiënt inzicht krijgen in uw gegevens.

## Veelgestelde vragen

### 1. Wat is het doel van draaitabellen in Excel?

Draaitabellen in Excel worden gebruikt om grote datasets samen te vatten en te analyseren. Ze stellen u in staat om aangepaste weergaven van uw gegevens te maken, waardoor het gemakkelijker wordt om patronen en trends te identificeren.

### 2. Hoe kan ik de groepering van gegevens in een draaitabel aanpassen?

 U kunt de groepering van gegevens in een draaitabel aanpassen met behulp van de`PivotField` klasse in Aspose.Cells voor Java. Hiermee kunt u groeperingscriteria opgeven, zoals op datum gebaseerde intervallen of aangepaste regels.

### 3. Kan ik het maken van draaitabellen automatiseren met Aspose.Cells voor Java?

Ja, u kunt het maken van draaitabellen in Excel automatiseren met Aspose.Cells voor Java, zoals wordt gedemonstreerd in de meegeleverde broncodevoorbeelden.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
