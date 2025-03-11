---
title: Creazione di convalida dati personalizzata
linktitle: Creazione di convalida dati personalizzata
second_title: API di elaborazione Excel Java Aspose.Cells
description: Scopri come creare una convalida dati personalizzata usando Aspose.Cells per Java. Guida passo passo con codice sorgente.
weight: 10
url: /it/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creazione di convalida dati personalizzata


## Introduzione

La convalida dei dati aiuta a mantenere l'integrità dei dati impedendo agli utenti di immettere dati non corretti o non validi nei fogli di calcolo Excel. Mentre Excel offre opzioni di convalida dei dati integrate, ci sono scenari in cui è necessario definire regole di convalida personalizzate. Aspose.Cells per Java ti consente di ottenere questo risultato in modo efficiente.

## Prerequisiti

Prima di immergerti nel codice, assicurati di disporre dei seguenti prerequisiti:

-  Aspose.Cells per Java: Scarica e installa la libreria da[Qui](https://releases.aspose.com/cells/java/).

## Passaggio 1: impostazione del progetto Java

Per iniziare, crea un nuovo progetto Java nel tuo Integrated Development Environment (IDE) preferito. Aggiungi la libreria Aspose.Cells per Java al classpath del tuo progetto.

## Passaggio 2: creazione di una cartella di lavoro Excel

Iniziamo creando una nuova cartella di lavoro di Excel utilizzando Aspose.Cells per Java.

```java
// Codice Java per creare una nuova cartella di lavoro di Excel
Workbook workbook = new Workbook();
```

## Passaggio 3: aggiunta di un foglio di lavoro

Aggiungiamo ora un foglio di lavoro alla cartella di lavoro in cui applicheremo la convalida dei dati personalizzata.

```java
// Codice Java per aggiungere un foglio di lavoro
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Fase 4: Definizione dei criteri di convalida personalizzati

In questo passaggio, definiremo i criteri di convalida personalizzati a cui i nostri dati devono attenersi. Supponiamo di voler limitare l'età immessa in una cella a un intervallo compreso tra 18 e 60.

```java
// Codice Java per definire criteri di convalida personalizzati
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## Passaggio 5: applicazione della convalida dei dati a un intervallo

Ora che abbiamo definito i nostri criteri di convalida personalizzati, applichiamoli a un intervallo specifico di celle.

```java
// Codice Java per applicare la convalida dei dati a un intervallo
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // Applica la convalida alle prime dieci righe
area.endColumn = 0;

validation.addArea(area);
```

## Passaggio 6: salvataggio del file Excel

Infine, salva il file Excel con le regole di convalida dei dati personalizzate applicate.

```java
// Codice Java per salvare il file Excel
workbook.save("CustomDataValidation.xlsx");
```

## Conclusione

In questo tutorial, abbiamo esplorato come creare regole di convalida dati personalizzate utilizzando Aspose.Cells per Java. Seguendo questi passaggi, puoi assicurarti che i tuoi dati Excel aderiscano a criteri specifici, migliorando l'integrità e l'accuratezza dei dati.

## Domande frequenti

### Come posso scaricare Aspose.Cells per Java?

 Puoi scaricare Aspose.Cells per Java dal sito web all'indirizzo[Qui](https://releases.aspose.com/cells/java/).

### Posso applicare la convalida dei dati personalizzata a più intervalli nello stesso foglio di lavoro?

Sì, è possibile applicare la convalida dei dati personalizzata a più intervalli all'interno dello stesso foglio di lavoro ripetendo il passaggio 5 per ciascun intervallo desiderato.

### Esistono altri tipi di convalida dei dati supportati da Aspose.Cells per Java?

Sì, Aspose.Cells per Java supporta vari tipi di convalida dei dati, tra cui numeri interi, decimali, data, ora, lunghezza del testo e altro ancora.

### Come posso personalizzare il messaggio di errore visualizzato quando la convalida dei dati non riesce?

 È possibile personalizzare il messaggio di errore modificando il`setErrorMessage` metodo nel passaggio 4, in cui si definiscono i criteri di convalida.

### Aspose.Cells per Java funziona con file Excel in formati diversi?

Sì, Aspose.Cells per Java supporta un'ampia gamma di formati di file Excel, tra cui XLS, XLSX, XLSM e altri.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
