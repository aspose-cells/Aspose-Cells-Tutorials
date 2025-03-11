---
title: Bild in Kopf- und Fußzeile des Arbeitsblatts einfügen
linktitle: Bild in Kopf- und Fußzeile des Arbeitsblatts einfügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden Handbuch, wie Sie mit Aspose.Cells für .NET ganz einfach ein Bild in Kopf-/Fußzeilen einfügen.
weight: 15
url: /de/net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild in Kopf- und Fußzeile des Arbeitsblatts einfügen

## Einführung
Wenn es darum geht, professionell aussehende Excel-Tabellen zu erstellen, können kleine Details einen großen Unterschied machen. Ein solches Detail ist das Hinzufügen von Bildern zur Kopf- oder Fußzeile Ihrer Arbeitsblätter. Dies ist eine todsichere Möglichkeit, Ihre Dokumente zu branden und ihnen einen Hauch von Professionalität zu verleihen. Dies mag zwar kompliziert klingen, insbesondere wenn Sie kein Technikfreak sind, aber die Verwendung von Aspose.Cells für .NET vereinfacht den Vorgang erheblich. Lassen Sie uns also eintauchen und lernen, wie Sie dies Schritt für Schritt erledigen können!
## Voraussetzungen
Bevor Sie mit dem Einfügen von Bildern in Kopf- und Fußzeilenabschnitte beginnen, stellen Sie sicher, dass einige Dinge bereit sind:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Diese IDE ist ein Kraftpaket für die .NET-Entwicklung.
2.  Aspose.Cells für .NET: Sie können eine kostenlose Testversion erhalten oder es kaufen, wenn Sie Ihre Excel-Fähigkeiten wirklich maximieren möchten. Laden Sie es herunter[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Grundlegende Kenntnisse in C# und der Ausführung einer .NET-Anwendung sind von Vorteil.
4. Bilddatei: Bereiten Sie eine Bilddatei wie ein Firmenlogo vor. In diesem Beispiel nennen wir es`aspose-logo.jpg`.
## Pakete importieren
Um mit dem Programmieren zu beginnen, stellen Sie sicher, dass Sie die erforderlichen Pakete in Ihr C#-Projekt importiert haben. Sie benötigen den Aspose.Cells-Namespace, der alle Klassen und Methoden enthält, mit denen Sie arbeiten werden.
So fügen Sie es in Ihren Code ein:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nachdem wir nun alles eingerichtet haben, gehen wir den Vorgang in leicht verständlichen Schritten durch.
## Schritt 1: Richten Sie Ihr Verzeichnis ein
Legen Sie fest, wo Ihre Dateien gespeichert werden.
 Zunächst müssen wir den Pfad zu unserem Dokumentenverzeichnis angeben, in dem sich die Excel-Datei und das Bild befinden. Sie können jeden beliebigen Pfad angeben. Ersetzen Sie einfach`"Your Document Directory"` durch Ihren tatsächlichen Verzeichnispfad.
```csharp
string dataDir = "Your Document Directory";
```
## Schritt 2: Erstellen eines Arbeitsmappenobjekts
Erstellen Sie eine Instanz Ihrer Excel-Arbeitsmappe.
Nachdem der Pfad festgelegt ist, müssen wir nun eine neue Instanz eines Arbeitsblatts erstellen, in das wir unser Bild einfügen. 
```csharp
Workbook workbook = new Workbook();
```
## Schritt 3: Laden Sie Ihr Bild
Öffnen und lesen Sie die Bilddatei und konvertieren Sie sie zur Verarbeitung in ein Byte-Array.
Als nächstes legen wir den Pfad für unser Bild (in diesem Fall das Logo) fest und initialisieren ein`FileStream` Objekt, um das Bild zu lesen. So geht's:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarieren eines FileStream-Objekts
FileStream inFile;
byte[] binaryData;
// Erstellen der Instanz des FileStream-Objekts
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Schritt 4: Lesen Sie das Bild in ein Byte-Array
Konvertieren Sie die Bilddateidaten in ein Byte-Array.
Um mit dem Bild arbeiten zu können, müssen wir es in ein Byte-Array einlesen. Dies ist wichtig, da wir so das Bild innerhalb der Anwendung bearbeiten können.
```csharp
// Instanziieren des Byte-Arrays der Größe des FileStream-Objekts
binaryData = new byte[inFile.Length];
// Liest einen Byteblock aus dem Stream und schreibt Daten in einen angegebenen Puffer eines Byte-Arrays.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Schritt 5: Seiteneinrichtung für Kopf-/Fußzeile konfigurieren
Greifen Sie auf das PageSetup-Objekt zu, um die Kopf- und Fußzeilenabschnitte zu bearbeiten.
Um unser Bild einzufügen, müssen wir das Seiteneinrichtungsobjekt konfigurieren. Dadurch können wir die Kopfzeile unseres Arbeitsblatts anpassen:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Schritt 6: Fügen Sie das Logo in die Kopfzeile ein
Betten Sie das Bild in den Kopfbereich des Arbeitsblatts ein.
Das ist der magische Moment! Wir fügen unser Logo in den zentralen Bereich der Kopfzeile ein:
```csharp
// Platzieren Sie das Logo/Bild im mittleren Bereich des Seitenkopfes.
pageSetup.SetHeaderPicture(1, binaryData);
// Legen Sie das Skript für das Logo/Bild fest
pageSetup.SetHeader(1, "&G");
// Setzen Sie den Namen des Blattes im rechten Abschnitt des Seitenkopfes mit dem Skript
pageSetup.SetHeader(2, "&A");
```
## Schritt 7: Speichern Sie Ihre Arbeitsmappe
Speichern Sie Ihre Änderungen in einer neuen Excel-Datei.
Nachdem wir alles konfiguriert haben, können wir unsere Arbeitsmappe speichern. Geben Sie Ihrer Ausgabedatei unbedingt einen neuen Namen:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Schritt 8: Ressourcen bereinigen
Schließen Sie den FileStream, um Ressourcen freizugeben.
 Vergessen Sie nach all den Manipulationen nicht, aufzuräumen, indem Sie Ihre`FileStream`!
```csharp
inFile.Close();
```
## Abschluss
Und da haben Sie es! Sie haben erfolgreich ein Bild in die Kopf-/Fußzeile eines Excel-Arbeitsblatts eingefügt, indem Sie Aspose.Cells für .NET verwendet haben. Es ist ganz einfach, oder? Sobald Sie die Schritte verstanden haben, können Sie es weiter an Ihre spezifischen Anforderungen anpassen. Egal, ob Sie Berichte für Ihr Unternehmen mit Ihrem Markenzeichen versehen oder einfach eine persönliche Note hinzufügen möchten, diese Technik ist unglaublich nützlich. 
## Häufig gestellte Fragen
### Kann ich jedes beliebige Bildformat verwenden?
Ja, Aspose.Cells unterstützt verschiedene Bildformate, darunter JPEG, PNG und BMP für Kopf- und Fußzeilenbilder.
### Ist die Nutzung von Aspose.Cells kostenlos?
 Aspose.Cells bietet eine kostenlose Testversion an, für die weitere Nutzung müssen Sie jedoch eine Lizenz erwerben. Erfahren Sie mehr über die Preise[Hier](https://purchase.aspose.com/buy).
### Wie greife ich auf die Aspose.Cells-Dokumentation zu?
 Sie können tief in die Features und Funktionen von Aspose.Cells eintauchen, indem Sie die[Dokumentation](https://reference.aspose.com/cells/net/).
### Kann ich Aspose.Cells ohne Visual Studio verwenden?
Ja, solange Sie über die .NET-Laufzeitumgebung verfügen, können Sie Aspose.Cells in jeder .NET-kompatiblen Entwicklungsumgebung verwenden.
### Was soll ich tun, wenn ich auf Probleme stoße?
 Wenn Sie auf Probleme stoßen oder Unterstützung benötigen, überprüfen Sie die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9) für Hilfe von der Community und den Entwicklern.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
