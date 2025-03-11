---
title: Registrieren und Aufrufen der Funktion vom Add-In in Excel
linktitle: Registrieren und Aufrufen der Funktion vom Add-In in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie mit unserem einfachen Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Funktionen von Add-Ins in Excel registrieren und aufrufen.
weight: 20
url: /de/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Registrieren und Aufrufen der Funktion vom Add-In in Excel

## Einführung
Möchten Sie Ihre Excel-Erfahrung verbessern, indem Sie Funktionen aus einem Add-In aufrufen? Wenn ja, sind Sie hier richtig! Excel-Add-Ins sind wie die guten Feen der Tabellenkalkulationen; sie erweitern auf magische Weise die Funktionalität und geben Ihnen eine Reihe neuer Tools an die Hand. Und mit Aspose.Cells für .NET ist es einfacher denn je, diese Add-In-Funktionen zu registrieren und zu verwenden. 
In dieser Anleitung führe ich Sie durch den Prozess der Registrierung und des Aufrufs einer Funktion aus einem Excel-Add-In mithilfe von Aspose.Cells für .NET. Wir werden alles Schritt für Schritt durchgehen, sodass Sie sich im Handumdrehen wie ein Profi fühlen!
## Voraussetzungen
Bevor wir uns in die Zauberei der Codierung stürzen, wollen wir uns ansehen, was Sie dafür benötigen:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer eingerichtet ist. Hier werden wir unseren Code schreiben und ausführen.
2.  Aspose.Cells-Bibliothek: Sie müssen die Aspose.Cells-Bibliothek installiert haben. Sie können sie von ihrem[Download-Seite](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Ein wenig Verständnis von C# wird Ihnen sehr helfen; es wird Ihnen helfen, nahtlos mitzukommen.
4.  Excel-Add-Ins: Sie sollten eine Add-In-Datei haben (wie`.xlam`), das die Funktionen enthält, die Sie registrieren und verwenden möchten.
5.  Ein Beispiel für ein Excel-Add-In: Für dieses Tutorial verwenden wir ein Excel-Add-In namens`TESTUDF.xlam`. Stellen Sie also sicher, dass Sie dies zur Verfügung haben!
Jetzt, da Sie eingerichtet sind, krempeln wir die Ärmel hoch und legen mit dem Programmieren los!
## Pakete importieren
Um zu beginnen, müssen Sie einige wichtige Namespaces oben in Ihre C#-Datei importieren. Folgendes müssen Sie einschließen:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Diese Namespaces ermöglichen Ihnen den Zugriff auf die Klassen und Methoden, die wir in diesem Tutorial verwenden werden.
Lassen Sie uns dies in überschaubare Schritte unterteilen. Am Ende dieses Handbuchs verfügen Sie über ein solides Verständnis dafür, wie Sie Add-In-Funktionen registrieren und in Ihren Excel-Arbeitsmappen verwenden.
## Schritt 1: Richten Sie Ihre Quell- und Ausgabeverzeichnisse ein
Bevor Sie Ihr Add-In registrieren können, müssen Sie definieren, wo Ihr Add-In und die Ausgabedateien gespeichert werden.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad, auf dem Ihr`.xlam` Datei und Ausgabedateien werden gespeichert. Das ist so, als würde man die Bühne vorbereiten, bevor die Show beginnt.
## Schritt 2: Erstellen Sie eine leere Arbeitsmappe
Als Nächstes möchten Sie eine leere Arbeitsmappe erstellen, in der wir mit Add-In-Funktionen herumspielen können.
```csharp
// Leere Arbeitsmappe erstellen
Workbook workbook = new Workbook();
```
Diese Codezeile erstellt eine neue Arbeitsmappe, die uns als Spielplatz dient. Betrachten Sie sie als eine frische Leinwand, bereit für Ihre kreativen Striche.
## Schritt 3: Registrieren der Add-In-Funktion
Kommen wir nun zum Kern der Sache! Es ist Zeit, Ihre Add-In-Funktion zu registrieren. So geht's:
```csharp
// Makrofähiges Add-In zusammen mit dem Funktionsnamen registrieren
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Diese Zeile registriert die Add-In-Funktion namens`TEST_UDF` gefunden in der`TESTUDF.xlam` Add-In-Datei. Die`false`Der Parameter bedeutet, dass das Add-In nicht im „isolierten“ Modus geladen wird. 
## Schritt 4: Zusätzliche Funktionen registrieren (sofern vorhanden)
Wenn Sie weitere Funktionen in derselben Add-In-Datei registriert haben, können Sie diese auch registrieren!
```csharp
// Weitere Funktionen in der Datei registrieren (sofern vorhanden)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Hier sehen Sie, wie einfach es ist, aus demselben Add-In weitere Funktionen hinzuzufügen. Stapeln Sie sie einfach wie Bausteine!
## Schritt 5: Zugriff auf das Arbeitsblatt
Fahren wir fort und rufen das Arbeitsblatt auf, in dem wir unsere Funktion verwenden werden. 
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
```
Wir greifen auf das erste Arbeitsblatt in der Arbeitsmappe zu, um unsere Formel einzugeben. Es ist, als würden wir die Tür zu dem Raum öffnen, in dem der Spaß stattfindet.
## Schritt 6: Auf eine bestimmte Zelle zugreifen
Als nächstes müssen wir auswählen, welche Zelle wir für unsere Formel verwenden möchten. 
```csharp
// Zugriff auf die erste Zelle
var cell = worksheet.Cells["A1"];
```
Hier zeigen wir auf Zelle A1. Hier werden wir unsere Zauberformel einfügen. Man könnte es sich so vorstellen, als ob man ein Ziel auf seiner Schatzkarte festlegt!
## Schritt 7: Legen Sie die Formel fest
Jetzt ist es Zeit für die große Enthüllung! Lassen Sie uns die Formel festlegen, die unsere registrierte Funktion aufruft.
```csharp
// Im Add-In vorhandenen Formelnamen festlegen
cell.Formula = "=TEST_UDF()";
```
Mit dieser Zeile sagen wir Excel, dass es unsere Funktion in Zelle A1 verwenden soll. Das ist, als ob wir Excel einen Befehl geben und sagen: „Hey, mach das!“
## Schritt 8: Speichern Sie die Arbeitsmappe
Zu guter Letzt ist es Zeit, unser Meisterwerk zu retten.
```csharp
// Speichern Sie die Arbeitsmappe im Ausgabeformat XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Hier speichern wir unsere Arbeitsmappe als XLSX-Datei. Dieser letzte Schritt ist, als würden Sie Ihr Gemälde in einen Rahmen stecken und es für die Präsentation vorbereiten!
## Schritt 9: Ausführung bestätigen
Lassen Sie uns zum Schluss alles zusammenfassen, indem wir eine Erfolgsmeldung auf der Konsole ausgeben.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Diese Linie dient als unsere Siegesflagge. Sie ist eine nette kleine Geste, um zu bestätigen, dass alles reibungslos gelaufen ist.
## Abschluss 
Und da haben Sie es! Sie haben nicht nur gelernt, wie Sie mit Aspose.Cells für .NET Funktionen aus Excel-Add-Ins registrieren und aufrufen, sondern auch ein tieferes Verständnis für jeden einzelnen Schritt gewonnen. Das Leben ist jetzt ein bisschen einfacher, nicht wahr? Warum probieren Sie es also nicht selbst aus? Tauchen Sie ein in diese Excel-Add-Ins und verleihen Sie Ihren Tabellenkalkulationen ein neues Maß an Interaktivität und Funktionalität.
## Häufig gestellte Fragen
### Was ist ein Excel-Add-In?  
Ein Excel-Add-In ist ein Programm, das Excel benutzerdefinierte Features, Funktionen oder Befehle hinzufügt, sodass Benutzer dessen Fähigkeiten erweitern können.
### Kann ich Aspose.Cells verwenden, ohne es lokal zu installieren?  
Nein, Sie müssen die Aspose.Cells-Bibliothek installieren, um sie in Ihren .NET-Anwendungen zu verwenden.
### Wie erhalte ich eine temporäre Lizenz für Aspose.Cells?  
 Besuchen Sie ihre[Seite mit der temporären Lizenz](https://purchase.aspose.com/temporary-license/) für weitere Informationen.
### Ist es möglich, mehrere Funktionen von einem einzigen Add-In aus aufzurufen?  
 Ja! Sie können mehrere Funktionen aus derselben Add-In-Datei registrieren, indem Sie`RegisterAddInFunction` Verfahren.
### Wo finde ich weitere Dokumentation zu Aspose.Cells?  
 Sie können die umfassende Dokumentation auf der Website erkunden.[Hier](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
