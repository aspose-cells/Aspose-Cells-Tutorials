---
category: general
date: 2026-02-09
description: Crea un nuovo foglio di lavoro Excel e impara a copiare le tabelle pivot
  senza sforzo. Questa guida mostra come duplicare una tabella pivot e salvare il
  foglio di lavoro come nuovo.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: it
og_description: Crea un nuovo workbook Excel in C# e copia una tabella pivot istantaneamente.
  Scopri come duplicare la tabella pivot e salvare il workbook come nuovo con un esempio
  di codice completo.
og_title: Crea nuova cartella di lavoro Excel – Copia pivot passo passo
tags:
- excel
- csharp
- aspose.cells
- automation
title: Crea nuovo foglio di lavoro Excel – Copia e duplica tabella pivot
url: /it/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Nuova Cartella di Lavoro Excel – Copia & Duplica Tabella Pivot

Ti è mai capitato di **creare una nuova cartella di lavoro Excel** che riporti una tabella pivot complessa da un file esistente? Non sei l'unico: molti sviluppatori incontrano questo ostacolo quando automatizzano pipeline di reporting. La buona notizia è che, con poche righe di C# e la libreria Aspose.Cells, puoi **come copiare pivot** rapidamente, **duplicare la tabella pivot**, e **salvare la cartella di lavoro come nuova** senza aprire Excel manualmente.

In questa guida percorreremo l'intero processo, dal caricamento della cartella di lavoro sorgente al salvataggio della versione duplicata. Alla fine avrai uno snippet pronto da eseguire che potrai inserire in qualsiasi progetto .NET. Niente fronzoli, solo una soluzione pratica che puoi testare subito.

## Cosa Copre Questo Tutorial

* **Prerequisiti** – .NET 6+ (o .NET Framework 4.6+), Visual Studio e il pacchetto NuGet Aspose.Cells per .NET.  
* Codice passo‑passo che **crea una nuova cartella di lavoro Excel**, copia la pivot e scrive il risultato su disco.  
* Spiegazioni del **perché** ogni riga è importante, non solo del **cosa** fa.  
* Suggerimenti per gestire casi limite come fogli nascosti o intervalli di dati molto grandi.  
* Uno sguardo rapido a **come copiare un foglio di lavoro** se ti serve l'intero foglio invece della sola pivot.

Pronto? Immergiamoci.

![illustrazione creazione nuova cartella di lavoro excel](image.png "Diagramma che mostra la cartella di lavoro sorgente, la copia della pivot e la cartella di lavoro di destinazione")

## Passo 1: Configura il Progetto e Installa Aspose.Cells

Prima di poter **creare una nuova cartella di lavoro Excel**, ci serve un progetto che faccia riferimento alla libreria corretta.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Perché è importante:* Aspose.Cells funziona interamente in memoria, quindi non devi mai avviare Excel sul server. Inoltre preserva le informazioni della cache della pivot, essenziali per una vera **duplicazione della tabella pivot**.

> **Consiglio esperto:** Se stai puntando a .NET Core, assicurati che l'identificatore di runtime (RID) del tuo progetto corrisponda alla piattaforma su cui verrà distribuito; altrimenti potresti incorrere in errori di caricamento delle librerie native.

## Passo 2: Carica la Cartella di Lavoro Sorgente che Contiene la Pivot

Ora **come copiare pivot** da un file esistente. La cartella di lavoro sorgente può trovarsi ovunque su disco, in uno stream o anche in un array di byte.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Perché scegliamo un intervallo:* Una tabella pivot vive all'interno di un intervallo di celle normale, ma ha anche dati di cache nascosti collegati al foglio. Copiando l'intervallo **includendo la pivot**, Aspose.Cells garantisce che la cache viaggi con esso, fornendoti una **duplicazione della tabella pivot** funzionante nel file di destinazione.

## Passo 3: Crea una Nuova Cartella di Lavoro Excel per Ricevere i Dati Copiati

Qui è dove **creiamo una nuova cartella di lavoro Excel** che conterrà la pivot duplicata.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Perché una cartella di lavoro nuova?** Partire da una base pulita garantisce che nessuna formattazione residua o oggetti nascosti interferiscano con la pivot copiata. Inoltre rende il file risultante più leggero, utile per allegati email automatizzati.

## Passo 4: Copia l'Intervallo della Pivot nella Nuova Cartella di Lavoro

Ora eseguiamo l'operazione di **come copiare pivot** vera e propria.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Quella singola riga fa il lavoro pesante:

* I valori delle celle, le formule e la formattazione vengono trasferiti.  
* La cache della pivot viene duplicata, così la nuova pivot rimane pienamente funzionale.  
* Qualsiasi riferimento relativo all'interno della pivot si adatta automaticamente alla nuova posizione.

### Gestione dei Casi Limite

* **Fogli nascosti:** Se il foglio sorgente è nascosto, la pivot si copia comunque, ma potresti voler rendere visibile il foglio di destinazione per l'utente:  
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Set di dati grandi:** Per intervalli più grandi di qualche migliaio di righe, considera l'uso di `CopyTo` con `CopyOptions` per eseguire lo streaming dell'operazione e ridurre la pressione sulla memoria.

## Passo 5: Salva la Cartella di Lavoro di Destinazione come Nuovo File

Infine, **salviamo la cartella di lavoro come nuova** e verifichiamo il risultato.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Se apri `copied.xlsx` vedrai una replica esatta della pivot originale, pronta per ulteriori manipolazioni o distribuzioni.

### Opzionale: Come Copiare un Foglio di Lavoro Invece della Solo Pivot

A volte ti serve l'intero foglio, non solo la pivot. La stessa API lo rende banale:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Questo soddisfa la richiesta **come copiare foglio di lavoro** e può essere utile quando devi preservare impostazioni a livello di foglio aggiuntive.

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco un'app console autonoma che puoi compilare ed eseguire:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Output previsto:** la console stampa un messaggio di successo e `copied.xlsx` appare in `C:\Reports` con una pivot funzionale identica a quella di `source.xlsx`.

## Domande Frequenti & Trappole

* **Le formule dentro la pivot si romperanno?** No—poiché la cache della pivot viaggia con l'intervallo, tutti i campi calcolati rimangono intatti.  
* **E se la pivot sorgente usa connessioni dati esterne?** Quelle connessioni *non* vengono copiate. Dovrai ristabilirle nella cartella di lavoro di destinazione o convertire la pivot in una tabella statica prima.  
* **Posso copiare più pivot contemporaneamente?** Assolutamente—basta definire un intervallo più ampio che includa tutte le pivot, o iterare su ogni oggetto `PivotTable` in `sourceSheet.PivotTables` e copiarle singolarmente.  
* **Devo rilasciare gli oggetti `Workbook`?** Implementano `IDisposable`, quindi avvolgerli in blocchi `using` è una buona abitudine, soprattutto in servizi ad alto volume.

## Conclusione

Ora sai **come creare una nuova cartella di lavoro Excel**, copiare una pivot, **duplicare la tabella pivot** e **salvare la cartella di lavoro come nuova** usando C# e Aspose.Cells. I passaggi sono semplici: carica, crea, copia e salva. Con lo snippet opzionale **come copiare foglio di lavoro** hai anche una soluzione di riserva per la duplicazione dell'intero foglio.

Prossimi passi, potresti esplorare:

* Aggiungere formattazioni personalizzate alla pivot duplicata.  
* Aggiornare la cache della pivot programmaticamente dopo modifiche ai dati.  
* Esportare la cartella di lavoro in PDF o CSV per sistemi a valle.

Provalo, modifica l'intervallo e lascia che l'automazione tolga il lavoro pesante dal tuo flusso di reporting. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}