---
category: general
date: 2026-04-07
description: Scrivi data e ora in Excel usando C#. Scopri come inserire una data nel
  foglio di lavoro, gestire il valore della data in una cella di Excel e convertire
  la data del calendario giapponese in pochi passaggi.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: it
og_description: Scrivi data e ora in Excel rapidamente. Questa guida mostra come inserire
  la data in un foglio di lavoro, gestire il valore della data in una cella di Excel
  e convertire la data del calendario giapponese con C#.
og_title: Scrivi data e ora in Excel – Tutorial C# passo passo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Scrivi data e ora in Excel – Guida completa per gli sviluppatori C#
url: /it/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Scrivere datetime su Excel – Guida completa per sviluppatori C#

Ti è mai capitato di dover **scrivere datetime su Excel** senza sapere quale chiamata API memorizzi effettivamente una data Excel corretta? Non sei l’unico. In molti strumenti aziendali dobbiamo inserire un `DateTime` C# in un foglio di calcolo, e il risultato deve comportarsi come una vera data Excel—ordinabile, filtrabile e pronta per le tabelle pivot.  

In questo tutorial vedremo passo passo come *inserire una data nel foglio di lavoro* usando Aspose.Cells, spiegheremo perché è importante impostare la cultura e mostreremo anche come **convertire una data del calendario giapponese** in un `DateTime` regolare prima di scriverla. Alla fine avrai uno snippet autonomo da copiare‑incollare in qualsiasi progetto .NET.

## Cosa ti serve

- **.NET 6+** (o qualsiasi versione recente di .NET; il codice funziona anche su .NET Framework)  
- **Aspose.Cells for .NET** – un pacchetto NuGet che consente di manipolare file Excel senza avere Office installato.  
- Una conoscenza di base di `DateTime` C# e delle culture.  

Nessuna libreria aggiuntiva, nessun interop COM e nessuna installazione di Excel richiesta. Se hai già un’istanza di foglio di lavoro (`ws`), sei pronto per partire.

## Passo 1: Configurare la cultura giapponese (Convertire data del calendario giapponese)

Quando ricevi una data come `"R02/05/01"` (Reiwa 2, 1 maggio) devi indicare a .NET come interpretare i simboli dell’era. Il calendario giapponese non è il calendario gregoriano predefinito, quindi creiamo un `CultureInfo` che sostituisce il suo calendario con `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Perché è importante:**  
Se analizzi la stringa con la cultura predefinita, .NET solleverà un’eccezione di formato perché non riesce a mappare `R` (l’era Reiwa) a un anno. Sostituendo con `JapaneseCalendar`, il parser comprende i simboli dell’era e li traduce nell’anno gregoriano corretto.

## Passo 2: Analizzare la stringa basata sull’era in un `DateTime`

Ora che la cultura è pronta, possiamo chiamare in sicurezza `DateTime.ParseExact`. La stringa di formato `"ggyy/MM/dd"` indica al parser:

- `gg` – designatore dell’era (es. `R` per Reiwa)  
- `yy` – anno a due cifre all’interno dell’era  
- `MM/dd` – mese e giorno.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Consiglio professionale:** Se potresti ricevere date in altri formati (es. `"Heisei 30/12/31"`), avvolgi l’analisi in un `try/catch` e ricorri a `DateTime.TryParseExact`. In questo modo il tuo intero processo di importazione non si bloccherà a causa di una singola riga errata.

## Passo 3: Scrivere il `DateTime` in una cella Excel (Valore data della cella Excel)

Aspose.Cells tratta un `DateTime` .NET come una data Excel nativa quando usi `PutValue`. La libreria converte automaticamente i tick in un numero seriale Excel (il numero di giorni dal 1900‑01‑00). Questo significa che la cella mostrerà un corretto **excel cell date value** e potrai formattarla in seguito usando gli stili data integrati di Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Cosa vedrai in Excel:**  
La cella C1 ora contiene il numero seriale `44796`, che Excel visualizza come `2020‑05‑01` (o qualunque formato tu abbia applicato). Il valore sottostante è una vera data, non una stringa, quindi l’ordinamento funziona come previsto.

## Passo 4: Salvare la cartella di lavoro (Conclusione)

Se non hai ancora salvato la cartella di lavoro, fallo ora. Questo passo non riguarda direttamente la scrittura del datetime, ma completa il flusso di lavoro.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Ecco fatto—quattro passaggi concisi, e hai **scrivere datetime su Excel** con successo, gestendo una data dell’era giapponese lungo il percorso.

---

![esempio di scrittura datetime su excel](/images/write-datetime-to-excel.png "Screenshot che mostra un progetto C# che scrive un DateTime nella cella C1 di Excel")

*L’immagine sopra illustra il file Excel finale con la data visualizzata correttamente nella cella C1.*

## Domande frequenti e casi particolari

### E se la variabile worksheet non è ancora pronta?

Puoi creare una nuova cartella di lavoro al volo:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Come posso conservare la stringa originale dell’era giapponese nel foglio?

Se ti servono sia la stringa originale sia la data analizzata, scrivile in celle adiacenti:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Funziona con versioni .NET più vecchie?

Sì. `JapaneseCalendar` esiste sin da .NET 2.0, e Aspose.Cells supporta .NET Framework 4.5+. Assicurati solo di fare riferimento all’assembly corretto.

### E i fusi orari?

`DateTime.ParseExact` restituisce un **Kind** di `Unspecified`. Se le tue date di origine sono in UTC, convertili prima:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Posso impostare un formato data personalizzato (es. “yyyy年MM月dd日”)?

Assolutamente. Usa la proprietà `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Ora Excel mostrerà `2020年05月01日` mantenendo comunque un valore data reale.

## Riepilogo

Abbiamo coperto tutto ciò che ti serve per **scrivere datetime su Excel** da C#:

1. **Configura** una cultura giapponese con `JapaneseCalendar` per **convertire date del calendario giapponese**.  
2. **Analizza** la stringa basata sull’era usando `DateTime.ParseExact`.  
3. **Inserisci** il `DateTime` risultante in una cella, garantendo un corretto **excel cell date value**.  
4. **Salva** la cartella di lavoro affinché i dati persistano.

Con questi quattro passaggi puoi inserire in modo sicuro **date nel foglio di lavoro** indipendentemente dal formato di origine. Il codice è completamente eseguibile, richiede solo Aspose.Cells e funziona su qualsiasi runtime .NET moderno.

## Qual è il prossimo passo?

- **Importazione bulk:** Scorri le righe di un CSV, analizza ogni data giapponese e scrivile in celle consecutive.  
- **Stilizzazione:** Applica formattazione condizionale per evidenziare le scadenze passate.  
- **Performance:** Usa `WorkbookDesigner` o il caching di `CellStyle` quando gestisci migliaia di righe.  

Sentiti libero di sperimentare—sostituisci l’era giapponese con il calendario gregoriano, cambia la cella di destinazione o esporta in un formato diverso (CSV, ODS). L’idea di base rimane la stessa: analizza, converti e **scrivi datetime su Excel** con fiducia.

Buon coding, e che i tuoi fogli di calcolo si ordinino sempre correttamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}