---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET bearbeitbare Bereiche in Excel-Arbeitsblättern erstellen, sodass bestimmte Zellen bearbeitet werden können, während der Rest durch Arbeitsblattschutz geschützt wird."
"linktitle": "Erlauben Sie Benutzern, Bereiche im Arbeitsblatt mit Aspose.Cells zu bearbeiten"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Erlauben Sie Benutzern, Bereiche im Arbeitsblatt mit Aspose.Cells zu bearbeiten"
"url": "/de/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Erlauben Sie Benutzern, Bereiche im Arbeitsblatt mit Aspose.Cells zu bearbeiten

## Einführung
Excel-Dokumente enthalten oft vertrauliche Daten oder strukturierte Inhalte, die Sie vor unerwünschten Änderungen schützen möchten. Möglicherweise möchten Sie jedoch bestimmte Zellen oder Bereiche für bestimmte Benutzer bearbeitbar machen. Hier kommt Aspose.Cells für .NET ins Spiel: ein leistungsstarkes Tool, mit dem Sie ein ganzes Arbeitsblatt schützen und gleichzeitig Bearbeitungsberechtigungen für bestimmte Bereiche gewähren können. Stellen Sie sich vor, Sie geben eine Budgettabelle frei, in der nur bestimmte Zellen bearbeitet werden können, während andere geschützt bleiben – Aspose.Cells macht dies einfach und effizient.
## Voraussetzungen
Bevor wir uns in den Codierungsteil stürzen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:
- Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Bibliothek Aspose.Cells für .NET installiert haben. Sie können sie herunterladen [Hier](https://releases.aspose.com/cells/net/).
- Entwicklungsumgebung: Visual Studio oder jede C#-kompatible IDE.
- .NET Framework: Version 4.0 oder höher.
- Lizenz: Erwägen Sie den Erwerb einer Lizenz, um Einschränkungen bei der Testversion zu vermeiden. Sie erhalten eine [vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/).
## Pakete importieren
Stellen Sie sicher, dass Sie den erforderlichen Aspose.Cells-Namespace am Anfang Ihres Codes einfügen:
```csharp
using System.IO;
using Aspose.Cells;
```
Dadurch wird sichergestellt, dass Sie auf alle Klassen und Methoden zugreifen können, die zum Einrichten geschützter Bereiche in Excel-Dateien erforderlich sind.
Nachdem die Grundlagen nun gelegt sind, gehen wir den Code Schritt für Schritt im Detail durch.
## Schritt 1: Einrichten des Verzeichnisses
Bevor Sie mit Dateien arbeiten, müssen Sie das Verzeichnis einrichten, in dem Sie die Excel-Datei speichern. So stellen Sie sicher, dass Ihre Dateien gut organisiert und sicher gespeichert sind.
```csharp
// Definieren Sie den Pfad zu Ihrem Dokumentenverzeichnis
string dataDir = "Your Document Directory";
// Prüfen Sie, ob das Verzeichnis existiert. Wenn nicht, erstellen Sie es
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Dieser Teil des Codes stellt sicher, dass Ihr Verzeichnis für Dateioperationen bereit ist. Betrachten Sie ihn als Grundlage für alles Folgende.
## Schritt 2: Initialisieren der Arbeitsmappe und des Arbeitsblatts
Fahren wir nun fort, indem wir eine neue Arbeitsmappe erstellen und auf ihr Standardarbeitsblatt zugreifen.
```csharp
// Initialisieren einer neuen Arbeitsmappe
Workbook book = new Workbook();
// Greifen Sie auf das erste Arbeitsblatt in der Arbeitsmappe zu
Worksheet sheet = book.Worksheets[0];
```
Hier initialisieren wir eine Excel-Arbeitsmappe und wählen das erste Arbeitsblatt darin aus. Dieses Arbeitsblatt dient als Arbeitsfläche, auf der wir unsere Schutzeinstellungen anwenden und bearbeitbare Bereiche definieren.
## Schritt 3: Zugriff auf die Sammlung „Bereiche bearbeiten zulassen“
Aspose.Cells hat eine Funktion namens `AllowEditRanges`, eine Sammlung von Bereichen, die bearbeitet werden können, auch wenn das Arbeitsblatt geschützt ist.
```csharp
// Zugriff auf die Sammlung „Bereiche bearbeiten zulassen“
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Diese Zeile richtet den Zugriff auf eine spezielle Sammlung editierbarer Bereiche ein. Stellen Sie sich das wie einen „VIP“-Bereich in Ihrem Arbeitsblatt vor, in dem nur bestimmte Bereiche den Schutz umgehen dürfen.
## Schritt 4: Definieren und Erstellen eines geschützten Bereichs
Definieren und erstellen wir nun einen geschützten Bereich in unserem Arbeitsblatt. Wir legen die Start- und Endzellen für diesen Bereich fest.
```csharp
// Definieren einer ProtectedRange-Variable
ProtectedRange protectedRange;
// Fügen Sie der Sammlung einen neuen Bereich mit einem bestimmten Namen und bestimmten Zellenpositionen hinzu
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
In diesem Codeblock:
- `EditableRange` ist der dem Bereich zugewiesene Name.
- Die Zahlen (1, 1, 3, 3) definieren die Bereichskoordinaten, d. h. sie beginnen bei Zelle B2 (Zeile 1, Spalte 1) und reichen bis Zelle D4 (Zeile 3, Spalte 3).
## Schritt 5: Legen Sie ein Kennwort für den geschützten Bereich fest
Für zusätzliche Sicherheit können Sie ein Kennwort für den geschützten Bereich festlegen. Dadurch wird sichergestellt, dass nur autorisierte Benutzer den Bereich bearbeiten können.
```csharp
// Legen Sie ein Passwort für den bearbeitbaren Bereich fest
protectedRange.Password = "123";
```
Hier haben wir ein Passwort hinzugefügt (`"123"`) in den geschützten Bereich. Diese Kennwortanforderung bietet zusätzliche Kontrolle darüber, wer Änderungen vornehmen kann.
## Schritt 6: Schützen Sie das Arbeitsblatt
Nachdem der bearbeitbare Bereich festgelegt wurde, besteht der nächste Schritt darin, das gesamte Arbeitsblatt zu schützen. Diese Schutzeinstellung stellt sicher, dass alle Zellen außerhalb des definierten Bereichs gesperrt und nicht bearbeitbar sind.
```csharp
// Wenden Sie einen Schutz auf das Arbeitsblatt an, sodass alle anderen Zellen nicht mehr bearbeitet werden können.
sheet.Protect(ProtectionType.All);
```
Der `Protect` Die Methode sperrt das gesamte Arbeitsblatt mit Ausnahme der als editierbar definierten Bereiche. Dieser Schritt erstellt im Wesentlichen eine sichere, schreibgeschützte Umgebung mit Zugriff auf bestimmte Zellen nach Bedarf.
## Schritt 7: Speichern der Arbeitsmappe
Der letzte Schritt besteht darin, die Arbeitsmappe zu speichern, damit Ihre Einstellungen angewendet und gespeichert werden.
```csharp
// Speichern Sie die Excel-Datei im angegebenen Verzeichnis
book.Save(dataDir + "protectedrange.out.xls");
```
In diesem Schritt speichern wir unsere Arbeitsmappe als „protectedrange.out.xls“ in dem Verzeichnis, das wir in Schritt 1 eingerichtet haben. Jetzt verfügen Sie über eine voll funktionsfähige, sichere Excel-Datei, in der nur bestimmte Bereiche bearbeitet werden können!
## Abschluss
Aspose.Cells für .NET bietet eine hervorragende Möglichkeit, Schutz und Berechtigungen in Ihren Excel-Dateien zu verwalten. Durch die Erstellung editierbarer Bereiche können Sie Ihre Arbeitsblätter schützen und gleichzeitig den Zugriff auf bestimmte Bereiche ermöglichen. Diese Funktion ist besonders nützlich für kollaborative Dokumente, bei denen nur wenige Zellen zur Bearbeitung geöffnet und andere gesperrt bleiben sollen.
## Häufig gestellte Fragen
### Kann ich einem Arbeitsblatt mehrere bearbeitbare Bereiche hinzufügen?
Ja, Sie können mehrere Bereiche hinzufügen, indem Sie einfach die `allowRanges.Add()` Methode für jeden neuen Bereich.
### Was passiert, wenn ich einen geschützten Bereich später entfernen möchte?
Verwenden Sie die `allowRanges.RemoveAt()` Methode mit dem Index des Bereichs, den Sie entfernen möchten.
### Kann ich für jeden Bereich ein anderes Passwort festlegen?
Absolut. Jeder `ProtectedRange` kann über ein eigenes, eindeutiges Passwort verfügen, das Ihnen eine detaillierte Kontrolle ermöglicht.
### Was passiert, wenn ich das Arbeitsblatt ohne bearbeitbare Bereiche schütze?
Wenn Sie keine bearbeitbaren Bereiche definieren, ist das gesamte Arbeitsblatt nach dem Schutz nicht mehr bearbeitbar.
### Ist der geschützte Bereich für andere Benutzer sichtbar?
Nein, der Schutz ist intern. Benutzer werden nur dann zur Eingabe eines Passworts aufgefordert, wenn sie versuchen, den geschützten Bereich zu bearbeiten.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}