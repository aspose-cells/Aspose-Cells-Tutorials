---
category: general
date: 2026-02-23
description: Wie man ein Arbeitsbuch mit Aspose.Cells erstellt und Marker mit einem
  JSON‑Array hinzufügt. Erfahren Sie, wie Sie Marker hinzufügen, ein JSON‑Array verwenden
  und Smart‑Marker in Aspose.Cells in wenigen Minuten nutzen.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: de
og_description: Wie man mit Aspose.Cells eine Arbeitsmappe erstellt, Marker hinzufügt
  und ein JSON‑Array verwendet. Diese Schritt‑für‑Schritt‑Anleitung zeigt Ihnen alles,
  was Sie benötigen.
og_title: Wie man ein Arbeitsbuch mit Smart Markern erstellt – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Wie man eine Arbeitsmappe mit Smart Markern erstellt – Aspose.Cells‑Leitfaden
url: /de/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man eine Arbeitsmappe mit Smart Markers erstellt – Aspose.Cells Anleitung

Haben Sie sich jemals gefragt, **wie man eine Arbeitsmappe erstellt**, die Daten automatisch aus einer JSON‑Quelle füllt? Sie sind nicht allein – Entwickler fragen ständig, wie man Marker hinzufügt, die Werte aus Arrays ziehen, besonders beim Arbeiten mit Aspose.Cells. Die gute Nachricht? Es ist ziemlich einfach, sobald man das Smart‑Marker‑Konzept versteht. In diesem Tutorial gehen wir Schritt für Schritt durch das Erstellen einer Arbeitsmappe, das Hinzufügen von Markern, die Verwendung eines JSON‑Arrays und das Konfigurieren von Smart Markern in Aspose.Cells, sodass Sie Excel‑Dateien on‑the‑fly erzeugen können.

Wir behandeln alles, was Sie wissen müssen: Initialisierung der Arbeitsmappe, Aufbau einer `MarkerCollection`, Einspeisen eines JSON‑Arrays, Umschalten des „ArrayAsSingle“-Flags und schließlich Anwenden der Marker. Am Ende haben Sie ein voll funktionsfähiges C#‑Programm, das eine Excel‑Datei mit den Werten **A**, **B** und **C** automatisch befüllt. Keine externen Dienste, nur reiner Aspose.Cells‑Zauber.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)
- Aspose.Cells für .NET NuGet‑Paket (`Install-Package Aspose.Cells`)
- Grundlegendes Verständnis der C#‑Syntax (wenn Sie ganz neu sind, sind die Snippets stark kommentiert)
- Visual Studio oder eine beliebige IDE Ihrer Wahl

Wenn Sie das bereits haben, großartig – lassen Sie uns loslegen.

## Schritt 1: Wie man eine Arbeitsmappe erstellt (Excel‑Datei initialisieren)

Das erste, was Sie benötigen, ist ein leeres Workbook‑Objekt. Stellen Sie sich das als leere Leinwand vor, die Aspose.Cells später mit Daten füllt.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Warum das wichtig ist:** `Workbook` ist der Einstiegspunkt für jede Excel‑Operation. Ohne ihn können Sie keine Smart Markers anhängen oder die Datei speichern. Das Erstellen des Workbooks zuerst sorgt außerdem für eine saubere Umgebung für die nachfolgenden Schritte.

## Schritt 2: Wie man Marker hinzufügt – Initialisieren einer Marker‑Collection

Smart Markers befinden sich in einer `MarkerCollection`. Diese Collection ist der Ort, an dem Sie Platzhalter (die Marker) und die Daten, die sie ersetzen sollen, definieren.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Pro‑Tipp:** Sie können dieselbe `MarkerCollection` für mehrere Arbeitsblätter wiederverwenden, aber das Beibehalten einer pro Blatt erleichtert das Debuggen.

## Schritt 3: JSON‑Array verwenden – Einen Marker mit JSON‑Daten hinzufügen

Jetzt fügen wir tatsächlich einen Marker hinzu. Der Platzhalter `{SmartMarker}` wird durch das bereitgestellte JSON‑Array ersetzt. Das JSON muss ein stringifiziertes Array sein, z. B. `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Erklärung:** Die `Add`‑Methode nimmt zwei Argumente entgegen: den Marker‑Text und die Datenquelle. Hier ist die Datenquelle ein JSON‑Array, das Aspose.Cells automatisch parsen kann. Das ist das Kernstück von **JSON‑Array verwenden** mit Smart Markern.

## Schritt 4: Marker konfigurieren – Das Array als einzelnen Wert behandeln

Standardmäßig erweitert Aspose.Cells ein JSON‑Array in separate Zeilen. Wenn Sie das gesamte Array als einzelnen Zellenwert behandeln möchten (nützlich für Dropdown‑Listen oder verkettete Zeichenketten), setzen Sie das `ArrayAsSingle`‑Flag.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Wann man es verwendet:** Wenn das Array in einer Zelle erscheinen soll (z. B. `"A,B,C"`), aktivieren Sie dieses Flag. Andernfalls schreibt Aspose.Cells jedes Element in eine eigene Zeile.

## Schritt 5: Marker an das Arbeitsblatt anhängen und anwenden

Zum Schluss binden Sie die Marker‑Collection an das Arbeitsblatt und lassen Aspose.Cells die Platzhalter durch die tatsächlichen Daten ersetzen.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Ergebnis:** Nach dem Ausführen des Programms enthält `SmartMarkerResult.xlsx` den Wert **A** (oder das gesamte Array, wenn `ArrayAsSingle` true ist) in Zelle `A1`. Öffnen Sie die Datei, um dies zu überprüfen.

### Erwartete Ausgabe

| A |
|---|
| A |   *(wenn `ArrayAsSingle` false ist, füllt das erste Element die Zelle)*

Wenn Sie `ArrayAsSingle = true` setzen, enthält Zelle `A1` die Zeichenkette `["A","B","C"]`.

## Schritt 6: Wie man Marker hinzufügt – Erweiterte Szenarien (Optional)

Sie fragen sich vielleicht, *was ist, wenn ich mehr als einen Marker brauche?* Die Antwort ist einfach: Rufen Sie einfach erneut `Add` auf.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Warum das funktioniert:** Jeder Marker arbeitet unabhängig, sodass Sie „Array as single“ und „Expand into rows“ im selben Arbeitsblatt kombinieren können. Diese Flexibilität ist ein Markenzeichen von **Smart Markers Aspose.Cells**.

## Häufige Fallstricke & wie man sie vermeidet

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Marker nicht ersetzt | Platzhaltertext fehlt oder Tippfehler | Stellen Sie sicher, dass die Zelle den genauen Marker‑String (`{SmartMarker}`) enthält |
| JSON nicht geparst | Ungültige JSON‑Syntax (fehlende Anführungszeichen) | Verwenden Sie einen JSON‑Validator oder doppelte Escape‑Zeichen für Anführungszeichen in C#‑Strings |
| Array wird unerwartet erweitert | `ArrayAsSingle` bleibt auf dem Standardwert `false` | Setzen Sie `["ArrayAsSingle"] = true` für den jeweiligen Marker |
| Arbeitsmappe leer gespeichert | `Apply()` wurde nicht vor `Save()` aufgerufen | Rufen Sie immer `worksheet.SmartMarkers.Apply()` vor dem Speichern auf |

## Vollständiges funktionierendes Beispiel (Copy‑Paste bereit)

Unten finden Sie das komplette Programm, das Sie in eine Konsolen‑App einfügen können. Keine zusätzlichen Dateien sind erforderlich.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Führen Sie das Programm aus, öffnen Sie `SmartMarkerResult.xlsx`, und Sie sehen das JSON‑Array (oder sein erstes Element) ordentlich in Zelle **A1** platziert.

## Nächste Schritte: Lösung erweitern

Jetzt, wo Sie **wie man eine Arbeitsmappe erstellt**, **wie man Marker hinzufügt** und **JSON‑Array verwenden** mit Aspose.Cells kennen, bedenken Sie diese weiterführenden Ideen:

1. **Mehrere Arbeitsblätter** – Durchlaufen Sie eine Liste von Arbeitsblättern und hängen Sie jedem ein unterschiedliches Marker‑Collection an.
2. **Dynamisches JSON** – Holen Sie JSON von einer Web‑API (`HttpClient`) und füttern Sie es direkt in `smartMarkerCollection.Add`.
3. **Ausgabe formatieren** – Nach dem Anwenden der Marker formatieren Sie Zellen (Schriftarten, Farben), um den Bericht zu verfeinern.
4. **Exportformate** – Speichern Sie die Arbeitsmappe als PDF, CSV oder HTML, indem Sie `workbook.Save("file.pdf")` ändern.

Jedes dieser Themen beinhaltet natürlich **Smart Markers Aspose.Cells**, sodass Sie dieselben Kernkonzepte, die Sie gerade gelernt haben, erweitern.

## Fazit

Wir haben **wie man eine Arbeitsmappe erstellt**, **wie man Marker hinzufügt** und **JSON‑Array verwendet** mit Aspose.Cells Smart Markern durchgegangen. Das vollständige, ausführbare Beispiel demonstriert den gesamten Workflow, von der Initialisierung des `Workbook` bis zum Speichern der finalen Datei. Durch das Umschalten des `ArrayAsSingle`‑Flags erhalten Sie eine feinkörnige Kontrolle darüber, wie JSON‑Daten in Excel erscheinen, wodurch die Lösung für ein breites Spektrum an Reporting‑Szenarien anpassbar wird.

Probieren Sie den Code aus, passen Sie das JSON an und experimentieren Sie mit zusätzlichen Markern. Wenn Sie diese Bausteine beherrschen, wird das Erzeugen anspruchsvoller Excel‑Berichte zum Kinderspiel. Haben Sie Fragen oder möchten Sie einen coolen Anwendungsfall teilen? Hinterlassen Sie unten einen Kommentar – happy coding!

![Diagramm, das zeigt, wie man eine Arbeitsmappe mit Smart Markern in Aspose.Cells erstellt](https://example.com/images/create-workbook-smart-markers.png "wie man eine Arbeitsmappe mit Aspose.Cells Smart Markern erstellt")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}