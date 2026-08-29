---
category: general
date: 2026-06-21
description: Aspose Cells datumformaatgids – leer hoe u een aangepast datumformaat
  instelt, de locale van de werkmap wijzigt en een globaal datumformaat toepast in
  Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: nl
og_description: 'Aspose Cells datumformaat‑tutorial: leer hoe je een aangepast datumformaat
  instelt, de werkmap‑locale wijzigt en een globaal datumformaat instelt voor Java‑projecten.'
og_title: Aspose Cells-datumformaat – Aangepaste datumopmaak instellen in Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Aspose Cells-datumformaat: Hoe een aangepast datumformaat in Java instellen'
url: /nl/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Datumnotatie – Complete Java‑gids

Heb je je ooit afgevraagd hoe je een aangepast datumformaat instelt in Aspose Cells voor Java? Je bent niet de enige. Of je nu rapporten genereert voor een Japanse klant of gewoon een consistente datumstijl wilt in een heel werkboek, het beheersen van **aspose cells date format** is essentieel.

In deze tutorial lopen we stap voor stap door een praktisch, end‑to‑end voorbeeld dat laat zien **hoe je datumformaat** globaal instelt, de locale van het werkboek wijzigt en een aangepast patroon toepast zoals het Japanse jaartal. Aan het einde heb je een herbruikbare code‑snippet die je in elk project kunt gebruiken – geen giswerk meer.

## Wat deze gids behandelt

- Een nieuw `Workbook`‑object aanmaken.
- De locale van het werkboek wijzigen zodat ingebouwde formaten regionale regels volgen.
- Een **set custom date format** definiëren met `DateTimeFormatter`.
- Dat formaat globaal toepassen via `WorkbookSettings`.
- Veelvoorkomende valkuilen (bijv. het overschrijven van cel‑niveau formaten) en hoe deze te vermijden.
- Snelle variaties voor andere locales of format‑strings.

Je hebt alleen een Java‑ontwikkelomgeving nodig, Maven of Gradle om Aspose Cells binnen te halen, en een basisbegrip van Java‑syntaxis. Klaar? Laten we beginnen.

## Stap 1: Zet je project op en importeer Aspose Cells

Allereerst – zorg dat Aspose Cells voor Java op je classpath staat. Als je Maven gebruikt, voeg dan de volgende dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle‑gebruikers kunnen toevoegen:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Pro tip:** Aspose biedt een gratis proeflicentie van 30 dagen. Plaats het bestand `Aspose.Cells.lic` in de root van je project en roep `License license = new License(); license.setLicense("Aspose.Cells.lic");` aan voordat je een werkboek maakt.

Importeer nu de klassen die we nodig hebben:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Deze imports geven ons toegang tot de werkboekcontainer, de instellingen en de locale‑bewuste formatter.

## Stap 2: Maak een nieuw werkboek en krijg de instellingen op

Een nieuw `Workbook` start met de standaard (meestal US) locale. Om datumverwerking globaal te controleren, moeten we het `WorkbookSettings`‑object ophalen:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

Het `settings`‑object is een centraal knooppunt. Alles wat je hier wijzigt – zoals het datumformaat – heeft invloed op elke cel die **geen** expliciete stijl heeft die het overschrijft.

## Stap 3: Definieer een aangepast datum/tijd‑formaat (Japans era‑voorbeeld)

Stel, je hebt datums nodig in het Japanse era‑formaat, bv. “令和04.10.01”. Het patroon `"ggyy.MM.dd"` doet het werk wanneer het gekoppeld wordt aan een Japanse cultuur:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Als je een eenvoudigere ISO‑stijl wilt (`"yyyy-MM-dd"`), vervang dan gewoon de patroon‑string – geen andere wijzigingen nodig.

## Stap 4: Pas het aangepaste formaat toe als globaal datumformaat

Nu binden we de formatter aan de globale instellingen van het werkboek. Dit is de **set global date format** stap die ervoor zorgt dat elke cel die een datum weergeeft automatisch ons patroon gebruikt:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

Op dit moment zal elke datum die je in het blad schrijft – of via `Cell.putValue(new Date())` of door een gegevensbron te lezen – weergegeven worden met het Japanse era‑patroon.

## Stap 5: Vul het werkboek met voorbeeld‑datums (optioneel)

Laten we een paar rijen toevoegen zodat je het formaat in actie kunt zien. Dit deel is niet strikt vereist voor de datum‑formattering, maar helpt om te verifiëren dat alles werkt:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Wanneer je het werkboek opslaat, zullen die cellen iets tonen als:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(Het exacte era‑jaar hangt af van de huidige Japanse kalender.)

## Stap 6: Sla het werkboek op en controleer de output

Schrijf tenslotte het werkboek naar een bestand zodat je het kunt openen in Excel, LibreOffice of een andere viewer die het formaat respecteert:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Open `CustomDateFormatDemo.xlsx` en je zou de datums moeten zien die zijn opgemaakt volgens het patroon dat we hebben ingesteld. Als je een afwijking opmerkt, controleer dan of er geen cel‑niveau stijl is die de globale instelling overschrijft (zie de sectie “Randgevallen” hieronder).

## Randgevallen & Variaties

### 1. Het globale formaat op cel‑niveau overschrijven

Als een cel al een stijl heeft met een specifiek getalformaat, wordt de globale instelling genegeerd voor die cel. Om het globale formaat af te dwingen, maak je de stijl van de cel leeg:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Werkboek‑locale wijzigen zonder een aangepast patroon

Soms wil je alleen **change workbook locale** zodat ingebouwde datumformaten (zoals `14‑03‑2024`) regionale conventies volgen. Dat kan zonder een `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Nu zal elke standaard datumstijl verschijnen als `21/04/2025` in plaats van `04/21/2025`.

### 3. Meerdere aangepaste formaten in één werkboek gebruiken

Aspose Cells staat je toe verschillende aangepaste formaten te definiëren en ze selectief toe te passen:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Terugkeren naar het standaardformaat

Als je wilt terugschakelen naar de standaard datumafhandeling van Aspose, geef je simpelweg `null` door:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Veelgestelde vragen beantwoord

- **Heeft dit invloed op bestaande werkbladen?**  
  Ja – elk werkblad dat wordt geladen in de `Workbook` nadat je het globale formaat hebt ingesteld, erft het, tenzij een cel al een expliciete stijl heeft.

- **Kan ik het formaat instellen nadat ik data heb geschreven?**  
  Absoluut. Het globale formaat wordt toegepast op render‑tijd, dus je kunt eerst cellen vullen en daarna het formaat instellen.

- **Wat als ik een locale‑specifieke kalender nodig heb (bijv. Thais Boeddhistisch)?**  
  Gebruik de juiste `CultureInfo`‑code (`"th-TH"`), en de formatter respecteert die kalender automatisch.

- **Is er een prestatie‑penalty?**  
  Verwaarloosbaar. De formatter wordt gecached in `WorkbookSettings`, dus de overhead treedt slechts één keer per werkboek op.

## Volledig werkend voorbeeld

Hieronder vind je het complete, kant‑klaar programma dat elke stap uit de tutorial bevat:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Verwachte output in Excel:**

| Cel  | Weergegeven waarde |
|------|--------------------|
| A1   | 令和05.04.21       |
| A2   | 令和06.12.31       |
| A3   | 令和05.04.21 14:45:03 (tijddeel kan variëren) |

Open het bestand, en je ziet de datums precies zoals gedefinieerd.

## Conclusie

Je hebt zojuist geleerd hoe je **aspose cells date format** een werkboek in Java kunt toepassen, van het wijzigen van de locale tot het instellen van een **set custom date format** dat globaal werkt. Door `WorkbookSettings` en `DateTimeFormatter` te gebruiken, krijg je precieze controle over hoe elke datum verschijnt – geen handmatige styling meer nodig.

Vervolgens kun je **how to set date format** voor specifieke kolommen verkennen, of aangepaste getalformaten combineren met conditionele opmaak voor een gepolijste rapportage. Dezelfde principes gelden: definieer een formatter, koppel deze via een stijl, en laat Aspose de rest doen.

Happy coding, en experimenteer gerust met andere locales – je gebruikers zullen je dankbaar zijn voor de verzorgde, cultureel bewuste spreadsheets!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Efficiënt Excel naar PDF converteren met aangepaste datumformaten met Aspose.Cells voor Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Meesterschap in gegevenspresentatie in Excel: getal‑ en aangepaste datumformattering met Aspose.Cells voor Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Hoe Excel‑cellen maken & formatteren met Aspose.Cells voor Java: een stap‑voor‑stap gids](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}