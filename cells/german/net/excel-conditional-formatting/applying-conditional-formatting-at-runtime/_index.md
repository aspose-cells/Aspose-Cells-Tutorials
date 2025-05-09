---
"description": "Erfahren Sie in dieser umfassenden Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET zur Laufzeit in Excel bedingte Formatierung anwenden."
"linktitle": "Anwenden der bedingten Formatierung zur Laufzeit in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Anwenden der bedingten Formatierung zur Laufzeit in Excel"
"url": "/de/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Anwenden der bedingten Formatierung zur Laufzeit in Excel

## Einführung

Sie sind leistungsstarke Werkzeuge für die Datenanalyse und -visualisierung. Eine der herausragenden Funktionen von Excel ist die bedingte Formatierung. Sie ermöglicht es Benutzern, Zellen basierend auf ihren Werten spezifische Formatierungsstile zuzuweisen. Dies erleichtert das Erkennen von Trends, das Hervorheben wichtiger Datenpunkte oder verbessert einfach die Lesbarkeit von Daten. Wenn Sie bedingte Formatierung programmgesteuert in Ihre Excel-Dateien implementieren möchten, sind Sie hier genau richtig! In dieser Anleitung erfahren Sie, wie Sie bedingte Formatierung zur Laufzeit mit Aspose.Cells für .NET anwenden.

## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg benötigen:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Sie können jede Version verwenden, die die .NET-Entwicklung unterstützt.
2. Aspose.Cells für .NET: Sie benötigen Aspose.Cells für .NET. Sie können es von der [Aspose-Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Codeausschnitte besser verstehen.
4. .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf eine kompatible Version des .NET Frameworks abzielt.

Nachdem wir nun die Voraussetzungen abgedeckt haben, können wir mit dem spaßigen Teil beginnen!

## Pakete importieren
Um mit Aspose.Cells zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. So geht's:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Über diese Namespaces erhalten Sie Zugriff auf die Klassen und Methoden, die zum Bearbeiten von Excel-Dateien und Anwenden der bedingten Formatierung erforderlich sind.

Lassen Sie uns nun den Vorgang der Anwendung der bedingten Formatierung in überschaubare Schritte unterteilen.

## Schritt 1: Richten Sie Ihr Projekt ein
Zunächst müssen Sie ein neues C#-Projekt in Visual Studio erstellen. So geht's:

1. Öffnen Sie Visual Studio und wählen Sie Datei > Neu > Projekt.
2. Wählen Sie „Konsolen-App (.NET Framework)“ und geben Sie Ihrem Projekt einen Namen.
3. Klicken Sie auf „Erstellen“.

## Schritt 2: Aspose.Cells-Referenz hinzufügen
Sobald Ihr Projekt eingerichtet ist, müssen Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzufügen:

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2. Wählen Sie „NuGet-Pakete verwalten“ aus.
3. Suchen Sie nach Aspose.Cells und installieren Sie es.

Dadurch können Sie alle Funktionen der Aspose.Cells-Bibliothek nutzen.

## Schritt 3: Erstellen Sie ein Arbeitsmappenobjekt
Als Nächstes erstellen wir eine neue Arbeitsmappe und ein neues Arbeitsblatt. Hier geschieht der ganze Zauber:

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

In diesem Schritt definieren wir das Verzeichnis, in dem unsere Excel-Datei gespeichert wird, erstellen eine neue Arbeitsmappe und greifen auf das erste Arbeitsblatt zu.

## Schritt 4: Bedingte Formatierung hinzufügen
Fügen wir nun eine bedingte Formatierung hinzu. Wir beginnen mit der Erstellung eines leeren Objekts für bedingte Formatierung:

```csharp
// Fügt eine leere bedingte Formatierung hinzu
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Hier fügen wir unserem Arbeitsblatt eine neue Sammlung bedingter Formatierung hinzu, die unsere Formatierungsregeln enthält.

## Schritt 5: Definieren Sie den Formatbereich
Als Nächstes müssen wir den Zellbereich angeben, auf den die bedingte Formatierung angewendet werden soll. Nehmen wir an, wir möchten die erste Zeile und die zweite Spalte formatieren:

```csharp
// Legt den Bereich für das bedingte Format fest.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

In diesem Code definieren wir zwei Bereiche für die bedingte Formatierung. Der erste Bereich ist für die Zelle bei (0,0) und der zweite für (1,1). Passen Sie diese Bereiche gerne an Ihre spezifischen Bedürfnisse an!

## Schritt 6: Bedingte Formatierungsbedingungen hinzufügen
Nun legen wir die Bedingungen für unsere Formatierung fest. Nehmen wir an, wir möchten Zellen basierend auf ihren Werten hervorheben:

```csharp
// Fügt Bedingung hinzu.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Fügt Bedingung hinzu.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

In diesem Schritt fügen wir zwei Bedingungen hinzu: eine für Werte zwischen `A2` Und `100`und ein weiteres für Werte zwischen `50` Und `100`. Dadurch können Sie Zellen basierend auf ihren Werten dynamisch hervorheben.

## Schritt 7: Formatierungsstile festlegen
Nachdem unsere Bedingungen festgelegt sind, können wir nun die Formatierungsstile festlegen. Ändern wir die Hintergrundfarbe für unsere Bedingungen:

```csharp
// Legt die Hintergrundfarbe fest.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Hier setzen wir die Hintergrundfarbe der ersten Bedingung auf Rot. Sie können dies weiter anpassen, indem Sie die Schriftfarbe, Rahmen und andere Stile nach Bedarf ändern!

## Schritt 8: Speichern Sie die Excel-Datei
Zum Schluss ist es Zeit, unsere Arbeit zu speichern! Wir speichern die Arbeitsmappe im angegebenen Verzeichnis:

```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "output.xls");
```

Diese Codezeile speichert die Excel-Datei mit der angewendeten bedingten Formatierung. Überprüfen Sie unbedingt das angegebene Verzeichnis für Ihre Ausgabedatei!

## Abschluss
Und fertig! Sie haben mit Aspose.Cells für .NET erfolgreich bedingte Formatierung zur Laufzeit in Excel angewendet. Diese leistungsstarke Bibliothek vereinfacht die programmgesteuerte Bearbeitung von Excel-Dateien, ermöglicht Ihnen die Automatisierung mühsamer Aufgaben und die Optimierung Ihrer Datenpräsentationen. Ob Sie an einem kleinen Projekt oder einer umfangreichen Anwendung arbeiten – Aspose.Cells hilft Ihnen, Ihren Workflow zu optimieren und Ihre Produktivität zu steigern.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, mit der Entwickler Excel-Dateien programmgesteuert erstellen, bearbeiten und konvertieren können.

### Kann ich Aspose.Cells mit anderen Programmiersprachen verwenden?
Ja, Aspose.Cells ist für mehrere Programmiersprachen verfügbar, darunter Java, Python und mehr.

### Gibt es eine kostenlose Testversion für Aspose.Cells?
Ja, Sie können eine kostenlose Testversion herunterladen von der [Aspose-Website](https://releases.aspose.com/).

### Wie erhalte ich Support für Aspose.Cells?
Sie erhalten Unterstützung durch den Besuch der [Aspose-Supportforum](https://forum.aspose.com/c/cells/9).

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
Ja, für die kommerzielle Nutzung ist eine Lizenz erforderlich. Sie können jedoch eine temporäre Lizenz anfordern. [Hier](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}