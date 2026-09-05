---
category: general
date: 2026-09-05
description: Impara come copiare un intervallo in Excel, esportare Excel in PowerPoint
  e convertire Excel in pptx con un esempio Java completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: it
lastmod: 2026-09-05
og_description: Come copiare un intervallo ed esportare Excel in PowerPoint usando
  Java. Segui questa guida passo‑passo per convertire Excel in PPTX in modo efficiente.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Come copiare un intervallo da Excel ed esportarlo in PowerPoint con Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Come copiare un intervallo da Excel ed esportarlo in PowerPoint usando Java
url: /it/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare un intervallo da Excel ed esportarlo in PowerPoint usando Java

Se hai bisogno di **how to copy range** da una cartella di lavoro Excel e poi **export excel to PowerPoint**, questa guida ti fornisce una soluzione completa, pronta all'uso. Vedrai esattamente come copiare un intervallo contenente una tabella pivot, creare un nuovo foglio di lavoro per la copia e, infine, **convert Excel to PPTX** con una singola chiamata di metodo.

Copiare intervalli ed esportare cartelle di lavoro è una necessità comune quando generi report, presentazioni o dashboard in modo programmatico. Alla fine di questo tutorial avrai un programma Java che:

* Carica un file `.xlsx` esistente.
* Copia l'intervallo `A1:H20` (inclusa una tabella pivot) in un nuovo foglio.
* Salva la cartella di lavoro come una presentazione `.pptx` modificabile.

Hai bisogno solo della libreria Aspose.Cells for Java; non sono richieste dipendenze aggiuntive.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java 17 (o versioni successive) installato.
* Maven o Gradle per gestire le dipendenze.
* Aspose.Cells for Java 23.9 (o l'ultima versione) – aggiungila al tuo progetto come mostrato nello snippet Maven qui sotto.
* Un file Excel (`input.xlsx`) che contiene i dati e una tabella pivot che desideri copiare.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Passo 1: Caricare la cartella di lavoro da un file

La prima operazione in **how to copy range** è aprire la cartella di lavoro di origine. Questo ti dà accesso a fogli, celle e tabelle pivot.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Perché questo passo?*  
Il caricamento del file crea una rappresentazione in memoria del documento Excel, consentendoti di manipolarne il contenuto senza toccare il file originale.

## Passo 2: Ottenere il foglio di lavoro di origine che contiene i dati

Tipicamente il primo foglio contiene i dati che vuoi copiare. Puoi recuperarlo per indice.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Se la tua cartella di lavoro memorizza la tabella pivot in un foglio diverso, sostituisci `0` con l'indice appropriato o usa `get("SheetName")`.

## Passo 3: Aggiungere un nuovo foglio di lavoro per l'intervallo copiato

Creare un foglio di destinazione isola i dati copiati e rende l'esportazione successiva più pulita.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Puoi dare al foglio qualsiasi nome; il nome “Copy” segnala chiaramente che contiene l'intervallo duplicato.

## Passo 4: Copiare l'intervallo (how to copy range) includendo la tabella pivot

Ora eseguiamo l'operazione principale di **how to copy range**. Il metodo `copyRange` copia sia i valori sia la formattazione, e preserva la definizione della tabella pivot.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Perché usare `CopyOptions`?*  
Fornire un'istanza di `CopyOptions` ti permette di affinare cosa viene copiato (ad es., formule, larghezze delle colonne). Il costruttore predefinito copia tutto, il che è ideale quando vuoi una replica esatta di una **copy pivot table sheet**.

## Passo 5: Preparare le opzioni per esportare la cartella di lavoro come presentazione PowerPoint modificabile

L'esportazione in PowerPoint avviene tramite `ImageOrPrintOptions`. Impostare il formato di salvataggio su `SaveFormat.PPTX` indica ad Aspose.Cells di generare un file PowerPoint anziché un'immagine.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Puoi anche regolare le dimensioni della diapositiva, DPI e altre impostazioni della presentazione tramite `pptOptions` se ti serve un layout personalizzato.

## Passo 6: Salvare la cartella di lavoro come file PPTX (convert excel to pptx)

Infine, invoca `workbook.save` con le opzioni PPTX. Questo passo **how to export excel** in una presentazione diapositive.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Al termine dell'esecuzione, `output.pptx` conterrà una singola diapositiva in cui l'intervallo copiato appare esattamente come in Excel, inclusi i controlli della tabella pivot.

### Output previsto

Apri `output.pptx` in Microsoft PowerPoint o in qualsiasi visualizzatore compatibile. Dovresti vedere una diapositiva con l'intervallo `A1:H20` visualizzato, preservando colori delle celle, bordi e layout della tabella pivot. La diapositiva è completamente modificabile — puoi spostare, ridimensionare o formattare la tabella proprio come qualsiasi contenuto nativo di PowerPoint.

## Esempio completo eseguibile

Mettere insieme tutti i passaggi ti fornisce una classe Java autonoma:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Esegui la classe dal tuo IDE o dalla riga di comando:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Vedrai il messaggio di conferma una volta che il file è stato scritto.

## Domande frequenti e casi particolari

| Domanda | Risposta |
|----------|--------|
| **Posso copiare un intervallo non contiguo?** | Usa `copyRange` con un intervallo denominato che includa più aree, oppure chiama `copyRange` più volte per ciascun blocco. |
| **Cosa succede se il foglio di origine contiene più tabelle pivot?** | Ogni tabella pivot all'interno del rettangolo copiato viene trasferita. Per le tabelle al di fuori del rettangolo, copiale separatamente. |
| **Come esportare più fogli come diapositive separate?** | Itera sui fogli di lavoro, copia ciascuno in un foglio temporaneo e chiama `workbook.save` con `pptOptions` per ogni iterazione, aggiungendo al medesimo PPTX tramite l'API `Presentation`. |
| **Il PPTX generato è modificabile?** | Sì. L'esportazione crea oggetti PowerPoint nativi, quindi puoi modificare testo, ridimensionare tabelle o aggiungere animazioni in seguito. |
| **E per le cartelle di lavoro di grandi dimensioni?** | Aumenta `pptOptions.setDpi(300)` per una fedeltà maggiore, ma tieni presente l'uso di memoria; elabora i fogli in batch se necessario. |

## Consigli professionali

* **Preserva le larghezze delle colonne** – imposta `CopyOptions.setColumnWidth(true)` prima di copiare se ti serve una corrispondenza esatta delle larghezze.
* **Usa una dimensione diapositiva personalizzata** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` per corrispondere a una presentazione 16:9.
* **Aggiungi una diapositiva titolo** – dopo l'esportazione, apri il PPTX con Aspose.Slides e inserisci una diapositiva con titolo e data.

## Conclusione

Ora sai **how to copy range** da una cartella di lavoro Excel, **export excel to PowerPoint**, e **convert excel to pptx** usando Java. Seguendo i sei passaggi sopra potrai automatizzare la generazione di report, creare presentazioni da dati live e mantenere intatta la funzionalità delle tabelle pivot.

### Cosa fare dopo?

* Esplora le varianti di **copy pivot table sheet** come la copia solo della cache pivot.
* Combina questo flusso di lavoro con **Aspose.Slides** per aggiungere animazioni o branding personalizzati.
* Automatizza l'elaborazione batch per decine di cartelle di lavoro in un job pianificato.

Sentiti libero di sperimentare con le opzioni e adattare il codice al tuo pipeline di reporting. Se incontri problemi, la documentazione di Aspose.Cells for Java fornisce approfondimenti su `CopyOptions` e `ImageOrPrintOptions`. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}