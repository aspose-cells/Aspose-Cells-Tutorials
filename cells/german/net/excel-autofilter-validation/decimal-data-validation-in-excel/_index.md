---
title: Dezimaldatenüberprüfung in Excel
linktitle: Dezimaldatenüberprüfung in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie mit unserer leicht verständlichen Anleitung, wie Sie die Dezimaldatenüberprüfung in Excel mit Aspose.Cells für .NET implementieren. Verbessern Sie mühelos die Datenintegrität.
weight: 11
url: /de/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dezimaldatenüberprüfung in Excel

## Einführung

Das Erstellen von Tabellen mit genauen Daten ist für eine klare Kommunikation in jedem Unternehmen unerlässlich. Eine Möglichkeit, die Datengenauigkeit sicherzustellen, ist die Verwendung der Datenüberprüfung in Excel. In diesem Tutorial nutzen wir die Leistungsfähigkeit von Aspose.Cells für .NET, um einen dezimalen Datenüberprüfungsmechanismus zu erstellen, der Ihre Daten zuverlässig und sauber hält. Wenn Sie Ihre Excel-Kenntnisse verbessern möchten, sind Sie hier richtig!

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie alles für ein reibungsloses Erlebnis eingerichtet haben:

1. Visual Studio: Laden Sie Visual Studio herunter und installieren Sie es, falls Sie dies noch nicht getan haben. Es ist die perfekte Umgebung für die Entwicklung von .NET-Anwendungen.
2.  Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells zu Ihrem Projekt hinzufügen. Sie können sie herunterladen über[dieser Link](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wir erklären Ihnen zwar alles Schritt für Schritt, aber wenn Sie über grundlegende Kenntnisse der C#-Programmierung verfügen, werden Sie die Konzepte besser verstehen.
4. .NET Framework: Stellen Sie sicher, dass Sie das erforderliche .NET Framework installiert haben, das mit Aspose.Cells kompatibel ist.
5. Bibliotheken: Verweisen Sie in Ihrem Projekt auf die Bibliothek Aspose.Cells, um Kompilierungsfehler zu vermeiden.

Nachdem wir nun die Grundlagen behandelt haben, stürzen wir uns auf den spannenden Teil: das Codieren.

## Pakete importieren

Zu Beginn müssen Sie die erforderlichen Pakete in Ihre C#-Datei importieren. Dadurch können Sie auf die Funktionen von Aspose.Cells zugreifen.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Indem Sie diese Zeile oben in Ihre Datei einfügen, weisen Sie C# an, nach der Aspose.Cells-Funktionalität zu suchen, mit der Sie Excel-Dateien bearbeiten können.

Nachdem wir nun die Bühne bereitet haben, gehen wir die erforderlichen Schritte durch, um eine Dezimaldatenüberprüfung in einem Excel-Arbeitsblatt zu erstellen.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Bevor Sie Dateien speichern können, müssen Sie sicherstellen, dass Ihr Dokumentverzeichnis richtig eingerichtet ist:

```csharp
string dataDir = "Your Document Directory";
```

 Ersetzen`"Your Document Directory"` durch den Pfad, in dem Sie Ihre Excel-Dateien speichern möchten.

## Schritt 2: Überprüfen Sie, ob ein Verzeichnis vorhanden ist

Dieses Snippet prüft, ob das Verzeichnis existiert und erstellt es, wenn nicht:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Mit diesem Schritt stellen Sie sicher, dass Ihr Arbeitsplatz bereit ist, bevor Sie ein neues Projekt starten. Kein Chaos, kein Stress!

## Schritt 3: Erstellen eines Arbeitsmappenobjekts

Als Nächstes erstellen wir ein neues Arbeitsmappenobjekt, das im Wesentlichen eine Excel-Datei ist:

```csharp
Workbook workbook = new Workbook();
```

Stellen Sie sich eine Arbeitsmappe als leere Leinwand für Ihre Daten vor. Sie hat noch keinen Inhalt, ist aber bereit, ausgemalt zu werden.

## Schritt 4: Erstellen und Zugreifen auf das Arbeitsblatt


Lassen Sie uns nun ein Arbeitsblatt erstellen und auf das erste Blatt in der Arbeitsmappe zugreifen:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

So wie ein Buch mehrere Seiten hat, kann eine Arbeitsmappe mehrere Arbeitsblätter haben. Wir konzentrieren uns derzeit auf das erste.

## Schritt 5: Abrufen der Validierungssammlung

Lassen Sie uns nun die Validierungssammlung aus dem Arbeitsblatt aufrufen, da wir hier unsere Datenvalidierungsregeln verwalten werden:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Dieser Schritt ist vergleichbar mit dem Auschecken des Werkzeugkastens, bevor Sie ein Projekt starten.

## Schritt 6: Definieren Sie den Zellbereich für die Validierung

Wir müssen den Bereich definieren, in dem die Validierung gilt:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Hier legen wir fest, dass die Datenüberprüfung auf eine einzelne Zelle angewendet wird, und zwar auf die erste Zelle im Arbeitsblatt (A1).

## Schritt 7: Validierung erstellen und hinzufügen

Lassen Sie uns unser Validierungsobjekt erstellen und es der Validierungssammlung hinzufügen:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Jetzt haben wir ein Validierungsobjekt, das wir konfigurieren werden, um unsere Dezimalbedingungen durchzusetzen.

## Schritt 8: Legen Sie den Validierungstyp fest

Als Nächstes geben wir die gewünschte Art der Validierung an:

```csharp
validation.Type = ValidationType.Decimal;
```

Indem wir den Typ auf „Dezimal“ festlegen, weisen wir Excel an, in der validierten Zelle Dezimalwerte zu erwarten.

## Schritt 9: Den Operator festlegen

Nun legen wir die Bedingung für zulässige Werte fest. Wir möchten sicherstellen, dass die eingegebenen Daten zwischen zwei Bereichen liegen:

```csharp
validation.Operator = OperatorType.Between;
```

Stellen Sie es sich als das Ziehen einer Grenzlinie vor. Alle Zahlen außerhalb dieses Bereichs werden abgelehnt, sodass Ihre Daten sauber bleiben!

## Schritt 10: Grenzwerte für die Validierung festlegen

Als Nächstes legen wir die Unter- und Obergrenzen für unsere Validierung fest:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Mit diesen Grenzen wird jede Dezimalzahl, egal wie groß oder klein, akzeptiert, solange sie gültig ist!

## Schritt 11: Anpassen der Fehlermeldung

Stellen wir sicher, dass die Benutzer wissen, warum ihre Eingabe abgelehnt wurde, indem wir eine Fehlermeldung hinzufügen:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Dies führt zu einer benutzerfreundlichen Erfahrung, da es Anleitungen für die Eingabe bietet.

## Schritt 12: Definieren Sie den Validierungsbereich

Geben wir nun die Zellen an, die dieser Validierung unterzogen werden:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

In dieser Konfiguration sagen wir, dass die Validierung von Zelle A1 bis A10 gilt.

## Schritt 13: Validierungsbereich hinzufügen

Nachdem wir nun unseren Validierungsbereich definiert haben, wenden wir ihn an:

```csharp
validation.AddArea(area);
```

Ihre Validierung ist nun fest installiert und bereit, alle unangemessenen Eingaben abzufangen!

## Schritt 14: Speichern Sie die Arbeitsmappe

Lassen Sie uns abschließend die Arbeitsmappe mit der Überprüfung der Dezimaldaten speichern:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Und da haben Sie es! Sie haben erfolgreich eine Arbeitsmappe mit Dezimaldatenüberprüfung mit Aspose.Cells für .NET erstellt.

## Abschluss

Die Implementierung der Dezimaldatenüberprüfung in Excel mit Aspose.Cells für .NET ist ein Kinderspiel, wenn Sie diese einfachen Schritte befolgen. Sie stellen nicht nur sicher, dass die Daten sauber und strukturiert bleiben, sondern verbessern auch die allgemeine Datenintegrität in Ihren Tabellenkalkulationen und machen sie zuverlässig und benutzerfreundlich.
Egal, ob Sie im Finanzwesen, im Projektmanagement oder in einem anderen Bereich tätig sind, in dem Datenberichte verwendet werden, die Beherrschung dieser Fähigkeiten wird Ihre Produktivität erheblich steigern. Probieren Sie es also aus! Ihre Tabellenkalkulationen werden es Ihnen danken.

## Häufig gestellte Fragen

### Was ist Datenvalidierung in Excel?
Die Datenüberprüfung in Excel ist eine Funktion, die den Datentyp einschränkt, der in eine bestimmte Zelle oder einen bestimmten Bereich eingegeben werden kann, und so die Datenintegrität sicherstellt.

### Kann ich die Fehlermeldung bei der Datenüberprüfung anpassen?
Ja! Sie können benutzerdefinierte Fehlermeldungen bereitstellen, um Benutzer bei falschen Dateneingaben zu unterstützen.

### Ist die Nutzung von Aspose.Cells kostenlos?
 Aspose.Cells bietet eine kostenlose Testversion an, für die langfristige Nutzung benötigen Sie jedoch eine Lizenz. Weitere Informationen zum Erwerb einer temporären Lizenz finden Sie hier[Hier](https://purchase.aspose.com/temporary-license/).

### Welche Datentypen kann ich in Excel validieren?
Mit Aspose.Cells können Sie verschiedene Datentypen validieren, darunter ganze Zahlen, Dezimalzahlen, Daten, Listen und benutzerdefinierte Formeln.

### Wo finde ich weitere Aspose.Cells-Dokumentation?
 Sie können die umfangreiche Dokumentation erkunden[Hier](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
