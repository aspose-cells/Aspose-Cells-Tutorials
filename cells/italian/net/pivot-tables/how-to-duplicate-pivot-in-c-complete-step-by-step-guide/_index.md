---
category: general
date: 2026-03-22
description: Scopri come duplicare una tabella pivot in C# usando Aspose.Cells. Questa
  guida mostra anche come copiare righe e caricare un workbook Excel in C# per un'automazione
  Excel fluida nella copia delle righe.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: it
og_description: Come duplicare un pivot in C#? Segui questo conciso tutorial per caricare
  una cartella di lavoro Excel in C#, copiare le righe e padroneggiare l'automazione
  di Excel per copiare le righe.
og_title: Come duplicare Pivot in C# – Guida completa
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Come duplicare Pivot in C# – Guida completa passo passo
url: /it/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come duplicare una tabella pivot in C# – Guida completa passo‑passo

Ti sei mai chiesto **come duplicare una pivot** programmaticamente senza trascinarla manualmente in Excel? Non sei l'unico. In molti flussi di reporting è necessario lo stesso layout pivot su un nuovo set di righe, e farlo a mano è una perdita di tempo.  

La buona notizia? Con poche righe di C# puoi caricare una cartella di lavoro Excel, definire l'area che contiene la pivot e **come copiare le righe** in modo che la pivot appaia in una nuova posizione—tutto in un'unica esecuzione automatizzata. In questo tutorial copriremo anche le basi di **load excel workbook c#** e ti forniremo una solida base per le attività di **excel automation copy rows**.

> **Cosa otterrai**  
> • Un esempio completo e eseguibile che duplica una tabella pivot.  
> • Una spiegazione del motivo per cui ogni riga è importante.  
> • Suggerimenti per gestire casi particolari come fogli nascosti o più pivot.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

- **.NET 6.0** (o qualsiasi versione recente di .NET) installata.  
- **Aspose.Cells for .NET** – la libreria che useremo per manipolare i file Excel. Puoi ottenerla tramite NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Un workbook di origine (`Source.xlsx`) che contiene già una tabella pivot nell'intervallo **A1:J20** (l'intervallo che duplicheremo).  
- Familiarità di base con la sintassi C# – niente di complicato, solo le consuete istruzioni `using` e il metodo `Main`.

Se qualcuno di questi ti è sconosciuto, fermati un attimo e installa il pacchetto; il resto della guida presuppone che la libreria sia pronta all'uso.

![Illustrazione di come duplicare una pivot in C# usando Aspose.Cells](https://example.com/duplicate-pivot.png "illustrazione di come duplicare una pivot in C#")

*Testo alternativo dell'immagine: "come duplicare una pivot in C# esempio che mostra le righe della pivot originale e duplicate".*

## Passo 1: Caricare un workbook Excel C# – Aprire il file

La prima cosa da fare quando vuoi **load excel workbook c#** è creare un'istanza `Workbook` che punti al tuo file. Questo oggetto ti dà accesso a ogni foglio, cella e pivot all'interno del file.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Perché è importante:**  
`Workbook` astrae l'intero file Excel in un modello in‑memoria. Senza caricarlo prima non puoi ispezionare la posizione della pivot o copiare le righe. Inoltre, il costruttore rileva automaticamente il formato del file (XLS, XLSX, CSV, ecc.), quindi non è necessario codice aggiuntivo per il rilevamento del formato.

## Passo 2: Come copiare le righe – Definire l'area della pivot

Ora che il workbook è in memoria, dobbiamo indicare ad Aspose.Cells quali righe contengono la pivot. Nel nostro esempio la pivot si trova in **A1:J20**, che corrisponde alle righe **0‑19** (indicizzazione a zero). Avvolgeremo questo in una struttura `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Perché usiamo `CellArea`:**  
È un modo leggero per descrivere un blocco rettangolare. Quando in seguito chiami `CopyRows`, il metodo legge questo oggetto per sapere esattamente quali righe duplicare. Se dovessi mai modificare l'intervallo (ad esempio la pivot si espande alla colonna K), devi cambiare solo il valore `endColumn`.

## Passo 3: Accedere al foglio di lavoro di destinazione

La maggior parte dei workbook ha un solo foglio, ma l'API funziona allo stesso modo per più fogli. Prendi il primo foglio (indice 0) – è lì che si trova la pivot originale.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Suggerimento professionale:**  
Se hai fogli con nome, puoi recuperarli anche per nome: `workbook.Worksheets["Sheet1"]`. Questo aiuta a evitare di codificare a mano gli indici quando la struttura del workbook cambia.

## Passo 4: Come copiare le righe – Duplicare la tabella pivot

Ecco il cuore di **how to duplicate pivot**: copiamo le righe contenenti la pivot in una nuova posizione. Nel nostro caso iniziamo dalla riga 31 (indice zero‑based 30). Il metodo `CopyRows` copia *sia* i dati sia la cache della pivot sottostante, quindi le nuove righe si comportano esattamente come quelle originali.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Cosa succede dietro le quinte?**  
`CopyRows` clona ogni riga, preservando formule, stili e definizioni della pivot. Poiché la cache della pivot vive a livello di workbook, la pivot duplicata fa automaticamente riferimento alla stessa fonte dati – non è necessaria alcuna configurazione aggiuntiva.

**Caso particolare – righe nascoste:**  
Se alcune delle righe nell'intervallo di origine sono nascoste, rimarranno nascoste dopo la copia. Se desideri renderle visibili, chiama `worksheet.Rows[destRow].IsHidden = false` dopo la copia.

## Passo 5: Salvare il workbook – Verificare il duplicato

Infine, scrivi le modifiche su disco. Puoi sovrascrivere il file originale o, più sicuro, salvare con un nuovo nome così da poter confrontare prima/dopo.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Risultato atteso:**  
Apri `CopyWithPivot.xlsx`. Troverai la pivot originale in **A1:J20** e una copia identica che inizia in **A31:J50**. Entrambe le pivot possono essere aggiornate indipendentemente, e qualsiasi slicer collegato all'originale funzionerà ancora per la copia perché condividono la stessa cache.

## Domande comuni e variazioni

### Posso duplicare più pivot contemporaneamente?

Assolutamente. Scorri tutte le tabelle pivot (`worksheet.PivotTables`) e copia l'intervallo di ciascuna in una destinazione diversa. Assicurati solo che gli intervalli di destinazione non si sovrappongano.

### E se il workbook di origine è protetto da password?

Aspose.Cells ti consente di aprire un file protetto passando la password al costruttore `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Come copiare le righe senza influire sulle formule?

Se ti servono solo i *valori* (senza formule), usa `CopyRows` con il flag `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### È possibile copiare le righe in un *diverso* workbook?

Sì. Dopo aver copiato le righe nel foglio di origine, puoi clonare il foglio in un'altra istanza `Workbook` tramite `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## Suggerimenti professionali per una copia affidabile di righe in Excel Automation

- **Convalida l'intervallo** prima di copiare. Un rapido `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` previene errori fuori intervallo.  
- **Disattiva il calcolo** durante la copia di grandi intervalli: `workbook.Settings.CalcMode = CalcMode.Manual;` – questo velocizza notevolmente l'operazione.  
- **Rilascia gli oggetti** (`workbook.Dispose()`) se stai elaborando molti file in un ciclo per liberare le risorse native.  
- **Registra l'operazione** – soprattutto nei pipeline di produzione – così puoi tracciare quali file sono stati elaborati e rilevare i fallimenti in anticipo.

## Conclusione

Ora sai **how to duplicate pivot** tabelle in C# usando Aspose.Cells, e hai visto l'intero flusso di lavoro da **load excel workbook c#** a **excel automation copy rows** fino al salvataggio del risultato. L'esempio è autonomo, funziona subito, e può essere esteso per gestire più pivot, file protetti o copie tra workbook.

Passi successivi? Prova ad adattare lo script per:

- Aggiornare la pivot duplicata programmaticamente (`pivotTable.RefreshData();`).  
- Esportare l'area duplicata in CSV per l'elaborazione successiva.  
- Integrare il codice in un'API ASP.NET Core così gli utenti possono caricare un file e ricevere immediatamente una versione con pivot duplicata.

Buon coding, e che la tua automazione Excel sia sempre fluida!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}