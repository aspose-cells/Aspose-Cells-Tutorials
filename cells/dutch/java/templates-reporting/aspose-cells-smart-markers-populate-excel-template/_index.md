---
category: general
date: 2026-06-30
description: Leer hoe u Aspose Cells Smart Markers kunt gebruiken om een Excel‑sjabloon
  te vullen en een Excel‑rapport te genereren in Java. Volledige stapsgewijze code
  inbegrepen.
draft: false
keywords:
- aspose cells smart markers
- populate excel template
- generate excel report
- load and save workbook
language: nl
og_description: Aspose Cells Smart Markers laten u een Excel‑sjabloon vullen met gegevens
  en een Excel‑rapport genereren in Java. Volg deze gids voor een volledige, uitvoerbare
  oplossing.
og_title: Aspose Cells Smart Markers – Vul Excel-sjabloon
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to use Aspose Cells Smart Markers to populate an Excel template
    and generate an Excel report in Java. Full step‑by‑step code included.
  headline: Aspose Cells Smart Markers – Populate Excel Template
  type: TechArticle
- description: Learn how to use Aspose Cells Smart Markers to populate an Excel template
    and generate an Excel report in Java. Full step‑by‑step code included.
  name: Aspose Cells Smart Markers – Populate Excel Template
  steps:
  - name: '**Loads** an existing Excel file that contains a smart‑marker placeholder.'
    text: '**Loads** an existing Excel file that contains a smart‑marker placeholder.'
  - name: '**Defines** a master‑detail template (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).'
    text: '**Defines** a master‑detail template (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).'
  - name: '**Creates** a `SmartMarkerProcessor` and a populated data model.'
    text: '**Creates** a `SmartMarkerProcessor` and a populated data model.'
  - name: '**Applies** the processor to the first worksheet.'
    text: '**Applies** the processor to the first worksheet.'
  - name: '**Saves** the workbook to a new file, giving you a ready‑to‑use report.'
    text: '**Saves** the workbook to a new file, giving you a ready‑to‑use report.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
- Smart Markers
title: Aspose Cells Smart Markers – Vul Excel‑sjabloon in
url: /nl/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Smart Markers – Excel‑sjabloon invullen

Heb je je ooit afgevraagd hoe je een **excel‑sjabloon** kunt **invullen** zonder eindeloze lussen en cel‑voor‑cel toewijzingen te schrijven? Het antwoord is vaak **Aspose Cells Smart Markers**, een declaratieve manier om je Java‑objecten direct aan een Excel‑werkmap te binden. In deze tutorial lopen we door het laden van een werkmap, het definiëren van een master‑detail smart‑marker‑sjabloon, het voeden van een datamodel, en tenslotte het opslaan van het resultaat als een volledig ingevuld **generate excel report**‑bestand.

Beschouw het als een mail‑merge voor spreadsheets: je ontwerpt de lay-out één keer, en laat de bibliotheek het zware werk doen. Geen handmatige `cell.setValue()`‑aanroepen meer, geen off‑by‑one‑fouten meer. Klaar om het in actie te zien?

## Wat je gaat bouwen

Aan het einde van deze gids heb je een Java‑programma dat:

1. **Laadt** een bestaand Excel‑bestand dat een smart‑marker‑placeholder bevat.
2. **Definieert** een master‑detail‑sjabloon (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).
3. **Maakt** een `SmartMarkerProcessor` en een gevulde datamodel.
4. **Past** de processor toe op het eerste werkblad.
5. **Slaat** de werkmap op naar een nieuw bestand, waardoor je een kant‑klaar rapport krijgt.

Je krijgt ook tips over het omgaan met grote datasets, meerdere werkbladen en veelvoorkomende valkuilen.

## Vereisten

- Java 8 of nieuwer (de code gebruikt de Stream‑API voor beknoptheid).
- Aspose.Cells for Java‑bibliotheek (download van [aspose.com/cells/java](https://products.aspose.com/cells/java/)).
- Een Excel‑bestand (`input.xlsx`) dat de smart‑marker‑placeholders zoals hieronder weergegeven bevat.
- Een basisbegrip van Java‑collecties en -maps.

Als je een van deze mist, haal ze dan nu op—anders, laten we beginnen.

![aspose cells smart markers workflow-diagram](image-url-placeholder.png)

## Stap 1 – Werkmap laden en opslaan

Het eerste wat we doen is **werkmap laden en opslaan**. Aspose.Cells abstraheert het bestandsformaat, zodat je kunt werken met `.xlsx`, `.xls` of zelfs `.csv` zonder een regel code te wijzigen.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the smart‑marker template
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // All processing happens here (see later steps)

        // Save the workbook with the populated data
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Pro tip:** Als je met enorme bestanden werkt, overweeg dan `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` te gebruiken om het geheugenverbruik laag te houden.

## Stap 2 – Ontwerp het Smart‑Marker‑sjabloon

Open `input.xlsx` in Excel en typ het volgende in een cel (meestal de eerste rij van een tabel):

```
${Orders.OrderId}
${Orders.Details:DetailRow}
```

- `${Orders.OrderId}` – haalt het `OrderId`‑veld op uit elk `Order`‑object.
- `${Orders.Details:DetailRow}` – vertelt Aspose de rij te herhalen voor elk item in de `Details`‑collectie (master‑detail).

Het `:DetailRow`‑achtervoegsel is de **detail‑marker**; het herhaalt de volledige rij voor elk element in de collectie, en past automatisch de rijnummers aan.

## Stap 3 – Maak de SmartMarkerProcessor

De processor is de werkpaard die het sjabloon leest, markers aan je gegevens koppelt en het resultaat terugschrijft naar het werkblad.

```java
// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Je kunt het gedrag aanpassen (bijv. `processor.setOptions(SmartMarkerOptions.REMOVE_EMPTY_ROWS);` inschakelen), maar de standaardinstellingen werken voor de meeste scenario's.

## Stap 4 – Bouw het datamodel

Aspose verwacht een `Map<String, Object>` waarbij de sleutel overeenkomt met de markernaam (`Orders` in ons geval). Hieronder staat een minimaal, *volledig* datamodel dat een master‑lijst van orders bevat, elk met een lijst van detailitems.

```java
import java.util.*;

public class DataProvider {
    // Returns a map that Aspose will use to replace the markers
    public static Map<String, Object> getOrderData() {
        List<Order> orders = new ArrayList<>();

        // Sample Order 1
        Order order1 = new Order(1001);
        order1.addDetail(new Detail("Apple", 3, 1.20));
        order1.addDetail(new Detail("Banana", 5, 0.80));
        orders.add(order1);

        // Sample Order 2
        Order order2 = new Order(1002);
        order2.addDetail(new Detail("Orange", 2, 1.50));
        order2.addDetail(new Detail("Grapes", 1, 2.00));
        orders.add(order2);

        // The key must match the marker name in the template
        Map<String, Object> model = new HashMap<>();
        model.put("Orders", orders);
        return model;
    }
}

// --- POJOs used above ----------------------------------------------------
class Order {
    private int orderId;
    private List<Detail> details = new ArrayList<>();

    public Order(int orderId) { this.orderId = orderId; }

    public int getOrderId() { return orderId; }

    public List<Detail> getDetails() { return details; }

    public void addDetail(Detail d) { details.add(d); }
}

class Detail {
    private String product;
    private int quantity;
    private double price;

    public Detail(String product, int quantity, double price) {
        this.product = product;
        this.quantity = quantity;
        this.price = price;
    }

    public String getProduct() { return product; }
    public int getQuantity() { return quantity; }
    public double getPrice() { return price; }
}
```

> **Waarom een Map?**  
> De smart‑marker‑engine gebruikt reflectie om property‑getters (`getOrderId()`, `getDetails()`) te lezen. Door een map te leveren, kun je elke objectgrafiek inwisselen zonder het sjabloon opnieuw te schrijven.

## Stap 5 – Pas de processor toe op het werkblad

Nu verbinden we alles. De processor scant het eerste werkblad (index 0) op markers, voegt de gegevens samen en breidt rijen uit indien nodig.

```java
// Inside main() after loading the workbook
Map<String, Object> dataModel = DataProvider.getOrderData();

// Apply the processor to the first worksheet using the model
processor.apply(wb.getWorksheets().get(0), dataModel);
```

Als je sjabloon zich op een ander blad bevindt, wijzig dan gewoon de index (`get(1)`, `get("Sheet2")`, enz.). De processor werkt ook over meerdere bladen in één oproep als je de volledige `Workbook` doorgeeft in plaats van een enkele `Worksheet`.

## Stap 6 – Controleer de output

Voer het programma uit. Open `output.xlsx` en je zou iets moeten zien zoals:

| OrderId | Product | Quantity | Price |
|--------|---------|----------|-------|
| 1001   | Apple   | 3        | 1.20  |
| 1001   | Banana  | 5        | 0.80  |
| 1002   | Orange  | 2        | 1.50  |
| 1002   | Grapes  | 1        | 2.00  |

Merk op hoe de master‑detail‑rijen automatisch worden gegenereerd—geen lussen, geen handmatige celreferenties. Dat is de kracht van **aspose cells smart markers**.

## Geavanceerde onderwerpen & randgevallen

### 1. Omgaan met grote datasets
Wanneer je een rapport moet genereren met tienduizenden rijen, schakel dan streaming in:



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel Smart Markers automatiseren met Aspose.Cells voor Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Aspose.Cells Java beheersen: Smart Markers & formules implementeren voor Excel‑automatisering](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)
- [Excel vullen met gegevens met Aspose.Cells en Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}