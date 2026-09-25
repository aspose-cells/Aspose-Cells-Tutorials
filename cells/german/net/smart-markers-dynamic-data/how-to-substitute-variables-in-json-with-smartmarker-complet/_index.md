---
category: general
date: 2026-03-29
description: Wie man Variablen in JSON mit SmartMarker ersetzt – lerne, if‑Ausdrücke
  zu verwenden, bedingte Logik anzuwenden, Werte zu multiplizieren und JSON mühelos
  zu erzeugen.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: de
og_description: Wie man Variablen in JSON mit SmartMarker ersetzt. Entdecken Sie,
  wie man If‑Ausdrücke verwendet, bedingte Logik anwendet, Werte multipliziert und
  JSON in Minuten generiert.
og_title: Wie man Variablen in JSON mit SmartMarker ersetzt – Schritt für Schritt
tags:
- C#
- SmartMarker
- JSON templating
title: Wie man Variablen in JSON mit SmartMarker ersetzt – Vollständige Anleitung
url: /de/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Variablen in JSON mit SmartMarker ersetzt – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man Variablen** in einer JSON‑Payload ersetzt, ohne einen eigenen Parser zu schreiben? Sie sind nicht allein. In vielen Integrationsszenarien – denken Sie an Rechnungen, Preis‑Engines oder dynamische Konfigurationsdateien – müssen Sie Laufzeitwerte einfügen, einfache Bedingungen anwenden und vielleicht sogar eine schnelle Multiplikation durchführen. Dieses Tutorial zeigt Ihnen genau **wie man Variablen** mit der SmartMarker‑Bibliothek ersetzt, und das, während das JSON sauber und lesbar bleibt.

Wir gehen ein praxisnahes Beispiel durch, das **if‑Ausdruck verwenden**, **wie man Bedingungen anwendet**, **wie man Werte multipliziert** und **wie man JSON** on the fly erzeugt. Am Ende haben Sie ein sofort ausführbares C#‑Snippet, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie lernen werden

- `SmartMarkerOptions` einrichten, um wiederverwendbare Variablen zu speichern.  
- Eine JSON‑Vorlage schreiben, die einen `if`‑Ausdruck für bedingte Logik enthält.  
- Einen Wert innerhalb der Vorlage mit einer Variablen multiplizieren.  
- Die Vorlage mit `SmartMarkerProcessor` verarbeiten und den finalen JSON‑String erhalten.  
- Häufige Fallstricke beheben, wie fehlende Variablen oder fehlerhafte Ausdrücke.

Keine externen Dienste, keine schweren Abhängigkeiten – nur reines C# und das SmartMarker‑NuGet‑Paket.

---

## Wie man Variablen ersetzt – Schritt‑für‑Schritt‑Übersicht

Unten sehen Sie eine schematische Darstellung des Workflows. Stellen Sie sich das als Pipeline vor, bei der Ihre rohe JSON‑Vorlage links eingibt, die SmartMarker‑Engine ihre Magie wirkt und das vollständig gerenderte JSON rechts ausgegeben wird.

![Diagramm, das zeigt, wie Variablen in JSON ersetzt werden](https://example.com/images/smartmarker-flow.png "Wie man Variablen in JSON ersetzt")

*Bildbeschreibung: Diagramm, das zeigt, wie Variablen in JSON ersetzt werden.*

---

## Schritt 1: SmartMarker installieren und importieren

Bevor Sie beginnen, stellen Sie sicher, dass das SmartMarker‑Paket in Ihrem Projekt referenziert ist. Wenn Sie die .NET‑CLI verwenden, führen Sie aus:

```bash
dotnet add package SmartMarker
```

Fügen Sie anschließend die erforderlichen `using`‑Direktiven am Anfang Ihrer C#‑Datei hinzu:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Profi‑Tipp:** Die neueste Version (Stand März 2026) ist 2.4.1. Sie unterstützt .NET 6 und höher, funktioniert aber auch einwandfrei mit .NET Framework 4.7.

---

## Schritt 2: SmartMarker‑Optionen erstellen und Variablen definieren

Jetzt erstellen wir eine Instanz von `SmartMarkerOptions`, die alle Variablen enthält, die wir in der Vorlage wiederverwenden möchten. Hier beantworten wir die Frage **wie man Variablen ersetzt** – die Variablen fungieren als Platzhalter, die SmartMarker später ersetzt.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Warum den Satz in `Variables` speichern statt ihn fest zu codieren? Weil Sie diese Zahl möglicherweise aus einer Datenbank, einer Konfigurationsdatei oder einer Benutzereingabe beziehen. In den Optionen zu halten macht die Vorlage wiederverwendbar und testbar.

---

## Schritt 3: JSON‑Vorlage mit einem `if`‑Ausdruck schreiben

Hier kommt das Schlüsselwort **use if expression** zum Einsatz. SmartMarker ermöglicht es, bedingte Logik direkt im JSON‑String einzubetten. Die Syntax sieht ein wenig wie ein Property‑Name aus, aber SmartMarker behandelt sie als Anweisung.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Beachten Sie den Schlüssel `if(Amount>500)`. SmartMarker wertet den Ausdruck `Amount>500` aus; ist er wahr, wird der entsprechende Wert (`${Amount * Rate}`) in die Ausgabe eingefügt. Die `${...}`‑Syntax ist die *Variable‑Substitutions‑Engine* – hier **wie man Werte multipliziert** (`Amount * Rate`), bevor das Ergebnis eingefügt wird.

---

## Schritt 4: Vorlage verarbeiten und das finale JSON abrufen

Mit den Optionen und der Vorlage bereit, übergeben wir alles an den Prozessor. Die Methode `ProcessJson` parsed die Vorlage, wendet die Bedingung an, führt die Multiplikation aus und gibt einen sauberen JSON‑String zurück.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Running the snippet prints:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Was ist passiert?**  
- `Amount` ist 1000, was `Amount>500` erfüllt.  
- SmartMarker wertet `${Amount * Rate}` aus → `1000 * 0.08 = 80`.  
- Der ursprüngliche bedingte Schlüssel (`if(Amount>500)`) wird durch einen sauberen Property‑Namen (`Result`) ersetzt. Standardmäßig verwendet SmartMarker `"Result"`, Sie können ihn jedoch anpassen (mehr dazu später).

Wenn Sie `Amount` auf `400` ändern, sieht die Ausgabe folgendermaßen aus:

```json
{
  "Amount": 400
}
```

Der bedingte Block verschwindet, weil der Ausdruck zu `false` ausgewertet wurde. Das ist das Wesentliche von **wie man Bedingungen anwendet** in JSON.

---

## Schritt 5: Anpassen des Ausgabe‑Property‑Namens (optional)

Manchmal möchten Sie nicht den generischen Schlüssel `"Result"` verwenden. SmartMarker ermöglicht es, einen benutzerdefinierten Namen über die Option `RenameIfExpression` anzugeben:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Ausgabe:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

---

## Häufige Stolperfallen und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Variable nicht gefunden | Sie haben eine Variable referenziert, die nicht in `smartMarkerOptions.Variables` enthalten ist. | Rechtschreibung prüfen und sicherstellen, dass die Variable vor der Verarbeitung hinzugefügt wird. |
| Ungültige `if`‑Syntax | Fehlende Klammern oder falscher Operator (`>`, `<`, `==`). | Verwenden Sie exakt das Muster `if(<expression>)`; SmartMarker unterstützt nur einfache numerische Vergleiche. |
| JSON wird fehlerhaft | Durch ein versehentliches Komma nach dem bedingten Block entsteht ein Syntaxfehler. | Lassen Sie SmartMarker die Entfernung übernehmen; halten Sie die ursprüngliche Vorlage syntaktisch korrekt. |
| Unerwartetes Zahlenformat | Das Ergebnis erscheint als String `"80"` statt als Zahl. | Später casten oder parsen, oder `${(Amount * Rate):N0}` für numerische Formatierung verwenden. |

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das komplette Programm, das Sie kompilieren und ausführen können. Es demonstriert **wie man JSON erzeugt** mit dynamischen Variablen, Bedingungen und arithmetischen Operationen – alles in weniger als 30 Zeilen.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Erwartete Konsolenausgabe**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Passen Sie `Amount` gerne an, um den bedingten Zweig zu testen, oder ändern Sie `Rate`, um verschiedene Rabattberechnungen zu sehen.

---

## Das Muster erweitern – Weitere „Wie‑man‑…“-Szenarien

- **Wie man Variablen** aus einer Konfigurationsdatei ersetzt: Laden Sie ein `Dictionary<string, object>` aus `appsettings.json` und übergeben Sie es an `smartMarkerOptions.Variables`.  
- **Wie man if expression** für mehrere Bedingungen verwendet: Verkettung wie `"if(Amount>500 && CustomerType=='VIP')"` – SmartMarker unterstützt logisches UND/ODER.  
- **Wie man conditional** Formatierung anwendet: Verwenden Sie `${Amount:0.00}` im Ausdruck, um Dezimalstellen zu steuern.  
- **Wie man values** multipliziert mit komplexerer Mathematik: `${(Amount - Discount) * TaxRate}` funktioniert genauso.  
- **Wie man json** für verschachtelte Objekte erzeugt: Platzieren Sie den bedingten Block in einem anderen JSON‑Objekt, und SmartMarker erhält die Hierarchie bei.

---

## Fazit

Wir haben **wie man Variablen** in JSON mit SmartMarker ersetzt, **use if expression** für bedingte Einbindung demonstriert, **wie man Bedingungen anwendet** erklärt, **wie man Werte multipliziert** innerhalb einer Vorlage gezeigt und schließlich **wie man JSON** erzeugt, das für nachgelagerte Systeme bereit ist. Der Ansatz ist leichtgewichtig, erfordert keine externe Templating‑Engine und fügt sich nahtlos in jede C#‑Codebasis ein.

Probieren Sie es aus – passen Sie die Variablen an, fügen Sie weitere Bedingungen hinzu oder verpacken Sie das Ganze in eine Hilfsklasse zur Wiederverwendung in Ihrer Lösung. Wenn Sie schnell dynamisches JSON erzeugen müssen, ist SmartMarker eine solide, produktionsreife Option.

---

**Nächste Schritte**

- Vertiefen Sie sich in SmartMarkers erweiterte Funktionen wie Schleifen (`foreach`) und benutzerdefinierte Funktionen.  
- Kombinieren Sie diese Technik mit ASP.NET‑Core‑Endpoints, um dynamische JSON‑APIs bereitzustellen.  
- Erkunden Sie andere Templating‑Bibliotheken (z. B. Handlebars.NET) zum Vergleich, besonders wenn Sie eine umfangreichere Syntax benötigen.

Haben Sie Fragen oder ein konkretes Anwendungsbeispiel, bei dem Sie feststecken? Hinterlassen Sie unten einen Kommentar, und wir lösen das Problem gemeinsam. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}