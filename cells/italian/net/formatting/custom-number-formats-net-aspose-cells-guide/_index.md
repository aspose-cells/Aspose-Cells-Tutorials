---
"date": "2025-04-05"
"description": "Scopri come implementare formati numerici personalizzati in .NET utilizzando Aspose.Cells per una presentazione precisa dei dati Excel. Questa guida illustra la configurazione e la formattazione di date, percentuali e valute."
"title": "Come utilizzare formati numerici personalizzati in .NET con Aspose.Cells&#58; una guida passo passo"
"url": "/it/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Come utilizzare formati numerici personalizzati in .NET con Aspose.Cells: una guida passo passo

## Introduzione

Migliora la manipolazione dei file Excel utilizzando C# e .NET con un controllo preciso sui formati numerici. Questo tutorial ti guida nell'impostazione di formati numerici personalizzati nelle applicazioni .NET utilizzando Aspose.Cells per .NET, una potente libreria progettata per la manipolazione di Excel.

Sfruttando Aspose.Cells, puoi applicare diversi stili ai dati senza sforzo, garantendo chiarezza e precisione nei tuoi report. Che si tratti di formattare date, percentuali o valori di valuta, padroneggiare questa funzionalità semplifica il flusso di lavoro.

**Cosa imparerai:**
- Impostazione di Aspose.Cells per .NET
- Implementazione di formati numerici personalizzati con C#
- Applicazione di stili a livello di programmazione alle celle di Excel
- Applicazioni pratiche della formattazione personalizzata dei numeri

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:
1. **Ambiente di sviluppo**: Una configurazione funzionante di .NET con Visual Studio o qualsiasi IDE compatibile.
2. **Aspose.Cells per la libreria .NET**: Per questa guida è richiesta la versione 22.x o successiva.
3. **Conoscenza di base di C#**: La familiarità con la sintassi C# e con i concetti di programmazione ti aiuterà a seguire il corso senza problemi.

## Impostazione di Aspose.Cells per .NET

Per utilizzare Aspose.Cells nel tuo progetto, installa la libreria tramite .NET CLI o Package Manager Console in Visual Studio.

**Installazione .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Installazione del gestore pacchetti:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Acquisizione della licenza

Aspose.Cells offre una prova gratuita per la valutazione e opzioni per un utilizzo esteso tramite una licenza temporanea o acquistata.
- **Prova gratuita**: Scarica da [Qui](https://releases.aspose.com/cells/net/).
- **Licenza temporanea**: Applica a [Pagina della licenza temporanea Aspose](https://purchase.aspose.com/temporary-license/) per rimuovere le limitazioni di valutazione.
- **Acquistare**: Per l'accesso completo, visita il [Pagina di acquisto](https://purchase.aspose.com/buy).

Per inizializzare Aspose.Cells nel tuo progetto:
```csharp
// Importa lo spazio dei nomi
using Aspose.Cells;

// Inizializza un nuovo oggetto Workbook
Workbook workbook = new Workbook();
```

## Guida all'implementazione

Vedremo le funzionalità principali per personalizzare i formati numerici utilizzando Aspose.Cells.

### Aggiunta di un formato data personalizzato
**Panoramica**: Impara a formattare le date nelle celle di Excel con uno stile personalizzato.
1. **Creare o accedere a un foglio di lavoro**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **Imposta la data corrente del sistema con formato personalizzato**
   Aggiungi la data corrente alla cella "A1" e applica un formato di visualizzazione personalizzato.
   ```csharp
   // Inserisci la data corrente del sistema in A1
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // Recupera l'oggetto stile per la personalizzazione
   Style style = worksheet.Cells["A1"].GetStyle();

   // Imposta il formato numerico personalizzato su "g-mmm-aa"
   style.Custom = "d-mmm-yy";

   // Applica nuovamente lo stile personalizzato alla cella A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### Formattazione dei valori numerici come percentuale
**Panoramica**: Visualizza i valori numerici in formato percentuale.
1. **Inserisci e formatta il valore**
   ```csharp
   // Aggiungi un valore numerico alla cella A2
   worksheet.Cells["A2"].PutValue(20);

   // Ottieni lo stile per la formattazione
   Style style = worksheet.Cells["A2"].GetStyle();

   // Applica il formato numerico personalizzato come percentuale
   style.Custom = "0.0%";

   // Ripristina lo stile formattato sulla cella A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### Applicazione del formato di valuta
**Panoramica**: Mostra i numeri in formato valuta, con formattazione specifica per i valori negativi.
1. **Inserisci e assegna uno stile al valore della valuta**
   ```csharp
   // Aggiungi un valore alla cella A3
   worksheet.Cells["A3"].PutValue(2546);

   // Accedi all'oggetto stile
   Style style = worksheet.Cells["A3"].GetStyle();

   // Imposta formato valuta personalizzato
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // Applica alla cella A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## Applicazioni pratiche

La formattazione personalizzata dei numeri è preziosa in scenari come:
1. **Rapporti finanziari**: Formattazione dei valori di valuta per maggiore chiarezza.
2. **Dashboard di vendita**: Visualizzazione delle cifre di vendita come percentuali per evidenziare le metriche delle prestazioni.
3. **Pianificazione di eventi**: Utilizzo di formati data per organizzare e presentare in modo fluido i programmi degli eventi.

## Considerazioni sulle prestazioni
Quando si lavora con set di dati di grandi dimensioni, ottimizzare le prestazioni di Aspose.Cells:
- Ridurre al minimo l'utilizzo della memoria eliminando prontamente gli oggetti utilizzando `GC.Collect()` dopo aver salvato i file.
- Utilizzare flussi per leggere/scrivere file Excel anziché caricare interi documenti nella memoria.
- Implementare le best practice nella gestione della memoria .NET per mantenere l'efficienza.

## Conclusione
Seguendo questa guida, hai imparato a implementare formati numerici personalizzati nelle tue applicazioni .NET utilizzando Aspose.Cells. Questa funzionalità migliora la presentazione dei dati e garantisce accuratezza e un impatto visivo gradevole in report e fogli di calcolo.

**Prossimi passi**sperimenta altre opzioni di formattazione disponibili in Aspose.Cells, come la formattazione condizionale o i miglioramenti dei grafici.

## Sezione FAQ
1. **Come posso ottenere una licenza temporanea per Aspose.Cells?**
   - Presentare domanda presso [Pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/).
2. **Quali formati sono supportati per gli stili numerici personalizzati in Aspose.Cells?**
   - Data, percentuale, valuta e altro ancora, utilizzando stringhe di formato Excel standard.
3. **Posso usare Aspose.Cells con altri linguaggi .NET come VB.NET?**
   - Sì, la libreria è compatibile con tutti i linguaggi supportati da .NET.
4. **Cosa devo fare se i numeri formattati non vengono visualizzati correttamente?**
   - Controlla attentamente la stringa del formato numerico personalizzato per individuare eventuali errori di battitura o di sintassi.
5. **Dove posso trovare altri esempi di utilizzo di Aspose.Cells?**
   - Esplora la documentazione dettagliata e i codici di esempio su [Documentazione di Aspose](https://reference.aspose.com/cells/net/).

## Risorse
- [Documentazione di Aspose.Cells per .NET](https://reference.aspose.com/cells/net/)
- [Scarica l'ultima versione](https://releases.aspose.com/cells/net/)
- [Acquista una licenza](https://purchase.aspose.com/buy)
- [Download di prova gratuito](https://releases.aspose.com/cells/net/)
- [Richiesta di licenza temporanea](https://purchase.aspose.com/temporary-license/)
- [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}