---
date: '2026-02-22'
description: Lernen Sie, wie Sie die Excel-Berichterstellung mit Aspose.Cells in Java
  automatisieren, indem Sie CopyOptions und PasteOptions einsetzen, um Formeln korrekt
  zu erhalten und nur sichtbare Werte einzufügen.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Excel-Berichte automatisieren – CopyOptions und PasteOptions in Java mit Aspose.Cells
  meistern
url: /de/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatisieren von Excel-Berichten mit Aspose.Cells: CopyOptions & PasteOptions in Java

Suchen Sie nach einer Möglichkeit, **Excel-Berichte** mit Java zu **automatisieren**? Mit Aspose.Cells können Sie programmgesteuert kopieren, einfügen und Formeln anpassen, sodass Ihre Berichte genau bleiben und nur die benötigten Daten übertragen werden. In diesem Tutorial führen wir Sie durch zwei wesentliche Funktionen—**CopyOptions.ReferToDestinationSheet** und **PasteOptions**—die es Ihnen ermöglichen, Formelreferenzen zu erhalten und Werte nur aus sichtbaren Zellen einzufügen.

## Schnelle Antworten
- **Was bewirkt `CopyOptions.ReferToDestinationSheet`?** Passt Formeln an, sodass sie beim Kopieren von Daten auf das Zielblatt verweisen.  
- **Wie kann ich nur sichtbare Zellen einfügen?** Setzen Sie `PasteOptions.setOnlyVisibleCells(true)` zusammen mit `PasteType.VALUES`.  
- **Welche Bibliotheksversion ist erforderlich?** Aspose.Cells 25.3 oder höher.  
- **Benötige ich eine Lizenz für die Produktion?** Ja, eine permanente oder temporäre Lizenz entfernt die Evaluationsbeschränkungen.  
- **Kann ich Maven oder Gradle verwenden?** Beide werden unterstützt; siehe die untenstehenden Abhängigkeits‑Snippets.

## Was bedeutet „Excel-Berichte automatisieren“?
Das Automatisieren von Excel-Berichten bedeutet, Excel‑Arbeitsmappen programmgesteuert zu erstellen, zu konsolidieren und zu formatieren, wodurch manuelle Kopier‑ und Einfüge‑Schritte entfallen und Fehler reduziert werden. Aspose.Cells bietet eine umfangreiche API, die Java‑Entwicklern die Manipulation von Tabellenkalkulationen im großen Maßstab ermöglicht.

## Warum CopyOptions und PasteOptions für Berichte verwenden?
- **Formelintegrität erhalten** beim Verschieben von Daten zwischen Arbeitsblättern.  
- **Versteckte Zeilen/Spalten ausschließen**, um Berichte sauber und fokussiert zu halten.  
- **Leistung steigern**, indem nur die notwendigen Daten anstelle ganzer Bereiche kopiert werden.

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
- **Kostenlose Testversion** – Vollständiger Funktionsumfang für die Evaluierung.  
- **Temporäre Lizenz** – Entfernt die Einschränkungen der Testversion während des Tests.  
- **Permanente Lizenz** – Empfohlen für produktive Arbeitslasten.

Initialisieren Sie Aspose.Cells in Ihrem Java‑Code:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Schritt‑für‑Schritt‑Anleitung

### 1. CopyOptions mit ReferToDestinationSheet

#### Übersicht
Durch das Setzen von `CopyOptions.ReferToDestinationSheet` auf `true` werden Formelreferenzen neu geschrieben, sodass sie nach dem Kopiervorgang auf das neue Blatt verweisen.

#### Schritt 1: Arbeitsmappe und Arbeitsblätter initialisieren
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Schritt 2: CopyOptions konfigurieren
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Schritt 3: Kopiervorgang ausführen
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Warum das wichtig ist*: Formeln, die ursprünglich `Sheet1` referenzierten, verweisen nun korrekt auf `DestSheet`, wodurch Ihre automatisierten Berichte zuverlässig bleiben.

**Fehlerbehebungshinweis**: Wenn Formeln weiterhin das alte Blatt referenzieren, stellen Sie sicher, dass `setReferToDestinationSheet(true)` **vor** dem Kopiervorgang aufgerufen wird.

### 2. PasteOptions für Nur‑Werte aus sichtbaren Zellen

#### Übersicht
`PasteOptions` ermöglicht es Ihnen, zu definieren, was eingefügt wird. Die Verwendung von `PasteType.VALUES` zusammen mit `onlyVisibleCells=true` kopiert nur die angezeigten Werte und ignoriert versteckte Zeilen/Spalten sowie Formatierungen.

#### Schritt 1: Arbeitsmappe und Arbeitsblätter initialisieren
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Schritt 2: PasteOptions konfigurieren
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Schritt 3: Einfüge‑Vorgang ausführen
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Warum das wichtig ist*: Ideal zum Extrahieren gefilterter Daten oder zum Erstellen sauberer Berichte ohne versteckte Zeilen oder Formatierungs‑Rauschen.

**Fehlerbehebungshinweis**: Stellen Sie sicher, dass Zeilen/Spalten in Excel tatsächlich ausgeblendet sind, bevor Sie kopieren; andernfalls werden sie einbezogen.

## Praktische Anwendungsfälle
1. **Finanzkonsolidierung** – Monatliche Arbeitsblätter zu einer Master‑Arbeitsmappe zusammenführen und dabei alle Formeln korrekt behalten.  
2. **Export gefilterter Daten** – Nur sichtbare Zeilen aus einer gefilterten Tabelle in ein Zusammenfassungs‑Arbeitsblatt übernehmen.  
3. **Geplante Berichtserstellung** – Nächtliche automatisierte Erstellung von Excel‑Berichten mit präzisen Zellwerten und korrekten Referenzen.

## Leistungsüberlegungen
- **Arbeitsmappen freigeben** nach Gebrauch (`wb.dispose();`), um native Ressourcen zu befreien.  
- **Batch‑Operationen** – Mehrere Kopier‑/Einfüge‑Aufrufe gruppieren, um Overhead zu reduzieren.  
- **Speicher überwachen** – Große Arbeitsmappen können einen erhöhten Heap benötigen (`-Xmx2g`).

## Häufig gestellte Fragen

**Q1: Wofür wird `CopyOptions.ReferToDestinationSheet` verwendet?**  
A: Es schreibt Formelreferenzen neu, sodass sie nach einem Kopiervorgang auf das Zielblatt verweisen und die Berichtsformeln korrekt bleiben.

**Q2: Wie füge ich nur sichtbare Zellen ein?**  
A: Setzen Sie `PasteOptions.setOnlyVisibleCells(true)` und wählen Sie `PasteType.VALUES`.

**Q3: Kann ich Aspose.Cells ohne Kauf einer Lizenz nutzen?**  
A: Ja, eine kostenlose Testversion oder temporäre Lizenz steht für die Evaluierung zur Verfügung, jedoch ist für die Produktion eine permanente Lizenz erforderlich.

**Q4: Warum sind einige Referenzen nach dem Kopieren immer noch falsch?**  
A: Überprüfen Sie, dass `ReferToDestinationSheet` **vor** dem Kopiervorgang aktiviert ist und dass die Quellformeln keine externen Arbeitsmappen‑Links enthalten.

**Q5: Welche Best Practices für das Speicher‑Management sollte ich befolgen?**  
A: Geben Sie `Workbook`‑Objekte nach Gebrauch frei, verarbeiten Sie große Dateien in Teilen und überwachen Sie die JVM‑Heap‑Nutzung.

**Q6: Ist es möglich, CopyOptions und PasteOptions in einem Vorgang zu kombinieren?**  
A: Ja, Sie können sie verketten, indem Sie zuerst mit `CopyOptions` kopieren und anschließend `PasteOptions` auf den Zielbereich anwenden.

## Ressourcen
- **Dokumentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Kauf**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Kostenlose Testversion**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporäre Lizenz**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support‑Forum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Zuletzt aktualisiert:** 2026-02-22  
**Getestet mit:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose