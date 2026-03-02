---
category: general
date: 2026-03-01
description: Leer hoe je CSV exporteert vanuit een Java-werkmap terwijl je significante
  cijfers en het exportbereik instelt, in één duidelijke gids.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: nl
og_description: Beheers hoe je CSV exporteert in Java, significante cijfers instelt
  en een bereik naar CSV exporteert, met praktische code en tips.
og_title: Hoe CSV te exporteren met Java – Volledige stapsgewijze handleiding
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Hoe CSV exporteren met Java – Stel significante cijfers in & Exporteer bereik
  naar CSV
url: /nl/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe CSV exporteren met Java – Significante cijfers instellen & bereik exporteren naar CSV

Heb je je ooit afgevraagd **hoe je csv kunt exporteren** vanuit een Java-werkmap zonder numerieke precisie te verliezen? Misschien heb je een snelle `toString()` geprobeerd en eindigde je met een puinhoop van afrondingsfouten. Dat is een veelvoorkomend probleem, vooral wanneer je **significante cijfers moet instellen** voor financiële gegevens of wetenschappelijke resultaten.  

In deze tutorial zie je een compleet, kant‑klaar voorbeeld dat laat zien **hoe je csv kunt exporteren**, hoe je **significante cijfers instelt**, en zelfs hoe je **een bereik naar csv exporteert** terwijl je gegevens netjes blijven. We lopen elke regel door, leggen het *waarom* achter de API‑aanroepen uit, en geven je tips om de gebruikelijke valkuilen te vermijden. Geen extra documentatie om te zoeken—gewoon een zelfstandige oplossing die je vandaag nog kunt copy‑pasten.

## Wat je zult leren

- Maak een werkmap en configureer numerieke precisie met `setNumberSignificantDigits`.
- Exporteer een specifiek celbereik als een net geformatteerde CSV‑string.
- Parse Japanse era‑datums met `DateTimeFormatInfo`.
- Herbereken formules zodat dynamische‑array resultaten actueel blijven.
- Render een draaitabel naar een PNG‑afbeelding.
- Gebruik Smart Marker om opmerkingen in te voegen en sla tenslotte de werkmap op.

Dit alles gebeurt met de Aspose.Cells for Java‑bibliotheek, versie 23.12 (de nieuwste op het moment van schrijven). Als je de JAR op je classpath hebt, ben je klaar om te gaan.

---

## Stap 1: Maak een werkmap en **stel significante cijfers in**

Voordat we iets kunnen exporteren, hebben we een werkmap‑object nodig. Het eerste waar veel ontwikkelaars overheen kijken, is numerieke precisie. Standaard gebruikt Aspose.Cells de volledige double‑precisie, wat kan leiden tot lange, onhandige strings in CSV. Het instellen van het aantal significante cijfers verkort de output terwijl de belangrijkste cijfers behouden blijven.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Waarom is dit belangrijk?**  
Als je een cel met `12345.6789` exporteert zonder het aantal cijfers te beperken, toont de CSV de volledige waarde, waardoor rapporten rommelig worden. Met `setNumberSignificantDigits(5)` wordt dezelfde cel `12346`, wat vaak is wat zakelijke gebruikers verwachten.

> **Pro tip:** Als je per kolom een andere precisie nodig hebt, kun je een aangepaste `Style` toepassen in plaats van de globale instelling.

---

## Stap 2: **Bereik exporteren naar CSV** – Opmaak is belangrijk

Nu de werkmap klaar is, laten we een rechthoekig blok gegevens ophalen en omzetten naar een CSV‑string. We zullen ook een twee‑decimalen formaat (`0.00`) afdwingen zodat elk getal netjes uitgelijnd is.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

De aanroep `exportDataTable` doet het zware werk. Omdat we `exportAsString` hebben ingesteld, retourneert de methode een `String` die we kunnen afdrukken, naar een bestand schrijven, of via HTTP verzenden. De stap **bereik exporteren naar csv** houdt ook rekening met de globale `setNumberSignificantDigits` die we eerder hebben gedefinieerd, zodat de getallen zowel afgerond worden op vijf significante cijfers *als* weergegeven worden met twee decimalen.

**Verwachte output (afgekapt):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Veelgestelde vraag:** *Wat als ik een ander scheidingsteken nodig heb, zoals een puntkomma?*  
> Roep simpelweg `exportOptions.setSeparator(";")` aan vóór het exporteren.

---

## Stap 3: Parse een Japanse era‑datum (bonus‑hulpmiddel)

Hoewel dit niet direct gerelateerd is aan CSV, bevatten veel Excel‑bladen locale‑specifieke datums. Hier zie je hoe je een Japanse era‑string zoals `"R3/04/01"` kunt omzetten naar een standaard `DateTime`‑object.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Output:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Waarom dit opnemen?**  
Als je CSV‑export downstream‑systemen voedt die ISO‑8601‑datums verwachten, moet je eerst alle gelokaliseerde formaten normaliseren. Deze code laat het *hoe* en *waarom* op één plek zien.

---

## Stap 4: Formules herberekenen – Houd dynamische‑array resultaten actueel

Als je werkmap formules bevat (bijv. `=SUM(A1:A10)`), worden deze niet automatisch bijgewerkt nadat we instellingen hebben gewijzigd. Het aanroepen van `calculateFormula` dwingt een volledige herberekening af, waardoor de geëxporteerde CSV de nieuwste waarden weergeeft.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Let op:** Grote werkmappen kunnen merkbare tijd kosten om te herberekenen. Voor prestatie‑kritische scenario's, overweeg `calculateFormula(FormulaCalculationOptions)` om de reikwijdte te beperken.

---

## Stap 5: Render de eerste draaitabel naar een PNG‑afbeelding

Soms heb je een visueel momentopname van een draaitabel nodig naast de CSV. De onderstaande code rendert de eerste draaitabel op het eerste werkblad naar een PNG‑bestand.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Tip:** Als de werkmap nog geen draaitabel bevat, kun je er een programmatisch maken—zie de Aspose.Cells‑documentatie voor een snel voorbeeld.

---

## Stap 6: Gebruik Smart Marker om een opmerking te schrijven en de werkmap op te slaan

Smart Marker laat je dynamische inhoud in cellen injecteren met eenvoudige placeholders. Hier schrijven we een opmerking zoals “Reviewed by QA” in een aangewezen cel en slaan vervolgens de werkmap op.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

De `${Comment}`‑placeholder kan overal in het blad worden geplaatst (bijv. cel `A1`). Wanneer `apply` wordt uitgevoerd, wordt de placeholder vervangen door de opgegeven waarde.

**Resultaat:** Je vindt een `output/commented.xlsx`‑bestand met de opmerking, plus de eerder gegenereerde `pivot.png` en de CSV‑string die naar de console wordt geprint.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het volledige programma dat je kunt compileren en uitvoeren:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Verwachte console‑output

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Je vindt ook `output/pivot.png` (als er een draaitabel bestond) en `output/commented.xlsx` op schijf.

---

## Veelgestelde vragen & randgevallen

- **Kan ik direct naar een fysiek CSV‑bestand exporteren?**  
  Ja. Vervang het `exportAsString`‑blok door `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Wat als mijn blad een andere locale voor getallen gebruikt?**  
  Stel `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))` in vóór het exporteren; dit zal 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}