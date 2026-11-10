---
category: general
date: 2026-10-16
description: Aspose.Cells Formel in Java mit der EXPAND‑Funktion setzen. Lernen Sie
  ein Schritt‑für‑Schritt‑Beispiel und sehen Sie, wie Sie Expand für dynamische Bereiche
  verwenden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: de
lastmod: 2026-10-16
og_description: Aspose.Cells Formel in Java mit der EXPAND‑Funktion setzen. Folgen
  Sie einem vollständigen Beispiel, um Bereiche in Excel‑Arbeitsmappen dynamisch zu
  erweitern.
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells Formel mit EXPAND festlegen – Java‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells Formel mit EXPAND‑Funktion festlegen – vollständiger Java‑Leitfaden
url: /de/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Formel setzen mit EXPAND‑Funktion – vollständige Java‑Anleitung

Wenn Sie programmgesteuert **aspose cells set formula** benötigen, zeigt Ihnen dieses Tutorial genau, wie es geht. Sie lernen, wie Sie die EXPAND‑Funktion verwenden, um einen dynamischen Bereich zu erstellen, der fünf Zeilen und fünf Spalten von einer Ausgangszelle aus erweitert, alles aus Java‑Code.

Die Arbeit mit Excel‑Formeln aus Java ist oft umständlich, aber Aspose.Cells abstrahiert die Komplexität. In den nachfolgenden Abschnitten gehen wir ein vollständiges, ausführbares Beispiel durch, erklären, warum jede Zeile wichtig ist, und untersuchen gängige Variationen wie unterschiedliche Startzellen oder variable Erweiterungsgrößen.

## Was dieses Tutorial abdeckt

* Laden einer bestehenden Arbeitsmappe mit Aspose.Cells  
* Zugriff auf ein Arbeitsblatt und dessen Zellen‑Sammlung  
* **aspose cells set formula** mit der `EXPAND`‑Funktion  
* Neuberechnung der Arbeitsmappe, damit die Formel ausgewertet wird  
* Speichern des Ergebnisses und Überprüfen der Ausgabe  

Keine externen Bibliotheken außer Aspose.Cells sind erforderlich, und der Code läuft auf jeder Java 8+‑Runtime. Am Ende können Sie das Muster für andere dynamische Formeln anpassen.

## Voraussetzungen

* Java Development Kit (JDK) 8 oder neuer  
* Aspose.Cells für Java (Download von der [official site](https://downloads.aspose.com/cells/java))  
* Eine Eingabe‑Excel‑Datei (`input.xlsx`) in einem bekannten Verzeichnis  
* Grundlegende Kenntnisse der Java‑Syntax und von Maven/Gradle für das Abhängigkeits‑Management  

## Schritt 1: Projekt einrichten und Aspose.Cells hinzufügen

Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

Für Gradle lautet das Äquivalent:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Verwenden Sie immer die neueste stabile Version; neuere Releases enthalten Leistungsverbesserungen für die Formelkalkulation.

## Schritt 2: Arbeitsmappe laden

Die erste Zeile unserer Lösung öffnet eine bestehende Arbeitsmappe. Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten Pfad, in dem sich `input.xlsx` befindet.

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Warum das wichtig ist*: Das Laden der Arbeitsmappe erzeugt eine In‑Memory‑Darstellung, die es Ihnen ermöglicht, Arbeitsblätter, Zellen und Formeln zu manipulieren, ohne das Dateisystem erneut zu berühren.

## Schritt 3: Ziel‑Arbeitsblatt und Zellen‑Sammlung zugreifen

Wir arbeiten mit dem ersten Arbeitsblatt (Index 0). Das `Cells`‑Objekt bietet direkten Zugriff auf einzelne Zellen per Adresse.

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

Wenn Sie ein anderes Blatt benötigen, ändern Sie den Index oder verwenden Sie `get("SheetName")`.

## Schritt 4: **aspose cells set formula** – EXPAND‑Funktion anwenden

Jetzt setzen wir die Formel in Zelle **B2**. Die `EXPAND`‑Funktion nimmt drei Argumente: die Referenzzelle, die Anzahl der Zeilen, die erweitert werden sollen, und die Anzahl der Spalten, die erweitert werden sollen.

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### Wie man EXPAND verwendet

* **Referenzzelle (`A2`)** – der Ausgangspunkt des dynamischen Bereichs.  
* **Zeilen (`5`)** – wie viele Zeilen der Bereich nach unten wachsen soll.  
* **Spalten (`5`)** – wie viele Spalten der Bereich nach rechts wachsen soll.

Sie können diese Werte durch Variablen ersetzen, wenn Sie eine flexible Lösung benötigen:

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## Schritt 5: Arbeitsmappe neu berechnen

Nachdem Sie eine Formel gesetzt haben, müssen Sie Aspose.Cells mitteilen, sie auszuwerten. Die Methode `calculateFormula()` verarbeitet alle Formeln in der Arbeitsmappe.

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **Warum neu berechnen?**  
> Ohne diesen Aufruf bleibt die Formel ungeprüft und die Ausgabedatei zeigt die rohe Zeichenkette `=EXPAND(...)` anstelle des erweiterten Arrays.

## Schritt 6: Aktualisierte Arbeitsmappe speichern

Schließlich schreiben Sie die Änderungen in eine neue Datei. Dadurch bleibt die ursprüngliche Arbeitsmappe zum Vergleich erhalten.

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Wenn Sie `output.xlsx` in Excel öffnen, zeigt Zelle **B2** ein 5 × 5‑Block von Werten, die aus dem Bereich kopiert wurden, der bei **A2** beginnt. Enthielt **A2** die Zahl `1`, zeigt der Block in jeder Zelle `1`, weil `EXPAND` den Quellwert über den erweiterten Bereich hinweg repliziert.

## Vollständiger, ausführbarer Quellcode

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Erwartete Ausgabe

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

(Die tatsächlichen Werte hängen davon ab, was `A2` in Ihrer Quelldatei enthält.)

## Häufige Variationen und Sonderfälle

| Szenario | Code‑Änderung | Grund |
|----------|---------------|-------|
| **Andere Startzelle** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | Verwenden Sie jede Zelle als Referenz; die Formel erweitert sich relativ zu dieser Zelle. |
| **Variable Erweiterungsgröße** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | Ermöglicht zur Laufzeit bestimmte Bereiche, nützlich in datengetriebenen Berichten. |
| **Erweiterung mit Größe 0** | `=EXPAND(A2,0,0)` | Gibt nur den ursprünglichen Zellenwert zurück; praktisch für bedingte Logik, bei der die Größe später erhöht werden kann. |
| **Verwendung eines benannten Bereichs** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | Funktioniert, wenn `MyRange` in der Arbeitsmappe definiert ist; hält Formeln lesbar. |

> **Achtung:** Die maximale Array‑Größe von Excel (16 384 Spalten × 1 048 576 Zeilen). Ein Versuch, darüber hinaus zu erweitern, führt zu einem Berechnungsfehler.

## Debugging‑Tipps

* **Formel wird nicht ausgewertet?** Stellen Sie sicher, dass `workbook.calculateFormula();` nach jedem `setFormula` aufgerufen wird.  
* **Unerwartete Werte?** Prüfen Sie, ob die Referenzzelle (`A2` im Beispiel) die Daten enthält, die Sie verbreiten möchten.  
* **Leistungs‑Bedenken** – Große Erweiterungen können kostenintensiv sein. Wenn Sie nur einen Teil benötigen, reduzieren Sie die Zeilen‑/Spalten‑Argumente.

## Fazit

Sie haben nun ein vollständiges **aspose cells set formula**‑Beispiel, das **zeigt, wie man EXPAND** in Java verwendet. Durch Laden einer Arbeitsmappe, Setzen der `EXPAND`‑Formel, Neuberechnung und Speichern können Sie dynamische Bereiche erzeugen, ohne manuell in Excel einzugreifen.  

Ab hier können Sie Folgendes erkunden:

* Verwendung anderer dynamischer Funktionen wie `FILTER` oder `SEQUENCE` mit Aspose.Cells.  
* Einbetten der Logik in einen Web‑Service, der Berichte auf Abruf erzeugt.  
* Kombination von `EXPAND` mit bedingter Formatierung über die Aspose.Cells‑API.

Experimentieren Sie gern mit unterschiedlichen Startzellen, variablen Größen oder benannten Bereichen, um Ihr spezifisches Automatisierungsszenario zu erfüllen. Wenn Ihnen dieses **expand function example** geholfen hat, teilen Sie es mit Ihrem Team oder tragen Sie Verbesserungen auf GitHub bei. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Aspose.Cells Java meistern: Wie man die Formelkalkulation in Excel unterbricht](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Excel-Tabellen in Bereiche konvertieren mit Aspose.Cells Java: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [Wie man die Excel-Dokumentversion mit Aspose.Cells für Java festlegt](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}