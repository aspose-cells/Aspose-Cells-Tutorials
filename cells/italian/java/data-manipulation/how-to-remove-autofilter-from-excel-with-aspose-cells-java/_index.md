---
category: general
date: 2026-09-27
description: Scopri come rimuovere l'autofiltro da Excel usando Aspose.Cells per Java.
  Guida passo‑passo per cancellare l'autofiltro nella cartella di lavoro, rimuovere
  il filtro della tabella Excel e salvare il file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- remove excel table filter
- remove filter from excel table
- clear autofilter in workbook
language: it
lastmod: 2026-09-27
og_description: Rimuovi l'autofiltro da Excel usando Aspose.Cells per Java. Questo
  tutorial mostra come cancellare l'autofiltro nella cartella di lavoro, rimuovere
  il filtro della tabella Excel e salvare il file aggiornato.
og_image_alt: Screenshot of an Excel worksheet after remove autofilter from excel
  using Java
og_title: Rimuovere l'autofiltro da Excel con Aspose.Cells Java – guida completa
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to remove autofilter from Excel using Aspose.Cells for Java.
    Step‑by‑step guide to clear autofilter in workbook, remove excel table filter
    and save the file.
  headline: How to remove autofilter from Excel with Aspose.Cells Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- AutoFilter
title: Come rimuovere l'autofiltro da Excel con Aspose.Cells Java
url: /it/java/data-manipulation/how-to-remove-autofilter-from-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rimuovere l'autofiltro da Excel con Aspose.Cells Java

Se hai bisogno di rimuovere l'autofiltro da Excel, questa guida mostra i passaggi esatti da seguire con Aspose.Cells per Java. Vedrai come cancellare l'autofiltro in una cartella di lavoro, eliminare il filtro collegato a una tabella Excel e salvare il risultato senza perdere dati.

Lavorare con Excel in modo programmatico spesso significa gestire tabelle che contengono già dei filtri. Rimuovere tali filtri evita la nascondita accidentale dei dati quando in seguito si elabora la cartella di lavoro. Questo tutorial copre tutto ciò di cui hai bisogno: librerie richieste, spiegazione del codice, gestione dei casi limite e verifica del file finale.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java Development Kit 8 o versioni successive.
* Maven o Gradle per gestire le dipendenze (l'esempio utilizza Maven).
* Aspose.Cells for Java 23.8 o successive – è possibile ottenere una licenza temporanea gratuita dal sito web di Aspose.
* Un file di esempio (`TableWithFilter.xlsx`) che contiene una tabella con un AutoFilter applicato.

## Passo 1: Configurare il progetto Maven

Crea un file `pom.xml` (o aggiungilo al tuo progetto esistente) e includi la dipendenza Aspose.Cells:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExcelFilterRemoval</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.8</version>
        </dependency>
    </dependencies>
</project>
```

Aggiungere la dipendenza garantisce che le classi `com.aspose.cells.*` siano disponibili al momento della compilazione. Dopo aver salvato il file, esegui `mvn clean install` per scaricare la libreria.

## Passo 2: Caricare la cartella di lavoro che contiene una tabella filtrata

La prima riga di codice crea un'istanza `Workbook` che punta al file di origine. Caricare la cartella di lavoro in memoria è necessario prima di poter interagire con gli oggetti dei fogli di lavoro.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");
```

Se il file non esiste, Aspose.Cells genera una `FileNotFoundException`. Verifica il percorso e il nome del file prima di eseguire il programma.

## Passo 3: Accedere al foglio di lavoro che contiene la tabella

La maggior parte delle cartelle di lavoro ha un foglio predefinito all'indice 0. È anche possibile recuperare un foglio per nome se la cartella di lavoro contiene più fogli.

```java
        // Access the first worksheet (where the table resides)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Ottenere il foglio corretto è essenziale perché `removeAutoFilter` opera su un `ListObject` (la tabella) che vive all'interno di un foglio specifico.

## Passo 4: Individuare il ListObject (tabella Excel) e rimuovere il suo filtro

Un `ListObject` rappresenta una tabella Excel. Il metodo `removeAutoFilter` elimina l'elemento UI AutoFilter collegato a quella tabella. Se la tabella non ha filtri, il metodo non fa nulla, rendendolo sicuro per esecuzioni ripetute.

```java
        // Retrieve the first ListObject (table) from the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Remove the AutoFilter element from the table
        table.removeAutoFilter();
```

**Perché questo passaggio è importante:**  
* `removeAutoFilter` elimina le frecce del filtro e tutte le righe nascoste causate dal filtro.  
* I dati sottostanti rimangono invariati, quindi è ancora possibile leggere o modificare le righe programmaticamente.  
* Se in seguito è necessario riapplicare un filtro, è possibile chiamare nuovamente `table.setAutoFilter()`.

### Gestione di più tabelle

Se il foglio contiene più di una tabella, itera attraverso la collezione:

```java
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }
```

Questo ciclo garantisce che **rimuovere il filtro della tabella Excel** venga applicato a ogni tabella, evitando righe nascoste in cartelle di lavoro più grandi.

## Passo 5: Salvare la cartella di lavoro senza l'AutoFilter

Dopo aver cancellato il filtro, scrivi la cartella di lavoro in un nuovo file. Il metodo `save` supporta molti formati; l'esempio salva come file `.xlsx`.

```java
        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

Il salvataggio crea una copia pulita (`TableNoFilter.xlsx`) che non mostra più le frecce del filtro. Apri il file in Excel per confermare che **rimuovere il filtro dalla tabella Excel** sia stato eseguito correttamente.

## Esempio completo e eseguibile

Unendo tutti i passaggi ottieni un programma autonomo che puoi compilare ed eseguire:

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook containing a filtered table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // 2. Get the first worksheet (adjust index if needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Remove AutoFilter from each table on the sheet
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }

        // 4. Save the workbook – the AutoFilter is now cleared
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

**Output previsto:**  
Quando apri `TableNoFilter.xlsx` in Microsoft Excel, le frecce a discesa del filtro sono scomparse e tutte le righe sono visibili. Nessun dato è stato perso e la cartella di lavoro si comporta esattamente come un file che non ha mai avuto un AutoFilter.

## Domande comuni e gestione dei casi limite

| Domanda | Risposta |
|----------|--------|
| *E se la cartella di lavoro non contiene tabelle?* | La chiamata `getListObjects().getCount()` restituisce 0, quindi il ciclo termina senza errori. |
| *Posso rimuovere il filtro solo da una colonna specifica?* | Aspose.Cells non espone la rimozione a livello di colonna; è necessario cancellare l'intero AutoFilter della tabella. |
| *`removeAutoFilter` influisce sulla formattazione condizionale?* | No. La formattazione condizionale rimane intatta perché il metodo tocca solo l'interfaccia del filtro. |
| *L'operazione è veloce per cartelle di lavoro di grandi dimensioni?* | Sì. Rimuovere il filtro è un'operazione O(1) per tabella; il costo dominante è il caricamento e il salvataggio della cartella di lavoro. |
| *È necessaria una licenza per l'uso in produzione?* | Una licenza valida di Aspose.Cells rimuove le filigrane di valutazione e abilita le prestazioni complete. |

## Consigli professionali

* **License early** – chiama `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` prima di caricare la cartella di lavoro per evitare il banner di valutazione.
* **Batch processing** – quando elabori decine di file, riutilizza una singola istanza `Workbook` caricando, cancellando, salvando e poi chiamando `workbook.dispose();` per liberare memoria.
* **Verification script** – dopo il salvataggio, puoi confermare programmaticamente che il filtro sia stato rimosso:

```java
Workbook check = new Workbook("YOUR_DIRECTORY/TableNoFilter.xlsx");
boolean hasFilter = check.getWorksheets().get(0).getListObjects().get(0).isAutoFilterEnabled();
System.out.println("Filter present? " + hasFilter); // should print false
```

## Conclusione

Ora sai come **remove autofilter from Excel** usando Aspose.Cells per Java, come **remove excel table filter** per ogni tabella in un foglio di lavoro, e come **clear autofilter in workbook** prima di salvare il file. L'esempio di codice completo dimostra un modello affidabile da integrare in pipeline di automazione più ampie, strumenti di migrazione dati o servizi di reporting.

I prossimi passi che potresti esplorare includono:

* Aggiungere la convalida dei dati dopo che il filtro è stato rimosso.
* Esportare la cartella di lavoro pulita in CSV o PDF.
* Utilizzare Aspose.Cells per applicare programmaticamente un nuovo filtro basato su regole di business.

Sentiti libero di sperimentare con strutture di cartelle di lavoro diverse e condividere i tuoi risultati nei commenti. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Cancella l'interfaccia del filtro in Excel con C# – Rimuovi il pulsante AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Implementa l'Autofiltro 'Ends With' in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)
- [Implementa AutoFilter 'Begins With' in Excel usando Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}