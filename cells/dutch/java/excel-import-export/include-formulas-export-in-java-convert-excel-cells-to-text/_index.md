---
category: general
date: 2026-07-03
description: Formules exporteren opnemen in Java om Excel-cellen naar tekst te converteren
  met Aspose.Cells. Leer hoe je een Excel-bereik kunt afdrukken en efficiënt celwaarden
  als string kunt ophalen.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: nl
og_description: Voeg formules export toe in Java om Excel‑cellen naar tekst te converteren.
  Stapsgewijze handleiding die laat zien hoe je een Excel‑bereik afdrukt en celwaarden
  als string ophaalt.
og_title: Formules exporteren in Java – Excelcellen naar tekst converteren
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Formules Exporteren Insluiten in Java – Excelcellen Converteren naar Tekst
url: /nl/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formules Exporteren in Java – Excel‑cellen naar Tekst Converteren

Heb je ooit **formules export** nodig gehad bij het uitlezen van gegevens uit een Excel‑werkmap? Misschien bouw je een rapportageservice die de oorspronkelijke formules moet behouden terwijl hij toch een nette tekst‑blob levert. In dat geval ben je hier op de juiste plek. Deze gids leidt je door het converteren van Excel‑cellen naar platte tekst—*inclusief* eventuele ingesloten formules—met Aspose.Cells voor Java.

We behandelen ook hoe je **Excel‑bereik afdrukt**, **export‑tabelopties** aanpast, en uiteindelijk **celwaarden als string krijgt** die je kunt loggen, via een API kunt verzenden of in een database kunt opslaan. Aan het einde heb je een volledig uitvoerbaar fragment en een goed begrip van het waarom achter elke aanroep.

## Wat je zult meenemen

- Een compleet, kant‑en‑klaar Java‑programma dat een `.xlsx`‑bestand leest, een bereik selecteert en het exporteert als een geformatteerde string.
- Inzicht in de `ExportTableOptions`‑klasse en waarom het schakelen van `setExportAsString` en `setIncludeFormula` van belang is.
- Tips voor het omgaan met grote werkbladen, verschillende gegevenstypen en het aanpassen van het uitvoerformaat.
- Een snelle checklist voor veelvoorkomende valkuilen (denk aan samengevoegde cellen, verborgen rijen en locale‑specifieke getalformaten).

### Vereisten

- Java 17 of nieuwer (de code compileert ook met oudere versies, maar we blijven bij de nieuwste LTS).
- Aspose.Cells voor Java 23.10 (of een recentere release) — te verkrijgen via Maven Central.
- Een voorbeeld‑`input.xlsx` in een map die je beheert (het pad is hard‑gecodeerd in het voorbeeld voor duidelijkheid).

Als je deze al hebt, laten we dan beginnen.

## Stap 1: Het project opzetten en afhankelijkheden toevoegen

Maak eerst een Maven‑project (of Gradle, als je dat verkiest). Voeg de Aspose.Cells‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** Als je een bedrijfsproxy gebruikt, zorg er dan voor dat de repository bereikbaar is; anders mislukt de build met een “Could not resolve dependencies”‑fout.

Zodra Maven klaar is met downloaden, kun je Java gaan schrijven.

## Stap 2: De werkmap laden en het gewenste werkblad pakken

De eerste regel van het code‑voorbeeld laat zien hoe je een bestaande werkmap opent:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad naar je bestand. De `Workbook`‑constructor detecteert automatisch het bestandsformaat (XLS, XLSX, CSV, enz.), dus je hoeft dit niet expliciet op te geven.

Vervolgens halen we het eerste blad op:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Waarom het eerste blad? In veel sjablonen staan de gegevens op het eerste tabblad, maar je kunt elke index gebruiken of zelfs `get("SheetName")` als je een benoemde aanpak verkiest.

## Stap 3: Het bereik definiëren dat je wilt exporteren

Nu komt het hart van de **excel‑cellen naar tekst converteren**‑operatie. Je vertelt Aspose.Cells welke cellen je wilt ophalen door een `Range`‑object te maken:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

De string `"A1:C3"` is een klassieke A1‑stijl adres. Deze kan ook programmatisch worden opgebouwd:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Die flexibiliteit helpt wanneer de omvang van het bereik dynamisch is — bijvoorbeeld als je de laatst gebruikte rij leest met `ws.getCells().getMaxDataRow()`.

## Stap 4: Export‑tabelopties configureren om formules op te nemen

Hier gebeurt de **include formulas export**‑magie. Standaard geeft Aspose.Cells de *weergegeven* waarden terug. Als een cel `=SUM(A1:A3)` bevat, krijg je het berekende getal, niet de formule‑tekst. Om dat te wijzigen, stel je `ExportTableOptions` in:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Waarom beide vlaggen? `setExportAsString(true)` vertelt de API de cellen te concateneren met de standaard scheidingsteken (tab voor kolommen, regeleinde voor rijen). `setIncludeFormula(true)` schakelt de bron van de waarde van “weergegeven waarde” naar “ruwe formule”. Als je alleen waarden wilt, laat je het `false`.

### Optionele aanpassingen

- `eto.setExportHiddenRows(true);` – ook verborgen rijen in Excel opnemen.
- `eto.setExportHiddenColumns(true);` – hetzelfde voor kolommen.
- `eto.setExportAsHTML(true);` – HTML krijgen in plaats van platte tekst.

Voel je vrij om te experimenteren; de opties‑klasse is een **export table options**‑speeltuin.

## Stap 5: Het bereik ophalen als een geformatteerde string

Nu halen we de gegevens op:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

De geretourneerde `txt` ziet er ongeveer zo uit (ervan uitgaande dat A1:C3 een mix van waarden en formules bevat):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Let op de tab (`\t`) die kolommen scheidt en het regeleinde (`\n`) dat rijen scheidt. Je kunt de string later splitsen als je een 2‑D‑array nodig hebt:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Stap 6: Het resultaat afdrukken – “Print Excel Range” eenvoudig gemaakt

Tot slot dumpen we de string naar de console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Het uitvoeren van het programma print exact de bovenstaande output. Vanaf hier kun je de string naar een logbestand schrijven, via HTTP verzenden of opslaan in een NoSQL‑document.

## Volledig, kant‑en‑klaar voorbeeld

Alles bij elkaar, hier is het complete programma. Kopiëren, plakken en **Run** — geen ontbrekende imports.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Verwachte output (voorbeeld)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Als je werkmap getallen bevat die als datums zijn opgemaakt, verschijnen ze in het locale‑specifieke formaat (bijv. `2026‑07‑03`). Om ISO‑datums af te dwingen, kun je `ExportTableOptions` aanpassen met een aangepaste `NumberFormat`.

## Edge‑cases en veelgestelde vragen behandelen

### Wat als het bereik samengevoegde cellen bevat?

Samengevoegde cellen worden behandeld als de waarde van de cel links‑boven. De rest van het samengevoegde gebied verschijnt als lege strings. Als je het adres van het samengevoegde gebied nodig hebt, vraag dan `Cell.getMergedRange()` op vóór export.

### Kan ik een enorm blad exporteren (honderdduizenden rijen)?

Ja, maar let op het geheugenverbruik. Gebruik `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` zodat Aspose.Cells gegevens naar schijf kan streamen. Overweeg ook om in delen te exporteren (bijv. 10 000 rijen per keer) om de string beheersbaar te houden.

### Hoe wijzig ik de kolomscheidingsteken?

`ExportTableOptions` biedt `setSeparator(char separator)`. Voor CSV‑achtige output stel je het in op `','`:

```java
eto.setSeparator(',');
```

### Respecteren formules externe verwijzingen?

Als een formule naar een andere werkmap verwijst, behoudt Aspose.Cells de referentietekst (`='[Other.xlsx]Sheet1'!A1`). Het zal de externe waarde niet evalueren tenzij je die werkmap ook laadt.

## Pro‑tips voor productie‑klare code

- **Cache de werkmap** als je de

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel exporteren naar HTML met Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Hoe Excel naar PDF converteren in Java met Aspose.Cells: Een stapsgewijze handleiding](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Excel‑werkmap exporteren als afbeelding met Aspose.Cells voor Java: Een stapsgewijze handleiding](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}