---
"description": "Impara a creare una tabella pivot in .NET tramite Aspose.Cells con la nostra guida passo passo. Analizza i tuoi dati in modo efficiente."
"linktitle": "Creare una nuova tabella pivot a livello di programmazione in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Creare una nuova tabella pivot a livello di programmazione in .NET"
"url": "/it/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Creare una nuova tabella pivot a livello di programmazione in .NET

## Introduzione
Creare una tabella pivot può sembrare un compito arduo, soprattutto se lo si fa a livello di codice. Ma niente paura! Con Aspose.Cells per .NET, creare una tabella pivot non è solo semplice, ma anche molto potente per l'analisi dei dati. In questo tutorial, vi guideremo passo dopo passo nella creazione di una nuova tabella pivot in un'applicazione .NET. Che stiate aggiungendo dati per le vendite, gli eventi sportivi o qualsiasi altra metrica aziendale, questa guida vi aiuterà a rendere operative le vostre tabelle pivot in pochissimo tempo.

## Prerequisiti
Prima di iniziare, assicuriamoci che tutto sia pronto. Ecco cosa devi fare:

1. Installa .NET Framework: assicurati di aver installato .NET Framework sul tuo computer. Aspose.Cells supporta diverse versioni, ma è meglio utilizzare la versione più recente.
2. Libreria Aspose.Cells: è necessaria la libreria Aspose.Cells. Puoi [scaricalo qui](https://releases.aspose.com/cells/net/) o ottenere un [licenza temporanea](https://purchase.aspose.com/temporary-license/) per la valutazione.
3. Configurazione IDE: avere a disposizione un IDE compatibile con C#, come Visual Studio, da cui poter avviare un nuovo progetto.
4. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a seguire il tutorial senza impantanarti troppo.

Tutto pronto? Ottimo! Iniziamo a importare i pacchetti necessari.

## Importa pacchetti
Per prima cosa, devi importare gli spazi dei nomi richiesti nel tuo progetto C#. Apri il file C# e aggiungi le seguenti direttive using:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Questi namespace forniscono l'accesso alle funzionalità di cartella di lavoro, foglio di lavoro e tabella pivot che utilizzeremo in questo tutorial.

## Passaggio 1: creare un oggetto cartella di lavoro
Creare una cartella di lavoro è l'inizio del tuo viaggio. Iniziamo creando una nuova cartella di lavoro e accedendo al primo foglio di lavoro.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creazione di un'istanza di un oggetto Workbook
Workbook workbook = new Workbook();

// Ottenere il riferimento del foglio di lavoro appena aggiunto
Worksheet sheet = workbook.Worksheets[0];
```

In questo passaggio creiamo un `Workbook` istanza che rappresenta il nostro file Excel e prendiamo il primo foglio di lavoro, che sarà il nostro campo di gioco per la tabella pivot.

## Passaggio 2: inserire i dati nelle celle
Ora, riempiamo il nostro foglio di lavoro con alcuni dati di esempio. Inseriremo righe per diversi sport, trimestri e dati di vendita per fornire alla nostra tabella pivot un riepilogo.

```csharp
Cells cells = sheet.Cells;

// Impostazione del valore nelle celle
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Riempimento datacell = cells["A2"];
cell.PutValue("Golf");
// ... Ulteriori inserimenti di dati
```

Qui definiamo le intestazioni di colonna e inseriamo valori sotto ogni intestazione. Questi dati fungeranno da fonte per la nostra tabella pivot, quindi assicuratevi che siano organizzati! Seguite questo passaggio e creerete un set di dati completo.

## Passaggio 3: aggiunta di una tabella pivot
Con i dati pronti, è il momento di creare la tabella pivot. Useremo la raccolta di tabelle pivot dal foglio di lavoro per aggiungere la nostra nuova tabella pivot.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Aggiungere una tabella pivot al foglio di lavoro
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

In questo frammento, aggiungiamo una tabella pivot al foglio di lavoro che fa riferimento al nostro intervallo di dati (in questo caso, le celle da A1 a C8). Posizioniamo la tabella pivot a partire dalla cella E3 e la chiamiamo "TabellaPivot2". Semplice, vero?

## Passaggio 4: personalizzare la tabella pivot
Ora che abbiamo la nostra tabella pivot, personalizziamola per visualizzare riepiloghi significativi. Possiamo controllare cosa appare nelle righe, nelle colonne e nelle aree dati della tabella pivot.

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

In questa fase, indichiamo alla tabella pivot di nascondere i totali complessivi per riga e poi specifichiamo quali campi vanno inseriti nelle aree riga, colonna e dati. I nomi degli sport riempiranno le righe, i trimestri riempiranno le colonne e i dati di vendita forniranno i riepiloghi.

## Passaggio 5: salvare la cartella di lavoro
Infine, vogliamo salvare la cartella di lavoro appena creata per vedere i frutti del nostro lavoro.

```csharp
// Salvataggio del file Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Basta specificare il percorso corretto e l'output della tabella pivot verrà salvato in un file Excel che potrai aprire e rivedere.

## Conclusione
Creare tabelle pivot a livello di codice utilizzando Aspose.Cells per .NET può farti risparmiare notevolmente tempo, soprattutto quando gestisci dataset di grandi dimensioni. Hai imparato come configurare il tuo progetto, importare i pacchetti necessari, popolare i dati e creare da zero una tabella pivot personalizzabile. Quindi, la prossima volta che ti ritrovi immerso nei numeri, ricorda questo tutorial e lascia che Aspose.Cells faccia il grosso del lavoro per te.

## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria .NET per la creazione e la gestione di fogli di calcolo Excel a livello di programmazione.

### Esiste una prova gratuita per Aspose.Cells?
Sì, puoi ottenere una prova gratuita [Qui](https://releases.aspose.com/).

### Posso personalizzare l'aspetto della tabella pivot?
Assolutamente! Puoi personalizzare la formattazione, il layout e persino gli stili della tabella pivot in base alle tue esigenze.

### Dove posso trovare altri esempi e documentazione su Aspose.Cells?
Puoi controllare il [documentazione](https://reference.aspose.com/cells/net/) per guide ed esempi completi.

### Come posso ottenere supporto per Aspose.Cells?
Puoi ottenere supporto tramite [Forum di Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}