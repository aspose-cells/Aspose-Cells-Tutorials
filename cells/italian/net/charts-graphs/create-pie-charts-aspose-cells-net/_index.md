---
"date": "2025-04-05"
"description": "Scopri come creare grafici a torta dinamici con linee guida utilizzando Aspose.Cells per .NET. Segui questa guida per migliorare le tue competenze di visualizzazione dei dati."
"title": "Creazione di grafici a torta con linee guida in Aspose.Cells .NET&#58; una guida completa"
"url": "/it/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Creazione di grafici a torta con linee guida utilizzando Aspose.Cells .NET

## Introduzione
Migliora la visualizzazione dei tuoi dati creando grafici a torta più informativi con Aspose.Cells per .NET. Questa guida passo passo ti mostra come aggiungere linee guida ai segmenti di un grafico a torta, semplificando l'identificazione a colpo d'occhio delle categorie di dati corrispondenti. Seguendo questo tutorial, le tue visualizzazioni saranno visivamente accattivanti e altamente funzionali.

**Cosa imparerai:**
- Impostazione di Aspose.Cells per .NET nel tuo ambiente
- Creazione di grafici a torta personalizzati con linee guida utilizzando C#
- Salvataggio del grafico come immagine o all'interno di una cartella di lavoro di Excel

Assicuratevi di avere tutto pronto per seguire in modo efficace.

## Prerequisiti
Prima di iniziare, assicurati di soddisfare questi prerequisiti:

- **Librerie e versioni**: Installa Aspose.Cells per .NET. Assicurati che il tuo progetto sia configurato con la versione più recente.
- **Configurazione dell'ambiente**: Questa guida presuppone un ambiente .NET compatibile con Aspose.Cells.
- **Prerequisiti di conoscenza**È preferibile una conoscenza di base della programmazione C# e delle operazioni di Excel.

## Impostazione di Aspose.Cells per .NET
Per iniziare, installa Aspose.Cells nel tuo progetto tramite:

**Interfaccia a riga di comando .NET**
```bash
dotnet add package Aspose.Cells
```

**Gestore dei pacchetti**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Ottieni una licenza per la piena funzionalità selezionando tra le seguenti opzioni:
- **Prova gratuita**: Inizia la tua prova gratuita su [Pagina di download di Aspose](https://releases.aspose.com/cells/net/).
- **Licenza temporanea**: Ottenere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).
- **Acquistare**: Per le funzionalità complete, acquista una licenza [Qui](https://purchase.aspose.com/buy).

Inizializza Aspose.Cells nel tuo progetto creando un'istanza di `Workbook` classe.

## Guida all'implementazione

### Creazione della cartella di lavoro e del foglio di lavoro
1. **Inizializzare la cartella di lavoro**
   Crea una nuova cartella di lavoro in formato XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Accesso al primo foglio di lavoro**
   Utilizzare il primo foglio di lavoro per inserire i dati:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Aggiunta di dati per grafico a torta**
   Compila il tuo foglio di lavoro con categorie e valori:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Aggiungi i nomi delle categorie rimanenti...
   worksheet.Cells["B1"].PutValue(10.4);
   // Aggiungi i valori corrispondenti...
   ```

### Aggiungere un grafico a torta al foglio di lavoro
1. **Crea il grafico a torta**
   Genera un grafico a torta e aggiungilo alla raccolta di grafici del tuo foglio di lavoro:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Configurare i dati di serie e categorie**
   Collega i dati per le serie e le categorie:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Personalizza le etichette dei dati**
   Disattiva la visualizzazione della legenda, imposta le etichette dei dati per mostrare i nomi delle categorie e le percentuali:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementazione delle linee guida
1. **Attiva le linee guida**
   Abilita le linee guida per collegamenti visivi più chiari:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Regola la posizione delle etichette dati**
   Garantire la visibilità regolando le posizioni delle etichette:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Salvataggio del grafico e della cartella di lavoro
1. **Salva come immagine**
   Trasforma il grafico in un file immagine:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Salva cartella di lavoro**
   Salva la cartella di lavoro per visualizzare il grafico in Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Applicazioni pratiche
- **Rapporti finanziari**: Rappresentare chiaramente le allocazioni di bilancio.
- **Analisi di marketing**: Visualizzare efficacemente i dati sulle quote di mercato in presentazioni o report.
- **Analisi delle vendite**Visualizza con facilità la distribuzione delle vendite tra diverse regioni/prodotti.

Le possibilità di integrazione includono l'esportazione di queste visualizzazioni in applicazioni web o la loro incorporazione in strumenti di reporting automatizzati.

## Considerazioni sulle prestazioni
Quando si utilizza Aspose.Cells, tenere presente quanto segue per prestazioni ottimali:
- Ridurre al minimo i grandi set di dati caricati in memoria contemporaneamente.
- Utilizzare cicli efficienti ed evitare calcoli non necessari al loro interno.
- Pulire regolarmente le risorse, come gli oggetti della cartella di lavoro, per evitare perdite di memoria.

## Conclusione
Hai imparato a creare grafici a torta con linee guida utilizzando Aspose.Cells per .NET. Questa funzionalità migliora la chiarezza delle visualizzazioni dei dati, rendendole più accessibili e di impatto. 

**Prossimi passi:**
Esplora ulteriori personalizzazioni nell'aspetto dei grafici o sperimenta altri tipi di grafici disponibili in Aspose.Cells.

## Sezione FAQ
1. **Cos'è una linea guida in un grafico a torta?**
   Le linee guida collegano le etichette dei dati ai rispettivi segmenti, migliorandone la leggibilità.

2. **Posso usare Aspose.Cells gratuitamente?**
   Sì, puoi iniziare con una prova gratuita, ma per usufruire di tutte le funzionalità è necessaria una licenza.

3. **È possibile esportare i grafici come immagini?**
   Assolutamente! Usa `ImageOrPrintOptions` per salvare il grafico in formati immagine come PNG o JPEG.

4. **Come posso regolare manualmente le posizioni delle etichette dati?**
   Modificare le coordinate X e Y delle etichette dati all'interno del ciclo dei punti della serie.

5. **Aspose.Cells può essere integrato con altri sistemi?**
   Sì, può essere utilizzato insieme a database, servizi Web e altro ancora per soluzioni di reporting automatizzate.

## Risorse
- [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Scarica Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Acquista licenza](https://purchase.aspose.com/buy)
- [Prova gratuita](https://releases.aspose.com/cells/net/)
- [Licenza temporanea](https://purchase.aspose.com/temporary-license/)
- [Forum di supporto](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}