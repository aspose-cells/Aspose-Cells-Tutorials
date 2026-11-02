---
category: general
date: 2026-04-07
description: Applica un formato numerico personalizzato a una cella di un foglio di
  calcolo e scopri come formattare i numeri nel foglio di calcolo durante l'esportazione
  del valore della cella con C#. Guida rapida e completa.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: it
og_description: Applica un formato numerico personalizzato a una cella di un foglio
  di calcolo ed esportala come stringa formattata. Scopri come formattare i numeri
  nel foglio di calcolo ed esportare il valore della cella.
og_title: Applica Formato Numerico Personalizzato – Tutorial Completo di Esportazione
  C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Applicare un formato numerico personalizzato nell'esportazione di fogli di
  calcolo C# – Guida passo passo
url: /it/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applica un formato numerico personalizzato in C# per l'esportazione di fogli di calcolo – Tutorial completo

Hai mai dovuto **applicare un formato numerico personalizzato** a una cella e poi estrarre quella stringa formattata da un foglio di calcolo? Non sei il solo. Molti sviluppatori si trovano in difficoltà quando scoprono che viene restituito il valore grezzo invece della stringa formattata, bella da vedere e sensibile alla localizzazione, che si aspettavano. In questa guida ti mostreremo esattamente come formattare i numeri nelle celle di un foglio di calcolo e come esportare il valore della cella come stringa formattata usando una popolare libreria C# per fogli di calcolo.

Al termine del walkthrough sarai in grado di **applicare un formato numerico personalizzato** a qualsiasi cella numerica, esportare il risultato con `ExportTable` e vedere l'output esatto che ti aspetti di mostrare in un'interfaccia UI o in un report. Nessuna documentazione esterna necessaria—tutto è qui.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+)
- Un riferimento alla libreria di fogli di calcolo che fornisce `Workbook`, `Worksheet` e `ExportTableOptions` (ad es., **Aspose.Cells** o **GemBox.Spreadsheet**; l'API mostrata corrisponde a Aspose.Cells)
- Conoscenze di base di C#—se sai scrivere un `Console.WriteLine`, sei pronto per partire

> **Pro tip:** Se usi una libreria diversa, i nomi delle proprietà sono solitamente simili (`NumberFormat`, `ExportAsString`). Basta mappare di conseguenza.

## Cosa copre il tutorial

1. Creare una cartella di lavoro e selezionare il primo foglio di lavoro.  
2. Inserire un valore numerico in una cella.  
3. Configurare `ExportTableOptions` per **applicare un formato numerico personalizzato** e restituire una stringa.  
4. Esportare la cella e stampare il risultato formattato.  
5. Gestione dei casi limite – cosa succede se la cella contiene una formula o un valore nullo?

Iniziamo.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Step 1 – Crea una cartella di lavoro e ottieni il primo foglio

La prima cosa di cui hai bisogno è un oggetto workbook. Pensalo come il file Excel che apriresti nell'app Office. Una volta ottenuto, prendi il primo foglio—la maggior parte dei tutorial parte da lì perché mantiene l'esempio conciso.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Perché è importante:** Un workbook nuovo ti offre una tela pulita, garantendo che nessuna formattazione nascosta interferisca con il nostro formato numerico personalizzato in seguito.

## Step 2 – Inserisci un valore numerico nella cella B2 (la cella che esporteremo)

Ora abbiamo bisogno di qualcosa da formattare. La cella **B2** è un punto comodo—facile da riferire e sufficientemente distante dall'angolo predefinito A1 per evitare sovrascritture accidentali.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**E se il valore fosse una formula?**  
Se in seguito sostituisci il valore grezzo con una formula (ad es., `=SUM(A1:A10)`), la routine di esportazione rispetterà comunque il formato numerico che applichiamo nel passaggio successivo, perché la formattazione è associata alla cella, non al tipo di valore.

## Step 3 – Configura le opzioni di esportazione per ricevere il valore come stringa formattata

Ecco il cuore del tutorial: diciamo alla libreria di **applicare un formato numerico personalizzato** durante l'esportazione. La stringa `NumberFormat` segue lo stesso schema che useresti nella categoria “Personalizzato” di Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` assicura che il metodo restituisca una `string` invece di un `double` grezzo.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` replica lo schema di Excel: virgole per le migliaia, due decimali e parentesi per i numeri negativi.

> **Perché usare un formato personalizzato?** Garantisce coerenza tra culture (ad es., separatori numerici US vs. Europei) e ti permette di inserire uno stile specifico per il business, come le parentesi contabili.

## Step 4 – Esporta la cella usando le opzioni configurate

Ora estraiamo effettivamente il valore dal foglio di lavoro, lasciando che la libreria si occupi di applicare il formato che abbiamo definito.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Caso limite – cella vuota:** Se `B2` fosse vuota, `formattedResult` sarebbe `null`. Puoi proteggerti con un semplice controllo null prima di stampare.

## Step 5 – Visualizza la stringa formattata

Infine, scriviamo il risultato sulla console. In un'app reale potresti inserire questa stringa in un PDF, in un'email o in un'etichetta UI.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Output previsto**

```
1,234.56
```

Se cambi il valore grezzo in `-9876.54`, lo stesso formato ti restituirà `(9,876.54)`—esattamente ciò che richiedono molti report contabili.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto console. Si compila ed esegue così com'è, a patto di aver aggiunto il pacchetto NuGet appropriato per la libreria di fogli di calcolo.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Rapida verifica di correttezza

- **Compila?** Sì—basta assicurarsi che il DLL `Aspose.Cells` (o equivalente) sia referenziato.  
- **Funziona con altre culture?** La stringa di formato è indipendente dalla cultura; la libreria rispetta lo schema che le fornisci. Se ti servono separatori specifici per locale, puoi aggiungere la gestione di `CultureInfo` prima dell'esportazione.

## Domande frequenti & variazioni

### Come **format number in spreadsheet** usando uno schema diverso?

Sostituisci la stringa `NumberFormat`. Per esempio, per mostrare una percentuale con una cifra decimale:

```csharp
NumberFormat = "0.0%";
```

### E se devo **how to export cell value** come HTML invece che testo semplice?

La maggior parte delle librerie offre un overload che **accetta** un tipo di esportazione. Imposteresti `ExportAsString = true` e aggiungeresti `ExportHtml = true` (o simile). Il principio rimane lo stesso: definisci il formato, poi scegli la rappresentazione di output.

### Posso applicare il formato a un intervallo intero, non solo a una cella?

Assolutamente. Puoi assegnare `NumberFormat` a un oggetto `Style` e poi applicare quello stile a un `Range`. La chiamata di esportazione rimane invariata; prenderà automaticamente lo stile.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Cosa succede quando la cella contiene una formula?

La routine di esportazione valuta prima la formula, poi formatta il valore numerico risultante. Non serve codice aggiuntivo—basta assicurarsi che `Calculate` sia stato chiamato se hai disabilitato il calcolo automatico.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusione

Ora sai come **applicare un formato numerico personalizzato** a una cella di un foglio di calcolo, **format number in spreadsheet** in vari contesti, e **how to export cell value** come stringa pronta per la visualizzazione. Il conciso esempio di codice sopra copre ogni passaggio—dalla creazione del workbook all'output finale—così puoi inserirlo direttamente in un progetto di produzione.

Pronto per la prossima sfida? Prova a combinare questa tecnica con **how to format numeric cell** per date, simboli di valuta o formattazione condizionale. Oppure esplora l'esportazione di più celle come CSV mantenendo il formato personalizzato di ciascuna. Il cielo è il limite, e con queste basi hai una solida fondazione.

Buon coding, e non dimenticare di sperimentare—a volte le migliori soluzioni emergono quando si aggiusta un po' la stringa di formato!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}