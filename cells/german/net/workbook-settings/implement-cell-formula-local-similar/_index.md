---
"description": "Entdecken Sie, wie Sie eine Zellformel implementieren, die der lokalen Bereichsformelfunktion in Aspose.Cells für .NET ähnelt. Erfahren Sie, wie Sie integrierte Excel-Funktionsnamen anpassen und vieles mehr."
"linktitle": "Implementieren Sie die lokale Zellformel ähnlich wie die lokale Bereichsformel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Implementieren Sie die lokale Zellformel ähnlich wie die lokale Bereichsformel"
"url": "/de/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementieren Sie die lokale Zellformel ähnlich wie die lokale Bereichsformel

## Einführung
Aspose.Cells für .NET ist eine leistungsstarke und flexible API zur Tabellenkalkulation, mit der Sie Excel-Dateien programmgesteuert erstellen, bearbeiten und konvertieren können. Eine der vielen Funktionen von Aspose.Cells ist die Möglichkeit, das Verhalten integrierter Excel-Funktionen anzupassen, einschließlich der Möglichkeit, eigene lokale Funktionsnamen zu erstellen. In diesem Tutorial führen wir Sie durch die Schritte zur Implementierung einer Zellenformel, die der lokalen Bereichsformelfunktion in Aspose.Cells für .NET ähnelt.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie über Folgendes verfügen:
1. Auf Ihrem System muss Microsoft Visual Studio 2010 oder höher installiert sein.
2. Die neueste Version der Aspose.Cells für .NET-Bibliothek muss in Ihrem Projekt installiert sein. Sie können die Bibliothek von der [Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/).
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Pakete in Ihr C#-Projekt importieren. Fügen Sie oben in Ihrer Codedatei die folgenden using-Anweisungen hinzu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Schritt 1: Erstellen einer benutzerdefinierten Globalisierungseinstellungsklasse
Der erste Schritt besteht darin, eine benutzerdefinierte `GlobalizationSettings` Klasse, mit der Sie das Standardverhalten von Excel-Funktionen überschreiben können. In diesem Beispiel ändern wir die Namen der `SUM` Und `AVERAGE` Funktionen zu `UserFormulaLocal_SUM` Und `UserFormulaLocal_AVERAGE`, jeweils.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Ändern Sie den Namen der SUM-Funktion nach Bedarf.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Ändern Sie den Funktionsnamen AVERAGE nach Bedarf.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Schritt 2: Erstellen einer neuen Arbeitsmappe und Zuweisen der benutzerdefinierten Globalisierungseinstellungen
Als nächstes erstellen Sie eine neue Workbook-Instanz und weisen die benutzerdefinierte `GlobalizationSettings` Implementierungsklasse zur Arbeitsmappe `Settings.GlobalizationSettings` Eigentum.
```csharp
//Arbeitsmappe erstellen
Workbook wb = new Workbook();
//Weisen Sie die Implementierungsklasse „GlobalizationSettings“ zu
wb.Settings.GlobalizationSettings = new GS();
```
## Schritt 3: Zugriff auf das erste Arbeitsblatt und eine Zelle
Greifen wir nun auf das erste Arbeitsblatt in der Arbeitsmappe und eine bestimmte Zelle in diesem Arbeitsblatt zu.
```csharp
//Greifen Sie auf das erste Arbeitsblatt zu
Worksheet ws = wb.Worksheets[0];
//Greifen Sie auf einige Zellen zu
Cell cell = ws.Cells["C4"];
```
## Schritt 4: Formeln zuweisen und FormulaLocal drucken
Zum Schluss weisen wir die `SUM` Und `AVERAGE` Formeln in die Zelle und drucken Sie die resultierende `FormulaLocal` Werte.
```csharp
//Weisen Sie die SUM-Formel zu und drucken Sie deren FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Weisen Sie die Formel AVERAGE zu und drucken Sie deren FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Abschluss
In diesem Tutorial haben Sie gelernt, wie Sie eine Zellformel implementieren, die der lokalen Bereichsformelfunktion in Aspose.Cells für .NET ähnelt. Durch die Erstellung einer benutzerdefinierten `GlobalizationSettings` Mit der Klasse können Sie das Standardverhalten von Excel-Funktionen überschreiben und die lokalen Funktionsnamen an Ihre Bedürfnisse anpassen. Dies ist besonders nützlich bei der Arbeit mit lokalisierten oder internationalisierten Excel-Dokumenten.
## Häufig gestellte Fragen
### Was ist der Zweck der `GlobalizationSettings` Klasse in Aspose.Cells?
Der `GlobalizationSettings` Mit der Klasse in Aspose.Cells können Sie das Verhalten integrierter Excel-Funktionen anpassen, einschließlich der Möglichkeit, die lokalen Funktionsnamen zu ändern.
### Kann ich das Verhalten anderer Funktionen außer Kraft setzen als `SUM` Und `AVERAGE`?
Ja, Sie können das Verhalten jeder integrierten Excel-Funktion überschreiben, indem Sie die `GetLocalFunctionName` Methode in Ihrem benutzerdefinierten `GlobalizationSettings` Klasse.
### Gibt es eine Möglichkeit, die Funktionsnamen auf ihre Standardwerte zurückzusetzen?
Ja, Sie können die Funktionsnamen zurücksetzen, indem Sie entweder die benutzerdefinierten `GlobalizationSettings` Klasse oder durch Rückgabe einer leeren Zeichenfolge aus der `GetLocalFunctionName` Verfahren.
### Kann ich diese Funktion verwenden, um benutzerdefinierte Funktionen in Aspose.Cells zu erstellen?
Nein, die `GlobalizationSettings` Die Klasse ist dafür konzipiert, das Verhalten integrierter Excel-Funktionen zu überschreiben, nicht aber, benutzerdefinierte Funktionen zu erstellen. Wenn Sie benutzerdefinierte Funktionen erstellen müssen, können Sie die `UserDefinedFunction` Klasse in Aspose.Cells.
### Ist diese Funktion in allen Versionen von Aspose.Cells für .NET verfügbar?
Ja, die `GlobalizationSettings` Klasse und die Möglichkeit, Funktionsnamen anzupassen, sind in allen Versionen von Aspose.Cells für .NET verfügbar.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}