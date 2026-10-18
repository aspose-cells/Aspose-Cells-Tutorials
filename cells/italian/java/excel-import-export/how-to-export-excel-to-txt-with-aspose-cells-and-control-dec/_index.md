---
category: general
date: 2026-08-20
description: Impara a esportare Excel in TXT limitando le cifre decimali, mantenendo
  le cifre significative e salvando la cartella di lavoro come TXT usando Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: it
lastmod: 2026-08-20
og_description: Esporta Excel in TXT con Aspose.Cells. Questa guida mostra come limitare
  le cifre decimali, mantenere le cifre significative e salvare la cartella di lavoro
  come TXT in Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Esporta Excel in TXT in Java – controlla i decimali e le cifre significative
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Come esportare Excel in TXT con Aspose.Cells e controllare la precisione decimale
url: /it/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel in TXT con Aspose.Cells e controllare la precisione decimale

Se hai bisogno di **esportare Excel in TXT** e garantire che l'output rispetti un numero specifico di cifre decimali, questa guida fornisce una soluzione completa. Vedrai come limitare le cifre decimali, mantenere le cifre significative e **salvare la cartella di lavoro come TXT** usando la libreria Aspose.Cells per Java.

Il tutorial mostra come creare una cartella di lavoro, inserire un valore ad alta precisione, configurare le opzioni di salvataggio TXT e scrivere il file su disco. Alla fine potrai generare un file di testo che contiene esattamente la precisione richiesta, senza elaborazione manuale post‑processo.

## Cosa ti serve

- Java 17 (o qualsiasi JDK supportato)
- Aspose.Cells per Java 23.10 o versioni successive
- Un IDE o uno strumento di build (Maven/Gradle) per gestire le dipendenze
- Permessi di scrittura sulla directory di output

## Passo 1: Creare una cartella di lavoro e accedere al primo foglio di lavoro

Creare una cartella di lavoro è il primo passo quando vuoi **esportare Excel in TXT**. La classe `Workbook` rappresenta l'intero file Excel, e `Worksheet` ti dà accesso alle celle.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Perché è importante*: L'oggetto workbook contiene tutti i dati, gli stili e i metadati. Iniziare con una cartella di lavoro nuova garantisce che nessuna formattazione nascosta interferisca con l'esportazione del testo.

## Passo 2: Aggiungere un valore numerico e limitare le cifre decimali

Inserisci un numero con molte cifre decimali così da poter dimostrare come **limitare le cifre decimali** durante l'esportazione.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Perché è importante*: Excel memorizza la precisione completa, ma quando esporti potresti voler troncare o arrotondare il valore. L'impostazione `limit decimal places` gestirà questo automaticamente.

## Passo 3: Configurare le opzioni di salvataggio TXT per mantenere le cifre significative

Aspose.Cells fornisce `TxtSaveOptions`. Impostare `significantDigits` indica all'esportatore di mantenere solo il numero richiesto di cifre significative, ignorando gli zeri iniziali.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Perché è importante*: L'opzione **keep significant digits** garantisce che il file di output contenga una quantità prevedibile di precisione, fondamentale per i sistemi a valle che si aspettano un formato numerico a larghezza fissa.

## Passo 4: Salvare la cartella di lavoro come TXT

Infine, scrivi la cartella di lavoro in un file di testo. Il metodo `save` rispetta le opzioni configurate, quindi il file risultante conterrà la rappresentazione decimale limitata.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Perché è importante*: Usare **save workbook as txt** con le `TxtSaveOptions` preparate garantisce che il file esportato rispetti i vincoli di precisione impostati nel passo precedente.

### Contenuto previsto di `SignificantDigits.txt`

```
0.00012346
```

Il valore mostra cinque cifre significative (`12346`) dopo l'arrotondamento, e gli zeri iniziali sono preservati secondo il formato TXT.

## Varianti e casi limite

| Scenario | Regolazione |
|----------|------------|
| **Diverso numero di cifre significative** | Chiama `txtOptions.setSignificantDigits(n)` dove `n` è 1‑15. |
| **Esportare un intervallo invece dell'intero foglio** | Usa `txtOptions.setExportRange("A1:B10")` prima di salvare. |
| **Preservare i separatori di colonna** | Imposta `txtOptions.setSeparator('\t')` per un output delimitato da tabulazioni. |
| **Fogli di lavoro grandi** | Aumenta `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` per evitare `OutOfMemoryError`. |

## Problemi comuni e consigli professionali

- **Non confondere le cifre significative con le cifre decimali**. Gli zeri iniziali non sono contati come significativi; usa `setSignificantDigits` per una precisione significativa e `setDecimalPlaces` se ti serve un numero fisso di cifre dopo il punto decimale.
- **Specifica sempre un percorso di output assoluto** quando esegui da un IDE per evitare errori di permessi.
- **Convalida il file generato** con una semplice chiamata `java.nio.file.Files.readAllLines(Paths.get(outputPath))` per assicurarti che il contenuto corrisponda alle aspettative prima di inviarlo ai processi a valle.

## Codice sorgente completo per riferimento

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Eseguendo il programma si genera `SignificantDigits.txt` contenente la singola riga `0.00012346`, dimostrando che il processo di **export excel to txt** rispetta sia i requisiti di **limit decimal places** che di **keep significant digits**.

## Conclusione

Ora sai come **esportare Excel in TXT** usando Aspose.Cells per Java controllando la precisione numerica. Configurando `TxtSaveOptions` puoi **limit decimal places**, **keep significant digits**, e salvare in modo affidabile **save workbook as txt** senza ulteriori post‑processi.

Successivamente, potresti esplorare:

- Esportare più fogli in file TXT separati (`save workbook as txt` per foglio)
- Usare `setSeparator` per creare output compatibile CSV
- Automatizzare conversioni batch per grandi set di dati

Sentiti libero di sperimentare con diversi conteggi di cifre e separatori per adattarli alle esigenze precise del tuo progetto. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come creare ed esportare Excel in HTML usando Aspose.Cells Java \| Guida alle operazioni su cartelle di lavoro](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Salva Excel come testo – Guida completa C# per esportare Excel in TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Esporta la cartella di lavoro Excel come immagine usando Aspose.Cells per Java&#58; Guida passo‑passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}