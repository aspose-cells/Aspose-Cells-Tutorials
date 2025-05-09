---
"date": "2025-04-05"
"description": "Ein Code-Tutorial für Aspose.Cells Net"
"title": "Erstellen Sie ein Kreisdiagramm in .NET mit Aspose.Cells – Eine vollständige Anleitung"
"url": "/de/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# So erstellen Sie ein Kreisdiagramm in .NET mit Aspose.Cells: Eine Schritt-für-Schritt-Anleitung

## Einführung

Die visuelle Darstellung von Daten ist eine wichtige Fähigkeit, insbesondere wenn es darum geht, komplexe Informationen einfach und effektiv zu vermitteln. Ob Sie an einem Geschäftsbericht arbeiten oder demografische Statistiken analysieren – Kreisdiagramme bieten eine einfache Möglichkeit, Teile eines Ganzen zu veranschaulichen. Diese Anleitung führt Sie durch die Erstellung eines Kreisdiagramms in .NET mit Aspose.Cells – einer leistungsstarken Bibliothek, die die programmgesteuerte Arbeit mit Excel-Dokumenten vereinfacht.

**Was Sie lernen werden:**
- So initialisieren und richten Sie eine Excel-Arbeitsmappe ein.
- Einfügen von Daten in Arbeitsblattzellen zur Visualisierung.
- Erstellen und Konfigurieren eines Kreisdiagramms mit Aspose.Cells für .NET.
- Anpassen der Segmentfarben im Kreisdiagramm für eine bessere Optik.
- Automatisches Anpassen von Spalten und Speichern Ihrer Arbeitsmappe.

Sehen wir uns an, wie Sie mit Aspose.Cells mühelos überzeugende Kreisdiagramme erstellen können. Bevor wir beginnen, stellen Sie sicher, dass Sie die Voraussetzungen erfüllen, um reibungslos mitarbeiten zu können.

## Voraussetzungen

Um mit diesem Lernprogramm zu beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:

- **Erforderliche Bibliotheken:** Sie benötigen die Bibliothek Aspose.Cells für .NET. Stellen Sie sicher, dass Ihr Projekt für die Verwendung eingerichtet ist.
- **Anforderungen für die Umgebungseinrichtung:** Auf Ihrem System ist eine geeignete Entwicklungsumgebung wie Visual Studio installiert.
- **Erforderliche Kenntnisse:** Grundlegende Kenntnisse der C#-Programmierung und Vertrautheit mit Excel-Dokumentstrukturen.

## Einrichten von Aspose.Cells für .NET

Bevor Sie mit dem Code beginnen, müssen Sie die Bibliothek Aspose.Cells in Ihrem Projekt installieren. So geht's:

### Installation über CLI
Öffnen Sie Ihr Terminal oder Ihre Eingabeaufforderung und führen Sie Folgendes aus:
```bash
dotnet add package Aspose.Cells
```

### Installation über den Paketmanager
Wenn Sie Visual Studio verwenden, öffnen Sie die NuGet-Paket-Manager-Konsole und führen Sie Folgendes aus:
```powershell
PM> Install-Package Aspose.Cells
```

#### Schritte zum Lizenzerwerb
Sie können Aspose.Cells zunächst kostenlos testen. Für eine längere Nutzung empfiehlt sich der Erwerb einer temporären Lizenz oder der direkte Kauf über die Website.

#### Grundlegende Initialisierung und Einrichtung

So initialisieren Sie die Bibliothek in Ihrem C#-Projekt:
```csharp
using Aspose.Cells;

// Erstellen Sie eine Instanz der Workbook-Klasse
Workbook workbook = new Workbook();
```

Mit dieser Grundkonfiguration können Sie programmgesteuert mit Excel-Dateien arbeiten.

## Implementierungshandbuch

### Funktion 1: Arbeitsmappe und Arbeitsblatt initialisieren

**Überblick:** Diese Funktion richtet eine neue Arbeitsmappe ein und greift auf das erste Arbeitsblatt zu, um die Bühne für die Dateneingabe und Diagrammerstellung vorzubereiten.

#### Schrittweise Initialisierung
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Erstellen eines neuen Arbeitsmappenobjekts
        Workbook workbook = new Workbook();
        
        // Greifen Sie auf das erste Arbeitsblatt in der Arbeitsmappe zu
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Hier, `Workbook` stellt eine Excel-Datei dar und der Zugriff `Worksheets[0]` gibt Ihnen das erste Blatt.

### Funktion 2: Daten für Kreisdiagramme auffüllen

**Überblick:** Das Ausfüllen der Daten ist entscheidend, da sie die Grundlage Ihres Diagramms bilden. In diesem Schritt tragen Sie Ländernamen und die entsprechenden Anteile an der Weltbevölkerung in die entsprechenden Zellen ein.

#### Schrittweise Datenerfassung
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Geben Sie die Länderdaten in Spalte C ein
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Geben Sie die Prozentdaten in Spalte D ein
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Dieser Schritt stellt sicher, dass Ihre Daten für die Visualisierung bereit sind.

### Funktion 3: Kreisdiagramm erstellen und konfigurieren

**Überblick:** Diese Funktion umfasst das Erstellen eines Kreisdiagramms, das Festlegen seiner Seriendaten und das Konfigurieren verschiedener Eigenschaften wie Titel und Legendenposition.

#### Schrittweise Erstellung eines Kreisdiagramms
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Fügen Sie dem Arbeitsblatt ein Kreisdiagramm hinzu
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Datenreihen für das Diagramm festlegen
        pie.NSeries.Add("D3:D8", true);

        // Kategoriedaten definieren und Titel konfigurieren
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Dieser Code erstellt ein optisch ansprechendes Diagramm, das mit Ihren Daten verknüpft ist.

### Funktion 4: Segmentfarben im Kreisdiagramm anpassen

**Überblick:** Durch die Personalisierung des Erscheinungsbilds jedes Segments verbessern Sie die Lesbarkeit und Ästhetik. In diesem Schritt werden den einzelnen Segmenten eindeutige Farben zugewiesen.

#### Schrittweise Farbanpassung
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Weisen Sie jedem Segment benutzerdefinierte Farben zu
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Dieser Schritt verleiht Ihrem Diagramm eine lebendige Note.

### Funktion 5: Spalten automatisch anpassen und Arbeitsmappe speichern

**Überblick:** Die letzten Schritte umfassen das Anpassen der Spaltenbreiten für eine bessere Datensichtbarkeit und das Speichern der Arbeitsmappe im Excel-Format.

#### Schrittweise Spaltenanpassung und Speicherung
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Spalten automatisch an Inhalt anpassen
        worksheet.AutoFitColumns();

        // Speichern Sie die Arbeitsmappe als Excel-Datei
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
Dadurch wird sichergestellt, dass Ihr endgültiges Dokument ausgefeilt und zur Präsentation bereit ist.

## Praktische Anwendungen

- **Geschäftsberichte:** Verwenden Sie Kreisdiagramme, um die Umsatzverteilung nach Regionen darzustellen.
- **Demografische Studien:** Visualisieren Sie Bevölkerungsdaten verschiedener Länder oder Regionen.
- **Lehrmittel:** Erstellen Sie ansprechende visuelle Hilfsmittel für Studenten in Statistikkursen.
- **Gesundheitsanalyse:** Zeigen Sie die Verteilung von Patientendaten innerhalb von Gesundheitseinrichtungen an.

## Überlegungen zur Leistung

Um eine optimale Leistung bei der Verwendung von Aspose.Cells sicherzustellen, beachten Sie Folgendes:

- **Effiziente Datenverarbeitung:** Verwalten Sie große Datensätze, indem Sie sie bei Bedarf in Blöcken verarbeiten.
- **Speicherverwaltung:** Entsorgen Sie Objekte ordnungsgemäß, um Ressourcen freizugeben und Speicherlecks zu vermeiden.
- **Optimierte Diagrammkonfigurationen:** Minimieren Sie komplexe Berechnungen oder Renderings während der Diagrammerstellung für eine schnellere Leistung.

## Abschluss

Sie haben nun gelernt, wie Sie mit Aspose.Cells ein Kreisdiagramm in .NET erstellen. Diese leistungsstarke Bibliothek vereinfacht die Bearbeitung von Excel-Dokumenten und ermöglicht es Ihnen, sich auf die Datenanalyse zu konzentrieren, anstatt sich mit den Feinheiten der Dateiverwaltung herumzuschlagen. Experimentieren Sie mit verschiedenen Diagrammtypen und Anpassungsmöglichkeiten von Aspose.Cells, um Ihre Anwendungen weiter zu verbessern.

**Nächste Schritte:**
- Entdecken Sie andere Diagrammtypen wie Balken- oder Liniendiagramme.
- Integrieren Sie Aspose.Cells-Funktionen in größere .NET-Projekte für automatisiertes Reporting.

Sind Sie bereit, Ihre Datenvisualisierungsfähigkeiten auf die nächste Stufe zu heben? Tauchen Sie tiefer ein, indem Sie weitere Funktionen von Aspose.Cells erkunden und diese noch heute in Ihre Projekte implementieren!

## FAQ-Bereich

1. **Wofür wird Aspose.Cells verwendet?**
   - Es handelt sich um eine Bibliothek zur programmgesteuerten Verwaltung von Excel-Dateien, mit der Sie Tabellenkalkulationen erstellen, ändern und analysieren können.

2. **Kann ich Aspose.Cells ohne Lizenz verwenden?**
   - Ja, allerdings mit Einschränkungen. Eine kostenlose Testversion oder eine temporäre Lizenz ermöglicht den vollständigen Zugriff auf alle Funktionen.

3. **Wie kann ich das Erscheinungsbild meines Kreisdiagramms weiter anpassen?**
   - Verwenden Sie zusätzliche Eigenschaften wie `pie.NSeries[0].Area.Formatting` für mehr Kontrolle über die Ästhetik.

4. **Welche häufigen Probleme treten beim Erstellen von Diagrammen in Aspose.Cells auf?**
   - Stellen Sie sicher, dass die Datenbereiche richtig angegeben sind und dass Sie vor dem Rendern alle erforderlichen Diagrammeigenschaften konfiguriert haben.

5. **Wie kann ich Aspose.Cells in andere .NET-Bibliotheken integrieren?**
   - Verwenden Sie Aspose.Cells als Teil einer größeren .NET-Lösung und nutzen Sie seine Funktionen zusammen mit anderen Bibliotheken für umfassende Anwendungen.

## Ressourcen

- **Dokumentation:** [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/)
- **Herunterladen:** [Aspose.Cells-Versionen](https://releases.aspose.com/cells/net/)
- **Kaufen:** [Aspose.Cells kaufen](https://purchase.aspose.com/buy)
- **Kostenlose Testversion:** [Kostenlose Testversion von Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Temporäre Lizenz:** [Holen Sie sich eine temporäre Lizenz](https://purchase.aspose.com/temporary-license/)
- **Unterstützung:** [Aspose Forum](https://forum.aspose.com/c/cells/9)

Mit dieser Anleitung können Sie nun mit Aspose.Cells optisch ansprechende Kreisdiagramme in .NET-Anwendungen erstellen. Viel Spaß beim Programmieren!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}