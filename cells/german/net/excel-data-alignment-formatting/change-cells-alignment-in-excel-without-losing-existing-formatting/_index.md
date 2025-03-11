---
title: Ändern Sie die Ausrichtung von Excel-Zellen, ohne die Formatierung zu verlieren
linktitle: Ändern Sie die Ausrichtung von Excel-Zellen, ohne die Formatierung zu verlieren
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET die Ausrichtung von Excel-Zellen ändern, ohne die Formatierung zu verlieren. Folgen Sie unserer umfassenden Schritt-für-Schritt-Anleitung für nahtlose Kontrolle.
weight: 10
url: /de/net/excel-data-alignment-formatting/change-cells-alignment-in-excel-without-losing-existing-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ändern Sie die Ausrichtung von Excel-Zellen, ohne die Formatierung zu verlieren

## Einführung

Die Verwaltung von Excel-Dateien kann sich manchmal wie das Navigieren durch ein Labyrinth anfühlen, insbesondere wenn es darum geht, die Formatierung beizubehalten und gleichzeitig wichtige Anpassungen wie die Änderung der Zellausrichtung vorzunehmen. Wenn Sie jemals versucht haben, die Ausrichtung von Zellen in Excel zu optimieren, nur um festzustellen, dass die Formatierung gestört wird, sind Sie nicht allein! In diesem Tutorial werden wir uns damit befassen, wie Sie die Ausrichtung von Excel-Zellen ändern können, ohne die Formatierung zu verlieren, indem Sie Aspose.Cells für .NET verwenden. Krempeln wir die Ärmel hoch und legen los!

## Voraussetzungen

Bevor wir mit der eigentlichen Codierung beginnen, müssen Sie sicherstellen, dass Sie alles richtig eingerichtet haben. Folgendes benötigen Sie:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio (jede Version, die .NET unterstützt) auf Ihrem Computer installiert ist.
2. Aspose.Cells für .NET: Laden Sie die Aspose.Cells-Bibliothek herunter und installieren Sie sie von[Asposes Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Ein wenig Vertrautheit mit der C#-Programmierung ist hilfreich, da wir in einem C#-Kontext arbeiten werden.
4.  Beispiel-Excel-Datei: Lassen Sie zur Demonstration eine Beispiel-Excel-Datei vorbereiten (z. B.`sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx`), das eine anfängliche Zellenformatierung enthält.

## Pakete importieren

Der erste Schritt bei der Verwendung von Aspose.Cells für .NET besteht darin, die erforderlichen Namespaces in Ihr Projekt einzubinden. So geht's:

### Öffnen Sie Ihr Projekt

Öffnen Sie Visual Studio und erstellen Sie ein neues C#-Projekt (eine Konsolenanwendung funktioniert problemlos).

### Verweis auf Aspose.Cells hinzufügen

- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
- Wählen Sie „NuGet-Pakete verwalten“.
-  Suchen nach`Aspose.Cells` und installieren Sie es.

### Importieren der erforderlichen Namespaces

Fügen Sie oben in Ihrer C#-Datei die folgenden Using-Direktiven hinzu:

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Tables;
```

Dadurch können Sie die von der Aspose.Cells-Bibliothek bereitgestellten Klassen und Methoden nahtlos verwenden.

Nachdem wir nun unsere Voraussetzungen sortiert und Pakete importiert haben, wollen wir den Vorgang zum Ändern der Zellenausrichtung Schritt für Schritt aufschlüsseln.

## Schritt 1: Richten Sie Ihre Quell- und Ausgabeverzeichnisse ein

Zu Beginn müssen Sie festlegen, wo Ihre Excel-Datei gespeichert ist und wo Sie sie nach der Verarbeitung speichern möchten.

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory\\"; // Ersetzen Sie es durch Ihr aktuelles Verzeichnis

// Ausgabeverzeichnis
string outputDir = "Your Document Directory\\"; // Ersetzen Sie es durch Ihr aktuelles Verzeichnis
```

 Dieser Code legt die Pfade für die Eingabe- und Ausgabedateien fest. Ersetzen Sie unbedingt`"Your Document Directory\\"` durch den tatsächlichen Pfad auf Ihrem Computer.

## Schritt 2: Laden Sie die Excel-Beispieldatei

Als Nächstes möchten Sie Ihre Excel-Beispieldatei in die Anwendung laden.

```csharp
// Laden Sie eine Beispiel-Excel-Datei mit formatierten Zellen.
Workbook wb = new Workbook(sourceDir + "sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx");
```

Diese Codezeile verwendet die Workbook-Klasse, um Ihre vorhandene Excel-Datei zu laden, damit wir ihren Inhalt bearbeiten können.

## Schritt 3: Zugriff auf das gewünschte Arbeitsblatt

Rufen Sie nach dem Laden der Arbeitsmappe das Arbeitsblatt auf, das Sie bearbeiten möchten. Excel-Dateien können mehrere Blätter enthalten. Stellen Sie daher sicher, dass Sie das richtige auswählen.

```csharp
// Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```

Dieses Beispiel greift auf das erste Arbeitsblatt zu. Wenn Ihre Daten auf einem anderen Blatt liegen, passen Sie den Index entsprechend an.

## Schritt 4: Erstellen Sie einen Zellbereich

Legen Sie fest, welche Zellen Sie ändern möchten, indem Sie einen Bereich erstellen. Diese Auswahl konzentriert sich auf einen angegebenen Bereich, z. B. „B2:D7“.

```csharp
//Zellenbereich erstellen.
Range rng = ws.Cells.CreateRange("B2:D7");
```

Dieser Bereich ermöglicht es uns, die neuen Ausrichtungseinstellungen direkt auf diese Zellen anzuwenden.

## Schritt 5: Erstellen und Anpassen eines Stilobjekts

Jetzt müssen wir die Ausrichtungsstile definieren, die wir anwenden möchten.

```csharp
// Stilobjekt erstellen.
Style st = wb.CreateStyle();

// Stellen Sie die horizontale und vertikale Ausrichtung auf Mitte ein.
st.HorizontalAlignment = TextAlignmentType.Center;
st.VerticalAlignment = TextAlignmentType.Center;
```

Hier wird ein neues Style-Objekt erstellt und wir stellen sowohl die horizontale als auch die vertikale Ausrichtung auf zentriert ein. Dies hilft dabei, den Text innerhalb der ausgewählten Zellen präzise auszurichten.

## Schritt 6: Stilflaggen einrichten

Das Setzen von Stilflags spielt eine entscheidende Rolle dabei, sicherzustellen, dass Ihre Stiländerungen angewendet werden. 

```csharp
// Erstellen Sie ein Stilflaggenobjekt.
StyleFlag flag = new StyleFlag();

// Setzen Sie die Ausrichtung der Stilflagge auf „true“. Dies ist eine entscheidende Anweisung.
flag.Alignments = true;
```

 Durch die Einstellung der`Alignments` Eigenschaft der StyleFlag auf`true`weisen Sie Aspose.Cells an, die Ausrichtungsstile richtig anzuwenden.

## Schritt 7: Den Stil auf den Zellbereich anwenden

Nachdem Sie Ihre Stile und Flags eingerichtet haben, können Sie diese auf den Zellbereich anwenden:

```csharp
//Stil auf Zellbereich anwenden.
rng.ApplyStyle(st, flag);
```

Dieser Schritt ändert effektiv die Ausrichtung aller Zellen innerhalb dieses Bereichs, während die vorhandene Formatierung erhalten bleibt.

## Schritt 8: Speichern Sie die Arbeitsmappe

Abschließend möchten Sie Ihre Änderungen in einer neuen Datei speichern, damit das Original erhalten bleibt.

```csharp
// Speichern Sie die Arbeitsmappe im XLSX-Format.
wb.Save(outputDir + "outputChangeCellsAlignmentAndKeepExistingFormatting.xlsx", SaveFormat.Xlsx);
```

Diese Zeile speichert die Arbeitsmappe mit allen Ausrichtungsänderungen im zuvor angegebenen Ausgabeverzeichnis.

## Schritt 9: Erfolg melden

Nach dem Speichern der Datei ist es schön, eine Rückmeldung zu geben, dass alles wie erwartet funktioniert hat!

```csharp
Console.WriteLine("ChangeCellsAlignmentAndKeepExistingFormatting executed successfully.");
```

Diese Meldung wird in der Konsole angezeigt, wenn Ihr Vorgang ohne Probleme abgeschlossen wird.

## Abschluss

Mit Aspose.Cells für .NET können Sie die Zellausrichtung in Excel ändern und dabei die vorhandene Formatierung beibehalten. Indem Sie diese Schritte befolgen, können Sie die Excel-Manipulation in Ihren Anwendungen vereinfachen und den Ärger vermeiden, wertvolle Formatierungen zu verlieren. Egal, ob Sie Berichte erstellen oder Datenfeeds verwalten, die Beherrschung dieser Fähigkeit kann bahnbrechend sein!

## Häufig gestellte Fragen

### Kann Aspose.Cells große Excel-Dateien verarbeiten?
Auf jeden Fall! Es ist auf Leistung optimiert und kann große Dateien effizient verarbeiten.

### Gibt es eine Testversion für Aspose.Cells?
 Ja! Sie können eine kostenlose Testversion von der Website herunterladen[Kostenlose Testversion](https://releases.aspose.com/).

### Welche Programmiersprachen unterstützt Aspose.Cells?
Aspose.Cells unterstützt hauptsächlich .NET, Java und mehrere andere Sprachen über entsprechende Bibliotheken.

### Wie kann ich Support für Aspose.Cells erhalten?
 Bei Fragen oder Support-Problemen besuchen Sie bitte die[Support-Forum](https://forum.aspose.com/c/cells/9).

### Kann ich mehrere Stile gleichzeitig anwenden?
Ja, Sie können mehrere Style-Objekte erstellen und diese je nach Bedarf nacheinander oder bedingt anwenden.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
