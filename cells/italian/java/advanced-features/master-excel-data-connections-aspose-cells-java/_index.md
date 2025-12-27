---
date: '2025-12-27'
description: Scopri come modificare la fonte dei dati di Excel programmaticamente
  usando Aspose.Cells per Java, modifica le connessioni dei dati di Excel e automatizza
  il tuo flusso di lavoro.
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: Come modificare la sorgente dati di Excel con Aspose.Cells per Java
url: /it/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifica la sorgente dati di Excel usando Aspose.Cells per Java

## Introduzione
Hai difficoltà a **cambiare la sorgente dati di Excel** e a modificare le connessioni dati all'interno dei file Excel in modo programmatico? Questa guida completa è pensata per gli sviluppatori che desiderano automatizzare i loro flussi di reporting con la potente libreria **Aspose.Cells for Java**. Ti guideremo attraverso il caricamento di una cartella di lavoro Excel, l'aggiornamento della sua connessione esterna e il salvataggio delle modifiche, tutto usando codice Java.

### Cosa imparerai
- Come configurare Aspose.Cells per Java in Maven o Gradle.  
- **Load Excel workbook Java** – leggi un file esistente in memoria.  
- **Modify Excel data connections** – aggiorna il nome della connessione, il percorso ODC e il comando SQL.  
- **Save Excel workbook Java** – scrivi la cartella di lavoro aggiornata su disco.  

Assicuriamoci di avere tutto il necessario prima di immergerci.

## Risposte rapide
- **Qual è la libreria principale?** Aspose.Cells for Java.  
- **Quale metodo carica una cartella di lavoro?** `new Workbook(filePath)`.  
- **Come aggiorno la stringa di connessione?** Usa `DBConnection.setConnectionInfo(...)`.  
- **Posso cambiare il percorso del file ODC?** Sì, tramite `ExternalConnection.setOdcFile(...)`.  
- **Ho bisogno di una licenza per la produzione?** Una licenza commerciale rimuove i limiti di valutazione.

## Prerequisiti
Prima di iniziare, verifica di avere quanto segue:

### Librerie richieste
Aspose.Cells for Java versione 25.3 o successiva fornisce le API utilizzate in questo tutorial.

### Configurazione dell'ambiente
- Java Development Kit (JDK) installato.  
- Un IDE come IntelliJ IDEA, Eclipse o NetBeans.

### Prerequisiti di conoscenza
La familiarità con Java, Maven o Gradle e i concetti di base di SQL ti aiuterà a seguire senza problemi.

## Configurazione di Aspose.Cells per Java
Per iniziare a usare Aspose.Cells, aggiungi la libreria al tuo progetto:

**Configurazione Maven**  
Aggiungi la dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Configurazione Gradle**  
Inserisci la seguente riga in `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Passaggi per l'acquisizione della licenza
Aspose.Cells offre una prova gratuita così puoi valutare la libreria prima di acquistare:

- Visita la [pagina della prova gratuita](https://releases.aspose.com/cells/java/) e scarica il pacchetto di valutazione.  
- Per l'uso a piena funzionalità, acquista una licenza dal [portale di acquisto](https://purchase.aspose.com/buy).  
- Hai bisogno di accesso temporaneo? Richiedi una [licenza temporanea](https://purchase.aspose.com/temporary-license/).

Una volta che la libreria è referenziata e licenziata, sei pronto a scrivere codice.

## Guida all'implementazione

### Funzionalità 1: Carica la cartella di lavoro da file
**Cosa fa questo passaggio?** Dimostra come **load Excel workbook Java** così puoi lavorare con le sue connessioni dati.

#### Istruzioni passo‑a‑passo
**Definisci la tua directory dei dati** – indica al programma dove si trova il file sorgente:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
Assicurati che `DataConnection.xlsx` esista in quella cartella.

**Carica la cartella di lavoro** – istanzia l'oggetto `Workbook`:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
L'istanza `Workbook` ora rappresenta il tuo file Excel in memoria.

### Funzionalità 2: Modifica la connessione dati nella cartella di lavoro
**Perché modificare?** Aggiornare la connessione esterna ti consente di **change Excel data source** senza aprire manualmente il file.

#### Istruzioni passo‑a‑passo
**Accedi alla connessione dati** – recupera la prima connessione (puoi iterare per più connessioni):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` restituisce una collezione di tutte le connessioni, consentendoti di **modify excel data connections** individualmente.

**Modifica le proprietà della connessione** – cambia nome, file ODC, tipo di comando e istruzione SQL:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

Esegui il cast a `DBConnection` per impostazioni specifiche del database:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
Qui **update excel external connection** dettagli come la query SQL e la stringa di connessione.

### Funzionalità 3: Salva la cartella di lavoro su file
**Cosa succede dopo?** Dopo aver aggiornato la connessione, devi **save Excel workbook Java** affinché le modifiche persistano.

#### Istruzioni passo‑a‑passo
**Definisci la directory di output** – dove verrà scritto il file modificato:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Salva la cartella di lavoro** – scrivi la cartella di lavoro su disco:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
Il metodo `save()` finalizza l'operazione di **change excel data source**.

## Applicazioni pratiche
Modificare le connessioni dati di Excel programmaticamente apre molte porte:

1. **Reporting automatizzato** – genera report che estraggono sempre gli ultimi dati da un database.  
2. **Sincronizzazione dati** – mantieni le cartelle di lavoro sincronizzate con sistemi live senza aggiornamenti manuali.  
3. **Dashboard dinamici** – crea dashboard che riflettono metriche in tempo reale.

Integrare Aspose.Cells con piattaforme CRM, ERP o BI può ridurre drasticamente lo sforzo manuale.

## Considerazioni sulle prestazioni
Quando si lavora con cartelle di lavoro grandi o set di risultati massivi:

- Elabora i dati in batch per evitare picchi di memoria.  
- Ottimizza le tue query SQL per la velocità.  
- Rilascia le risorse tempestivamente; chiama `workbook.dispose()` se non ti serve più l'oggetto.

Queste pratiche garantiscono che la tua applicazione rimanga reattiva durante il **changing Excel data source**.

## Conclusione
Ora hai imparato come **change Excel data source** caricando una cartella di lavoro, **modify excel data connections**, e salvando il file aggiornato usando **Aspose.Cells for Java**. Questa capacità ti consente di automatizzare flussi di lavoro basati sui dati e mantenere i file Excel sincronizzati con sistemi esterni.

### Prossimi passi
- Sperimenta con più connessioni usando un ciclo su `workbook.getDataConnections()`.  
- Esplora altre funzionalità di Aspose.Cells come la generazione di grafici, lo styling delle celle e la manipolazione delle tabelle pivot.  

Pronto a potenziare la tua automazione? Implementa questi snippet oggi stesso e guarda la tua produttività decollare!

## Domande frequenti

**D1: Come gestisco più connessioni dati in una cartella di lavoro?**  
A1: Usa `workbook.getDataConnections().get(index)` all'interno di un ciclo per accedere a ciascuna connessione individualmente.

**D2: Posso modificare altre proprietà di un file Excel usando Aspose.Cells Java?**  
A2: Assolutamente! Aspose.Cells supporta la formattazione delle celle, la gestione dei fogli di lavoro, la creazione di grafici e molto altro.

**D3: Cosa succede se il mio comando SQL non riesce a essere eseguito?**  
A3: Verifica la stringa di connessione, controlla i permessi del database e rivedi i dettagli dell'eccezione per indizi.

**D4: Dove posso ottenere supporto per i problemi di Aspose.Cells?**  
A4: Visita il [forum di Aspose](https://forum.aspose.com/c/cells/9) per porre domande o consultare soluzioni esistenti.

**D5: Ci sono limitazioni nella versione di prova gratuita?**  
A5: La versione di valutazione aggiunge filigrane e può limitare la capacità di elaborazione. Acquista una licenza per un uso senza restrizioni.

## Risorse
- **Documentazione:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ultimo aggiornamento:** 2025-12-27  
**Testato con:** Aspose.Cells Java 25.3  
**Autore:** Aspose