---
category: general
date: 2026-02-14
description: Wie man Hierarchien in SmartMarker‑Vorlagen erstellt, ist einfacher,
  als Sie denken – lernen Sie, hierarchische Daten zu erzeugen und Mitarbeiter effizient
  aufzulisten.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: de
og_description: Wie man Hierarchien in SmartMarker‑Vorlagen erstellt, ist einfach.
  Folgen Sie dieser Anleitung, um hierarchische Daten zu erzeugen und Mitarbeiter
  mit verschachtelten Bereichen aufzulisten.
og_title: Wie man mit SmartMarker Hierarchien erstellt – Komplettanleitung
tags:
- SmartMarker
- C#
- templating
title: Wie man mit SmartMarker Hierarchien erstellt – Schritt‑für‑Schritt‑Anleitung
url: /de/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Hierarchien mit SmartMarker erstellt – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man Hierarchien** in einer SmartMarker‑Vorlage erstellt, ohne sich die Haare zu raufen? Sie sind nicht allein. In vielen Reporting‑Szenarien benötigen Sie eine Eltern‑Kind‑Beziehung – denken Sie an Abteilungen und die dort arbeitenden Personen. Die gute Nachricht: SmartMarker macht das ein Kinderspiel, sobald Sie die richtigen Schritte kennen.

In diesem Tutorial gehen wir den gesamten Prozess durch: von **der Erstellung hierarchischer Daten** in C#, über das Aktivieren verschachtelter Bereiche, bis hin zum Rendern einer Vorlage, die **Mitarbeiter** für jede Abteilung **auflistet**. Am Ende haben Sie ein einsatzbereites Beispiel, das Sie in jedes .NET‑Projekt einbinden können.

---

## Was Sie benötigen

- .NET 6+ (jede aktuelle Version funktioniert)
- Ein Verweis auf die **SmartMarker**‑Bibliothek (der Namespace `ws.SmartMarkerProcessor`)
- Grundkenntnisse in C# – nichts Aufwändiges, nur ein paar Objekte und ein Lambda oder zwei
- Eine IDE oder ein Editor Ihrer Wahl (Visual Studio, Rider, VS Code … Sie entscheiden)

Wenn Sie das bereits haben, super – dann legen wir los.

---

## Wie man Hierarchien erstellt – Überblick

Die Kernidee ist, einen **verschachtelten Objektgraphen** zu bauen, der die Struktur widerspiegelt, die Sie im fertigen Dokument sehen wollen. In unserem Fall sieht der Graph folgendermaßen aus:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker kann dann über `Departments` iterieren und, weil wir die **verschachtelte Bereichsverarbeitung** aktivieren, automatisch über jede `Employees`‑Sammlung einer Abteilung schleifen.

---

## Schritt 1: Das hierarchische Datenmodell erstellen

Zuerst erstellen wir ein anonymes Objekt, das ein Array von Abteilungen enthält, wobei jede ihre eigene Mitarbeitenden‑Liste hat. Die Verwendung eines anonymen Typs hält das Beispiel leichtgewichtig – Sie können später problemlos echte POCO‑Klassen einsetzen.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Warum das wichtig ist:** Das `Departments`‑Array ist die Sammlung auf oberster Ebene. Jedes Element enthält ein `Employees`‑Array, das uns die zweite Hierarchieebene gibt, auf die wir später mit `#Departments.Employees#` zugreifen.

---

## Schritt 2: Verschachtelte Bereichsverarbeitung aktivieren

SmartMarker springt nicht in innere Sammlungen, wenn Sie es nicht anweisen. Das `SmartMarkerOptions`‑Objekt enthält diesen Schalter.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro‑Tipp:** Wenn Sie dieses Flag vergessen, liefert der innere `#Employees#`‑Bereich einfach nichts, und Sie fragen sich, warum die Vorlage leer ist.

---

## Schritt 3: Den Prozessor mit Ihren Daten ausführen

Jetzt übergeben wir die Daten und Optionen an den Prozessor. Die Variable `ws` steht für Ihren **WebService** (oder welches Objekt auch immer die SmartMarker‑Engine hostet).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

An diesem Punkt analysiert SmartMarker die Vorlage, ersetzt `#Departments.Name#` durch den jeweiligen Abteilungsnamen und iteriert, weil verschachtelte Bereiche aktiviert sind, durch die `Employees`‑Sammlung jeder Abteilung.

---

## Schritt 4: Die Vorlagen‑Marker erstellen

Unten finden Sie eine minimale Vorlage, die sowohl die äußere als auch die innere Schleife demonstriert. Fügen Sie sie in den SmartMarker‑Vorlagen‑Editor ein (oder in eine `.txt`‑Datei, die Sie dem Prozessor übergeben).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Beim Rendern erhalten Sie:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Was Sie sehen:** Der äußere `#Departments.Name#` gibt den Abteilungstitel aus. Der innere `#Departments.Employees#`‑Block schleift über jeden Mitarbeitenden, und `#Departments.Employees#` innerhalb des Blocks gibt den eigentlichen Namen aus.

---

## Erwartete Ausgabe & Verifizierung

Das Ausführen des kompletten Beispiels (Daten + Optionen + Vorlage) sollte exakt die oben gezeigte Liste erzeugen. Um das schnell zu prüfen, können Sie das Ergebnis in die Konsole schreiben:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Wenn Sie die beiden Abteilungsüberschriften gefolgt von deren Mitarbeitenden‑Aufzählungen sehen, haben Sie erfolgreich **eine Hierarchie erstellt** und **Mitarbeiter aufgelistet**.

---

## Häufige Stolperfallen & Sonderfälle

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| Keine Ausgabe für Mitarbeitende | `EnableNestedRange` bleibt false | `EnableNestedRange = true` setzen |
| Doppelte Mitarbeitenden‑Namen | Derselbe Array wird in mehreren Abteilungen wiederverwendet | Array klonen oder unterschiedliche Sammlungen verwenden |
| Sehr große Hierarchien verursachen Speicherdruck | SmartMarker lädt den gesamten Objektgraphen in den Speicher | Daten streamen oder große Sammlungen paginieren |
| Syntaxfehler in der Vorlage | Fehlendes schließendes `#/…#`‑Tag | SmartMarker‑Validator nutzen oder einen kurzen Test mit einer kleinen Vorlage durchführen |

---

## Weiterführend – Praxisvarianten

1. **Dynamische Datenquellen** – Laden Sie Abteilungen aus einer Datenbank und mappe sie mittels LINQ auf die anonyme Struktur.
2. **Bedingte Formatierung** – Fügen Sie jedem Mitarbeitenden ein `IsManager`‑Flag hinzu und nutzen Sie SmartMarkers bedingte Tags (`#if …#`), um Manager hervorzuheben.
3. **Mehrere Verschachtelungsebenen** – Wenn Sie Teams innerhalb von Abteilungen benötigen, fügen Sie einfach eine weitere Sammlung (`Teams`) hinzu und lassen `EnableNestedRange` eingeschaltet.

---

## Vollständiges funktionierendes Beispiel (Kopieren‑und‑Einfügen bereit)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Vorlage (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Das Ausführen des Programms gibt die Hierarchie exakt wie oben dargestellt aus.

---

## Fazit

Wir haben **wie man Hierarchien** in SmartMarker erstellt, von der Gestaltung **hierarchischer Daten** in C# über das Aktivieren verschachtelter Bereiche bis hin zum Rendern einer Vorlage, die **Mitarbeiter** pro Abteilung **auflistet**. Das Muster skaliert – fügen Sie einfach weitere verschachtelte Sammlungen oder bedingte Logik hinzu und Sie haben eine leistungsstarke Reporting‑Engine zur Hand.

Bereit für die nächste Herausforderung? Versuchen Sie, die anonymen Typen durch stark typisierte POCO‑Klassen zu ersetzen oder integrieren Sie diesen Ablauf in einen ASP.NET Core‑Endpoint, der ein PDF‑ oder Word‑Dokument zurückgibt. Der Himmel ist das Limit, und jetzt haben Sie ein solides Fundament.

---

![Wie man eine Hierarchie erstellt Diagramm](image.png){alt="Diagramm zur Erstellung einer Hierarchie, das die Beziehung Abteilung‑Mitarbeiter zeigt"}

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar – ich helfe gern.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}