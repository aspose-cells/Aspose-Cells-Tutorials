---
title: Utilizzare ICellsDataTableDataSource per Workbook Designer
linktitle: Utilizzare ICellsDataTableDataSource per Workbook Designer
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Impara a usare ICellsDataTableDataSource con Aspose.Cells per .NET per popolare dinamicamente i fogli Excel. Perfetto per automatizzare i dati dei clienti nelle cartelle di lavoro.
weight: 21
url: /it/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utilizzare ICellsDataTableDataSource per Workbook Designer

## Introduzione
 Creare fogli di calcolo avanzati con integrazione dati automatizzata può essere un punto di svolta, specialmente nelle applicazioni aziendali. In questo tutorial, approfondiremo come utilizzare`ICellsDataTableDataSource`per un progettista di cartelle di lavoro in Aspose.Cells per .NET. Ti guideremo nella creazione di una soluzione semplice e leggibile per caricare dati personalizzati in un file Excel in modo dinamico. Quindi, se lavori con elenchi di clienti, dati di vendita o simili, questa guida è per te!
## Prerequisiti
Per iniziare, assicurati di avere quanto segue:
-  Aspose.Cells per la libreria .NET – Puoi scaricarla da[Qui](https://releases.aspose.com/cells/net/) oppure ottieni una versione di prova gratuita.
- Ambiente di sviluppo .NET: Visual Studio è un'ottima scelta.
- Nozioni di base di C#: la familiarità con le classi e la gestione dei dati ti aiuterà a seguire il corso.
Prima di procedere, assicurati che il tuo ambiente di sviluppo sia configurato con i pacchetti necessari.
## Importa pacchetti
Per usare Aspose.Cells in modo efficace, devi importare pacchetti essenziali. Di seguito è riportato un rapido riferimento per i namespace richiesti:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Passaggio 1: definire una classe di dati del cliente
 Per iniziare, crea un semplice`Customer` classe. Questa classe conterrà i dettagli di base del cliente come`FullName` E`Address`Consideralo come un modo per definire la "forma" dei tuoi dati.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Passaggio 2: impostare la classe dell'elenco clienti
 Quindi, definisci un`CustomerList` classe che si estende`ArrayList` Questo elenco personalizzato conterrà istanze di`Customer` e consentire l'accesso indicizzato a ciascuna voce.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
In questa fase, inseriamo i nostri dati in un formato che Aspose.Cells può riconoscere ed elaborare.
## Passaggio 3: creare la classe di origine dati del cliente
 Ecco dove le cose si fanno interessanti. Creeremo un`CustomerDataSource` implementazione della classe`ICellsDataTable` per rendere i nostri dati compatibili con il progettista di cartelle di lavoro di Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 Questa usanza`CustomerDataSource` la classe consente ad Aspose.Cells di interpretare ogni`Customer` oggetto come riga nel file Excel.
## Passaggio 4: inizializzare i dati del cliente
Ora, aggiungiamo alcuni clienti alla nostra lista. Ecco dove carichiamo i dati da scrivere nella cartella di lavoro. Sentiti libero di aggiungere altre voci se necessario.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
In questo esempio, stiamo lavorando con un piccolo set di dati. Tuttavia, potresti facilmente espandere questo elenco caricando dati da un database o da altre fonti.
## Passaggio 5: caricare la cartella di lavoro
Ora, apriamo una cartella di lavoro Excel esistente che contiene gli Smart Marker necessari. Questa cartella di lavoro fungerà da modello e Aspose.Cells sostituirà dinamicamente gli Smart Marker con i dati del cliente.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Assicurare che`"SmartMarker1.xlsx"` contiene segnaposto come`&=Customer.FullName` E`&=Customer.Address` dove i dati devono essere compilati.
## Passaggio 6: impostare Workbook Designer
Ora configuriamo il progettista della cartella di lavoro per collegare la fonte dati del cliente con gli Smart Marker della cartella di lavoro.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 IL`SetDataSource` il metodo lega il nostro`CustomerDataSource` agli Smart Marker nella cartella di lavoro. Ogni marcatore etichettato`&=Customer` in Excel verranno ora sostituiti dai dati corrispondenti del cliente.
## Passaggio 7: elaborare e salvare la cartella di lavoro
Infine, elaboriamo la cartella di lavoro per compilare i dati e salvare i risultati.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Questo codice attiva l'elaborazione Smart Marker, sostituisce tutti i segnaposto con i dati e salva il risultato come`dest.xlsx`.
## Conclusione
 Congratulazioni! Hai implementato con successo`ICellsDataTableDataSource` per un progettista di cartelle di lavoro che usa Aspose.Cells per .NET. Questo approccio è ideale per automatizzare la compilazione dei dati nei fogli di calcolo, specialmente quando si ha a che fare con dati dinamici come elenchi di clienti o inventari di prodotti. Con queste competenze, sei sulla buona strada per creare applicazioni basate sui dati che rendono la creazione di report basati su Excel un gioco da ragazzi!
## Domande frequenti
###  Cosa è`ICellsDataTable` in Aspose.Cells?  
Si tratta di un'interfaccia che consente di collegare origini dati personalizzate con gli Smart Marker di Aspose.Cells per il popolamento dinamico dei dati.
### Come posso personalizzare i dati nel modello della cartella di lavoro?  
 Segnaposto denominati marcatori intelligenti, come`&=Customer.FullName`, vengono utilizzati. Questi marcatori vengono sostituiti con dati reali durante l'elaborazione.
### Aspose.Cells per .NET è gratuito?  
 Aspose.Cells offre una prova gratuita, ma l'accesso completo richiede una licenza a pagamento. Controlla il loro[prova gratuita](https://releases.aspose.com/) O[acquistare](https://purchase.aspose.com/buy) opzioni.
### Posso aggiungere altri dati sui clienti in modo dinamico?  
 Assolutamente! Basta popolare il`CustomerList`con voci aggiuntive prima di eseguire il programma.
### Dove posso trovare aiuto se sono bloccato?  
 Aspose ha un[forum di supporto](https://forum.aspose.com/c/cells/9) dove gli utenti possono porre domande e ricevere assistenza dalla community e dal team Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
