---
title: Copia l'archiviazione del progettista del modulo utente VBAMacro nella cartella di lavoro utilizzando Aspose.Cells
linktitle: Copia l'archiviazione del progettista del modulo utente VBAMacro nella cartella di lavoro utilizzando Aspose.Cells
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come copiare in modo efficiente VBA Macro User Form Designer in Aspose.Cells per .NET con il nostro tutorial completo passo dopo passo! Sblocca il potenziale di Excel.
weight: 11
url: /it/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia l'archiviazione del progettista del modulo utente VBAMacro nella cartella di lavoro utilizzando Aspose.Cells

## Introduzione
Benvenuti! Se stai cercando di migliorare la tua esperienza Excel con macro VBA e moduli utente, sei nel posto giusto! In questa guida, ci immergiamo in come puoi copiare senza problemi un VBA Macro UserForm Designer da una cartella di lavoro a un'altra utilizzando Aspose.Cells per .NET. Che tu sia uno sviluppatore esperto o alle prime armi, ti guideremo attraverso ogni passaggio cruciale. Considera questo il tuo manuale per padroneggiare l'arte di gestire i file Excel a livello di programmazione. Pronti a tuffarci? Andiamo!
## Prerequisiti
Prima di addentrarci nei dettagli della codifica, assicuriamoci di avere tutto ciò di cui hai bisogno:
1. Ambiente di sviluppo C#: dovresti avere un ambiente di lavoro pronto per lo sviluppo C#. Visual Studio è altamente raccomandato.
2.  Aspose.Cells per la libreria .NET: assicurati di avere la libreria Aspose.Cells integrata nel tuo progetto. Puoi facilmente[scaricalo qui](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di VBA e macro di Excel: una buona conoscenza di VBA e del funzionamento delle macro di Excel ti aiuterà a navigare con facilità in questo tutorial.
4. Un file Excel con un modulo utente: per sperimentare, creare o ottenere una cartella di lavoro Excel che contenga un modulo utente, preferibilmente con macro abilitate (come`.xlsm` file).
## Importa pacchetti
Nel tuo progetto C#, dovrai importare determinati namespace nella parte superiore del tuo file per utilizzare le funzionalità di Aspose.Cells. Ecco come fare:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Includendo questi namespace è possibile accedere a tutti i potenti strumenti incorporati nella libreria Aspose.Cells. 
Ora che abbiamo coperto i nostri prerequisiti e pacchetti, è tempo di passare alla parte divertente: la codifica! Analizziamola passo dopo passo.
## Passaggio 1: definire le directory di origine e di output
Per prima cosa, devi stabilire dove si trovano i tuoi file:
```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
// Directory di uscita
string outputDir = "Your Document Directory";
```
 Qui, sostituisci`"Your Document Directory"` con il percorso effettivo in cui sono archiviati i tuoi file. È da qui che verrà prelevata la nostra cartella di lavoro di origine (con UserForm) e dove verrà salvata la nuova cartella di lavoro.
## Passaggio 2: creare una cartella di lavoro di destinazione vuota
Ora creiamo la nostra cartella di lavoro di destinazione in cui copieremo il nostro modulo utente e le macro:
```csharp
// Crea una cartella di lavoro di destinazione vuota
Workbook target = new Workbook();
```
Questa riga di codice inizializza una nuova cartella di lavoro vuota da riempire con i dati. Considerala come una tela bianca per il tuo capolavoro!
## Passaggio 3: carica la cartella di lavoro del modello
Dobbiamo caricare la cartella di lavoro che contiene il modulo utente e le macro:
```csharp
// Caricare il file Excel contenente il modulo utente VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Assicurati di cambiare`"sampleDesignerForm.xlsm"` al nome del tuo file effettivo. Questa cartella di lavoro è come il tuo libro di ricette: è da lì che prenderemo i nostri ingredienti!
## Passaggio 4: Copia i fogli di lavoro nella cartella di lavoro di destinazione
Ora iniziamo a copiare i fogli di lavoro dal nostro modello alla cartella di lavoro di destinazione:
```csharp
// Copia tutti i fogli di lavoro modello nella cartella di lavoro di destinazione
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Inserisci il messaggio nella cella A2 del foglio di lavoro di destinazione
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
In questo passaggio, stiamo scorrendo ogni foglio di lavoro nel modello e copiandolo nella nostra cartella di lavoro di destinazione. Se ci pensi, è come trasferire le tue migliori ricette da un libro di cucina a un altro!
## Passaggio 5: Copiare le macro VBA dal modello
Successivamente, copieremo le macro VBA, inclusi i moduli UserForm Designer, nella nostra nuova cartella di lavoro:
```csharp
// Copiare il modulo utente di VBA-Macro Designer dal modello alla destinazione
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Copia il codice del modulo ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Copia il codice e i dati di altri moduli
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Ottieni i dati del modulo utente, ad esempio l'archiviazione del progettista
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Aggiungere l'archiviazione del progettista al progetto VBA di destinazione
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Questo pezzo di codice pesante gestisce il controllo di ogni modulo VBA nel file template. Stiamo copiando il design UserForm e i codici associati. È come assicurarsi di ottenere non solo la famosa ricetta della torta della nonna, ma anche le sue esatte tecniche di cottura!
## Passaggio 6: salvare la cartella di lavoro di destinazione
Dopo aver realizzato tutte le nostre copie, è il momento di salvare il nostro duro lavoro:
```csharp
// Salvare la cartella di lavoro di destinazione
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Assicurati di modificare il nome del file di output come necessario. Una volta salvato, stai effettivamente creando la tua versione personalizzata della cartella di lavoro, piena di macro e form utente. Quanto è eccitante?
## Passaggio 7: conferma il successo
Infine, stampiamo un messaggio di successo sulla console:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Questa piccola riga ti rassicura che il tuo processo è andato liscio. È la ciliegina sulla torta del tuo coding sundae!
## Conclusione
Congratulazioni! Hai completato la guida passo passo per copiare un VBA Macro User Form Designer da una cartella di lavoro a un'altra usando Aspose.Cells per .NET. All'inizio potrebbe sembrare un po' complicato, ma con la pratica, gestirai le manipolazioni delle cartelle di lavoro come un professionista. Ricorda, la codifica è tutta una questione di pratica, quindi non esitare a provare cose diverse nei tuoi file Excel. Se hai domande o riscontri problemi, sentiti libero di consultare i forum o la documentazione di Aspose per ricevere supporto!
## Domande frequenti
### Quali versioni di Excel sono supportate da Aspose.Cells?
Aspose.Cells supporta un'ampia gamma di formati Excel, tra cui XLSX, XLSM, CSV e altri.
### Posso usare Aspose.Cells gratuitamente?
 Sì! Puoi iniziare con una prova gratuita, che ti consente di valutare la libreria:[Prova gratuita](https://releases.aspose.com/).
### Ho bisogno di Visual Studio per eseguire questo codice?
Sebbene sia altamente consigliato per le sue funzionalità intuitive, qualsiasi IDE C# andrà bene, purché supporti lo sviluppo .NET.
### Dove posso trovare altri esempi e documentazione?
 Puoi esplorare il[Documentazione Aspose.Cells](https://reference.aspose.com/cells/net/) per ulteriori esempi e spiegazioni approfondite.
### Come posso risolvere i problemi durante l'utilizzo di Aspose.Cells?
 Dovresti visitare il[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9) per ricevere aiuto dalla comunità e dal personale di supporto di Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
