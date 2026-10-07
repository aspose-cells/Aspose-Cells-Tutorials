---
category: general
date: 2026-06-18
description: Parse Japanse era‑datum in Java met Aspose.Cells. Leer hoe je een datum
  uit een Excel‑cel leest en snel een datum/tijd uit een Excel‑cel extraheert.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: nl
og_description: Parse Japanse era datum in Java met Aspose.Cells. Deze gids laat zien
  hoe je een datum uit een Excel-cel leest en een datum‑tijd uit een Excel-cel extraheert
  in slechts een paar stappen.
og_title: Japanse jaartijd datum parseren uit Excel in Java – Complete tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: Japanse era datum uit Excel in Java parseren – volledige gids
url: /nl/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanse jaartijd datum uit Excel in Java parseren – Volledige gids

Heb je ooit moeten **parse Japanese era date** die is opgeslagen in een Excel-werkmap, maar wist je niet hoe je het naar een reguliere Gregoriaanse `DateTime` kon omzetten? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan bij het werken met oude Japanse boekhoudbladen of overheidsformulieren. Het goede nieuws is dat je met een paar regels Java en de juiste bibliotheek **date from Excel cell** kunt lezen en **datetime from Excel cell** kunt extraheren zonder handmatige stringmanipulatie.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat precies laat zien hoe je **parse Japanese era date** strings zoals “令和3年5月10日” omzet naar een Java `java.time.LocalDateTime`. We behandelen de benodigde Maven‑dependency, leggen uit waarom je era‑bewuste parsing moet inschakelen, en wijzen op veelvoorkomende valkuilen. Aan het einde heb je een solide, productie‑klare snippet die je in elk Java‑project kunt gebruiken.

## Vereisten

- Java 17 of nieuwer (de code werkt ook op Java 8+)
- Maven‑ of Gradle‑buildsysteem
- Basiskennis van Excel‑bestanden
- De **Aspose.Cells for Java**‑bibliotheek (gratis proefversie werkt voor testen)

Als een van deze onbekend klinkt, geen zorgen—ik laat je precies zien hoe je de bibliotheek toevoegt en aan de slag gaat.

## Stap 1: Voeg Aspose.Cells toe aan je project

Allereerst: je hebt de bibliotheek nodig die Japanse jaartijddatums begrijpt. Aspose.Cells doet het zware werk voor je.

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Zodra de dependency is opgelost, kun je code gaan schrijven die *reads date from Excel cell* en *extracts datetime from Excel cell*.

## Stap 2: Maak een Workbook en richt je op het eerste werkblad

We beginnen met het creëren van een nieuw workbook in het geheugen en pakken het eerste blad. Dit weerspiegelt de eerste twee regels van het originele voorbeeld.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Waarom starten met een fris workbook? Het garandeert een schone omgeving waarin we elke instelling kunnen controleren—cruciaal wanneer je later era‑bewuste parsing inschakelt.

## Stap 3: Plaats een Japanse jaartijd datumstring in cel A1

Nu simuleren we een Excel‑bestand dat al een Japanse jaartijddatum bevat. In de praktijk laad je waarschijnlijk een bestaande `.xlsx`, maar voor illustratie **write** we de waarde zelf.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

De string volgt de standaard Japanse notatie: *Era* + *Year* + *Month* + *Day*. Zonder extra configuratie zou Aspose.Cells dit behandelen als platte tekst, niet als datum.

## Stap 4: Schakel era‑bewuste datumparsing in

Hier is het cruciale deel: vertel het workbook om **parse Japanese era date** strings te verwerken wanneer het ze tegenkomt. Dit gebeurt via de `ParseDateUsingJapaneseEra`‑vlag.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Waarom is dit nodig? Standaard gaat Aspose.Cells uit van de Gregoriaanse kalender, dus “令和3年5月10日” zou als string blijven staan. Het inschakelen van de vlag instrueert de engine om het onder de motorkap om te zetten naar een `java.util.Date` (of het `java.time`‑equivalent).

## Stap 5: Haal de geparseerde DateTime-waarde op

Nu het workbook weet hoe het de era moet interpreteren, kunnen we de cel vragen om zijn `DateTime`‑representatie.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Let op: we **read date from Excel cell** met `cell.getDateTime()`. De methode retourneert een `java.util.Date`, die we meteen omzetten naar `LocalDateTime` voor betere type‑veiligheid. Dit voldoet aan de **extract datetime from excel cell**‑vereiste op een nette, idiomatische manier.

## Stap 6: Verifieer het resultaat

Tot slot printen we de Gregoriaanse datum om de succesvolle conversie te bevestigen.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Wanneer je het programma uitvoert, zou je moeten zien:

```
2021-05-10T00:00
```

Die output bewijst dat we succesvol **parse Japanese era date**, **read date from Excel cell**, en **extract datetime from excel cell** hebben uitgevoerd in één doorlopend proces.

## Omgaan met real‑world randgevallen

### Meerdere era's

Japan heeft verschillende era's gekend (Meiji, Taishō, Shōwa, Heisei, Reiwa). De `setParseDateUsingJapaneseEra(true)`‑vlag dekt ze allemaal automatisch, maar houd er rekening mee dat oudere data buiten het ondersteunde bereik van de bibliotheek kunnen vallen (meestal 1868‑heden). Als je een datum tegenkomt zoals “昭和45年12月31日”, zal dezelfde code deze omzetten naar 1970‑12‑31.

### Lege of ongeldige cellen

Als een cel leeg is of een onjuiste string bevat, gooit `cell.getDateTime()` een `CellsException`. Bescherm je code met een eenvoudige controle:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Tijdcomponent

Het voorbeeld bevat alleen een datum, maar als je Excel‑bestand ook tijd opslaat (bijv. “令和3年5月10日 14:30”), zal Aspose.Cells het tijdgedeelte behouden. De `LocalDateTime` die je ontvangt bevat uren, minuten en seconden.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het complete, copy‑and‑paste‑klare programma:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Sla dit op als `JapaneseEraDateParser.java`, compileer met `javac` en voer uit met `java`. Als alles correct is ingesteld, zie je de Gregoriaanse datum in de console verschijnen.

## Pro‑tips & veelvoorkomende valkuilen

- **Pro tip:** Zet `setParseDateUsingJapaneseEra(true)` **before** je enige celwaarden leest. De vlag later wijzigen converteert een reeds gelezen waarde niet retroactief.
- **Watch out for locale:** De bibliotheek parseert era‑strings op basis van Unicode‑tekens, dus je hoeft geen Japanse locale expliciet in te stellen.
- **Performance note:** Era‑parsing voegt een kleine overhead toe. Als je het slechts voor een handvol cellen nodig hebt, kun je de vlag tijdelijk aanzetten, de cellen lezen, en daarna weer uitschakelen.
- **Testing:** Gebruik de gratis proefversie van Aspose om te valideren met een echt Excel‑bestand dat meerdere era‑datums bevat. Zo weet je zeker dat je productiecodel zich gedraagt zoals verwacht.

## Conclusie

We hebben zojuist laten zien hoe je **parse Japanese era date**‑waarden direct uit een Excel‑werkmap kunt halen met Java en Aspose.Cells. Door era‑bewuste parsing in te schakelen, kun je **read date from Excel cell** en **extract datetime from Excel cell** op een nette, type‑veilige manier. De aanpak werkt voor elke moderne Japanse era, behandelt tijdcomponenten, en gaat elegant om met ongeldige data.

Klaar voor de volgende uitdaging? Probeer een echte `.xlsx` te laden die een mix van Gregoriaanse en Japanse jaartijddatums bevat, of experimenteer met het formatteren van de resulterende `LocalDateTime` naar strings die bij jouw locale passen. Je kunt ook onderzoeken hoe je de geconverteerde datums terug naar Excel schrijft voor downstream‑systemen die alleen Gregoriaanse datums begrijpen.

Heb je vragen of ben je een eigenzinnige randvoorwaarde tegengekomen? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}