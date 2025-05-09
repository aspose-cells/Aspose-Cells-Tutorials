---
"date": "2025-04-08"
"description": "Leer hoe je cirkeldiagrammen maakt en aanpast met Aspose.Cells voor Java. Een stapsgewijze handleiding met codevoorbeelden voor ontwikkelaars."
"title": "Aspose.Cells onder de knie krijgen&#58; cirkeldiagrammen maken en aanpassen in Java"
"url": "/nl/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells onder de knie krijgen: cirkeldiagrammen maken en aanpassen in Java

## Invoering
Het maken van visueel aantrekkelijke grafieken is een veelvoorkomende vereiste bij datavisualisatie in Excel. Of u nu demografische informatie presenteert of markttrends analyseert, cirkeldiagrammen bieden een duidelijke manier om proportionele gegevens weer te geven. Het programmatisch opzetten van deze diagrammen kan echter complex zijn. Deze tutorial begeleidt u bij het maken en aanpassen van een Aspose.Cells-cirkeldiagram met behulp van Java, wat het proces voor ontwikkelaars vereenvoudigt.

**Wat je leert:**
- Stel uw omgeving in met Aspose.Cells voor Java.
- Maak een nieuwe werkmap en open de cellen in het werkblad.
- Vul gegevens in specifieke cellen in ter voorbereiding op het maken van de grafiek.
- Genereer een cirkeldiagram op basis van deze gegevens.
- Pas het uiterlijk van uw cirkeldiagram aan, inclusief kleuren, titels en legenda.

Voordat je aan de slag gaat, zorg ervoor dat je basiskennis hebt van Java-programmering en Maven- of Gradle-afhankelijkheidsbeheer. Laten we onze omgeving opzetten!

## Vereisten
Om deze tutorial te kunnen volgen, heb je het volgende nodig:
- **Java-ontwikkelingskit (JDK)**: Versie 8 of hoger.
- **Geïntegreerde ontwikkelomgeving (IDE)**: Zoals IntelliJ IDEA of Eclipse.
- **Afhankelijkheidsbeheer**: Gebruik Maven of Gradle om uw afhankelijkheden te beheren.

### Vereiste bibliotheken en afhankelijkheden
Zorg ervoor dat u Aspose.Cells voor Java in uw project opneemt via Maven of Gradle.

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

### Stappen voor het verkrijgen van een licentie
Aspose.Cells voor Java is een commerciële bibliotheek, maar u kunt beginnen met een gratis proefperiode of een tijdelijke licentie aanvragen. Bezoek de [aankooppagina](https://purchase.aspose.com/buy) om licentieopties te verkennen.

## Aspose.Cells instellen voor Java
Zorg er allereerst voor dat uw projectomgeving de benodigde bibliotheken bevat door ze toe te voegen via Maven of Gradle, zoals hierboven weergegeven. Zodra u ze hebt toegevoegd, kunt u Aspose.Cells initialiseren:

```java
import com.aspose.cells.Workbook;

// Een nieuw werkmapexemplaar initialiseren
Workbook workbook = new Workbook();
```

## Implementatiegids

### Een werkmap maken en configureren
Het maken van een werkmap is de eerste stap waarin u uw gegevens indeelt.

#### Bibliotheken importeren
Zorg ervoor dat deze imports bovenaan uw bestand staan:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Stap 1: Een werkboekinstantie maken
```java
// Maakt een lege werkmapinstantie om mee te werken.
Workbook workbook = new Workbook();
```
Met deze stap initialiseert u uw Excel-bestand programmatisch, zodat u het kunt bewerken met de Aspose.Cells-functionaliteit.

### Werkbladcellen openen of wijzigen
Vul vervolgens de gegevens in de cellen van het werkblad in die u voor het cirkeldiagram wilt gebruiken.

#### Stap 2: Toegang tot een werkblad en de cellen ervan
```java
// Open het eerste werkblad in de werkmap.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Plaats voorbeeldwaarden die u voor een cirkeldiagram gebruikt, in specifieke cellen.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Plaats percentagewaarden voor een cirkeldiagram in specifieke cellen.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Hier vult u het werkblad met gegevens die de verschillende segmenten van een cirkeldiagram vertegenwoordigen.

### Maak een cirkeldiagram

#### Stap 3: Voeg een cirkeldiagram toe aan het werkblad
```java
// Maak een cirkeldiagram in het werkblad.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Met deze stap voegt u een nieuw cirkeldiagram toe aan uw werkblad op de opgegeven posities en afmetingen.

### Cirkeldiagramreeksen en gegevens configureren

#### Stap 4: Stel de serie voor de grafiek in
```java
// Configureer het reeksgegevensbereik voor de grafiek.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Koppel de titel van het cirkeldiagram aan een cel die de titeltekst bevat.
pie.getTitle().setLinkedSource("D2");
```
Deze code koppelt uw gegevensbereik en stelt de reeks voor het cirkeldiagram in.

### Legenda en titelweergave van grafiek configureren

#### Stap 5: Pas de legenda en titel van het diagram aan
```java
// Plaats de legenda onderaan de grafiek.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Stel lettertype-eigenschappen in voor de grafiektitel.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Door het uiterlijk aan te passen, verbetert u de leesbaarheid en visuele aantrekkingskracht.

### Pas de kleuren van de grafiekreeks aan

#### Stap 6: Wijzig de kleuren van de cirkelsegmenten
```java
import com.aspose.cells.Color;

// U kunt de kleuren van afzonderlijke cirkeldiagramsegmenten openen en aanpassen.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Met deze instellingen kunt u uw grafiek personaliseren, zodat deze past bij specifieke kleurenschema's.

### Kolommen automatisch aanpassen en werkmap opslaan

#### Stap 7: Kolombreedtes aanpassen en het bestand opslaan
```java
// Alle kolommen automatisch aanpassen.
worksheet.autoFitColumns();

// Definieer het tijdelijke pad naar de uitvoermap voor het opslaan van de werkmap.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Sla de gewijzigde werkmap op in een Excel-bestand in de opgegeven map.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Pas ten slotte de kolommen automatisch aan en sla uw werkmap op.

## Praktische toepassingen
1. **Demografische analyse**:Gebruik cirkeldiagrammen om de bevolkingsverdeling over verschillende landen of regio's weer te geven.
2. **Marktaandeelrapporten**: Illustreer het marktaandeel van verschillende bedrijven in een sector.
3. **Budgettoewijzing**:Visualiseer hoe budgetten worden verdeeld over verschillende afdelingen binnen een organisatie.

Deze toepassingen demonstreren de veelzijdigheid en bruikbaarheid van Aspose.Cells in realistische scenario's.

## Prestatieoverwegingen
Om de prestaties te optimaliseren bij het gebruik van Aspose.Cells:
- Minimaliseer het geheugengebruik door objecten die u niet meer nodig hebt, te verwijderen.
- Gebruik efficiënte datastructuren voor de verwerking van grote datasets.
- Maak een profiel van uw applicatie om knelpunten te identificeren.

Door best practices te volgen, zorgen we ervoor dat applicaties soepel en responsief werken.

## Conclusie
Deze tutorial leidde je door de stappen voor het maken en aanpassen van een cirkeldiagram met Aspose.Cells in Java. Met deze kennis kun je deze technieken nu toepassen op diverse datavisualisatietaken in je projecten. Voor verdere verdieping kun je je verdiepen in de extra grafiektypen en geavanceerde aanpassingsopties die beschikbaar zijn met Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}