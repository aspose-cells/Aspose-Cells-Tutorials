---
"date": "2025-04-08"
"description": "Lär dig hur du använder Aspose.Cells för Java för att lägga till textrutor och ange radavstånd i Excel-arbetsböcker. Förbättra dina arbetsbokspresentationer med formaterade textformer."
"title": "Lägg till textruta och ange radavstånd i Excel med hjälp av Aspose.Cells för Java"
"url": "/sv/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Lägg till en textruta och ange radavstånd i Excel med hjälp av Aspose.Cells för Java

## Introduktion

Att skapa dynamiska Excel-rapporter kräver ofta anpassad textformatering, till exempel att lägga till textrutor med specifikt radavstånd. Med Aspose.Cells för Java blir detta enkelt och effektivt. Den här handledningen guidar dig genom att förbättra dina arbetsbokspresentationer med Aspose.Cells för Java för att lägga till formaterade textformer.

I slutet av den här guiden kommer du att lära dig hur du:
- Skapa en ny Excel-arbetsbok och få åtkomst till dess arbetsblad
- Lägga till en textruteform i ett kalkylblad
- Ange anpassat radavstånd inuti en textform
- Spara din formaterade arbetsbok i XLSX-format

Låt oss börja med att konfigurera din miljö.

### Förkunskapskrav

Innan du börjar, se till att du har följande:
- Java Development Kit (JDK) installerat på din dator
- En IDE eller editor för att skriva Java-kod
- Maven- eller Gradle-byggsystem konfigurerat för att hantera beroenden

Grundläggande förståelse för Java-programmering och kännedom om Excel-filstrukturer är meriterande.

## Konfigurera Aspose.Cells för Java

Inkludera Aspose.Cells i ditt projekts beroendehantering med hjälp av Maven eller Gradle:

**Maven**

Lägg till följande beroendeblock till din `pom.xml` fil:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Inkludera detta i din `build.gradle` fil:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Skaffa sedan en licens för Aspose.Cells genom att välja en gratis provperiod, begära en tillfällig licens eller köpa en fullständig licens.

### Initierar Aspose.Cells

När biblioteket har inkluderats i ditt projekt, initiera det i din Java-applikation:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Initiera en instans av Workbook (representerar en Excel-fil)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Implementeringsguide

### Skapa en arbetsbok och ett Access-arbetsblad

Börja med att skapa en ny Excel-arbetsbok och öppna dess första kalkylblad. Det är här du lägger till din textruta.

#### Översikt

Att skapa en ny arbetsbok ger en tom tavla där du kan lägga till data, former och formatering efter behov.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Lägg till textruta i kalkylblad

Lägg sedan till en textruteform i det valda kalkylbladet. Denna form kan innehålla vilken text du vill.

#### Översikt

Textrutor är mångsidiga verktyg för att inkludera anpassad text som anteckningar eller instruktioner direkt i ett Excel-ark.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Lägg till en textruteform i kalkylbladet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Ange text i form

När din textruta är klar, ange dess innehåll och formatera texten inuti den.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Lägg till en textruteform i kalkylbladet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ange textinnehåll inuti formen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Få åtkomst till textstycken i form

Du kan komma åt enskilda stycken i en textruta för att tillämpa specifik formatering.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Lägg till en textruteform i kalkylbladet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ange textinnehåll inuti formen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Åtkomst till det andra stycket i formen
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Ställ in radavstånd för stycke

Att anpassa radavståndet kan förbättra läsbarheten. Så här ställer du in det:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Lägg till en textruteform i kalkylbladet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ange textinnehåll inuti formen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Åtkomst till det andra stycket i formen
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ställ in radavståndet till 20 punkter
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurera avstånd före och efter stycket
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Spara arbetsboken

Slutligen, spara din arbetsbok med den nyligen tillagda och formaterade textrutan.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Skapa en ny arbetsbok (Excel-fil)
        Workbook workbook = new Workbook();
        
        // Åtkomst till det första arbetsbladet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Lägg till en textruteform i kalkylbladet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ange textinnehåll inuti formen
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Åtkomst till det andra stycket i formen
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ställ in radavståndet till 20 punkter
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurera avstånd före och efter stycket
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Spara arbetsboken
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Slutsats

Du har nu lärt dig hur man lägger till en textruta och anger radavstånd i en Excel-arbetsbok med hjälp av Aspose.Cells för Java. Detta förbättrar din förmåga att skapa dynamiska och visuellt tilltalande rapporter.

## Nyckelordsrekommendationer
- "Aspose.Cells för Java"
- "Lägg till textruta i Excel"
- "Ställ in radavstånd i Excel"
- "Excel-arbetsbok med formaterad text"
- "Java och Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}