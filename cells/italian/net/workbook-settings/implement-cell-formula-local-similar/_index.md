---
"description": "Scopri come implementare una formula di cella simile alla funzionalità locale della formula di intervallo in Aspose.Cells per .NET. Impara a personalizzare i nomi delle funzioni predefinite di Excel e altro ancora."
"linktitle": "Implementa la formula locale della cella simile alla formula locale dell'intervallo"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Implementa la formula locale della cella simile alla formula locale dell'intervallo"
"url": "/it/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementa la formula locale della cella simile alla formula locale dell'intervallo

## Introduzione
Aspose.Cells per .NET è un'API potente e flessibile per la manipolazione di fogli di calcolo che consente di creare, manipolare e convertire file Excel a livello di codice. Una delle numerose funzionalità offerte da Aspose.Cells è la possibilità di personalizzare il comportamento delle funzioni Excel integrate, inclusa la possibilità di creare nomi di funzioni locali personalizzati. In questo tutorial, vi guideremo attraverso i passaggi per implementare una formula di cella simile alla funzionalità locale della formula di intervallo in Aspose.Cells per .NET.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1. Microsoft Visual Studio 2010 o versione successiva installato nel sistema.
2. L'ultima versione della libreria Aspose.Cells per .NET installata nel progetto. È possibile scaricare la libreria da [Pagina di download di Aspose.Cells per .NET](https://releases.aspose.com/cells/net/).
## Importa pacchetti
Per iniziare, dovrai importare i pacchetti necessari nel tuo progetto C#. Aggiungi le seguenti istruzioni using all'inizio del file di codice:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Passaggio 1: creare una classe di impostazioni di globalizzazione personalizzata
Il primo passo è creare un'immagine personalizzata `GlobalizationSettings` classe che ti permetterà di sovrascrivere il comportamento predefinito delle funzioni di Excel. In questo esempio, cambieremo i nomi delle `SUM` E `AVERAGE` funzioni a `UserFormulaLocal_SUM` E `UserFormulaLocal_AVERAGE`, rispettivamente.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Modifica il nome della funzione SOMMA in base alle tue esigenze.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Modifica il nome della funzione MEDIA in base alle tue esigenze.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Passaggio 2: creare una nuova cartella di lavoro e assegnare le impostazioni di globalizzazione personalizzate
Successivamente, crea una nuova istanza della cartella di lavoro e assegna la personalizzazione `GlobalizationSettings` classe di implementazione della cartella di lavoro `Settings.GlobalizationSettings` proprietà.
```csharp
//Crea cartella di lavoro
Workbook wb = new Workbook();
//Assegna la classe di implementazione GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Passaggio 3: accedi al primo foglio di lavoro e a una cella
Ora accediamo al primo foglio di lavoro della cartella di lavoro e a una cella specifica al suo interno.
```csharp
//Accedi al primo foglio di lavoro
Worksheet ws = wb.Worksheets[0];
//Accedi ad alcune celle
Cell cell = ws.Cells["C4"];
```
## Passaggio 4: assegnare le formule e stampare il file FormulaLocal
Infine, assegniamo il `SUM` E `AVERAGE` formule nella cella e stampare il risultato `FormulaLocal` valori.
```csharp
//Assegna la formula SUM e stampa la sua FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Assegna la formula MEDIA e stampa la sua FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusione
In questo tutorial, hai imparato come implementare una formula di cella simile alla funzionalità locale della formula di intervallo in Aspose.Cells per .NET. Creando una formula personalizzata `GlobalizationSettings` classe, è possibile ignorare il comportamento predefinito delle funzioni di Excel e personalizzare i nomi delle funzioni locali in base alle proprie esigenze. Questo può essere particolarmente utile quando si lavora con documenti Excel localizzati o internazionalizzati.
## Domande frequenti
### Qual è lo scopo del `GlobalizationSettings` classe in Aspose.Cells?
IL `GlobalizationSettings` La classe in Aspose.Cells consente di personalizzare il comportamento delle funzioni Excel integrate, inclusa la possibilità di modificare i nomi delle funzioni locali.
### Posso sovrascrivere il comportamento di funzioni diverse da `SUM` E `AVERAGE`?
Sì, puoi sovrascrivere il comportamento di qualsiasi funzione Excel integrata modificando `GetLocalFunctionName` metodo nella tua personalizzazione `GlobalizationSettings` classe.
### Esiste un modo per ripristinare i valori predefiniti dei nomi delle funzioni?
Sì, puoi reimpostare i nomi delle funzioni rimuovendo quelli personalizzati `GlobalizationSettings` classe o restituendo una stringa vuota dalla `GetLocalFunctionName` metodo.
### Posso usare questa funzionalità per creare funzioni personalizzate in Aspose.Cells?
No, il `GlobalizationSettings` La classe è progettata per sovrascrivere il comportamento delle funzioni predefinite di Excel, non per creare funzioni personalizzate. Se è necessario creare funzioni personalizzate, è possibile utilizzare `UserDefinedFunction` classe in Aspose.Cells.
### Questa funzionalità è disponibile in tutte le versioni di Aspose.Cells per .NET?
Sì, il `GlobalizationSettings` classe e la possibilità di personalizzare i nomi delle funzioni è disponibile in tutte le versioni di Aspose.Cells per .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}