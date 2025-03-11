---
title: Mantieni il prefisso a virgolette del valore della cella o dell'intervallo in Excel
linktitle: Mantieni il prefisso a virgolette del valore della cella o dell'intervallo in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come conservare i prefissi degli apici singoli nelle celle di Excel utilizzando Aspose.Cells per .NET con questo semplice tutorial passo dopo passo.
weight: 10
url: /it/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mantieni il prefisso a virgolette del valore della cella o dell'intervallo in Excel

## Introduzione

Quando lavori su file Excel, potresti trovarti in situazioni in cui devi preservare un singolo apice come prefisso nei valori delle celle. Questo può essere particolarmente cruciale quando i dati che stai gestendo necessitano di tale attenzione extra, come nel caso di identificatori o stringhe in cui non vuoi che Excel interpreti il valore. In questa guida, ci immergeremo in come ottenere questo risultato utilizzando Aspose.Cells per .NET. Quindi, prendi la tua bevanda preferita e iniziamo!

## Prerequisiti

Prima di intraprendere questo viaggio di programmazione, assicuriamoci di avere tutto ciò di cui hai bisogno:

1. Visual Studio: per eseguire il codice .NET avrai bisogno di un ambiente di sviluppo.
2.  Aspose.Cells per .NET: assicurati di aver scaricato questa libreria e di averla referenziata nel tuo progetto. Puoi prendere l'ultima versione da[Link per scaricare](https://releases.aspose.com/cells/net/).
3. Nozioni di base sulla programmazione C#: è utile conoscere C#, soprattutto se si prevede di modificare il codice.
4. Un sistema operativo Windows: poiché Aspose.Cells è principalmente incentrato su Windows, averlo installato renderà le cose più fluide.

Ora che abbiamo la nostra checklist, passiamo alla parte divertente: la codifica!

## Importa pacchetti

Per dare il via alle cose, dobbiamo importare i pacchetti necessari nel nostro progetto C#. Ecco il pacchetto che dovresti cercare:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Questa riga fornisce accesso a tutte le classi e ai metodi forniti dalla libreria Aspose.Cells, consentendo di manipolare i file Excel senza sforzo. 

Ora spieghiamo nel dettaglio i passaggi per mantenere il prefisso dell'apice singolo nei valori delle celle.

## Passaggio 1: impostare la cartella di lavoro

Per prima cosa dobbiamo creare una nuova cartella di lavoro e specificare le directory per i file di input e output.

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory/";

// Directory di uscita
string outputDir = "Your Document Directory/";

// Crea cartella di lavoro
Workbook wb = new Workbook();
```

 In questo passaggio, stiamo inizializzando la nostra cartella di lavoro, dove verranno gestiti i file Excel. Sostituisci`"Your Document Directory"` con il percorso effettivo in cui desideri archiviare i file.

## Passaggio 2: accedi al foglio di lavoro

Poi, mettiamo le mani sul primo foglio di lavoro del workbook. È qui che avrà luogo la nostra azione.

```csharp
// Accedi al primo foglio di lavoro
Worksheet ws = wb.Worksheets[0];
```

In questo modo viene semplicemente selezionato il primo foglio di lavoro, il che solitamente va bene per la maggior parte delle attività, a meno che non si abbiano esigenze specifiche per più fogli.

## Passaggio 3: accedere e modificare il valore della cella

Ora lavoriamo con una cella specifica: scegliamo la cella A1. 

```csharp
// Accedi alla cella A1
Cell cell = ws.Cells["A1"];

// Inserisci del testo nella cella, non deve avere virgolette singole all'inizio
cell.PutValue("Text");
```

In questo passaggio, inseriamo un valore nella cella A1 senza virgolette singole. Ma controlliamo lo stile della cella!

## Passaggio 4: controllare il prefisso del preventivo

È il momento di dare un'occhiata allo stile della nostra cella e verificare se il valore del prefisso tra virgolette è impostato.

```csharp
// Stile di accesso della cella A1
Style st = cell.GetStyle();

// Stampa il valore di Style.QuotePrefix della cella A1
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Qui, accediamo alle informazioni di stile per la cella. Inizialmente, il prefisso delle virgolette dovrebbe essere falso, poiché non c'è una virgoletta singola.

## Passaggio 5: aggiungere un prefisso con virgolette singole

Ora proviamo a sperimentare inserendo un singolo apice nel valore della cella.

```csharp
// Inserisci del testo nella cella, deve avere una virgoletta singola all'inizio
cell.PutValue("'Text");

// Stile di accesso della cella A1
st = cell.GetStyle();

// Stampa il valore di Style.QuotePrefix della cella A1
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Dopo questo passaggio, scoprirai che il prefisso delle virgolette cambia in true! Ciò dimostra che la nostra cella Excel è ora impostata per riconoscere la virgoletta singola.

## Passaggio 6: comprendere StyleFlags

 Ora, esploriamo come il`StyleFlag` può avere un impatto sul prefisso del nostro preventivo.

```csharp
// Crea uno stile vuoto
st = wb.CreateStyle();

// Crea flag di stile - imposta StyleFlag.QuotePrefix su falso
StyleFlag flag = new StyleFlag();
flag.QuotePrefix = false;

// Crea un intervallo costituito dalla singola cella A1
Range rng = ws.Cells.CreateRange("A1");

// Applica lo stile all'intervallo
rng.ApplyStyle(st, flag);
```

 Ecco il trucco! Specificando`flag.QuotePrefix = false`, stiamo dicendo al programma: "Ehi, non toccare il prefisso esistente". Quindi cosa succede?

## Passaggio 7: ricontrollare il prefisso del preventivo

Vediamo come le nostre modifiche influiscono sul prefisso di citazione esistente.

```csharp
// Accedi allo stile della cella A1
st = cell.GetStyle();

// Stampa il valore di Style.QuotePrefix della cella A1
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

Dopo aver applicato questo stile, l'output continuerà a essere true, perché non lo abbiamo aggiornato.

## Passaggio 8: Aggiorna il prefisso della citazione con StyleFlag

Bene, vediamo cosa succede quando vogliamo aggiornare il nostro prefisso.

```csharp
// Crea uno stile vuoto
st = wb.CreateStyle();

// Crea flag di stile - imposta StyleFlag.QuotePrefix come vero
flag = new StyleFlag();
flag.QuotePrefix = true;

// Applica lo stile all'intervallo
rng.ApplyStyle(st, flag);
```

In questo round, stiamo impostando`flag.QuotePrefix = true`, il che significa che vogliamo aggiornare il prefisso della cella.

## Fase 9: Controllo finale del prefisso del preventivo

Concludiamo controllando come appare ora il prefisso della citazione:

```csharp
// Accedi allo stile della cella A1
st = cell.GetStyle();

// Stampa il valore di Style.QuotePrefix della cella A1
Console.WriteLine("Quote Prefix of Cell A1: " + st.QuotePrefix);
```

A questo punto, l'output dovrebbe essere falso poiché abbiamo dichiarato esplicitamente di voler aggiornare il prefisso.

## Conclusione

Ed ecco fatto! Seguendo questi passaggi, hai imparato come preservare il prefisso a virgolette singole nei valori delle celle durante l'utilizzo di Aspose.Cells per .NET. Sebbene possa sembrare un piccolo dettaglio, mantenere l'integrità dei dati in Excel può essere cruciale in molte applicazioni, soprattutto se si gestiscono identificatori o stringhe formattate. 

## Domande frequenti

### Qual è lo scopo del prefisso apice singolo in Excel?  
Il prefisso con virgolette singole indica a Excel di trattare il valore come testo, il che garantisce che non venga interpretato come un numero o una formula.

### Posso usare Aspose.Cells nelle applicazioni web?  
Sì! Aspose.Cells per .NET funziona bene sia con le applicazioni desktop che con quelle web.

### Ci sono considerazioni sulle prestazioni quando si utilizza Aspose.Cells?  
In genere, Aspose.Cells è ottimizzato per le prestazioni, ma per set di dati molto grandi è sempre bene testare la memoria e la velocità.

### Come posso ottenere assistenza se riscontro problemi?  
 Puoi visitare il[forum di supporto](https://forum.aspose.com/c/cells/9) per ricevere assistenza dalla comunità e dallo staff di Aspose.

### Posso provare Aspose.Cells senza acquistarlo?  
 Assolutamente! Puoi accedere a una prova gratuita[Qui](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
