---
"date": "2025-04-05"
"description": "Scopri come aggiungere e personalizzare forme ovali in Excel utilizzando Aspose.Cells per .NET. Migliora le tue presentazioni di dati senza sforzo."
"title": "Aggiungere forme ovali a Excel con Aspose.Cells per .NET | Guida passo passo"
"url": "/it/net/images-shapes/add-oval-shapes-excel-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Come aggiungere forme ovali ai fogli di lavoro di Excel utilizzando Aspose.Cells per .NET

## Introduzione

Nel mondo della presentazione dei dati, rendere i fogli Excel visivamente accattivanti può migliorare significativamente la comprensione e il coinvolgimento. Aggiungere forme personalizzate come gli ovali non è sempre semplice con le funzionalità di base di Excel. **Aspose.Cells per .NET** Offre un potente strumento per inserire e personalizzare a livello di codice forme ovali nei fogli di lavoro. Questa guida passo passo ti mostrerà come sfruttare Aspose.Cells per aggiungere forme ovali ai tuoi file Excel in modo efficiente.

### Cosa imparerai:
- Come impostare Aspose.Cells nel tuo progetto .NET
- Il processo di aggiunta e configurazione di forme ovali in un foglio di lavoro Excel
- Opzioni di personalizzazione chiave per le forme ovali
- Le migliori pratiche per integrare queste funzionalità in progetti più ampi

Prima di iniziare a scrivere il codice, analizziamo i prerequisiti!

## Prerequisiti

Prima di iniziare ad aggiungere ovali ai tuoi fogli di lavoro, assicurati di avere quanto segue:

- **Aspose.Cells per .NET**: Una potente libreria che consente un'ampia manipolazione dei file Excel.
  - Per l'installazione, utilizzare:
    - **Interfaccia a riga di comando .NET**:
      ```bash
dotnet aggiunge il pacchetto Aspose.Cells
```
    - **Package Manager**:
      ```powershell
PM> NuGet\Install-Package Aspose.Cells
```
- **Ambiente di sviluppo**: assicurati di aver configurato un ambiente di sviluppo .NET adatto, come Visual Studio o VS Code con .NET SDK.
- **Conoscenza di base dei framework C# e .NET**: Sarà utile avere familiarità con i concetti di programmazione orientata agli oggetti in C#.

## Impostazione di Aspose.Cells per .NET

Configurare Aspose.Cells è semplice. Segui questi passaggi per iniziare:

1. **Installa il pacchetto**:
   Utilizzare i comandi forniti sopra per installare il pacchetto Aspose.Cells nel progetto.
   
2. **Acquisizione della licenza**:
   - Puoi iniziare con un [prova gratuita](https://releases.aspose.com/cells/net/) per testare le funzionalità.
   - Per funzionalità estese, prendi in considerazione l'ottenimento di una licenza temporanea o l'acquisto di una tramite [Pagina di acquisto di Aspose](https://purchase.aspose.com/buy).

3. **Inizializzazione**:
   Una volta installato e ottenuto il diritto di licenza, puoi inizializzare Aspose.Cells nella tua applicazione:
   
   ```csharp
utilizzando Aspose.Cells;
```

With the environment set up, let's move on to implementing oval shapes.

## Implementation Guide

### Adding an Oval Shape

This feature guides you through adding a basic oval shape to an Excel worksheet.

#### Overview
Adding ovals can enhance the visual appeal of your data presentation. In this section, we'll add and configure an oval in the first worksheet of our Excel file using Aspose.Cells.

#### Steps:

##### Step 1: Define Directory for Output

First, define where you want to save your output files:

```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";
string dataDir = Path.Combine(outputDir, "OvalShapeExample");

if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### Passaggio 2: creare un'istanza di una cartella di lavoro

Crea un'istanza di `Workbook` classe per iniziare a lavorare con i file Excel:

```csharp
Workbook excelbook = new Workbook();
```

##### Passaggio 3: aggiungere la forma ovale

Utilizzare il `AddOval` metodo per posizionare una forma ovale nel foglio di lavoro:

```csharp
// Aggiungi un ovale alle coordinate e alle dimensioni specificate
Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```

##### Passaggio 4: configurare il posizionamento

Imposta il tipo di posizionamento su `FreeFloating` per un maggiore controllo sul posizionamento:

```csharp
oval1.Placement = PlacementType.FreeFloating;
```

##### Passaggio 5: impostare le proprietà della linea

Personalizza l'aspetto del contorno dell'ovale impostando lo spessore della linea e lo stile del trattino:

```csharp
// Imposta lo spessore della linea e lo stile del trattino
oval1.Line.Weight = 1;
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### Passaggio 6: Salva la cartella di lavoro

Infine, salva la cartella di lavoro in un file nella directory specificata:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExample.xls"));
```

#### Suggerimenti per la risoluzione dei problemi:
- Assicurarsi che tutti i percorsi delle directory siano impostati correttamente per evitare errori di file non trovato.
- Se si utilizzano funzionalità che vanno oltre i limiti della versione di prova, verificare che Aspose.Cells disponga della licenza corretta.

### Aggiungere un'altra forma ovale (cerchio)

Aggiungiamo ora un'altra forma ovale, configurata come un cerchio, con proprietà diverse.

#### Panoramica
Aggiungere più forme può aiutare a creare visualizzazioni più complesse. Qui, mostreremo come aggiungere un ovale circolare al tuo foglio di lavoro.

#### Passaggi:

##### Passaggio 1: assicurarsi che la directory esista

Questo passaggio è simile alla sezione precedente; assicurati che la directory sia configurata correttamente.

```csharp
if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### Passaggio 2: creare un'istanza della cartella di lavoro

Crea un nuovo `Workbook` esempio per questa aggiunta di forma:

```csharp
Workbook excelbook = new Workbook();
```

##### Passaggio 3: aggiungere la forma del cerchio

Aggiungi un altro ovale con le dimensioni necessarie per farlo apparire come un cerchio:

```csharp
// Aggiungi una forma circolare con coordinate e dimensioni diverse
Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```

##### Passaggio 4: configurare il posizionamento

Imposta il tipo di posizionamento per la nuova forma:

```csharp
oval2.Placement = PlacementType.FreeFloating;
```

##### Passaggio 5: impostare le proprietà della linea

Definisci lo spessore della linea e lo stile del tratteggio per la personalizzazione:

```csharp
// Personalizza le proprietà della linea
oval2.Line.Weight = 1;
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### Passaggio 6: salva la cartella di lavoro con la nuova forma

Salva nuovamente la cartella di lavoro, questa volta includendo entrambe le forme:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExampleWithCircle.xls"));
```

## Applicazioni pratiche

Aspose.Cells consente un'ampia gamma di applicazioni pratiche per l'aggiunta di forme ovali ai fogli di lavoro di Excel:

1. **Visualizzazione dei dati**: Migliora i grafici di dati con annotazioni personalizzate.
2. **Progettazione del cruscotto**: Utilizza gli ovali per evidenziare metriche o sezioni chiave nei dashboard finanziari.
3. **Creazione di modelli**: Crea modelli riutilizzabili per report che richiedono elementi visivi coerenti.

Questi casi d'uso dimostrano la versatilità di Aspose.Cells in ambienti professionali e aziendali.

## Considerazioni sulle prestazioni

Quando si lavora con grandi set di dati o fogli di lavoro complessi, l'ottimizzazione delle prestazioni è fondamentale:

- **Gestione efficiente della memoria**: Assicurare il corretto smaltimento degli oggetti per liberare memoria.
- **Operazioni batch**: Ove possibile, eseguire le operazioni in batch per ridurre al minimo i tempi di elaborazione.
- **Utilizzo delle risorse**Monitora l'utilizzo delle risorse e ottimizza i percorsi del codice che sono computazionalmente costosi.

Seguendo queste buone pratiche è possibile mantenere prestazioni ottimali quando si utilizza Aspose.Cells per manipolazioni estese di Excel.

## Conclusione

In questo tutorial abbiamo illustrato come aggiungere e configurare forme ovali nei fogli di lavoro Excel utilizzando Aspose.Cells per .NET. Seguendo i passaggi descritti, è possibile migliorare le presentazioni dei dati con elementi visivi personalizzati senza sforzo. Per ulteriori approfondimenti, si consiglia di approfondire le funzionalità più avanzate di Aspose.Cells o di integrare queste tecniche in progetti più ampi.

## Sezione FAQ

1. **Posso usare Aspose.Cells senza licenza?**
   - Sì, ma con alcune limitazioni. È disponibile una versione di prova a scopo di test.
2. **Come faccio a cambiare il colore di una forma ovale?**
   - Utilizzare il `FillFormat` proprietà per personalizzare il colore e lo stile di riempimento.
3. **È possibile aggiungere del testo all'interno di una forma ovale?**
   - Sì, puoi inserire forme di testo all'interno degli ovali utilizzando l'API di Aspose.Cells.
4. **Posso automatizzare questo processo per più file?**
   - Certamente, esegui un ciclo nel tuo set di file e applica questi metodi a livello di programmazione.
5. **Quali sono i requisiti di sistema per eseguire Aspose.Cells?**
   - Supporta .NET Framework 2.0 e versioni successive, inclusi .NET Core e .NET 5/6.

## Risorse
- [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Scarica Aspose.Cells per .NET](https://releases.aspose.com/cells/net/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}