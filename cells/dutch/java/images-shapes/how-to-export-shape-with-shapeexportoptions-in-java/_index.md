---
category: general
date: 2026-10-01
description: Leer hoe u een vorm exporteert met ShapeExportOptions in Java, waarbij
  de vorm bewerkbaar blijft bij het converteren naar PPTX met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: nl
lastmod: 2026-10-01
og_description: Exporteer vorm met ShapeExportOptions in Java om bewerkbare PPTX‑bestanden
  te maken. Deze tutorial leidt je door het volledige proces met behulp van Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Vorm exporteren met ShapeExportOptions in Java – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Hoe een vorm te exporteren met ShapeExportOptions in Java
url: /nl/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een vorm exporteren met ShapeExportOptions in Java

Als je een **vorm moet exporteren met ShapeExportOptions** vanuit een Excel-werkmap, laat deze gids je de exacte stappen zien. Je zult zien hoe je de vorm bewerkbaar houdt bij het converteren naar een PPTX‑bestand, wat essentieel is voor nabewerkingen in PowerPoint.

Het exporteren van vormen is een veelvoorkomende taak wanneer je dia‑sets genereert vanuit spreadsheets—of je nu verkoop‑decks, rapportage‑dashboards of geautomatiseerde presentaties maakt. Deze tutorial behandelt alles wat je nodig hebt, van project‑opzet tot het verifiëren van het geëxporteerde bestand, en maakt gebruik van de **Aspose.Cells for Java**‑bibliotheek.

## Wat je nodig hebt

- Java 17 of nieuwer (de code compileert met elke recente JDK)
- Maven of Gradle voor afhankelijkheidsbeheer
- Een Excel‑bestand (`Shapes.xlsx`) dat minstens één tekstvak of andere vorm bevat
- Basiskennis van Aspose.Cells‑API's

## Stap 1: Voeg Aspose.Cells toe aan je project (Aspose Cells export shape)

Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Voor Gradle, plaats dit in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Registreer je licentie vroeg om evaluatiewatermerken te vermijden.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Stap 2: Laad de werkmap die de vorm bevat

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

Het `Workbook`‑object vertegenwoordigt het volledige Excel‑bestand. Het laden ervan is de eerste voorwaarde voor elke vorm‑manipulatie.

## Stap 3: Toegang tot het werkblad en haal de gewenste vorm op (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Waarom dit belangrijk is:** Vormen worden per werkblad opgeslagen, dus je moet naar het juiste blad navigeren voordat je een specifieke vorm kunt exporteren.

## Stap 4: Configureer **ShapeExportOptions** om de vorm bewerkbaar te houden (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Het instellen van `ExportAsEditable` op `true` vertelt Aspose.Cells de vectorgegevens van de vorm te behouden, waardoor PowerPoint‑gebruikers de vorm na import kunnen aanpassen.

## Stap 5: Exporteer de vorm direct naar een PPTX‑bestand (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

De `exportToImage`‑methode werkt voor verschillende afbeeldingsformaten; wanneer de doelbestandsnaam eindigt op `.pptx`, schrijft Aspose.Cells een PowerPoint‑dia die de vorm bevat.

### Verwacht resultaat

- `textbox.pptx` verschijnt in de opgegeven map.
- Het openen van het bestand in PowerPoint toont één dia met het oorspronkelijke tekstvak.
- Het tekstvak is volledig bewerkbaar (je kunt tekst, lettertype, grootte, enz. wijzigen).

## Stap 6: Verifieer de output en behandel veelvoorkomende randgevallen

### Programma‑matig verifiëren

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Als `slideCount` gelijk is aan `1`, is de export geslaagd.

### Randgeval: Meerdere vormen

Als het werkblad meerdere vormen bevat en je slechts één specifieke wilt, zoek deze dan op naam:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Randgeval: Vorm niet gevonden

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Randgeval: Exporteren naar andere formaten

`ShapeExportOptions` ondersteunt ook PNG, JPEG, SVG en EMF. Verander de bestandsextensie en stel eventueel `exportOptions.setImageFormat(ImageFormat.PNG)` in.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samenvoegen levert een zelfstandig programma op dat je kunt kopiëren‑plakken in je IDE:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Het uitvoeren van het programma maakt `textbox.pptx`. Open het in PowerPoint, klik met de rechtermuisknop op het tekstvak, en je ziet de gebruikelijke bewerkingsgrepen—wat bevestigt dat **export shape with ShapeExportOptions** de bewerkbaarheid heeft behouden.

## Veelgestelde vragen

| Vraag | Antwoord |
|----------|--------|
| *Kan ik een grafiekvorm exporteren?* | Ja. Dezelfde `exportToImage`‑aanroep werkt voor grafieken, afbeeldingen en SmartArt. |
| *Wat als ik een PNG met hogere resolutie nodig heb?* | Stel `options.setImageFormat(ImageFormat.PNG)` in en pas `options.setResolution(300)` aan vóór het exporteren. |
| *Is de geëxporteerde PPTX compatibel met oudere PowerPoint‑versies?* | De bibliotheek schrijft Office Open XML (PPTX) dat wordt ondersteund door PowerPoint 2007 en later. |
| *Heb ik een licentie nodig om dit te laten werken?* | Een gratis evaluatie werkt maar voegt een watermerk toe. Registreer een licentie om dit te verwijderen. |

## Volgende stappen

- Verken **Aspose.Slides for Java** als je meerdere geëxporteerde vormen wilt combineren tot één dia‑set.
- Gebruik **ShapeExportOptions.setExportAsEditable(false)** wanneer je de voorkeur geeft aan een rasterafbeelding (PNG/JPEG) voor snellere weergave.
- Automatiseer batchverwerking: loop door alle werkbladen en exporteer elke vorm naar afzonderlijke PPTX‑bestanden.

---

### Conclusie

Je weet nu hoe je **vorm kunt exporteren met ShapeExportOptions** in Java, waarbij je de bewerkbaarheid behoudt bij het converteren van een tekstvak (of een andere vorm) naar een PPTX‑bestand. Door de bovenstaande stappen te volgen—de bibliotheek instellen, de werkmap laden, `ShapeExportOptions` configureren en `exportToImage` aanroepen—kun je vorm‑export integreren in elke geautomatiseerde rapportage‑pipeline.

Voel je vrij om te experimenteren met verschillende vormen, uitvoerformaten en resolutie‑instellingen. Als je deze gids nuttig vond, deel hem dan met teamgenoten of bladert hem op voor later gebruik. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe vormmarges aanpassen in Excel met Aspose.Cells voor Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [Hoe 3D‑vormopmaak toepassen in Excel met Aspose.Cells voor Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Werkmap Vormen Kopiëren Gids](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}