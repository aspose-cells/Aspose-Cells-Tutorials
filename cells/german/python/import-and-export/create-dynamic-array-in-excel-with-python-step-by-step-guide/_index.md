---
category: general
date: 2026-06-21
description: Erstelle ein dynamisches Array mit Python und der SEQUENCE‑Funktion in
  Excel. Lerne, das Formel‑Ergebnis zu lesen, Excel‑Formeln neu zu berechnen, und
  sieh dir ein Beispiel für die Excel‑SEQUENCE‑Funktion an.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: de
og_description: Erstelle ein dynamisches Array in Excel mit Python. Dieses Tutorial
  zeigt, wie man die SEQUENCE‑Funktion verwendet, Excel‑Formeln neu berechnet und
  das Ergebnis einer Formel ausliest.
og_title: Dynamisches Array in Excel mit Python erstellen – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Dynamisches Array in Excel mit Python erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dynamisches Array in Excel mit Python erstellen – Komplett‑Anleitung

Haben Sie sich schon einmal gefragt, wie Sie **dynamische Array**‑Formeln in Excel erstellen können, ohne Ihr Python‑Skript zu verlassen? Sie sind nicht allein. Egal, ob Sie einen Monatsbericht automatisieren oder eine leichte Daten‑Engine bauen – ein `SEQUENCE`‑Formel in ein Workbook zu schreiben, neu zu berechnen und den Spill‑Bereich zurück nach Python zu holen, ist ein echter Game‑Changer.

In diesem Tutorial gehen wir Schritt für Schritt durch ein praxisnahes **Excel‑Sequence‑Beispiel**, zeigen Ihnen, wie Sie **Formelergebnis lesen** und erklären die beste Methode, **Excel‑Formeln neu zu berechnen**, nachdem Sie neue Logik injiziert haben. Am Ende haben Sie ein eigenständiges Skript, das Sie kopieren‑einfügen, ausführen und an Ihre Bedürfnisse anpassen können.

## Was Sie lernen werden

- Wie die `SEQUENCE`‑Funktion funktioniert und warum sie sich perfekt zum Erzeugen von Matrizen eignet.
- Der Unterschied zwischen einem regulären Zellenwert und einer Spill‑Bereich‑Adresse.
- Verwendung von `wb.calculate_formula()` (oder dem entsprechenden Aufruf), um Excel zu zwingen, neue Formeln zu evaluieren.
- Extrahieren der Adresse eines dynamischen Arrays mit `ANCHORARRAY`.
- Ein vollständiges, ausführbares Python‑Beispiel, das Sie in jedes Projekt einbinden können.

Vorkenntnisse mit der neuen dynamischen Array‑Engine von Excel sind nicht nötig – nur Grundkenntnisse in Python und einer Bibliothek wie **xlwings**, die mit Excel kommunizieren kann.

---

## Wie man ein dynamisches Array mit SEQUENCE in Excel mittels Python erstellt

Der erste Schritt besteht darin, eine **dynamische Array**‑Formel direkt in eine Arbeitsblattzelle zu schreiben. In modernem Excel kann die `SEQUENCE`‑Funktion eine Matrix von Zahlen „on the fly“ erzeugen. Hier ist die Syntax, die wir verwenden:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Warum `SEQUENCE`?**  
Man kann es sich wie das eingebaute `range()` von Excel vorstellen. Sie können Zeilen, Spalten, einen Startwert und einen Inkrementwert in einer einzigen Zeile angeben. In unserem Fall verlangen wir 3 Zeilen und 2 Spalten, beginnend bei 10 und mit einer Schrittweite von 5, was folgendes Ergebnis liefert:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Da die Formel in `A1` steht, „spült“ Excel das Ergebnis automatisch in die benachbarten Zellen `A1:B3`. Dieser Spill‑Bereich ist das, was wir später abrufen.

---

## Verwendung der SEQUENCE‑Funktion in Excel – Ein schnelles Excel‑Sequence‑Beispiel

Wenn Sie Excel manuell öffnen und `=SEQUENCE(3,2,10,5)` in eine Zelle eingeben, erscheint sofort dieselbe Matrix. Die Funktion ist Teil der **dynamic array**‑Engine von Excel, die mit Office 365 eingeführt wurde, und bedeutet:

- Kein Bedarf an Ctrl+Shift+Enter.
- Das Ergebnis kann sich automatisch ausdehnen oder zusammenziehen.
- Sie können den gesamten Spill‑Bereich mit Funktionen wie `@` oder `#` referenzieren.

In Python besteht der einzige Unterschied darin, dass wir die Formel als Zeichenkette der `.formula`‑Eigenschaft der Zelle zuweisen. Die Bibliothek übernimmt den Rest.

---

## Abrufen der Spill‑Bereich‑Adresse mit ANCHORARRAY

Sobald das dynamische Array steht, müssen Sie häufig wissen, wo Excel die Werte tatsächlich abgelegt hat. Hier kommt `ANCHORARRAY` ins Spiel. Es liefert die Adresse der oberen linken Zelle des Spill‑Bereichs – genau das, was wir zurück in unser Skript lesen müssen.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Wird diese Formel in `C1` platziert, erhalten wir einen Text wie `"A1:B3"`. Beachten Sie, dass wir **das Formelergebnis** als reinen Wert lesen, nicht als weitere Formel. Dieser kleine Trick erspart das manuelle Parsen des Arbeitsblatts.

---

## Excel‑Formeln neu berechnen und das Ergebnis lesen

Excel berechnet nicht immer sofort neu, wenn eine neue Formel von einem externen Skript injiziert wird. Um sicherzustellen, dass das Workbook die neuesten Änderungen widerspiegelt, lösen wir explizit einen Berechnungslauf aus.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Warum `calculate_formula()` aufrufen?**  
Wenn Sie diesen Schritt überspringen, könnte `ws.cells["C1"].value` immer noch `None` oder eine alte Adresse zurückgeben, weil Excel noch dabei ist, den Abhängigkeits‑Baum zu aktualisieren. Durch das Erzwingen einer Neuberechnung stellen wir sicher, dass das **gelesene Formelergebnis** aktuell ist.

---

## Vollständiges Skript – Von Anfang bis Ende

Im Folgenden finden Sie ein komplettes, sofort ausführbares Beispiel, das alles zusammenführt. Es setzt voraus, dass **xlwings** installiert ist (`pip install xlwings`) und dass Excel auf Ihrem Rechner verfügbar ist.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Erwartete Ausgabe

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Beim Ausführen des Skripts wird Excel geöffnet, die `SEQUENCE`‑Formel injiziert, neu berechnet und anschließend sowohl die Spill‑Adresse als auch die Matrix selbst ausgegeben. Keine manuellen Klicks nötig.

---

## Häufige Stolperfallen und Profi‑Tipps

- **Stolperfalle:** Vergessen von `wb.calculate_formula()`.  
  *Ergebnis:* `C1` bleibt leer oder zeigt eine veraltete Adresse.  
  *Lösung:* Nach dem Schreiben neuer Formeln immer eine Berechnung auslösen.

- **Stolperfalle:** Verwendung einer älteren Excel‑Version, die die `SEQUENCE`‑Funktion nicht kennt.  
  *Ergebnis:* `#NAME?`‑Fehler.  
  *Lösung:* Sicherstellen, dass Sie Office 365 oder Excel 2021+ besitzen.

- **Pro‑Tipp:** Wenn Sie den Spill‑Bereich für weitere Verarbeitung benötigen (z. B. für Diagramme), können Sie die Adresse direkt in `ws.range(spill_address)` verwenden, wie oben gezeigt.

- **Pro‑Tipp:** `ANCHORARRAY` funktioniert mit jedem dynamischen Array, nicht nur mit `SEQUENCE`. Ersetzen Sie die Formel durch `=SORT(A2:A10)` oder `=FILTER(...)` und Sie erhalten weiterhin die korrekte Spill‑Adresse.

- **Randfall:** Wenn der Zielbereich bereits belegt ist, gibt Excel einen `#SPILL!`‑Fehler zurück. In diesem Fall sollten Sie entweder den Zielbereich vorher leeren oder die Formel in eine andere Zelle verschieben.

---

## Erweiterung des Beispiels – Was kommt als Nächstes?

Jetzt, wo Sie wissen, wie man **dynamische Array**‑Formeln erstellt, **Formelergebnis liest** und **Excel‑Formeln neu berechnet**, können Sie komplexere Szenarien erkunden:

- **Dynamische Diagrammdaten** – einen Spill‑Bereich als Datenquelle für ein Diagramm verwenden und das Diagramm automatisch wachsen lassen.
- **Bedingte Formatierung** – Regeln auf den Spill‑Bereich anhand seiner Adresse anwenden.
- **Arbeitsbuch‑übergreifende Verweise** – ein dynamisches Array in einem Workbook schreiben und die Daten über `xlwings`‑Links in ein anderes Workbook ziehen.

All dies baut auf den hier behandelten Kernkonzepten auf, also experimentieren Sie gern. Die einzige Grenze ist Ihre Vorstellungskraft (und eventuell die maximalen Zeilen/Spalten von Excel).

---

## Fazit

Wir haben einen kompletten Workflow durchlaufen, um **dynamische Array**‑Formeln in Excel aus Python zu erstellen, die **SEQUENCE‑Funktion** zu nutzen, den Spill‑Bereich mit **ANCHORARRAY** abzurufen, **Excel‑Formeln neu zu berechnen** und schließlich das **Formelergebnis** zurück ins Skript zu lesen. Das kurze Beispiel zeigt, wie mächtig die neue dynamische Array‑Engine von Excel sein kann, wenn sie mit Automatisierungstools wie **xlwings** kombiniert wird.

Probieren Sie es in Ihren eigenen Projekten aus, ändern Sie die Matrix‑Dimensionen oder ersetzen Sie `SEQUENCE` durch eine andere dynamische Funktion. Sobald Sie sich damit vertraut gemacht haben, wird die Automatisierung von Excel nicht nur möglich, sondern auch angenehm unkompliziert.

Haben Sie Fragen oder möchten Sie teilen, wie Sie dieses Muster erweitert haben? Hinterlassen Sie einen Kommentar unten – happy coding!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Features zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}