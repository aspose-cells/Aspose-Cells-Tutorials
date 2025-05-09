---
"date": "2025-04-05"
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET dynamische Kreisdiagramme mit Führungslinien erstellen. Folgen Sie dieser Anleitung, um Ihre Fähigkeiten zur Datenvisualisierung zu verbessern."
"title": "Erstellen von Kreisdiagrammen mit Führungslinien in Aspose.Cells .NET – Ein umfassender Leitfaden"
"url": "/de/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Erstellen von Kreisdiagrammen mit Führungslinien mit Aspose.Cells .NET

## Einführung
Verbessern Sie Ihre Datenvisualisierung, indem Sie mit Aspose.Cells für .NET informativere Kreisdiagramme erstellen. Diese Schritt-für-Schritt-Anleitung zeigt Ihnen, wie Sie Kreisdiagrammsegmenten Führungslinien hinzufügen, um die entsprechenden Datenkategorien auf einen Blick zu erkennen. Mit diesem Tutorial werden Ihre Visualisierungen sowohl optisch ansprechend als auch hochfunktional.

**Was Sie lernen werden:**
- Einrichten von Aspose.Cells für .NET in Ihrer Umgebung
- Erstellen benutzerdefinierter Kreisdiagramme mit Führungslinien mit C#
- Speichern des Diagramms als Bild oder in einer Excel-Arbeitsmappe

Stellen Sie sicher, dass Sie alles bereit haben, um effektiv mitmachen zu können.

## Voraussetzungen
Stellen Sie vor dem Start sicher, dass Sie die folgenden Voraussetzungen erfüllen:

- **Bibliotheken und Versionen**: Installieren Sie Aspose.Cells für .NET. Stellen Sie sicher, dass Ihr Projekt mit der neuesten Version eingerichtet ist.
- **Umgebungs-Setup**: Diese Anleitung setzt eine kompatible .NET-Umgebung für Aspose.Cells voraus.
- **Voraussetzungen**Grundkenntnisse in C#-Programmierung und Excel-Operationen sind von Vorteil.

## Einrichten von Aspose.Cells für .NET
Installieren Sie zunächst Aspose.Cells in Ihrem Projekt über:

**.NET-CLI**
```bash
dotnet add package Aspose.Cells
```

**Paketmanager**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Erwerben Sie eine Lizenz für die volle Funktionalität, indem Sie aus den folgenden Optionen auswählen:
- **Kostenlose Testversion**: Starten Sie Ihre kostenlose Testversion auf der [Aspose-Downloadseite](https://releases.aspose.com/cells/net/).
- **Temporäre Lizenz**: Erhalten Sie eine temporäre Lizenz [Hier](https://purchase.aspose.com/temporary-license/).
- **Kaufen**: Für alle Funktionen erwerben Sie eine Lizenz [Hier](https://purchase.aspose.com/buy).

Initialisieren Sie Aspose.Cells in Ihrem Projekt, indem Sie eine Instanz des `Workbook` Klasse.

## Implementierungshandbuch

### Erstellen der Arbeitsmappe und des Arbeitsblatts
1. **Initialisieren der Arbeitsmappe**
   Erstellen Sie eine neue Arbeitsmappe im XLSX-Format:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Zugriff auf das erste Arbeitsblatt**
   Verwenden Sie das erste Arbeitsblatt zur Dateneingabe:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Hinzufügen von Daten für Kreisdiagramme**
   Füllen Sie Ihr Arbeitsblatt mit Kategorien und Werten:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Fügen Sie die restlichen Kategorienamen hinzu ...
   worksheet.Cells["B1"].PutValue(10.4);
   // Entsprechende Werte hinzufügen...
   ```

### Hinzufügen eines Kreisdiagramms zum Arbeitsblatt
1. **Erstellen Sie das Kreisdiagramm**
   Erstellen Sie ein Kreisdiagramm und fügen Sie es der Diagrammsammlung Ihres Arbeitsblatts hinzu:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Konfigurieren von Serien- und Kategoriendaten**
   Verknüpfen Sie die Daten der Serien und Kategorien:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Datenbeschriftungen anpassen**
   Schalten Sie die Legendenanzeige aus und legen Sie Datenbeschriftungen fest, um Kategorienamen und Prozentsätze anzuzeigen:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementieren von Führungslinien
1. **Führungslinien aktivieren**
   Aktivieren Sie Führungslinien für klarere visuelle Verbindungen:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Position der Datenbeschriftungen anpassen**
   Sorgen Sie für Sichtbarkeit, indem Sie die Positionen der Beschriftungen anpassen:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Speichern des Diagramms und der Arbeitsmappe
1. **Als Bild speichern**
   Rendern Sie das Diagramm in eine Bilddatei:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Arbeitsmappe speichern**
   Speichern Sie die Arbeitsmappe, um das Diagramm in Excel anzuzeigen:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Praktische Anwendungen
- **Finanzberichte**: Budgetzuweisungen klar darstellen.
- **Marketinganalyse**: Visualisieren Sie Marktanteilsdaten effektiv in Präsentationen oder Berichten.
- **Verkaufsanalyse**Zeigen Sie mühelos die Umsatzverteilung zwischen verschiedenen Regionen/Produkten an.

Zu den Integrationsmöglichkeiten gehört das Exportieren dieser Visualisierungen in Webanwendungen oder das Einbetten in automatisierte Berichtstools.

## Überlegungen zur Leistung
Beachten Sie bei der Verwendung von Aspose.Cells Folgendes, um eine optimale Leistung zu erzielen:
- Minimieren Sie große Datensätze, die auf einmal in den Speicher geladen werden.
- Verwenden Sie effiziente Schleifen und vermeiden Sie unnötige Berechnungen innerhalb von Schleifen.
- Bereinigen Sie regelmäßig Ressourcen wie Arbeitsmappenobjekte, um Speicherlecks zu vermeiden.

## Abschluss
Sie haben gelernt, wie Sie mit Aspose.Cells für .NET Kreisdiagramme mit Führungslinien erstellen. Diese Funktion verbessert die Übersichtlichkeit Ihrer Datenvisualisierungen und macht sie zugänglicher und wirkungsvoller. 

**Nächste Schritte:**
Erkunden Sie weitere Anpassungsmöglichkeiten für das Erscheinungsbild von Diagrammen oder experimentieren Sie mit anderen in Aspose.Cells verfügbaren Diagrammtypen.

## FAQ-Bereich
1. **Was ist eine Führungslinie in einem Kreisdiagramm?**
   Führungslinien verbinden Datenbeschriftungen mit ihren jeweiligen Segmenten und verbessern so die Lesbarkeit.

2. **Kann ich Aspose.Cells kostenlos nutzen?**
   Ja, Sie können mit einer kostenlosen Testversion beginnen, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich.

3. **Ist es möglich, Diagramme als Bilder zu exportieren?**
   Absolut! Verwenden `ImageOrPrintOptions` um Ihr Diagramm in Bildformaten wie PNG oder JPEG zu speichern.

4. **Wie passe ich die Positionen der Datenbeschriftungen manuell an?**
   Ändern Sie die X- und Y-Koordinaten der Datenbeschriftungen innerhalb der Serienpunktschleife.

5. **Kann Aspose.Cells in andere Systeme integriert werden?**
   Ja, es kann in Verbindung mit Datenbanken, Webdiensten und mehr für automatisierte Berichtslösungen verwendet werden.

## Ressourcen
- [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/)
- [Laden Sie Aspose.Cells herunter](https://releases.aspose.com/cells/net/)
- [Lizenz erwerben](https://purchase.aspose.com/buy)
- [Kostenlose Testversion](https://releases.aspose.com/cells/net/)
- [Temporäre Lizenz](https://purchase.aspose.com/temporary-license/)
- [Support-Forum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}