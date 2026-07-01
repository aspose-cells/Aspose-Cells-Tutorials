---
category: general
date: 2026-06-30
description: Vul een Excel‑sjabloon met gegevens met behulp van SmartMarkerProcessor
  en leer hoe je een Excel‑rapport uit een sjabloon maakt in Java – stapsgewijze handleiding.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: nl
og_description: Vul Excel-sjabloon met gegevens met behulp van SmartMarkerProcessor.
  Deze gids laat zien hoe je een Excel-rapport vanuit een sjabloon maakt in Java,
  compleet met code.
og_title: Vul Excel-sjabloon met gegevens – Maak Excel-rapport vanuit sjabloon
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Vul Excel-sjabloon met gegevens – Maak Excel-rapport vanuit sjabloon
url: /nl/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑sjabloon vullen met gegevens – Excel‑rapport maken vanuit sjabloon

Heb je ooit **een Excel‑sjabloon moeten vullen met gegevens** maar wist je niet welke bibliotheek het zware werk kon doen? Je bent niet de enige. Wanneer je maandelijkse dashboards, facturen of andere data‑gedreven spreadsheets bouwt, wordt handmatig invullen al snel een nachtmerrie.  

Het goede nieuws is dat de **SmartMarkerProcessor** van Aspose.Cells het moeiteloos maakt – geef gewoon een sjabloon en een gegevensbron, en je hebt binnen enkele seconden een gepolijst Excel‑rapport. In deze tutorial laten we ook zien **hoe je een Excel‑rapport maakt vanuit een sjabloon** met gewone Java, zodat je de oplossing direct in je project kunt opnemen.

## Voorvereisten (Wat je nodig hebt)

- Java 17 of nieuwer (de code compileert ook met oudere versies, maar 17 biedt de nieuwste taalfeatures).  
- Aspose.Cells for Java (het Maven‑artifact `com.aspose:aspose-cells` versie 24.9 of later).  
- Een Excel‑bestand dat Smart Markers bevat (bijv. `input.xlsx`).  
- Een eenvoudige gegevensbron die `IDataSource` implementeert (we bouwen er één voor je).  

Er is geen speciale IDE vereist – elke editor die Java kan compileren volstaat.  

---

## Excel‑sjabloon vullen met gegevens – Stap‑voor‑stap

Hieronder splitsen we het proces in zes logische stappen. Elke stap bevat **waarom** het belangrijk is, niet alleen **wat** je moet typen.

### Stap 1: Instantieer de SmartMarkerProcessor  

De processor is de motor die je werkmap scant, Smart Markers vindt en vervangt door echte waarden.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Waarom?*  
Een nieuwe processor zorgt voor een schone start. Als je een oude instantie hergebruikt, kunnen resterende instellingen doorsluipen naar de volgende run – iets wat je in een productie‑omgeving zeker wilt vermijden.

### Stap 2 (Optioneel): Hernoem het Detail‑blad  

Smart Markers genereren vaak een verborgen “detail”‑blad dat tussenliggende gegevens bevat. Het hernoemen maakt de uiteindelijke werkmap makkelijker te navigeren.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Pro‑tip:*  
Als je sjabloon al een blad met de naam “Detail” bevat, geef het gegenereerde blad dan een unieke suffix (bijv. `CopyOfDetail_2024`) om naamconflicten te voorkomen.

### Stap 3: Laad de Sjabloon‑Werkmap  

Hier wijs je de processor naar het Excel‑bestand dat de markers bevat.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Waarom?*  
Het laden van de werkmap in het geheugen laat Aspose.Cells deze manipuleren zonder het originele bestand op schijf aan te raken. Je kunt dezelfde sjabloon‑file veilig hergebruiken voor meerdere rapporten.

### Stap 4: Bereid een Gegevensbron voor  

SmartMarkerProcessor verwacht een `IDataSource`‑implementatie die weet hoe waarden voor elke marker opgehaald moeten worden. Hieronder staat een minimale **in‑memory** gegevensbron die een `Map<String, Object>` gebruikt.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*Waarom deze implementatie?*  
Hij is lichtgewicht, vereist geen externe database en is perfect voor demo’s of unit‑tests. In een echte situatie zou je `MapDataSource` vervangen door iets dat data haalt uit een JDBC‑resultset, een REST‑API of een ORM‑entity.

### Stap 5: Pas de Gegevens toe op de Werkmap  

Nu gebeurt de magie – Smart Markers worden vervangen door de waarden uit je `IDataSource`.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*Wat gebeurt er onder de motorkap?*  
Aspose.Cells doorloopt elke cel die een marker bevat zoals `${EmployeeName}`. Voor elke marker wordt `IDataSource.getValue("EmployeeName")` aangeroepen en de geretourneerde waarde in de cel geschreven. Als je een tabel‑marker hebt (`${Employees}`), breidt de processor automatisch rijen uit op basis van de array‑lengte.

### Stap 6: Sla de Verwerkte Werkmap op  

Tot slot schrijf je de gevulde werkmap naar schijf (of stream je deze direct naar een HTTP‑response als je in een webapplicatie zit).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Tip:*  
Gebruik de overload `workbook.save(OutputStream, SaveFormat.XLSX)` wanneer je het bestand naar een client moet sturen zonder het bestandssysteem te raken.

---

## Excel‑rapport maken vanuit sjabloon – Geavanceerde tips

Nu de basisstroom werkt, bekijken we een paar veelvoorkomende uitbreidingen die je **Excel‑rapport vanuit sjabloon** productie‑klaar maken.

### H3: Verzamelingen verwerken (Tabellen)

Als je sjabloon een herhalend blok bevat, zoals een verkoop‑tabel, vervang je de marker door een array in je gegevensbron.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

In het sjabloon zou je markers hebben zoals `${SalesData.Product}`, `${SalesData.Qty}`, enz., binnen een rij die Aspose voor elke invoer zal repliceren.

### H3: Datums en getallen opmaken

Smart Markers respecteren celopmaak. Als je een cel vooraf als *Currency* opmaakt in het sjabloon, wordt de numerieke waarde die je doorgeeft automatisch weergegeven met het juiste symbool en decimalen. Geen extra code nodig – zorg er alleen voor dat het datatype dat je retourneert (`Double`, `BigDecimal`, `LocalDate`) overeenkomt met de verwachte opmaak.

### H3: Prestatie‑overwegingen

- **Herbruik de processor** als je tientallen rapporten in één batch genereert; roep gewoon `processor.clear()` aan tussen de runs.  
- **Schakel berekening uit** (`workbook.getSettings().setRecalcOnLoad(false)`) wanneer je alleen waarden hoeft te schrijven, niet formules opnieuw moet berekenen.  
- **Stream de output** om grote tijdelijke bestanden te vermijden in een beperkte omgeving.

---

## Verwachte output

Na het uitvoeren van het zes‑stappen‑voorbeeld bevat `output.xlsx` het volgende:

| A               | B          | C            |
|-----------------|------------|--------------|
| WerknemerNaam   | Jane Doe   |              |
| Afdeling        | Engineering|              |
| Salaris         | 95.000     |              |
| RapportDatum    | 2026‑06‑30 |              |
| …               | …          | …            |

Als je het tabel‑voorbeeld hebt toegevoegd, zie je een volledig ingevulde verkooptabel direct onder de koprijen. Alle opmaak die je in `input.xlsx` hebt toegepast (valutasymbolen, datumformaten, vetgedrukte koppen) blijft behouden.

---

## Conclusie

We hebben zojuist laten zien hoe je **een Excel‑sjabloon vult met gegevens** gebruikt makend van Aspose.Cells’ `SmartMarkerProcessor`, en je weet nu precies hoe je **een Excel‑rapport maakt vanuit een sjabloon** in Java. Het kernidee is simpel: definieer Smart Markers in een herbruikbaar werkboek, lever een conforme `IDataSource`, en laat de bibliotheek het zware werk doen.  

Vanaf hier kun je:

- Een echte database aansluiten in plaats van de `MapDataSource`.  
- Grafieken toevoegen die automatisch de nieuwe data weergeven.  
- De code als microservice inzetten die het gegenereerde Excel‑bestand op aanvraag retourneert.  

Probeer het, pas de markers aan, en zie hoe je rapportage‑workflow drastisch krimpt. Vragen of een lastig marker‑scenario? Laat een reactie achter – happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel vullen met geneste data met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [XML‑data exporteren vanuit Excel met Aspose.Cells in Java: Stap‑voor‑stap‑gids](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [Hoe Excel‑cellen maken & opmaken met Aspose.Cells for Java: Een stap‑voor‑stap‑gids](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}