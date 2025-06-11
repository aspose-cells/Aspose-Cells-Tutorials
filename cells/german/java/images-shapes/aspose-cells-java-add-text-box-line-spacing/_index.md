---
"date": "2025-04-08"
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für Java Textfelder hinzufügen und Zeilenabstände in Excel-Arbeitsmappen festlegen. Optimieren Sie Ihre Arbeitsmappenpräsentationen mit formatierten Textformen."
"title": "Textfeld hinzufügen und Zeilenabstand in Excel festlegen mit Aspose.Cells für Java"
"url": "/de/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Fügen Sie mit Aspose.Cells für Java ein Textfeld hinzu und legen Sie den Zeilenabstand in Excel fest

## Einführung

Das Erstellen dynamischer Excel-Berichte erfordert oft eine individuelle Textformatierung, beispielsweise das Hinzufügen von Textfeldern mit spezifischem Zeilenabstand. Mit Aspose.Cells für Java wird dies einfach und effizient. Dieses Tutorial führt Sie durch die Verbesserung Ihrer Arbeitsmappenpräsentationen mit Aspose.Cells für Java, um formatierte Textformen hinzuzufügen.

Am Ende dieses Handbuchs erfahren Sie, wie Sie:
- Erstellen Sie eine neue Excel-Arbeitsmappe und greifen Sie auf deren Arbeitsblätter zu
- Hinzufügen einer Textfeldform zu einem Arbeitsblatt
- Benutzerdefinierten Zeilenabstand innerhalb einer Textform festlegen
- Speichern Sie Ihre formatierte Arbeitsmappe im XLSX-Format

Beginnen wir mit der Einrichtung Ihrer Umgebung.

### Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
- Java Development Kit (JDK) auf Ihrem Computer installiert
- Eine IDE oder ein Editor zum Schreiben von Java-Code
- Maven- oder Gradle-Build-System, konfiguriert zur Verwaltung von Abhängigkeiten

Grundkenntnisse in der Java-Programmierung und Vertrautheit mit Excel-Dateistrukturen sind von Vorteil.

## Einrichten von Aspose.Cells für Java

Integrieren Sie Aspose.Cells mithilfe von Maven oder Gradle in die Abhängigkeitsverwaltung Ihres Projekts:

**Maven**

Fügen Sie den folgenden Abhängigkeitsblock zu Ihrem `pom.xml` Datei:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Nehmen Sie dies in Ihre `build.gradle` Datei:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Erwerben Sie als Nächstes eine Lizenz für Aspose.Cells, indem Sie sich für eine kostenlose Testversion entscheiden, eine temporäre Lizenz anfordern oder eine Volllizenz erwerben.

### Initialisieren von Aspose.Cells

Sobald die Bibliothek in Ihr Projekt eingebunden ist, initialisieren Sie sie in Ihrer Java-Anwendung:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Initialisieren Sie eine Instanz von Workbook (stellt eine Excel-Datei dar)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Implementierungshandbuch

### Erstellen einer Arbeitsmappe und eines Access-Arbeitsblatts

Erstellen Sie zunächst eine neue Excel-Arbeitsmappe und öffnen Sie das erste Arbeitsblatt. Fügen Sie dort Ihr Textfeld ein.

#### Überblick

Durch das Erstellen einer neuen Arbeitsmappe wird eine leere Tafel bereitgestellt, in die Sie nach Bedarf Daten, Formen und Formatierungen einfügen können.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Textfeld zum Arbeitsblatt hinzufügen

Fügen Sie anschließend Ihrem ausgewählten Arbeitsblatt eine Textfeldform hinzu. Diese Form kann beliebige Textinhalte enthalten.

#### Überblick

Textfelder sind vielseitige Tools zum Einfügen von benutzerdefinierten Texten wie Notizen oder Anweisungen direkt in ein Excel-Blatt.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Fügen Sie dem Arbeitsblatt eine Textfeldform hinzu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Text in Form setzen

Sobald Ihr Textfeld fertig ist, legen Sie seinen Inhalt fest und formatieren Sie den darin enthaltenen Text.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Fügen Sie dem Arbeitsblatt eine Textfeldform hinzu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Textinhalt innerhalb der Form festlegen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Zugriff auf Textabsätze in Shape

Sie können auf einzelne Absätze innerhalb eines Textfelds zugreifen, um eine bestimmte Formatierung anzuwenden.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Fügen Sie dem Arbeitsblatt eine Textfeldform hinzu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Textinhalt innerhalb der Form festlegen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Greifen Sie auf den zweiten Absatz in der Form zu
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Zeilenabstand des Absatzes festlegen

Durch Anpassen des Zeilenabstands können Sie die Lesbarkeit verbessern. So legen Sie ihn fest:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Fügen Sie dem Arbeitsblatt eine Textfeldform hinzu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Textinhalt innerhalb der Form festlegen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Greifen Sie auf den zweiten Absatz in der Form zu
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Stellen Sie den Zeilenabstand auf 20 Punkte ein
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurieren Sie den Abstand vor und nach dem Absatz
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Arbeitsmappe speichern

Speichern Sie abschließend Ihre Arbeitsmappe mit dem neu hinzugefügten und formatierten Textfeld.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Erstellen Sie eine neue Arbeitsmappe (Excel-Datei)
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt zu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Fügen Sie dem Arbeitsblatt eine Textfeldform hinzu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Textinhalt innerhalb der Form festlegen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Greifen Sie auf den zweiten Absatz in der Form zu
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Stellen Sie den Zeilenabstand auf 20 Punkte ein
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurieren Sie den Abstand vor und nach dem Absatz
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Speichern der Arbeitsmappe
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Abschluss

Sie haben erfolgreich gelernt, wie Sie mit Aspose.Cells für Java ein Textfeld hinzufügen und den Zeilenabstand in einer Excel-Arbeitsmappe festlegen. Dies verbessert Ihre Fähigkeit, dynamische, optisch ansprechende Berichte zu erstellen.

## Keyword-Empfehlungen
- „Aspose.Cells für Java“
- "Textfeld in Excel hinzufügen"
- „Zeilenabstand in Excel festlegen“
- „Excel-Arbeitsmappe mit formatiertem Text“
- „Java und Aspose.Cells“


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}