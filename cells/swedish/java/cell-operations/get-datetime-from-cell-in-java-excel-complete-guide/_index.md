---
category: general
date: 2026-10-07
description: Lär dig hur du läser Excel-datum från celler i Java med Aspose.Cells
  och även skriver värden tillbaka till Excel på ett effektivt sätt.
draft: false
keywords:
- how to read excel
- write value to excel
- get datetime from excel
- extract datetime from cell
- Aspose.Cells Java date parsing
lastmod: 2026-10-07
og_description: Hur man läser Excel-datum från celler i Java med Aspose.Cells. Denna
  guide visar också hur man skriver värden till Excel-celler på ett effektivt sätt.
og_image_alt: 'Developer guide: reading and writing Excel dates with Aspose.Cells
  Java'
og_title: Hur man läser Excel-datum från celler i Java med Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  headline: How to read Excel dates from cells in Java using Aspose.Cells
  type: TechArticle
- description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  name: How to read Excel dates from cells in Java using Aspose.Cells
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
- date parsing
- Excel automation
title: Hur man läser Excel-datum från celler i Java med Aspose.Cells
url: /sv/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man läser Excel‑datum från celler i Java med Aspose.Cells

Om du behöver **how to read Excel**‑värden som lagras som japanska era‑strängar, är du på rätt plats. Många äldre arbetsböcker innehåller datum som “Reiwa 3/04/01”, och att extrahera ett korrekt `java.time.LocalDateTime` kan kännas som att knäcka en kod. Aspose.Cells för Java förstår dessa era‑notationer, och låter dig också **write value to excel**‑celler utan att förlora formatering. I den här guiden får du en komplett, steg‑för‑steg‑genomgång som du kan klistra in i vilket Maven‑projekt som helst redan idag.

## Snabba svar
- **Kan Aspose.Cells tolka japanska era‑datum?** Ja – aktivera flaggan för japansk era‑kalender och beräkna om formler.  
- **Måste jag beräkna om formler manuellt?** Absolut; utan ett beräkningspass förblir era‑strängen text.  
- **Hur många Excel‑format stöder Aspose.Cells?** Över 50 in‑ och utdataformat, inklusive XLSX, XLS, CSV och ODS.  
- **Är biblioteket kompatibelt med Java 8+?** Ja, det fungerar med Java 8 och nyare runtime‑versioner.  
- **Kan jag skriva ett gregorianskt datum tillbaka till samma cell?** Använd `putValue` med ett `LocalDateTime` och sätt talformatet till ISO‑8601.

## Vad är how to read Excel dates from cells?
Frasen **how to read Excel** avser att extrahera cellinnehåll – särskilt datum – till inbyggda programmeringstyper såsom `java.time.LocalDateTime`. Aspose.Cells abstraherar den lågnivå‑parsing som krävs, så att du kan fokusera på affärslogik istället för Excels serienummer‑egenskaper. Detta förenklar kodunderhåll och minskar risken för konverteringsfel när du arbetar med äldre kalkylblad.

## Varför använda Aspose.Cells för japansk era‑konvertering?
Aspose.Cells stödjer **50+** filformat och kan bearbeta arbetsböcker med **hundratals sidor** utan att ladda in hela filen i minnet. Att aktivera den japanska era‑kalendern tillför bara en försumbar prestandakostnad, vilket gör den idealisk för batch‑bearbetning av äldre kalkylblad. Biblioteket bevarar också cellstilar och formler under konverteringen, så att resultatet ser identiskt ut med originalarbetsboken.

## Förutsättningar

* **Java 8+** – exemplen använder det moderna `java.time`‑API‑et.  
* **Aspose.Cells för Java ≥ 23.9.0** – lägg till Maven/Gradle‑beroendet från det officiella lagret.  
* Grundläggande kunskap om Excel‑koncept (arbetsblad, celler, formler).  

Om du saknar biblioteket, hämta det från det officiella Aspose‑lagret:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Hur skapar man en arbetsbok och får åtkomst till det första arbetsbladet?
`Workbook` representerar en Excel‑fil som laddats i minnet. `Worksheet` representerar ett enskilt blad i den arbetsboken.  
Skapa ett `Workbook`‑objekt, som representerar en Excel‑fil i minnet, och hämta sedan det första `Worksheet`. Detta ger dig full kontroll innan någon data skrivs till disk. Genom att initiera arbetsboken först kan du konfigurera inställningar – såsom kalenderhantering – innan några cellvärden läses eller skrivs.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

## Hur skriver man en japansk era‑datumsträng till cell A1?
`Cell` är objektet som håller värdet för en enskild Excel‑cell.  
Infoga den äldre era‑strängen “Reiwa 3/04/01” i cell A1. Detta efterliknar ett användar‑inmatat värde som du senare konverterar. Att skriva strängen först låter dig demonstrera hela konverteringsflödet från text till ett korrekt datumobjekt.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

## Hur aktiverar man den japanska era‑kalendern för datum‑parsing?
`WorkbookSettings.setUseJapaneseEraCalendar(boolean)` slår på era‑konverteringsfunktionen.  
Sätt på kalenderflaggan så att Aspose.Cells vet hur man översätter era‑namn till gregorianska år. Att aktivera denna flagga talar om för beräkningsmotorn att tolka strängar som “Reiwa” som motsvarande gregorianska år, vilket är nödvändigt för korrekt datum‑parsing.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

## Hur beräknar man om formler så att era‑strängen konverteras till ett gregorianskt datum?
`Workbook.calculateFormula()` tvingar beräkningsmotorn att utvärdera alla formler i arbetsboken.  
Kör beräkningsmotorn en gång; den känner igen era‑mönstret, konverterar det och lagrar det gregorianska resultatet internt. Därefter returnerar `getDateTime()` ett `java.util.Date`, som du kan konvertera till `java.time`. Detta steg krävs eftersom era‑strängen initialt behandlas som ren text tills formlerna utvärderas.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

**Förväntad utdata**

```
2021-04-01T00:00:00.000+00:00
```

## Hur skriver man ett nytt värde tillbaka till samma cell (eller en annan cell)?
`Cell.putValue(Object)` skriver ett värde i en cell och hanterar automatiskt typkonvertering.  
Skriv över den ursprungliga era‑strängen med ett rent ISO‑8601‑datum samtidigt som cellens stil bevaras. `putValue` upptäcker `LocalDateTime`‑typen och konverterar den till Excels serienummer‑representation. Att sätta talformatet säkerställer att cellen visar datumet exakt som du förväntar dig när den öppnas i Excel.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

## Fullt fungerande exempel

Alla stegen ovan kombineras i en enda Java‑klass som du kan kompilera och köra. Den skapar en arbetsbok, skriver en era‑sträng, konverterar den och sparar slutligen filen.

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

Kör klassen med `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` och öppna **output.xlsx**. Cell A1 kommer att visa det konverterade gregorianska datumet, och konsolen loggar värdet “2021‑04‑01”.

## Vad händer om cellen redan innehåller ett riktigt Excel‑datum?
Om cellen redan lagrar ett inbyggt Excel‑datum kan du läsa det direkt utan extra bearbetning. Detta sparar tid eftersom beräkningsmotorn inte behöver tolka om värdet. Kontrollera helt enkelt celltypen och hämta datumet.

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

## Hur bearbetar man en hel kolumn med era‑strängar?
När många celler innehåller era‑strängar, iterera över det använda området och applicera samma konverteringslogik på varje cell. Detta batch‑tillvägagångssätt minskar overhead jämfört med att hantera celler individuellt. Kom ihåg att aktivera den japanska era‑kalendern innan loopen och beräkna om en gång efter bearbetning.

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

## Kan jag inaktivera den japanska era‑hanteringen senare?
Du kan stänga av era‑konverteringsflaggan efter att du har bearbetat de relevanta cellerna. Att inaktivera den återställer standard‑parsningsbeteendet för eventuella efterföljande operationer. Detta är användbart om du senare i samma arbetsbok behöver arbeta med vanliga datum.

```java
settings.setUseJapaneseEraCalendar(false);
```

Kom ihåg att beräkna om igen om du ändrar inställningen efter att ha skrivit data.

## Pro‑tips & fallgropar

* **Prestanda:** Att aktivera den japanska era‑kalendern tillför en minimal overhead. Växla den bara för de celler som behöver konverteras, och stäng sedan av den.  
* **Språkkänslighet:** Era‑strängen måste följa exakt mönstret “EraName yy/MM/dd”. Stavfel (t.ex. “Rewa”) lämnar cellen som ren text.  
* **Spara‑format:** `Workbook.save("output.xlsx")` skriver en XLSX‑fil. Använd `"output.xls"` för det äldre binära formatet, men notera att vissa avancerade funktioner – som era‑parsing – kan vara begränsade.

## Vanliga frågor

**Q: Fungerar detta tillvägagångssätt med andra kulturella kalendrar (Thai, Hijri)?**  
A: Ja – Aspose.Cells erbjuder liknande flaggor för thailändska buddhistiska och hijri‑kalendrar; aktivera rätt inställning och beräkna om.

**Q: Kan jag läsa datum från en lösenordsskyddad arbetsbok?**  
A: Ladda arbetsboken med lösenordsparametern, följ sedan samma steg; kalenderflaggan fungerar oförändrad.

**Q: Finns det någon gräns för hur många rader jag kan bearbeta?**  
A: Aspose.Cells kan hantera miljontals rader; det strömmar data för att hålla minnesanvändningen låg, särskilt när `setUseJapaneseEraCalendar` växlas per batch.

**Q: Hur bevarar jag befintliga cellstilar när jag skriver över datumet?**  
A: Hämta cellens `Style`‑objekt innan du anropar `putValue`, och återapplicera det efter skrivoperationen.

**Q: Behöver jag en kommersiell licens för produktionsbruk?**  
A: Ja, en giltig Aspose.Cells‑licens krävs för produktionsdistribution; en gratis provversion finns för utvärdering.

## Slutsats

Du vet nu **how to read Excel**‑datum som använder japansk era‑notation och hur du **write value to excel**‑celler med korrekt formatering. Genom att aktivera `setUseJapaneseEraCalendar(true)` och tvinga en formel‑omberäkning, förenar Aspose.Cells äldre era‑strängar med moderna gregorianska datum i bara några rader Java‑kod. Prova att utöka detta mönster till andra kulturella kalendrar eller batch‑processa stora arbetsböcker – samma enable‑recalculate‑read/write‑arbetsflöde gäller universellt.

Har du ett knepigt datumformat du inte kan knäcka? Lämna en kommentar nedan så felsöker vi tillsammans. Lycka till med kodningen!

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")
[Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [How to Implement Recursive Cell Calculation in Aspose.Cells Java for Enhanced Excel Automation](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

---


**Senast uppdaterad:** 2026-10-07  
**Testat med:** Aspose.Cells 23.9.0  
**Författare:** Aspose

## Relaterade handledningar

- [aspose cells performance: Retrieve Excel Cell Data with Java](/cells/java/cell-operations/aspose-cells-java-data-retrieval-excel/)
- [Change Excel 1904 date system with Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Master Java File Handling with Aspose.Cells: Read, Write & Process Data Efficiently](/cells/java/workbook-operations/java-file-handling-aspose-cells-read-write-process/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}