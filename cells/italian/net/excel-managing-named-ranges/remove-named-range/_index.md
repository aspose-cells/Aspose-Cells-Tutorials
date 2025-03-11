---
title: Rimuovere l'intervallo denominato in Excel
linktitle: Rimuovere l'intervallo denominato in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come rimuovere intervalli denominati in Excel utilizzando Aspose.Cells per .NET con istruzioni dettagliate passo dopo passo.
weight: 11
url: /it/net/excel-managing-named-ranges/remove-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rimuovere l'intervallo denominato in Excel

## Introduzione
Excel è diventato un punto fermo nella gestione e nell'analisi dei dati per molti individui e organizzazioni. Che tu sia un analista di dati esperto o semplicemente qualcuno a cui piace organizzare i propri dati, padroneggiare Excel è essenziale. Oggi, ci immergiamo in una funzionalità specifica ma potente: la rimozione di intervalli denominati tramite Aspose.Cells per .NET. Questa guida ti guiderà attraverso i passaggi per ottenere questo risultato in modo efficace. Quindi, rimboccati le maniche e iniziamo!

## Prerequisiti

Prima di passare alla codifica vera e propria, ecco alcune cose che devi sapere:

### Configurazione dell'ambiente .NET

Per lavorare senza problemi con Aspose.Cells per .NET, assicurati di avere quanto segue:

1.  Visual Studio: Scarica e installa Visual Studio (la Community Edition è perfetta) che puoi trovare su[Sito web di Visual Studio](https://visualstudio.microsoft.com/).
2. .NET Framework: assicurati di utilizzare una versione appropriata di .NET Framework. Aspose.Cells supporta .NET Framework 4.0 e versioni successive.
3. Libreria Aspose.Cells: devi scaricare e fare riferimento alla libreria Aspose.Cells per .NET nella tua applicazione. Puoi trovare il pacchetto scaricabile[Qui](https://releases.aspose.com/cells/net/).

### Nozioni di base di C#

Avrai bisogno di una conoscenza di base della programmazione C#. Questo ti aiuterà a comprendere i frammenti di codice che discuteremo.

### Accesso ai file Excel

Assicurati di avere a portata di mano un file Excel con cui fare esperimenti. In caso contrario, puoi crearne uno rapidamente utilizzando Microsoft Excel.

## Importa pacchetti

Ora che abbiamo coperto i nostri prerequisiti, importiamo i pacchetti di cui avremo bisogno nel nostro progetto. Apri Visual Studio e crea una nuova applicazione console. Quindi, includi il seguente namespace nel tuo programma:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Questa configurazione consente di sfruttare le funzionalità fornite da Aspose.Cells per manipolare facilmente i fogli Excel.

## Passaggio 1: impostazione della directory di output

Per prima cosa, dobbiamo definire dove verrà salvato il nostro file di output. Questo è fondamentale perché evita confusione in seguito su dove si trovano i tuoi file.

```csharp
// Directory di uscita
string outputDir = "Your Document Directory Here\\";
```

 Sostituire`"Your Document Directory Here\\"`con il percorso sul computer in cui desideri salvare il file.

## Passaggio 2: creazione di una nuova cartella di lavoro

Come si inizia con una lavagna nuova? Creando un nuovo quaderno di lavoro, ovviamente! Questo quaderno di lavoro servirà come tela bianca.

```csharp
// Crea una nuova cartella di lavoro.
Workbook workbook = new Workbook();
```

Questa riga di codice crea una nuova cartella di lavoro che possiamo manipolare.

## Passaggio 3: accesso alla raccolta di fogli di lavoro

Ogni cartella di lavoro è composta da uno o più fogli di lavoro. Per lavorare all'interno di un foglio di lavoro specifico, abbiamo bisogno di accedere a questa raccolta.

```csharp
// Ottieni tutti i fogli di lavoro presenti nel libro.
WorksheetCollection worksheets = workbook.Worksheets;
```

Qui abbiamo recuperato tutti i fogli di lavoro disponibili nella nostra nuova cartella di lavoro.

## Fase 4: Selezione del primo foglio di lavoro

Ora vogliamo lavorare sul primo foglio di lavoro, che in molti casi rappresenta il punto di partenza predefinito.

```csharp
// Ottieni il primo foglio di lavoro nella raccolta dei fogli di lavoro.
Worksheet worksheet = workbook.Worksheets[0];
```

Questo frammento di codice ci consente di selezionare facilmente il primo foglio di lavoro.

## Passaggio 5: creazione di intervalli denominati

Ora, creiamo un intervallo denominato, che è una parte essenziale di questo tutorial. Ciò ci consentirà di illustrare come rimuovere un intervallo denominato in seguito.

```csharp
// Crea un intervallo di celle.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Assegna un nome all'intervallo.
range1.Name = "FirstRange";
```

Qui definiamo un intervallo dalle celle E12 a I12 e lo chiamiamo "FirstRange".

## Passaggio 6: formattazione dell'intervallo denominato

Per dimostrare la versatilità di Aspose.Cells, aggiungiamo un po' di formattazione al nostro intervallo denominato.

```csharp
// Imposta il bordo del contorno sull'intervallo.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

Stiamo aggiungendo un bordo blu navy di medie dimensioni attorno alla nostra gamma per renderla visivamente accattivante.

## Passaggio 7: inserimento dei dati nell'intervallo

Ora possiamo popolare le nostre celle con alcuni dati per renderle funzionali.

```csharp
// Inserire alcuni dati con alcune formattazioni in alcune celle dell'intervallo.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

In questo passaggio abbiamo inserito la parola "Test" nella cella E12 e il numero 123 nella cella I12.

## Passaggio 8: creazione di un altro intervallo denominato

Per illustrare meglio il nostro punto, creeremo un altro intervallo denominato simile al primo.

```csharp
//Crea un altro intervallo di celle.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Assegna un nome all'intervallo.
range2.Name = "SecondRange";
```

Ora abbiamo a disposizione un altro intervallo denominato "SecondRange".

## Passaggio 9: Copia del primo intervallo nel secondo intervallo

Mostriamo come utilizzare il nostro secondo intervallo copiando i dati dal primo intervallo.

```csharp
// Copia il primo intervallo nel secondo intervallo.
range2.Copy(range1);
```

Con questo passaggio abbiamo effettivamente duplicato i dati da "FirstRange" a "SecondRange".

## Passaggio 10: rimozione dell'intervallo denominato

Ora il momento clou del nostro tutorial: la rimozione dell'intervallo denominato. Ecco dove tutto si unisce.

```csharp
// Rimuovere l'intervallo denominato precedente (range1) con il suo contenuto.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Questa riga cancella il contenuto dell'intervallo che vogliamo rimuovere, assicurandoci di non lasciare alcuna traccia!

## Passaggio 11: eliminazione dell'intervallo denominato dal foglio di lavoro

Un ultimo importante passaggio consiste nel rimuovere l'intervallo denominato dalla raccolta dei nomi del foglio di lavoro.

```csharp
worksheets.Names.RemoveAt(0);
```

Ciò rimuoverà effettivamente l'intervallo denominato "FirstRange" dalla cartella di lavoro.

## Passaggio 12: salvataggio della cartella di lavoro

Ultimo ma non meno importante, salviamo il nostro lavoro. 

```csharp
// Salvare il file Excel.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Questo comando salva la cartella di lavoro con le modifiche apportate: è qui che viene preservato tutto il tuo duro lavoro!

## Fase 13: Conferma dell'esecuzione corretta

Per concludere in modo più ordinato, potresti voler inviare un messaggio di successo alla console.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Questo ti avvisa che l'intera operazione è stata completata senza intoppi!

## Conclusione

Seguendo questa guida, hai imparato a manipolare intervalli denominati in Excel usando Aspose.Cells per .NET. Hai creato intervalli, li hai popolati con dati, ne hai copiato il contenuto e infine li hai rimossi, assicurandoti che il tuo file Excel rimanesse organizzato e pulito. Excel, proprio come un bar affollato, prospera grazie all'organizzazione. Quindi, che tu stia gestendo dati per un report o abbellendo il tuo foglio di budget personale, padroneggiare gli intervalli denominati può aiutarti a elaborare alcune soluzioni efficienti. 

## Domande frequenti

### Che cos'è Aspose.Cells?
Aspose.Cells è una libreria .NET progettata per la manipolazione programmatica di file Excel.

### Posso rimuovere più intervalli denominati contemporaneamente?
Sì, è possibile scorrere la raccolta di intervalli denominati e rimuoverli in base alle esigenze.

### È disponibile una versione di prova?
 Sì, puoi scaricare una versione di prova gratuita di Aspose.Cells[Qui](https://releases.aspose.com/).

### Quali linguaggi di programmazione supporta Aspose.Cells?
Supporta principalmente i linguaggi .NET come C# e VB.NET, tra gli altri.

### Dove posso cercare supporto se ho dei problemi?
 Puoi visitare il[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9) per qualsiasi domanda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
