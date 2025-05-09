---
"date": "2025-04-05"
"description": "Scopri come impostare un font predefinito quando converti file Excel in HTML utilizzando Aspose.Cells per .NET, assicurando una tipografia coerente e una presentazione professionale."
"title": "Imposta il font predefinito nella conversione da Excel a HTML con Aspose.Cells per .NET | Guida alle operazioni della cartella di lavoro"
"url": "/it/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Padroneggiare le impostazioni predefinite dei font in Excel per la conversione in HTML con Aspose.Cells per .NET

## Introduzione

Convertire una cartella di lavoro Excel in formato HTML mantenendo una tipografia coerente può essere impegnativo. Questo tutorial ti guiderà nell'impostazione di un font predefinito utilizzando Aspose.Cells per .NET, garantendo che i tuoi documenti convertiti appaiano curati e professionali. Padroneggiando questa funzionalità, supererai le difficoltà legate all'utilizzo di font sconosciuti o non disponibili durante il processo di conversione.

**Cosa imparerai:**
- Come impostare un font predefinito quando si convertono file Excel in HTML.
- Guida dettagliata all'utilizzo di Aspose.Cells per .NET.
- Tecniche per gestire in modo elegante i font sconosciuti durante il rendering.

Immergiamoci nella configurazione del tuo ambiente e iniziamo a esplorare questa funzionalità!

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

- **Ambiente .NET**: È installata una versione compatibile di .NET (ad esempio, .NET Core o .NET Framework).
- **Aspose.Cells per la libreria .NET**: Installa Aspose.Cells tramite NuGet.
- **Conoscenza di base di C#**Sarà utile avere familiarità con i concetti di programmazione C#.

## Impostazione di Aspose.Cells per .NET

Per iniziare, configura Aspose.Cells nel tuo ambiente di sviluppo seguendo questi passaggi:

**Installazione tramite CLI:**
```bash
dotnet add package Aspose.Cells
```

**Installazione tramite Gestione pacchetti:**
```shell
PM> NuGet\Install-Package Aspose.Cells
```

### Acquisizione della licenza
- **Prova gratuita**: Inizia con una prova gratuita per esplorare le funzionalità.
- **Licenza temporanea**: Ottenere una licenza temporanea per scopi di valutazione.
- **Acquistare**: Valutare l'acquisto di una licenza per l'uso in produzione.

Una volta installato, inizializza e configura il tuo progetto come segue:
```csharp
using Aspose.Cells;
```

## Guida all'implementazione

### Impostazione del font predefinito durante il rendering

Questa funzionalità garantisce che una cartella di lavoro Excel venga visualizzata con un font predefinito specifico durante la conversione in HTML. È particolarmente utile per gestire i casi in cui determinati font potrebbero non essere disponibili sul sistema di destinazione.

#### Passaggio 1: creare e accedere alla cartella di lavoro

Crea una nuova istanza di `Workbook` e accedi al suo primo foglio di lavoro:
```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

// Crea un oggetto cartella di lavoro e accedi al primo foglio di lavoro.
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];
```

#### Passaggio 2: modifica lo stile della cella

Accedi a una cella specifica, aggiungi del testo e imposta il font su uno sconosciuto per la dimostrazione:
```csharp
// Accedi alla cella B4 e aggiungi del testo al suo interno.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// Imposta il carattere della cella B4 su un carattere sconosciuto.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

#### Passaggio 3: definire le opzioni di salvataggio HTML

Imposta il font predefinito nel tuo output HTML. Qui, mostriamo tre font diversi:

**Corriere Nuovo:**
```csharp
// Salvare la cartella di lavoro in formato HTML con il font predefinito impostato su Courier New.
HtmlSaveOptions optsCourierNew = new HtmlSaveOptions();
optsCourierNew.DefaultFontName = "Courier New";
wb.Save(outputDir + "/out_courier_new_out.htm", optsCourierNew);
```

**Arial:**
```csharp
// Salva la cartella di lavoro in formato HTML con il font predefinito impostato su Arial.
HtmlSaveOptions optsArial = new HtmlSaveOptions();
optsArial.DefaultFontName = "Arial";
wb.Save(outputDir + "/out_arial_out.htm", optsArial);
```

**Times New Roman:**
```csharp
// Salvare la cartella di lavoro in formato HTML con il carattere predefinito impostato su Times New Roman.
HtmlSaveOptions optsTimesNewRoman = new HtmlSaveOptions();
optsTimesNewRoman.DefaultFontName = "Times New Roman";
wb.Save(outputDir + "/times_new_roman_out.htm", optsTimesNewRoman);
```

### Creazione di cartelle di lavoro e stile delle celle

Questa sezione riguarda la creazione di una cartella di lavoro, l'accesso a fogli di lavoro, celle e l'applicazione di stili:

#### Passaggio 1: inizializzare la cartella di lavoro
Crea un nuovo `Workbook` esempio:
```csharp
// Crea un oggetto cartella di lavoro.
Workbook wb = new Workbook();
```

#### Passaggio 2: accedi al foglio di lavoro e alla cella
Accedi al primo foglio di lavoro e alla cella B4 per aggiungere testo e formattarlo:
```csharp
// Accedi al primo foglio di lavoro nella cartella di lavoro.
Worksheet ws = wb.Worksheets[0];

// Accedi alla cella B4 e aggiungi del testo al suo interno.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// Imposta il carattere della cella B4 su un carattere sconosciuto.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

## Applicazioni pratiche
- **Branding coerente**: Assicurarsi che i font del marchio vengano applicati in modo coerente nei documenti HTML esportati.
- **Portabilità dei documenti**: Gestire scenari in cui gli ambienti di destinazione non dispongono di font specifici.
- **Reporting automatico**: Utilizza questa funzionalità per generare report automatizzati con una tipografia coerente.

## Considerazioni sulle prestazioni
Per prestazioni ottimali:
- Gestire l'utilizzo della memoria eliminando gli oggetti in modo appropriato.
- Ottimizza le impostazioni di rendering in base alle esigenze della tua applicazione.
- Aggiornare regolarmente Aspose.Cells all'ultima versione per funzionalità migliorate e correzioni di bug.

## Conclusione

Hai imparato come impostare un font predefinito durante la conversione di file Excel in HTML utilizzando Aspose.Cells per .NET. Questa funzionalità garantisce una tipografia coerente, anche quando alcuni font non sono disponibili nel sistema di destinazione. Per migliorare ulteriormente le tue competenze, esplora le funzionalità aggiuntive di Aspose.Cells e sperimenta diverse opzioni di rendering.

**Prossimi passi**: Prova a implementare questa soluzione nei tuoi progetti e personalizzala in base alle tue esigenze specifiche.

## Sezione FAQ
1. **Che cos'è Aspose.Cells per .NET?**
   - Una libreria che consente la manipolazione e la conversione di file Excel all'interno di applicazioni .NET.
2. **Come faccio a installare Aspose.Cells?**
   - Utilizzare NuGet Package Manager o .NET CLI come mostrato sopra.
3. **Posso utilizzare questa funzionalità con versioni precedenti di .NET?**
   - Assicurare la compatibilità controllando i requisiti di sistema della libreria.
4. **Cosa succede se il mio font predefinito non è supportato su tutti i sistemi?**
   - Verrà utilizzato il font predefinito specificato, garantendo la coerenza su tutte le piattaforme.
5. **Dove posso trovare ulteriori risorse e supporto per Aspose.Cells?**
   - Fare riferimento a [Documentazione di Aspose](https://reference.aspose.com/cells/net/) o il [Forum di supporto](https://forum.aspose.com/c/cells/9).

## Risorse
- **Documentazione**: [Riferimento Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **Scaricamento**: [Pagina delle versioni](https://releases.aspose.com/cells/net/)
- **Acquistare**: [Acquista Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova gratuita**: [Scarica la versione di prova](https://releases.aspose.com/cells/net/)
- **Licenza temporanea**: [Richiesta di licenza](https://purchase.aspose.com/temporary-license/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}