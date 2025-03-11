---
title: Unterstützung benannter Bereichsformeln im deutschen Gebietsschema
linktitle: Unterstützung benannter Bereichsformeln im deutschen Gebietsschema
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie, wie Sie mit Aspose.Cells für .NET mit benannten Bereichsformeln im deutschen Gebietsschema umgehen. Erfahren Sie, wie Sie Excel-Dateien programmgesteuert erstellen, bearbeiten und speichern.
weight: 14
url: /de/net/workbook-settings/support-named-range-formulas-in-german/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Unterstützung benannter Bereichsformeln im deutschen Gebietsschema

## Einführung
In diesem Tutorial erfahren Sie, wie Sie mit benannten Bereichsformeln in der deutschen Sprache mithilfe der Aspose.Cells-Bibliothek für .NET arbeiten. Aspose.Cells ist eine leistungsstarke API zur Tabellenkalkulationsbearbeitung, mit der Sie Excel-Dateien programmgesteuert erstellen, lesen und ändern können. Wir führen Sie Schritt für Schritt durch den Prozess und behandeln verschiedene Aspekte der Arbeit mit benannten Bereichen und Formeln in einer deutschen Sprache.
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1.  Visual Studio: Sie müssen Microsoft Visual Studio auf Ihrem System installiert haben. Sie können die neueste Version von Visual Studio von der[Webseite](https://visualstudio.microsoft.com/downloads/).
2.  Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells für .NET in Ihrem Projekt installiert haben. Sie können die neueste Version der Bibliothek von der[Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/).
3. C#-Kenntnisse: Da wir mit C#-Code arbeiten werden, sind grundlegende Kenntnisse der Programmiersprache C# erforderlich.
## Pakete importieren
Zunächst müssen Sie die erforderlichen Pakete in Ihr C#-Projekt importieren. Fügen Sie Folgendes hinzu`using` -Anweisungen oben in Ihrer Codedatei:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Schritt 1: Einrichten der Quell- und Ausgabeverzeichnisse
Definieren wir zunächst die Quell- und Ausgabeverzeichnisse für unser Beispiel:
```csharp
//Quellverzeichnis
string sourceDir = "Your Document Directory";
//Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` mit den tatsächlichen Pfaden zu Ihren Quell- und Ausgabeverzeichnissen.
## Schritt 2: Erstellen Sie einen benannten Bereich mit einer Formel im deutschen Gebietsschema
Als Nächstes erstellen wir einen neuen benannten Bereich mit einer Formel im deutschen Gebietsschema:
```csharp
const string name = "HasFormula";
const string value = "=GET.ZELLE(48, INDIREKT(\"ZS\",FALSCH))";
Workbook wbSource = new Workbook(sourceDir + "sampleNamedRangeTest.xlsm");
WorksheetCollection wsCol = wbSource.Worksheets;
int nameIndex = wsCol.Names.Add(name);
Name namedRange = wsCol.Names[nameIndex];
namedRange.RefersTo = value;
```
In diesem Schritt:
1.  Definiert den Namen und den Wert des benannten Bereichs. Die Formel`=GET.ZELLE(48, INDIREKT("ZS",FALSCH))` ist das deutsche Äquivalent der englischen Formel`=GET.CELL(48, INDIRECT("ZS",FALSE))`.
2.  Erstellt ein neues`Workbook` Objekt und erhielt die`WorksheetCollection` davon.
3.  Es wurde ein neuer benannter Bereich mit dem angegebenen Namen und der angegebenen Formel hinzugefügt. Dabei wurde der`Add` Methode der`Names`Sammlung.
4.  Erhalten Sie die neu geschaffene`Name` Objekt und legen Sie dessen`RefersTo` -Eigenschaft dem Formelwert.
## Schritt 3: Speichern Sie die Arbeitsmappe mit dem benannten Bereich
Abschließend speichern wir die Arbeitsmappe mit dem benannten Bereich:
```csharp
wbSource.Save(outputDir + "sampleOutputNamedRangeTest.xlsm");
Console.WriteLine("SupportNamedRangeFormulasInGermanLocale executed successfully.\r\n");
```
In diesem Schritt:
1.  Gespeichert die geänderten`Workbook`Objekt in das angegebene Ausgabeverzeichnis.
2. Eine Erfolgsmeldung wurde auf der Konsole gedruckt.
Und das war’s! Sie haben jetzt erfolgreich einen benannten Bereich mit einer Formel im deutschen Gebietsschema mit Aspose.Cells für .NET erstellt.
## Abschluss
In diesem Tutorial haben Sie gelernt, wie Sie mit benannten Bereichsformeln in einem deutschen Gebietsschema mithilfe der Aspose.Cells-Bibliothek für .NET arbeiten. Sie haben erfahren, wie Sie einen neuen benannten Bereich erstellen, seine Formel festlegen und die geänderte Arbeitsmappe speichern. Dieses Wissen kann nützlich sein, wenn Sie mit Excel-Dateien arbeiten, die eine bestimmte Lokalisierung erfordern, oder wenn Sie benannte Bereiche und Formeln in Ihren Anwendungen programmgesteuert verwalten müssen.
## Häufig gestellte Fragen
### Was ist der Zweck benannter Bereiche in Excel?
Benannte Bereiche in Excel ermöglichen es Ihnen, einer Zelle oder einem Zellbereich einen beschreibenden Namen zuzuweisen. Dies erleichtert das Verweisen auf die Daten und ihre Verwendung in Formeln und Funktionen.
### Kann Aspose.Cells für .NET benannte Bereiche in verschiedenen Gebietsschemas verarbeiten?
Ja, Aspose.Cells für .NET unterstützt das Arbeiten mit benannten Bereichen in verschiedenen Gebietsschemas, einschließlich des deutschen Gebietsschemas. Das Beispiel in diesem Tutorial zeigt, wie Sie einen benannten Bereich mit einer Formel im deutschen Gebietsschema erstellen.
### Gibt es eine Möglichkeit, eine benannte Bereichsformel von einem Gebietsschema in ein anderes zu konvertieren?
 Ja, Aspose.Cells für .NET bietet Methoden zum Konvertieren von Formeln zwischen verschiedenen Gebietsschemas. Sie können die`ConvertFormula` Methode der`Formula` Klasse zum Konvertieren einer Formel von einem Gebietsschema in ein anderes.
### Kann ich Aspose.Cells für .NET verwenden, um Excel-Dateien programmgesteuert zu erstellen und zu bearbeiten?
Ja, Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Sie Excel-Dateien programmgesteuert erstellen, lesen und ändern können. Sie können eine Vielzahl von Vorgängen ausführen, z. B. Arbeitsblätter erstellen, Zellen formatieren und Formeln und Funktionen anwenden.
### Wo finde ich weitere Ressourcen und Support für Aspose.Cells für .NET?
 Die Dokumentation zu Aspose.Cells für .NET finden Sie auf der[Aspose-Dokumentationswebsite](https://reference.aspose.com/cells/net/) Darüber hinaus können Sie die neueste Version der Bibliothek von der[Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/) . Wenn Sie weitere Hilfe benötigen oder Fragen haben, können Sie sich an das Aspose-Supportteam wenden über[Aspose.Cells-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
