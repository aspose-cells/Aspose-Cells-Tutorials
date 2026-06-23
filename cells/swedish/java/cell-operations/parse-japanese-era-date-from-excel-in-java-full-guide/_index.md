---
category: general
date: 2026-06-18
description: Analysera japanskt era‑datum i Java med Aspose.Cells. Lär dig hur du
  läser datum från en Excel‑cell och snabbt extraherar datum och tid från en Excel‑cell.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: sv
og_description: Analysera japanskt era‑datum i Java med Aspose.Cells. Den här guiden
  visar hur du läser datum från en Excel‑cell och extraherar datum och tid från en
  Excel‑cell på bara några steg.
og_title: Analysera japanskt era‑datum från Excel i Java – Komplett handledning
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
title: Analysera japanska eradatum från Excel i Java – Fullständig guide
url: /sv/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Läs in japanskt era‑datum från Excel i Java – Fullständig guide

Har du någonsin behövt **läsa in japanskt era‑datum** som lagras i en Excel‑arbetsbok men inte vet hur du ska omvandla det till ett vanligt gregorianskt `DateTime`? Du är inte ensam – många utvecklare stöter på detta problem när de hanterar äldre japanska bokföringsblad eller myndighetsformulär. Den goda nyheten är att med några rader Java‑kod och rätt bibliotek kan du *read date from Excel cell* och *extract datetime from Excel cell* utan någon manuell strängmanipulation.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar exakt hur du **parse Japanese era date**‑strängar som “令和3年5月10日” till ett Java `java.time.LocalDateTime`. Vi täcker det nödvändiga Maven‑beroendet, förklarar varför du måste aktivera era‑medveten parsning och pekar på vanliga fallgropar. När du är klar har du ett robust, produktionsklart kodsnutt som du kan klistra in i vilket Java‑projekt som helst.

## Förutsättningar

- Java 17 eller nyare (koden fungerar även på Java 8+)
- Maven eller Gradle som byggsystem
- Grundläggande kunskap om Excel‑filer
- **Aspose.Cells for Java**‑biblioteket (gratis provversion räcker för testning)

Om någon av dessa är okänd för dig, oroa dig inte – jag visar exakt hur du lägger till biblioteket och kommer igång.

## Steg 1: Lägg till Aspose.Cells i ditt projekt

Först och främst: du behöver biblioteket som förstår japanska era‑datum. Aspose.Cells sköter det tunga lyftet åt dig.

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

När beroendet är löst kan du börja skriva kod som *reads date from Excel cell* och *extracts datetime from Excel cell*.

## Steg 2: Skapa en Workbook och rikta in dig på det första kalkylbladet

Vi börjar med att skapa en ny arbetsbok i minnet och hämta det första bladet. Detta motsvarar de två första raderna i originalexemplet.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Varför börja med en tom arbetsbok? Det garanterar en ren miljö där vi kan kontrollera varje inställning – kritiskt när du senare aktiverar era‑medveten parsning.

## Steg 3: Sätt in en japansk era‑datumsträng i cell A1

Nu simulerar vi en Excel‑fil som redan innehåller ett japanskt era‑datum. I verkligheten skulle du förmodligen läsa in en befintlig `.xlsx`, men för illustration **skriver** vi själva värdet.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Strängen följer den vanliga japanska notationen: *Era* + *Year* + *Month* + *Day*. Utan extra konfiguration skulle Aspose.Cells behandla detta som ren text, inte som ett datum.

## Steg 4: Aktivera era‑medveten datumparsning

Här kommer den avgörande delen: tala om för arbetsboken att **parse Japanese era date**‑strängar när den stöter på dem. Detta görs via flaggan `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Varför är detta nödvändigt? Som standard antar Aspose.Cells den gregorianska kalendern, så “令和3年5月10日” skulle förbli en sträng. Genom att sätta flaggan instrueras motorn att konvertera den till ett `java.util.Date` (eller motsvarande `java.time`‑typ) under huven.

## Steg 5: Hämta det parsade DateTime‑värdet

Nu när arbetsboken vet hur den ska tolka eran kan vi be cellen om dess `DateTime`‑representation.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Observera att vi **read date from Excel cell** med `cell.getDateTime()`. Metoden returnerar ett `java.util.Date`, som vi omedelbart konverterar till `LocalDateTime` för bättre typ‑säkerhet. Detta uppfyller kravet **extract datetime from excel cell** på ett rent och idiomatiskt sätt.

## Steg 6: Verifiera resultatet

Till sist skriver vi ut det gregorianska datumet för att bekräfta att konverteringen lyckades.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

När du kör programmet bör du se:

```
2021-05-10T00:00
```

Denna utskrift bevisar att vi framgångsrikt **parse Japanese era date**, **read date from Excel cell** och **extract datetime from Excel cell** i ett enda flöde.

## Hantera verkliga edge‑cases

### Flera eror

Japan har haft flera eror (Meiji, Taishō, Shōwa, Heisei, Reiwa). Flaggan `setParseDateUsingJapaneseEra(true)` täcker alla automatiskt, men var medveten om att äldre datum kan ligga utanför bibliotekets stödda intervall (vanligtvis 1868‑nutid). Om du stöter på ett datum som “昭和45年12月31日” konverteras det till 1970‑12‑31.

### Tomma eller ogiltiga celler

Om en cell är tom eller innehåller en felaktig sträng kastar `cell.getDateTime()` ett `CellsException`. Skydda dig mot detta med en enkel kontroll:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Tidskomponent

Exemplet innehåller bara ett datum, men om din Excel‑fil även lagrar tid (t.ex. “令和3年5月10日 14:30”) bevarar Aspose.Cells tidsdelen. `LocalDateTime` du får tillbaka kommer då att inkludera timmar, minuter och sekunder.

## Fullständigt fungerande exempel

Sätter vi ihop allt får du följande kompletta, copy‑and‑paste‑klara program:

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

Spara detta som `JapaneseEraDateParser.java`, kompilera med `javac` och kör med `java`. Om allt är korrekt konfigurerat ser du det gregorianska datumet skrivet i konsolen.

## Pro‑tips & vanliga fallgropar

- **Pro‑tips:** Sätt alltid `setParseDateUsingJapaneseEra(true)` **innan** du läser några cellvärden. Att ändra flaggan efter att en cell lästs omvandlar inte värdet retroaktivt.
- **Tänk på locale:** Biblioteket parsar era‑strängar baserat på Unicode‑tecken, så du behöver inte explicit ange en japansk locale.
- **Prestanda:** Att aktivera era‑parsning ger en liten overhead. Om du bara behöver det för ett fåtal celler kan du tillfälligt slå på flaggan, läsa cellerna och sedan slå av den igen.
- **Testning:** Använd Asposes gratis provversion för att validera mot en riktig Excel‑fil som innehåller flera era‑datum. Detta säkerställer att din produktionskod beter sig som förväntat.

## Slutsats

Vi har just demonstrerat hur du **parse Japanese era date**‑värden direkt från en Excel‑arbetsbok med Java och Aspose.Cells. Genom att aktivera era‑medveten parsning kan du **read date from Excel cell** och **extract datetime from Excel cell** på ett rent, typ‑säkert sätt. Metoden fungerar för alla moderna japanska eror, hanterar tidskomponenter och tar elegant hand om ogiltiga data.

Redo för nästa utmaning? Prova att läsa in en riktig `.xlsx`‑fil som innehåller en blandning av gregorianska och japanska era‑datum, eller experimentera med att formatera den resulterande `LocalDateTime` till strängar som matchar din locale. Du kan också utforska att skriva tillbaka de konverterade datumen till Excel för downstream‑system som bara förstår gregorianska datum.

Har du frågor eller stött på ett märkligt edge‑case? Lämna en kommentar nedan, och happy coding!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}