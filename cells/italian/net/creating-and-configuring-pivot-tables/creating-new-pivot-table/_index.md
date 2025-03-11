---
title: Creare una nuova tabella pivot a livello di programmazione in .NET
linktitle: Creare una nuova tabella pivot a livello di programmazione in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Impara a creare una tabella pivot a livello di programmazione in .NET usando Aspose.Cells con la nostra guida passo-passo. Analizza in modo efficiente i tuoi dati.
weight: 13
url: /it/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creare una nuova tabella pivot a livello di programmazione in .NET

## Introduzione
Creare una tabella pivot può sembrare un compito intimidatorio, soprattutto quando lo si fa a livello di programmazione. Ma non temere! Con Aspose.Cells per .NET, mettere insieme una tabella pivot non è solo semplice, ma anche piuttosto potente per l'analisi dei dati. In questo tutorial, ti guideremo passo dopo passo su come creare una nuova tabella pivot in un'applicazione .NET. Che tu stia aggiungendo dati per vendite, sport o qualsiasi altra metrica aziendale, questa guida ti aiuterà a far funzionare le tue tabelle pivot in pochissimo tempo.

## Prerequisiti
Prima di tuffarcisi, assicuriamoci che tutto sia pronto per partire. Ecco cosa devi fare:

1. Installa .NET Framework: assicurati di avere .NET Framework installato sul tuo computer. Aspose.Cells supporta varie versioni, ma è meglio attenersi all'ultima.
2.  Libreria Aspose.Cells: è necessario disporre della libreria Aspose.Cells. È possibile[scaricalo qui](https://releases.aspose.com/cells/net/) ottenere un[licenza temporanea](https://purchase.aspose.com/temporary-license/) per la valutazione.
3. Configurazione IDE: avere a disposizione un IDE compatibile con C#, come Visual Studio, in cui poter avviare un nuovo progetto.
4. Conoscenza di base di C#: la familiarità con la programmazione in C# ti aiuterà a seguire il programma senza impantanarti troppo.

Tutto pronto? Ottimo! Passiamo all'importazione dei pacchetti necessari.

## Importa pacchetti
Per prima cosa, devi importare i namespace richiesti nel tuo progetto C#. Apri il tuo file C# e aggiungi le seguenti direttive using:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Questi namespace forniscono l'accesso alle funzionalità di cartella di lavoro, foglio di lavoro e tabella pivot che utilizzeremo in questo tutorial.

## Passaggio 1: creare un oggetto cartella di lavoro
Creare una cartella di lavoro è l'inizio del tuo viaggio. Iniziamo con l'istanziare una nuova cartella di lavoro e accedere al primo foglio di lavoro.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();

// Ottenere il riferimento del foglio di lavoro appena aggiunto
Worksheet sheet = workbook.Worksheets[0];
```

 In questo passaggio creiamo un`Workbook`istanza che rappresenta il nostro file Excel e prendiamo il primo foglio di lavoro, che sarà il nostro campo di gioco per la tabella pivot.

## Passaggio 2: inserire i dati nelle celle
Ora, popoliamo il nostro foglio di lavoro con alcuni dati campione. Inseriremo righe per diversi sport, trimestri e cifre di vendita per dare alla nostra tabella pivot qualcosa da riassumere.

```csharp
Cells cells = sheet.Cells;

// Impostazione del valore nelle celle
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Riempimento cella dati = cells["A2"];
cell.PutValue("Golf");
// ... Ulteriori voci di dati
```

Qui, stiamo definendo le intestazioni delle nostre colonne e inserendo valori sotto ogni intestazione. Questi dati fungeranno da origine per la nostra tabella pivot, quindi assicurati che siano organizzati! Segui questo blocco e creerai un set di dati completo.

## Passaggio 3: aggiunta di una tabella pivot
Con i nostri dati pronti, è il momento di creare la tabella pivot. Utilizzeremo la raccolta di tabelle pivot dal foglio di lavoro per aggiungere la nostra nuova tabella pivot.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Aggiungere una tabella pivot al foglio di lavoro
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

In questo frammento, aggiungiamo una tabella pivot al foglio di lavoro che fa riferimento al nostro intervallo di dati (in questo caso, celle da A1 a C8). Posizioniamo la tabella pivot a partire dalla cella E3 e la chiamiamo "PivotTable2". Semplice, vero?

## Passaggio 4: personalizzare la tabella pivot
Ora che abbiamo la nostra tabella pivot, personalizziamola per mostrare riepiloghi significativi. Possiamo controllare cosa appare nelle righe, colonne e aree dati della tabella pivot.

```csharp
// Accesso all'istanza della tabella pivot appena aggiunta
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Disattivazione della visualizzazione dei totali generali per le righe.
pivotTable.RowGrand = false;

// Trascinando il primo campo nell'area della riga.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Trascinando il secondo campo nell'area della colonna.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Trascinando il terzo campo nell'area dati.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

In questo passaggio, diciamo alla tabella pivot di nascondere i totali generali per le righe e poi specifichiamo quali campi vanno nelle aree riga, colonna e dati. I nomi degli sport riempiranno le righe, i trimestri riempiranno le colonne e le cifre delle vendite forniranno i riepiloghi.

## Passaggio 5: salvare la cartella di lavoro
Infine, vogliamo salvare la nostra cartella di lavoro appena creata per vedere i frutti del nostro lavoro.

```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Basta specificare un percorso corretto e l'output della tabella pivot verrà salvato in un file Excel che potrai aprire e rivedere.

## Conclusione
Creare tabelle pivot a livello di programmazione usando Aspose.Cells per .NET può farti risparmiare molto tempo, specialmente quando hai a che fare con grandi set di dati. Hai imparato come impostare il tuo progetto, importare i pacchetti necessari, popolare i dati e creare una tabella pivot personalizzabile da zero. Quindi, la prossima volta che ti ritrovi sommerso dai numeri, ricorda questo tutorial e lascia che Aspose.Cells faccia il grosso del lavoro per te.

## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una potente libreria .NET per creare e gestire fogli di calcolo Excel a livello di programmazione.

### Esiste una prova gratuita per Aspose.Cells?
 Sì, puoi ottenere una prova gratuita[Qui](https://releases.aspose.com/).

### Posso personalizzare l'aspetto della tabella pivot?
Assolutamente! Puoi personalizzare la formattazione, il layout e persino gli stili della tabella pivot in base alle tue esigenze.

### Dove posso trovare altri esempi e documentazione su Aspose.Cells?
 Puoi controllare il[documentazione](https://reference.aspose.com/cells/net/) per guide ed esempi completi.

### Come posso ottenere supporto per Aspose.Cells?
 Puoi ottenere supporto tramite[Forum di Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
