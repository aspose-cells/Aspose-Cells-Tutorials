---
title: Digitale Signatur zur signierten Excel-Datei hinzufügen
linktitle: Digitale Signatur zur signierten Excel-Datei hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen. Sichern Sie Ihre Dokumente.
weight: 12
url: /de/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Digitale Signatur zur signierten Excel-Datei hinzufügen

## Einführung
In der heutigen digitalen Welt ist die Gewährleistung der Authentizität und Integrität von Dokumenten von entscheidender Bedeutung. Digitale Signaturen dienen als zuverlässiges Mittel zur Überprüfung, dass ein Dokument nicht verändert wurde und aus einer legitimen Quelle stammt. Wenn Sie mit Excel-Dateien in .NET arbeiten und einer bereits signierten Datei eine digitale Signatur hinzufügen möchten, sind Sie hier richtig! In diesem Handbuch führen wir Sie durch den Prozess des Hinzufügens einer neuen digitalen Signatur zu einer vorhandenen signierten Excel-Datei mit Aspose.Cells für .NET. 
## Voraussetzungen
Bevor wir ins Detail gehen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg benötigen:
1.  Aspose.Cells für .NET: Zunächst einmal müssen Sie Aspose.Cells in Ihrer .NET-Umgebung installiert haben. Sie können es herunterladen von der[Veröffentlichungsseite](https://releases.aspose.com/cells/net/).
2. .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist. Diese Anleitung setzt voraus, dass Sie mit den grundlegenden Konzepten der .NET-Programmierung vertraut sind.
3. Digitales Zertifikat: Sie benötigen ein gültiges digitales Zertifikat (im PFX-Format), um eine digitale Signatur zu erstellen. Wenn Sie keins haben, können Sie zu Testzwecken ein selbstsigniertes Zertifikat erstellen.
4. Entwicklungsumgebung: Ein Code-Editor oder eine IDE wie Visual Studio, in der Sie Ihren C#-Code schreiben und ausführen können.
5. Beispiel einer Excel-Datei: Sie sollten über eine vorhandene Excel-Datei verfügen, die bereits digital signiert ist. Dies ist die Datei, der wir eine weitere Signatur hinzufügen.
Nachdem diese Voraussetzungen erfüllt sind, können wir uns nun an den Code machen!
## Pakete importieren
Bevor Sie mit dem Codieren beginnen, stellen Sie sicher, dass Sie die erforderlichen Namespaces importieren. Folgendes müssen Sie oben in Ihre C#-Datei einfügen:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Über diese Namespaces erhalten Sie Zugriff auf die Klassen und Methoden, die zum Bearbeiten von Excel-Dateien und Verarbeiten digitaler Signaturen erforderlich sind.
Lassen Sie uns den Vorgang nun in überschaubare Schritte unterteilen. Wir gehen jeden Schritt durch, um sicherzustellen, dass Sie verstehen, wie Sie einer bereits signierten Excel-Datei eine digitale Signatur hinzufügen.
## Schritt 1: Definieren Sie Ihre Verzeichnisse
Zuerst müssen Sie angeben, wo sich Ihre Quelldateien befinden und wo die Ausgabedatei gespeichert werden soll. Das ist unkompliziert, aber entscheidend:
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory"; // Ersetzen Sie es durch Ihr aktuelles Verzeichnis
// Ausgabeverzeichnis
string outputDir = "Your Document Directory"; // Ersetzen Sie es durch Ihr aktuelles Verzeichnis
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad, in dem Ihre Dateien gespeichert sind. Dies legt die Grundlage für Ihre Dateivorgänge.
## Schritt 2: Laden Sie die vorhandene signierte Arbeitsmappe
Als Nächstes laden Sie die vorhandene, bereits signierte Excel-Arbeitsmappe. Hier beginnt die Magie:
```csharp
// Laden Sie die Arbeitsmappe, die bereits digital signiert ist, um eine neue digitale Signatur hinzuzufügen
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 Diese Zeile initialisiert eine neue`Workbook` Objekt mit der angegebenen Datei. Stellen Sie sicher, dass der Dateiname mit Ihrer vorhandenen signierten Excel-Datei übereinstimmt.
## Schritt 3: Erstellen Sie eine digitale Signaturensammlung
Um Ihre digitalen Signaturen zu verwalten, müssen Sie eine Sammlung erstellen. So können Sie bei Bedarf mehrere Signaturen speichern:
```csharp
// Erstellen der digitalen Signaturensammlung
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
In dieser Sammlung fügen Sie Ihre neue digitale Signatur hinzu, bevor Sie sie auf die Arbeitsmappe anwenden.
## Schritt 4: Laden Sie Ihr Zertifikat hoch
Jetzt ist es an der Zeit, Ihr digitales Zertifikat zu laden. Dieses Zertifikat wird zum Erstellen der neuen Signatur verwendet:
```csharp
// Zertifikatsdatei und ihr Passwort
string certFileName = sourceDir + "AsposeDemo.pfx"; // Ihre Zertifikatsdatei
string password = "aspose"; //Ihr Zertifikatspasswort
// Neues Zertifikat erstellen
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 Ersetzen Sie unbedingt`AsposeDemo.pfx` durch den Namen Ihrer Zertifikatsdatei und aktualisieren Sie das Passwort entsprechend. Dieser Schritt ist wichtig, da Sie ohne das richtige Zertifikat keine gültige Signatur erstellen können.
## Schritt 5: Erstellen Sie eine neue digitale Signatur
Nachdem Sie Ihr Zertifikat geladen haben, können Sie nun eine neue digitale Signatur erstellen. Diese Signatur wird Ihrer Sammlung hinzugefügt:
```csharp
// Neue digitale Signatur erstellen und zur Sammlung digitaler Signaturen hinzufügen
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
Hier geben Sie eine Nachricht ein, die die Signatur beschreibt. Dies kann bei der Dokumentation hilfreich sein. Der Zeitstempel stellt sicher, dass die Signatur dem richtigen Zeitpunkt zugeordnet wird.
## Schritt 6: Hinzufügen der Signatursammlung zur Arbeitsmappe
Nachdem Sie die Signatur erstellt haben, ist es an der Zeit, die gesamte Sammlung zur Arbeitsmappe hinzuzufügen:
```csharp
// Fügen Sie der Arbeitsmappe eine Sammlung digitaler Signaturen hinzu
workbook.AddDigitalSignature(dsCollection);
```
Mit diesem Schritt wenden Sie Ihre neue digitale Signatur effektiv auf die Arbeitsmappe an und verleihen ihr zusätzliche Authentizität.
## Schritt 7: Speichern Sie die Arbeitsmappe
Speichern Sie abschließend die Arbeitsmappe mit der neuen digitalen Signatur. Dies ist der Moment, in dem sich all Ihre harte Arbeit auszahlt:
```csharp
//Speichern und entsorgen Sie die Arbeitsmappe.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
Geben Sie Ihrer Ausgabedatei unbedingt einen Namen. Dies ist die neue Version Ihrer Excel-Datei, komplett mit der zusätzlichen digitalen Signatur.
## Schritt 8: Erfolg bestätigen
Abschließend empfiehlt es sich, nach erfolgreichem Abschluss des Vorgangs Feedback zu geben:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
Diese Zeile druckt eine Bestätigungsmeldung auf der Konsole und informiert Sie, dass alles reibungslos verlaufen ist.
## Abschluss
Und da haben Sie es! Sie haben einer bereits signierten Excel-Datei mit Aspose.Cells für .NET erfolgreich eine neue digitale Signatur hinzugefügt. Dieser Vorgang erhöht nicht nur die Sicherheit Ihrer Dokumente, sondern stellt auch sicher, dass sie vertrauenswürdig und überprüfbar sind. 
Digitale Signaturen sind in der heutigen digitalen Landschaft unverzichtbar, insbesondere für Unternehmen und Fachleute, die die Integrität ihrer Dokumente wahren müssen. Mit dieser Anleitung können Sie digitale Signaturen in Ihren Excel-Dateien problemlos verwalten und so sicherstellen, dass Ihre Daten sicher und authentisch bleiben.
## Häufig gestellte Fragen
### Was ist eine digitale Signatur?
Eine digitale Signatur ist ein mathematisches Verfahren zur Überprüfung der Authentizität und Integrität digitaler Nachrichten oder Dokumente. Sie stellt sicher, dass das Dokument nicht verändert wurde und bestätigt die Identität des Unterzeichners.
### Benötige ich zum Erstellen einer digitalen Signatur ein spezielles Zertifikat?
Ja, Sie benötigen ein digitales Zertifikat, das von einer vertrauenswürdigen Zertifizierungsstelle (CA) ausgestellt wurde, um eine gültige digitale Signatur zu erstellen.
### Kann ich zum Testen ein selbstsigniertes Zertifikat verwenden?
Auf jeden Fall! Sie können für Entwicklungs- und Testzwecke ein selbstsigniertes Zertifikat erstellen, für die Produktion ist es jedoch am besten, ein Zertifikat einer vertrauenswürdigen Zertifizierungsstelle zu verwenden.
### Was passiert, wenn ich versuche, einem nicht signierten Dokument eine Signatur hinzuzufügen?
Der Versuch, einem noch nicht signierten Dokument eine digitale Signatur hinzuzufügen, funktioniert zwar problemlos, die Originalsignatur ist jedoch nicht vorhanden.
### Wo finde ich weitere Informationen zu Aspose.Cells?
 Sie können die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für ausführliche Anleitungen und API-Referenzen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
