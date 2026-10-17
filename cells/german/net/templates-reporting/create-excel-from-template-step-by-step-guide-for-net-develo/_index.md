---
category: general
date: 2026-05-04
description: Erstelle Excel aus einer Vorlage und mappe JSON zu Excel mit dynamischer
  Arbeitsblattbenennung. Lerne, wie du Excel aus JSON befüllst und Excel mithilfe
  von JSON in wenigen Minuten generierst.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: de
og_description: Erstelle Excel schnell aus einer Vorlage. Dieser Leitfaden zeigt,
  wie man JSON nach Excel abbildet, Excel aus JSON befüllt, dynamische Arbeitsblattnamen
  verwendet und Excel mithilfe von JSON generiert.
og_title: Excel aus Vorlage erstellen – Vollständiges .NET‑Tutorial
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Excel aus Vorlage erstellen – Schritt‑für‑Schritt‑Anleitung für .NET‑Entwickler
url: /de/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel aus Vorlage erstellen – Komplettes .NET‑Tutorial

Haben Sie schon einmal **Excel aus einer Vorlage erstellen** müssen und waren dabei mit JSON‑Daten und Arbeitsblattnamen überfordert? Sie sind nicht allein. In vielen Reporting‑Projekten enthält die Vorlage das Layout, während die JSON‑Payload die eigentlichen Werte liefert – und diese beiden zum Laufen zu bringen, kann eine echte Herausforderung sein.  

Die gute Nachricht? Mit ein paar Zeilen C# und dem SmartMarker‑Engine von Aspose Cells können Sie **Excel aus JSON befüllen**, Detail‑Sheets zur Laufzeit umbenennen und schließlich **Excel mithilfe von JSON generieren**, ohne jemals die UI zu berühren.  

In diesem Tutorial gehen wir den gesamten Prozess durch: Laden einer Vorlage, Zuordnen von JSON zu Excel, Konfigurieren dynamischer Arbeitsblattnamen und Speichern der finalen Arbeitsmappe. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jeden .NET‑Service einbinden können. Keine externen Tools, nur reiner Code.

---

## Was Sie benötigen

- **Aspose.Cells for .NET** (v24.10 oder neuer) – die Bibliothek, die SmartMarker antreibt.  
- Eine **template.xlsx**‑Datei, die SmartMarker‑Tags wie `{Master:Name}` und `{Detail:Item}` enthält.  
- Eine **data.json**‑Datei, die der Master‑Detail‑Struktur entspricht.  
- Visual Studio 2022 (oder eine andere IDE Ihrer Wahl) mit Ziel‑Framework .NET 6 oder höher.

Das war’s. Wenn Sie diese Bestandteile bereits haben, können Sie loslegen.

---

## Excel aus Vorlage erstellen – Überblick

Die Grundidee ist simpel: Behandeln Sie die Excel‑Datei als *Vorlage* und lassen Sie SmartMarker Platzhalter durch Werte aus Ihrem JSON ersetzen. Die Bibliothek ermöglicht zudem das Umbenennen des Detail‑Worksheets basierend auf einem Master‑Feld – hier kommt **dynamic worksheet naming excel** zum Einsatz.

Unten finden Sie den vollständigen, sofort ausführbaren Code. Kopieren Sie ihn einfach in eine Konsolen‑App und passen Sie die Pfade an Ihre Dateien an.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Erwartetes Ergebnis:**  
> - Das Master‑Sheet zeigt den Namen aus `Master.Name`.  
> - Das Detail‑Sheet wird in etwa zu `Detail_JohnDoe` umbenannt.  
> - Alle `{Detail:Item}`‑Zeilen werden mit dem `items`‑Array aus dem JSON gefüllt.

---

## JSON zu Excel zuordnen – Daten laden

Bevor die SmartMarker‑Engine ihre Magie entfalten kann, muss das JSON **wohlgeformt** sein und die Hierarchie der Vorlage widerspiegeln. Ein typisches Master‑Detail‑JSON sieht so aus:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Warum das wichtig ist:**  
- Die Schlüssel `Master` und `Detail` entsprechen exakt den Tags `{Master:…}` und `{Detail:…}`.  
- Weicht die JSON‑Struktur ab, findet SmartMarker keine Übereinstimmung und die Zellen bleiben leer.  

**Tipp:** Validieren Sie Ihr JSON mit einem schnellen Online‑Validator oder mit `System.Text.Json.JsonDocument.Parse(json)`, um Syntaxfehler früh zu erkennen.

---

## Excel aus JSON befüllen – SmartMarker‑Einrichtung

SmartMarker scannt die Arbeitsmappe nach Tags und fügt dann Daten ein. Der **populate excel from json**‑Schritt ist im Wesentlichen der `Execute`‑Aufruf, den wir bereits gesehen haben, aber es gibt ein paar optionale Einstellungen, die erwähnenswert sind:

| Einstellung | Was sie bewirkt | Wann sie zu verwenden |
|------------|----------------|-----------------------|
| `Options.CaseSensitive` | Behandelt Tag‑Namen als case‑sensitive. | Wenn Ihre Vorlage gemischte Groß‑/Kleinschreibung verwendet und Sie strikte Übereinstimmung benötigen. |
| `Options.RemoveEmptyRows` | Löscht Zeilen, die keine Daten erhalten haben. | Um das fertige Sheet übersichtlich zu halten, wenn einige Detail‑Einträge optional sind. |
| `Options.EnableHyperlink` | Macht Hyperlinks aus dem JSON anklickbar. | Wenn Sie klickbare URLs im Report benötigen. |

Sie können sie so verketten:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Dynamic Worksheet Naming Excel – Detail‑Sheet‑Name konfigurieren

Eine der kniffligeren Anforderungen vieler Projekte ist **dynamic worksheet naming excel**. Statt eines statischen „Detail“-Sheets möchten Sie vielleicht, dass jeder Report den Kundennamen oder eine Bestellnummer trägt.

Die Zeile:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

macht genau das. Der Platzhalter `{Master.Name}` wird *nach* der JSON‑Verarbeitung ersetzt, sodass der neue Sheet‑Name `Detail_JohnDoe` wird.  

**Randfall:** Enthält der Name Zeichen, die in Sheet‑Namen nicht erlaubt sind (`:`, `\`, `/`, `?`, `*`, `[`, `]`), bereinigt Aspose sie automatisch. Sie können den String jedoch bereits im JSON vor‑bereinigen, wenn Sie ein bestimmtes Format benötigen.

---

## Excel mit JSON generieren – Ausführen und Speichern

Die letzten beiden Zeilen des Codes (`Execute` und `Save`) sind dort, wo die **generate excel using json**‑Magie passiert. Im Hintergrund parst Aspose das JSON in eine Datentabelle, iteriert über die Vorlage und schreibt die Ausgabedatei.

Wenn Sie mehrere Arbeitsmappen in einer Schleife erzeugen müssen (z. B. eine pro Kunde), verschieben Sie die `Workbook`‑Instanziierung einfach in die Schleife und passen den Ausgabedateinamen an:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Dieses Muster ist in Batch‑Reporting‑Services üblich.

---

## Häufige Stolperfallen & Pro‑Tipps

- **Fehlende Tags:** Zeigt eine Zelle noch `{Master:Name}`, wurde das Tag nicht erkannt. Prüfen Sie Rechtschreibung und ob das Tag innerhalb einer Zelle und nicht in einem Kommentar steht.  
- **Große JSON‑Payloads:** Bei riesigen Datensätzen sollten Sie das JSON streamen oder ein `DataTable` statt eines rohen Strings verwenden, um den Speicherverbrauch zu reduzieren.  
- **Thread‑Safety:** `Workbook`‑Instanzen sind nicht thread‑sicher. Erzeugen Sie pro Thread eine neue Instanz, wenn Sie parallele Jobs ausführen.  
- **Dateisperren:** Stellen Sie sicher, dass die Vorlage nicht in Excel geöffnet ist, während Ihr Code läuft; sonst erhalten Sie eine `IOException`.  

> **Pro‑Tipp:** Legen Sie eine Kopie der Originalvorlage in einem schreibgeschützten Ordner ab. Das verhindert versehentliche Überschreibungen beim Debuggen.

---

## Vollständiges funktionierendes Beispiel – Zusammenfassung

Hier noch einmal das gesamte Programm, diesmal mit Inline‑Kommentaren zu jeder nicht‑offensichtlichen Zeile:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Führen Sie diese Konsolen‑App aus, erzeugt sie `output.xlsx` mit einem umbenannten Detail‑Sheet und allen Daten gefüllt.

---

## Nächste Schritte & verwandte Themen

- **Export nach PDF:** Nach dem Erzeugen der Arbeitsmappe können Sie `wb.Save("report.pdf", SaveFormat.Pdf);` aufrufen, um eine PDF‑Version zu liefern.  
- **Diagramme befüllen:** SmartMarker unterstützt auch Diagrammdatenquellen; binden Sie einfach das JSON‑Array an den Datenbereich der Diagramm‑Serie.  
- **Bedingte Formatierung:** Nutzen Sie die integrierten Regeln von Excel in der Vorlage; sie bleiben nach dem SmartMarker‑Ersetzen erhalten.  
- **Performance‑Optimierung:** Für Szenarien mit hohem Volumen können Sie eine einzelne `Workbook`‑Instanz mit `Clone` wiederverwenden, um wiederholte Datei‑I/O zu vermeiden.

Experimentieren Sie gern mit unterschiedlichen JSON‑Strukturen, Umbenennungs‑Mustern oder sogar mit mehreren Vorlagen in einem Durchlauf. Die Flexibilität von **create excel from template** mit Aspose.Cells erlaubt Ihnen, die Lösung an Rechnungen, Dashboards oder jede andere Reporting‑Anforderung anzupassen.

---

## Visuelle Zusammenfassung

![Create Excel from Template workflow showing JSON → SmartMarker → Dynamic Sheet Naming](/images/create-excel-from-template-workflow.png "Create Excel from Template workflow diagram")

*(Alt‑Text enthält das Haupt‑Keyword für SEO)*

---

### Abschluss

Wir haben alles behandelt, was Sie benötigen, um **Excel aus einer Vorlage zu erstellen**, **JSON zu Excel zuzuordnen**, **Excel aus JSON zu befüllen**, **dynamic worksheet naming excel** zu nutzen und schließlich **Excel mit JSON zu generieren**. Der Code ist vollständig, die Erklärungen zeigen *warum* jede Zeile wichtig ist, und Sie verfügen nun über ein solides Fundament, um größere Reporting‑Pipelines zu bauen.

Haben Sie eine besondere Anforderung, die Sie umsetzen möchten? Hinterlassen Sie einen Kommentar unten, und wir lösen das gemeinsam. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}