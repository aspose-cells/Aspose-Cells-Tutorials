---
category: general
date: 2026-08-20
description: Skapa smarta markörer för kalkylblad i Java med Aspose.Cells och kontrollera
  namn på detaljblad med SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: sv
lastmod: 2026-08-20
og_description: Skapa smartmarkörer för kalkylblad i Java med Aspose.Cells. Lär dig
  hur du dynamiskt namnger detaljblad med SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Skapa kalkylblad med smarta markörer – Java‑guide med Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Hur man skapar smarta markörer för kalkylblad med Aspose.Cells
url: /sv/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar smarta markörer i kalkylblad med Aspose.Cells

Om du behöver **skapa smarta markörer i kalkylblad** i en Java‑arbetsbok, visar den här guiden exakt hur du gör det med Aspose.Cells. Du får se hur du konfigurerar `SmartMarkerOptions` så att varje detaljark får ett unikt, förutsägbart namn.

Att generera Excel‑rapporter som expanderar en master‑detail‑mall är ett vanligt krav i finans-, lager‑ och rapporteringssystem. Genom att använda smarta markörer elimineras manuell kopiering av ark och du kan fokusera på data istället för infrastrukturen.

## Vad du kommer att lära dig

* Hur du laddar en master‑arbetsbok som innehåller smarta markörer.  
* Hur du sätter `SmartMarkerOptions` för att styra namngivningen av genererade detaljarbetsblad.  
* Hur du levererar en `DataTable` med exempeldata och applicerar den på de smarta markörerna.  
* Hur du sparar resultatet så att varje detaljkalkylblad har ett distinkt namn och undviker duplicerade ark‑namn.

**Förutsättningar**  
* Java 17 eller senare (koden kompileras även med JDK 8+).  
* Aspose.Cells för Java 23.9 eller nyare – biblioteket tillhandahåller `Workbook`, `SmartMarkerOptions` och relaterade klasser.  
* En IDE såsom IntelliJ IDEA, Eclipse eller VS Code.

Sekundära begrepp du kommer att stöta på inkluderar **Aspose.Cells Java**, **smart marker options** och hantering av **duplicate sheet names** när mallen expanderas.

## Skapa smarta markörer i kalkylblad – steg‑för‑steg‑guide

Följande avsnitt delar upp processen i diskreta, återanvändbara steg. Varje steg innehåller ett kodexempel, en förklaring av varför det är viktigt och praktiska tips för att undvika vanliga fallgropar.

### Steg 1: Ställ in Maven‑projektet och lägg till Aspose.Cells

Skapa en ny Maven‑modul (eller Gradle‑projekt) och lägg till Aspose.Cells‑beroendet:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Varför detta steg är viktigt** – Biblioteket levererar `Workbook`‑klassen som läser och skriver Excel‑filer, samt smart‑marker‑motorn som automatiskt expanderar din mall. Utan rätt beroende kan kompilatorn inte lösa API‑anropen som används senare.

> **Proffstips:** Om du arbetar bakom en företagsproxy, konfigurera Maven’s `settings.xml` för att hämta Aspose‑arkivet på ett säkert sätt.

### Steg 2: Ladda master‑arbetsboken som innehåller smarta markörer

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Varför detta steg är viktigt** – Master‑arbetsboken definierar layout, formler och platshållartaggar (`«SmartMarker»`) som motorn kommer att ersätta. Att läsa in filen en gång håller minnesanvändningen låg och gör att du kan återanvända samma arbetsbok för flera dataset.

### Steg 3: Konfigurera SmartMarkerOptions för anpassade detaljark‑namn

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Varför detta steg är viktigt** – Som standard skapar Aspose.Cells detaljarbetsblad med generiska namn som “DetailSheet”. När mallen expanderas för många rader kolliderar dessa namn, vilket leder till **duplicate sheet names** och ett körningsfel. Mönstret `"DetailSheet_{0}"` garanterar ett unikt namn per rad och löser dupliceringsproblemet.

### Steg 4: Bygg en DataTable som matchar smart‑marker‑fälten

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Varför detta steg är viktigt** – `DataTable` levererar de faktiska värdena som ersätter smart‑marker‑platshållarna. Kolumnnamnen måste matcha markörnamnen i mallen; annars hoppar motorn över ersättningen tyst.

> **Vanligt misstag:** Att använda ett kolumnnamn som skiljer sig i versal‑/gemen‑form (t.ex. “id” vs “Id”) leder till saknade data i de genererade arken.

### Steg 5: Applicera data på de smarta markörerna med namngivningsalternativen

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Varför detta steg är viktigt** – Metoden `apply` triggar smart‑marker‑motorn. Den läser varje rad, skapar ett nytt detaljark med namn enligt mönstret i `SmartMarkerOptions` och fyller arket med radens data. Detta enkla anrop ersätter dussintals rader med manuell ark‑kloning och cell‑fyllning.

### Steg 6: Spara arbetsboken och verifiera resultatet

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Efter körning, öppna `MasterDetailDuplicatedNames.xlsx`. Du bör se:

* Det ursprungliga master‑arket oförändrat.  
* Två nya kalkylblad med namnen `DetailSheet_1` och `DetailSheet_2`.  
* Varje detaljark innehåller värdena från motsvarande rad i `DataTable`.

**Varför detta steg är viktigt** – Att persistera arbetsboken slutför smart‑marker‑expansionen. Filen kan nu skickas till downstream‑system, bifogas i e‑post eller öppnas i Excel för vidare analys.

## Hantera kantfall och variationer

### Flera master‑ark

Om din mall innehåller mer än ett master‑ark, iterera över varje arks smarta markörer:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Anpassad namngivning bortom rad‑indexet

Du kan bädda in vilken datakolumn som helst i ark‑namnet genom att använda platshållare som `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Se till att kolumnen `OrderId` finns i den levererade `DataTable`.

### Förhindra alltför långa ark‑namn

Excel begränsar ark‑namn till 31 tecken. Om ditt namn‑mönster riskerar att överskrida denna gräns, trunkera eller hash‑a värdet:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Trunkera sedan det genererade namnet med `StringUtils.abbreviate` innan du skickar det till Aspose.

## Komplett körbart exempel

Nedan är hela källfilen som du kan kopiera, justera fil‑sökvägarna och köra direkt:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Förväntad output**

* `MasterDetailDuplicatedNames.xlsx` innehåller:


## Vad bör du lära dig härnäst?


Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Behärska Aspose.Cells Java: Använd smarta markörer för dynamisk data i kalkylblad](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Skapa dynamiska diagram med smarta markörer i Aspose.Cells för Java | Steg‑för‑steg‑guide](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}