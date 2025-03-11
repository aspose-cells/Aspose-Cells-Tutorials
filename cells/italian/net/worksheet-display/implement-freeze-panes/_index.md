---
title: Implementare i riquadri bloccati nel foglio di lavoro
linktitle: Implementare i riquadri bloccati nel foglio di lavoro
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come implementare i riquadri bloccati in Excel usando Aspose.Cells per .NET con questa guida dettagliata, passo dopo passo. Migliora l'usabilità del tuo foglio di lavoro in modo efficiente.
weight: 15
url: /it/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementare i riquadri bloccati nel foglio di lavoro

## Introduzione
Immagina di avere un foglio di lavoro Excel con un enorme set di dati e ogni volta che scorri verso il basso o in orizzontale, perdi traccia di quelle importanti intestazioni. Non sarebbe comodo se quelle intestazioni potessero semplicemente rimanere al loro posto mentre scorri? Ecco dove entrano in gioco i riquadri bloccati, rendendo la navigazione fluida ed efficiente. Aspose.Cells per .NET semplifica questo processo, dandoti la possibilità di implementare i riquadri bloccati senza problemi. Questa guida ti guiderà attraverso il processo, suddividendolo passo dopo passo in modo che tu possa impostare quelle intestazioni bloccate in pochissimo tempo.
## Prerequisiti
Prima di immergerti, assicurati di avere alcune cose pronte:
-  Aspose.Cells per la libreria .NET: dovrai scaricare questa libreria da[Pagina delle release di Aspose](https://releases.aspose.com/cells/net/).
- .NET Framework installato: assicurati di aver installato .NET nel tuo ambiente di sviluppo.
- Conoscenza di base di C#: la familiarità con C# sarà utile per seguire il corso.
- File Excel: tieni pronto un file Excel (ad esempio, "book1.xls") a cui applicherai i blocchi riquadro.
Puoi esplorare maggiori dettagli su Aspose.Cells sul loro[pagina di documentazione](https://reference.aspose.com/cells/net/).

## Importa pacchetti
Iniziamo importando i pacchetti necessari. Apri il tuo progetto C# e assicurati di importare questi:
```csharp
using System.IO;
using Aspose.Cells;
```
Una volta impostati i pacchetti, passiamo alla guida passo dopo passo.
Passeremo in rassegna ogni fase dell'impostazione dei riquadri di congelamento usando Aspose.Cells per .NET. Segui attentamente ogni passaggio e avrai i riquadri di congelamento applicati al tuo foglio di lavoro senza sforzo.
## Passaggio 1: definire il percorso per la directory dei documenti
 Prima di poter aprire il file Excel, dovrai specificare il percorso del documento. Imposta un`dataDir` variabile che contiene il percorso della directory per i tuoi file.
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"` con il percorso effettivo in cui sono archiviati i tuoi file Excel. Questo aiuterà il programma a localizzare il tuo file.
## Passaggio 2: aprire il file Excel utilizzando FileStream
Poi, dobbiamo caricare il file Excel in modo che Aspose.Cells possa fare la sua magia. Per farlo, creeremo un flusso di file e apriremo il file Excel usando quel flusso.
```csharp
// Creazione di un flusso di file contenente il file Excel da aprire
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Utilizzando un flusso di file, si apre il file affinché Aspose.Cells possa accedervi senza alterare il file originale finché non si salvano esplicitamente le modifiche.
## Passaggio 3: creare un'istanza dell'oggetto Workbook
 Con il flusso di file in atto, è il momento di creare un`Workbook` oggetto. Questo oggetto è essenziale perché rappresenta l'intera cartella di lavoro di Excel, consentendoti di lavorare con singoli fogli, celle e impostazioni all'interno del file.
```csharp
// Creazione di un'istanza di un oggetto Workbook
// Apertura del file Excel tramite il flusso di file
Workbook workbook = new Workbook(fstream);
```
 Pensa a`Workbook` come il raccoglitore che tiene insieme tutti i tuoi fogli. Una volta aperto il raccoglitore, puoi accedere a qualsiasi pagina (foglio di lavoro) al suo interno.
## Passaggio 4: accedi al primo foglio di lavoro
Ora che la tua cartella di lavoro è caricata, puoi scegliere a quale foglio di lavoro applicare i riquadri bloccati. In questo esempio, lavoreremo con il primo foglio. Aspose.Cells semplifica la selezione di un foglio tramite indicizzazione.
```csharp
// Accesso al primo foglio di lavoro nel file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Se hai bisogno di lavorare su un foglio diverso, regola semplicemente l'indice in`workbook.Worksheets[0]`.
## Passaggio 5: applicare le impostazioni di Blocco riquadri
 Ecco dove avviene la magia! Per impostare i riquadri di congelamento, usa`FreezePanes`metodo, specificando la riga e la colonna in cui si desidera che inizi il blocco, nonché il numero di righe e colonne da bloccare.
```csharp
// Applicazione delle impostazioni di congelamento dei riquadri
worksheet.FreezePanes(3, 2, 3, 2);
```
Analizziamo i parametri:
- Prima riga (3): iniziare il congelamento dalla riga 3.
- Prima colonna (2): inizia il congelamento dalla colonna 2.
- Conteggio delle righe (3): Congela 3 righe.
- Conteggio colonne (2): blocca 2 colonne.
Adatta questi valori in base alle tue esigenze specifiche. Il punto di congelamento sarà l'intersezione della riga e della colonna specificate.
## Passaggio 6: salvare il file Excel modificato
 Dopo aver applicato i riquadri di congelamento, è il momento di salvare le modifiche. Salvare il file della cartella di lavoro modificata assicura che le impostazioni di congelamento vengano mantenute. Puoi salvare il file aggiornato utilizzando`Save` metodo.
```csharp
// Salvataggio del file Excel modificato
workbook.Save(dataDir + "output.xls");
```
Se vuoi conservare anche il file originale, assicurati di salvarlo con un nome diverso.
## Passaggio 7: chiudere il flusso di file
Infine, ricordatevi di chiudere il flusso di file. Questo libera risorse di sistema e finalizza tutte le connessioni aperte al file.
```csharp
// Chiusura del flusso di file per liberare tutte le risorse
fstream.Close();
```
Immagina di chiudere lo stream come se rimettessi il file sullo scaffale una volta che hai finito di usarlo. È una buona abitudine di pulizia.

## Conclusione
Congratulazioni! Hai applicato con successo i riquadri bloccati a un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Questa tecnica è incredibilmente utile per gestire grandi set di dati, assicurando che le intestazioni o righe e colonne specifiche rimangano visibili durante lo scorrimento dei dati. Seguendo questa guida passo passo, puoi implementare con sicurezza i riquadri bloccati e migliorare l'usabilità dei tuoi fogli di calcolo.
## Domande frequenti
### Posso bloccare più di un foglio in una cartella di lavoro?
 Sì, basta ripetere l'`FreezePanes` metodo su ogni foglio a cui vuoi applicarlo.
### Cosa succede se utilizzo valori di riga e colonna che superano l'intervallo del foglio?
Aspose.Cells genererà un'eccezione, quindi assicurati che i tuoi valori rientrino nei limiti del foglio di lavoro.
### Posso modificare le impostazioni dei riquadri bloccati dopo averle applicate?
 Assolutamente! Chiama semplicemente il`FreezePanes`metodo nuovamente con nuovi parametri per aggiornare le impostazioni.
### Il riquadro di blocco funziona su tutte le versioni dei file Excel?
Sì, i riquadri bloccati verranno conservati nella maggior parte dei formati Excel (ad esempio, XLS, XLSX) supportati da Aspose.Cells.
### Posso sbloccare i vetri?
 Per rimuovere i vetri bloccati, basta chiamare`UnfreezePanes()` sul foglio di lavoro.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
