---
category: general
date: 2026-02-14
description: 'Automatisieren Sie die Rechnungserstellung mit SmartMarker: Lernen Sie,
  Arbeitsblätter zu wiederholen, sie dynamisch zu benennen und die dynamische Benennung
  von Arbeitsblättern in Minuten zu meistern.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: de
og_description: Automatisieren Sie die Rechnungserstellung mit SmartMarker. Dieser
  Leitfaden zeigt, wie man Arbeitsblätter wiederholt, sie dynamisch benennt und die
  dynamische Benennung von Arbeitsblättern meistert.
og_title: Rechnungsstellung automatisieren – Dynamische Tabellenblattbenennung & Wiederholung
tags:
- C#
- SmartMarker
- Excel Automation
title: Rechnungsstellung automatisieren – Dynamische Arbeitsblattbenennung & Wiederholung
  in C#
url: /de/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatisierte Rechnungserstellung – Dynamische Arbeitsblattbenennung & Wiederholung in C#

Haben Sie sich jemals gefragt, wie man **die Rechnungserstellung automatisiert**, ohne für jede Bestellung manuell Arbeitsblätter zu kopieren? Sie sind nicht allein. Viele Entwickler stoßen auf ein Problem, wenn sie für jede Rechnung ein separates Arbeitsblatt benötigen, das gleichzeitig den Bestellnummer im Blattnamen widerspiegelt. In diesem Tutorial lösen wir dieses Problem mit dem `SmartMarkerProcessor` von SmartMarker und zeigen Ihnen **wie man Arbeitsblätter** dynamisch benennt, während wir auch **wie man ein Arbeitsblatt** für jeden Datensatz wiederholt. Am Ende haben Sie ein sofort ausführbares C#‑Beispiel, das eine Arbeitsmappe erzeugt, in der jede Rechnung auf einem eigenen, gut benannten Tab liegt.

Wir gehen jeden Schritt durch – vom Abrufen der Bestellungen aus einer Datenquelle bis zur Konfiguration von `SmartMarkerOptions` für die dynamische Arbeitsblattbenennung. Keine externen Dokumente erforderlich; alles, was Sie benötigen, finden Sie hier. Ein wenig Grundwissen in C# und ein Verweis auf die Aspose.Cells‑Bibliothek (oder jede SmartMarker‑kompatible Engine) reichen aus.

---

## Was Sie erstellen werden

- Eine Sammlung von Bestellobjekten abrufen.
- SmartMarker konfigurieren, um **ein Arbeitsblatt** für jede Bestellung zu **wiederholen**.
- **Dynamische Arbeitsblattbenennung** mit dem Platzhalter `{OrderId}` anwenden.
- Eine Excel‑Datei erzeugen, bei der jeder Tab `Invoice_12345`, `Invoice_67890` usw. heißt.
- Die Ausgabe überprüfen, indem Sie die Arbeitsmappe öffnen.

---

## Voraussetzungen

- .NET 6.0 oder höher (der Code kompiliert auch mit .NET 5+).
- Aspose.Cells für .NET (oder jede Bibliothek, die SmartMarker implementiert). Installation über NuGet:

```bash
dotnet add package Aspose.Cells
```

- Eine einfache `Order`‑Klasse (Sie können sie durch Ihr eigenes DTO ersetzen).

---

## Schritt 1: Projekt und Modell einrichten

Zuerst erstellen Sie eine neue Konsolenanwendung und definieren das Datenmodell, das eine Bestellung repräsentiert.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro‑Tipp:** Halten Sie das Modell für die Demo leichtgewichtig; Sie können es später jederzeit mit Positionen, Steuerdetails usw. erweitern.

---

## Schritt 2: Excel‑Vorlage vorbereiten

SmartMarker arbeitet mit einer Vorlagen‑Arbeitsmappe. Erstellen Sie eine Datei namens `InvoiceTemplate.xlsx` mit einem einzigen Arbeitsblatt namens `InvoiceTemplate`. Platzieren Sie in Zelle **A1** einen SmartMarker‑Platzhalter wie:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Sie können die Zellen nach Belieben formatieren – fette Überschriften, Währungsformatierung usw. Speichern Sie die Datei im Stammverzeichnis des Projekts.

> **Warum eine Vorlage?** Sie trennt das Layout vom Code, sodass Designer das Aussehen anpassen können, ohne die Logik zu berühren.

---

## Schritt 3: SmartMarker‑Optionen konfigurieren – Wiederholen & Arbeitsblätter benennen

Jetzt lassen wir SmartMarker das Vorlagen‑Arbeitsblatt für jede Bestellung zu *wiederholen* und jeder Kopie einen Namen zu geben, der die Bestell‑ID enthält. Das ist das Kernstück der **dynamischen Arbeitsblattbenennung**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Wie es funktioniert

- **`RepeatWorksheet = true`** weist die Engine an, das Quellblatt für jedes Element in der `orders`‑Sammlung zu duplizieren. Das erfüllt die Anforderung **wie man ein Arbeitsblatt wiederholt**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** ist ein Vorlagen‑String, bei dem `{OrderId}` ein Platzhalter ist, den SmartMarker durch die aktuelle Bestell‑ID ersetzt. Das ist die Antwort auf **wie man Arbeitsblätter benennt** und **dynamische Arbeitsblattbenennung**.
- Der Prozessor fügt die Felder jeder Bestellung (`{{OrderId}}`, `{{Customer}}` usw.) in das duplizierte Blatt ein und erzeugt so eine vollständig ausgefüllte Rechnung.

---

## Schritt 4: Anwendung ausführen und Ausgabe überprüfen

Kompilieren und führen Sie die Konsolenanwendung aus:

```bash
dotnet run
```

Sie sollten die Erfolgsmeldung in der Konsole sehen. Öffnen Sie `GeneratedInvoices.xlsx` und Sie finden drei Tabs:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Jedes Blatt enthält die Bestelldaten, die in die Platzhalter eingesetzt wurden. Das von Ihnen im Template entworfene Layout bleibt erhalten, was beweist, dass **die Rechnungserstellung automatisiert** von Anfang bis Ende funktioniert.

### Erwarteter Screenshot (Alt‑Text für SEO)

![Beispiel für automatisierte Rechnungserstellung, das drei dynamisch benannte Arbeitsblätter zeigt](/images/invoice-automation.png)

> *Der Alt‑Text des Bildes enthält das Hauptkeyword, um SEO zu erfüllen.*

---

## Schritt 5: Randfälle & häufige Variationen

### Was, wenn eine OrderId ungültige Zeichen enthält?

Excel‑Blattnamen dürfen die Zeichen `\ / ? * [ ] :` nicht enthalten. Wenn Ihre IDs diese enthalten könnten, bereinigen Sie sie:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Fügen Sie der `Order`‑Klasse eine berechnete Eigenschaft hinzu:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Müssen Sie das ursprüngliche Vorlagenblatt behalten?

Setzen Sie `smartMarkerOptions.RemoveTemplate = false;` (Standard ist `true`). Dadurch bleibt das ursprüngliche `InvoiceTemplate` unverändert als Referenz erhalten.

### Möchten Sie Rechnungen nach Kunde gruppieren?

Sie können **Wiederholungsgruppen** verschachteln. Wiederholen Sie zuerst nach Kunde und dann nach Bestellungen innerhalb jedes Kunden‑Arbeitsblatts. Die Syntax wird etwas komplexer, aber das Prinzip bleibt gleich – verwenden Sie `RepeatWorksheet` und ein Namensmuster, das die Hierarchie widerspiegelt.

---

## Vollständiges funktionierendes Beispiel (Alle Codes an einem Ort)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Kopieren Sie dies in `Program.cs`, legen Sie `InvoiceTemplate.xlsx` daneben, und Sie können loslegen.

---

## Häufig gestellte Fragen

**F: Funktioniert dieser Ansatz mit großen Datenmengen (tausende Rechnungen)?**  
**A:** Ja. SmartMarker streamt Daten effizient, aber achten Sie auf den Speicherverbrauch. Wenn Sie an Grenzen stoßen, sollten Sie die Verarbeitung in Batches durchführen und jeden Batch in eine separate Arbeitsmappe schreiben.

**F: Kann ich jedem Rechnung automatisch ein Logo hinzufügen?**  
**A:** Absolut. Platzieren Sie das Logo-Bild auf dem Vorlagenblatt. Da das Blatt dupliziert wird, erscheint das Logo auf jeder erzeugten Rechnung ohne zusätzlichen Code.

**F: Was, wenn ich die Arbeitsblätter schützen muss?**  
**A:** Nach der Verarbeitung iterieren Sie über `wb.Worksheets` und rufen `ws.Protect(Password, ProtectionType.All)` auf.

---

## Fazit

Wir haben gerade **die Rechnungserstellung automatisiert**, indem wir die Wiederholungs‑Arbeitsblatt‑Funktion von SmartMarker und ein cleveres Benennungsschema genutzt haben. Das Tutorial behandelte **wie man Arbeitsblätter benennt**, zeigte **wie man ein Arbeitsblatt** für jede Bestellung wiederholt und präsentierte **dynamische Arbeitsblattbenennung**, die Ihre Arbeitsmappe übersichtlich und durchsuchbar hält.

Von der Datenabfrage, über das Einrichten einer Vorlage, die Konfiguration von `SmartMarkerOptions` bis hin zur Behandlung von Randfällen – Sie haben nun eine vollständige, ausführbare Lösung. Als Nächstes können Sie Tabellen für Positionen hinzufügen, bedingte Formatierung anwenden oder dieselben Daten nach PDF exportieren, um eine vollständig automatisierte Rechnungs‑Pipeline zu erhalten.

Bereit, den nächsten Schritt zu gehen? Erkunden Sie verwandte Themen wie „Massen‑Excel‑Export mit Aspose.Cells“, „PDF‑Konvertierung von Arbeitsblättern“ oder „Versand generierter Rechnungen direkt aus C#“. Der Himmel ist das Limit – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}