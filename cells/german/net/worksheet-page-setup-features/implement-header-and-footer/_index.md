---
title: Kopf- und Fußzeile im Arbeitsblatt implementieren
linktitle: Kopf- und Fußzeile im Arbeitsblatt implementieren
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie anhand einer Schritt-für-Schritt-Anleitung, praktischen Beispielen und nützlichen Tipps, wie Sie mit Aspose.Cells für .NET Kopf- und Fußzeilen in Excel-Arbeitsblättern einrichten.
weight: 22
url: /de/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopf- und Fußzeile im Arbeitsblatt implementieren

## Einführung

Beim Arbeiten mit Excel-Tabellen spielen Kopf- und Fußzeilen eine Schlüsselrolle, wenn es darum geht, Ihrem Publikum wichtige Kontextinformationen wie Dateinamen, Daten oder Seitenzahlen zu übermitteln. Ob Sie Berichte automatisieren oder dynamische Dateien generieren, mit Aspose.Cells für .NET können Sie Kopf- und Fußzeilen in Arbeitsblättern ganz einfach programmgesteuert anpassen. In diesem Handbuch erfahren Sie Schritt für Schritt, wie Sie mit Aspose.Cells für .NET Kopf- und Fußzeilen hinzufügen und Ihren Excel-Dateien so noch mehr Glanz und Professionalität verleihen.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes eingerichtet haben:

1.  Aspose.Cells für .NET: Sie müssen Aspose.Cells für .NET installiert haben.[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
2. IDE-Setup: Visual Studio (oder Ihre bevorzugte IDE) mit installiertem .NET-Framework.
3.  Lizenz: Sie können mit der kostenlosen Testversion beginnen, aber mit dem Erwerb einer Voll- oder Zeitlizenz können Sie das volle Potenzial von Aspose.Cells ausschöpfen.[Erhalten Sie eine temporäre Lizenz](https://purchase.aspose.com/temporary-license/).

Die Dokumentation für Aspose.Cells ist eine praktische Ressource für den gesamten Prozess. Sie finden sie[Hier](https://reference.aspose.com/cells/net/).

## Pakete importieren

Importieren Sie in Ihr Projekt die erforderlichen Namespaces:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Durch das Importieren dieses Pakets haben Sie Zugriff auf die Klassen und Methoden, die zum Arbeiten mit Kopf- und Fußzeilen und anderen Excel-Funktionen in Aspose.Cells erforderlich sind.

In dieser Anleitung erläutern wir jeden Schritt, sodass Sie ihn problemlos nachvollziehen können, auch wenn Sie mit Aspose.Cells oder .NET noch nicht vertraut sind.

## Schritt 1: Richten Sie Ihre Arbeitsmappe und Seiteneinrichtung ein

Das Wichtigste zuerst: Erstellen Sie eine neue Arbeitsmappe und rufen Sie die Seiteneinrichtung des Arbeitsblatts auf. Dadurch erhalten Sie die Tools, die Sie zum Ändern der Kopf- und Fußzeile für das Arbeitsblatt benötigen.

```csharp
// Definieren Sie den Pfad zum Speichern Ihres Dokuments
string dataDir = "Your Document Directory";

// Instanziieren eines Workbook-Objekts
Workbook excel = new Workbook();
```

 Hier haben wir ein`Workbook` Objekt, das unsere Excel-Datei darstellt. Das`PageSetup` des Arbeitsblattes können wir Kopf- und Fußzeilenoptionen ändern.


## Schritt 2: Zugriff auf die Eigenschaften von Arbeitsblatt und Seiteneinrichtung

 In Aspose.Cells hat jedes Arbeitsblatt eine`PageSetup`Eigenschaft, die Layout-Funktionen steuert, einschließlich Kopf- und Fußzeilen. Lassen Sie uns die`PageSetup` Objekt für unser Arbeitsblatt.

```csharp
// Holen Sie sich den Verweis auf das PageSetup des ersten Arbeitsblatts
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Damit`pageSetup` enthält jetzt alle Einstellungen, die zum Anpassen von Kopf- und Fußzeilen erforderlich sind.


## Schritt 3: Linken Bereich der Kopfzeile festlegen

Überschriften in Excel sind in drei Abschnitte unterteilt: links, Mitte und rechts. Beginnen wir damit, den linken Abschnitt so einzustellen, dass der Arbeitsblattname angezeigt wird.

```csharp
// Legen Sie den Arbeitsblattnamen im linken Abschnitt der Kopfzeile fest
pageSetup.SetHeader(0, "&A");
```

 Verwenden von`&A` ermöglicht Ihnen die dynamische Anzeige des Arbeitsblattnamens. Dies ist insbesondere dann hilfreich, wenn Sie mehrere Blätter in einer Arbeitsmappe haben und jede Kopfzeile den Blatttitel wiedergeben soll.


## Schritt 4: Datum und Uhrzeit in der Mitte der Kopfzeile hinzufügen

Als Nächstes fügen wir dem mittleren Abschnitt der Kopfzeile das aktuelle Datum und die aktuelle Uhrzeit hinzu. Darüber hinaus verwenden wir für die Formatierung eine benutzerdefinierte Schriftart.

```csharp
// Datum und Uhrzeit im mittleren Bereich der Kopfzeile in Fettschrift einstellen
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

In diesem Code:
- `&D`fügt das aktuelle Datum ein.
- `&T` fügt die aktuelle Uhrzeit ein.
- `"Times New Roman,Bold"` wendet auf diese Elemente Times New Roman in Fettschrift an.


## Schritt 5: Dateinamen im rechten Abschnitt der Kopfzeile anzeigen

Um die Kopfzeile zu vervollständigen, zeigen wir auf der rechten Seite den Dateinamen zusammen mit einer Schriftartanpassung an.

```csharp
// Dateinamen im rechten Abschnitt der Kopfzeile mit benutzerdefinierter Schriftgröße anzeigen
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` stellt den Dateinamen dar und macht deutlich, zu welcher Datei die ausgedruckten Seiten gehören.
- `&12` ändert die Schriftgröße für diesen Abschnitt auf 12.


## Schritt 6: Fügen Sie dem linken Fußzeilenabschnitt Text mit benutzerdefinierter Schriftart hinzu

Weiter geht’s mit den Fußzeilen! Wir beginnen mit der Einrichtung des linken Fußzeilenabschnitts mit benutzerdefiniertem Text und einem angegebenen Schriftstil.

```csharp
// Fügen Sie im linken Abschnitt der Fußzeile benutzerdefinierten Text mit Schriftstil hinzu
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 Der`&\"Courier New\"&14` Die Einstellung im obigen Code wendet die Schriftart "Courier New" mit Größe 14 auf den angegebenen Text an (`123`). Der restliche Text bleibt in der Standardschriftart der Fußzeile.


## Schritt 7: Seitenzahl in der Mitte der Fußzeile einfügen

Durch die Aufnahme von Seitenzahlen in die Fußzeile können Leser leichter den Überblick über mehrseitige Dokumente behalten.

```csharp
// Seitenzahl in den mittleren Bereich der Fußzeile einfügen
pageSetup.SetFooter(1, "&P");
```

 Hier,`&P` fügt die aktuelle Seitenzahl zum mittleren Abschnitt der Fußzeile hinzu. Dies ist ein kleines Detail, aber für professionell aussehende Dokumente von entscheidender Bedeutung.


## Schritt 8: Gesamtseitenzahl im rechten Fußzeilenbereich anzeigen

Zum Abschluss vervollständigen wir die Fußzeile, indem wir im rechten Abschnitt die Gesamtseitenzahl anzeigen.

```csharp
// Gesamtseitenzahl im rechten Abschnitt der Fußzeile anzeigen
pageSetup.SetFooter(2, "&N");
```

- `&N` gibt die Gesamtseitenzahl an und teilt dem Leser mit, wie lang das Dokument ist.


## Schritt 9: Speichern der Arbeitsmappe

Nachdem Sie Ihre Kopf- und Fußzeilen eingerichtet haben, ist es an der Zeit, die Arbeitsmappe zu speichern. Dies ist der letzte Schritt zum Generieren einer Excel-Datei mit vollständig angepassten Kopf- und Fußzeilen.

```csharp
// Speichern der Arbeitsmappe
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Diese Zeile speichert die Datei mit den benutzerdefinierten Kopf- und Fußzeilen im angegebenen Verzeichnis.


## Abschluss

Das Hinzufügen von Kopf- und Fußzeilen zu Excel-Arbeitsblättern ist eine wertvolle Fähigkeit zum Erstellen organisierter, professioneller Dokumente. Mit Aspose.Cells für .NET haben Sie die vollständige Kontrolle über die Kopf- und Fußzeilen Ihrer Excel-Dateien, von der Anzeige des Arbeitsblattnamens bis zum Einfügen von benutzerdefiniertem Text, Datum, Uhrzeit und sogar dynamischen Seitenzahlen. Nachdem Sie nun jeden Schritt in Aktion gesehen haben, können Sie Ihre Excel-Automatisierung auf die nächste Ebene bringen.

## Häufig gestellte Fragen

### Kann ich für unterschiedliche Abschnitte von Kopf- und Fußzeilen unterschiedliche Schriftarten verwenden?  
Ja, Aspose.Cells für .NET ermöglicht Ihnen, mithilfe spezifischer Schriftart-Tags Schriftarten für jeden Abschnitt der Kopf- und Fußzeile festzulegen.

### Wie entferne ich Kopf- und Fußzeilen?  
 Sie können Kopf- und Fußzeilen löschen, indem Sie den Text der Kopf- oder Fußzeile auf eine leere Zeichenfolge setzen mit`SetHeader` oder`SetFooter`.

### Kann ich mit Aspose.Cells für .NET Bilder in Kopf- oder Fußzeilen einfügen?  
Derzeit unterstützt Aspose.Cells hauptsächlich Text in Kopf- und Fußzeilen. Für Bilder ist möglicherweise ein Workaround erforderlich, z. B. das Einfügen von Bildern in das Arbeitsblatt selbst.

### Unterstützt Aspose.Cells dynamische Daten in Kopf- und Fußzeilen?  
 Ja, Sie können verschiedene dynamische Codes verwenden (wie`&D` für Datum oder`&P` für die Seitenzahl), um dynamischen Inhalt hinzuzufügen.

### Wie kann ich die Höhe der Kopf- oder Fußzeile anpassen?  
 Aspose.Cells bietet Optionen innerhalb der`PageSetup` Klasse zum Anpassen der Kopf- und Fußzeilenränder, sodass Sie die Abstände steuern können.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
