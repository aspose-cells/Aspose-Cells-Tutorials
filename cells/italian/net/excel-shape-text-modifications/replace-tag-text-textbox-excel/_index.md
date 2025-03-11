---
title: Sostituisci tag con testo nella casella di testo in Excel
linktitle: Sostituisci tag con testo nella casella di testo in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Sostituisci senza sforzo il testo nelle caselle di testo nei tuoi fogli Excel usando Aspose.Cells per .NET. Una guida passo passo per l'automazione di Excel.
weight: 11
url: /it/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sostituisci tag con testo nella casella di testo in Excel

## Introduzione
In questo articolo, ci immergeremo in un'attività specifica: sostituire i tag con testo all'interno di caselle di testo in un foglio Excel usando Aspose.Cells. Ti guideremo passo dopo passo attraverso l'intero processo, assicurandoti di comprendere ogni dettaglio. Alla fine di questo tutorial, non solo migliorerai la tua comprensione di Aspose.Cells, ma semplificherai anche le tue attività relative a Excel!
## Prerequisiti
Prima di iniziare, devi avere a disposizione alcune cose:
1. Visual Studio: assicurati di avere installato Visual Studio. È un IDE flessibile che rende la codifica in C# un gioco da ragazzi.
2.  Libreria Aspose.Cells: se non l'hai ancora fatto, scarica la libreria Aspose.Cells per .NET da[pagina](https://releases.aspose.com/cells/net/)Puoi anche ottenere una versione di prova gratuita per verificarne le funzionalità.
3. Conoscenza di base di C#: una conoscenza di base della programmazione C# ti sarà molto utile per seguire facilmente questa guida.
Ora che è tutto pronto, passiamo alla parte divertente: scrivere il codice!
## Importa pacchetti
Prima di tutto, importiamo i pacchetti necessari. Questo è fondamentale perché senza le importazioni giuste, il tuo codice non riconoscerà le classi e i metodi che utilizzeremo.
## Avvia il tuo progetto C#
Apri Visual Studio e crea un nuovo progetto C#, preferibilmente un'applicazione console, poiché ti consentirà di visualizzare facilmente l'output.
## Aggiungi riferimento Aspose.Cells
- Fai clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Selezionare “Aggiungi” > “Riferimento”.
- Vai alla posizione in cui hai scaricato la libreria Aspose.Cells e includila nel tuo progetto.
## Importare gli spazi dei nomi necessari
 Dopo aver aggiunto il riferimento, aggiungi quanto segue`using` direttiva in cima al tuo file principale:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Ciò consente di accedere alle classi all'interno dello spazio dei nomi Aspose.Cells.
Ora che abbiamo impostato il nostro ambiente, passiamo alla parte succosa: la codifica! Il nostro obiettivo è trovare tag specifici nelle caselle di testo all'interno di un file Excel e sostituirli con il testo fornito.
## Passaggio 1: definire la directory di origine e di output
Per prima cosa dobbiamo specificare dove si trova il file Excel di origine e dove vogliamo salvare la versione modificata.
```csharp
// Directory di origine e di output
string sourceDir = "Your Document Directory"; // Passa alla tua directory
string outputDir = "Your Document Directory"; // Passa alla tua directory
```
## Passaggio 2: caricare la cartella di lavoro
Qui è dove caricheremo la nostra cartella di lavoro Excel. Se il file non esiste, viene generato un errore. Quindi, assicurati che il percorso del file sia corretto!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Qui, stiamo caricando un file Excel esistente chiamato`sampleReplaceTagWithText.xlsx`.
## Passaggio 3: definire i tag e il testo sostitutivo
Ora dobbiamo definire i tag che stiamo cercando e con cosa vogliamo sostituirli.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 In questo esempio, i tag vengono divisi utilizzando`$`Puoi sostituirlo con qualsiasi delimitatore tu preferisca.
## Passaggio 4: Esegui il ciclo sui tag e sostituiscili
Creeremo un loop per passare attraverso ogni tag che vogliamo sostituire. Ecco dove avviene la magia!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Passaggio 5: salvare la cartella di lavoro
Ora che abbiamo fatto le nostre sostituzioni, è il momento di salvare la cartella di lavoro modificata nel formato desiderato. Ecco come convertirla in un PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Puoi salvarlo anche in altri formati, tra cui XLSX.
## Fase 6: implementare la logica di sostituzione
 È qui che risiede il cuore della nostra funzionalità. Il`sheetReplace` Il metodo gestirà la sostituzione effettiva nei fogli di lavoro Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Per prima cosa, scorriamo ogni foglio di lavoro nella cartella di lavoro.
- Sostituiamo il tag principale non solo nel contenuto delle celle, ma anche nelle intestazioni e nei piè di pagina (se presenti).
- Infine, controlliamo ogni casella di testo nel foglio e sostituiamo il testo al suo interno, in base al tag che stiamo cercando.
## Conclusione
Ed ecco fatto! Ora hai imparato a sostituire i tag con il testo nelle caselle di testo nei tuoi documenti Excel usando Aspose.Cells per .NET. Questo può farti risparmiare davvero tempo, specialmente quando hai a che fare con attività ripetitive nei fogli di calcolo.
## Domande frequenti
### Posso sostituire i tag in più file Excel contemporaneamente?
Sì, scorrendo un elenco di file è possibile applicare la stessa logica a più file Excel.
### Ho bisogno di una licenza a pagamento per utilizzare Aspose.Cells?
 Puoi iniziare con una prova gratuita, ma per la piena funzionalità, dovrai acquistare una licenza. Dai un'occhiata[Opzioni di acquisto di Aspose](https://purchase.aspose.com/buy).
### Posso sostituire le immagini nelle caselle di testo utilizzando Aspose.Cells?
Aspose.Cells si occupa principalmente di testo. Tuttavia, puoi manipolare le immagini separatamente se necessario.
### In quali formati posso salvare il mio file Excel modificato?
Puoi salvarlo in vari formati, tra cui XLSX, PDF, CSV, ecc.
### Dove posso trovare supporto per Aspose.Cells?
 Puoi trovare supporto e porre domande su[Forum di Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
