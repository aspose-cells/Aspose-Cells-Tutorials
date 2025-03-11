---
title: Schützen Sie bestimmte Zellen im Arbeitsblatt mit Aspose.Cells
linktitle: Schützen Sie bestimmte Zellen im Arbeitsblatt mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET bestimmte Zellen in einem Excel-Arbeitsblatt schützen. Sichern Sie vertrauliche Daten und verhindern Sie versehentliche Änderungen in nur wenigen Schritten.
weight: 14
url: /de/net/worksheet-security/protect-specific-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schützen Sie bestimmte Zellen im Arbeitsblatt mit Aspose.Cells

## Einführung
In diesem Tutorial führen wir Sie durch den Prozess zum Schützen bestimmter Zellen in einem Excel-Arbeitsblatt. Am Ende können Sie Zellen sicher wie ein Profi sperren, unbefugte Änderungen verhindern und gleichzeitig Ihr Arbeitsblatt bei Bedarf flexibel halten.
## Voraussetzungen
Bevor wir in die Details eintauchen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial problemlos folgen zu können:
1. Visual Studio – Falls noch nicht geschehen, laden Sie Visual Studio herunter und installieren Sie es. Es wird die primäre Umgebung sein, in der Sie Ihre .NET-Anwendungen ausführen.
2.  Aspose.Cells für .NET – Sie benötigen die Aspose.Cells-Bibliothek, um mit Excel-Dateien in Ihren .NET-Anwendungen zu arbeiten. Wenn Sie sie noch nicht installiert haben, können Sie die neueste Version von der[Aspose-Website](https://releases.aspose.com/cells/net/).
3. .NET Framework oder .NET Core – Dieses Tutorial funktioniert sowohl mit .NET Framework als auch mit .NET Core. Stellen Sie einfach sicher, dass Ihr Projekt mit Aspose.Cells kompatibel ist.
Sobald Sie diese eingerichtet haben, können Sie loslegen.
## Pakete importieren
Bevor Sie mit der Schritt-für-Schritt-Anleitung beginnen, müssen Sie sicherstellen, dass Sie die erforderlichen Namespaces für die Arbeit mit Aspose.Cells importieren. Fügen Sie in Ihrem Projekt die folgenden Importanweisungen oben in die Datei ein:
```csharp
using System.IO;
using Aspose.Cells;
```
Diese Namespaces ermöglichen Ihnen die Interaktion mit Excel-Dateien und den Klassen, die zum Formatieren und Schützen der Arbeitsblattzellen erforderlich sind.
Lassen Sie uns nun in einfache Schritte unterteilen, um bestimmte Zellen in Ihrem Arbeitsblatt mit Aspose.Cells für .NET zu schützen. Wir schützen die Zellen A1, B1 und C1 und lassen den Rest des Arbeitsblatts für Änderungen geöffnet.
## Schritt 1: Erstellen Sie eine neue Arbeitsmappe und ein neues Arbeitsblatt
Als Erstes müssen Sie eine neue Arbeitsmappe (Excel-Datei) und ein Arbeitsblatt darin erstellen. Hier wenden Sie Ihren Zellschutz an.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
// Erstellen Sie eine neue Arbeitsmappe.
Workbook wb = new Workbook();
// Erstellen Sie ein Arbeitsblattobjekt und rufen Sie das erste Blatt ab.
Worksheet sheet = wb.Worksheets[0];
```
 In diesem Schritt erstellen Sie auch ein Verzeichnis zum Speichern der resultierenden Excel-Datei, falls diese noch nicht vorhanden ist.`Workbook` Klasse initialisiert eine neue Excel-Datei und`Worksheets[0]` ermöglicht es uns, mit dem ersten Blatt im Arbeitsbuch zu arbeiten.
## Schritt 2: Alle Spalten entsperren
Als Nächstes entsperren Sie alle Spalten im Arbeitsblatt. Dadurch wird sichergestellt, dass standardmäßig alle Zellen im Arbeitsblatt bearbeitet werden können. Wir werden später nur die Zellen sperren, die wir schützen möchten.
```csharp
// Definieren Sie das Stilobjekt.
Style style;
// Definieren Sie das Styleflag-Objekt
StyleFlag styleflag;
// Durchlaufen Sie alle Spalten im Arbeitsblatt und entsperren Sie sie.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
 In diesem Codeblock durchlaufen wir alle Spalten (bis zu 255) und setzen die`IsLocked` Eigentum an`false` Dadurch werden im Wesentlichen alle Zellen in diesen Spalten entsperrt und sie sind standardmäßig bearbeitbar. Anschließend wenden wir den Stil auf die Spalte mit dem`ApplyStyle()` Verfahren.
## Schritt 3: Bestimmte Zellen sperren (A1, B1, C1)
 Nachdem nun alle Spalten entsperrt sind, konzentrieren wir uns auf das Sperren bestimmter Zellen, nämlich A1, B1 und C1. Wir ändern die Zellstile und legen ihre`IsLocked` Eigentum an`true`.
```csharp
// Sperren Sie die drei Zellen, also A1, B1, C1.
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
Dieser Schritt stellt sicher, dass die Zellen A1, B1 und C1 gesperrt sind. Dies sind die Zellen, die geschützt werden und nicht mehr bearbeitet werden können, sobald der Arbeitsblattschutz angewendet wird.
## Schritt 4: Schützen Sie das Arbeitsblatt
Nachdem die erforderlichen Zellen gesperrt wurden, besteht der nächste Schritt darin, das gesamte Arbeitsblatt zu schützen. Dieser Schritt macht die gesperrten Zellen (A1, B1, C1) unveränderbar, während andere Zellen für Änderungen geöffnet bleiben.
```csharp
// Schützen Sie nun abschließend das Blatt.
sheet.Protect(ProtectionType.All);
```
 Der`Protect` Methode wird auf dem Arbeitsblatt aufgerufen und gibt an, dass alle Aspekte des Blattes geschützt werden sollen. Dadurch werden die spezifischen Zellen gesperrt, die mit`IsLocked = true` und stellt sicher, dass sie nicht von Benutzern geändert werden können.
## Schritt 5: Speichern der Arbeitsmappe
Sobald die Zellen gesperrt und das Blatt geschützt sind, können Sie die Arbeitsmappe am gewünschten Speicherort speichern.
```csharp
// Speichern Sie die Excel-Datei.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Dieser Schritt speichert die Arbeitsmappe im`dataDir` Ordner mit dem Dateinamen`output.out.xls`. Sie können den Dateinamen und das Verzeichnis Ihren Bedürfnissen entsprechend ändern. Die Datei wird im Excel 97-2003-Format gespeichert, Sie können dies jedoch Ihren Anforderungen entsprechend anpassen.
## Abschluss
Das Schützen bestimmter Zellen in Ihrem Excel-Arbeitsblatt mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang. Indem Sie die oben genannten Schritte befolgen, können Sie bestimmte Zellen sperren, während andere weiterhin bearbeitet werden können. Diese Funktion ist äußerst nützlich, wenn Sie Arbeitsmappen mit anderen teilen, da Sie damit steuern können, welche Daten geändert werden können und welche geschützt bleiben sollen. Egal, ob Sie mit vertraulichen Daten arbeiten oder einfach nur versehentliche Änderungen verhindern möchten, Aspose.Cells bietet eine flexible und leistungsstarke Lösung.
## Häufig gestellte Fragen
### Wie kann ich einen bestimmten Zellbereich statt nur einige wenige schützen?
Sie können den Code so ändern, dass er einen bestimmten Zell- oder Spaltenbereich durchläuft und sperrt, anstatt einzelne Zellen manuell zu sperren.
### Kann ich zum Schutz des Arbeitsblatts Passwörter hinzufügen?
Ja, Sie können beim Anrufen ein Passwort angeben.`Protect()` Methode, um zu verhindern, dass Benutzer den Blattschutz ohne das richtige Kennwort aufheben.
### Kann ich statt Zellen bestimmte Zeilen oder Spalten schützen?
 Ja, Aspose.Cells ermöglicht es Ihnen, ganze Zeilen oder Spalten zu sperren, indem Sie die`IsLocked` -Eigenschaft für die Zeilen oder Spalten, ähnlich wie wir Zellen gesperrt haben.
### Wie kann ich den Schutz eines Arbeitsblatts aufheben?
 Um den Schutz eines Arbeitsblatts aufzuheben, verwenden Sie die`Unprotect()` Methode, optional mit Angabe des Kennworts, falls während des Schutzes eines festgelegt wurde.
### Kann ich Aspose.Cells für andere Excel-Manipulationen verwenden, beispielsweise zum Hinzufügen von Formeln oder Diagrammen?
Auf jeden Fall! Aspose.Cells ist eine robuste Bibliothek, mit der Sie eine Vielzahl von Excel-Operationen durchführen können, darunter das Hinzufügen von Formeln, das Erstellen von Diagrammen und vieles mehr.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
