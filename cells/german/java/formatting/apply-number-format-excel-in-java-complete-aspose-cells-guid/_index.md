---
category: general
date: 2026-07-20
description: Wenden Sie das Zahlenformat in Excel mit Java und Aspose.Cells an. Erfahren
  Sie, wie Sie den Währungsstil in Excel anwenden, ein Excel-Arbeitsbuch in Java erstellen
  und Datentabellen effizient nach Excel importieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: de
lastmod: 2026-07-20
og_description: Zahlenformat in Excel mit Java anwenden. Dieser Leitfaden zeigt Ihnen,
  wie Sie das Währungsformat in Excel anwenden, ein Excel‑Arbeitsbuch mit Java erstellen
  und eine Datentabelle Schritt für Schritt nach Excel importieren.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Zahlenformat in Excel mit Java anwenden – Vollständiges Aspose.Cells‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Zahlenformat in Excel mit Java anwenden – Vollständiger Aspose.Cells‑Leitfaden
url: /de/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Number-Format in Excel mit Java anwenden – Vollständige Aspose.Cells‑Anleitung

Haben Sie sich schon einmal gefragt, wie Sie **Number Format Excel** direkt aus Java‑Code anwenden können? Vielleicht erstellen Sie Finanzberichte oder benötigen eine schnelle Möglichkeit, eine Spalte mit Beträgen zu formatieren, ohne Excel manuell zu öffnen. Die gute Nachricht: Mit Aspose.Cells lässt sich das in wenigen Zeilen erledigen, und Sie lernen gleichzeitig, wie Sie **Currency Style Excel** anwenden, **Excel Workbook Java** erstellen und **Datatable nach Excel** importieren – alles in einer kompakten Routine.

In diesem Tutorial gehen wir ein konkretes Beispiel durch: Eine Liste von Beträgen, gespeichert in einer Java `List<Map<String,Object>>`, wird in ein frisches Workbook importiert, die erste Spalte erhält ein integriertes Währungsformat, und die Datei wird gespeichert – bereit für die Verteilung. Bereit, zu sehen, wie einfach das ist? Dann legen wir los.

## Voraussetzungen – Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie folgendes haben:

- **Java Development Kit (JDK) 8+** – der Code läuft auf jedem aktuellen JDK.
- **Aspose.Cells for Java**‑Bibliothek (das Maven‑Artifact `com.aspose:aspose-cells`) – das ist die Engine, die Excel‑Dateien ohne installierte Office‑Version manipuliert.
- Eine **bevorzugte IDE** (IntelliJ IDEA, Eclipse, VS Code …) – jeder Editor funktioniert, aber eine IDE beschleunigt das Debuggen.
- Grundlegende Kenntnisse mit **Java‑Collections** – wir verwenden eine `List` von `Map`s, um eine DataTable zu simulieren.

Das war’s. Keine externen Services, keine Excel‑Installation, nur reines Java.

## Schritt 1: Excel‑Workbook in Java erstellen – Instanziierung des Workbooks

Das Erste, was wir benötigen, ist ein Workbook‑Objekt. Denken Sie daran wie an eine leere Leinwand, auf der alles Platz findet.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Warum das Workbook zuerst erstellen? Aspose.Cells arbeitet komplett im Speicher, sodass Sie Tabellen, Stile und Daten hinzufügen können, bevor Sie überhaupt die Festplatte berühren. Dieser Ansatz ist schnell und hält Ihren Code testbar.

## Schritt 2: Daten vorbereiten – Datatable nach Excel importieren mit einer List von Maps

In vielen Unternehmens‑Apps kommen Daten aus Datenbanken als Tabellen. Hier simulieren wir das mit einer `List<Map<String,Object>>`. Jede Map stellt eine Zeile dar, und der Schlüssel `"Amount"` verweist auf einen numerischen Wert.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Sie fragen sich vielleicht: „Warum nicht ein `ResultSet` oder POJOs verwenden?“ Die Methode `importDataTable` akzeptiert jede Collection, die sich wie eine DataTable verhält, und eine List von Maps ist der einfachste Weg, das Konzept zu demonstrieren, ohne zusätzliche Abhängigkeiten einzubinden.

## Schritt 3: Number Format definieren – Currency Style Excel anwenden

Jetzt kommt der Kern des Tutorials: **apply number format excel**. Aspose.Cells liefert integrierte Number‑Formate; das Währungsformat hat den Index 5. Wir holen den Standard‑Style des ersten Arbeitsblatts, passen das Number‑Format an und speichern ihn für die spätere Verwendung.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Warum den Standard‑Style als Basis nutzen? Er enthält bereits die Standard‑Schriftart, Ausrichtung und weitere Einstellungen des Workbooks, sodass Sie nur das ändern müssen, was wichtig ist – in diesem Fall das Number‑Format. Wenn Sie ein benutzerdefiniertes Format benötigen (z. B. “€#,##0.00”), könnten Sie stattdessen `currencyStyle.setCustom("#,##0.00 €")` aufrufen.

## Schritt 4: Import‑Optionen festlegen – Verknüpfung des Style‑Arrays

Aspose.Cells erlaubt es, ein Array von `Style`‑Objekten zu übergeben, das den zu importierenden Spalten entspricht. Da unsere Daten nur eine Spalte haben, übergeben wir ein ein‑elementiges Array, das den Währungs‑Style enthält.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Falls Sie mehrere Spalten unterschiedlich formatieren müssen, erweitern Sie einfach das Array: `new Style[] { styleForCol1, styleForCol2, … }`. Die Reihenfolge der Styles entspricht der Reihenfolge der Spalten in den Quelldaten.

## Schritt 5: Daten importieren – Datatable ins Arbeitsblatt bringen

Mit dem vorbereiteten Workbook, den Daten und den definierten Styles können wir nun **import datatable to excel**. Wir starten bei Zelle `A1`, schließen Spaltenüberschriften ein (`true`) und übergeben die `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Beachten Sie das `true`‑Flag – Aspose.Cells erzeugt automatisch eine Header‑Zeile basierend auf den Map‑Keys (`"Amount"`). Wenn Sie `false` setzen, wird die Kopfzeile weggelassen, was Ihnen mehr Kontrolle über das Endlayout gibt.

## Schritt 6: Datei speichern – Excel‑Workbook in Java auf Festplatte erstellen

Der letzte Baustein ist das Persistieren des im Speicher befindlichen Workbooks in eine physische Datei. Sie können jedes von Aspose unterstützte Format wählen (`.xlsx`, `.xls`, `.csv`, …). Hier speichern wir als XLSX‑Datei.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Nach dem Ausführen des Programms öffnen Sie die erzeugte Datei. Sie sehen die Spalte `"Amount"` mit einem Dollar‑Zeichen, zwei Dezimalstellen und korrekten Tausendertrennzeichen – genau das, was Sie erwarten, wenn Sie **apply number format excel** für Währungswerte verwenden.

## Erwartetes Ergebnis

| Betrag |
|--------|
| $1,234.56 |
| $7,890.12 |

Die Überschrift „Betrag“ erscheint fett (Standard‑Style), und jede darunterliegende Zelle zeigt das von uns gesetzte Währungsformat. Keine manuelle Formatierung in Excel nötig.

## Pro‑Tipps und häufige Stolperfallen

- **Styles wiederverwenden** – Styles sind leichtgewichtig, aber das Erzeugen eines neuen `Style` für jede Zelle kann die Performance beeinträchtigen. Verwenden Sie ein Style‑Objekt mehrfach, wenn Sie dasselbe Format auf viele Zellen anwenden, so wie wir es mit `currencyStyle` getan haben.
- **Benutzerdefinierte Formate** – Wenn Ihr Locale ein anderes Währungssymbol nutzt, ersetzen Sie `currencyStyle.setNumber(5)` durch `currencyStyle.setCustom("€#,##0.00")`. Testen Sie das Format in Excel, um sicherzugehen, dass es wie erwartet funktioniert.
- **Große Datensätze** – Bei tausenden Zeilen sollten Sie `importDataTable` mit dem Flag `ImportTableOptions.setImportDataOnly(true)` verwenden, um die Header‑Erzeugung zu überspringen und den Import zu beschleunigen.
- **Thread‑Safety** – Aspose.Cells‑Objekte sind **nicht** thread‑sicher. Erzeugen Sie pro Thread ein separates `Workbook`, wenn Sie Berichte parallel generieren.

## Häufig gestellte Fragen

**F: Kann ich das Number‑Format auf ein bestehendes Workbook anwenden?**  
A: Absolut. Öffnen Sie das Workbook mit `new Workbook("Existing.xlsx")`, holen Sie das Ziel‑Worksheet und führen Sie die Schritte 3‑5 aus, um das Style‑Array auf neue Daten anzuwenden.

**F: Was, wenn ich statt Währung Daten formatieren muss?**  
A: Verwenden Sie einen anderen integrierten Number‑Index (`14` für kurzes Datum, `22` für langes Datum) oder ein benutzerdefiniertes Format wie `yyyy‑mm‑dd`. Der Workflow bleibt gleich.

**F: Funktioniert das auch mit älteren Excel‑Versionen (.xls)?**  
A: Ja. Ändern Sie einfach die Dateierweiterung in `workbook.save("MyFile.xls")`. Aspose wechselt automatisch in das Binärformat.

## Fazit – Was wir erreicht haben

Wir haben **apply number format excel** auf eine Spalte mit Geldbeträgen angewendet, gezeigt, wie man **apply currency style excel** nutzt, den einfachsten Weg demonstriert, **create excel workbook java** zu erstellen, und Aspose.Cells verwendet, um **import datatable to excel** ohne UI‑Interaktion durchzuführen. All das geschah in einem kompakten, eigenständigen Programm, das Sie kopieren, einfügen und ausführen können.

Was kommt als Nächstes? Versuchen Sie, das Beispiel zu erweitern:

- Weitere Spalten hinzufügen (z. B. „Date“, „Description“) und pro Spalte unterschiedliche Styles zuweisen.
- dieselben Daten nach CSV exportieren und beobachten, wie Number‑Formate verloren gehen.
- Den Code in einen Spring Boot‑Service integrieren, der das Workbook als herunterladbare HTTP‑Antwort zurückgibt.

Viel Spaß beim Experimentieren – und falls Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar. Happy coding!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}