---
category: general
date: 2026-10-01
description: Erfahren Sie, wie Sie benutzerdefinierte Eigenschaften zu einer Excel‑Arbeitsmappe
  mit Aspose.Cells hinzufügen. Dieser Leitfaden zeigt außerdem, wie Sie eine Projekt‑ID
  hinzufügen und benutzerdefinierte Eigenschaften auslesen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: de
lastmod: 2026-10-01
og_description: Fügen Sie einer Excel‑Arbeitsmappe benutzerdefinierte Eigenschaften
  mit Aspose.Cells hinzu. Folgen Sie diesem vollständigen Tutorial, um eine Projekt‑ID
  hinzuzufügen, Reviewer‑Informationen festzulegen und benutzerdefinierte Eigenschaften
  programmgesteuert auszulesen.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Benutzerdefinierte Eigenschaften zu einer Excel‑Arbeitsmappe hinzufügen
  – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man benutzerdefinierte Eigenschaften zu einer Excel‑Arbeitsmappe hinzufügt
url: /de/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man benutzerdefinierte Eigenschaften zu einer Excel‑Arbeitsmappe hinzufügt

Wenn Sie **benutzerdefinierte Eigenschaften** zu einer Excel‑Arbeitsmappe hinzufügen müssen, zeigt Ihnen diese Anleitung genau, wie Sie dies mit Aspose.Cells für .NET erledigen. Außerdem erfahren Sie, wie Sie eine Projekt‑ID, einen Prüfer‑Namen festlegen und später **benutzerdefinierte Eigenschaften** aus der Datei **auslesen** können.

Die Arbeit mit benutzerdefinierten Metadaten ermöglicht es Ihnen, geschäftsspezifische Informationen direkt in die Tabelle einzubetten, sodass Sie Eigentümerschaft, Version oder andere Kontexte leicht nachverfolgen können, ohne eine separate Datenbank zu pflegen. Die nachstehenden Schritte decken den vollständigen End‑zu‑End‑Workflow ab, von der Erstellung der Arbeitsmappe bis zum Persistieren der neuen Eigenschaften.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder höher installiert  
* Eine gültige Aspose.Cells‑für‑.NET‑Lizenz (oder eine kostenlose Testversion)  
* Visual Studio 2022 (oder eine beliebige C#‑IDE)  

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Cells` hinaus erforderlich.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie eine neue Konsolenanwendung und fügen Sie den Aspose.Cells‑Verweis hinzu:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Der Namespace `Aspose.Cells` enthält die Klassen `Workbook`, `Worksheet` und `CustomPropertyCollection`, die wir verwenden werden.

## Schritt 2: Eine vorhandene Arbeitsmappe laden (oder eine neue erstellen)

Sie können mit einer bestehenden `.xlsb`‑Datei beginnen oder eine frische Arbeitsmappe erzeugen. Das folgende Beispiel lädt eine Datei namens **Data.xlsb**, die sich in einem Ordner namens `YOUR_DIRECTORY` befindet.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Falls die Datei nicht existiert, ersetzen Sie den Code durch `new Workbook();`, um eine leere Arbeitsmappe zu erstellen.

## Schritt 3: Benutzerdefinierte Eigenschaften zum ersten Arbeitsblatt hinzufügen

Der zentrale Vorgang besteht darin, **benutzerdefinierte Eigenschaften** zu einem Arbeitsblatt hinzuzufügen. Aspose.Cells speichert benutzerdefinierte Eigenschaften in einer Sammlung, die sich wie ein Wörterbuch verhält.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Warum wir `CustomProperties.Add` anstelle von `CustomProperties["Name"] = value` verwenden, liegt darin, dass die `Add`‑Methode den Eintrag erstellt, falls er nicht existiert, und den korrekten Datentyp garantiert. Dieser Ansatz verhindert versehentliche Typinkompatibilitäten, die später beim Auslesen der Werte Laufzeitfehler verursachen könnten.

## Schritt 4: Die Arbeitsmappe mit den neuen Eigenschaften speichern

Nachdem Sie die Metadaten eingefügt haben, speichern Sie die Änderungen in einer neuen Datei, sodass das Original unverändert bleibt.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Zu diesem Zeitpunkt enthält die Excel‑Datei die von Ihnen definierten benutzerdefinierten Metadaten. Sie können die Eigenschaften mit den Schritten im nächsten Abschnitt überprüfen.

## Schritt 5: Benutzerdefinierte Eigenschaften aus einer Arbeitsmappe auslesen

Das Auslesen von **Excel‑benutzerdefinierten Eigenschaften** folgt demselben Sammlungs‑Muster. Dieses Snippet zeigt, wie Sie die Werte, die wir gerade gespeichert haben, abrufen.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

Der Indexer von `CustomPropertyCollection` gibt ein `CustomProperty`‑Objekt zurück; über dessen `Value`‑Eigenschaft erhalten Sie die gespeicherten Daten im ursprünglichen Typ. Das Prüfen auf `null` vor dem Casten verhindert `NullReferenceException`, falls eine Eigenschaft fehlt.

### Erwartete Konsolenausgabe

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Der Zeitstempel entspricht dem genauen Moment, an dem Sie `Add` in Schritt 3 aufgerufen haben.

## Profi‑Tipp: Vorhandene benutzerdefinierte Eigenschaft aktualisieren

Wenn Sie später **wie man benutzerdefinierte** Informationen hinzufügen muss (z. B. den Prüfer ändern), verwenden Sie den Setter von `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Dieses Muster stellt sicher, dass die Eigenschaft entweder aktualisiert oder erstellt wird – nützlich in iterativen Workflows wie der automatisierten Berichtserstellung.

## Schritt 6: Die Eigenschaften in Excel überprüfen (optional)

Sie können die benutzerdefinierten Eigenschaften auch direkt in Excel anzeigen:

1. Öffnen Sie die gespeicherte Datei `DataWithProps.xlsb` in Microsoft Excel.  
2. Navigieren Sie zu **Datei → Info → Eigenschaften → Erweiterte Eigenschaften**.  
3. Wählen Sie die Registerkarte **Benutzerdefiniert**.  

Sie sehen die Einträge `ProjectId`, `Reviewer` und `CreatedOn` mit den jeweiligen Werten.

## Vollständiges funktionierendes Beispiel

Im Folgenden finden Sie das komplette, eigenständige Programm, das alle vorherigen Snippets kombiniert. Kopieren Sie es in `Program.cs` und führen Sie es aus; die Konsole zeigt die abgerufenen Werte an.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Die Ausführung dieses Programms erzeugt die zuvor gezeigte Konsolenausgabe und erstellt `DataWithProps.xlsb`, das die eingebetteten Metadaten enthält.

## Häufige Fragen und Sonderfälle

| Frage | Antwort |
|---|---|
| **Kann ich nicht‑primitive Typen speichern?** | Aspose.Cells unterstützt `string`, `int`, `double`, `DateTime` und `bool`. Für komplexe Objekte serialisieren Sie diese zuerst nach JSON oder XML und speichern den String. |
| **Was, wenn die Arbeitsmappe passwortgeschützt ist?** | Öffnen Sie die Arbeitsmappe mit einem Passwort (`new Workbook(path, password)`) bevor Sie auf `CustomProperties` zugreifen. Die Eigenschaften bleiben nach der Entschlüsselung zugänglich. |
| **Überleben benutzerdefinierte Eigenschaften eine Formatkonvertierung?** | Beim Speichern in ein anderes Format (z. B. `.xlsx`) bewahrt Aspose.Cells benutzerdefinierte Eigenschaften, solange das Zielformat sie unterstützt. |
| **Wie lösche ich eine benutzerdefinierte Eigenschaft?** | Verwenden Sie `worksheet.CustomProperties.Remove("PropertyName");`. Damit wird der Eintrag aus der Sammlung entfernt. |

## Nächste Schritte

Jetzt, wo Sie **benutzerdefinierte Eigenschaften hinzufügen** können, könnten Sie verwandte Themen erkunden, etwa:

* **excel custom properties** für Dokumentenversionierung  
* **read custom properties** aus mehreren Arbeitsblättern einer einzigen Arbeitsmappe  
* Verwendung von **Aspose.Cells**, um Pivot‑Tabellen zu erstellen, die auf benutzerdefinierten Metadaten basieren  
* Export der Arbeitsmappe nach PDF unter Beibehaltung der benutzerdefinierten Eigenschaften  

Experimentieren Sie mit verschiedenen Datentypen, kombinieren Sie benutzerdefinierte Eigenschaften mit Zellkommentaren oder integrieren Sie die Metadaten in ein größeres Dokumenten‑Management‑System.

---

**Bereit, Ihre Excel‑Berichte zu automatisieren?** Fügen Sie den obigen Code zu Ihrem Projekt hinzu, passen Sie die Eigenschaftsnamen an Ihre geschäftlichen Anforderungen an, und Sie erhalten eine selbsterklärende Tabelle, die für nachgelagerte Prozesse bereitsteht.


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}