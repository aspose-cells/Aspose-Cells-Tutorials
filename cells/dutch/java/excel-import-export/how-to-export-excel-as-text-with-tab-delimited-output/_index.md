---
category: general
date: 2026-11-22
description: Leer hoe je Excel als tekst exporteert en een tab‑gescheiden bestand
  maakt. Deze gids laat zien hoe je alle velden tussen aanhalingstekens zet en de
  spreadsheet‑tekst efficiënt opslaat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: nl
lastmod: 2026-11-22
og_description: Exporteer Excel als tekst en maak een tab‑gescheiden bestand. Volg
  deze stap‑voor‑stap tutorial om alle velden te omringen met aanhalingstekens en
  de spreadsheet‑tekst op te slaan met Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Excel exporteren als tekst – gids voor tab‑gescheiden bestanden
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Hoe Excel exporteren als tekst met tab‑gescheiden output
url: /nl/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel exporteren als tekst met tab‑gescheiden uitvoer

Als je **Excel wilt exporteren als tekst**, leidt deze tutorial je door het volledige proces van het maken van een tab‑gescheiden bestand vanuit een werkmap. Of je nu een data‑migratie‑pipeline bouwt of een snelle CSV‑achtige dump nodig hebt voor downstream verwerking, de onderstaande stappen laten je **spreadsheet‑tekst opslaan** met volledige controle over scheidingstekens en aanhalingstekens.

Het exporteren van spreadsheet‑gegevens als platte tekst is vaak draagbaarder dan het behouden van het native `.xlsx`‑formaat. In deze gids leer je ook hoe je **alle velden moet aanhalen**, wat garandeert dat waarden met tabs, komma's of regeleinden veilig worden ingesloten.

## Wat je nodig hebt

* Java 17 of later geïnstalleerd.
* De Aspose.Cells for Java‑bibliotheek (de code gebruikt `ExportOptions` en `ExportTableOptions` uit deze bibliotheek). Je kunt deze toevoegen via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Een IDE of een eenvoudige teksteditor om het Java‑programma te compileren en uit te voeren.

## Excel exporteren als tekst – stap‑voor‑stap

De volgende secties verdelen de taak in drie logische stappen. Elke stap legt **waarom** het belangrijk is uit, niet alleen **wat** je moet typen.

### Stap 1: Bereid de werkmap en voorbeeldgegevens voor

Het maken van een werkmap geeft je iets om te exporteren. In een echt project zou je een bestaand bestand laden met `new Workbook("input.xlsx")`; hier genereren we een klein blad zodat het voorbeeld direct werkt.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Waarom deze stap?*  
Een werkmap is het bronobject voor elke exportbewerking. Door een paar rijen toe te voegen kun je verifiëren dat de **quote all fields**‑optie echt komma's en andere speciale tekens beschermt.

### Stap 2: Configureer exportopties – scheidingsteken, aanhalingstekens en uitvoermodus

De kern van **export spreadsheet tab‑delimited** zit in `ExportTableOptions`. Je stelt het scheidingsteken in op een tab (`'\t'`) en schakelt `setQuoteAllFields(true)` in zodat elke cel wordt omgeven door dubbele aanhalingstekens. Dit elimineert ambiguïteit wanneer een cel zelf een tab of regeleinde bevat.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Waarom deze stap?*  
- **Delimiter** bepaalt hoe kolommen worden gescheiden. Een tab (`\t`) creëert een **tab‑delimited file** die veel data‑verwerkingstools accepteren.  
- **Quote all fields** garandeert dat zelfs als een cel een scheidingsteken bevat, de resulterende tekst parseerbaar blijft.  
- Het instellen van `ExportAsString` vertelt Aspose.Cells om een string te genereren in plaats van een binair werkmap, wat precies is wat je nodig hebt voor **save spreadsheet text**.

### Stap 3: Sla de werkmap op als een tab‑gescheiden tekstbestand

Nu **exporteer je Excel daadwerkelijk als tekst**. De `save`‑methode neemt het doelpad en de `ExportOptions` die je hebt geconfigureerd.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Wanneer het programma is voltooid, vind je `output/table.txt` met de volgende inhoud:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Waarom deze stap?*  
De `save`‑aanroep schrijft het **tab‑delimited file** naar schijf, waardoor je effectief **spreadsheet‑tekst opslaat** in een formaat dat geopend kan worden door Excel, Notepad of elk data‑importtool dat tabs begrijpt.

## Hoe alle velden aan te halen bij het exporteren van Excel als tekst

Als je `setQuoteAllFields(true)` weglaat, zullen cellen die tabs, komma's of regeleinden bevatten de structuur van het uitvoerbestand breken. Bijvoorbeeld, de rij `Bob, Jr.` zou worden opgesplitst in twee kolommen, waardoor de dataset corrupt raakt. Schakel altijd aanhalingstekens in wanneer:

* Je brongegevens kunnen komma's, tabs of regeleinden bevatten.
* Downstream‑parsers verwachten geciteerde CSV/TSV‑bestanden.
* Je een deterministische export nodig hebt, ongeacht de celinhoud.

## Een tab‑gescheiden bestand maken zonder Aspose.Cells (optioneel)

Als je de voorkeur geeft aan een pure‑Java‑oplossing zonder externe bibliotheken, kun je over rijen itereren en ze handmatig schrijven:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Deze snippet demonstreert dezelfde **export spreadsheet tab‑delimited**‑logica: een tab‑scheidingsteken, elk veld aanhalen, en het resultaat schrijven als platte tekst. Het gebruik van Aspose.Cells vereenvoudigt echter het verwerken van grote werkmappen, behoudt opmaak en vermindert boilerplate.

## Veelvoorkomende valkuilen en pro‑tips

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Ontbrekende tabs in output** | Scheidingsteken bleef op de standaard komma. | Roep expliciet `setDelimiter('\t')` aan. |
| **Ongequoteerde komma's breken kolommen** | `quoteAllFields` niet ingeschakeld. | Gebruik `setQuoteAllFields(true)` of citeer handmatig. |
| **Bestand niet aangemaakt** | Uitvoermap bestaat niet. | Zorg ervoor dat de map `output/` bestaat of gebruik `Files.createDirectories`. |
| **Coderingproblemen** | Standaard platformcodering kan niet‑ASCII‑tekens corrupt maken. | Geef `ExportOptions.setEncoding(Encoding.getUTF8())` door indien nodig. |

## Het resultaat testen

Na het uitvoeren van het programma:

1. Open `output/table.txt` in een platte‑tekst editor. Je zou elke waarde tussen dubbele aanhalingstekens moeten zien en kolommen gescheiden door één tab‑teken.  
2. Importeer het bestand in Excel (`Data → From Text/CSV`). Kies **Tab** als scheidingsteken; Excel zal elke aangehaalde waarde correct in een eigen cel plaatsen.  
3. Verify that special characters (commas, line breaks

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [hoe excel exporteren – Tab‑Delimited Text Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Excel opslaan als tekstbestand met aangepaste scheidingsteken met Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Hoe Excel opslaan als tekst met Aspose.Cells – stap‑voor‑stap gids](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}