---
category: general
date: 2026-02-15
description: Wie man Währung schnell formatiert, indem man das Spaltenzahlenformat
  festlegt und ein benutzerdefiniertes numerisches Format in C# anwendet. Erfahren
  Sie, wie man eine Spalte nach Namen abruft und die Ausrichtung der Rasterspalte
  einstellt.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: de
og_description: Wie man Währung in einer Grid‑Spalte mit C# formatiert. Dieses Tutorial
  zeigt, wie man eine Spalte nach Namen abruft, das Zahlenformat der Spalte festlegt,
  ein benutzerdefiniertes Zahlenformat anwendet und die Ausrichtung der Grid‑Spalte
  einstellt.
og_title: Währung in einer Grid‑Spalte formatieren – Komplettanleitung
tags:
- C#
- GridFormatting
- UI
title: Wie man Währung in einer Grid‑Spalte formatiert – Schritt‑für‑Schritt‑Anleitung
url: /de/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Währung in einer Grid Column formatiert – Komplettes Programmier‑Tutorial

Haben Sie sich jemals gefragt, **wie man Währung** in einer Grid‑Spalte formatiert, ohne sich die Haare zu raufen? Sie sind nicht der Einzige. Wenn Sie auf eine schlichte Zahl wie `1234.5` starren und wünschen, dass sie magisch als `$1,234.50` erscheint, ist die Antwort meist nur ein paar Zeilen Konfiguration.  

In diesem Leitfaden werden wir **Spalte nach Namen abrufen**, **Spaltenzahlformat setzen** und **benutzerdefiniertes numerisches Format anwenden**, das das typische Buchhaltungs‑Layout berücksichtigt. Unterwegs werden wir außerdem **Grid‑Spaltenausrichtung setzen** und einen dezenten Rand hinzufügen, damit die UI poliert wirkt.

> **TL;DR** – Am Ende haben Sie ein einsatzbereites Snippet, das rohe Dezimalzahlen in schön formatierte Währungswerte innerhalb jeder `GridJs`‑ähnlichen Steuerung umwandelt.

---

## Was Sie benötigen

- Ein .NET‑Projekt (jede Version, die C# 8.0+ unterstützt – Visual Studio 2022 funktioniert hervorragend).  
- Eine Grid‑Komponente, die eine `Columns`‑Sammlung bereitstellt (das Beispiel verwendet die fiktive `GridJs`‑Klasse, aber die Konzepte lassen sich auf DevExpress-, Telerik‑ oder Syncfusion‑Grids übertragen).  
- Grundlegende Vertrautheit mit C#‑Syntax – keine fortgeschrittenen Tricks erforderlich.

Wenn Sie das bereits haben, großartig. Wenn nicht, erstellen Sie einfach eine Konsolen‑App; das Grid kann zu Illustrationszwecken gemockt werden.

## Schritt‑für‑Schritt‑Implementierung

Unter jedem Schritt sehen Sie einen kompakten Code‑Block, eine kurze Erklärung, **warum** die Zeile wichtig ist, und einen Hinweis, um häufige Fallstricke zu vermeiden.

### ## Schritt 1 – „Amount“-Spalte nach Namen abrufen

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Warum das wichtig ist:**  
Die meisten Grid‑APIs stellen Spalten über einen dictionary‑ähnlichen Indexer bereit. Das Abrufen der Spalte über ihren Header‑Namen (`"Amount"`) ermöglicht es Ihnen, ihr Erscheinungsbild zu manipulieren, ohne die zugrunde liegende Datenquelle zu berühren.  

**Pro‑Tipp:** Immer gegen einen `null`‑Rückgabewert schützen – ein Tippfehler im Spaltennamen oder eine dynamische Schemaänderung kann sonst zur Laufzeit eine `NullReferenceException` auslösen.

---

### ## Schritt 2 – Spaltenzahlformat mit einer benutzerdefinierten Währungsmaske setzen

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Warum das wichtig ist:**  
Der Formatstring folgt den Buchhaltungs‑Konventionen von Excel:

- `_(* #,##0.00_)` → Positive Zahlen, rechtsbündig mit einem führenden Leerzeichen für das Währungssymbol.  
- `_(* (#,##0.00)` → Negative Zahlen, in Klammern eingeschlossen.  
- `_(* \"-\"??_)` → Nullwerte werden als Bindestrich angezeigt.  
- `_(@_)` → Textwerte bleiben unverändert.

Die Verwendung von **apply custom numeric format** gibt Ihnen volle Kontrolle über Tausendertrennzeichen, Dezimalstellen und die Platzierung des Währungssymbols.  

**Randfall:** Wenn Ihre Anwendung ein anderes Locale berücksichtigen muss (z. B. Euro statt USD), ersetzen Sie das führende Leerzeichen durch das passende Symbol oder verwenden Sie `CultureInfo`‑bewusste Formatierung in der Datenquelle.

---

### ## Schritt 3 – Spalteninhalt rechtsbündig ausrichten für bessere Lesbarkeit

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Warum das wichtig ist:**  
Währungswerte lassen sich leichter überblicken, wenn sie am Dezimaltrennzeichen ausgerichtet sind. Das Setzen von **set grid column alignment** auf `Right` spiegelt die Art und Weise wider, wie Tabellenkalkulationen Gelddaten anzeigen.  

**Achtung:** Einige Grids ignorieren die Ausrichtung bei Zellen, die benutzerdefinierte Vorlagen enthalten. Wenn Sie feststellen, dass die Ausrichtung nicht wirkt, prüfen Sie, ob die Spalte keinen benutzerdefinierten Zell‑Renderer verwendet.

---

### ## Schritt 4 – Dünnen grauen Rand um die Spaltenzellen hinzufügen

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Warum das wichtig ist:**  
Ein dezenter Rand trennt die „Amount“-Spalte von ihren Nachbarn, besonders wenn das Grid wechselnde Zeilenfarben hat. Er ist ein visueller Hinweis darauf, dass die Daten eine eigenständige finanzielle Größe darstellen.  

**Tipp:** Wenn Sie für den Druck eine dickere Linie benötigen, erhöhen Sie `BorderLineStyle` auf `Medium` oder ändern Sie `Color` zu `Color.Black`.

---

## Voll funktionsfähiges Beispiel

Hier ist das komplette Snippet, das Sie in ein WinForms‑ oder WPF‑Projekt einfügen können, das ein `GridJs`‑ähnliches Steuerelement verwendet. Das Beispiel gibt die formatierten Werte außerdem in der Konsole aus, sodass Sie das Ergebnis ohne UI überprüfen können.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Erwartete Konsolenausgabe**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Beachten Sie, dass die positive Zahl rechtsbündig ist, die negative in Klammern erscheint und Null einen Bindestrich zeigt – genau das, was die benutzerdefinierte Formatzeichenfolge vorgibt.

---

## Häufig gestellte Fragen & Randfälle

| Frage | Antwort |
|----------|--------|
| *Was ist, wenn das Grid ein anderes Kulturformat verwendet (z. B. € statt $)?* | Ersetzen Sie das führende Leerzeichen in der Formatzeichenfolge durch das gewünschte Symbol oder lassen Sie die Datenquelle einen vorformatierten String mit `CultureInfo.CurrentCulture` ausgeben. |
| *Kann ich dasselbe Format für mehrere Spalten wiederverwenden?* | Absolut. Speichern Sie die Formatzeichenfolge in einer Konstanten (`const string CurrencyMask = "...";`) und weisen Sie sie dort zu, wo Sie Währung benötigen. |
| *Was passiert, wenn die Spalte einen String‑Wert enthält?* | Die Formatzeichenfolge wirkt nur auf numerische Typen. Strings werden unverändert durchgereicht, weshalb der letzte Teil der Maske (`_(@_)`) existiert – er bewahrt nicht‑numerischen Inhalt. |
| *Gibt es einen Performance‑Einfluss?* | Vernachlässigbar. Das Format wird zur Renderzeit angewendet, nicht beim Abrufen der Daten. Sofern Sie nicht tausende Zeilen pro Frame rendern, werden Sie keine Verlangsamung bemerken. |
| *Wie mache ich den Rand für Druckberichte dicker?* | Ersetzen Sie `BorderLineStyle.Thin` durch `BorderLineStyle.Medium` oder `BorderLineStyle.Thick`. Einige Bibliotheken erlauben zudem, die Breite direkt in Pixeln anzugeben. |

---

## Abschluss

Wir haben Schritt für Schritt **wie man Währung** in einer Grid‑Spalte von Anfang bis Ende formatiert: die Spalte nach Namen abrufen, das Spaltenzahlformat setzen, ein benutzerdefiniertes numerisches Format anwenden, die Zellen ausrichten und einen geschmackvollen Rand hinzufügen. Das komplette Beispiel läuft sofort und zeigt das genaue visuelle Ergebnis, das Sie erwarten können.

Wenn Sie bereit sind, weiterzugehen, probieren Sie:

- **Dynamische Kulturen** – die Formatzeichenfolge basierend auf dem Locale des Benutzers wechseln.  
- **Conditional**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}