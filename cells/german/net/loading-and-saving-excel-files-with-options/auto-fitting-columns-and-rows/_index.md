---
title: Automatisches Anpassen von Spalten und Zeilen beim Laden von HTML in die Arbeitsmappe
linktitle: Automatisches Anpassen von Spalten und Zeilen beim Laden von HTML in die Arbeitsmappe
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET Spalten und Zeilen beim Laden von HTML in Excel automatisch anpassen. Schritt-für-Schritt-Anleitung enthalten.
weight: 10
url: /de/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatisches Anpassen von Spalten und Zeilen beim Laden von HTML in die Arbeitsmappe

## Einführung
Haben Sie sich schon einmal gefragt, wie Sie die Spalten- und Zeilengrößen beim Laden von HTML-Inhalten in eine Excel-Arbeitsmappe mit Aspose.Cells für .NET automatisch anpassen können? Dann sind Sie hier richtig! In diesem Tutorial erfahren Sie im Detail, wie Sie eine HTML-Tabelle in eine Arbeitsmappe laden und sicherstellen, dass die Spalten und Zeilen automatisch an den Inhalt angepasst werden. Wenn Sie mit dynamischen Daten arbeiten, die sich häufig ändern, ist dieser Leitfaden Ihre erste Anlaufstelle zum Erstellen gut formatierter Excel-Tabellen aus HTML.
### Voraussetzungen
Bevor Sie mit dem Code beginnen, müssen Sie einige Dinge auf Ihrem System einrichten. Keine Sorge, es ist ganz einfach!
1. Visual Studio installiert: Sie benötigen Visual Studio oder eine andere .NET-Entwicklungsumgebung.
2.  Aspose.Cells für .NET: Sie können[Laden Sie die neueste Version herunter](https://releases.aspose.com/cells/net/) oder verwenden Sie den NuGet-Paket-Manager, um es zu installieren.
3. .NET Framework: Stellen Sie sicher, dass Sie .NET Framework 4.0 oder höher installiert haben.
4. Grundlegende Kenntnisse in C#: Wenn Sie über einige Kenntnisse in C# verfügen, wird Ihnen dieses Tutorial leichter fallen.
5. HTML-Tabellendaten: Bereiten Sie HTML-Inhalte (auch eine einfache Tabelle) vor, die Sie in Excel laden möchten.
## Pakete importieren
Das Wichtigste zuerst: Lassen Sie uns zunächst die erforderlichen Namespaces importieren. Hier ist eine einfache Liste der zu importierenden Elemente:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Mit diesen Paketen können Sie die Arbeitsmappe verwalten, HTML-Daten bearbeiten und sie nahtlos in Excel laden.
Lassen Sie uns diesen Prozess in überschaubare Abschnitte aufteilen, damit Sie ihn problemlos nachvollziehen können. Am Ende haben Sie ein funktionierendes Beispiel dafür, wie Sie Spalten und Zeilen automatisch anpassen, während Sie HTML mit Aspose.Cells für .NET in eine Arbeitsmappe laden.
## Schritt 1: Einrichten des Dokumentverzeichnisses
Damit Sie Dateien einfach speichern und abrufen können, geben wir den Pfad an, in dem Ihre Dokumente gespeichert werden. Sie können den Verzeichnispfad durch Ihren eigenen Ordnerspeicherort ersetzen.
```csharp
string dataDir = "Your Document Directory";
```
Diese Zeile legt das Verzeichnis fest, in dem Ihre Excel-Dateien gespeichert werden. Wenn Sie an mehreren Projekten arbeiten, ist es wichtig, Ihre Dateien richtig zu organisieren. Stellen Sie sich dies als den Aktenschrank Ihres Projekts vor!
## Schritt 2: HTML-Daten als String erstellen
Als Nächstes definieren wir einige grundlegende HTML-Inhalte. Für dieses Beispiel verwenden wir eine einfache HTML-Tabelle. Sie können sie entsprechend den Anforderungen Ihres Projekts anpassen.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Wir definieren hier einen sehr einfachen HTML-String. Er enthält eine Tabelle mit einigen Zeilen und Spalten. Sie können je nach Bedarf weitere Zeilen oder Spalten hinzufügen. Stellen Sie es sich so vor, als würden Sie die Zutaten vor dem Kochen einer Mahlzeit vorbereiten!
## Schritt 3: HTML-String in MemoryStream laden
 Nachdem wir nun unseren HTML-Inhalt fertig haben, besteht der nächste Schritt darin, ihn in den Speicher zu laden.`MemoryStream`. Dadurch können wir den HTML-Inhalt im Speicher bearbeiten, ohne ihn vorher auf der Festplatte zu speichern.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 Indem wir den HTML-String in ein Byte-Array umwandeln und ihn in ein`MemoryStream`können wir mit den HTML-Daten im Speicher arbeiten. Stellen Sie sich diesen Schritt so vor, als ob Sie das Gericht in einem Topf zubereiten, bevor Sie es in den Ofen schieben!
## Schritt 4: MemoryStream in eine Arbeitsmappe laden (ohne automatische Anpassung)
 Sobald wir den HTML-Inhalt im Speicher haben, laden wir ihn in ein Aspose`Workbook`An diesem Punkt passen wir die Spalten und Zeilen noch nicht automatisch an. Dies ist unser „Vorher“-Szenario, das wir später mit der automatisch angepassten Version vergleichen.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Die Arbeitsmappe wird mit dem HTML-Inhalt geladen, aber die Spalten und Zeilen werden noch nicht automatisch an den Text angepasst. Stellen Sie sich das so vor, als würden Sie einen Kuchen backen, aber vergessen, die Temperatur zu überprüfen – es funktioniert, aber es ist möglicherweise nicht perfekt!
## Schritt 5: HTML-Ladeoptionen mit aktivierter automatischer Anpassung festlegen
 Und jetzt kommt der Zauber! Wir erstellen eine Instanz von`HtmlLoadOptions` und aktivieren Sie die`AutoFitColsAndRows` Eigenschaft. Dadurch wird sichergestellt, dass beim Laden des HTML-Inhalts die Spalten und Zeilen an den darin enthaltenen Inhalt angepasst werden.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Indem wir diese Option festlegen, weisen wir Aspose.Cells an, die Größe der Zeilen und Spalten automatisch anzupassen. Stellen Sie sich das so vor, als würden Sie den Ofen auf die perfekte Temperatur einstellen, damit der Kuchen genau richtig aufgeht!
## Schritt 6: HTML in Arbeitsmappe laden und dabei die automatische Anpassung aktivieren
 Nun laden wir den HTML-Inhalt erneut, diesmal jedoch mit dem`AutoFitColsAndRows`Option aktiviert. Dadurch werden die Spaltenbreiten und Zeilenhöhen basierend auf dem Inhalt angepasst.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Dieser Schritt lädt den HTML-Inhalt in eine neue Arbeitsmappe und speichert sie als Excel-Datei, aber jetzt werden die Spalten und Zeilen automatisch angepasst! Stellen Sie sich das wie den perfekt gebackenen Kuchen vor, bei dem alles genau die richtige Größe hat.
## Abschluss
Indem Sie diese einfachen Schritte befolgen, haben Sie gelernt, wie Sie mit Aspose.Cells für .NET HTML-Inhalte in eine Arbeitsmappe laden und die Spalten und Zeilen automatisch anpassen. Dadurch wird sichergestellt, dass Ihre Excel-Tabellen immer ordentlich aussehen, egal wie dynamisch der Inhalt ist. Es ist eine einfache, aber leistungsstarke Funktion, mit der Sie beim Formatieren und Organisieren Ihrer Excel-Daten jede Menge Zeit sparen können.
Da Sie nun über dieses Wissen verfügen, können Sie mit komplexeren HTML-Inhalten experimentieren, Stile hinzufügen und sogar ganze Excel-Arbeitsmappen aus Webseiten erstellen!
## Häufig gestellte Fragen
### Kann ich mit dieser Methode große HTML-Tabellen laden?
Ja, Aspose.Cells verarbeitet große HTML-Tabellen effizient, aber für eine optimale Leistung ist es ratsam, Tests mit Ihren Datengrößen durchzuführen.
### Kann ich nach der automatischen Anpassung bestimmte Spaltenbreiten und Zeilenhöhen manuell anwenden?
Auf jeden Fall! Sie können einzelne Spalten und Zeilen auch nach der Verwendung der Funktion zur automatischen Anpassung noch anpassen.
### Wie kann ich die Tabelle nach dem Laden von HTML formatieren?
Sie können Stile mit den umfangreichen Stiloptionen von Aspose.Cells anwenden, nachdem Sie das HTML geladen haben.
### Ist Aspose.Cells für .NET mit älteren Versionen von .NET Framework kompatibel?
Ja, Aspose.Cells für .NET unterstützt .NET Framework 4.0 und höher.
### Kann ich mit Aspose.Cells auch andere Inhaltstypen als HTML in Excel laden?
Ja, Aspose.Cells unterstützt das Laden verschiedener Formate wie CSV, JSON und XML in Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
