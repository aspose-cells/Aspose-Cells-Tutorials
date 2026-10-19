---
category: general
date: 2026-06-27
description: Sla Excel snel op als TSV met Java. Leer hoe je een werkblad naar tekst
  exporteert, een blad als platte tekst exporteert en Excel‑gegevens als string exporteert
  met Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: nl
og_description: Sla Excel op als TSV met Java. Deze tutorial laat zien hoe je een
  werkblad naar tekst exporteert, het blad als platte tekst exporteert en Excel-gegevens
  efficiënt als string exporteert.
og_title: Excel opslaan als TSV – Stap‑voor‑stap exportgids
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Excel opslaan als TSV – Complete gids voor het exporteren van werkbladen naar
  tekst
url: /nl/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Excel as TSV – Complete Guide to Exporting Worksheets to Text

Heb je ooit **save Excel as TSV** nodig gehad, maar wist je niet welke API‑aanroep je moet gebruiken? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een spreadsheet proberen om te zetten naar een tab‑gescheiden bestand voor downstream verwerking. Het goede nieuws? Met een paar regels Java en Aspose.Cells kun je een werkblad exporteren naar tekst, export sheet plain text, en zelfs export Excel data string exporteren zonder moeite.

In deze tutorial lopen we het volledige workflow door — van het laden van een werkmap tot het configureren van exportopties en uiteindelijk het schrijven van een TSV‑bestand naar schijf. Aan het einde kun je **save Excel as TSV** in elk Java‑project, of je nu één blad verwerkt of tientallen bestanden in batch.

## Wat deze gids behandelt

* Een Excel-werkmap laden vanaf schijf  
* Het juiste werkblad selecteren (of over meerdere itereren)  
* `ExportTableOptions` configureren om platte‑tekst output te produceren  
* De gegevens wegschrijven als een tab‑gescheiden waarden (TSV) bestand  
* Tips voor het omgaan met grote bereiken, verschillende scheidingstekens en Unicode‑tekens  

Geen externe tools vereist — alleen Aspose.Cells voor Java en een Java 8+ runtime.

## Stap 1: Stel je project in en laad de werkmap

Voordat we in de code duiken, zorg ervoor dat je de Aspose.Cells JAR aan de classpath van je project hebt toegevoegd. Als je Maven gebruikt, ziet de afhankelijkheid er als volgt uit:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Now we can load the workbook:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Why this matters:** Loading the file is the first step in any **export Excel data string** workflow. If the file can’t be opened, nothing else will work.

> **Waarom dit belangrijk is:** Het laden van het bestand is de eerste stap in elke **export Excel data string** workflow. Als het bestand niet geopend kan worden, werkt niets anders.

### Pro tip
Als je te maken hebt met met wachtwoord beveiligde bestanden, roep dan `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})` aan.

## Stap 2: Kies het werkblad dat je wilt exporteren

Je kunt het eerste blad pakken, een blad op naam, of over alle bladen itereren. Hier is het eenvoudigste geval — het exporteren van het eerste werkblad:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Als je voor elk blad **export worksheet to text** moet uitvoeren, wikkel dan het bovenstaande in een `for`‑lus:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

## Stap 3: Maak en configureer exportopties

Het hart van **export sheet plain text** zit in `ExportTableOptions`. Door een paar eigenschappen te schakelen, zetten we het bereik om in een platte‑tekst string met een tab‑scheidingsteken:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Why use `setExportAsString(true)`?**  
> It tells Aspose.Cells to treat the output as raw text, which is exactly what you need when you want to **save Excel as TSV**. The alternative would be a CSV or HTML export, neither of which gives you clean tab separation.

> Waarom `setExportAsString(true)` gebruiken?  
> Het vertelt Aspose.Cells om de output als ruwe tekst te behandelen, wat precies is wat je nodig hebt wanneer je **save Excel as TSV** wilt. Het alternatief zou een CSV‑ of HTML‑export zijn, die geen schone tab‑scheiding geven.

### Randgeval: Aangepaste scheidingstekens
Als je downstream‑systeem een pipe (`|`) verwacht in plaats van een tab, wijzig dan simpelweg het scheidingsteken:

```java
exportOptions.setDelimiter('|');
```

## Stap 4: Exporteer het gewenste bereik naar een tekstbestand

Nu schrijven we daadwerkelijk het TSV‑bestand. De `exportTable`‑methode neemt drie argumenten: het celbereik, het uitvoerpad, en de `ExportTableOptions` die we zojuist hebben geconfigureerd.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Als je het *entire* gebruikte bereik wilt exporteren, vervang dan `"A1:D20"` door `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro tip
Na het exporteren kun je de string ook direct vastleggen:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Dat geeft je de ruwe **export Excel data string** zonder het bestandssysteem aan te raken.

## Stap 5: Omgaan met grote bestanden en prestatie‑tips

Bij het omgaan met enorme spreadsheets (honderdduizenden rijen), overweeg deze optimalisaties:

| Probleem | Oplossing |
|----------|-----------|
| Geheugendruk | Gebruik `WorkbookFactory.create(InputStream)` om het bestand te streamen in plaats van het volledig te laden. |
| Trage I/O | Schrijf naar een `BufferedWriter` of gebruik NIO `Files.newBufferedWriter`. |
| Unicode‑tekens | Zorg ervoor dat het uitvoerbestand wordt geschreven met UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Hieronder staat een fragment dat streaming en UTF‑8‑codering combineert:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

## Veelvoorkomende valkuilen en hoe ze te vermijden

1. **Vergeten `setExportAsString(true)` in te stellen.**  
   Zonder deze vlag zal Aspose een binair Excel‑bestand genereren, waardoor je **export worksheet to text** doel wordt verbroken.

2. **Het verkeerde scheidingsteken gebruiken.**  
   Een komma in plaats van een tab geeft je CSV, niet TSV. Controleer `setDelimiter('\t')`.

3. **Onjuiste bereik‑syntaxis.**  
   `"A1:D20"` is goed, maar `"A1:D20:"` (extra dubbele punt) zal een `IllegalArgumentException` veroorzaken.

4. **Bestandsrechten.**  
   Zorg ervoor dat de doelmap beschrijfbaar is. Op Linux lost `chmod 755` het probleem vaak op.

## Alles samenvatten – Volledig werkend voorbeeld

Hier is het complete, kant‑klaar programma dat **save Excel as TSV** van begin tot eind demonstreert:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Het uitvoeren van dit programma produceert een tab‑gescheiden bestand (`out.tsv`) dat elk downstream‑systeem — of het nu een database‑loader, een Unix `awk`‑script of een eenvoudige spreadsheet‑viewer is — kan verwerken.

## Conclusie

We hebben alles behandeld wat je nodig hebt om **save Excel as TSV** te gebruiken met Java en Aspose.Cells. Beginnend met het laden van de werkmap, het selecteren van het juiste blad, het configureren van `ExportTableOptions`, en uiteindelijk het schrijven van het bestand, heb je nu een solide, productie‑klaar patroon voor **export worksheet to text**, **export sheet plain text**, en **export Excel data string** scenario's.  

Wat is het volgende? Probeer meerdere bereiken te exporteren, scheidingstekens dynamisch te wijzigen, of de output direct naar een HTTP‑respons te streamen voor web‑gebaseerde downloads. Dezelfde principes gelden, en je zult merken dat het omgaan met Excel‑gegevens in platte tekst een eitje is zodra de basis op orde is.  

Heb je vragen of loop je tegen een eigenzinnige randgeval aan? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}