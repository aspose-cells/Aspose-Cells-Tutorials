---
category: general
date: 2026-10-07
description: Läs datum från Excel i Java med Aspose.Cells. Denna guide visar hur du
  parsar japanska eradatumen, läser datum från Excel-celler och extraherar datum och
  tid från Excel-celler snabbt.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Läs datum från Excel i Java med Aspose.Cells. Denna guide visar hur
  du parsar japanska eradatumen, läser datum från Excel-celler och extraherar datum
  och tid från Excel-celler på bara några få steg.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Läs datum från Excel i Java med Aspose.Cells – fullständig guide
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
title: Läs datum från Excel i Java med Aspose.Cells – fullständig guide
url: /sv/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Läs datum från Excel i Java med Aspose.Cells – fullständig guide

Om du behöver **read date from Excel** kalkylblad som innehåller japanska era‑strängar, har du kommit till rätt ställe. I många äldre bokförings‑ eller myndighetskalkylblad lagras datumet som “令和3年5月10日”, och att konvertera det till en standard Gregorian `LocalDateTime` kan vara felbenäget. Denna handledning visar dig, steg för steg, hur du aktiverar era‑medveten parsning, läser cellvärdet och **extract datetime from Excel** med Aspose.Cells för Java.

## Snabba svar
- **Vilket bibliotek hanterar japanska era‑datum?** Aspose.Cells for Java.
- **Vilken Java‑version krävs?** Java 17 or newer (Java 8 works as well).
- **Behöver jag en licens för testning?** A free trial is sufficient for development.
- **Kan samma kod läsa Gregorian‑datum?** Yes, the API automatically detects the format.
- **Bevaras tidsinformation?** Absolutely – hours, minutes, and seconds survive the conversion.

## Vad är read date from Excel?
Frasen “read date from Excel” avser att hämta ett cells datumvärde och konvertera det till ett Java datum‑tid‑objekt såsom `java.time.LocalDateTime`. Aspose.Cells abstraherar det lågnivå Excel‑binära formatet, så du kan arbeta med datum utan manuell strängparsning.

## Varför använda Aspose.Cells för japansk era‑parsning?
Aspose.Cells stödjer **50+ in‑ och utdataformat** och kan bearbeta arbetsböcker med flera hundra sidor utan att ladda hela filen i minnet. Dess inbyggda era‑medvetna parser konverterar varje japansk era (Meiji, Taishō, Shōwa, Heisei, Reiwa) till Gregorian‑datum i ett enda API‑anrop, vilket eliminerar skört regular‑expression‑kod.

## Förutsättningar
- Java 17 (or Java 8+) installerat på din maskin.
- Maven‑ eller Gradle‑byggsystem.
- Grundläggande kunskap om Excel‑filer.
- Aspose.Cells för Java‑bibliotek (trial or licensed version).

Om någon av dessa känns obekant, oroa dig inte — du kommer att se exakt hur du lägger till biblioteket i nästa steg.

## Hur man läser datum från Excel i Java?
Läs in din arbetsbok, aktivera era‑medveten parsning och be cellen om dess `DateTime`‑värde. Hela processen tar **två rader funktionell kod** när biblioteket finns på classpath.

### Steg 1: lägg till Aspose.Cells i ditt projekt

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

Efter att beroendet har lösts kan du börja använda API‑et för att **read date from Excel** celler.

### Steg 2: skapa en arbetsbok och rikta in dig på det första kalkylbladet

`Workbook`‑klassen representerar en hel Excel‑fil i minnet. Att skapa en ny instans garanterar en ren miljö för de efterföljande parsningsstegen.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Steg 3: placera en japansk era‑datumsträng i cell A1

För demonstration skriver vi era‑strängen själva; i produktion skulle du ladda en befintlig `.xlsx`.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Texten följer det konventionella japanska mönstret: *Era* + *Year* + *Month* + *Day*.

### Steg 4: aktivera era‑medveten datumparsning

Berätta för Aspose.Cells att behandla era‑strängar som datum genom att sätta flaggan `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` är en egenskap som, när den är sann, möjliggör automatisk konvertering av japanska era‑strängar till Gregorian‑datum.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Utan denna flagga skulle biblioteket behandla “令和3年5月10日” som vanlig text, och du skulle förlora den automatiska konverteringen.

### Steg 5: hämta det parsade DateTime‑värdet

Be cellen nu om dess datumrepresentation. `cell.getDateTime()` returnerar cellens värde som ett `java.util.Date`‑objekt. Metoden returnerar ett `java.util.Date`, som vi omedelbart konverterar till den moderna `java.time.LocalDateTime`. `LocalDateTime` är en Java‑klass som representerar datum och tid utan en tidszon.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Detta uppfyller **extract datetime from Excel**‑kravet på ett typ‑säkert sätt.

### Steg 6: verifiera resultatet

Skriv ut Gregorian‑datumet för att bekräfta att konverteringen lyckades.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

When you run the program you should see:

```
2021-05-10T00:00
```

Utdata visar att vi framgångsrikt **read date from Excel**, parsade den japanska eran och **extracted datetime from Excel** i ett enda flöde.

## Hantera verkliga edge‑case

### Flera eror

Japan har haft flera eror (Meiji, Taishō, Shōwa, Heisei, Reiwa). Flaggan `setParseDateUsingJapaneseEra(true)` täcker alla automatiskt, men var medveten om att äldre datum kan ligga utanför bibliotekets stödområde (vanligtvis 1868‑nutid). Om du stöter på ett datum som “昭和45年12月31日”, kommer samma kod att konvertera det till 1970‑12‑31.

### Tomma eller ogiltiga celler

Om en cell är tom eller innehåller en felaktig sträng, kastar `cell.getDateTime()` ett `CellsException`. Skydda mot detta med en enkel kontroll:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Tidskomponent

Exemplet innehåller bara ett datum, men om din Excel‑fil också lagrar tid (t.ex. “令和3年5月10日 14:30”), kommer Aspose.Cells att bevara tidsdelen. `LocalDateTime` du får kommer att inkludera timmar, minuter och sekunder.

## Fullt fungerande exempel

När allt sätts ihop, här är det kompletta, kopiera‑och‑klistra‑klara programmet:

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

Spara detta som `JapaneseEraDateParser.java`, kompilera med `javac` och kör med `java`. Om allt är korrekt konfigurerat kommer du att se Gregorian‑datumet skrivet till konsolen.

## Pro‑tips & vanliga fallgropar

- **Pro tip:** Aktivera `setParseDateUsingJapaneseEra(true)` **innan** du läser några cellvärden. Att ändra flaggan senare konverterar inte redan‑lästa celler retroaktivt.
- **Locale note:** Parsaren arbetar på Unicode‑tecknen själva, så du behöver inte explicit sätta en japansk locale.
- **Performance:** Era‑parsning lägger till en försumbar overhead. Om du bara behöver den för några få celler, slå på flaggan bara för dessa läsningar.
- **Testing:** Använd Asposes gratisprov för att validera mot en riktig arbetsbok som blandar Gregorian‑ och era‑datum. Detta säkerställer att produktionskoden beter sig som förväntat.

## Vanliga frågor

**Q: Kan jag använda detta tillvägagångssätt med en befintlig .xlsx‑fil?**  
A: Ja. Ladda filen med `new Workbook("path/to/file.xlsx")` och samma flagga kommer att parsra eventuella era‑strängar den hittar.

**Q: Vad händer om cellen innehåller ett Gregorian‑datum?**  
A: Biblioteket returnerar Gregorian‑värdet oförändrat; era‑parsning påverkar bara strängar som matchar era‑mönstret.

**Q: Stöder Aspose.Cells datum tidigare än Meiji (1868)?**  
A: Nej. Datum före 1868 ligger utanför det stödda intervallet och kommer att behandlas som vanlig text.

**Q: Hur hanterar jag stora arbetsböcker utan att tömma minnet?**  
A: Använd `Workbook`‑konstruktorn som accepterar `LoadOptions` med `setMemorySetting(MemorySetting.MemoryPreference)` för att strömma data istället för att ladda allt på en gång.

**Q: Krävs en kommersiell licens för produktionsanvändning?**  
A: Ja, en giltig Aspose.Cells‑licens tar bort utvärderingsbegränsningar och möjliggör full prestanda.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska 1904-datumsystemet i Excel med Aspose.Cells Java för effektiva celloperationer](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Konvertera Excel till PDF effektivt med anpassade datumformat med Aspose.Cells för Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Hur man väljer cellområden i Excel med Aspose.Cells för Java (2023‑guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

**Senast uppdaterad:** 2026-10-07  
**Testat med:** Aspose.Cells 24.12 för Java  
**Författare:** Aspose

## Relaterade handledningar

- [Analysera japanskt era‑datum från Excel i Java – fullständig guide](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Läs Excel‑fil i Java med Aspose.Cells – komplett guide](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Spara Excel‑arbetsbok med Aspose.Cells för Java – komplett guide](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}