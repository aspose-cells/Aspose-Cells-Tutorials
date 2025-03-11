---
title: Il filtro automatico inizia con in Excel
linktitle: Il filtro automatico inizia con in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come filtrare automaticamente le righe di Excel utilizzando Aspose.Cells in .NET senza sforzo con questa guida completa passo dopo passo.
weight: 10
url: /it/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Il filtro automatico inizia con in Excel

## Introduzione

Quando si tratta di lavorare con i dati, Excel si è affermato come applicazione di riferimento per innumerevoli settori e scopi. Una delle sue funzionalità più potenti è AutoFilter, che semplifica notevolmente la scansione di ampi set di dati. Se utilizzi Aspose.Cells per .NET, puoi sfruttare questa funzionalità a livello di programmazione e migliorare significativamente le tue attività di gestione dei dati. In questa guida, ti guideremo attraverso il processo di implementazione di una funzionalità che filtra le righe di Excel in base al fatto che inizino con una determinata stringa.

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti prerequisiti:

1. Ambiente di sviluppo: familiarizza con un ambiente di sviluppo .NET. Potrebbe essere Visual Studio o qualsiasi altro IDE di tua scelta.
2.  Aspose.Cells per .NET: devi avere Aspose.Cells per .NET installato. Se non lo hai ancora fatto, puoi scaricarlo comodamente[Qui](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: una conoscenza di base di C# e di come lavorare con le librerie .NET ti aiuterà a seguire il corso senza problemi.
4.  Dati di esempio: dovresti avere un file Excel, preferibilmente denominato`sourseSampleCountryNames.xlsx`, situato nella directory sorgente designata. Questo file conterrà i dati che filtreremo.
5.  Licenza: per la piena funzionalità, si consiglia di acquistare una licenza tramite questo[collegamento](https://purchase.aspose.com/buy) Se vuoi testare le funzionalità, puoi richiedere un[licenza temporanea](https://purchase.aspose.com/temporary-license/).

Tutto pronto? Andiamo!

## Importa pacchetti

Per iniziare, importa gli spazi dei nomi necessari nella parte superiore del file C#:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

In questo modo vengono importate le funzionalità principali di Aspose.Cells insieme alle funzionalità di sistema di base su cui faremo affidamento per l'interazione con la console.

Ora che hai configurato il tuo ambiente e importato i pacchetti necessari, scomponiamo la funzionalità Autofilter in passaggi gestibili. Implementeremo un filtro che estrae le righe che iniziano con "Ba".

## Passaggio 1: definire le directory di origine e di output

Per prima cosa, definiamo dove si trova il nostro file Excel di input e dove vogliamo salvare il nostro output filtrato:

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory\\";

// Directory di uscita
string outputDir = "Your Document Directory\\";
```

 Spiegazione: qui, sostituisci`"Your Document Directory\\"` con il percorso effettivo delle tue directory. Assicurati di terminare i percorsi delle directory con una doppia barra rovesciata (`\\`) per evitare qualsiasi problema di percorso.

## Passaggio 2: creare un'istanza dell'oggetto Workbook

Successivamente, creeremo un oggetto Workbook che punta al nostro file Excel:

```csharp
// Creazione di un'istanza di un oggetto Workbook contenente dati di esempio
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 Spiegazione: questa riga inizializza una nuova istanza della cartella di lavoro utilizzando il percorso del file specificato.`Workbook` La classe è fondamentale in quanto rappresenta l'intero file Excel.

## Fase 3: Accesso al primo foglio di lavoro

Ora dobbiamo accedere al foglio di lavoro specifico con cui vogliamo lavorare:

```csharp
// Accesso al primo foglio di lavoro nel file Excel
Worksheet worksheet = workbook.Worksheets[0];
```

 Spiegazione: Il`Worksheets` la raccolta ci consente di accedere a fogli individuali. Utilizzando`[0]` fa riferimento al primo foglio di lavoro del file Excel, il che è generalmente una pratica comune quando si lavora con un file composto da un solo foglio.

## Passaggio 4: impostazione del filtro automatico

Ecco dove inizia la magia! Creeremo un intervallo AutoFilter per i nostri dati:

```csharp
// Creazione di un filtro automatico specificando l'intervallo di celle
worksheet.AutoFilter.Range = "A1:A18";
```

 Spiegazione: Il`AutoFilter.Range` proprietà consente di specificare quali righe filtrare. In questo caso, stiamo filtrando le righe nell'intervallo da A1 a A18, che si suppone contengano i nostri dati.

## Passaggio 5: applicare la condizione del filtro

Il passo successivo è definire la condizione del filtro. Vogliamo visualizzare solo quelle righe i cui valori della prima colonna iniziano con "Ba":

```csharp
// Inizializza il filtro per le righe che iniziano con la stringa "Ba"
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 Spiegazione: Il`Custom` metodo definisce la nostra logica di filtraggio. Il primo argomento (`0` ) indica che stiamo filtrando in base alla prima colonna (A) e`FilterOperatorType.BeginsWith` specifica la nostra condizione per cercare le righe che iniziano con "Ba".

## Passaggio 6: Aggiorna il filtro

Dopo aver applicato la condizione del filtro, dobbiamo assicurarci che Excel si aggiorni per riflettere le modifiche:

```csharp
// Aggiorna il filtro per mostrare/nascondere le righe filtrate
worksheet.AutoFilter.Refresh();
```

Spiegazione: questa riga richiama un aggiornamento su AutoFilter per garantire che le righe visibili corrispondano ai criteri di filtro applicati. È simile a premere il pulsante di aggiornamento in Excel.

## Passaggio 7: salvare il file Excel modificato

Adesso è il momento di salvare le modifiche apportate:

```csharp
// Salvataggio del file Excel modificato
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 Spiegazione: Il`Save` il metodo riscrive la Workbook modificata nel percorso di output specificato. Ciò rientra nella scrittura dei filtri definiti in un nuovo file in modo che i dati originali rimangano intatti.

## Fase 8: Conferma dell'output

Infine, confermiamo che la nostra operazione è andata a buon fine:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Spiegazione: questa semplice riga invia un messaggio di conferma alla console, informandoti che il processo di filtraggio è stato completato senza errori.

## Conclusione

In un mondo in cui la gestione dei dati può sembrare opprimente, padroneggiare funzionalità come AutoFilter in Excel tramite Aspose.Cells per .NET ti consente di manipolare i dati in modo efficiente ed efficace. Hai imparato a filtrare le righe di Excel che iniziano con "Ba", implementando il metodo passo dopo passo. Con la pratica, sarai in grado di adattare questo metodo a varie esigenze di filtraggio dei dati nei tuoi progetti in corso.

## Domande frequenti

### Qual è lo scopo del filtro automatico in Excel?  
AutoFilter consente agli utenti di ordinare e filtrare rapidamente i dati in un foglio di calcolo, facilitando l'attenzione su set di dati specifici.

### Posso filtrare in base a più criteri con Aspose.Cells?  
Sì, Aspose.Cells supporta opzioni di filtro avanzate che consentono di impostare più criteri.

### Ho bisogno di una licenza per utilizzare Aspose.Cells?  
Sebbene sia possibile iniziare con una prova gratuita, per usufruire di tutte le funzionalità e rimuovere eventuali limitazioni della prova è necessaria una licenza.

### Quali tipi di filtraggio posso eseguire utilizzando Aspose.Cells?  
Puoi filtrare i dati in base al valore, alla condizione (ad esempio inizia con o finisce con) e al filtro personalizzato per soddisfare le tue esigenze specifiche.

### Dove posso trovare maggiori informazioni su Aspose.Cells per .NET?  
 Puoi controllare la documentazione[Qui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
