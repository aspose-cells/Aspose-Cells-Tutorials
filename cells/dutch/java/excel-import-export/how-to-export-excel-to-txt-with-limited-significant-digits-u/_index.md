---
category: general
date: 2026-08-17
description: Exporteer Excel naar TXT met beperking van significante cijfers – leer
  hoe je cijfers instelt en Excel naar tekst converteert in Java met een volledig
  Aspose.Cells‑voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: nl
lastmod: 2026-08-17
og_description: Exporteer Excel naar TXT met beperking van significante cijfers. Deze
  tutorial laat zien hoe je het aantal cijfers instelt en Excel converteert naar tekst
  met Aspose.Cells voor Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Excel exporteren naar TXT met beperkte significante cijfers – Java‑gids
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Hoe Excel exporteren naar TXT met beperkte significante cijfers met Java
url: /nl/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel naar TXT met beperkt aantal significante cijfers met Java

Als je **Excel naar TXT wilt exporteren** en tegelijkertijd het aantal significante cijfers wilt beheersen, biedt deze gids een kant‑klaar werkende oplossing. Je ziet hoe je cijfers instelt, Excel naar tekst converteert en de output netjes houdt met één configuratiewijziging.

Het voorbeeld maakt gebruik van Aspose.Cells for Java 25.10, waarin de optie `setSignificantDigits` is geïntroduceerd. Aan het einde van de tutorial kun je een TXT‑bestand genereren dat alleen de gewenste cijfers bevat, zonder extra afrondingscode.

## Wat je gaat bereiken

- Programma­matig een werkmap maken.
- Een numerieke waarde in een cel plaatsen.
- TXT‑opslaoptopties configureren om significante cijfers te beperken.
- De werkmap opslaan als een platte‑tekstbestand.
- Begrijpen hoe de instelling `significantDigits` werkt en hoe je deze voor andere scenario’s kunt aanpassen.

### Vereisten

- Java 17 of hoger (de code compileert ook met Java 8).
- Aspose.Cells for Java 25.10 of nieuwer. Download de JAR van de [Aspose website](https://products.aspose.com/cells/java) en voeg deze toe aan de classpath van je project.
- Een IDE of een eenvoudige teksteditor en een command‑line build‑tool (Maven/Gradle).

## Stap 1: Het project opzetten en Aspose.Cells importeren

Maak een nieuw Java‑project aan en voeg de Aspose.Cells‑JAR toe aan het build‑pad. Als je Maven gebruikt, voeg dan de volgende dependency toe aan `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Gebruik de `jdk17`‑classifier voor de nieuwste Java‑runtime; dit verkleint het risico op compatibiliteitswaarschuwingen.

## Stap 2: Een werkmap maken en een waarde schrijven

De werkmap vertegenwoordigt een Excel‑bestand in het geheugen. Je kunt data aan elke cel toevoegen met de methode `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Het getal `123.456789` dient als bron voor onze TXT‑export. Standaard zou Aspose.Cells alle decimalen schrijven, wat vaak leidt tot ruis in tekstbestanden.

## Stap 3: TXT‑opslaoptopties configureren om significante cijfers te beperken

Aspose.Cells biedt `TxtSaveOptions` voor fijnmazige controle over de platte‑tekstoutput. De methode `setSignificantDigits` vertelt de exporter hoeveel cijfers **in totaal** moeten worden behouden, niet alleen na de decimale punt.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Wanneer `significantDigits` is ingesteld op `4`, rondt de exporter de waarde `123.456789` af naar `123.5`. Dit gedrag komt overeen met de wiskundige definitie van significante cijfers: de eerste vier niet‑nul cijfers worden behouden.

### Hoe deze instelling verschilt van “beperk decimalen”

- **beperk decimalen** (`setDecimalPlaces`) verwijdert cijfers *na* de decimale punt, ongeacht het gehele deel.
- **significante cijfers** (`setSignificantDigits`) telt cijfers vanaf het eerste niet‑nul cijfer, wat handig is wanneer getallen in grootte variëren.

Als je een vast aantal decimalen wilt, vervang dan de bovenstaande regel door:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Stap 4: De werkmap opslaan als een TXT‑bestand

Schrijf nu de werkmap naar schijf met de geconfigureerde opties.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Het uitvoeren van het programma maakt `significant_digits.txt` aan in de werkmap. Het bestand bevat één enkele regel:

```
123.5
```

### Verwachte output

| Cel | Originele waarde | Geëxporteerd (4 significante cijfers) |
|------|------------------|---------------------------------------|
| A1   | 123.456789       | 123.5                                 |

Als je `setSignificantDigits(4)` verandert naar `6`, wordt de output `123.457`. Experimenteer met verschillende waarden om te zien hoe de afronding zich aanpast.

## Stap 5: Veelvoorkomende variaties en randgevallen

### Een heel bereik exporteren

Wil je meer dan één cel exporteren, vul dan het bereik vóór het opslaan:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Dezelfde `significantDigits`‑instelling wordt toegepast op elke numerieke cel, waardoor de precisie in het hele bestand consistent blijft.

### Omgaan met locale‑specifieke decimale scheidingstekens

Aspose.Cells respecteert de systeem‑locale bij het schrijven van tekst. Om een punt (`.`) als decimale scheidingsteken af te dwingen, stel je de cultuur van `TxtSaveOptions` in:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Dit is handig wanneer de doelapplicatie een specifiek formaat verwacht, zoals CSV‑parsers die alleen `.` accepteren.

### Bestaande bestanden overschrijven

De `save`‑methode overschrijft het doelbestand standaard. Als je onbedoeld gegevensverlies wilt voorkomen, controleer dan eerst of het bestand bestaat:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Grote werkmappen en geheugenverbruik

Bij het exporteren van zeer grote werkbladen kun je overwegen de output te streamen:

```java
saveOptions.setEnableMemorySaving(true);
```

Deze optie vermindert het heap‑verbruik door rijen geleidelijk te schrijven.

## Volledig werkend voorbeeld

Hieronder vind je het complete programma dat je direct kunt kopiëren, plakken en uitvoeren:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Het uitvoeren van deze code produceert `significant_digits.txt` met de volgende inhoud (tab‑gescheiden kolommen):

```
123.5	0.001235	98770
```

Elk getal volgt de regel **4 significante cijfers**, wat aantoont dat de instelling werkt voor verschillende grootten.

## Conclusie

Je weet nu hoe je **Excel naar TXT kunt exporteren** terwijl je het aantal significante cijfers beheerst. Door `TxtSaveOptions.setSignificantDigits` te gebruiken, kun je **cijfers instellen**, **decimalen beperken** en **significante cijfers beperken** in één onderhoudbare regel code. De aanpak werkt voor enkele cellen, volledige bereiken en grote werkmappen.

### Volgende stappen

- Verken andere eigenschappen van `TxtSaveOptions` zoals `setDelimiter('\t')` om kolomscheidingstekens aan te passen.
- Combineer de exporter met `CsvSaveOptions` als je komma‑gescheiden waarden wilt in plaats van platte tekst.
- Integreer de routine in een webservice die geüploade Excel‑bestanden accepteert en direct een getrimde TXT‑output teruggeeft.

Voel je vrij om te experimenteren met verschillende cijferlimieten en locales. Als je een scenario tegenkomt waarin de ingebouwde opties niet aan een speciale eis voldoen, kun je altijd het gegenereerde TXT‑bestand nabewerken met standaard Java‑I/O‑hulpmiddelen.

Happy coding!


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe tekst naar getallen converteren in Excel met Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Hoe een Excel‑bestand maken en exporteren naar HTML met Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hoe aangepaste Excel‑eigenschappen exporteren naar PDF met Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}