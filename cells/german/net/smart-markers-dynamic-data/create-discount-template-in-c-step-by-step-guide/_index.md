---
category: general
date: 2026-02-14
description: Erstellen Sie schnell eine Rabattvorlage und lernen Sie, wie Sie Rabatte
  in einer Tabelle anwenden, Daten in die Vorlage einfügen und einen variablen Präfix
  für Smart Marker definieren.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: de
og_description: Erstelle eine Rabattvorlage mit C#. Lerne, Rabatte in einer Tabelle
  anzuwenden, Daten in die Vorlage zu injizieren und ein variables Präfix für Smart
  Marker zu definieren.
og_title: Discount‑Vorlage erstellen – Vollständiger C#‑Leitfaden
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Rabattvorlage in C# erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rabattvorlage erstellen – Vollständige C# Anleitung

Haben Sie jemals eine **create discount template** für einen Verkaufsbericht benötigt, wussten aber nicht, wie Sie die Zahlen automatisch in eine Tabelle einfügen können? Sie sind nicht allein. In diesem Tutorial zeigen wir Ihnen genau, wie Sie **create discount template** erstellen, dann **apply discount in spreadsheet** Zellen anwenden, **inject data into template** einfügen und sogar **define variable prefix** für Ihre Smart Marker festlegen – alles mit sauberem C#‑Code.

Wir beginnen mit einer Darstellung des Problems und springen dann direkt zu einer funktionierenden Lösung, die Sie copy‑paste können. Am Ende haben Sie ein wiederverwendbares Muster, das funktioniert, egal ob Sie Rechnungen, Preislisten oder irgendeine Tabelle erstellen, die dynamische Rabatte benötigt.

---

## Was Sie lernen werden

- Wie man eine rabatt‑bewusste Tabellenvorlage entwirft.
- Wie man ein benutzerdefiniertes `VariablePrefix` / `VariableSuffix` konfiguriert, damit Marker leicht zu erkennen sind.
- Wie man ein anonymes Objekt (`discountData`) an den `SmartMarkerProcessor` übergibt.
- Wie die resultierende Formel (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automatisch den Endpreis berechnet.
- Tipps zum Umgang mit Sonderfällen wie Zeilen ohne Rabatt oder mehreren Rabattstufen.

**Voraussetzungen** – ein aktuelles .NET‑Runtime (≥ .NET 6), ein Verweis auf die `Aspose.Cells`‑Bibliothek (oder ähnlich), die `SmartMarkerProcessor` bereitstellt, sowie ein grundlegendes Verständnis der C#‑Syntax. Nichts Exotisches.

---

## Schritt 1: Rabattvorlage in Ihrer Tabelle erstellen

Öffnen Sie zunächst eine neue Arbeitsmappe (oder verwenden Sie eine vorhandene) und platzieren Sie einen Platzhalter dort, wo der Rabatt angewendet werden soll. Betrachten Sie die Vorlage als eine einfache Excel‑Datei mit „Smart Markern“, die der Prozessor ersetzt.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Warum das wichtig ist:** Durch das Einbetten von `#Discount#` in die Formel teilen wir dem Prozessor genau mit, wo der Rabattwert hin gehört. Der `SmartMarkerProcessor` ersetzt `#Discount#` später durch die von Ihnen bereitgestellte Zahl und lässt den Rest der Formel unverändert.

---

## Schritt 2: Variablenpräfix für Smart Marker definieren

Standardmäßig suchen viele Bibliotheken nach `${Variable}` oder `{{Variable}}`. In unserem Fall wollen wir einen sauberen, menschenlesbaren Marker, daher **define variable prefix** und das Suffix explizit.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro‑Tipp:** Die Verwendung von `#` hält die Marker kurz und leicht in der Excel‑Formelleiste zu erkennen. Wenn Sie Kollisionen mit bestehenden Excel‑Funktionen vermeiden müssen, wählen Sie ein anderes Paar (z. B. `[[` und `]]`).

---

## Schritt 3: Daten in die Vorlage einfügen mit SmartMarkerProcessor

Jetzt übergeben wir den tatsächlichen Rabattwert. Der Prozessor scannt das Arbeitsblatt, findet jedes `#Discount#` und ersetzt es durch den Wert des anonymen Objekts, das wir übergeben.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Nach diesem Aufruf sieht die Formel in `B2` folgendermaßen aus:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Wenn die Arbeitsmappe berechnet, zeigt `B2` **90** an, d. h. einen 10 %‑Rabatt auf den ursprünglichen Preis von 100.

**Warum es funktioniert:** `StartSmartMarkerProcessing` durchläuft jede Zelle, sucht nach dem Token `#Discount#` und ersetzt ihn durch den numerischen Wert. Da das Token in einer `IF`‑Anweisung steht, verarbeitet die Tabelle weiterhin Fälle, in denen der Rabatt null sein könnte.

---

## Schritt 4: Rabatt in der Tabelle anwenden – Ergebnis überprüfen

Lassen Sie uns die Berechnung auslösen und den Endpreis in der Konsole ausgeben. Dieser Schritt beweist, dass der **apply discount in spreadsheet**‑Ablauf erfolgreich war.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Erwartete Ausgabe**

```
Original: 100
Discounted (10%): 90
```

Wenn Sie `discountData.Discount` auf `0.25` ändern und den Prozessor erneut ausführen, wird die Ausgabe automatisch einen 25 %‑Rabatt widerspiegeln – kein zusätzlicher Code nötig.

---

## Schritt 5: Sonderfälle & mehrere Rabatte behandeln

### Zeilen ohne Rabatt

Manchmal ist ein Produkt nicht im Angebot. Um die Formel robust zu halten, deckt das `IF`, das Sie zuvor eingefügt haben, diesen Fall bereits ab: Wenn `#Discount#` `0` ist, wird der ursprüngliche Preis unverändert übernommen.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Mehrere Rabattspalten

Wenn Sie für jede Zeile separate Rabatte benötigen, geben Sie jeder Zeile ihren eigenen Marker, z. B. `#Discount1#`, `#Discount2#`, und übergeben Sie eine Sammlung:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Der Prozessor ordnet die Marker sequenziell zu, sodass jede Zeile den richtigen Wert erhält.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, copy‑ready Programm, das alle oben genannten Schritte integriert. Speichern Sie es als `Program.cs`, fügen Sie einen Verweis auf `Aspose.Cells` hinzu und führen Sie es aus.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Beim Ausführen werden die erwarteten Zahlen ausgegeben und eine `DiscountedPricing.xlsx`‑Datei erzeugt, die Sie in Excel öffnen können, um die bereits aufgelöste Formel zu sehen.

---

## Fazit

Sie wissen jetzt, wie man **create discount template**, **apply discount in spreadsheet**, **inject data into template** und **define variable prefix** für Smart Marker verwendet – alles mit ein paar prägnanten C#‑Zeilen. Das Muster skaliert – ändern Sie einfach das anonyme Objekt oder übergeben Sie eine Sammlung für Massen‑Updates, und dieselbe Vorlage verarbeitet jedes Rabatt‑Szenario, das Sie ihr geben.

Bereit für die nächste Stufe? Versuchen Sie:

- Steuerberechnungen neben den Rabatten hinzufügen.
- Rabatt‑Prozentsätze aus einer Datenbank statt hartkodiert beziehen.
- Bedingte Formatierung verwenden, um Zeilen mit hohen Rabatten hervorzuheben.

Diese Erweiterungen erhalten die Kernidee, erweitern jedoch die Nützlichkeit Ihrer Rabattvorlage.

Haben Sie Fragen oder ein cooles Anwendungsbeispiel? Hinterlassen Sie unten einen Kommentar und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}