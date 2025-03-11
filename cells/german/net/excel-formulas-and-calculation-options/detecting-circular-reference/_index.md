---
title: Zirkelbezüge in Excel programmgesteuert erkennen
linktitle: Zirkelbezüge in Excel programmgesteuert erkennen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Mit Aspose.Cells für .NET können Sie Zirkelbezüge in Excel ganz einfach erkennen. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um genaue Berechnungen in Ihren Tabellen sicherzustellen.
weight: 13
url: /de/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zirkelbezüge in Excel programmgesteuert erkennen

## Einführung
Wenn Sie mit Excel-Dateien arbeiten, ist ein zirkulärer Verweis eines der frustrierendsten Probleme, auf das Sie stoßen können. Dies geschieht, wenn eine Formel entweder direkt oder indirekt auf ihre eigene Zelle verweist und eine Schleife erzeugt, die die Berechnungs-Engine von Excel verwirren kann. Aber keine Angst! Mit Aspose.Cells für .NET können Sie diese lästigen zirkulären Verweise programmgesteuert erkennen und so sicherstellen, dass Ihre Tabellenkalkulationen funktionsfähig und genau bleiben. In dieser Anleitung führen wir Sie Schritt für Schritt durch den Prozess und machen ihn kinderleicht.
## Voraussetzungen
Bevor wir uns in die Einzelheiten der Erkennung von Zirkelbezügen vertiefen, stellen wir sicher, dass Sie über alles verfügen, was Sie für den Einstieg benötigen:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Dies wird Ihre Entwicklungsumgebung sein.
2. .NET Framework: Stellen Sie sicher, dass Sie eine kompatible Version des .NET Frameworks verwenden (mindestens .NET Framework 4.0).
3.  Aspose.Cells-Bibliothek: Sie benötigen die Aspose.Cells-Bibliothek. Sie können sie herunterladen von[Aspose-Website](https://releases.aspose.com/cells/net/).
4. Grundkenntnisse in C#: Kenntnisse in der C#-Programmierung sind von Vorteil, da wir Code in dieser Sprache schreiben werden.
5. Excel-Datei: Halten Sie eine Excel-Datei bereit, die zirkuläre Referenzen zum Testen enthält. Sie können eine einfache Datei erstellen oder ein Beispiel herunterladen.
Nachdem wir nun die Voraussetzungen geschaffen haben, können wir mit dem spaßigen Teil fortfahren!
## Pakete importieren
Bevor Sie mit dem Programmieren beginnen können, müssen Sie die erforderlichen Pakete importieren. So geht's:
### Neues Projekt erstellen
- Öffnen Sie Visual Studio und erstellen Sie ein neues C#-Konsolenanwendungsprojekt.
### Aspose.Cells-Referenz hinzufügen
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
- Wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie nach „Aspose.Cells“ und installieren Sie die neueste Version.
### Erforderliche Namespaces importieren
 Ganz oben auf Ihrer`Program.cs` Importieren Sie die erforderlichen Namespaces:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nachdem wir nun alles eingerichtet haben, tauchen wir in den Code ein, um Zirkelbezüge in einer Excel-Datei zu erkennen.
## Schritt 1: Definieren Sie das Eingabeverzeichnis
Zuerst müssen Sie das Verzeichnis angeben, in dem sich Ihre Excel-Datei befindet. Dorthin laden Sie Ihre Excel-Datei.
```csharp
// Eingabeverzeichnis
string sourceDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad zu Ihrer Excel-Datei.
## Schritt 2: Laden der Arbeitsmappe mit LoadOptions
Als Nächstes laden Sie Ihre Excel-Arbeitsmappe. Hier beginnt die Magie!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Hier erstellen wir eine neue Instanz von`LoadOptions` und laden Sie die Arbeitsmappe vom angegebenen Pfad. Stellen Sie sicher, dass Ihr Excel-Dateiname übereinstimmt!
## Schritt 3: Iterationseinstellungen aktivieren
Um zirkuläre Referenzen zuzulassen, müssen Sie die Iterationseinstellungen in der Arbeitsmappe aktivieren.
```csharp
objWB.Settings.Iteration = true;
```
Dies weist Aspose.Cells an, zirkuläre Referenzen während der Berechnung zuzulassen.
## Schritt 4: Berechnungsoptionen und Rundmonitor erstellen
Erstellen wir nun die Berechnungsoptionen und unseren benutzerdefinierten Rundmonitor.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Hier erstellen wir eine Instanz von`CalculationOptions` und eine benutzerdefinierte`CircularMonitor`Dieser Monitor hilft dabei, alle während der Berechnungen gefundenen Zirkelbezüge zu verfolgen.
## Schritt 5: Berechnen Sie die Formeln
Jetzt ist es Zeit, die Formeln in Ihrer Arbeitsmappe zu berechnen.
```csharp
objWB.CalculateFormula(copts);
```
Diese Zeile führt die Berechnung aus und prüft auf zirkuläre Referenzen.
## Schritt 6: Zirkuläre Referenzen zählen
Nach der Berechnung können Sie zählen, wie viele Zirkelverweise gefunden wurden.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Dadurch wird die Anzahl der in Ihrer Excel-Datei erkannten Zirkelverweise ausgegeben.
## Schritt 7: Ergebnisse anzeigen
Lassen Sie uns abschließend die Ergebnisse anzeigen und bestätigen, dass unsere Methode erfolgreich ausgeführt wurde.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Schritt 8: Implementieren Sie die CircularMonitor-Klasse
 Um den Vorgang abzuschließen, müssen Sie Folgendes implementieren:`CircularMonitor` Klasse. Diese Klasse erbt von`AbstractCalculationMonitor` und handhaben Sie die Erkennung von Zirkelverweisen.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Diese Klasse erfasst die Details jedes gefundenen Zirkelverweises, einschließlich des Arbeitsblattnamens und des Zellenindex.
## Abschluss
Das Erkennen von Zirkelbezügen in Excel mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang, wenn Sie ihn in überschaubare Schritte aufteilen. Wenn Sie dieser Anleitung folgen, können Sie Zirkelbezüge in Ihren Tabellenkalkulationen problemlos erkennen und behandeln und so sicherstellen, dass Ihre Berechnungen genau und zuverlässig bleiben. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, Aspose.Cells bietet leistungsstarke Tools zur Verbesserung Ihrer Excel-Manipulationsfunktionen. 
## Häufig gestellte Fragen
### Was ist ein Zirkelverweis in Excel?
Ein zirkulärer Verweis liegt vor, wenn eine Formel auf ihre eigene Zelle zurückverweist und dadurch eine Endlosschleife in den Berechnungen verursacht.
### Wie kann ich zirkuläre Referenzen programmgesteuert erkennen?
Sie können die Aspose.Cells-Bibliothek in .NET verwenden, um zirkuläre Referenzen programmgesteuert zu erkennen, indem Sie einen benutzerdefinierten Berechnungsmonitor implementieren.
### Was sind die Voraussetzungen für die Nutzung von Aspose.Cells?
Sie müssen Visual Studio, das .NET Framework und die Aspose.Cells-Bibliothek installiert haben.
### Kann ich Aspose.Cells kostenlos nutzen?
Ja, Aspose.Cells bietet eine kostenlose Testversion an, mit der Sie die Funktionen erkunden können.
### Wo finde ich weitere Informationen zu Aspose.Cells?
 Besuchen Sie die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für detaillierte Informationen und Beispiele.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
