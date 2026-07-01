---
category: general
date: 2026-06-30
description: Erfahren Sie, wie Sie Aspose Cells Smart Markers verwenden, um eine Excel‑Vorlage
  zu füllen und einen Excel‑Bericht in Java zu erstellen. Vollständiger Schritt‑für‑Schritt‑Code
  ist enthalten.
draft: false
keywords:
- aspose cells smart markers
- populate excel template
- generate excel report
- load and save workbook
language: de
og_description: Aspose Cells Smart Markers ermöglichen es Ihnen, eine Excel‑Vorlage
  mit Daten zu füllen und einen Excel‑Bericht in Java zu erstellen. Folgen Sie dieser
  Anleitung für eine vollständige, ausführbare Lösung.
og_title: Aspose Cells Smart Markers – Excel‑Vorlage ausfüllen
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
title: Aspose Cells Smart Markers – Excel‑Vorlage ausfüllen
url: /de/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Smart Markers – Excel-Vorlage ausfüllen

Haben Sie sich jemals gefragt, wie man **populate excel template** ausfüllt, ohne endlose Schleifen und Zelle‑für‑Zelle‑Zuweisungen zu schreiben? Die Antwort ist häufig **Aspose Cells Smart Markers**, ein deklarativer Weg, Ihre Java‑Objekte direkt in ein Excel‑Arbeitsbuch zu binden. In diesem Tutorial führen wir Sie durch das Laden eines Arbeitsbuchs, das Definieren einer Master‑Detail‑Smart‑Marker‑Vorlage, das Befüllen mit einem Datenmodell und schließlich das Speichern des Ergebnisses als vollständig ausgefüllte **generate excel report**‑Datei.

Stellen Sie sich das wie einen Seriendruck für Tabellenkalkulationen vor: Sie entwerfen das Layout einmal und lassen dann die Bibliothek die schwere Arbeit übernehmen. Keine manuellen `cell.setValue()`‑Aufrufe mehr, keine Off‑by‑One‑Fehler mehr. Bereit, es in Aktion zu sehen?

## Was Sie erstellen werden

Am Ende dieses Leitfadens haben Sie ein Java‑Programm, das:

1. **Loads** eine vorhandene Excel‑Datei, die einen Smart‑Marker‑Platzhalter enthält.
2. **Defines** eine Master‑Detail‑Vorlage (`${Orders.OrderId}` … `${Orders.Details:DetailRow}`).
3. **Creates** einen `SmartMarkerProcessor` und ein befülltes Datenmodell.
4. **Applies** den Prozessor auf das erste Arbeitsblatt.
5. **Saves** das Arbeitsbuch in einer neuen Datei, sodass Sie einen sofort einsatzbereiten Bericht erhalten.

Sie erhalten außerdem Tipps zum Umgang mit großen Datenmengen, mehreren Arbeitsblättern und häufigen Fallstricken.

## Voraussetzungen

- Java 8 oder neuer (der Code nutzt die Stream‑API für Kürze).
- Aspose.Cells for Java‑Bibliothek (Download von [aspose.com/cells/java](https://products.aspose.com/cells/java/)).
- Eine Excel‑Datei (`input.xlsx`), die die unten gezeigten Smart‑Marker‑Platzhalter enthält.
- Grundlegendes Verständnis von Java‑Collections und Maps.

Wenn Ihnen etwas davon fehlt, holen Sie es jetzt – andernfalls können wir loslegen.

![aspose cells smart markers workflow diagram](image-url-placeholder.png)

## Schritt 1 – Arbeitsbuch laden und speichern

Das Erste, was wir tun, ist **load and save workbook**. Aspose.Cells abstrahiert das Dateiformat, sodass Sie mit `.xlsx`, `.xls` oder sogar `.csv` arbeiten können, ohne eine Codezeile zu ändern.

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

> **Pro Tipp:** Wenn Sie mit riesigen Dateien arbeiten, sollten Sie `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` verwenden, um den Speicherverbrauch gering zu halten.

## Schritt 2 – Smart‑Marker‑Vorlage entwerfen

Öffnen Sie `input.xlsx` in Excel und geben Sie das Folgende in eine Zelle ein (gewöhnlich die erste Zeile einer Tabelle):

```
${Orders.OrderId}
${Orders.Details:DetailRow}
```

- `${Orders.OrderId}` – ruft das Feld `OrderId` jedes `Order`‑Objekts ab.
- `${Orders.Details:DetailRow}` – weist Aspose an, die Zeile für jedes Element in der `Details`‑Sammlung zu wiederholen (Master‑Detail).

Der Suffix `:DetailRow` ist der **detail marker**; er wiederholt die gesamte Zeile für jedes Element in der Sammlung und passt dabei automatisch die Zeilennummern an.

## Schritt 3 – SmartMarkerProcessor erstellen

Der Prozessor ist das Arbeitspferd, das die Vorlage liest, Marker mit Ihren Daten abgleicht und das Ergebnis zurück in das Arbeitsblatt schreibt.

```java
// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Sie können sein Verhalten anpassen (z. B. `processor.setOptions(SmartMarkerOptions.REMOVE_EMPTY_ROWS);` aktivieren), aber die Standardeinstellungen funktionieren für die meisten Szenarien.

## Schritt 4 – Datenmodell erstellen

Aspose erwartet ein `Map<String, Object>`, bei dem der Schlüssel dem Markernamen entspricht (`Orders` in unserem Fall). Unten finden Sie ein minimales, *vollständiges* Datenmodell, das eine Master‑Liste von Bestellungen enthält, wobei jede Bestellung eine Liste von Detail‑Elementen hat.

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

> **Warum ein Map?**  
> Die Smart‑Marker‑Engine verwendet Reflection, um Property‑Getter (`getOrderId()`, `getDetails()`) zu lesen. Durch die Bereitstellung einer Map können Sie jede Objektstruktur austauschen, ohne die Vorlage neu zu schreiben.

## Schritt 5 – Prozessor auf das Arbeitsblatt anwenden

Jetzt verbinden wir alles. Der Prozessor scannt das erste Arbeitsblatt (Index 0) nach Markern, fügt die Daten zusammen und erweitert bei Bedarf die Zeilen.

```java
// Inside main() after loading the workbook
Map<String, Object> dataModel = DataProvider.getOrderData();

// Apply the processor to the first worksheet using the model
processor.apply(wb.getWorksheets().get(0), dataModel);
```

Wenn sich Ihre Vorlage auf einem anderen Blatt befindet, ändern Sie einfach den Index (`get(1)`, `get("Sheet2")` usw.). Der Prozessor funktioniert auch über mehrere Blätter hinweg in einem Aufruf, wenn Sie das gesamte `Workbook` anstelle eines einzelnen `Worksheet` übergeben.

## Schritt 6 – Ausgabe überprüfen

Führen Sie das Programm aus. Öffnen Sie `output.xlsx` und Sie sollten etwa Folgendes sehen:

| OrderId | Product | Quantity | Price |
|--------|---------|----------|-------|
| 1001   | Apple   | 3        | 1.20  |
| 1001   | Banana  | 5        | 0.80  |
| 1002   | Orange  | 2        | 1.50  |
| 1002   | Grapes  | 1        | 2.00  |

Beachten Sie, wie die Master‑Detail‑Zeilen automatisch erzeugt werden – keine Schleifen, keine manuellen Zellreferenzen. Das ist die Kraft von **aspose cells smart markers**.

## Fortgeschrittene Themen & Sonderfälle

### 1. Umgang mit großen Datenmengen
Wenn Sie einen Bericht mit Zehntausenden von Zeilen erzeugen müssen, aktivieren Sie Streaming:



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Automate Excel Smart Markers with Aspose.Cells for Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Mastering Aspose.Cells Java: Implement Smart Markers & Formulas for Excel Automation](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)
- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}