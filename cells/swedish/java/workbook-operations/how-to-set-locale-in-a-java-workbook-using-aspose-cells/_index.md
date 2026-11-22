---
category: general
date: 2026-11-22
description: Lär dig hur du ställer in locale i en Java‑arbetsbok, ändrar arbetsbokens
  språk och sätter kalendern till japanska med tydliga kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: sv
lastmod: 2026-11-22
og_description: Hur du snabbt ställer in locale i en Java-arbetsbok. Följ den här
  handledningen för att ändra arbetsbokens språk, ställa in locale till japanska och
  konfigurera den japanska kalendern.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Hur man ställer in locale i en Java-arbetsbok – steg‑för‑steg‑guide
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
title: Hur man anger locale i en Java-arbetsbok med Aspose.Cells
url: /sv/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man anger språkregion i en Java‑arbetsbok med Aspose.Cells

Att ange språkregion i en Java‑arbetsbok är ett vanligt krav när du behöver anpassa ditt kalkylblad till olika regioner. I den här guiden lär du dig hur du anger språkregion, ändrar arbetsbokens språk och ställer in kalendern till japansk med hjälp av Aspose.Cells‑API:t.

Internationalisering av en arbetsbok går bortom att bara översätta text; det påverkar även talformat, datumparsning och det förvalda kalendersystemet. I slutet av tutorialen kommer du att kunna:

* Konfigurera arbetsbokens språkregion till japanska (Japan) – **set locale to japanese**.  
* Ändra arbetsbokens språk så att formler och UI‑strängar respekterar mål‑kulturen – **change workbook language**.  
* Byta kalender till den japanska kejserliga kalendern – **how to set calendar**.  

Stegen fungerar med vilken recent version som helst av Aspose.Cells för Java (v23.9 eller senare) och kräver bara en standard Java‑utvecklingsmiljö.

## Förutsättningar

| Requirement | Reason |
|-------------|--------|
| Java 8 eller högre | Biblioteket riktar sig mot Java 8+. |
| Aspose.Cells för Java (v23.9+) | Tillhandahåller `Workbook`, `WorkbookSettings` och språkregion‑verktyg. |
| IDE (IntelliJ IDEA, Eclipse eller VS Code) | För att kompilera och köra exemplet. |
| Grundläggande kunskap i Java | Krävs för att förstå kodsnuttarna. |

Lägg till Aspose.Cells Maven‑beroendet i din `pom.xml` (eller ladda ner JAR‑filen manuellt):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Hur man anger språkregion och kalender i en arbetsbok

Det första steget är att skapa en arbetsboksinstans och hämta dess inställningsobjekt. Inställningsobjektet exponerar språkregion‑ och kalender‑API:er.

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

### Varför varje rad är viktig

* **`new Workbook()`** – Skapar en tom arbetsbok som du kan manipulera innan du sparar den.  
* **`getSettings()`** – Returnerar ett `WorkbookSettings`‑objekt; alla regionala alternativ finns här.  
* **`setCalendar(...)`** – Ersätter den förvalda gregorianska kalendern med den japanska kejserliga kalendern, vilket påverkar hur datum renderas och parsas.  
* **`setLocale(new Locale("ja","JP"))`** – Ändrar språk och regionala konventioner (t.ex. månader, decimalavgränsare). Detta är kärnan i **how to set locale** för arbetsboken.  

När programmet körs skapas `LocaleDemo.xlsx`. Öppna den i Excel eller LibreOffice så ser du japanska månadsnamn, japanska yen‑valutasymboler och datum formaterade enligt den japanska kalendern.

## Ändra arbetsbokens språk (ange språkregion till japanska)

Om ditt primära mål är att **change workbook language**, kan du fokusera enbart på anropet `setLocale`. Följande kodsnutt isolerar just det steget:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Vad förändras?**  
* Cellformatsträngar byts till japanska (t.ex. `#,##0.00` blir `#,##0.00` med en yen‑symbol).  
* Inbyggda funktionsnamn (som `SUM`) förblir engelska eftersom Excels funktionsspråk är oberoende, men datumsträngar och felmeddelanden följer japanska konventioner.  

**När ska du använda detta?**  
* När du behöver ett kalkylblad som visar siffror och datum för en japansk publik men den underliggande kalendern kan förbli gregoriansk.  
* För rapporter som exporteras till PDF eller skrivs ut, så att det visuella språket matchar målmarknaden.

## Hur man ställer in kalendern till den japanska kalendern

Ibland är **how to set calendar**‑kravet separat från språkregionen. För äldre system som lagrar datum i den japanska kejserliga eran måste du explicit ange kalendern samtidigt som du eventuellt behåller standard‑språkregionen.

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

**Viktiga punkter:**

* `Calendar.getInstance(Locale.JAPAN)` returnerar ett `java.util.Calendar` konfigurerat för den japanska eran.  
* Arbetsboken kommer nu att rendera datum med erasymboler (R för Reiwa, H för Heisei, osv.).  
* Denna inställning påverkar **inte** talformat eller UI‑språk; kombinera den med `setLocale` om du behöver båda.

## Fullständigt end‑to‑end‑exempel

Nedan är ett komplett, körbart program som demonstrerar **how to set locale**, **change workbook language** och **set the calendar** i ett sammanhängande flöde. Det lägger också till en exempelcell för att illustrera effekten.

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

**Förväntat resultat:**  
När du öppnar `FullJapaneseLocale.xlsx` visas den första cellen med ett datum som `R3/04/01` (Reiwa 3) och den andra cellen formaterad som `¥1,234,567.89`. Detta bekräftar att **how to set locale**, **change workbook language** och **how to set calendar** fungerar tillsammans.

## Vanliga fallgropar och hur du undviker dem

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Använder `Locale.CHINA` istället för `new Locale("ja","JP")` | `Locale.CHINA` sätter kinesiskt språk, inte japanska. | Instansiera alltid `Locale` med `"ja", "JP"` för japanska. |
| Glömmer att anropa `settings.setCalendar(...)` efter `setLocale` | Kalendern återgår till gregoriansk, så datum visas i fel era. | Anropa `setCalendar` **efter** `setLocale`, eller sätt båda samtidigt som i exemplet. |
| Sparar arbetsboken innan inställningarna har tillämpats | Inställningarna appliceras på objektet i minnet; tidig sparning skriver standard‑språkregion. | Tillämpa alla språkregion‑/kalender‑ändringar **innan** du anropar `workbook.save()`. |
| Använder en föråldrad Aspose.Cells‑version | Äldre versioner saknar `setCalendar`‑overloads. | Uppgradera till v23.9+ eller kontrollera release‑noterna för språkregionsstöd. |

## Testa din konfiguration

1. Kör klassen **FullLocaleExample**.  
2. Öppna den genererade `FullJapaneseLocale.xlsx` i Excel.  
3. Verifiera att:  
   * Datumkolumnen visar japanska erasymboler (`R`, `H`, osv.).  
   * Nummerkolumnen använder yen‑symbolen och kommatecken som tusentalsavgränsare.  
   * Eventuella inbyggda felmeddelanden (t.ex. `#DIV/0!`) visas på japanska om arbetsboken innehåller fel.  

Om någon av dessa kontroller misslyckas, dubbelkolla att du har modifierat samma `WorkbookSettings`‑instans som används vid sparning.

## Nästa steg

* **Lokaliserade formler** – Medan språkregionen styr formatering kan du även översätta egna funktionsnamn med `FormulaParser`.  
* **Applicera språkregion på befintliga arbetsböcker** – Läs in en arbetsbok med `new Workbook` ...

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}