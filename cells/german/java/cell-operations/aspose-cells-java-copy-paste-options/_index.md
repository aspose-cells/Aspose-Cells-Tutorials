---
date: '2026-10-28'
description: Erfahren Sie, wie Sie Werte mit den Kopier- und Einfügeoptionen von Aspose.Cells
  in Java einfügen, inklusive Schritt-für-Schritt-Code, Maven-Abhängigkeits-Setup
  und Lizenzierungstipps.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Erfahren Sie, wie Sie Werte mit den Kopier- und Einfügeoptionen von
  Aspose.Cells in Java einfügen, inklusive Schritt-für-Schritt-Code, Maven-Abhängigkeits-Setup
  und Lizenzierungstipps.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Wie man Werte mit den Kopier- und Einfügeoptionen von Aspose.Cells einfügt
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Wie man Werte mit den Kopier- und Einfügeoptionen von Aspose.Cells einfügt
url: /de/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Werte mit Aspose.Cells Kopier‑ und Einfügeoptionen einfügt

Automatisieren von Excel‑Berichten in Java bedeutet, dass Sie Arbeitsmappen erzeugen, konsolidieren und formatieren können, ohne Excel manuell zu öffnen. Mit **Aspose.Cells** erhalten Sie die volle Kontrolle über Formeln, ausgeblendete Zeilen und Zellwerte, sodass Ihre Berichte genau und leichtgewichtig bleiben. In diesem Tutorial lernen Sie, wie Sie **CopyOptions.ReferToDestinationSheet** verwenden, um Formeln korrekt zu halten, und **PasteOptions**, um nur die benötigten sichtbaren Werte einzufügen.

## Schnelle Antworten
- **Was macht `CopyOptions.ReferToDestinationSheet`?** Es schreibt Formeln um, sodass sie nach einer Kopieroperation auf das Zielblatt verweisen.  
- **Wie kann ich nur sichtbare Zellen einfügen?** Rufen Sie `PasteOptions.setOnlyVisibleCells(true)` zusammen mit `PasteType.VALUES` auf.  
- **Welche Bibliotheksversion ist erforderlich?** Aspose.Cells 25.3 oder höher.  
- **Benötige ich eine Lizenz für die Produktion?** Ja – eine permanente oder temporäre Lizenz entfernt Evaluationsbeschränkungen.  
- **Kann ich Maven oder Gradle verwenden?** Beide werden unterstützt; siehe die Abhängigkeits‑Snippets unten.

## Was bedeutet „Excel‑Berichte automatisieren“?
Excel‑Berichte automatisieren bedeutet, Excel‑Arbeitsmappen programmgesteuert zu erzeugen und zu aktualisieren, sodass Sie Berichte erstellen, zusammenführen und formatieren können, ohne manuelles Kopieren‑Einfügen. Das reduziert Fehler und spart Stunden wiederholter Arbeit. Dieser Ansatz ist ideal für geplante Batch‑Jobs, datengetriebene Dashboards und Finanzkonsolidierungs‑Pipelines.

## Warum CopyOptions und PasteOptions für Berichte verwenden?
Diese beiden Klassen ermöglichen es, Formelreferenzen beim Kopieren von Daten **und** das Extrahieren nur der nach dem Filtern oder Ausblenden von Zeilen sichtbaren Zellen beizubehalten. Die gleichzeitige Verwendung reduziert die zu übertragende Datenmenge in typischen gefilterten Tabellenszenarien um bis zu 80 % und stellt sicher, dass Formeln im Zielblatt weiterhin korrekt berechnet werden.

## Voraussetzungen
- Java 8 oder höher.  
- Maven oder Gradle für das Abhängigkeits‑Management.  
- Aspose.Cells 25.3+ (Testversion, temporäre oder permanente Lizenz).  

## Einrichtung von Aspose.Cells für Java

Fügen Sie die Bibliothek Ihrem Projekt mit einer der folgenden Methoden hinzu:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Lizenzbeschaffung
- **Kostenlose Testversion** – vollständiger Funktionsumfang für die Evaluierung.  
- **Temporäre Lizenz** – entfernt Testbeschränkungen während des Tests.  
- **Permanente Lizenz** – empfohlen für Produktions‑Workloads.

Initialisieren Sie Aspose.Cells in Ihrem Java‑Code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Schritt‑für‑Schritt‑Anleitung

### 1. copyOptions mit referToDestinationSheet

#### Überblick
`CopyOptions` ist das Konfigurationsobjekt von Aspose.Cells, das steuert, wie Formeln und Zellreferenzen während einer Kopieroperation behandelt werden. Das Setzen von `CopyOptions.ReferToDestinationSheet` auf `true` schreibt Formelreferenzen um, sodass sie nach der Kopieroperation auf das neue Blatt verweisen.

#### Schritt 1: Arbeitsmappe und Arbeitsblätter initialisieren  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Schritt 2: copyOptions konfigurieren  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Schritt 3: Kopieroperation ausführen  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Warum das wichtig ist*: Formeln, die ursprünglich `Sheet1` referenzierten, verweisen nun korrekt auf `DestSheet`, wodurch Ihre automatisierten Berichte zuverlässig bleiben.

**Fehlerbehebungshinweis**: Wenn Formeln weiterhin das alte Blatt referenzieren, stellen Sie sicher, dass `setReferToDestinationSheet(true)` **vor** dem Kopiervorgang aufgerufen wird.

### 2. pasteOptions für ausschließlich Werte aus sichtbaren Zellen

#### Überblick
`PasteOptions` ist das Einstellungsobjekt von Aspose.Cells, das definiert, was eingefügt wird. Die Verwendung von `PasteType.VALUES` zusammen mit `onlyVisibleCells=true` kopiert nur die angezeigten Werte und ignoriert ausgeblendete Zeilen/Spalten sowie Formatierungen.

#### Schritt 1: Arbeitsmappe und Arbeitsblätter initialisieren  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Schritt 2: pasteOptions konfigurieren  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Schritt 3: Einfügeoperation ausführen  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Warum das wichtig ist*: Ideal zum Extrahieren gefilterter Daten oder zum Erstellen sauberer Berichte ohne ausgeblendete Zeilen oder Formatierungsrauschen.

**Fehlerbehebungshinweis**: Stellen Sie sicher, dass Zeilen/Spalten in Excel tatsächlich ausgeblendet sind, bevor Sie kopieren; andernfalls werden sie einbezogen.

## Praktische Anwendungsfälle
1. **Finanzkonsolidierung** – monatliche Tabellenblätter in eine Master‑Arbeitsmappe zusammenführen und dabei alle Formeln exakt halten.  
2. **Export gefilterter Daten** – nur sichtbare Zeilen aus einer gefilterten Tabelle in ein Zusammenfassungsblatt übernehmen.  
3. **Geplante Berichtserstellung** – nächtliche Excel‑Berichtserstellung automatisieren mit präzisen Zellwerten und korrekten Referenzen.

## Leistungsüberlegungen
- **Arbeitsmappen freigeben** wenn sie nicht mehr benötigt werden (`wb.dispose();`), um native Ressourcen zu befreien.  
- **Batch‑Operationen** – mehrere Kopier‑/Einfüge‑Aufrufe gruppieren, um den Overhead zu reduzieren.  
- **Speicher überwachen** – große Arbeitsmappen können einen erhöhten Heap benötigen (`-Xmx2g`).  
- Aspose.Cells unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate** und kann Arbeitsmappen mit **bis zu 2 Millionen Zeilen** verarbeiten, ohne die gesamte Datei in den Speicher zu laden, und liefert eine Hochdurchsatz‑Leistung für Unternehmens‑Workloads.

## Häufig gestellte Fragen

**Q: Wofür wird `CopyOptions.ReferToDestinationSheet` verwendet?**  
A: Es schreibt Formelreferenzen um, sodass sie nach einer Kopie auf das Zielblatt verweisen und die Berichtsformeln korrekt bleiben.

**Q: Wie füge ich nur sichtbare Zellen ein?**  
A: Setzen Sie `PasteOptions.setOnlyVisibleCells(true)` und wählen Sie `PasteType.VALUES`.

**Q: Kann ich Aspose.Cells ohne Kauf einer Lizenz verwenden?**  
A: Ja, eine kostenlose Testversion oder temporäre Lizenz steht für die Evaluierung zur Verfügung, aber für die Produktion ist eine permanente Lizenz erforderlich.

**Q: Warum sind einige Referenzen nach dem Kopieren noch falsch?**  
A: Überprüfen Sie, dass `ReferToDestinationSheet` **vor** dem Kopiervorgang aktiviert ist und dass die Quellformeln keine externen Arbeitsmappen‑Links enthalten.

**Q: Welche Best Practices für das Speicher‑Management sollte ich befolgen?**  
A: Geben Sie `Workbook`‑Objekte frei, wenn sie nicht mehr benötigt werden, verarbeiten Sie große Dateien in Teilen und überwachen Sie die JVM‑Heap‑Nutzung.

**Q: Ist es möglich, CopyOptions und PasteOptions in einer Operation zu kombinieren?**  
A: Ja, Sie können sie verketten, indem Sie zuerst mit `CopyOptions` kopieren und anschließend `PasteOptions` auf den Zielbereich anwenden.

## Ressourcen
- **Dokumentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Kauf**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Kostenlose Testversion**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Temporäre Lizenz**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Support‑Forum**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Zuletzt aktualisiert:** 2026-10-28  
**Getestet mit:** Aspose.Cells 25.3 für Java  
**Autor:** Aspose

## Verwandte Tutorials

- [Excel‑Datei in Java lesen – Arbeitsmappen‑Zellmanipulation mit Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Daten in Zelle in Excel mit Aspose.Cells für Java hinzufügen](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Excel‑Zellen‑Zeilen‑Spalten‑Indizes mit Aspose.Cells Java konvertieren](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}