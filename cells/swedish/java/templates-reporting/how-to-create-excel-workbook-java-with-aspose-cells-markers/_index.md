---
category: general
date: 2026-11-25
description: Skapa ett Excel‑arbetsbok Java‑kodexempel som använder Aspose.Cells smarta
  markörer för att binda JSON‑arrayer som enskilda värden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: sv
lastmod: 2026-11-25
og_description: Skapa Excel-arbetsbok i Java med Aspose.Cells för att enkelt exportera
  JSON‑arrayer som enskilda celler. Följ steg‑för‑steg‑guiden.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Skapa Excel‑arbetsbok i Java – Aspose.Cells smart marker‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hur man skapar en Excel‑arbetsbok i Java med Aspose.Cells‑markörer
url: /sv/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så skapar du en Excel-arbetsbok i Java med Aspose.Cells-markörer

Om du behöver **create Excel workbook Java** kod som skriver en JSON-array i en enda cell, visar den här handledningen exakt hur du gör. Med Aspose.Cells smart markers kan du behandla en hel array som ett värde, vilket undviker manuella loopar och cell‑för‑cell‑skrivningar.

Du kommer att lära dig hur du sätter upp en arbetsbok, definierar en smart marker, binder en `Map`‑datakälla som innehåller en JSON‑liknande array och slutligen sparar filen. Exemplet fungerar med Java 17+, Maven och det kostnadsfria Aspose.Cells for Java provbiblioteket.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Skärmbild av en Excel-arbetsbok skapad i Java med Aspose.Cells smart markers"}

## Förutsättningar

| Krav | Varför det är viktigt |
|-------------|----------------|
| Java 17 eller senare | De senaste språkfunktionerna och säkerhetsuppdateringarna |
| Maven 3.6+ | Förenklar hantering av beroenden |
| Aspose.Cells for Java (v23.12 or newer) | Tillhandahåller `Workbook`, `Worksheet` och smart‑marker API:er som används i exemplet |
| Grundläggande kunskap om Java‑samlingar | Du kommer att skapa en `Map<String, Object>` som fungerar som datakälla |

Lägg till Aspose.Cells‑beroendet i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Skapa Excel-arbetsbok Java – komplett exempel

Följande program är en **fullständig, körbar** lösning. Kopiera det till en fil med namnet `ExcelSmartMarkerDemo.java`, kompilera och kör.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Vad koden gör

1. **Skapar en ny arbetsbok** – `new Workbook()` ger dig en Excel‑fil i minnet med ett standardsheet.  
2. **Placera en smart marker i cell A1** – `{{jsonArray:ArrayAsSingle}}` instruerar Aspose.Cells att ersätta markören med hela arrayen, sammanfogad med kommatecken.  
3. **Bygger en `Map`‑datakälla** – Nyckeln `"jsonArray"` matchar markörens namn; värdet är en `String[]`.  
4. **Anropar `setSmartMarkerData`** – Detta binder kartan till markören och utför ersättningen.  
5. **Sparar filen** – `workbook.save(...)` skriver `JsonSingleValue.xlsx` till disk.

När du öppnar den genererade Excel‑filen, innehåller cell **A1**:

```
One, Two, Three
```

Arrayen renderas som en enda, kommaseparerad sträng på grund av `ArrayAsSingle`‑alternativet.

---

## Använda Aspose.Cells smart marker för att binda JSON‑data

Aspose.Cells smart markers är ett kraftfullt sätt att mappa komplexa objekt (inklusive JSON‑liknande strukturer) direkt på kalkylblad. Syntaxen `{{fieldName:Option}}` fungerar ungefär som en mallmotor:

* **fieldName** – nyckeln i din datakälla (`Map`, POJO eller `DataTable`).  
* **Option** – styr hur samlingar hanteras. `ArrayAsSingle` behandlar hela samlingen som ett värde; andra alternativ som `Array` skulle expandera arrayen över rader.

**Varför använda en smart marker istället för en loop?**  
En loop kräver manuella beräkningar av celladresser, felbenägen indexering och extra kod för formatering. Smart markers låter dig skriva deklarativa platshållare, hålla din Java‑kod kort och låter biblioteket hantera layoutdetaljer.

---

## Ställa in Java‑Map‑datakällan

`Map<String, Object>` är den enklaste databehållaren för Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Nyckeln (`jsonArray`) måste matcha markörens namn exakt.*  
Du kan också använda en `List<String>`, en anpassad POJO eller till och med en nästlad `Map` för mer komplexa JSON‑strukturer. Aspose.Cells kommer automatiskt att traversera objektgrafen.

**Tips:** Om du behöver formatera den sammanslagna strängen annorlunda (t.ex. med semikolon), förbehandla arrayen i Java innan du tilldelar den till kartan:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Spara arbetsboken och verifiera resultatet

```java
workbook.save("JsonSingleValue.xlsx");
```

`save`‑metoden stödjer många format (`.xlsx`, `.xls`, `.csv`, `.pdf`). För den här handledningen behåller vi standardformatet Excel Open XML.

**Verifieringssteg**

1. Öppna `JsonSingleValue.xlsx` i Microsoft Excel, LibreOffice Calc eller Google Sheets.  
2. Bekräfta att cell **A1** visar `One, Two, Three`.  
3. Kontrollera att inga extra rader eller kolumner har lagts till – smart marker utförde en ersättning på plats.

Om cellen visar den råa markörtexten (`{{jsonArray:ArrayAsSingle}}`), dubbelkolla att:

* Markörens namn matchar kartans nyckel exakt (skiftlägeskänsligt).  
* `setSmartMarkerData` anropas **efter** att markören placerats.  
* Aspose.Cells‑versionen stödjer `ArrayAsSingle`‑alternativet (tillgängligt sedan v20.3).

---

## Vanliga variationer och kantfall

| Scenario | Justering |
|----------|------------|
| **Olika avgränsare** | Använd `ArrayAsSingle` tillsammans med en anpassad sammanslagning i Java (se tippen ovan). |
| **Flera arrayer i ett blad** | Placera ytterligare markörer som `{{anotherArray:ArrayAsSingle}}` i andra celler och lägg till motsvarande poster i kartan. |
| **Nästlade JSON‑objekt** | Tillhandahåll en nästlad `Map<String, Object>`; referera till fält med punktnotation (`{{parent.child}}`). |
| **Stora datamängder** | För tusentals rader, föredra `Array`‑alternativet så att Aspose.Cells expanderar rader automatiskt, vilket |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar och exporterar Excel till HTML med Aspose.Cells Java \| Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Exportera Excel-arbetsbok som bild med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Hur man skapar och sparar en Excel‑arbetsbok som SVG med Aspose.Cells för Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}