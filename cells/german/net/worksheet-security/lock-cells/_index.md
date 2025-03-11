---
title: Zellen im Arbeitsblatt mit Aspose.Cells sperren
linktitle: Zellen im Arbeitsblatt mit Aspose.Cells sperren
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie Zellen in Excel mit Aspose.Cells für .NET sperren. Schützen Sie Ihre Daten mit detaillierten Codebeispielen und einfachen Anweisungen.
weight: 25
url: /de/net/worksheet-security/lock-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zellen im Arbeitsblatt mit Aspose.Cells sperren

## Einführung
Das Sperren von Zellen in einem Excel-Arbeitsblatt ist eine wichtige Funktion, insbesondere wenn Sie Ihre Dokumente mit anderen teilen. Durch das Sperren von Zellen können Sie steuern, welche Teile Ihres Arbeitsblatts bearbeitet werden können, wodurch die Datenintegrität gewahrt und unerwünschte Änderungen verhindert werden. In diesem Handbuch erfahren Sie ausführlich, wie Sie mit Aspose.Cells für .NET bestimmte Zellen in einem Arbeitsblatt sperren können. Aspose.Cells ist eine leistungsstarke Bibliothek, mit der Sie Excel-Dateien problemlos programmgesteuert bearbeiten können, und das Sperren von Zellen ist eine der vielen Funktionen, die sie bietet.

## Voraussetzungen

Bevor wir mit dem Lernprogramm beginnen, wollen wir die wichtigsten Dinge durchgehen, die Sie zum Mitmachen benötigen.

1.  Aspose.Cells für .NET: Stellen Sie zunächst sicher, dass Sie die Aspose.Cells-Bibliothek installiert haben. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/) oder installieren Sie es über NuGet in Visual Studio, indem Sie Folgendes ausführen:

```bash
Install-Package Aspose.Cells
```

2. Entwicklungsumgebung: Dieses Tutorial setzt voraus, dass Sie eine .NET-Entwicklungsumgebung (wie Visual Studio) verwenden. Stellen Sie sicher, dass sie eingerichtet und bereit ist, C#-Code auszuführen.

3.  Lizenzeinrichtung (optional): Obwohl Aspose.Cells mit einer kostenlosen Testversion verwendet werden kann, benötigen Sie für die volle Funktionalität eine Lizenz. Sie erhalten eine[vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/) wenn Sie den kompletten Funktionsumfang testen möchten.


## Pakete importieren

Um mit Aspose.Cells zu beginnen, müssen Sie die erforderlichen Namespaces importieren. Diese Namespaces bieten Zugriff auf die Klassen und Methoden, die Sie zum Bearbeiten von Excel-Dateien verwenden.

Fügen Sie oben in Ihrer C#-Datei die folgende Zeile hinzu:

```csharp
using System.IO;
using Aspose.Cells;
```

Lassen Sie uns den Vorgang des Zellensperrens in klare, überschaubare Schritte unterteilen.

## Schritt 1: Richten Sie Ihre Arbeitsmappe ein und laden Sie eine Excel-Datei

Laden wir zunächst die Excel-Datei, in der wir bestimmte Zellen sperren möchten. Dies kann eine vorhandene oder eine neue Datei sein, die Sie zu Testzwecken erstellen.

```csharp
// Geben Sie den Pfad zu Ihrer Excel-Datei an
string dataDir = "Your Document Directory";

// Laden der Arbeitsmappe
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```

Folgendes ist passiert:
- Wir geben das Verzeichnis an, in dem Ihre Excel-Datei liegt.
-  Der`Workbook`Objekt stellt die gesamte Excel-Datei dar, und durch das Laden`Book1.xlsx`, bringen wir es in Erinnerung.

## Schritt 2: Zugriff auf das gewünschte Arbeitsblatt

Nachdem die Arbeitsmappe nun geladen ist, greifen wir auf das spezifische Arbeitsblatt zu, in dem Sie Zellen sperren möchten.

```csharp
// Greifen Sie auf das erste Arbeitsblatt in der Excel-Datei zu
Worksheet worksheet = workbook.Worksheets[0];
```

Über diese Zeile können Sie mit dem ersten Arbeitsblatt in Ihrer Arbeitsmappe interagieren. Wenn Sie ein anderes Arbeitsblatt ansprechen möchten, passen Sie einfach den Index an oder geben Sie den Namen des Blatts an.

## Schritt 3: Bestimmte Zellen sperren

In diesem Schritt sperren wir eine bestimmte Zelle, sodass niemand sie bearbeiten kann. Hier sehen Sie als Beispiel, wie das für die Zelle „A1“ geht.

```csharp
// Betreten Sie Zelle A1 und verriegeln Sie sie
Style style = worksheet.Cells["A1"].GetStyle();
style.IsLocked = true;
worksheet.Cells["A1"].SetStyle(style);
```

Dieser Codeausschnitt:
- Greift auf die Zelle bei „A1“ zu.
- Ruft den aktuellen Stil der Zelle ab.
-  Legt die`IsLocked` Eigentum an`true`, wodurch die Zelle verriegelt wird.
- Wendet den aktualisierten Stil wieder auf die Zelle an.

## Schritt 4: Schützen Sie das Arbeitsblatt

Das Sperren der Zellen allein reicht nicht aus. Um die Sperre zu erzwingen, müssen wir auch das Arbeitsblatt schützen. Ohne Schutz können die gesperrten Zellen weiterhin bearbeitet werden.

```csharp
// Schützen Sie das Arbeitsblatt, um die Zellensperre zu aktivieren
worksheet.Protect(ProtectionType.All);
```

Dies bewirkt Folgendes:
-  Der`Protect` -Methode wird aufgerufen auf`worksheet` Objekt, wobei der Schutz auf das gesamte Blatt angewendet wird.
-  Wir verwenden`ProtectionType.All` um alle Arten von Schutz abzudecken und sicherzustellen, dass unsere verschlossenen Zellen sicher bleiben.

## Schritt 5: Speichern der Arbeitsmappe

Nachdem Sie die Zellensperren und den Arbeitsblattschutz angewendet haben, ist es an der Zeit, Ihre Änderungen zu speichern. Sie können sie als neue Datei speichern oder die vorhandene überschreiben.

```csharp
// Speichern der Arbeitsmappe mit gesperrten Zellen
workbook.Save(dataDir + "output.xlsx");
```

Dieser Code:
-  Speichert die Arbeitsmappe mit den gesperrten Zellen in einer neuen Datei namens`output.xlsx` im angegebenen Verzeichnis.
- Wenn Sie die Originaldatei überschreiben möchten, können Sie stattdessen den ursprünglichen Dateinamen verwenden.


## Abschluss

Und das war’s! Sie haben erfolgreich bestimmte Zellen in einem Arbeitsblatt mit Aspose.Cells für .NET gesperrt. Indem Sie diese Schritte befolgen, können Sie wichtige Daten in Ihren Excel-Dateien schützen und sicherstellen, dass nur die von Ihnen ausgewählten Zellen bearbeitet werden können. Aspose.Cells macht es einfach, diese Funktionalität mit minimalem Code hinzuzufügen, wodurch Ihre Dokumente sicherer und professioneller werden.


## Häufig gestellte Fragen

### Kann ich mehrere Zellen gleichzeitig sperren?
Ja, Sie können einen Zellbereich durchlaufen und auf jede Zelle denselben Stil anwenden, um mehrere Zellen gleichzeitig zu sperren.

### Muss ich das gesamte Arbeitsblatt schützen, um Zellen zu sperren?
Ja, damit das Sperren von Zellen wirksam wird, ist der Arbeitsblattschutz erforderlich. Ohne diesen wird die Sperreigenschaft ignoriert.

### Kann ich Aspose.Cells mit einer kostenlosen Testversion nutzen?
 Absolut! Sie können es mit einer kostenlosen Testversion ausprobieren. Für längere Tests sollten Sie eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).

### Wie entsperre ich Zellen, nachdem ich sie gesperrt habe?
 Sie können festlegen`IsLocked` Zu`false` Klicken Sie auf den Stil der Zelle, um sie zu entsperren, und entfernen Sie dann den Schutz vom Arbeitsblatt.

### Ist es möglich, das Arbeitsblatt mit einem Passwort zu schützen?
Ja, Aspose.Cells ermöglicht Ihnen, beim Schutz des Arbeitsblatts ein Kennwort hinzuzufügen und so eine zusätzliche Sicherheitsebene hinzuzufügen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
