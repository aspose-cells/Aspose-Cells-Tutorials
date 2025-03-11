---
title: Schützen Sie Zellen und Bereiche im Arbeitsblatt mit Aspose.Cells
linktitle: Schützen Sie Zellen und Bereiche im Arbeitsblatt mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie Zellen und Bereiche in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET schützen. Folgen Sie dieser Schritt-für-Schritt-Anleitung, um Ihre Tabellen zu sichern.
weight: 11
url: /de/net/worksheet-security/protect-cells-and-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schützen Sie Zellen und Bereiche im Arbeitsblatt mit Aspose.Cells

## Einführung
Beim Arbeiten mit Tabellenkalkulationen müssen oft bestimmte Teile des Blattes vor unerwünschten Änderungen geschützt werden, insbesondere in kollaborativen Umgebungen. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET bestimmte Zellen und Bereiche in einem Arbeitsblatt schützen können. Wir führen Sie durch den Prozess des Einrichtens eines geschützten Blattes, geben an, welche Bereiche bearbeitet werden können, und speichern die Datei. Dies kann eine äußerst nützliche Funktion sein, wenn Sie den Zugriff auf vertrauliche Daten einschränken und gleichzeitig zulassen möchten, dass bestimmte Abschnitte von anderen geändert werden.
## Voraussetzungen
Bevor Sie mit dem Lernprogramm beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek in Ihrem Projekt installiert haben. Wenn Sie dies noch nicht getan haben, können Sie sie von der[Aspose-Website](https://releases.aspose.com/cells/net/).
2. Visual Studio: Diese Anleitung setzt voraus, dass Sie Visual Studio oder eine ähnliche IDE verwenden, die die C#-Entwicklung unterstützt.
3. Grundkenntnisse in C#: Sie sollten mit den Grundlagen der C#-Programmierung und dem Einrichten eines Projekts in Visual Studio vertraut sein.
4.  Aspose.Cells-Lizenz: Obwohl Aspose eine kostenlose Testversion anbietet, können Sie mit einer gültigen Lizenz den gesamten Funktionsumfang der Bibliothek nutzen. Wenn Sie keine haben, können Sie eine[vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/).
Sobald Sie sichergestellt haben, dass Sie alles oben genannte bereit haben, können wir mit dem Codierungsteil fortfahren.
## Pakete importieren
Um mit Aspose.Cells arbeiten zu können, müssen Sie zunächst die erforderlichen Namespaces in Ihre C#-Datei importieren. So können Sie sie importieren:
```csharp
using System.IO;
using Aspose.Cells;
```
 Der`Aspose.Cells` Namespace gibt Ihnen Zugriff auf die Kernfunktionen zur Bearbeitung von Excel-Dateien und`System.IO` wird für Dateioperationen wie das Speichern der Arbeitsmappe verwendet.
Lassen Sie uns nun die Schritte zum Schützen von Zellen und Bereichen in einem Arbeitsblatt mit Aspose.Cells aufschlüsseln.
## Schritt 1: Richten Sie Ihre Umgebung ein
Erstellen Sie zunächst ein Verzeichnis, in dem Sie Ihre Excel-Dateien speichern möchten. Wenn das Verzeichnis noch nicht vorhanden ist, erstellen wir eines. So stellen Sie sicher, dass Sie einen Ort zum Speichern Ihrer Ausgabedatei haben.
```csharp
// Definieren Sie den Pfad zu Ihrem Dokumentverzeichnis
string dataDir = "Your Document Directory";
// Überprüfen Sie, ob das Verzeichnis existiert. Wenn nicht, erstellen Sie es
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
 Hier verwenden wir`System.IO.Directory.Exists()` um zu prüfen, ob der Ordner existiert, und wenn nicht, erstellen wir ihn mit`Directory.CreateDirectory()`.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe
Lassen Sie uns nun ein neues Workbook-Objekt instanziieren. Dies dient als unsere Excel-Datei, in der wir unsere Zellen und Bereiche definieren.
```csharp
// Instanziieren eines neuen Workbook-Objekts
Workbook book = new Workbook();
```
 Der`Workbook` Klasse ist der Einstiegspunkt für die Arbeit mit Excel-Dateien in Aspose.Cells. Sie stellt das Excel-Dokument dar.
## Schritt 3: Zugriff auf das Standardarbeitsblatt
Jede neu erstellte Arbeitsmappe verfügt über ein Standardarbeitsblatt. Wir rufen es ab, um mit seinem Inhalt zu arbeiten.
```csharp
// Holen Sie sich das erste (Standard-)Arbeitsblatt in der Arbeitsmappe
Worksheet sheet = book.Worksheets[0];
```
 Hier,`Worksheets[0]` gibt uns das erste Blatt in der Arbeitsmappe (die Indizierung beginnt bei 0).
## Schritt 4: Editierbare Bereiche definieren
Um bestimmte Teile des Arbeitsblatts zu schützen und Benutzern gleichzeitig das Bearbeiten bestimmter Zellen zu ermöglichen, müssen wir bearbeitbare Bereiche definieren. Wir erstellen einen bearbeitbaren Bereich und fügen ihn der AllowEditRanges-Sammlung des Arbeitsblatts hinzu.
```csharp
// Abrufen der AllowEditRanges-Sammlung
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// Definieren Sie einen ProtectedRange und fügen Sie ihn der Sammlung hinzu
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
Im obigen Code:
- `"r2"` ist der Name des bearbeitbaren Bereichs.
-  Die Zahlen`1, 1, 3, 3` stellen die Start- und Endzeilen- und Spaltenindizes für den Bereich dar (d. h. von Zelle B2 bis D4).
## Schritt 5: Legen Sie ein Passwort für den geschützten Bereich fest
Nachdem wir nun den bearbeitbaren Bereich definiert haben, fügen wir ein Kennwort hinzu, um ihn zu schützen. Dies bedeutet, dass Benutzer das Kennwort benötigen, um diesen bestimmten Bereich zu bearbeiten.
```csharp
// Geben Sie das Passwort für den editierbaren Bereich an
protectedRange.Password = "123";
```
 Hier haben wir das Passwort wie folgt festgelegt:`"123"`, Sie können jedoch ein beliebiges sicheres Passwort wählen. Dieser Schritt ist für die Zugriffskontrolle auf die bearbeitbaren Bereiche unerlässlich.
## Schritt 6: Schützen Sie das gesamte Blatt
In diesem Schritt schützen wir das gesamte Arbeitsblatt. Durch den Schutz des Arbeitsblatts wird sichergestellt, dass andere Teile des Blatts, mit Ausnahme der zulässigen Bereiche, nicht bearbeitet werden können.
```csharp
// Schützen Sie das Blatt mit dem angegebenen Schutztyp (Alle)
sheet.Protect(ProtectionType.All);
```
Dadurch wird sichergestellt, dass alle Zellen im Blatt gesperrt sind, mit Ausnahme der Zellen in den bearbeitbaren Bereichen.
## Schritt 7: Speichern Sie die Arbeitsmappe
Zum Schluss speichern wir die Arbeitsmappe in einer Datei. Das geschützte Blatt wird unter dem von Ihnen angegebenen Namen gespeichert.
```csharp
// Speichern Sie die Excel-Datei im angegebenen Verzeichnis
book.Save(dataDir + "protectedrange.out.xls");
```
 Hier wird die Excel-Datei gespeichert als`protectedrange.out.xls` in dem Verzeichnis, das wir zuvor definiert haben. Wenn Sie es unter einem anderen Namen oder in einem anderen Format speichern möchten, können Sie den Dateinamen und die Erweiterung ändern.
## Abschluss
In diesem Tutorial haben Sie gelernt, wie Sie Zellen und Bereiche in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET schützen. Mit diesem Ansatz können Sie flexibel steuern, welche Bereiche Ihrer Tabelle bearbeitet werden können und welche nicht. Sie können diese Fähigkeiten nun in Ihren eigenen Projekten anwenden und so sicherstellen, dass Ihre vertraulichen Daten geschützt bleiben, während Sie den Benutzern bearbeitbare Bereiche zur Verfügung stellen.
Denken Sie daran, dass Aspose.Cells einen robusten Satz an Tools für die Arbeit mit Excel-Dateien bietet und dies nur eines der vielen Dinge ist, die Sie damit tun können. 
## Häufig gestellte Fragen
### Kann ich nur bestimmte Zellen in einem Arbeitsblatt schützen?
 Ja, mit dem`AllowEditRanges` können Sie angeben, welche Zellen oder Bereiche bearbeitet werden können, während der Rest des Arbeitsblatts geschützt bleibt.
### Kann ich den Schutz nachträglich wieder entfernen?
 Ja, Sie können den Schutz eines Arbeitsblatts aufheben, indem Sie`Unprotect()` Methode. Wenn ein Kennwort festgelegt wurde, müssen Sie es eingeben.
### Wie schütze ich ein ganzes Blatt mit einem Passwort?
 Zum Schutz des gesamten Blattes verwenden Sie einfach die`Protect()` Methode mit oder ohne Passwort. Beispiel:`sheet.Protect("password")`.
### Kann ich mehrere bearbeitbare Bereiche hinzufügen?
 Absolut! Sie können so viele editierbare Bereiche hinzufügen, wie Sie benötigen, indem Sie`allowRanges.Add()` mehrmals.
### Welche anderen Sicherheitsfunktionen bietet Aspose.Cells?
Aspose.Cells unterstützt verschiedene Sicherheitsfunktionen wie Arbeitsmappenverschlüsselung, Festlegen von Dateikennwörtern und Schutz von Zellen und Blättern.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
