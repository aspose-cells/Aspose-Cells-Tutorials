---
"description": "Scopri come creare tabelle pivot in Excel utilizzando Aspose.Cells per Java. Automatizza il raggruppamento e l'analisi dei dati con esempi di codice sorgente."
"linktitle": "Raggruppamento dei dati nelle tabelle pivot"
"second_title": "API di elaborazione Excel Java Aspose.Cells"
"title": "Raggruppamento dei dati nelle tabelle pivot"
"url": "/it/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Raggruppamento dei dati nelle tabelle pivot


Le tabelle pivot sono un potente strumento per analizzare e riassumere i dati nei fogli di calcolo. Consentono di raggruppare e categorizzare i dati per ottenere informazioni preziose. In questo articolo, esploreremo come raggruppare efficacemente i dati nelle tabelle pivot utilizzando Aspose.Cells per Java, corredati da esempi di codice sorgente.

## Introduzione

Le tabelle pivot offrono un modo flessibile per organizzare e riassumere i dati provenienti da grandi set di dati. Consentono di creare visualizzazioni personalizzate dei dati raggruppandoli in categorie o gerarchie. Questo può aiutare a identificare più facilmente tendenze, pattern e valori anomali nei dati.

## Passaggio 1: creare una tabella pivot

Iniziamo creando una tabella pivot utilizzando Aspose.Cells per Java. Di seguito è riportato un esempio di come creare una tabella pivot da un file Excel di esempio.

```java
// Carica il file Excel
Workbook workbook = new Workbook("sample.xlsx");

// Accedi al foglio di lavoro contenente i dati
Worksheet worksheet = workbook.getWorksheets().get(0);

// Specificare l'intervallo di dati
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Supponendo 20 righe di dati
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Supponendo 4 colonne di dati

// Crea una tabella pivot basata sull'intervallo di dati
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Ottieni la tabella pivot tramite indice
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Aggiungere campi a righe e colonne
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Aggiungi valori e applica l'aggregazione
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Salvare il file Excel modificato
workbook.save("output.xlsx");
```

## Passaggio 2: raggruppare i dati

In Aspose.Cells per Java, è possibile raggruppare i dati all'interno della tabella pivot utilizzando `PivotField` classe. Ecco un esempio di come raggruppare un campo nella tabella pivot:

```java
// Accedi al campo "Prodotto" nella tabella pivot
PivotField productField = pivotTable.getPivotFields().get("Product");

// Raggruppa il campo "Prodotto" in base a un criterio specifico, ad esempio in base alla lettera iniziale
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Salvare il file Excel modificato con i dati raggruppati
workbook.save("output_grouped.xlsx");
```

## Passaggio 3: personalizzare il raggruppamento

È possibile personalizzare ulteriormente le impostazioni di raggruppamento, ad esempio specificando intervalli di raggruppamento basati sulla data o regole di raggruppamento personalizzate. Ecco un esempio di personalizzazione del raggruppamento basato sulla data:

```java
// Accedere al campo "Data" nella tabella pivot (supponendo che sia un campo data)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Raggruppa le date per mese
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Salva il file Excel modificato con raggruppamento data personalizzato
workbook.save("output_custom_grouping.xlsx");
```

## Conclusione

Raggruppare i dati in tabelle pivot è una tecnica preziosa per analizzare e riassumere i dati in Excel, e Aspose.Cells per Java semplifica l'automazione di questo processo. Con gli esempi di codice sorgente forniti, è possibile creare tabelle pivot, personalizzare il raggruppamento e ottenere informazioni dai dati in modo efficiente.

## Domande frequenti

### 1. Qual è lo scopo delle tabelle pivot in Excel?

Le tabelle pivot in Excel vengono utilizzate per riassumere e analizzare grandi set di dati. Consentono di creare visualizzazioni personalizzate dei dati, facilitando l'identificazione di pattern e tendenze.

### 2. Come posso personalizzare il raggruppamento dei dati in una tabella pivot?

È possibile personalizzare il raggruppamento dei dati in una tabella pivot utilizzando `PivotField` classe in Aspose.Cells per Java. Ciò consente di specificare criteri di raggruppamento, come intervalli basati sulla data o regole personalizzate.

### 3. Posso automatizzare la creazione di tabelle pivot utilizzando Aspose.Cells per Java?

Sì, è possibile automatizzare la creazione di tabelle pivot in Excel utilizzando Aspose.Cells per Java, come dimostrato negli esempi di codice sorgente forniti.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}