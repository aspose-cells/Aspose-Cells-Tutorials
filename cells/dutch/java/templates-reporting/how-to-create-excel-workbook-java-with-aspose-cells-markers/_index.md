---
category: general
date: 2026-11-25
description: Maak een Java‑codevoorbeeld voor het maken van een Excel‑werkmap met
  Aspose.Cells‑smart‑markers om JSON‑arrays als enkele waarden te binden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: nl
lastmod: 2026-11-25
og_description: Maak een Excel‑werkboek in Java met Aspose.Cells om JSON‑arrays eenvoudig
  als enkele cellen te exporteren. Volg de stapsgewijze handleiding.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Excel-werkmap maken in Java – Aspose.Cells smart‑marker‑gids
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
title: Hoe een Excel-werkmap te maken in Java met Aspose.Cells-markeringen
url: /nl/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een Excel workbook Java met Aspose.Cells-markeringen

Als je **create Excel workbook Java** code moet maken die een JSON-array in één cel schrijft, laat deze tutorial je precies zien hoe. Met Aspose.Cells smart markers kun je een volledige array behandelen als één waarde, waardoor handmatige lussen en cel‑voor‑cel schrijven worden vermeden.

Je leert hoe je een werkmap opstelt, een smart marker definieert, een `Map`‑datasource bindt die een JSON‑achtige array bevat, en uiteindelijk het bestand opslaat. Het voorbeeld werkt met Java 17+, Maven en de gratis Aspose.Cells for Java trial‑bibliotheek.

---

![Schermafbeelding van een Excel-werkmap gemaakt in Java met Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Schermafbeelding van een Excel-werkmap gemaakt in Java met Aspose.Cells smart markers"}

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Java 17 of hoger | De nieuwste taalfeatures en beveiligingsupdates |
| Maven 3.6+ | Vereenvoudigt het beheer van afhankelijkheden |
| Aspose.Cells for Java (v23.12 of newer) | Biedt de `Workbook`, `Worksheet` en smart‑marker API's die in het voorbeeld worden gebruikt |
| Basiskennis van Java-collecties | Je maakt een `Map<String, Object>` die fungeert als de gegevensbron |

Voeg de Aspose.Cells‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Maak Excel workbook Java – volledig voorbeeld

Het volgende programma is een **volledige, uitvoerbare** oplossing. Kopieer het naar een bestand met de naam `ExcelSmartMarkerDemo.java`, compileer en voer uit.

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

### Wat de code doet

1. **Creates a fresh workbook** – `new Workbook()` geeft je een Excel‑bestand in het geheugen met een standaardblad.  
2. **Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` vertelt Aspose.Cells om de marker te vervangen door de *hele* array, gescheiden door komma's.  
3. **Builds a `Map` data source** – De sleutel `"jsonArray"` komt overeen met de markernaam; de waarde is een `String[]`.  
4. **Calls `setSmartMarkerData`** – Dit bindt de map aan de marker en voert de vervanging uit.  
5. **Saves the file** – `workbook.save(...)` schrijft `JsonSingleValue.xlsx` naar schijf.

Wanneer je het gegenereerde Excel‑bestand opent, bevat cel **A1**:

```
One, Two, Three
```

De array wordt weergegeven als één, door komma's gescheiden tekenreeks vanwege de `ArrayAsSingle`‑optie.

---

## Aspose.Cells smart marker gebruiken om JSON‑gegevens te binden

Aspose.Cells smart markers zijn een krachtige manier om complexe objecten (inclusief JSON‑achtige structuren) direct op werkbladen te mappen. De syntaxis `{{fieldName:Option}}` werkt ongeveer als een template‑engine:

* **fieldName** – de sleutel in je gegevensbron (`Map`, POJO, of `DataTable`).  
* **Option** – bepaalt hoe collecties worden behandeld. `ArrayAsSingle` behandelt de hele collectie als één waarde; andere opties zoals `Array` zouden de array over rijen uitbreiden.

**Waarom een smart marker gebruiken in plaats van een lus?**  
Een lus vereist handmatige berekeningen van celadressen, foutgevoelige indexering en extra code voor opmaak. Smart markers laten je declaratieve placeholders schrijven, houden je Java‑code kort, en laten de bibliotheek de lay‑outdetails afhandelen.

---

## De Java‑Map‑gegevensbron instellen

De `Map<String, Object>` is de eenvoudigste gegevenscontainer voor Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*De sleutel (`jsonArray`) moet exact overeenkomen met de markernaam.*

Je kunt ook een `List<String>`, een aangepaste POJO, of zelfs een geneste `Map` gebruiken voor complexere JSON‑structuren. Aspose.Cells doorloopt de objectgrafiek automatisch.

**Tip:** Als je de samengevoegde tekenreeks anders wilt formatteren (bijv. met puntkomma's), verwerk dan de array in Java vóór het toewijzen aan de map:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## De werkmap opslaan en de uitvoer verifiëren

```java
workbook.save("JsonSingleValue.xlsx");
```

De `save`‑methode ondersteunt vele formaten (`.xlsx`, `.xls`, `.csv`, `.pdf`). Voor deze tutorial behouden we het standaard Excel Open XML‑formaat.

**Verificatiestappen**

1. Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc of Google Sheets.  
2. Bevestig dat cel **A1** `One, Two, Three` weergeeft.  
3. Controleer dat er geen extra rijen of kolommen zijn toegevoegd – de smart marker voerde een vervanging op zijn plaats uit.

Als de cel de ruwe marker‑tekst toont (`{{jsonArray:ArrayAsSingle}}`), controleer dan:

* De markernaam komt exact overeen met de map‑sleutel (hoofdlettergevoelig).  
* `setSmartMarkerData` wordt aangeroepen **na** het plaatsen van de marker.  
* De Aspose.Cells‑versie ondersteunt de `ArrayAsSingle`‑optie (beschikbaar sinds v20.3).

---

## Veelvoorkomende variaties en randgevallen

| Scenario | Aanpassing |
|----------|------------|
| **Andere scheidingsteken** | Gebruik `ArrayAsSingle` in combinatie met een aangepaste join in Java (zie tip hierboven). |
| **Meerdere arrays in één blad** | Plaats extra markers zoals `{{anotherArray:ArrayAsSingle}}` in andere cellen en voeg de bijbehorende items toe aan de map. |
| **Geneste JSON‑objecten** | Voorzie een geneste `Map<String, Object>`; verwijs naar velden met puntnotatie (`{{parent.child}}`). |
| **Grote datasets** | Voor duizenden rijen, geef de voorkeur aan de `Array`‑optie zodat Aspose.Cells rijen automatisch uitbreidt, wat |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe maak en exporteer je Excel naar HTML met Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Excel-werkmap exporteren als afbeelding met Aspose.Cells for Java: Een stapsgewijze handleiding](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Hoe maak en sla je een Excel-werkmap op als SVG met Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}