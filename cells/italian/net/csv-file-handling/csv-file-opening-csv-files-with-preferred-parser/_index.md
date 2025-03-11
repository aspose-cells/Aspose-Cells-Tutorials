---
title: Apertura di file CSV con il parser preferito
linktitle: Apertura di file CSV con il parser preferito
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come aprire e analizzare file CSV con parser personalizzati in Aspose.Cells per .NET. Gestisci testo e date senza sforzo. Perfetto per gli sviluppatori.
weight: 11
url: /it/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apertura di file CSV con il parser preferito

## Introduzione
Quando si gestiscono file CSV, a volte si desidera gestire diversi tipi di dati con parser personalizzati. Questo tutorial ti guiderà su come aprire file CSV con un parser preferito utilizzando Aspose.Cells per .NET. Che tu voglia gestire testo, date o altri formati personalizzati, questa guida ti guiderà attraverso ogni passaggio con una spiegazione chiara.
## Prerequisiti
Prima di immergerci nel codice, vediamo gli elementi essenziali di cui hai bisogno per iniziare.
1.  Aspose.Cells per la libreria .NET: assicurati di avere la libreria Aspose.Cells installata. Puoi scaricarla[Qui](https://releases.aspose.com/cells/net/) Puoi anche utilizzare la prova gratuita[Qui](https://releases.aspose.com/).
2. Ambiente di sviluppo .NET: si consiglia Visual Studio, ma funzionerà qualsiasi IDE compatibile con .NET.
3. Conoscenza di base di C#: questo tutorial presuppone che tu abbia familiarità con C# e con la programmazione orientata agli oggetti.
## Importa pacchetti
Per utilizzare Aspose.Cells, è necessario importare gli spazi dei nomi necessari nella parte superiore del file C#:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Ora che abbiamo impostato la scena, vediamo come aprire un file CSV con un parser preferito, gestendo diversi formati di dati come testo e date.
## Passaggio 1: definire parser personalizzati
 Per gestire diversi tipi di dati, come testo o formati di data specifici, è necessario definire parser personalizzati. In Aspose.Cells, i parser personalizzati implementano`ICustomParser` interfaccia.
### 1.1 Creare un parser di testo
Questo parser gestisce valori di testo regolari. Non modifica il formato, quindi il valore viene restituito così com'è.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 IL`ParseObject` restituisce semplicemente il valore di input. È come dire, "Non cambiare niente, dammi solo il testo!"
### 1.2 Creare un parser di date
 Per le date, dovrai assicurarti che i dati CSV siano analizzati correttamente in`DateTime` oggetti. Ecco come puoi creare un parser di date:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 In questo parser, utilizziamo`ParseExact` per garantire che la data venga interpretata correttamente in base a un formato predefinito (`"dd/MM/yyyy"`). In questo modo, qualsiasi data nel tuo CSV che segue questo formato verrà elaborata senza problemi.
## Passaggio 2: configurare le opzioni di caricamento
 Successivamente, devi configurare il modo in cui viene caricato il file CSV. Questo viene fatto utilizzando`TxtLoadOptions` classe, che consente di specificare opzioni di analisi, tra cui la codifica e i parser personalizzati.
### 2.1 Imposta le opzioni di carico
 Inizieremo inizializzando il`TxtLoadOptions` e definendo parametri chiave come il separatore e la codifica:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Separatore: definisce il carattere utilizzato per separare i valori nel file CSV (in questo caso, virgole).
- Codifica: utilizziamo la codifica UTF-8 per gestire un'ampia gamma di caratteri.
-  ConvertDateTimeData: impostando questa opzione su true si garantisce che i valori della data vengano automaticamente convertiti in`DateTime` oggetti quando possibile.
### 2.2 Applicare parser personalizzati
Successivamente assegneremo i parser creati in precedenza per gestire i valori nel CSV:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Questo dice ad Aspose.Cells di usare il`TextParser` per valori di testo generali e`DateParser`per tutti i campi data riscontrati nel file CSV.
## Passaggio 3: caricare e leggere il file CSV
 Ora che le opzioni di caricamento sono configurate, puoi caricare il file CSV in un`Aspose.Cells.Workbook` oggetto.
### 3.1 Caricare il file CSV
 Carichiamo il file CSV passando il percorso del file e il configurato`TxtLoadOptions` al`Workbook` costruttore:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Questo passaggio converte i dati CSV in una cartella di lavoro Excel completamente funzionale, in cui ogni valore viene analizzato in base alle regole preferite.
## Passaggio 4: accesso e visualizzazione dei dati delle celle
Una volta caricato il CSV nella cartella di lavoro, puoi iniziare a lavorare con i dati. Ad esempio, potresti voler stampare il tipo e il valore di celle specifiche.
### 4.1 Recupera e visualizza la cella A1
Recuperiamo la prima cella (A1) e visualizziamone il valore e il tipo:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Qui, il`Type` la proprietà mostra il tipo di dati (ad esempio`String` O`DateTime` ), E`DisplayStringValue` fornisce il valore formattato.
### 4.2 Recupera e visualizza la cella B1
Allo stesso modo, possiamo recuperare e visualizzare un'altra cella, ad esempio B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Questo processo può essere ripetuto per tutte le celle che si desidera ispezionare.
## Passaggio 5: salvare la cartella di lavoro
 Dopo aver lavorato con i dati, potresti voler salvare la cartella di lavoro in un nuovo file. Aspose.Cells semplifica questa operazione con un semplice`Save` metodo:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
In questo modo la cartella di lavoro viene salvata come file Excel, mantenendo tutta la formattazione e l'analisi dei dati applicate.
## Conclusione
L'apertura di file CSV con un parser preferito in Aspose.Cells per .NET è un modo flessibile e potente per gestire diversi tipi di dati. Creando parser personalizzati e configurando le opzioni di caricamento, puoi assicurarti che i tuoi file CSV vengano analizzati esattamente come ti servono, che tu stia gestendo testo, date o altri formati personalizzati. Con questo tutorial, ora sei equipaggiato per gestire scenari di analisi dei dati più complessi nei tuoi progetti.
## Domande frequenti
### Qual è lo scopo dei parser personalizzati in Aspose.Cells per .NET?
I parser personalizzati consentono di definire come determinati tipi di dati, ad esempio testo o date, debbano essere analizzati durante il caricamento di un file CSV.
### Posso usare un carattere separatore diverso nel file CSV?
 Sì, puoi specificare qualsiasi carattere come separatore nel`TxtLoadOptions.Separator` proprietà.
### Come gestisco la codifica in Aspose.Cells quando carico un CSV?
 Puoi impostare il`Encoding` proprietà di`TxtLoadOptions` a qualsiasi schema di codifica come UTF-8, ASCII, ecc.
### Cosa succede se il formato della data nel CSV è diverso?
È possibile definire il formato di data specifico utilizzando un parser personalizzato, assicurando la corretta analisi dei valori di data.
### Posso salvare la cartella di lavoro in altri formati?
Sì, Aspose.Cells consente di salvare la cartella di lavoro in vari formati, come XLSX, CSV, PDF e altri.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
