---
"description": "Scopri come impostare i formati dei campi di pagina nelle tabelle pivot a livello di codice utilizzando Aspose.Cells per .NET. Segui il nostro tutorial passo passo per una gestione dei dati impeccabile."
"linktitle": "Impostazione del formato del campo di pagina a livello di programmazione in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Impostazione del formato del campo di pagina a livello di programmazione in .NET"
"url": "/it/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Impostazione del formato del campo di pagina a livello di programmazione in .NET

## Introduzione
Creare e manipolare file Excel tramite codice può essere molto utile, soprattutto quando si devono analizzare dataset di grandi dimensioni. Uno degli strumenti più efficaci a disposizione è Aspose.Cells per .NET, che consente di interagire a livello di codice con i file Excel e di creare strutture di reporting complesse. In questo tutorial, approfondiremo come impostare i formati dei campi pagina in una tabella pivot utilizzando questa potente libreria. Che siate sviluppatori esperti o principianti, al termine di questa guida avrete acquisito una solida conoscenza di come utilizzare le tabelle pivot e le loro diverse impostazioni in .NET.
## Prerequisiti
Prima di immergerci a capofitto nella programmazione, assicuriamoci di aver configurato tutto correttamente. Avrai bisogno di quanto segue:
- Visual Studio: un ambiente di lavoro in cui puoi scrivere ed eseguire il codice .NET.
- Aspose.Cells: puoi scaricare la libreria [Qui](https://releases.aspose.com/cells/net/).
- Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
- File Excel: avere pronto un file Excel (come `Book1.xls`) contenente dati adatti alla creazione di tabelle pivot. 
Se non l'hai ancora fatto, ottieni la tua prova gratuita di Aspose.Cells [Qui](https://releases.aspose.com/).
## Importa pacchetti
Per iniziare, devi importare i pacchetti corretti nel tuo progetto. Inizia aggiungendo riferimenti alla libreria Aspose.Cells nel tuo progetto C#. Ecco come fare:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Verranno inserite tutte le classi e i metodi necessari per manipolare i file Excel utilizzando Aspose.Cells.
## Passaggio 1: configura il tuo spazio di lavoro
Inizia definendo la directory di lavoro in cui verranno archiviati i file Excel. Ad esempio, puoi dichiarare una variabile come questa:
```csharp
string dataDir = "Your Document Directory";
```
## Caricamento della cartella di lavoro
Il prossimo passo è caricare il nostro modello Excel. Questo è un passaggio fondamentale perché definisce il contesto delle nostre operazioni:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Questa riga carica la cartella di lavoro esistente dalla directory specificata.
## Passaggio 2: accedi al foglio di lavoro
Una volta caricata la cartella di lavoro, è il momento di accedere al foglio di lavoro che contiene la tabella pivot o i dati che si desidera analizzare. Ecco come fare:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Questo comando cattura il primo foglio di lavoro della cartella di lavoro caricata. Puoi facilmente modificare l'indice se stai lavorando con più fogli.
## Passaggio 3: accesso alla tabella pivot
Proseguendo, accediamo alla tabella pivot nel foglio di lavoro scelto. Se si utilizza una singola tabella pivot, è possibile impostarne l'indice su `0`:
```csharp
int pivotindex = 0;
// Accesso alla tabella pivot
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Questo frammento di codice seleziona la prima tabella pivot nel foglio di lavoro. 
## Passaggio 4: configurazione della tabella pivot
Ora arriva la parte interessante! Impostiamo la tabella pivot in modo che mostri i totali complessivi per le righe:
```csharp
pivotTable.RowGrand = true;
```
Questa riga garantisce che il report visualizzi i totali generali, che possono costituire un riepilogo utile per l'analisi dei dati.
## Passaggio 5: accesso e configurazione dei campi di riga
Ora dobbiamo accedere ai campi riga della tabella pivot:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Questa raccolta ci consente di manipolare i campi in base alle nostre esigenze.
## Configura il campo della prima riga
Vuoi impostare tipi di subtotale specifici? Accediamo al primo campo della nostra raccolta e configuriamolo:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Impostazione dei subtotali.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
Abilitando `Sum` E `Count` subtotali, possiamo riassumere rapidamente i dati nel nostro report.
## Passaggio 6: impostazione delle opzioni di ordinamento automatico
Ora, mettiamo in pratica un ordinamento intelligente. In questo modo, la tabella pivot disporrà i dati in un ordine significativo:
```csharp
// Impostazione delle opzioni di ordinamento automatico.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Utilizzando un campo di ordinamento predefinito.
```
Questo frammento di codice abilita l'ordinamento automatico e specifica l'ordine crescente. 
## Passaggio 7: impostazione delle opzioni di visualizzazione automatica
Desideri filtrare ulteriormente i tuoi dati? L'opzione AutoShow è utile per mostrare punti dati specifici in determinate condizioni:
```csharp
// Impostazione delle opzioni di visualizzazione automatica.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Specifica il campo da visualizzare automaticamente.
```
In questo modo si garantisce che la tabella pivot visualizzi solo i dati rilevanti, migliorando la chiarezza e l'attenzione.
## Passaggio 8: salvataggio del lavoro
Dopo tutte queste configurazioni, non vorrai perdere il tuo lavoro! Salva la cartella di lavoro modificata in questo modo:
```csharp
workbook.Save(dataDir + "output.xls");
```
Ora puoi trovare il file Excel appena creato nella directory dei documenti.
## Conclusione
Ed ecco fatto! Abbiamo illustrato un approccio completo e pratico per impostare i formati dei campi pagina a livello di codice in una tabella pivot utilizzando Aspose.Cells per .NET. Con i semplici passaggi illustrati, dovresti sentirti sicuro nel modificare i dati di Excel in base alle tue esigenze di reporting. È incredibile cosa si può ottenere combinando la potenza di C# con Aspose.Cells.
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una libreria .NET che consente agli sviluppatori di creare, manipolare e convertire file Excel a livello di programmazione.
### Come faccio a installare Aspose.Cells?
Puoi scaricarlo direttamente da [Sito web di Aspose](https://releases.aspose.com/cells/net/).
### Posso usare Aspose.Cells senza installare Excel?
Sì, Aspose.Cells è una libreria autonoma che non richiede l'installazione di Microsoft Excel.
### Dove posso trovare supporto dettagliato?
Puoi accedere al supporto dettagliato e ai forum su [Supporto Aspose](https://forum.aspose.com/c/cells/9).
### Come posso ottenere una licenza temporanea?
È possibile acquisire una licenza temporanea da [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}