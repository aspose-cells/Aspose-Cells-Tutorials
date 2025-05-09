---
"description": "Scopri come aggiungere una casella combinata a un foglio di lavoro Excel tramite codice utilizzando Aspose.Cells per .NET. Questa guida dettagliata ti guiderà passo passo in ogni dettaglio."
"linktitle": "Aggiungi casella combinata al foglio di lavoro in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Aggiungi casella combinata al foglio di lavoro in Excel"
"url": "/it/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi casella combinata al foglio di lavoro in Excel

## Introduzione
La creazione di fogli di calcolo Excel interattivi può migliorare notevolmente l'esperienza utente, soprattutto quando si aggiungono elementi ai moduli come le caselle combinate. Le caselle combinate consentono agli utenti di selezionare opzioni da un elenco predefinito, semplificando ed efficientendo l'inserimento dei dati. Con Aspose.Cells per .NET, è possibile creare caselle combinate nei fogli Excel a livello di codice, senza utilizzare Excel direttamente. Questa potente libreria consente agli sviluppatori di manipolare i file Excel in vari modi, inclusa la possibilità di automatizzare i controlli dei moduli.
In questo tutorial, ti guideremo attraverso il processo di aggiunta di una casella combinata a un foglio di lavoro in Excel utilizzando Aspose.Cells per .NET. Se desideri creare fogli di calcolo dinamici e intuitivi, questa guida ti aiuterà a iniziare.
## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di avere tutto il necessario:
- Aspose.Cells per .NET: Scarica e installa la libreria Aspose.Cells per .NET da [pagina di download](https://releases.aspose.com/cells/net/).
- .NET Framework: assicurati di aver installato .NET Framework sul tuo computer. Qualsiasi versione supportata da Aspose.Cells funzionerà.
- Ambiente di sviluppo: utilizza un IDE come Visual Studio per gestire il progetto e scrivere il codice.
- Licenza Aspose: puoi lavorare senza licenza in modalità di valutazione, ma per una versione completa dovrai applicare una licenza. Ottieni una [licenza temporanea](https://purchase.aspose.com/temporary-license/) se necessario.
## Importa pacchetti
Per iniziare, devi importare gli spazi dei nomi richiesti nel tuo progetto. Ecco cosa ti serve:
```csharp
using System.IO;
using Aspose.Cells;
```
Sono essenziali per interagire con i file Excel e manipolare gli elementi dei moduli, come le caselle combinate nella cartella di lavoro.
Per facilitarne la comprensione, scomponiamo il processo di aggiunta di una casella combinata in più semplici passaggi.
## Passaggio 1: impostare la directory dei documenti
Il primo passo è creare una directory in cui salvare i file Excel. Puoi creare una nuova cartella se non esiste già.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: specifica la posizione in cui verrà salvato il file di output.
- System.IO.Directory.Exists: controlla se la directory esiste già.
- System.IO.Directory.CreateDirectory: crea la directory se mancante.
## Passaggio 2: creare una nuova cartella di lavoro
Ora crea una nuova cartella di lavoro Excel in cui aggiungerai la casella combinata.

```csharp
// Crea una nuova cartella di lavoro.
Workbook workbook = new Workbook();
```

- Cartella di lavoro cartella di lavoro: Inizializza una nuova istanza della classe Workbook, che rappresenta un file Excel.
## Passaggio 3: Ottieni il foglio di lavoro e le celle
Successivamente, accedi al primo foglio di lavoro dalla cartella di lavoro e recupera la raccolta di celle in cui inserirai i dati.

```csharp
// Ottieni il primo foglio di lavoro.
Worksheet sheet = workbook.Worksheets[0];
// Ottieni la raccolta di celle del foglio di lavoro.
Cells cells = sheet.Cells;
```

- Foglio di lavoro: recupera il primo foglio di lavoro dalla cartella di lavoro.
- Celle celle: Ottiene la raccolta di celle dal foglio di lavoro.
## Passaggio 4: immettere i valori per la casella combinata
Ora dobbiamo inserire alcuni valori nelle celle. Questi valori serviranno come opzioni per la casella combinata.

```csharp
// Inserisci un valore.
cells["B3"].PutValue("Employee:");
// Impostalo in grassetto.
cells["B3"].GetStyle().Font.IsBold = true;
// Immettere alcuni valori che indicano l'intervallo di input per la casella combinata.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: inserisce l'etichetta "Dipendente" nella cella B3.
- Font.IsBold = true: imposta il testo in grassetto per farlo risaltare.
- Intervallo di input: consente di inserire diversi ID dipendente nelle celle da A2 ad A7. Questi appariranno nel menu a discesa.
## Passaggio 5: aggiungere la casella combinata al foglio di lavoro
Il passaggio successivo consiste nell'aggiungere il controllo casella combinata al foglio di lavoro. Questa casella combinata consentirà agli utenti di selezionare uno degli ID dipendente inseriti in precedenza.

```csharp
// Aggiungi una nuova casella combinata.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Aggiunge una nuova casella combinata al foglio di lavoro. I numeri (2, 0, 2, 0, 22, 100) rappresentano la posizione e le dimensioni della casella combinata.
## Passaggio 6: collegare la casella combinata a una cella e impostare l'intervallo di input
Per rendere funzionale la casella combinata, dobbiamo collegarla a una cella specifica e definire l'intervallo di celle da cui estrarrà le sue opzioni.

```csharp
// Imposta la cella collegata.
comboBox.LinkedCell = "A1";
// Imposta l'intervallo di input.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Collega la selezione della casella combinata alla cella A1. Il valore selezionato dalla casella combinata apparirà in questa cella.
- InputRange: definisce l'intervallo di celle (A2:A7) contenente i valori che popoleranno le opzioni della casella combinata.
## Passaggio 7: personalizzare l'aspetto della casella combinata
È possibile personalizzare ulteriormente la casella combinata specificando il numero di linee del menu a discesa e abilitando l'ombreggiatura 3D per una migliore estetica.

```csharp
// Imposta il numero di righe di elenco visualizzate nella parte elenco della casella combinata.
comboBox.DropDownLines = 5;
// Imposta la casella combinata con ombreggiatura 3D.
comboBox.Shadow = true;
```

- DropDownLines: controlla quante opzioni saranno visibili contemporaneamente nel menu a discesa della casella combinata.
- Ombra: aggiunge un effetto di ombreggiatura 3D alla casella combinata.
## Passaggio 8: Adatta automaticamente le colonne e salva la cartella di lavoro
Infine, adattiamo automaticamente le colonne per ottenere un layout pulito e salviamo la cartella di lavoro.

```csharp
// Adatta automaticamente colonne
sheet.AutoFitColumns();
// Salva il file.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: adatta automaticamente la larghezza delle colonne al contenuto.
- Salva: salva la cartella di lavoro come file Excel nella directory specificata.

## Conclusione
Aggiungere una casella combinata ai fogli di lavoro Excel utilizzando Aspose.Cells per .NET è un processo semplice che migliora notevolmente la flessibilità nell'input dei dati. Creando controlli di modulo a livello di codice, è possibile creare fogli di calcolo interattivi con facilità. Questo tutorial ha mostrato come aggiungere una casella combinata, collegarla a una cella e configurarne l'intervallo di input, il tutto utilizzando Aspose.Cells.
Aspose.Cells offre una vasta gamma di funzionalità per la manipolazione di file Excel, rendendolo la scelta ideale per gli sviluppatori che desiderano automatizzare le attività dei fogli di calcolo. Provalo con un [prova gratuita](https://releases.aspose.com/).
## Domande frequenti
### Posso usare Aspose.Cells senza Excel installato?
Sì, Aspose.Cells funziona indipendentemente da Excel e non richiede l'installazione di Excel.
### Come faccio ad applicare una licenza in Aspose.Cells?
È possibile richiedere una licenza ottenendola da [Qui](https://purchase.aspose.com/buy) e chiamando `License.SetLicense()` nel tuo codice.
### Quali formati supporta Aspose.Cells per il salvataggio dei file?
Aspose.Cells supporta il salvataggio di file in numerosi formati, come XLSX, XLS, CSV, PDF e altri.
### C'è un limite al numero di caselle combinate che posso aggiungere?
No, non esiste un limite preciso: puoi aggiungere tutte le caselle combinate di cui ha bisogno il tuo progetto.
### Come posso ottenere supporto per Aspose.Cells?
Puoi ottenere supporto da [Forum di Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}