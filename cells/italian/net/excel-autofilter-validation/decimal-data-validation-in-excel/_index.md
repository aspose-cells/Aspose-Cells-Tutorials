---
title: Convalida dei dati decimali in Excel
linktitle: Convalida dei dati decimali in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come implementare la convalida dei dati decimali in Excel usando Aspose.Cells per .NET con la nostra guida facile da seguire. Migliora l'integrità dei dati senza sforzo.
weight: 11
url: /it/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convalida dei dati decimali in Excel

## Introduzione

Creare fogli di calcolo con dati accurati è essenziale per una comunicazione chiara in qualsiasi attività. Un modo per garantire l'accuratezza dei dati è tramite l'uso della convalida dei dati in Excel. In questo tutorial, sfrutteremo la potenza di Aspose.Cells per .NET per creare un meccanismo di convalida dei dati decimali che mantenga i tuoi dati affidabili e puliti. Se stai cercando di migliorare il tuo gioco Excel, sei nel posto giusto!

## Prerequisiti

Prima di immergerti nel codice, assicurati di aver impostato tutto per un'esperienza di navigazione senza intoppi:

1. Visual Studio: scarica e installa Visual Studio se non l'hai già fatto. È l'ambiente perfetto per sviluppare applicazioni .NET.
2.  Aspose.Cells per .NET: dovrai aggiungere la libreria Aspose.Cells al tuo progetto. Puoi scaricarla tramite[questo collegamento](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: anche se spiegheremo tutto passo dopo passo, avere una conoscenza di base della programmazione C# ti consentirà di afferrare meglio i concetti.
4. .NET Framework: assicurarsi di aver installato la versione .NET Framework necessaria, compatibile con Aspose.Cells.
5. Librerie: fai riferimento alla libreria Aspose.Cells nel tuo progetto per evitare errori di compilazione.

Ora che abbiamo visto le basi, passiamo alla parte interessante: la codifica.

## Importa pacchetti

Per iniziare, devi importare i pacchetti necessari nel tuo file C#. Questo ti consente di accedere alle funzionalità di Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Includendo questa riga all'inizio del file, stai dicendo a C# di cercare la funzionalità Aspose.Cells che consente di manipolare i file Excel.

Ora che abbiamo impostato la scena, vediamo i passaggi necessari per creare la convalida dei dati decimali in un foglio di lavoro Excel.

## Passaggio 1: imposta la directory dei documenti

Prima di poter salvare qualsiasi file, devi assicurarti che la directory dei documenti sia impostata correttamente:

```csharp
string dataDir = "Your Document Directory";
```

 Sostituire`"Your Document Directory"` con il percorso in cui desideri salvare i file Excel.

## Passaggio 2: verificare l'esistenza della directory

Questo frammento controlla se la directory esiste e la crea in caso contrario:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Questo passaggio è come assicurarsi che il tuo spazio di lavoro sia pronto prima di iniziare un nuovo progetto. Niente confusione, niente stress!

## Passaggio 3: creare un oggetto cartella di lavoro

Ora creiamo un nuovo oggetto cartella di lavoro, che è essenzialmente un file Excel:

```csharp
Workbook workbook = new Workbook();
```

Pensa a una cartella di lavoro come a una tela bianca per i tuoi dati. A questo punto, non ha alcun contenuto ma è pronta per essere dipinta.

## Passaggio 4: creare e accedere al foglio di lavoro


Ora creiamo un foglio di lavoro e accediamo al primo foglio della cartella di lavoro:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Proprio come un libro ha più pagine, un quaderno di lavoro può avere più fogli di lavoro. Al momento ci stiamo concentrando sul primo.

## Passaggio 5: ottenere la raccolta delle convalide

Ora, estraiamo la raccolta di convalida dal foglio di lavoro, poiché è qui che gestiremo le nostre regole di convalida dei dati:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Questo passaggio è simile al controllo della cassetta degli attrezzi prima di iniziare un progetto.

## Passaggio 6: definire l'area della cella per la convalida

Dobbiamo definire l'area in cui si applica la convalida:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Qui stiamo stabilendo che la convalida dei dati verrà applicata a una singola cella, nello specifico alla prima cella del foglio di lavoro (A1).

## Passaggio 7: creare e aggiungere la convalida

Creiamo il nostro oggetto di convalida e aggiungiamolo alla raccolta delle convalide:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Ora abbiamo un oggetto di convalida che configureremo per applicare le nostre condizioni decimali.

## Passaggio 8: impostare il tipo di convalida

Ora specificheremo il tipo di convalida che desideriamo:

```csharp
validation.Type = ValidationType.Decimal;
```

Impostando il tipo su Decimale, stiamo indicando a Excel di aspettarsi valori decimali nella cella convalidata.

## Passaggio 9: specificare l'operatore

Ora, specificheremo la condizione per i valori ammissibili. Vogliamo assicurarci che i dati immessi siano compresi tra due intervalli:

```csharp
validation.Operator = OperatorType.Between;
```

Immagina di tracciare una linea di confine. Qualsiasi numero al di fuori di questo intervallo verrà rifiutato, mantenendo i tuoi dati puliti!

## Fase 10: stabilire limiti per la convalida

Ora imposteremo i limiti inferiore e superiore per la nostra convalida:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Con questi limiti, ogni numero decimale, non importa quanto grande o piccolo, è accettato, purché sia valido!

## Passaggio 11: personalizzazione del messaggio di errore

Assicuriamoci che gli utenti sappiano perché il loro input è stato rifiutato aggiungendo un messaggio di errore:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Ciò si traduce in un'esperienza intuitiva, poiché fornisce indicazioni su cosa inserire.

## Passaggio 12: definire l'area di convalida

Ora, specifichiamo le celle che saranno sottoposte a questa convalida:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

In questa configurazione, diciamo che la convalida si applica dalla cella A1 alla cella A10.

## Passaggio 13: aggiungere l'area di convalida

Ora che abbiamo definito la nostra area di convalida, applichiamola:

```csharp
validation.AddArea(area);
```

La convalida è ora saldamente in atto, pronta a rilevare qualsiasi input inappropriato!

## Passaggio 14: Salvare la cartella di lavoro

Infine, salviamo la cartella di lavoro con la convalida dei dati decimali attivata:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Ed ecco fatto! Hai creato con successo una cartella di lavoro con convalida dei dati decimali utilizzando Aspose.Cells per .NET.

## Conclusione

Implementare la convalida dei dati decimali in Excel usando Aspose.Cells per .NET è un gioco da ragazzi se segui questi semplici passaggi. Non solo ti assicuri che i dati rimangano puliti e strutturati, ma migliori anche l'integrità complessiva dei dati nei tuoi fogli di calcolo, rendendoli affidabili e intuitivi.
Che tu lavori nel settore finanziario, nella gestione di progetti o in qualsiasi altro campo che utilizzi il reporting dei dati, padroneggiare queste competenze migliorerà notevolmente la tua produttività. Quindi, vai avanti, provaci! I tuoi fogli di calcolo ti ringrazieranno.

## Domande frequenti

### Che cos'è la convalida dei dati in Excel?
La convalida dei dati in Excel è una funzionalità che limita il tipo di dati che possono essere immessi in una determinata cella o intervallo, garantendone l'integrità.

### Posso personalizzare il messaggio di errore nella convalida dei dati?
Sì! Puoi fornire messaggi di errore personalizzati per guidare gli utenti quando vengono immessi dati errati.

### Aspose.Cells è gratuito?
 Aspose.Cells offre una prova gratuita, ma avrai bisogno di una licenza per un utilizzo a lungo termine. Puoi trovare maggiori informazioni sull'acquisizione di una licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/).

### Quali tipi di dati posso convalidare in Excel?
Con Aspose.Cells puoi convalidare vari tipi di dati, tra cui numeri interi, decimali, date, elenchi e formule personalizzate.

### Dove posso trovare ulteriore documentazione su Aspose.Cells?
 Puoi esplorare la vasta documentazione[Qui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
