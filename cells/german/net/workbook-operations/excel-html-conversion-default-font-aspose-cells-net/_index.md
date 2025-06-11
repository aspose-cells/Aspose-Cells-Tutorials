---
"date": "2025-04-05"
"description": "Erfahren Sie, wie Sie beim Konvertieren von Excel-Dateien in HTML mit Aspose.Cells für .NET eine Standardschriftart festlegen und so eine konsistente Typografie und professionelle Präsentation gewährleisten."
"title": "Festlegen der Standardschriftart bei der Excel-zu-HTML-Konvertierung mit Aspose.Cells für .NET | Arbeitsmappen-Betriebshandbuch"
"url": "/de/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Beherrschen der Standardschriftarteinstellung in Excel zur HTML-Konvertierung mit Aspose.Cells für .NET

## Einführung

Das Konvertieren einer Excel-Arbeitsmappe ins HTML-Format unter Beibehaltung einer konsistenten Typografie kann eine Herausforderung sein. Dieses Tutorial führt Sie durch das Festlegen einer Standardschriftart mit Aspose.Cells für .NET und sorgt dafür, dass Ihre konvertierten Dokumente elegant und professionell aussehen. Mit dieser Funktion meistern Sie Herausforderungen im Zusammenhang mit unbekannten oder nicht verfügbaren Schriftarten im Konvertierungsprozess.

**Was Sie lernen werden:**
- So legen Sie beim Konvertieren von Excel-Dateien in HTML eine Standardschriftart fest.
- Schritt-für-Schritt-Anleitung zur Verwendung von Aspose.Cells für .NET.
- Techniken zum reibungslosen Umgang mit unbekannten Schriftarten während des Renderings.

Lassen Sie uns mit der Einrichtung Ihrer Umgebung beginnen und diese Funktion erkunden!

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:

- **.NET-Umgebung**: Eine kompatible Version von .NET ist installiert (z. B. .NET Core oder .NET Framework).
- **Aspose.Cells für die .NET-Bibliothek**: Installieren Sie Aspose.Cells über NuGet.
- **Grundlegende C#-Kenntnisse**Kenntnisse der C#-Programmierkonzepte sind hilfreich.

## Einrichten von Aspose.Cells für .NET

Richten Sie zunächst Aspose.Cells in Ihrer Entwicklungsumgebung ein, indem Sie die folgenden Schritte ausführen:

**Installation über CLI:**
```bash
dotnet add package Aspose.Cells
```

**Installation über den Paketmanager:**
```shell
PM> NuGet\Install-Package Aspose.Cells
```

### Lizenzerwerb
- **Kostenlose Testversion**: Beginnen Sie mit einer kostenlosen Testversion, um die Funktionen zu erkunden.
- **Temporäre Lizenz**: Erwerben Sie eine temporäre Lizenz zu Evaluierungszwecken.
- **Kaufen**: Erwägen Sie den Erwerb einer Lizenz für den Produktionseinsatz.

Nach der Installation initialisieren und richten Sie Ihr Projekt wie folgt ein:
```csharp
using Aspose.Cells;
```

## Implementierungshandbuch

### Festlegen der Standardschriftart beim Rendern

Diese Funktion stellt sicher, dass eine Excel-Arbeitsmappe beim Konvertieren in HTML mit einer bestimmten Standardschriftart gerendert wird. Dies ist besonders nützlich, wenn bestimmte Schriftarten auf dem Zielsystem möglicherweise nicht verfügbar sind.

#### Schritt 1: Arbeitsmappe erstellen und darauf zugreifen

Erstellen Sie eine neue Instanz von `Workbook` und greifen Sie auf das erste Arbeitsblatt zu:
```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

// Erstellen Sie ein Arbeitsmappenobjekt und greifen Sie auf das erste Arbeitsblatt zu.
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];
```

#### Schritt 2: Zellenstil ändern

Greifen Sie auf eine bestimmte Zelle zu, fügen Sie Text hinzu und stellen Sie zur Demonstration die Schriftart auf eine unbekannte ein:
```csharp
// Greifen Sie auf Zelle B4 zu und fügen Sie dort Text ein.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// Legen Sie für die Schriftart der Zelle B4 eine unbekannte Schriftart fest.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

#### Schritt 3: HTML-Speicheroptionen definieren

Legen Sie die Standardschriftart für Ihre HTML-Ausgabe fest. Hier demonstrieren wir dies anhand von drei verschiedenen Schriftarten:

**Kurier Neu:**
```csharp
// Speichern Sie die Arbeitsmappe im HTML-Format mit der Standardschriftart „Courier New“.
HtmlSaveOptions optsCourierNew = new HtmlSaveOptions();
optsCourierNew.DefaultFontName = "Courier New";
wb.Save(outputDir + "/out_courier_new_out.htm", optsCourierNew);
```

**Arial:**
```csharp
// Speichern Sie die Arbeitsmappe im HTML-Format mit der Standardschriftart Arial.
HtmlSaveOptions optsArial = new HtmlSaveOptions();
optsArial.DefaultFontName = "Arial";
wb.Save(outputDir + "/out_arial_out.htm", optsArial);
```

**Times New Roman:**
```csharp
// Speichern Sie die Arbeitsmappe im HTML-Format mit der Standardschriftart Times New Roman.
HtmlSaveOptions optsTimesNewRoman = new HtmlSaveOptions();
optsTimesNewRoman.DefaultFontName = "Times New Roman";
wb.Save(outputDir + "/times_new_roman_out.htm", optsTimesNewRoman);
```

### Erstellen von Arbeitsmappen und Formatieren von Zellen

In diesem Abschnitt wird das Erstellen einer Arbeitsmappe, der Zugriff auf Arbeitsblätter und Zellen sowie das Anwenden von Stilen behandelt:

#### Schritt 1: Arbeitsmappe initialisieren
Erstellen Sie ein neues `Workbook` Beispiel:
```csharp
// Erstellen Sie ein Arbeitsmappenobjekt.
Workbook wb = new Workbook();
```

#### Schritt 2: Auf Arbeitsblatt und Zelle zugreifen
Greifen Sie auf das erste Arbeitsblatt und die Zelle B4 zu, um Text hinzuzufügen und zu formatieren:
```csharp
// Greifen Sie auf das erste Arbeitsblatt in der Arbeitsmappe zu.
Worksheet ws = wb.Worksheets[0];

// Greifen Sie auf Zelle B4 zu und fügen Sie dort Text ein.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// Legen Sie für die Schriftart der Zelle B4 eine unbekannte Schriftart fest.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

## Praktische Anwendungen
- **Einheitliches Branding**: Stellen Sie sicher, dass Markenschriftarten in exportierten HTML-Dokumenten einheitlich angewendet werden.
- **Dokumentenportabilität**: Behandeln Sie Szenarien, in denen in Zielumgebungen bestimmte Schriftarten fehlen.
- **Automatisiertes Reporting**: Verwenden Sie diese Funktion zum Erstellen automatisierter Berichte mit konsistenter Typografie.

## Überlegungen zur Leistung
Für optimale Leistung:
- Verwalten Sie die Speichernutzung, indem Sie Objekte entsprechend entsorgen.
- Optimieren Sie die Rendering-Einstellungen basierend auf den Anforderungen Ihrer Anwendung.
- Aktualisieren Sie regelmäßig auf die neueste Aspose.Cells-Version, um verbesserte Funktionen und Fehlerbehebungen zu erhalten.

## Abschluss

Sie haben gelernt, wie Sie beim Konvertieren von Excel-Dateien in HTML mit Aspose.Cells für .NET eine Standardschriftart festlegen. Diese Funktion gewährleistet eine konsistente Typografie, selbst wenn bestimmte Schriftarten im Zielsystem nicht verfügbar sind. Um Ihre Kenntnisse weiter zu vertiefen, erkunden Sie zusätzliche Funktionen von Aspose.Cells und experimentieren Sie mit verschiedenen Rendering-Optionen.

**Nächste Schritte**: Versuchen Sie, diese Lösung in Ihren Projekten zu implementieren und passen Sie sie an Ihre spezifischen Anforderungen an.

## FAQ-Bereich
1. **Was ist Aspose.Cells für .NET?**
   - Eine Bibliothek, die die Bearbeitung und Konvertierung von Excel-Dateien innerhalb von .NET-Anwendungen ermöglicht.
2. **Wie installiere ich Aspose.Cells?**
   - Verwenden Sie den NuGet-Paket-Manager oder die .NET-CLI wie oben gezeigt.
3. **Kann ich diese Funktion mit älteren Versionen von .NET verwenden?**
   - Stellen Sie die Kompatibilität sicher, indem Sie die Systemanforderungen der Bibliothek überprüfen.
4. **Was ist, wenn meine Standardschriftart nicht auf allen Systemen unterstützt wird?**
   - Um plattformübergreifende Konsistenz zu gewährleisten, wird die angegebene Standardschriftart verwendet.
5. **Wo finde ich weitere Ressourcen und Support für Aspose.Cells?**
   - Siehe [Aspose-Dokumentation](https://reference.aspose.com/cells/net/) oder die [Support-Forum](https://forum.aspose.com/c/cells/9).

## Ressourcen
- **Dokumentation**: [Aspose.Cells .NET-Referenz](https://reference.aspose.com/cells/net/)
- **Herunterladen**: [Seite „Veröffentlichungen“](https://releases.aspose.com/cells/net/)
- **Kaufen**: [Aspose.Cells kaufen](https://purchase.aspose.com/buy)
- **Kostenlose Testversion**: [Testversion herunterladen](https://releases.aspose.com/cells/net/)
- **Temporäre Lizenz**: [Lizenzanfrage](https://purchase.aspose.com/temporary-license/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}