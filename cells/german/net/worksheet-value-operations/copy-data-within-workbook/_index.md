---
title: Kopieren von Daten innerhalb der Arbeitsmappe mit Aspose.Cells
linktitle: Kopieren von Daten innerhalb der Arbeitsmappe mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie mithilfe einer Schritt-für-Schritt-Anleitung, Codebeispielen und hilfreichen Tipps, wie Sie mit Aspose.Cells für .NET Daten effizient in einer Excel-Arbeitsmappe kopieren.
weight: 12
url: /de/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieren von Daten innerhalb der Arbeitsmappe mit Aspose.Cells

## Einführung
Die Verwaltung von Daten in Excel-Arbeitsmappen ist ein zentraler Bestandteil vieler Anwendungen. Stellen Sie sich vor, Sie haben eine Vorlage oder ein Blatt mit wichtigen Daten und möchten diese zur weiteren Verwendung in derselben Arbeitsmappe duplizieren. Hier glänzt Aspose.Cells für .NET! In diesem Handbuch führen wir Sie mit einem benutzerfreundlichen und klaren Schritt-für-Schritt-Tutorial durch das Kopieren von Daten innerhalb derselben Arbeitsmappe mit Aspose.Cells.
## Voraussetzungen
Bevor wir mit der Codierung beginnen, stellen wir sicher, dass wir alles haben, was wir zum Abschließen dieser Aufgabe benötigen:
1.  Aspose.Cells für .NET-Bibliothek – Laden Sie die neueste Version herunter von[Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/).
2. Entwicklungsumgebung – Sie benötigen eine .NET-kompatible IDE wie Visual Studio.
3.  Lizenz – Verwenden Sie eine kostenlose Testversion oder eine gekaufte Lizenz für Aspose.Cells. Sie können eine temporäre Lizenz erhalten[Hier](https://purchase.aspose.com/temporary-license/) oder Kaufoptionen erkunden[Hier](https://purchase.aspose.com/buy).
## Pakete importieren
In Ihrem Code müssen Sie Aspose.Cells importieren, um dessen Klassen und Methoden zu nutzen:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Tauchen wir in den Code ein! Wir werden die Aufgabe des Kopierens von Daten innerhalb einer Arbeitsmappe mit Aspose.Cells für .NET in leicht verständliche Schritte aufteilen.
## Schritt 1: Richten Sie Ihre Verzeichnispfade ein
Bevor wir mit der Bearbeitung der Arbeitsmappe beginnen, definieren wir, wo sich unsere Dateien befinden und wo wir die Ausgabe speichern möchten. Durch das Einrichten eines Verzeichnispfads bleibt die Übersichtlichkeit erhalten.
```csharp
// Legen Sie den Verzeichnispfad für Dokumente fest.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Ersetzen Sie hier`"Your Document Directory"` durch den tatsächlichen Pfad, in dem Ihre Arbeitsmappe gespeichert ist. Mit dieser Pfadvariable können Sie ganz einfach auf Ihre Eingabe- und Ausgabedateien verweisen.
## Schritt 2: Öffnen Sie die vorhandene Excel-Datei
Um mit einer Excel-Datei arbeiten zu können, müssen wir sie in das Arbeitsmappenobjekt in Aspose.Cells laden. Dieser Schritt öffnet die Datei, aus der Sie Daten kopieren möchten.
```csharp
// Öffnen Sie eine vorhandene Excel-Datei.
Workbook wb = new Workbook(inputPath);
```
 Damit ist unser`Workbook` Objekt`wb` ist nun bereit zur Interaktion mit den Inhalten von`book1.xls`.
## Schritt 3: Zugriff auf die Arbeitsblattsammlung
 Nachdem die Arbeitsmappe nun geöffnet ist, greifen wir auf die Arbeitsblattsammlung zu.`WorksheetCollection` Die Klasse hilft uns, mit mehreren Blättern innerhalb der Arbeitsmappe zu arbeiten.
```csharp
// Erstellen Sie ein Worksheets-Objekt, das auf alle Blätter in der Arbeitsmappe verweist.
WorksheetCollection sheets = wb.Worksheets;
```
 Hier,`sheets` ermöglicht uns, jedes Blatt in der Arbeitsmappe zu bearbeiten, einschließlich des Hinzufügens einer Kopie eines vorhandenen Blatts.
## Schritt 4: Daten in ein neues Blatt kopieren
Der Hauptteil unserer Aufgabe besteht darin, den Inhalt eines Blattes in ein neues Blatt innerhalb derselben Arbeitsmappe zu kopieren. In diesem Beispiel kopieren wir Daten aus „Blatt1“ in ein neues Blatt.
```csharp
// Kopieren Sie Daten aus „Sheet1“ in ein neues Blatt innerhalb der Arbeitsmappe.
sheets.AddCopy("Sheet1");
```
 Der`AddCopy`Methode erstellt eine exakte Kopie des angegebenen Blatts und hängt es an die Arbeitsmappe an. Hier duplizieren wir „Sheet1“. Sie können den Namen jedes Blatts angeben, das Sie kopieren möchten.
## Schritt 5: Speichern Sie die Arbeitsmappe mit dem neuen Blatt
Speichern Sie die Arbeitsmappe nach dem Kopieren des Blattes unter einem neuen Namen oder an einem neuen Speicherort, um die Änderungen beizubehalten.
```csharp
// Speichern Sie die Arbeitsmappe mit den kopierten Daten.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Diese Zeile speichert die geänderte Arbeitsmappe als`CopyWithinWorkbook_out.xls` im angegebenen Verzeichnis.
## Abschluss
Und da haben Sie es! Das Kopieren von Daten innerhalb einer Arbeitsmappe mit Aspose.Cells für .NET ist ein Kinderspiel. Aspose.Cells macht die Handhabung von Excel-Dateien unkompliziert und ermöglicht Ihnen die mühelose Durchführung komplexer Datenverwaltungsaufgaben. Ob Sie Blätter zur Verwendung von Vorlagen, für Backups oder zum Erstellen neuer Versionen duplizieren müssen, die von uns beschriebenen Schritte helfen Ihnen, Ihre Ziele zu erreichen.
 Wenn Sie mehr entdecken möchten, besuchen Sie die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für erweiterte Funktionen und Fähigkeiten.
## Häufig gestellte Fragen
### Kann ich mehrere Blätter auf einmal kopieren?
Aspose.Cells unterstützt nicht das Kopieren mehrerer Blätter in einem einzigen Aufruf, aber Sie können die Blätter, die Sie duplizieren möchten, durchlaufen und sie einzeln kopieren.
### Kann ich das kopierte Blatt umbenennen?
 Ja, nachdem Sie das Blatt kopiert haben, können Sie es umbenennen mit`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Ist Aspose.Cells mit .NET Core kompatibel?
Absolut! Aspose.Cells unterstützt sowohl .NET Framework- als auch .NET Core-Umgebungen.
### Wie gehe ich mit der Formatierung beim Kopieren von Blättern um?
 Der`AddCopy` Bei dieser Methode bleiben der gesamte Inhalt und die Formatierung erhalten, sodass Ihr kopiertes Blatt genauso aussieht wie das Original.
### Was passiert, wenn ich ein Blatt in eine andere Arbeitsmappe kopieren möchte?
Sie können die`Copy` -Methode mit einem Verweis auf eine andere Arbeitsmappe, wie`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
