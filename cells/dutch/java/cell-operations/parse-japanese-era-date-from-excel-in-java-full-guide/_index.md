---
category: general
date: 2026-10-07
description: Datum lezen uit Excel in Java met Aspose.Cells. Deze gids laat zien hoe
  je Japanese era dates kunt parseren, datum uit Excel-cellen kunt lezen en datetime
  uit Excel-cellen snel kunt extraheren.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Datum lezen uit Excel in Java met Aspose.Cells. Deze gids laat zien
  hoe je Japanese era dates kunt parseren, datum uit Excel-cellen kunt lezen en datetime
  uit Excel-cellen in slechts een paar stappen kunt extraheren.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Datum lezen uit Excel in Java met Aspose.Cells – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
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
- read date from excel
- java excel date conversion
title: Datum lezen uit Excel in Java met Aspose.Cells – volledige gids
url: /nl/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lees datum uit Excel in Java met Aspose.Cells – volledige gids

Als je **datum uit Excel** wilt lezen uit werkbladen die Japanse era‑strings bevatten, ben je hier op het juiste adres. In veel legacy‑boekhoud‑ of overheids‑spreadsheets wordt de datum opgeslagen als “令和3年5月10日”, en het omzetten daarvan naar een standaard Gregoriaanse `LocalDateTime` kan foutgevoelig zijn. Deze tutorial laat je stap voor stap zien hoe je era‑bewuste parsing inschakelt, de celwaarde leest, en **datetime uit Excel haalt** met Aspose.Cells voor Java.

## Snelle antwoorden
- **Welke bibliotheek verwerkt Japanse era‑datums?** Aspose.Cells voor Java.
- **Welke Java‑versie is vereist?** Java 17 of nieuwer (Java 8 werkt ook).
- **Heb ik een licentie nodig voor testen?** Een gratis trial is voldoende voor ontwikkeling.
- **Kan dezelfde code Gregoriaanse datums lezen?** Ja, de API detecteert het formaat automatisch.
- **Wordt tijdinformatie bewaard?** Absoluut – uren, minuten en seconden blijven behouden bij de conversie.

## Wat is datum lezen uit Excel?
De uitdrukking “datum uit Excel lezen” verwijst naar het ophalen van de datumwaarde van een cel en deze omzetten naar een Java‑datum‑tijdobject zoals `java.time.LocalDateTime`. Aspose.Cells abstraheert het low‑level Excel‑binaire formaat, zodat je met datums kunt werken zonder handmatige string‑parsing.

## Waarom Aspose.Cells gebruiken voor Japanese era parsing?
Aspose.Cells ondersteunt **50+ invoer‑ en uitvoerformaten** en kan werkboeken van honderden pagina’s verwerken zonder het volledige bestand in het geheugen te laden. De ingebouwde era‑bewuste parser zet elke Japanse era (Meiji, Taishō, Shōwa, Heisei, Reiwa) om naar Gregoriaanse datums met één API‑aanroep, waardoor breekbare reguliere‑expressie‑code wordt geëlimineerd.

## Vereisten
- Java 17 (of Java 8+) geïnstalleerd op je machine.
- Maven‑ of Gradle‑buildsysteem.
- Basiskennis van Excel‑bestanden.
- Aspose.Cells voor Java‑bibliotheek (trial of gelicentieerde versie).

Als een van deze punten onbekend is, maak je geen zorgen – je ziet precies hoe je de bibliotheek in de volgende stap toevoegt.

## Hoe datum uit Excel lezen in Java?

Laad je werkmap, schakel era‑bewuste parsing in, en vraag de cel om zijn `DateTime`‑waarde. Het hele proces bestaat uit **twee regels functionele code** zodra de bibliotheek op het classpath staat.

### Stap 1: voeg Aspose.Cells toe aan je project

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

Na het oplossen van de afhankelijkheid kun je de API gebruiken om **datum uit Excel**‑cellen te lezen.

### Stap 2: maak een werkmap en richt je op het eerste werkblad

De `Workbook`‑klasse vertegenwoordigt een volledig Excel‑bestand in het geheugen. Het maken van een nieuwe instantie garandeert een schone omgeving voor de daaropvolgende parsing‑stappen.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Stap 3: zet een Japanse era‑datumstring in cel A1

Voor demonstratie schrijven we zelf de era‑string; in productie laad je een bestaand `.xlsx`.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

De tekst volgt het conventionele Japanse patroon: *Era* + *Jaar* + *Maand* + *Dag*.

### Stap 4: schakel era‑bewuste datumparsing in

Vertel Aspose.Cells era‑strings als datums te behandelen door de `ParseDateUsingJapaneseEra`‑vlag in te stellen.  
`ParseDateUsingJapaneseEra` is een eigenschap die, wanneer true, automatische conversie van Japanse era‑strings naar Gregoriaanse datums inschakelt.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Zonder deze vlag zou de bibliotheek “令和3年5月10日” als platte tekst behandelen, en zou je de automatische conversie verliezen.

### Stap 5: haal de geparseerde DateTime‑waarde op

Vraag nu de cel om zijn datumrepresentatie. `cell.getDateTime()` retourneert de celwaarde als een `java.util.Date`‑object. De methode geeft een `java.util.Date` terug, die we direct omzetten naar de moderne `java.time.LocalDateTime`. `LocalDateTime` is een Java‑klasse die datum en tijd zonder tijdzone vertegenwoordigt.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Dit voldoet aan de **extract datetime from Excel**‑vereiste op een type‑veilige manier.

### Stap 6: controleer het resultaat

Print de Gregoriaanse datum om de conversie te bevestigen.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Wanneer je het programma uitvoert, zie je:

```
2021-05-10T00:00
```

De output bewijst dat we succesvol **datum uit Excel** hebben gelezen, de Japanse era hebben geparseerd, en **datetime uit Excel** in één stroom hebben geëxtraheerd.

## Reële randgevallen afhandelen

### Meerdere era's

Japan heeft verschillende era's (Meiji, Taishō, Shōwa, Heisei, Reiwa). De `setParseDateUsingJapaneseEra(true)`‑vlag dekt ze allemaal automatisch, maar houd er rekening mee dat oudere datums buiten het ondersteunde bereik van de bibliotheek kunnen vallen (meestal 1868‑heden). Als je een datum tegenkomt zoals “昭和45年12月31日”, zet dezelfde code deze om naar 1970‑12‑31.

### Lege of ongeldige cellen

Als een cel leeg is of een misvormde string bevat, gooit `cell.getDateTime()` een `CellsException`. Bescherm je code met een eenvoudige controle:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Tijdcomponent

Het voorbeeld bevat alleen een datum, maar als je Excel‑bestand ook tijd opslaat (bijv. “令和3年5月10日 14:30”), zal Aspose.Cells het tijdgedeelte behouden. De `LocalDateTime` die je ontvangt, bevat uren, minuten en seconden.

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

Sla dit op als `JapaneseEraDateParser.java`, compileer met `javac`, en voer uit met `java`. Als alles correct is ingesteld, zie je de Gregoriaanse datum op de console geprint.

## Pro‑tips & veelvoorkomende valkuilen

- **Pro‑tip:** Schakel `setParseDateUsingJapaneseEra(true)` **vóór** het lezen van celwaarden in. De vlag later wijzigen converteert niet retroactief reeds gelezen cellen.
- **Locale‑opmerking:** De parser werkt op de Unicode‑tekens zelf, dus je hoeft geen Japanse locale expliciet in te stellen.
- **Prestaties:** Era‑parsing voegt een verwaarloosbare overhead toe. Als je het alleen voor een paar cellen nodig hebt, zet de vlag alleen voor die reads aan.
- **Testen:** Gebruik de gratis trial van Aspose om te valideren tegen een echt werkboek dat zowel Gregoriaanse als era‑datums bevat. Zo weet je zeker dat de productiecodelogica correct werkt.

## Veelgestelde vragen

**Q: Kan ik deze aanpak gebruiken met een bestaand .xlsx‑bestand?**  
A: Ja. Laad het bestand met `new Workbook("path/to/file.xlsx")` en dezelfde vlag parseert alle era‑strings die het tegenkomt.

**Q: Wat gebeurt er als de cel een Gregoriaanse datum bevat?**  
A: De bibliotheek retourneert de Gregoriaanse waarde ongewijzigd; era‑parsing beïnvloedt alleen strings die aan het era‑patroon voldoen.

**Q: Ondersteunt Aspose.Cells datums vóór Meiji (1868)?**  
A: Nee. Datums vóór 1868 vallen buiten het ondersteunde bereik en worden als platte tekst behandeld.

**Q: Hoe ga ik om met grote werkboeken zonder het geheugen te overbelasten?**  
A: Gebruik de `Workbook`‑constructor die `LoadOptions` accepteert met `setMemorySetting(MemorySetting.MemoryPreference)` om data te streamen in plaats van alles tegelijk te laden.

**Q: Is een commerciële licentie vereist voor productiegebruik?**  
A: Ja, een geldige Aspose.Cells‑licentie verwijdert evaluatiebeperkingen en biedt volledige prestaties.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Laatst bijgewerkt:** 2026-10-07  
**Getest met:** Aspose.Cells 24.12 voor Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Parse Japanese Era Date From Excel In Java Full Guide](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Read Excel File Java with Aspose.Cells – Complete Guide](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}