---
title: Le funzioni di testo di Excel svelate
linktitle: Le funzioni di testo di Excel svelate
second_title: API di elaborazione Excel Java Aspose.Cells
description: Scopri i segreti delle funzioni di testo di Excel con Aspose.Cells per Java. Impara a manipolare, estrarre e trasformare il testo in Excel senza sforzo.
weight: 18
url: /it/java/basic-excel-functions/excel-text-functions-demystified/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Le funzioni di testo di Excel svelate


# Le funzioni di testo di Excel svelate usando Aspose.Cells per Java

In questo tutorial, ci addentreremo nel mondo della manipolazione del testo in Excel utilizzando l'API Aspose.Cells for Java. Che tu sia un utente esperto di Excel o alle prime armi, comprendere le funzioni di testo può migliorare significativamente le tue competenze sui fogli di calcolo. Esploreremo varie funzioni di testo e forniremo esempi pratici per illustrarne l'utilizzo.

## Iniziare

 Prima di iniziare, assicurati di aver installato Aspose.Cells for Java. Puoi scaricarlo[Qui](https://releases.aspose.com/cells/java/)Una volta impostato, immergiamoci nell'affascinante mondo delle funzioni di testo di Excel.

## CONCATENARE - Combinare testo

 IL`CONCATENATE`funzione consente di unire testo da celle diverse. Vediamo come farlo con Aspose.Cells per Java:

```java
// Codice Java per concatenare il testo utilizzando Aspose.Cells
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
Cell cell = worksheet.getCells().get("A1");

cell.putValue("Hello, ");
cell = worksheet.getCells().get("B1");
cell.putValue("World!");

// Concatenare A1 e B1 in C1
cell = worksheet.getCells().get("C1");
cell.setFormula("=CONCATENATE(A1,B1)");

workbook.calculateFormula();
```

Ora la cella C1 conterrà "Hello, World!".

## SINISTRA e DESTRA - Estrazione del testo

 IL`LEFT` E`RIGHT` funzioni consentono di estrarre un numero specificato di caratteri da sinistra o da destra di una stringa di testo. Ecco come puoi usarle:

```java
// Codice Java per estrarre testo utilizzando Aspose.Cells
Cell cell = worksheet.getCells().get("A2");
cell.putValue("Excel Rocks!");

// Estrai i primi 5 caratteri
cell = worksheet.getCells().get("B2");
cell.setFormula("=LEFT(A2, 5)");

// Estrai gli ultimi 5 caratteri
cell = worksheet.getCells().get("C2");
cell.setFormula("=RIGHT(A2, 5)");

workbook.calculateFormula();
```

Nella cella B2 ci sarà la scritta "Excel" e nella cella C2 ci sarà la scritta "Rocks!".

## LEN - Conteggio dei caratteri

 IL`LEN` funzione conta il numero di caratteri in una stringa di testo. Vediamo come utilizzarla con Aspose.Cells per Java:

```java
// Codice Java per contare i caratteri utilizzando Aspose.Cells
Cell cell = worksheet.getCells().get("A3");
cell.putValue("Excel");

// Conta i caratteri
cell = worksheet.getCells().get("B3");
cell.setFormula("=LEN(A3)");

workbook.calculateFormula();
```

La cella B3 conterrà "5", poiché in "Excel" ci sono 5 caratteri.

## MAIUSCOLO e INFERIORE - Cambio maiuscole/minuscole

 IL`UPPER` E`LOWER` funzioni consentono di convertire il testo in maiuscolo o minuscolo. Ecco come puoi farlo:

```java
// Codice Java per modificare maiuscole/minuscole utilizzando Aspose.Cells
Cell cell = worksheet.getCells().get("A4");
cell.putValue("java programming");

// Converti in maiuscolo
cell = worksheet.getCells().get("B4");
cell.setFormula("=UPPER(A4)");

// Converti in minuscolo
cell = worksheet.getCells().get("C4");
cell.setFormula("=LOWER(A4)");

workbook.calculateFormula();
```

La cella B4 conterrà "PROGRAMMAZIONE JAVA" e la cella C4 conterrà "programmazione Java".

## TROVA e SOSTITUISCI - Individuazione e sostituzione del testo

 IL`FIND` la funzione consente di individuare la posizione di un carattere o di un testo specifico all'interno di una stringa, mentre`REPLACE` funzione ti aiuta a sostituire il testo. Vediamoli in azione:

```java
// Codice Java per trovare e sostituire utilizzando Aspose.Cells
Cell cell = worksheet.getCells().get("A5");
cell.putValue("Search for me");

// Trova la posizione di "for"
cell = worksheet.getCells().get("B5");
cell.setFormula("=FIND(\"for\", A5)");

// Sostituisci "per" con "con"
cell = worksheet.getCells().get("C5");
cell.setFormula("=REPLACE(A5, B5, 3, \"with\")");

workbook.calculateFormula();
```

La cella B5 conterrà "9" (la posizione di "for") e la cella C5 conterrà "Cerca con me".

## Conclusione

Le funzioni di testo in Excel sono potenti strumenti per manipolare e analizzare dati di testo. Con Aspose.Cells per Java, puoi facilmente incorporare queste funzioni nelle tue applicazioni Java, automatizzando le attività correlate al testo e potenziando le tue capacità di Excel. Esplora altre funzioni di testo e libera tutto il potenziale di Excel con Aspose.Cells per Java.

## Domande frequenti

### Come faccio a concatenare il testo di più celle?

 Per concatenare il testo da più celle, utilizzare`CONCATENATE` funzione. Ad esempio:
```java
Cell cell = worksheet.getCells().get("A1");
cell.setFormula("=CONCATENATE(A1, B1)");
```

### Posso estrarre il primo e l'ultimo carattere da una stringa di testo?

 Sì, puoi usare il`LEFT` E`RIGHT` funzioni per estrarre caratteri dall'inizio o dalla fine di una stringa di testo. Ad esempio:
```java
Cell cell = worksheet.getCells().get("A2");
cell.setFormula("=LEFT(A2, 5)");
```

### Come posso contare i caratteri in una stringa di testo?

 Utilizzare il`LEN` funzione per contare i caratteri in una stringa di testo. Ad esempio:
```java
Cell cell = worksheet.getCells().get("A3");
cell.setFormula("=LEN(A3)");
```

### È possibile modificare le maiuscole e le minuscole del testo?

 Sì, puoi convertire il testo in maiuscolo o minuscolo utilizzando`UPPER` E`LOWER` funzioni. Ad esempio:
```java
Cell cell = worksheet.getCells().get("A4");
cell.setFormula("=UPPER(A4)");
```

### Come faccio a trovare e sostituire il testo all'interno di una stringa?

Per trovare e sostituire il testo all'interno di una stringa, utilizzare`FIND` E`REPLACE` funzioni. Ad esempio:
```java
Cell cell = worksheet.getCells().get("A5");
cell.setFormula("=FIND(\"for\", A5)");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
