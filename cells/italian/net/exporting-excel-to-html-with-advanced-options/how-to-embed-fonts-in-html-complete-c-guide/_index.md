---
category: general
date: 2026-01-14
description: Come incorporare i font in HTML e forzare il calcolo delle formule durante
  la conversione di Excel in HTML. Impara a impostare l'area di stampa ed esportare
  i grafici.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: it
og_description: Come incorporare i font in HTML, forzare il calcolo delle formule
  e convertire Excel in HTML con le impostazioni dell'area di stampa—tutto in C#.
og_title: Come incorporare i font in HTML – Guida completa C#
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Come incorporare i font in HTML – Guida completa a C#
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font in HTML – Guida completa C#

Ti sei mai chiesto **come incorporare i font in HTML** quando esporti una cartella di lavoro Excel? Non sei l'unico. Molti sviluppatori si trovano di fronte a un ostacolo quando l'HTML generato appare corretto sul loro computer ma perde la tipografia su un altro dispositivo. La buona notizia? Con Aspose.Cells per .NET puoi incorporare i file dei font direttamente nell'output HTML—niente più glifi mancanti.

In questo tutorial percorreremo un esempio completo che non solo mostra **come incorporare i font in HTML**, ma dimostra anche **forzare il calcolo delle formule**, **convertire Excel in HTML**, e persino **come impostare l'area di stampa** prima di esportare un grafico in un PPTX modificabile. Alla fine avrai un unico programma C# eseguibile da inserire in qualsiasi progetto .NET.

---

## Cosa costruirai

- Crea una nuova cartella di lavoro, scrivi un paio di formule array e **forza il calcolo delle formule** in modo che i risultati siano incorporati nel file.  
- Salva la cartella di lavoro come HTML mentre **incorpori i font** e i loro selettori di variazione.  
- Carica una seconda cartella di lavoro che contiene un grafico, definisci una **area di stampa** e esporta quel foglio in una presentazione PowerPoint modificabile.  
- Tutto questo usando solo poche righe di codice C# pulito e ben commentato.

Nessuno strumento esterno, nessuna copia manuale dei file dei font—Aspose.Cells fa il lavoro pesante per te.

---

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0 o successivo | Funzionalità moderne del linguaggio e migliori prestazioni |
| Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`) | Fornisce `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions`, ecc. |
| Un paio di file di font TrueType/OpenType (es. `Arial.ttf`) posizionati nella cartella del progetto | Necessari per l'incorporamento; Aspose li preleverà automaticamente se sono installati sul sistema host |
| Conoscenza di base di C# | Per seguire il codice e adattarlo ai propri scenari |

---

## Passo 1 – Crea una cartella di lavoro e scrivi formule array  

Per prima cosa creiamo una nuova istanza di `Workbook` e inseriamo due formule array nelle celle **A1** e **A3**. Queste formule (`WRAPCOLS` e `WRAPROWS`) producono un piccolo array 2‑colonne/2‑righe che più tardi vedremo renderizzato nell'output HTML.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Perché è importante:** Inserendo le formule ottieni contenuti dinamici che verranno valutati quando forzeremo il calcolo in seguito. Dimostra inoltre che l'esportazione HTML può gestire correttamente i risultati delle formule array.

---

## Passo 2 – Forza il calcolo delle formule  

Aspose.Cells valuta le formule in modo pigro. Per garantire che il nostro HTML contenga i valori calcolati (invece delle formule grezze), chiamiamo `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Consiglio professionale:** Se salti questo passaggio, l'HTML mostrerà il testo della formula (`=WRAPCOLS...`) anziché i numeri, vanificando lo scopo di un'esportazione curata.

---

## Passo 3 – Configura le opzioni di salvataggio HTML per incorporare i font  

Ora arriva la star dello spettacolo: l'incorporamento dei font. Impostare `EmbedFonts` su `true` indica ad Aspose di includere i dati del font come flussi codificati Base64 all'interno del file HTML generato. Abilitare `EmbedFontVariationSelectors` garantisce che anche eventuali selettori di variazione OpenType (usati per tipografia avanzata) vengano preservati.

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **Come funziona:** Quando l'HTML viene scritto, Aspose inietta un blocco `<style>` con regole `@font-face` che fanno riferimento ai data URI incorporati. I browser renderanno lo stesso font indipendentemente dai font installati sul client.

---

## Passo 4 – Salva la cartella di lavoro come HTML  

Salviamo prima la cartella di lavoro in un file `.xlsx` (per il caso tu abbia bisogno della sorgente) e poi la esportiamo in HTML usando le opzioni appena definite.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Risultato:** Apri `fontDemo.html` in qualsiasi browser moderno e vedrai i valori dell'array renderizzati con il font incorporato, anche se il font non è installato sulla tua macchina.

---

## Passo 5 – Carica una cartella di lavoro con un grafico e imposta l'area di stampa  

Successivamente dimostriamo **come impostare l'area di stampa** prima di esportare un foglio che contiene un grafico. L'area di stampa limita ciò che viene renderizzato, utile quando vuoi includere solo un intervallo specifico nel PPTX finale.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **Perché impostare un'area di stampa?** Senza di essa, Aspose esporterebbe l'intero foglio, potenzialmente includendo righe/colonne vuote e gonfiando il file PPTX.

---

## Passo 6 – Esporta il foglio di lavoro in un PPTX modificabile  

Infine esportiamo il foglio di lavoro in un file PowerPoint modificabile. Impostando `ExportChartAsEditable = true`, il grafico viene salvato come forme native di PowerPoint, consentendo agli utenti finali di modificarlo direttamente in PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **Cosa ottieni:** `editableChart.pptx` contiene il grafico da `chartEditable.xlsx` come oggetti PowerPoint modificabili, limitati all'intervallo `A1:G20`.

---

## Panoramica dell'output previsto  

| File | Descrizione |
|------|-------------|
| `fontDemo.xlsx` | Cartella di lavoro originale con formule array calcolate. |
| `fontDemo.html` | File HTML che **incorpora i font**, mostra i risultati dell'array e funziona offline. |
| `editableChart.pptx` | Presentazione PowerPoint con un grafico modificabile, rispettando l'**area di stampa** impostata. |

Apri `fontDemo.html` in Chrome o Edge; noterai che il testo utilizza esattamente il font che hai incorporato (es. Arial) anche se il tuo sistema non lo possiede. Il grafico in `editableChart.pptx` può essere doppio‑cliccato e modificato come qualsiasi grafico nativo di PowerPoint.

---

## Domande comuni e casi limite  

### Cosa succede se il mio font non è installato sul server?  
Aspose.Cells incorporerà solo i font che sono *disponibili* al runtime. Se un determinato file di font manca, l'HTML ricadrà sul font predefinito del browser. Per garantire l'incorporamento, copia i file `.ttf`/`.otf` necessari nella cartella dell'applicazione e riferiscili tramite `FontInfo` (scenario avanzato).

### Posso incorporare solo un sottoinsieme di caratteri per ridurre le dimensioni del file?  
Sì. Usa `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. Questo indica ad Aspose di includere solo i glifi effettivamente utilizzati nella cartella di lavoro, riducendo drasticamente il peso dell'HTML.

### Il **forzare il calcolo delle formule** funziona anche per funzioni volatili come `NOW()`?  
Assolutamente. `CalculateFormula()` valuta tutte le formule, incluse quelle volatili, al momento della chiamata. Se hai bisogno che il calcolo rifletta una data/ora specifica, imposta prima le `CalculationOptions` della cartella di lavoro.

### E per cartelle di lavoro grandi – l'incorporamento dei font gonfierà l'HTML?  
L'incorporamento dei font aggiunge circa 100‑200 KB per font (a seconda delle dimensioni). Per report molto grandi, considera di collegare font ospitati sul web invece di incorporarli, oppure usa la modalità sottoinsieme menzionata sopra.

---

## Consigli professionali e migliori pratiche  

- **Salvataggi batch:** Se generi decine di file HTML, riutilizza una singola istanza di `HtmlSaveOptions` per evitare allocazioni inutili.  
- **Cache delle aree di stampa:** Quando esporti molti fogli, memorizza l'area di stampa desiderata in un file di configurazione per mantenere il codice DRY.  
- **Convalida dell'output:** Dopo aver salvato l'HTML, esegui un rapido controllo con un browser headless (es. Puppeteer) per assicurarti che i font vengano renderizzati correttamente prima di distribuirli agli utenti.  
- **Blocco della versione:** Il codice sopra è mirato a Aspose.Cells 23.12+. Versioni più recenti potrebbero introdurre opzioni aggiuntive come `FontEmbeddingMode`. Controlla sempre le note di rilascio.

---

## Conclusione  

Abbiamo coperto **come incorporare i font in HTML** usando Aspose.Cells, mostrato l'importanza di **forzare il calcolo delle formule**, dimostrato un flusso di lavoro pulito per **convertire Excel in HTML**, e spiegato **come impostare l'area di stampa** prima di esportare un grafico in un PPTX modificabile. L'esempio completo e eseguibile si trova in un unico file `Program.cs`, così puoi copiarlo, modificare i percorsi e farlo girare subito.

Pronto per il passo successivo? Prova a sostituire il font incorporato con un carattere personalizzato del tuo brand, o sperimenta la modalità `Subset` per mantenere leggero l'HTML. Lo stesso schema funziona per PDF, immagini e persino esportazioni CSV—basta cambiare la classe `SaveOptions`.

Hai altre domande su incorporamento dei font, gestione delle formule o trucchi sull'area di stampa? Lascia un commento qui sotto o contattami nei forum della community Aspose. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}