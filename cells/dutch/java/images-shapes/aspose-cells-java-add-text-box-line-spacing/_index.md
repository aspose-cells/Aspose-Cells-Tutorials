---
"date": "2025-04-08"
"description": "Leer hoe u Aspose.Cells voor Java gebruikt om tekstvakken toe te voegen en de regelafstand in Excel-werkmappen in te stellen. Verbeter uw werkmappresentaties met gestileerde tekstvormen."
"title": "Tekstvak toevoegen en regelafstand instellen in Excel met Aspose.Cells voor Java"
"url": "/nl/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Een tekstvak toevoegen en regelafstand instellen in Excel met Aspose.Cells voor Java

## Invoering

Het maken van dynamische Excel-rapporten vereist vaak aangepaste tekstopmaak, zoals het toevoegen van tekstvakken met een specifieke regelafstand. Met Aspose.Cells voor Java wordt dit eenvoudig en efficiënt. Deze tutorial begeleidt u bij het verbeteren van uw werkmappresentaties met Aspose.Cells voor Java om gestileerde tekstvormen toe te voegen.

Aan het einde van deze handleiding leert u het volgende:
- Een nieuwe Excel-werkmap maken en toegang krijgen tot de werkbladen
- Een tekstvakvorm toevoegen aan een werkblad
- Aangepaste regelafstand instellen in een tekstvorm
- Sla uw opgemaakte werkmap op in XLSX-formaat

Laten we beginnen met het instellen van uw omgeving.

### Vereisten

Voordat u begint, moet u ervoor zorgen dat u het volgende heeft:
- Java Development Kit (JDK) geïnstalleerd op uw machine
- Een IDE of editor voor het schrijven van Java-code
- Maven- of Gradle-bouwsysteem geconfigureerd om afhankelijkheden te beheren

Een basiskennis van Java-programmering en vertrouwdheid met Excel-bestandsstructuren zijn nuttig.

## Aspose.Cells instellen voor Java

Neem Aspose.Cells op in het afhankelijkheidsbeheer van uw project met behulp van Maven of Gradle:

**Maven**

Voeg het volgende afhankelijkheidsblok toe aan uw `pom.xml` bestand:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Neem dit op in uw `build.gradle` bestand:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Schaf vervolgens een licentie voor Aspose.Cells aan door te kiezen voor een gratis proefversie, een tijdelijke licentie aan te vragen of een volledige licentie aan te schaffen.

### Aspose.Cells initialiseren

Zodra de bibliotheek in uw project is opgenomen, initialiseert u deze in uw Java-toepassing:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Initialiseer een exemplaar van Werkmap (vertegenwoordigt een Excel-bestand)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Implementatiegids

### Een werkmap en Access-werkblad maken

Begin met het maken van een nieuwe Excel-werkmap en open het eerste werkblad. Hier voegt u uw tekstvak toe.

#### Overzicht

Wanneer u een nieuwe werkmap maakt, hebt u een lege pagina om naar behoefte gegevens, vormen en opmaak toe te voegen.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Tekstvak toevoegen aan werkblad

Voeg vervolgens een tekstvakvorm toe aan het geselecteerde werkblad. Deze vorm kan elke gewenste tekstinhoud bevatten.

#### Overzicht

Tekstvakken zijn veelzijdige hulpmiddelen waarmee u aangepaste teksten, zoals notities of instructies, rechtstreeks in een Excel-werkblad kunt opnemen.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Een tekstvakvorm toevoegen aan het werkblad
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Tekst in vorm zetten

Zodra uw tekstvak klaar is, kunt u de inhoud ervan bepalen en de tekst erin opmaken.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Een tekstvakvorm toevoegen aan het werkblad
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Tekstinhoud in de vorm instellen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Toegang tot tekstparagrafen in vorm

U kunt toegang krijgen tot afzonderlijke alinea's binnen een tekstvak om specifieke opmaak toe te passen.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Een tekstvakvorm toevoegen aan het werkblad
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Tekstinhoud in de vorm instellen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Toegang tot de tweede alinea in de vorm
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Regelafstand van alinea instellen

Het aanpassen van de regelafstand kan de leesbaarheid verbeteren. Zo stelt u het in:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Een tekstvakvorm toevoegen aan het werkblad
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Tekstinhoud in de vorm instellen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Toegang tot de tweede alinea in de vorm
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Stel de regelafstand in op 20 punten
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Ruimte voor en na de alinea configureren
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Werkboek opslaan

Sla ten slotte uw werkmap op met het nieuw toegevoegde en opgemaakte tekstvak.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Een nieuwe werkmap maken (Excel-bestand)
        Workbook workbook = new Workbook();
        
        // Toegang tot het eerste werkblad
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Een tekstvakvorm toevoegen aan het werkblad
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Tekstinhoud in de vorm instellen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Toegang tot de tweede alinea in de vorm
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Stel de regelafstand in op 20 punten
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Ruimte voor en na de alinea configureren
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Sla de werkmap op
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusie

Je hebt met succes geleerd hoe je een tekstvak toevoegt en de regelafstand instelt in een Excel-werkmap met Aspose.Cells voor Java. Dit verbetert je vermogen om dynamische, visueel aantrekkelijke rapporten te maken.

## Aanbevelingen voor trefwoorden
- "Aspose.Cells voor Java"
- "Tekstvak toevoegen in Excel"
- "Regelafstand instellen in Excel"
- "Excel-werkmap met opgemaakte tekst"
- "Java en Aspose.Cellen"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}