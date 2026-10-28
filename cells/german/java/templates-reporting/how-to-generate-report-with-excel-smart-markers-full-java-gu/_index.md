---
category: general
date: 2026-07-03
description: Wie man einen Bericht erstellt, indem man eine Excel‑Vorlage mit Smart
  Markern füllt. Lernen Sie, ein Detailblatt zu erstellen, Smart Marker zu verwenden
  und die Dateneinfügung zu automatisieren.
draft: false
keywords:
- how to generate report
- populate excel template
- how to create detail
- create detail sheet
- use smart markers
language: de
og_description: Wie man Berichte mit Smart Markers in Java erstellt. Dieser Leitfaden
  zeigt, wie man eine Excel‑Vorlage füllt, ein Detailblatt erstellt und Master‑Detail‑Berichte
  automatisiert.
og_title: Wie man Berichte mit Excel Smart Markers erstellt – Java‑Tutorial
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
title: Wie man einen Bericht mit Excel Smart Markern erstellt – Vollständiger Java‑Leitfaden
url: /de/java/templates-reporting/how-to-generate-report-with-excel-smart-markers-full-java-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So erstellen Sie Berichte mit Excel Smart Markers – Vollständige Java‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man einen Bericht** aus einer Excel‑Vorlage erzeugt, ohne Millionen Zeilen Schleifen‑Code zu schreiben? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie Daten aus einer Datenbank holen, in eine Master‑Detail‑Arbeitsmappe einfügen und dabei das Layout professionell halten wollen.  

Die gute Nachricht? Mit Aspose.Cells **Smart Markers** können Sie **eine Excel‑Vorlage** in einem einzigen, lesbaren Aufruf befüllen – ohne umständliche Zelle‑für‑Zelle‑Gymnastik. In diesem Tutorial führen wir Sie durch den gesamten Prozess, von der Vorbereitung der Vorlage bis zum Speichern der finalen Datei, und zeigen Ihnen außerdem **wie man Detail‑Sheets** zur Laufzeit erstellt.

Am Ende dieses Leitfadens können Sie:

* Eine vorgefertigte Arbeitsmappe laden, die als Master‑Sheet dient.  
* Einen Smart‑Marker‑Platzhalter einfügen, den Aspose durch echte Bestelldaten ersetzt.  
* Eine Java `Map` als Datenquelle übergeben und die **create detail sheet**‑Optionen konfigurieren.  
* Den Prozessor ausführen und einen professionellen Master‑Detail‑Bericht erhalten, der sofort geteilt werden kann.

> **Pro‑Tipp:** Wenn Sie bereits eine Vorlage haben, die Ihr Business‑Team liebt, müssen Sie das Layout überhaupt nicht ändern – setzen Sie einfach die Smart‑Marker‑Tags in die richtigen Zellen.

---

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie Folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Aspose.Cells for Java** (neueste Version) | Stellt `SmartMarkerProcessor`, `Workbook` und zugehörige APIs bereit. |
| **Java 8+** | Das Beispiel verwendet Streams und die `Map.of`‑Factory‑Methode, die in Java 9 eingeführt wurde; passen Sie es an, falls Sie Java 8 nutzen. |
| **Eine Excel‑Vorlage** (`template.xlsx`) mit einer Platzhalterzelle für den Smart Marker | Dies ist die Datei, die Sie laden und später als `masterDetail.xlsx` speichern. |
| **Ein einfaches Datenmodell** (z. B. `Order`‑Klasse) | Gibt dem Prozessor etwas Konkretes, das die Marker ersetzen können. |

Falls Sie Aspose.Cells noch nicht besitzen, holen Sie sich eine kostenlose Testversion von der offiziellen Website und fügen Sie das JAR Ihrem Projekt‑Classpath hinzu.

---

## Schritt 1: Excel‑Vorlage einrichten (populate excel template)

Öffnen Sie Excel und erstellen Sie eine Arbeitsmappe namens `template.xlsx`. Geben Sie in Zelle **A1** des ersten Blatts den Smart‑Marker‑Tag ein:

```
{{Detail:Orders}}
```

Dieser Tag weist Aspose an, die `Orders`‑Sammlung als **Detail**‑Datensatz zu behandeln und für jedes Element Zeilen zu erzeugen. Speichern Sie die Datei in einem Ordner, den Sie später referenzieren, z. B. `C:/Reports/`.

> **Warum das wichtig ist:** Durch das Einbetten des Markers direkt in die Vorlage bleibt das visuelle Design vom Code getrennt. Designer können Schriftarten, Farben und Formeln anpassen, ohne Java zu berühren.

---

## Schritt 2: Projektstruktur in Java erstellen

Hier ein minimales Maven‑`pom.xml`‑Snippet, das Aspose.Cells einbindet:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

Erzeugen Sie das Paket `com.example.report` und fügen Sie zwei Klassen hinzu: `ReportGenerator` (der Haupttreiber) und `Order` (unser Datenmodell).

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

## Schritt 3: Arbeitsmappe laden und Smart Marker einfügen (use smart markers)

Jetzt schreiben wir die Kernlogik. Beachten Sie, wie der Code das ursprüngliche Snippet spiegelt, jedoch Importe, Fehlerbehandlung und Kommentare zur Klarheit hinzufügt.

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

### Was der Code Schritt für Schritt macht

| Schritt | Erklärung |
|---------|-----------|
| **Arbeitsmappe laden** | Liest die Vorlage und bewahrt sämtliche Formatierungen. |
| **Marker einfügen** | Stellt sicher, dass der Platzhalter existiert, selbst wenn Sie die Vorlage programmatisch erstellt haben. |
| **Daten vorbereiten** | Der `Map`‑Schlüssel (`"Orders"`) muss mit dem Smart‑Marker‑Tag (`{{Detail:Orders}}`) übereinstimmen. |
| **Optionen konfigurieren** | `setDetailSheetNewName` weist Aspose an, ein **create detail sheet** namens *OrderDetail* zu erzeugen. |
| **Verarbeiten** | Der `SmartMarkerProcessor` durchläuft die Arbeitsmappe, ersetzt den Tag und erzeugt Zeilen im neuen Blatt. |
| **Speichern** | Schreibt die finale `masterDetail.xlsx` auf die Festplatte. |

> **Warum Smart Markers verwenden?** Sie beschreiben *was* Sie wollen (eine Tabelle mit Bestellungen), nicht *wie* Sie Zeilen und Spalten durchlaufen. Die Bibliothek übernimmt Paginierung, Stilkopieren und sogar die Neuberechnung von Formeln automatisch.

---

## Schritt 4: Ausgabe prüfen (how to generate report – verification)

Führen Sie die Klasse `ReportGenerator` aus. Nach der Ausführung sollten Sie zwei Arbeitsblätter sehen:

1. **Sheet1** – das ursprüngliche Master‑Sheet (enthält weiterhin `{{Detail:Orders}}`, aber der Prozessor blendet es aus).  
2. **OrderDetail** – ein brandneues Blatt mit einer Zeile pro `Order`‑Objekt:

| Order ID | Customer   | Amount |
|----------|------------|--------|
| ORD001   | Acme Corp  | 1250.75|
| ORD002   | Beta Ltd.  | 980.00 |
| ORD003   | Gamma Inc. | 432.50 |

Öffnen Sie die Datei in Excel, werden Sie feststellen, dass Spaltenbreiten, Schriftarten und alle vorab angewendeten Stile aus der Vorlage erhalten bleiben. Das ist die Schönheit von **use smart markers**: Sie bewahren die Präsentation und fügen gleichzeitig Daten ein.

---

## Schritt 5: Häufige Varianten & Sonderfälle (populate excel template, how to create detail)

### 5.1 Mehrere Detail‑Datensätze

Sie können mehrere Smart Markers in derselben Vorlage einbetten, z. B. `{{Detail:Customers}}` und `{{Detail:Orders}}`. Fügen Sie einfach entsprechende Einträge zur `Map` hinzu:

```java
data.put("Customers", getCustomers());
data.put("Orders", getOrders());
```

Jeder Eintrag erzeugt ein eigenes Blatt, wenn Sie `DetailSheetNewName` passend setzen.

### 5.2 Benutzerdefinierte Blattnamen pro Zeile

Falls Sie für jede Bestellung ein separates Blatt benötigen (statt eines einzigen Detail‑Blatts), verwenden Sie das `DetailSheetNewName`‑Muster mit Platzhaltern:

```java
smOpt.setDetailSheetNewName("Order_{OrderId}");
```

Aspose ersetzt `{OrderId}` durch den tatsächlichen Wert jeder Zeile.

### 5.3 Umgang mit großen Datensätzen

Bei tausenden Zeilen aktivieren Sie das Streaming, um den Speicherverbrauch gering zu halten:

```java
WorkbookSettings ws = wb.getSettings();
ws.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 5.4 Zahlen‑ und Datumsformatierung

Smart Markers respektieren das vorhandene Zellenformat. Ist Spalte B in der Vorlage als **Currency** formatiert, werden die Beträge automatisch mit dem richtigen Symbol angezeigt. Für benutzerdefinierte Datumsformate setzen Sie das Zahlenformat der Zelle einfach vor der Verarbeitung.

---

## Schritt 6: Tipps & Stolperfallen (how to create detail, use smart markers)

* **Nie Dateipfade hartkodieren** in der Produktion. Nutzen Sie eine Konfigurationsdatei oder Umgebungsvariablen.
* **Ressourcen immer schließen**, wenn Sie Streams manuell öffnen; die `Workbook`‑Klasse implementiert in neueren Versionen `AutoCloseable`.
* **Auf Namenskollisionen achten** – existiert bereits ein Blatt mit demselben Namen, hängt Aspose eine numerische Endung an. Für eindeutige Namen prefixed Sie den Namen mit einem Zeitstempel.
* **Leere Sammlungen testen**. Ist `Orders` leer, erstellt der Prozessor trotzdem das Blatt, lässt es jedoch leer – behandeln Sie das downstream, wenn Sie unnötige Tabs vermeiden wollen.
* **Debugging von Smart Markers**: Setzen Sie `smOpt.setThrowExceptionOnMissingData(true)`, um eine klare Ausnahme zu erhalten, wenn ein Marker zu keinen Daten passt.

---

![How to generate report using Smart Markers in Java](/images/how-to-generate-report-smart-markers.png "how to generate report")

*Bildunterschrift: Die finale `masterDetail.xlsx` mit dem Master‑Sheet und dem erzeugten **OrderDetail**‑Sheet.*

---

## Fazit

Wir haben gerade demonstriert, **wie man einen Bericht erzeugt**, indem man eine Excel‑Vorlage mit Aspose.Cells Smart Markers befüllt, und wir haben alles behandelt, was Sie benötigen, um **automatisch Detail‑Sheets** zu erstellen. Der Ansatz bewahrt das Layout und automatisiert die Dateninjektion.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [How to Automate Excel Smart Markers with Aspose.Cells for Java](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}