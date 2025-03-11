---
title: Automatisches Formatieren einer Pivot-Tabelle programmgesteuert in .NET festlegen
linktitle: Automatisches Formatieren einer Pivot-Tabelle programmgesteuert in .NET festlegen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie die automatische Formatierung für Excel-Pivot-Tabellen programmgesteuert mit Aspose.Cells für .NET festlegen.
weight: 18
url: /de/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatisches Formatieren einer Pivot-Tabelle programmgesteuert in .NET festlegen

## Einführung
Wenn es um die Analyse von Daten geht, können Pivot-Tabellen in Excel eine bahnbrechende Neuerung sein. Sie ermöglichen Ihnen die dynamische Zusammenfassung und Analyse von Daten und helfen Ihnen, Erkenntnisse zu gewinnen, die manuell kaum zu gewinnen wären. Aber was, wenn Sie den Formatierungsprozess Ihrer Pivot-Tabellen in .NET automatisieren möchten? Hier zeige ich Ihnen, wie Sie die automatische Formatierung einer Pivot-Tabelle mithilfe der leistungsstarken Aspose.Cells-Bibliothek für .NET programmgesteuert festlegen.
In diesem Handbuch erkunden wir die Grundlagen, gehen die Voraussetzungen durch, importieren die erforderlichen Pakete und tauchen dann in ein Schritt-für-Schritt-Tutorial ein, damit Sie Pivot-Tabellen wie ein Profi formatieren. Klingt gut? Dann legen wir gleich los!
## Voraussetzungen
Bevor wir beginnen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg benötigen:
1. Eine .NET-Entwicklungsumgebung: Stellen Sie sicher, dass Sie über eine funktionierende Instanz von Visual Studio (oder einer anderen IDE, die .NET unterstützt) verfügen.
2.  Aspose.Cells-Bibliothek: Um problemlos mit Excel-Dateien arbeiten zu können, müssen Sie die Aspose.Cells-Bibliothek installieren. Wenn Sie das noch nicht getan haben, können Sie sie von der[Download-Seite](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Schritte besser.
4.  Excel-Datei (Vorlage): Sie benötigen zunächst eine Excel-Vorlagendatei, die in unserem Beispiel verarbeitet wird. Der Einfachheit halber können Sie eine Beispieldatei mit dem Namen`Book1.xls`.
## Pakete importieren
Um Aspose.Cells in Ihrem Projekt verwenden zu können, müssen Sie die erforderlichen Pakete importieren. So können Sie das in Ihrem .NET-Projekt einrichten:
### Neues Projekt erstellen
Beginnen Sie mit der Erstellung eines neuen .NET-Projekts in Ihrer bevorzugten IDE. 
### Verweise hinzufügen
Stellen Sie sicher, dass Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzufügen. Wenn Sie die Bibliothek heruntergeladen haben, fügen Sie die DLLs aus der Extraktion hinzu. Wenn Sie NuGet verwenden, können Sie einfach Folgendes ausführen:
```bash
Install-Package Aspose.Cells
```
### Namespaces importieren
Jetzt müssen Sie in Ihrer Codedatei den Aspose.Cells-Namespace importieren. Sie können dies tun, indem Sie oben in Ihrer C#-Datei die folgende Zeile hinzufügen:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Wenn Sie diese Schritte abgeschlossen haben, können Sie mit dem Schreiben des Codes beginnen!
Lassen Sie uns nun den von Ihnen bereitgestellten Code in detaillierte Schritte mit Erklärungen zur Funktion der einzelnen Teile aufschlüsseln. 
## Schritt 1: Definieren Sie Ihr Dokumentverzeichnis
Zunächst müssen Sie den Pfad zu Ihrem Dokumentenverzeichnis festlegen, in dem sich Ihre Excel-Dateien befinden. In unserem Beispiel definieren wir ihn folgendermaßen:
```csharp
string dataDir = "Your Document Directory";  // Bei Bedarf ändern
```
 Diese Zeile erstellt eine String-Variable`dataDir`das den Dateipfad zu Ihren Dokumenten enthält. Ersetzen Sie unbedingt`"Your Document Directory"` durch den tatsächlichen Pfad auf Ihrem System.
## Schritt 2: Laden Sie die Vorlagendatei
Als Nächstes möchten Sie eine vorhandene Arbeitsmappe laden, die Ihre Pivot-Tabelle enthält:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
 Diese Zeile initialisiert eine neue`Workbook` Objekt durch Laden der angegebenen Excel-Datei. Die Datei sollte mindestens eine Pivot-Tabelle enthalten, damit die nachfolgenden Schritte wirksam sind.
## Schritt 3: Zugriff auf das gewünschte Arbeitsblatt
Identifizieren Sie, an welchem Arbeitsblatt Sie arbeiten müssen, um auf die Pivot-Tabelle zuzugreifen. In diesem Fall holen wir uns einfach das erste:
```csharp
int pivotIndex = 0;  // Index der Pivot-Tabelle
Worksheet worksheet = workbook.Worksheets[0];
```
 Hier,`worksheet` ruft das erste Arbeitsblatt aus der Arbeitsmappe ab. Der Index der Pivot-Tabelle wird auf`0`, was bedeutet, dass wir auf die erste Pivot-Tabelle in diesem Arbeitsblatt greifen.
## Schritt 4: Suchen Sie die Pivot-Tabelle
Wenn das Arbeitsblatt fertig ist, können Sie auf Ihre Pivot-Tabelle zugreifen:
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
 Dies initialisiert einen neuen`PivotTable` -Objekt, indem die Pivot-Tabelle am angegebenen Index aus dem Arbeitsblatt abgerufen wird.
## Schritt 5: Automatische Formatierungseigenschaft festlegen
Kommen wir nun zum interessanten Teil: Festlegen der automatischen Formatierungsoptionen für Ihre Pivot-Tabelle.
```csharp
pivotTable.IsAutoFormat = true; // Automatische Formatierung aktivieren
```
 Diese Zeile aktiviert die Autoformatierungsfunktion für die Pivot-Tabelle. Wenn sie auf`true`, formatiert sich die Pivot-Tabelle automatisch anhand vordefinierter Stile.
## Schritt 6: Einen bestimmten Auto-Format-Typ auswählen
Wir möchten auch angeben, welchen automatischen Formatierungsstil die Pivot-Tabelle verwenden soll. Aspose.Cells bietet verschiedene Formate, aus denen wir wählen können. So legen Sie es fest:
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
 Mit dieser Zeile weisen wir der Pivot-Tabelle einen bestimmten Autoformattyp zu.`Report5` ist nur ein Beispiel für einen Stil; Sie können je nach Bedarf aus einer Vielzahl von Optionen wählen. 
## Schritt 7: Speichern Sie die Arbeitsmappe
Vergessen Sie nicht, Ihre Arbeitsmappe zu speichern, nachdem Sie alle Änderungen vorgenommen haben:
```csharp
workbook.Save(dataDir + "output.xls");
```
 Diese Codezeile speichert die geänderte Arbeitsmappe in einer neuen Datei namens`output.xls` im angegebenen Verzeichnis. Überprüfen Sie unbedingt diese Datei, um Ihre schön formatierte Pivot-Tabelle anzuzeigen!
## Abschluss
Herzlichen Glückwunsch! Sie haben gerade eine Excel-Pivot-Tabelle so programmiert, dass sie mit Aspose.Cells in .NET automatisch formatiert wird. Dieser Vorgang spart Ihnen nicht nur Zeit bei der Erstellung von Berichten, sondern sorgt auch dafür, dass Ihre Daten bei jedem Durchlauf konsistent aussehen. Mit nur wenigen Codezeilen können Sie Ihre Excel-Dateien erheblich verbessern – wie ein digitaler Zauberer.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek zur Verarbeitung von Excel-Dateien, ohne dass Microsoft Excel installiert sein muss.
### Kann ich mehrere Pivot-Tabellen in einer Arbeitsmappe formatieren?
Ja, Sie können mehrere PivotTable-Objekte in Ihrer Arbeitsmappe durchlaufen, um sie einzeln zu formatieren.
### Gibt es eine kostenlose Testversion für Aspose.Cells?
 Absolut! Sie können mit einer kostenlosen Testversion beginnen, die verfügbar ist[Hier](https://releases.aspose.com/).
### Was ist, wenn meine Pivot-Tabelle nicht richtig formatiert ist?
Stellen Sie sicher, dass die Pivot-Tabelle richtig referenziert wird und der Auto-Format-Typ vorhanden ist. Andernfalls wird möglicherweise auf die Standardeinstellungen zurückgegriffen.
### Kann ich diesen Prozess mit geplanten Aufgaben automatisieren?
Ja! Indem Sie diesen Code in eine geplante Aufgabe integrieren, können Sie die Berichterstellung und -formatierung regelmäßig automatisieren.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
