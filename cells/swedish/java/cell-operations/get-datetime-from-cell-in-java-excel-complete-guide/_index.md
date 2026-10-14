---
category: general
date: 2026-06-08
description: Hämta datum och tid från en cell med Aspose.Cells Java och lär dig hur
  du skriver ett värde till en Excel‑cell på bara några steg.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: sv
og_description: Hämta datum och tid från cell med Aspose.Cells Java. Denna handledning
  visar också hur man skriver värde till en Excel‑cell på ett effektivt sätt.
og_title: Hämta datum och tid från cell i Java Excel – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Hämta datum och tid från cell i Java Excel – Komplett guide
url: /sv/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta datum och tid från cell i Java Excel – Komplett guide

Har du någonsin behövt **get datetime from cell** men värdet ser ut som en japansk era‑sträng? Du är inte ensam. I många äldre kalkylblad lagras datum som “Reiwa 3/04/01”, och att extrahera ett korrekt `java.time.LocalDateTime` från det kan kännas som att avkoda ett hemligt meddelande.  

Lyckligtvis kan Aspose.Cells for Java hantera konverteringen åt dig, och medan vi är igång visar vi också hur du **write value to excel cell** så att du kan runda‑trip data utan att bryta kalkylbladets logik.

I den här handledningen kommer du att lära dig:

* Hur du skapar en arbetsbok och riktar in dig på ett specifikt kalkylblad.  
* De exakta stegen för att aktivera den japanska era‑kalendern för parsning.  
* Varför du måste beräkna om formler innan du läser datumet.  
* Hur du skriver ett nytt värde tillbaka till en cell utan att förlora formatering.  

Inga externa verktyg, ingen magi—bara ren Java‑kod som du kan släppa in i vilket Maven‑projekt som helst idag.

---

## Förutsättningar

* **Java 8+** (exemplet använder det moderna `java.time`‑API:t).  
* **Aspose.Cells for Java** ≥ 23.9.0 – lägg till beroendet via Maven eller Gradle.  
* Grundläggande kunskap om Excel‑koncept (kalkylblad, celler, formler).  

Om du saknar biblioteket, hämta det från det officiella Aspose‑arkivet:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Steg 1: Skapa en ny arbetsbok och öppna det första kalkylbladet

För att börja behöver vi ett fräscht `Workbook`‑objekt. Tänk på det som att öppna en ny Excel‑fil i minnet.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Varför detta är viktigt:*  
Att skapa arbetsboken programatiskt ger dig full kontroll över inställningarna innan någon data rör filsystemet. Det första kalkylbladet (`index 0`) är där vi demonstrerar både läsning och skrivning.

---

## Steg 2: Skriv en japansk era‑datumssträng till cell A1

Nu ska vi **write value to excel cell** A1. Detta speglar ett verkligt scenario där en användare manuellt har skrivit in “Reiwa 3/04/01”.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Snabbtips:* `putValue` är mångsidig—den accepterar strängar, tal, datum och till och med formler. När du skickar en ren sträng lagrar Aspose den exakt som den är, vilket är perfekt för vår demo.

---

## Steg 3: Aktivera den japanska era‑kalendern för datumparsning

Som standard använder Aspose.Cells den gregorianska kalendern. För att förstå “Reiwa” slår vi på en inställning.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Varför aktivera detta?*  
Den japanska era‑kalendern mappar eranamn (Reiwa, Heisei, Showa) till deras gregorianska motsvarigheter. Utan denna flagga skulle biblioteket behandla strängen som ren text, och du skulle aldrig få ett korrekt `DateTime`‑objekt.

---

## Steg 4: Beräkna om formler så att era‑strängen konverteras till ett gregorianskt datum

Aspose parsar inte automatiskt strängen till ett datum. Istället behandlar den cellen som ett formelresultat efter ett beräkningspass.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

När `calculateFormula()` körs känner motorn igen era‑mönstret, tillämpar den japanska kalendern och lagrar det resulterande gregorianska datumet internt. `getDateTime()`‑anropet returnerar då ett `java.util.Date` (eller så kan du konvertera till `java.time`).

**Förväntad utdata**

```
2021-04-01T00:00:00.000+00:00
```

---

## Steg 5: Skriv ett nytt värde tillbaka till samma cell (eller en annan cell)

Anta att du behöver skriva över den ursprungliga strängen med ett rent ISO‑8601‑datum. Så här **write value to excel cell** du säkert, samtidigt som du bevarar cellens stil.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Vad händer?*  
`putValue` upptäcker `LocalDateTime`‑typen och konverterar den till Excels serienummerrepresentation. Att sätta talformatet säkerställer att cellen visar datumet exakt som du förväntar dig när den öppnas i Excel.

---

## Fullt fungerande exempel

Sätter vi ihop allt får du en enda Java‑klass som du kan kompilera och köra. Den skapar en arbetsbok, skriver en era‑sträng, konverterar den och sparar slutligen filen.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Kör detta med `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` och öppna **output.xlsx**. Du kommer att se att cell A1 visar det aktuella datumet, medan konsolen loggar det konverterade värdet “2021‑04‑01”.

---

## Hantera kantfall & vanliga frågor

### Vad händer om cellen redan innehåller ett riktigt Excel‑datum?

Om `cell.getType()` returnerar `CellValueType.IS_DATE_TIME` kan du hoppa över beräkningssteget och läsa värdet direkt:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Hur bearbetar jag en hel kolumn med era‑strängar?

Loopa genom det använda området och applicera samma inställningar en gång:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Kan jag inaktivera den japanska era‑hanteringen senare?

Ja—vänd bara flaggan tillbaka:

```java
settings.setUseJapaneseEraCalendar(false);
```

Kom ihåg att beräkna om igen om du ändrar inställningen efter att ha skrivit data.

---

## Pro‑tips & fallgropar

* **Prestanda:** Att aktivera den japanska era‑kalendern lägger till en liten overhead. Om du bara behöver den för några få celler, överväg att slå på inställningen, bearbeta, och sedan stänga av den igen.  
* **Lokalmedvetenhet:** Era‑strängen måste exakt matcha mönstret “EraName yy/MM/dd”. Felstavning av “Reiwa” (t.ex. “Rewa”) lämnar cellen som ren text.  
* **Sparformat:** `Workbook.save("output.xlsx")` skriver en XLSX‑fil. Använd `"output.xls"` om du behöver det äldre binära formatet, men notera att vissa funktioner (som era‑parsning) kan vara begränsade.

---

## Slutsats

Du vet nu hur du **get datetime from cell** när källan använder en japansk era‑notation, och du har också sett ett rent sätt att **write value to excel cell** med korrekt formatering. Genom att slå på `setUseJapaneseEraCalendar(true)` och tvinga en formelberäkning bygger Aspose.Cells en bro mellan äldre era‑strängar och moderna gregorianska datum—allt med ett fåtal rader Java‑kod.

Vad blir nästa steg? Prova att utöka detta mönster till andra kulturella kalendrar (Thai, Hijri) eller batch‑processa stora arbetsböcker med samma tillvägagångssätt. Samma principer—aktivera rätt kalender, beräkna om, läs/skriv—gäller överallt.

Har du ett knepigt datumformat du inte kan knäcka? Lämna en kommentar nedan, så felsöker vi tillsammans. Lycka till med kodningen!  

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [How to Implement Recursive Cell Calculation in Aspose.Cells Java for Enhanced Excel Automation](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}