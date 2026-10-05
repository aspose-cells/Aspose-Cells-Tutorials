---
category: general
date: 2026-02-15
description: Erstelle eine neue Arbeitsmappe in C# und kopiere eine Pivot‑Tabelle,
  ohne ihre Definition zu verlieren. Lerne, wie man Zeilen kopiert, die Pivot‑Tabelle
  beibehält und die Pivot‑Tabelle einfach dupliziert.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: de
og_description: Erstelle ein neues Arbeitsbuch in C# und kopiere eine Pivot‑Tabelle,
  wobei deren Definition erhalten bleibt. Schritt‑für‑Schritt‑Anleitung für Entwickler.
og_title: Neues Arbeitsbuch in C# erstellen – Pivot‑Tabelle beibehalten
tags:
- Aspose.Cells
- C#
- Excel automation
title: Neues Arbeitsbuch in C# erstellen – Pivot‑Tabelle beibehalten
url: /de/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues Arbeitsbuch in C# erstellen – Pivot‑Tabelle erhalten

Haben Sie jemals **neues Arbeitsbuch erstellen** in C# benötigt, das eine exakte Kopie einer Pivot‑Tabelle aus einer anderen Datei enthält? Sie sind nicht der Einzige. In vielen Reporting‑Pipelines ist die Pivot‑Tabelle das Herzstück der Analyse, und das Verlieren ihrer Definition beim Verschieben von Daten ist ein Albtraum.

Die gute Nachricht? Mit ein paar Zeilen Aspose.Cells‑Code können Sie Zeilen – einschließlich der Pivot‑Tabelle – in ein frisches Arbeitsbuch kopieren und alles intakt behalten. Im Folgenden sehen Sie **wie man Zeilen kopiert**, **Pivot‑Tabelle erhalten**‑Einstellungen und sogar **Pivot‑Tabelle duplizieren** über Dateien hinweg, ohne Formeln oder Cache zu beschädigen.

> **Pro‑Tipp:** Aspose.Cells funktioniert mit .NET Core, .NET Framework und sogar Xamarin, sodass das gleiche Snippet überall läuft, wo Sie es benötigen.

---

![Neues Arbeitsbuch mit kopierter Pivot‑Tabelle](/images/create-new-workbook-pivot.png "Neues Arbeitsbuch mit kopierter Pivot‑Tabelle")

## Schritt 1 – Neues Arbeitsbuch erstellen und die Quelldatei laden

Das Erste, was wir tun, ist **neues Arbeitsbuch erstellen**‑Objekte. Eines enthält die Originaldaten, das andere erhält den kopierten Bereich.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Warum das wichtig ist:*  
`Workbook` ist der Einstiegspunkt für jede Excel‑Manipulation in Aspose.Cells. Durch das Instanziieren eines frischen Arbeitsbuchs garantieren wir eine saubere Basis – keine versteckten Stile oder fremden Arbeitsblätter, die später stören könnten.

## Schritt 2 – Wie man Zeilen einschließlich einer Pivot‑Tabelle kopiert

Jetzt kommt der Kern des Problems: **wie man Zeilen kopiert**, die die Pivot‑Tabelle umfassen, ohne sie zu flach zu machen. Die Methode `CopyRows` erledigt genau das.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Ein paar Dinge, die zu beachten sind:

* `startRow` und `totalRows` definieren den Block, der die Pivot‑Tabelle enthält.  
* Die Methode kopiert **sowohl** Rohdaten als auch den Pivot‑Cache, sodass das Zielarbeitsbuch weiß, wie es die Pivot‑Tabelle on‑the‑fly neu aufbauen kann.  
* Wenn Ihre Pivot‑Tabelle tiefer im Blatt beginnt, ändern Sie einfach die Indizes – ein anderer API‑Aufruf ist nicht nötig.

> **Häufige Frage:** *Verliert die kopierte Pivot‑Tabelle ihre Quell‑Datenreferenz?*  
> Nein. Aspose.Cells bettet den Cache direkt in das Arbeitsblatt ein, sodass die Pivot‑Tabelle in der neuen Datei eigenständig ist.

## Schritt 3 – Pivot‑Tabelle beim Speichern des Ziels erhalten

Nachdem die Zeilen kopiert wurden, befindet sich die Pivot‑Tabelle im Zielarbeitsbuch exakt so, wie sie im Quellarbeitsbuch war. Das Speichern der Datei ist unkompliziert.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Wenn Sie `destination.xlsx` in Excel öffnen, sehen Sie die Pivot‑Tabelle bereit zum Aktualisieren. Das **Pivot‑Tabelle erhalten**‑Verhalten ist automatisch, weil der Cache mit den Zeilen mitgereist ist.

### Ergebnis überprüfen

Öffnen Sie die Datei und:

1. Klicken Sie auf die Pivot‑Tabelle.  
2. Beachten Sie, dass die Feldliste erscheint – das bedeutet, der Cache ist intakt.  
3. Versuchen Sie eine Aktualisierung; die Daten werden ohne Fehler aktualisiert.

Falls Sie einen *#REF!*‑Fehler erhalten, prüfen Sie doppelt, dass der kopierte Bereich die versteckten Cache‑Zeilen enthält (normalerweise direkt nach den sichtbaren Daten).

## Schritt 4 – Pivot‑Tabelle in mehrere Arbeitsbücher duplizieren (optional)

Manchmal benötigen Sie dieselbe Pivot‑Tabelle in mehreren Berichten. Das Muster, das wir gerade verwendet haben, skaliert gut – wiederholen Sie einfach das Kopieren für jedes neue Arbeitsbuch.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Dieses Snippet **dupliziert die Pivot‑Tabelle** dreimal mit einer einzigen Schleife. Passen Sie das `targets`‑Array an Ihren Reporting‑Zeitplan an.

### Randfälle, die Sie beachten sollten

| Situation | Worauf zu achten ist | Lösung |
|-----------|----------------------|--------|
| Pivot verwendet externe Datenquelle | Der Cache kann eine Verbindung referenzieren, die auf dem neuen Rechner nicht existiert | Betten Sie die Datenquelle ein oder erstellen Sie die Verbindung im Zielarbeitsbuch neu |
| Sehr große Pivot ( > 100 k Zeilen ) | `CopyRows` kann speicherintensiv sein | Verwenden Sie `CopyRows` in Teilen oder erwägen Sie `Copy` mit `PasteOptions`, um den Speicherverbrauch zu begrenzen |
| Arbeitsblatt hat versteckte Zeilen/Spalten | Versteckte Cache‑Zeilen könnten übersprungen werden, wenn Sie nur sichtbare Zeilen kopieren | Kopieren Sie stets den genauen Zeilenbereich, der den Cache enthält, nicht nur den sichtbaren Bereich |

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein eigenständiges Programm, das Sie in eine Konsolen‑App einfügen können.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Führen Sie das Programm aus, öffnen Sie `destination.xlsx`, und Sie sehen dieselbe Pivot‑Tabelle, bereit, Ihre Daten zu analysieren. Keine manuelle Neuerstellung erforderlich.

## Fazit

Wir haben gerade gezeigt, wie man **neues Arbeitsbuch erstellen** in C# und **Pivot‑Tabelle kopieren** kann, während jede Einstellung erhalten bleibt. Durch die Verwendung von `CopyRows` erhalten Sie eine zuverlässige Methode, um **Pivot‑Tabelle erhalten**‑Funktionalität zu gewährleisten, die uralte Frage „**wie man Zeilen kopiert**“ zu beantworten und sogar **Pivot‑Tabelle duplizieren** über mehrere Berichte hinweg mit minimalem Code.

Nächste Schritte? Versuchen Sie, den kopierten Bereich zu ändern, um Diagramme einzuschließen, die dieselbe Pivot‑Tabelle referenzieren, oder experimentieren Sie mit `PasteOptions`, um die Formatierung exakt beizubehalten. Das gleiche Muster funktioniert für andere Aspose.Cells‑Objekte wie Tabellen und benannte Bereiche, also fühlen Sie sich frei, es zu erweitern.

Haben Sie ein Problem, mit dem Sie kämpfen – vielleicht eine Pivot‑Tabelle, die Daten aus einer externen Datenbank zieht, oder ein Arbeitsbuch, das in der Cloud liegt? Hinterlassen Sie unten einen Kommentar, und wir werden es gemeinsam angehen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}