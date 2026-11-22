---
category: general
date: 2026-11-22
description: Leer hoe je de locale instelt in een Java-werkmap, de taal van de werkmap
  wijzigt en de kalender op Japans zet, met duidelijke codevoorbeelden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: nl
lastmod: 2026-11-22
og_description: Hoe je snel de locale in een Java-werkmap instelt. Volg deze tutorial
  om de taal van de werkmap te wijzigen, de locale op Japans in te stellen en de Japanse
  kalender te configureren.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Hoe je de locale instelt in een Java-werkmap – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Hoe de locale instellen in een Java-werkmap met Aspose.Cells
url: /nl/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe locale instellen in een Java-werkmap met Aspose.Cells

Locale instellen in een Java-werkmap is een veelvoorkomende vereiste wanneer je je spreadsheet moet aanpassen aan verschillende regio's. In deze gids leer je hoe je de locale instelt, de werkmaptaal wijzigt en de kalender op Japans zet met behulp van de Aspose.Cells API.

Het internationaliseren van een werkmap gaat verder dan het vertalen van tekst; het beïnvloedt ook getalformaten, datumparsing en het standaard kalendersysteem. Aan het einde van deze tutorial kun je:

* De locale van de werkmap configureren naar Japans (Japan) – **set locale to japanese**.  
* De werkmaptaal wijzigen zodat formules en UI‑strings de doeltaal respecteren – **change workbook language**.  
* De kalender overschakelen naar de Japanse keizerlijke kalender – **how to set calendar**.  

De stappen werken met elke recente versie van Aspose.Cells voor Java (v23.9 of later) en vereisen alleen een standaard Java‑ontwikkelomgeving.

## Vereisten

| Vereiste | Reden |
|----------|-------|
| Java 8 of hoger | De bibliotheek richt zich op Java 8+. |
| Aspose.Cells for Java (v23.9+) | Biedt `Workbook`, `WorkbookSettings` en locale‑hulpmiddelen. |
| IDE (IntelliJ IDEA, Eclipse, of VS Code) | Voor het compileren en uitvoeren van het voorbeeld. |
| Basiskennis van Java | Nodig om de codefragmenten te begrijpen. |

Voeg de Aspose.Cells Maven‑dependency toe aan je `pom.xml` (of download de JAR handmatig):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Hoe locale en kalender in een werkmap instellen

De eerste stap is het maken van een workbook‑instance en het verkrijgen van het instellingen‑object. Het instellingen‑object biedt de locale‑ en kalender‑API's.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Waarom elke regel belangrijk is

* **`new Workbook()`** – Maakt een lege werkmap aan die je kunt manipuleren vóór het opslaan.  
* **`getSettings()`** – Retourneert een `WorkbookSettings`‑object; alle regionale opties bevinden zich hier.  
* **`setCalendar(...)`** – Vervangt de standaard Gregoriaanse kalender door de Japanse keizerlijke kalender, wat invloed heeft op hoe datums worden weergegeven en geparseerd.  
* **`setLocale(new Locale("ja","JP"))`** – Wijzigt de taal en regionale conventies (bijv. maanden, decimaal‑scheidingstekens). Dit is de kern van **how to set locale** voor de werkmap.  

Het uitvoeren van het programma maakt `LocaleDemo.xlsx` aan. Open het in Excel of LibreOffice en je zult Japanse maandnamen, Japanse Yen‑valutasymbolen en datums zien die zijn opgemaakt volgens de Japanse kalender.

## Werkmaptaal wijzigen (locale instellen op Japans)

Als je primaire doel is om **de werkmaptaal te wijzigen**, kun je je alleen op de `setLocale`‑aanroep richten. Het volgende fragment isoleert die stap:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Wat verandert er?**  
* Celopmaak‑strings schakelen over naar Japans (bijv. `#,##0.00` wordt `#,##0.00` met een yen‑symbool).  
* Ingebouwde functienamen (zoals `SUM`) blijven Engels omdat de functie‑locale van Excel onafhankelijk is, maar datum‑strings en foutmeldingen volgen Japanse conventies.  

**Wanneer gebruik je dit?**  
* Wanneer je een spreadsheet nodig hebt die cijfers en datums weergeeft voor een Japans publiek, maar de onderliggende kalender Gregorian kan blijven.  
* Voor rapporten die naar PDF worden geëxporteerd of afgedrukt, zodat de visuele taal overeenkomt met de doellmarkt.

## Hoe de kalender instellen op de Japanse kalender

Soms is de **how to set calendar**‑vereiste gescheiden van de locale. Voor legacy‑systemen die datums opslaan in het Japanse keizerlijke tijdperk, moet je de kalender expliciet instellen, eventueel met de standaard locale behouden.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Belangrijke punten:**  
* `Calendar.getInstance(Locale.JAPAN)` retourneert een `java.util.Calendar` geconfigureerd voor het Japanse tijdperk.  
* De werkmap zal nu datums weergeven met era‑symbolen (R voor Reiwa, H voor Heisei, enz.).  
* Deze instelling heeft **geen** invloed op getalopmaak of UI‑taal; combineer het met `setLocale` als je beide nodig hebt.  

## Volledig end‑to‑end voorbeeld

Hieronder staat een volledig, uitvoerbaar programma dat **how to set locale**, **change workbook language** en **set the calendar** in één samenhangende stroom demonstreert. Het voegt ook een voorbeeldcel toe om het effect te illustreren.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Verwachte output:**  
Het openen van `FullJapaneseLocale.xlsx` toont de eerste cel met een datum zoals `R3/04/01` (Reiwa 3) en de tweede cel opgemaakt als `¥1,234,567.89`. Dit bevestigt dat **how to set locale**, **change workbook language**, en **how to set calendar** allemaal samenwerken.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| `Locale.CHINA` gebruiken in plaats van `new Locale("ja","JP")` | `Locale.CHINA` stelt de Chinese taal in, niet Japans. | Instantieer `Locale` altijd met `"ja", "JP"` voor Japans. |
| Vergeten `settings.setCalendar(...)` aan te roepen na `setLocale` | De kalender standaard naar Gregorian, waardoor datums in de verkeerde era verschijnen. | Roep `setCalendar` **na** het instellen van de locale aan, of stel beide tegelijk in zoals getoond. |
| De werkmap opslaan vóór het toepassen van instellingen | Instellingen worden toegepast op het in‑memory object; vroeg opslaan schrijft de standaard locale. | Pas alle locale-/kalender‑wijzigingen toe **voordat** `workbook.save()` wordt aangeroepen. |
| Een verouderde Aspose.Cells‑versie gebruiken | Oudere versies missen `setCalendar`‑overloads. | Upgrade naar v23.9+ of controleer de release‑notes voor locale‑ondersteuning. |

## Je configuratie testen

1. Voer de **FullLocaleExample**‑klasse uit.  
2. Open het gegenereerde `FullJapaneseLocale.xlsx` in Excel.  
3. Controleer dat:  
   * De datumkolom Japanse era‑symbolen toont (`R`, `H`, etc.).  
   * De getalkolom het Yen‑symbool en komma‑scheidingstekens gebruikt.  
   * Eventuele ingebouwde foutmeldingen (bijv. `#DIV/0!`) in het Japans verschijnen als de werkmap fouten bevat.  

Als een van deze controles faalt, controleer dan dubbel dat het `WorkbookSettings`‑object dat je hebt aangepast dezelfde instantie is die bij het opslaan wordt gebruikt.

## Volgende stappen

* **Formules lokaliseren** – Terwijl de locale opmaak regelt, kun je ook aangepaste functienamen vertalen met `FormulaParser`.  
* **Locale toepassen op bestaande werkmappen** – Laad een werkmap met `new Workbook

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose Cells datumformaat: hoe aangepaste datumopmaak instellen in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Hoe taal instellen in Excel‑bestanden met Aspose.Cells .NET voor meertalige ondersteuning](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Hoe celnummeropmaak instellen en Japanse datums converteren in C# met Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}