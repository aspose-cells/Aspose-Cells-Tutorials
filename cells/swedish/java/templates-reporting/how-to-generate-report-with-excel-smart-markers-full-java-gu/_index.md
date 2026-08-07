---
category: general
date: 2026-07-03
description: Hur man genererar en rapport genom att fylla i en Excel‑mall med smarta
  markörer. Lär dig skapa ett detaljblad, använda smarta markörer och automatisera
  datainmatning.
draft: false
keywords:
- how to generate report
- populate excel template
- how to create detail
- create detail sheet
- use smart markers
language: sv
og_description: Hur man genererar rapport med Smart Markers i Java. Den här guiden
  visar hur man populär en Excel‑mall, skapar ett detaljblad och automatiserar master‑detail‑rapportering.
og_title: Hur man genererar rapport med Excel Smart Markers – Java-handledning
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  headline: How to Generate Report with Excel Smart Markers – Full Java Guide
  type: TechArticle
- description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  name: How to Generate Report with Excel Smart Markers – Full Java Guide
  steps:
  - name: What the code does, step by step
    text: '| Step | Explanation | |------|-------------| | **Load workbook** | Reads
      the template, preserving all formatting. | | **Insert marker** | Guarantees
      the placeholder exists even if you built the template programmatically. | |
      **Prepare data** | The `Map` key (`"Orders"`) must match the Smart Marker '
  - name: 5.1 Multiple Detail Datasets
    text: 'You can embed several Smart Markers in the same template, e.g., `{{Detail:Customers}}`
      and `{{Detail:Orders}}`. Just add corresponding entries to the `Map`:'
  - name: 5.2 Custom Sheet Names per Row
    text: 'If you need a unique sheet per order (instead of a single detail sheet),
      use the `DetailSheetNewName` pattern with placeholders:'
  - name: 5.3 Handling Large Datasets
    text: 'When dealing with thousands of rows, enable streaming to keep memory usage
      low:'
  - name: 5.4 Formatting Numbers and Dates
    text: Smart Markers respect the cell’s existing format. If column B in the template
      is formatted as **Currency**, the amounts will automatically display with the
      correct symbol. For custom date formats, just set the cell’s number format before
      processing.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Hur man genererar rapport med Excel Smart Markers – Fullständig Java‑guide
url: /sv/java/templates-reporting/how-to-generate-report-with-excel-smart-markers-full-java-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man genererar rapport med Excel Smart Markers – Fullständig Java-guide

Har du någonsin undrat **hur man genererar rapport** från en Excel-mall utan att skriva miljontals rader med loopkod? Du är inte ensam. Många utvecklare stöter på problem när de måste hämta data från en databas, föra in den i en master‑detail‑arbetsbok och ändå behålla layouten snygg.  

Den goda nyheten? Med Aspose.Cells **Smart Markers** kan du **fylla i Excel-mallen** i ett enda, läsbart anrop—ingen krånglig cell‑för‑cell‑gymnastik behövs. I den här handledningen går vi igenom hela processen, från att förbereda mallen till att spara den slutliga filen, och vi visar också **hur man skapar detalj**-blad på flygande fot.

Vid slutet av den här guiden kommer du att kunna:

* Ladda en fördesignad arbetsbok som fungerar som ditt mastersblad.  
* Infoga en Smart Marker‑platshållare som Aspose kommer att ersätta med riktig orderdata.  
* Mata in en Java `Map` som datakälla och konfigurera **create detail sheet**-alternativen.  
* Köra processorn och få en polerad master‑detail‑rapport klar att dela.  

> **Pro tip:** Om du redan har en mall som ditt affärsteam älskar, behöver du inte röra layouten alls—släpp bara in Smart Marker‑taggarna i rätt celler.

---

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande:

| Krav | Varför det är viktigt |
|------|------------------------|
| **Aspose.Cells for Java** (latest version) | Tillhandahåller `SmartMarkerProcessor`, `Workbook` och relaterade API:er. |
| **Java 8+** | Exemplet använder streams och fabriksmetoden `Map.of` som introducerades i Java 9; justera om du använder Java 8. |
| **An Excel template** (`template.xlsx`) with a placeholder cell for the Smart Marker | Detta är filen du kommer att ladda och senare spara som `masterDetail.xlsx`. |
| **A simple data model** (e.g., `Order` class) | Ger processorn något konkret att ersätta markörerna med. |

Om du ännu inte har Aspose.Cells, skaffa en gratis provversion från den officiella webbplatsen och lägg till JAR‑filen i ditt projekts classpath.

---

## Steg 1: Ställ in Excel-mallen (populate excel template)

Öppna Excel och skapa en arbetsbok kallad `template.xlsx`. I cell **A1** på det första bladet, skriv in Smart Marker‑taggen:

```
{{Detail:Orders}}
```

Den taggen instruerar Aspose att behandla `Orders`‑samlingen som ett **detail**‑dataset och att generera rader för varje objekt. Spara filen i en mapp du senare refererar till, t.ex. `C:/Reports/`.

> **Varför detta är viktigt:** Genom att bädda in markören direkt i mallen håller du den visuella designen separerad från koden. Designers kan justera teckensnitt, färger och formler utan att röra Java.

---

## Steg 2: Skapa Java-projektstrukturen

Här är ett minimalt Maven `pom.xml`‑utdrag som hämtar in Aspose.Cells:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

Skapa ett paket `com.example.report` och lägg till två klasser: `ReportGenerator` (huvuddrivrutinen) och `Order` (vår datamodell).

```java
package com.example.report;

public class Order {
    public String orderId;
    public String customer;
    public double amount;

    public Order(String orderId, String customer, double amount) {
        this.orderId = orderId;
        this.customer = customer;
        this.amount = amount;
    }

    // Getters are optional for Smart Marker; public fields work fine.
}
```

---

## Steg 3: Ladda arbetsboken och infoga Smart Marker (use smart markers)

Nu ska vi skriva kärnlogiken. Lägg märke till hur koden speglar det ursprungliga kodsnutten men lägger till imports, felhantering och kommentarer för tydlighet.

```java
package com.example.report;

import com.aspose.cells.*;
import java.util.*;

public class ReportGenerator {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the workbook that contains the master sheet
            Workbook wb = new Workbook("C:/Reports/template.xlsx");

            // 2️⃣ Grab the first worksheet (the master)
            Worksheet master = wb.getWorksheets().get(0);

            // 3️⃣ Insert a Smart Marker placeholder if you prefer to do it programmatically.
            //    This is optional because we already placed {{Detail:Orders}} in A1.
            master.getCells().putValue("A1", "{{Detail:Orders}}");

            // 4️⃣ Prepare the data source for the Smart Marker
            Map<String, Object> data = new HashMap<>();
            data.put("Orders", getOrders()); // getOrders() returns List<Order>

            // 5️⃣ Configure Smart Marker options – this is where we **create detail sheet**
            SmartMarkerOptions smOpt = new SmartMarkerOptions();
            smOpt.setDetailSheetNewName("OrderDetail"); // New sheet will be named "OrderDetail"

            // 6️⃣ Process the Smart Marker to generate the master‑detail report
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.process(master, data, smOpt);

            // 7️⃣ Save the resulting workbook
            wb.save("C:/Reports/masterDetail.xlsx");

            System.out.println("Report generated successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Simulates fetching order data from a database or service.
     * In a real‑world scenario replace this with JDBC/ORM calls.
     */
    private static List<Order> getOrders() {
        return Arrays.asList(
            new Order("ORD001", "Acme Corp", 1250.75),
            new Order("ORD002", "Beta Ltd.", 980.00),
            new Order("ORD003", "Gamma Inc.", 432.50)
        );
    }
}
```

### Vad koden gör, steg för steg

| Steg | Förklaring |
|------|------------|
| **Load workbook** | Läser in mallen, bevarar all formatering. |
| **Insert marker** | Säkerställer att platshållaren finns även om du byggde mallen programatiskt. |
| **Prepare data** | `Map`‑nyckeln (`"Orders"`) måste matcha Smart Marker‑taggen (`{{Detail:Orders}}`). |
| **Configure options** | `setDetailSheetNewName` instruerar Aspose att skapa ett **create detail sheet** kallat *OrderDetail*. |
| **Process** | `SmartMarkerProcessor` går igenom arbetsboken, ersätter taggen och genererar rader på det nya bladet. |
| **Save** | Skriver den slutliga `masterDetail.xlsx` till disk. |

> **Varför använda Smart Markers?** De låter dig beskriva *vad* du vill ha (en tabell med orders) istället för *hur* du ska loopa genom rader och kolumner. Biblioteket hanterar paginering, stilkopiering och till och med formelomräkning automatiskt.

---

## Steg 4: Verifiera resultatet (how to generate report – verification)

Kör klassen `ReportGenerator`. Efter körning bör du se två arbetsblad:

1. **Sheet1** – det ursprungliga mastersbladet (innehåller fortfarande `{{Detail:Orders}}` men processorn döljer det).  
2. **OrderDetail** – ett helt nytt blad med en rad för varje `Order`‑objekt:

| Order-ID | Kund | Belopp |
|----------|------|--------|
| ORD001   | Acme Corp  | 1250.75|
| ORD002   | Beta Ltd.  | 980.00 |
| ORD003   | Gamma Inc. | 432.50 |

Om du öppnar filen i Excel kommer du att märka att kolumnbredder, teckensnitt och eventuella förinställda stilar från mallen är intakta. Det är fördelarna med **use smart markers**: de bevarar presentationen samtidigt som de injicerar data.

---

## Steg 5: Vanliga variationer & kantfall (populate excel template, how to create detail)

### 5.1 Flera detalj‑datasets

Du kan bädda in flera Smart Markers i samma mall, t.ex. `{{Detail:Customers}}` och `{{Detail:Orders}}`. Lägg bara till motsvarande poster i `Map`:

```java
data.put("Customers", getCustomers());
data.put("Orders", getOrders());
```

### 5.2 Anpassade bladnamn per rad

Om du behöver ett unikt blad per order (istället för ett enda detaljblad), använd `DetailSheetNewName`‑mönstret med platshållare:

```java
smOpt.setDetailSheetNewName("Order_{OrderId}");
```

### 5.3 Hantera stora dataset

När du hanterar tusentals rader, aktivera streaming för att hålla minnesanvändningen låg:

```java
WorkbookSettings ws = wb.getSettings();
ws.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 5.4 Formatera tal och datum

Smart Markers respekterar cellens befintliga format. Om kolumn B i mallen är formaterad som **Currency**, visas beloppen automatiskt med rätt symbol. För anpassade datumformat, ställ bara in cellens talformat innan bearbetning.

---

## Steg 6: Tips & fallgropar (how to create detail, use smart markers)

* **Kod aldrig in filvägar** i produktion. Använd en konfigurationsfil eller miljövariabel.  
* **Stäng alltid resurser** om du öppnar strömmar manuellt; `Workbook`‑klassen implementerar `AutoCloseable` i nyare versioner.  
* **Var uppmärksam på namnkonflikter**—om ett blad med samma namn redan finns, kommer Aspose att lägga till ett numeriskt suffix. För att garantera unikhet, prefixa namnet med en tidsstämpel.  
* **Testa med tomma samlingar**. Om `Orders` är tom, skapar processorn fortfarande bladet men lämnar det tomt—hantera detta senare om du inte vill ha överflödiga flikar.  
* **Felsökning av Smart Markers**: sätt `smOpt.setThrowExceptionOnMissingData(true)` för att få ett tydligt undantag när en markör inte matchar något datafält.

![How to generate report using Smart Markers in Java](/images/how-to-generate-report-smart-markers.png "how to generate report")

*Bildtext: Den slutliga `masterDetail.xlsx` som visar mastersbladet och det genererade **OrderDetail**‑bladet.*

---

## Slutsats

Vi har just demonstrerat **hur man genererar rapport** genom att **fylla i en Excel-mall** med Aspose.Cells Smart Markers, och vi har täckt allt du behöver för att automatiskt **skapa detaljblad**. Metoden håller

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man automatiserar Excel Smart Markers med Aspose.Cells för Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Fyll i Excel med data med Aspose.Cells och Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}