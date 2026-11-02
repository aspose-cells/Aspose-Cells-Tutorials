---
category: general
date: 2026-06-30
description: Ställ in anpassat talformat i Excel med Java. Lär dig hur du skapar en
  Excel‑arbetsbok i Java, hämtar datum/tid från en cell, beräknar arbetsbokens formler
  och skriver ut datum/tidsvärdet.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: sv
og_description: Ställ in anpassat talformat i Excel med Java. Denna guide visar hur
  man skapar en Excel-arbetsbok i Java, hämtar datum/tid från en cell, beräknar arbetsboksformler
  och skriver ut datum/tidsvärdet.
og_title: Ställ in anpassat talformat i Excel med Java – Fullständig handledning
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Ställ in anpassat talformat i Excel med Java – Komplett guide
url: /sv/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa talformat i Excel med Java – Komplett guide

Har du någonsin behövt **set custom number format** i ett Excel‑ark medan du arbetar i Java? Du är inte ensam. Oavsett om du bygger en rapporteringsmotor eller bara försöker visa japanska era‑datum korrekt, så sparar det här knepet otaliga timmar av efterbehandling. I den här handledningen går vi igenom ett verkligt exempel som **creates Excel workbook Java**, applicerar ett lokalanpassat format, räknar om formler och slutligen **gets DateTime from cell** för att **output datetime value**.

Vi kommer att använda det populära Aspose.Cells for Java‑biblioteket eftersom det hanterar talformat och kultur‑medvetna datum direkt. I slutet av guiden har du ett självständigt, körbart program som du kan lägga in i vilket Maven‑ eller Gradle‑projekt som helst. Inga vaga “se dokumentationen”-genvägar—bara solid kod och tydliga förklaringar.

---

## Vad du kommer att lära dig

- Hur man **create Excel workbook Java** programatiskt.
- De exakta stegen för att **set custom number format** för japanska era‑datum.
- Varför anropet **calculate workbook formulas** är nödvändigt innan värdet extraheras.
- Det korrekta sättet att **get datetime from cell** och **output datetime value**.
- Vanliga fallgropar (saknad locale, föråldrade formler) och snabba lösningar.

---

## Förutsättningar

- Java 8 eller nyare installerat på din maskin.  
- Aspose.Cells for Java 23.11 (eller någon nyare version).  
- En grundläggande IDE eller textredigerare—IntelliJ IDEA, Eclipse, VS Code, vad du än föredrar.  

Om du ännu inte har lagt till Aspose.Cells i ditt projekt, klistra in följande Maven‑snutt i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gradle‑användare kan lägga till:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Nu när miljön är klar, låt oss dyka ner i koden.

---

## Steg 1: Använd anpassat talformat – Översikt

Innan vi skriver någon Java är det bra att visualisera vad vi vill uppnå. Föreställ dig en Excel‑cell som ska visa **“令和2年4月1日”** istället för ISO‑8601‑strängen “2020‑04‑01”. Det underliggande värdet förblir ett riktigt datum (så formler fortfarande fungerar), men *visningen* följer det japanska era‑formatet. Detta är exakt vad operationen **set custom number format** åstadkommer.

Nedan är hela källfilen. Känn dig fri att kopiera‑klistra in den i `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Varför detta fungerar

- **`setNumberFormat`** talar om för Excel hur det ska *visa* det underliggande numeriska värdet. Formatsträngen `[$-ja-JP]ggge年m月d日` är nyckeln; `ggg` väljer eranamnet, `e` året inom eran, följt av månad- och dag‑bokstäver.
- **`calculateFormula`** tvingar Aspose.Cells att tolka texten “R02-04-01” som ett datum baserat på den japanska kalendern. Att hoppa över detta steg lämnar cellen som ren text, och `getDateTime()` skulle kasta ett undantag.
- **`getDateTime`** extraherar slutligen det *verkliga* `java.util.Calendar`‑objektet, som du kan manipulera, formatera eller lagra någon annanstans.

---

## Steg 2: Skapa Excel‑arbetsbok Java – Djupare titt

När du **create Excel workbook Java**, allokerar du inte bara minne; du etablerar också standardstilar, ett standardarbetsblad och en standardkultur (vanligtvis systemets locale). Om du behöver en annan standard‑locale kan du skicka ett `LoadOptions`‑objekt:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

För de flesta scenarier är den enkla konstruktorn tillräcklig, men det är bra att känna till alternativet—särskilt när du hanterar flera locales i samma applikation.

*Pro tip:* Behåll alltid arbetsboken i minnet tills du är klar med formateringen. Att skriva till disk efter varje ändring medför onödig I/O‑belastning.

---

## Steg 3: Hämta DateTime från cell – Hantera resultatet

Raden `java.util.Calendar dt = cellA1.getDateTime();` gör det tunga arbetet. Bakom kulisserna konverterar Aspose.Cells det interna serienumret (antalet dagar sedan 1899‑12‑31) till en `Calendar`. Denna konvertering respekterar arbetsbokens locale, så du får rätt gregorianska datum även om visningen använder den japanska eran.

Om du behöver ett `java.time.LocalDate` (det nyare API‑et), konvertera så här:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Det täcker kravet på **output datetime value** samtidigt som det är modernt.

---

## Steg 4: Beräkna arbetsbokens formler – När det är viktigt

Du kanske undrar: *“Behöver jag verkligen anropa `calculateFormula()`?”* Svaret är ett rungande ja, såvida du inte matar cellen med ett inbyggt Java `Date`‑objekt från början. När du **set custom number format** på en textsträng behandlar Excel (och Aspose.Cells) den som ett formel‑liknande uttryck som måste utvärderas. Utan omräkning kommer `getDateTime()` att returnera standardvärdet `1900‑01‑00` eller kasta ett `CellValueException`.

Om din arbetsbok redan innehåller komplexa formler som refererar till den nyformatta cellen, anropa `calculateFormula()` *en gång* efter alla ändringar. Upprepade anrop är kostsamma.

---

## Steg 5: Skriva ut DateTime‑värde – Verifiera resultatet

Att köra demon skriver ut något i stil med:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Den raden bekräftar tre saker:

1. **set custom number format** har tillämpats (du kan öppna den genererade `.xlsx` i Excel för att se “令和2年4月1日”).
2. **calculate workbook formulas**‑steget lyckades, och omvandlade era‑strängen till ett riktigt datum.
3. **get datetime from cell**‑anropet returnerade en korrekt `Calendar`, som vi sedan **output datetime value** till konsolen.

Om du öppnar arbetsboken med ett kalkylprogram ser du den formaterade texten, men det underliggande cellvärdet förblir serienumret `43831` (Excel‑representationen av 2020‑04‑01). Denna dualitet är vad som gör Excel kraftfullt.

---

## Vanliga fallgropar & edge‑cases

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| `cellA1.getDateTime()` throws `CellValueException` | Cellen är fortfarande en sträng eftersom `calculateFormula()` utelämnades. | Anropa alltid `workbook.calculateFormula()` efter att ha ställt in ett textdatum som behöver konverteras. |
| Japanese era not displayed correctly | Locale‑kod saknas eller är felaktig. | Använd `[$-ja-JP]` i formatsträngen, eller sätt arbetsbokens locale via `LoadOptions`. |
| Format shows “#VALUE!” in Excel | Formatsträngen är felaktigt formaterad. | Dubbelkolla hakparenteser och tecken; mönstret `ggge年m月d日` krävs för era‑året. |
| Time component appears (e.g., “00:00:00”) | Källsträngen innehåller tid eller cellens stil lägger till den. | Trimma källsträngen eller justera formatet till `ggge年m月d日;@`. |

---

## Fullt fungerande exempel – Ett‑klick‑körning

Om du föredrar en enda fil utan extra kommentarer, här är den minimala versionen:



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel&#58; Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}