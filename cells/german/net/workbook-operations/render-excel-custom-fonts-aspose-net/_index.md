---
"date": "2025-04-05"
"description": "Erfahren Sie, wie Sie Excel-Dateien mit Aspose.Cells für .NET in die Formate PNG, TIFF und PDF konvertieren und dabei benutzerdefinierte Schriftarten verwenden. Stellen Sie eine konsistente Typografie bei allen Dokumentkonvertierungen sicher."
"title": "Rendern Sie Excel mit Aspose.Cells in PNG, TIFF, PDF mit benutzerdefinierten Schriftarten in .NET"
"url": "/de/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Rendern Sie Excel-Dateien mit benutzerdefinierten Schriftarten in PNG, TIFF und PDF mit Aspose.Cells für .NET

## Einführung

Die Wahrung der Schriftintegrität bei der Konvertierung von Excel-Dateien in Bilder oder PDFs ist entscheidend für die Markenkonsistenz. Aspose.Cells für .NET bietet eine robuste Lösung, indem Sie benutzerdefinierte Standardschriftarten für Ihre Dokumentkonvertierungen festlegen können.

In diesem Tutorial führen wir Sie durch das Rendern von Excel-Dateien in die Formate PNG, TIFF und PDF mit Aspose.Cells für .NET und angegebenen benutzerdefinierten Standardschriftarten. Dies ist ideal, wenn Sie:
- Achten Sie auf eine einheitliche Typografie in den gerenderten Dokumenten.
- Während der Konvertierung müssen die Schrifteinstellungen angepasst werden.
- Möchten Sie die Konfigurationsoptionen in Aspose.Cells für .NET erkunden.

Lassen Sie uns Ihre Umgebung einrichten und diese Funktionen nahtlos implementieren.

### Voraussetzungen

Stellen Sie vor dem Start sicher, dass Sie über Folgendes verfügen:
- **.NET-Umgebung**: Auf Ihrem Computer einrichten (vorzugsweise .NET Core oder .NET Framework).
- **Aspose.Cells für die .NET-Bibliothek**: In Ihrem Projekt installiert.
- **Excel-Datei**: Eine Excel-Arbeitsmappe mit zu konvertierenden Daten.

### Einrichten von Aspose.Cells für .NET

Fügen Sie zunächst die Bibliothek Aspose.Cells zu Ihrem Projekt hinzu:

**Verwenden der .NET-CLI:**
```bash
dotnet add package Aspose.Cells
```

**Verwenden des Paketmanagers:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Erwerben Sie eine Lizenz für den vollständigen Funktionszugriff:
- **Kostenlose Testversion**: Besuchen [Kostenlose Aspose-Testversion](https://releases.aspose.com/cells/net/) für den ersten Zugriff.
- **Temporäre Lizenz**: Erhalten Sie es von [Aspose Temporäre Lizenz](https://purchase.aspose.com/temporary-license/).
- **Kaufen**: Für eine dauerhafte Lizenz gehen Sie zu [Aspose Kauf](https://purchase.aspose.com/buy).

Initialisieren Sie Aspose.Cells in Ihrer Anwendung, nachdem Sie Ihre Lizenz erworben haben:
```csharp
// Legen Sie die Lizenz für Aspose.Cells fest.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Implementierungshandbuch

### Rendern in PNG mit benutzerdefinierter Standardschriftart

Das Rendern eines Excel-Arbeitsblatts im PNG-Format mit benutzerdefinierter Standardschriftart gewährleistet visuelle Konsistenz. So geht's:

#### Schritt 1: Bildoptionen konfigurieren

Konfigurieren Sie Rendering-Optionen für Ihre Bildausgabe.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Verzeichnisse angeben.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Öffnen Sie eine Excel-Datei.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Richten Sie Optionen zur Bildwiedergabe ein.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Verwenden Sie für fehlende Schriftarten in der Arbeitsmappe eine benutzerdefinierte Schriftart.
imgOpt.DefaultFont = "Times New Roman";
```

#### Schritt 2: Rendern und Speichern

Rendern Sie Ihr Arbeitsblatt mit diesen Einstellungen in eine Bilddatei.
```csharp
// Rendern Sie das erste Arbeitsblatt in ein PNG-Bild.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Rendern in TIFF mit benutzerdefinierter Standardschriftart

Das TIFF-Format eignet sich ideal für hochwertige Bilder. So rendern Sie eine ganze Arbeitsmappe als TIFF-Datei:

#### Schritt 3: Bildoptionen für TIFF einrichten

Konfigurieren Sie Rendering-Optionen speziell für die TIFF-Ausgabe.
```csharp
// Verwenden Sie zuvor definierte Verzeichnisse erneut und öffnen Sie die Excel-Datei.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Konfigurieren Sie Bildwiedergabeoptionen für TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Schritt 4: Gesamte Arbeitsmappe in TIFF rendern

Konvertieren Sie die gesamte Arbeitsmappe in eine einzelne TIFF-Datei.
```csharp
// Rendern Sie die Arbeitsmappe als TIFF-Bild.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Rendern in PDF mit benutzerdefinierter Standardschriftart

Das Speichern einer Excel-Arbeitsmappe als PDF unter Wahrung der Schriftartenkonsistenz ist für eine professionelle Dokumentation von entscheidender Bedeutung.

#### Schritt 5: PDF-Speicheroptionen konfigurieren

Richten Sie die erforderlichen Optionen zum Speichern Ihrer Datei als PDF ein.
```csharp
using Aspose.Cells;

// Öffnen Sie die Arbeitsmappe erneut.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Richten Sie PDF-Speicheroptionen ein.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Verwenden Sie für fehlende Schriftarten in der Arbeitsmappe eine benutzerdefinierte Schriftart.
```

#### Schritt 6: Als PDF speichern

Exportieren Sie Ihre Arbeitsmappe in ein PDF-Dokument.
```csharp
// Speichern Sie die Arbeitsmappe als PDF-Datei.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Praktische Anwendungen

- **Geschäftsberichte**: Sorgen Sie durch die Verwendung benutzerdefinierter Schriftarten für ein einheitliches Branding in allen exportierten Berichten.
- **Dokumentenarchivierung**: Konvertieren Sie ältere Excel-Dateien in PDFs zum einfachen Teilen und Archivieren mit einheitlicher Typografie.
- **Grafikdesign**: Erstellen Sie hochauflösende TIFF-Bilder von Excel-Daten für Präsentationen oder Designprojekte.

Durch die Integration mit anderen Systemen, wie etwa CRM-Plattformen oder Dokumentenmanagementlösungen, können diese Anwendungsfälle noch weiter verbessert werden, indem Exporte auf der Grundlage bestimmter Auslöser oder Ereignisse automatisiert werden.

## Überlegungen zur Leistung

Die Optimierung Ihres Rendering-Prozesses ist entscheidend:
- **Speicherverwaltung**: Entsorgen `Workbook`, `SheetRender`, Und `WorkbookRender` Objekte umgehend, um Ressourcen freizugeben.
- **Stapelverarbeitung**Wenn Sie mit mehreren Dateien arbeiten, implementieren Sie zur effizienten Handhabung eine Stapelverarbeitung.
- **Asynchrone Vorgänge**: Nutzen Sie nach Möglichkeit asynchrone Methoden, um die Reaktionsfähigkeit von Anwendungen zu verbessern.

## Abschluss

Sie beherrschen nun das Rendern von Excel-Arbeitsmappen in den Formaten PNG, TIFF und PDF und legen mit Aspose.Cells für .NET benutzerdefinierte Standardschriftarten fest. Diese Funktion stellt sicher, dass Ihre Dokumente plattformübergreifend und für verschiedene Anwendungen visuell integr bleiben.

Entdecken Sie die zusätzlichen Funktionen von Aspose.Cells, um die Dokumentenverarbeitung weiter zu verbessern. Weitere Informationen oder Unterstützung finden Sie im [Aspose Forum](https://forum.aspose.com/c/cells/9).

## FAQ-Bereich

**1. Was ist Aspose.Cells für .NET?**
   – Aspose.Cells für .NET ist eine Bibliothek, die robuste Funktionen zum programmgesteuerten Verwalten und Konvertieren von Excel-Dateien bietet.

**2. Kann ich Aspose.Cells in Webanwendungen verwenden?**
   — Ja, Aspose.Cells können in ASP.NET oder jede andere .NET-basierte Webanwendung integriert werden.

**3. Wie gehe ich mit fehlenden Schriftarten beim Rendern um?**
   — Durch die Einstellung der `CheckWorkbookDefaultFont` auf false und die Angabe eines `DefaultFont`stellen Sie sicher, dass für den gesamten Text die von Ihnen gewählte Schriftart verwendet wird, auch wenn das Original nicht verfügbar ist.

**4. Werden andere Formate als PNG, TIFF und PDF unterstützt?**
   – Ja, Aspose.Cells unterstützt verschiedene Bildformate wie JPEG, BMP usw. und bietet umfangreiche Funktionen zur Dokumentkonvertierung.

**5. Was sind einige Best Practices für die Verwendung von Aspose.Cells in groß angelegten Anwendungen?**
   – Nutzen Sie effiziente Speicherverwaltungstechniken, Stapelverarbeitung zur Handhabung mehrerer Dateien und ziehen Sie asynchrone Vorgänge in Betracht, um die Anwendungsleistung zu verbessern.

## Ressourcen
- **Dokumentation**: [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/)
- **Herunterladen**: [Aspose.Cells-Versionen](https://releases.aspose.com/cells/net/)
- **Kaufen**: [Aspose.Cells kaufen](https://purchase.aspose.com/buy)
- **Kostenlose Testversion**: [Testen Sie Aspose.Cells kostenlos](https://releases.aspose.com/cells/net/)
- **Temporäre Lizenz**: [Holen Sie sich eine temporäre Lizenz](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}