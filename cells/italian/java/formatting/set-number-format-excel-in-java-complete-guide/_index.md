---
category: general
date: 2026-06-18
description: Imposta il formato numerico di Excel usando Java, impara la notazione
  scientifica in Java, scrivi valori in una cella, imposta le cifre significative
  e esporta i dati in xlsx in pochi minuti.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: it
og_description: Imposta il formato numerico di Excel con Java. Scopri come utilizzare
  la notazione scientifica in Java, scrivere valori in una cella, impostare le cifre
  significative e esportare i dati in xlsx in modo efficiente.
og_title: Imposta il formato numerico di Excel in Java – Tutorial passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: Imposta il formato numerico di Excel in Java – Guida completa
url: /it/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il formato numerico Excel in Java – Guida completa

Ti sei mai chiesto come **impostare il formato numerico Excel** da un programma Java senza impazzire? Non sei l'unico. Che tu stia generando report finanziari o esportando log di sensori, far visualizzare correttamente quei numeri enormi in un file *.xlsx* è una competenza indispensabile.

In questo tutorial percorreremo una soluzione pratica, end‑to‑end: creare una cartella di lavoro, configurare **scientific notation java**, limitare **set significant digits**, scrivere un valore in una cella e infine **export data to xlsx**. Alla fine avrai uno snippet autonomo da inserire direttamente nel tuo progetto.

## Cosa imparerai

- Come inizializzare una cartella di lavoro con JExcel‑API (o Apache POI) in Java.  
- Le chiamate esatte per **set number format excel** per forzare la notazione scientifica.  
- Come **write value to cell** preservando la precisione.  
- Regolare le impostazioni della cartella di lavoro per **set significant digits** a un conteggio personalizzato.  
- Salvare il file in modo che possa essere aperto in qualsiasi applicazione di foglio di calcolo moderna (**export data to xlsx**).  

Nessun servizio esterno, nessuna magia. Solo Java puro e qualche classe ben documentata.

---

## Prerequisiti

- JDK 17 o successivo (il codice funziona anche su versioni più vecchie, ma gli esempi usano la sintassi moderna `var` per brevità).  
- Maven o Gradle per includere la dipendenza `org.apache.poi:poi-ooxml`.  
- Una conoscenza di base delle collezioni Java – se hai già scritto un ciclo `for`, sei a posto.

---

## Passo 1: Aggiungi la dipendenza Apache POI

Se usi Maven, incolla questo nel tuo `pom.xml`. Gli utenti Gradle possono tradurlo nella sintassi `implementation`.

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **Suggerimento:** Mantieni POI aggiornato. La versione 5.x aggiunge un miglior supporto per i formati numerici e per fogli di lavoro di grandi dimensioni.

---

## Passo 2: Crea una cartella di lavoro e accedi alle sue impostazioni  

La prima cosa di cui abbiamo bisogno è un nuovo oggetto workbook. Apache POI non espone una classe `WorkbookSettings` come faceva JExcel, ma possiamo ottenere lo stesso effetto creando successivamente un `CellStyle`.

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

Perché iniziamo con un **new workbook**? Pensalo come una tela vuota; ogni decisione di formattazione che prenderemo in seguito verrà applicata a questa tela.  

---

## Passo 3: Definisci un CellStyle per la notazione scientifica e le cifre significative  

Apache POI ti consente di creare una stringa di formato dati. Per imporre **scientific notation java** e limitare il numero di cifre, usiamo il pattern `"0.####E0"` – i simboli `#` controllano quante cifre significative vengono visualizzate.

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*Cosa sta succedendo?* Il formato dice a Excel: “Mostra il numero in notazione scientifica, ma mantieni solo fino a quattro cifre significative.” Se ti serve una precisione diversa, basta aggiungere o rimuovere i simboli `#`.  

---

## Passo 4: Scrivi un numero grande in una cella  

Ora **write value to cell** *A1* usando lo stile appena creato. Gli oggetti `Sheet` e `Row` sono leggeri, quindi crearli al volo è poco costoso.

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

Nota che non è stato necessario fare cast del numero; POI gestisce automaticamente i `double`. Collegando `sciStyle`, garantiamo che quando l'utente apre il file, Excel visualizzi `1.235E7` (arrotondato a quattro cifre significative) invece della stringa grezza a 8 cifre.

---

## Passo 5: Salva la cartella di lavoro – Export Data to XLSX  

L'ultimo passo è **export data to xlsx**. Scriveremo la cartella di lavoro in un file nella directory corrente, ma puoi indicare qualsiasi percorso desideri.

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Quando fai doppio clic su `sigDigits.xlsx`, vedrai la colonna **A** che mostra `1.235E7` – esattamente ciò che abbiamo richiesto.

### Output previsto

| A (Formatted) |
|---------------|
| 1.235E7       |

Se apri il file e cambi manualmente il formato della cella, noterai che il valore sottostante è ancora `12345678.9`. Questa è la magia di **set number format excel**: la visualizzazione cambia, i dati rimangono intatti.

---

## Domande frequenti e casi particolari

### Come modifico il numero di cifre significative?

Basta modificare la stringa di formato. Per tre cifre usa `"0.###E0"`; per sei cifre usa `"0.######E0"`.

### E se ho bisogno di una locale diversa (virgola come separatore decimale)?

Aggiungi un formato sensibile alla locale, ad esempio `df.getFormat("0,####E0")`. Excel rispetta le impostazioni regionali dell'utente, quindi la virgola apparirà solo se il workbook viene aperto su un sistema che la utilizza.

### Posso applicare lo stesso stile a un'intera colonna?

Assolutamente. Crea lo stile una volta (come mostrato) e poi itera le righe, applicando `cell.setCellStyle(sciStyle)` ogni volta. Per fogli di grandi dimensioni, considera l'uso di `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – è più veloce e mantiene il codice ordinato.

### E se sono bloccato con una versione Java più vecchia che non supporta `var`?

Sostituisci `var` con il tipo esplicito (`Workbook workbook = new XSSFWorkbook();`). Il resto del codice rimane identico.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Esegui la classe, apri `sigDigits.xlsx` e vedrai il numero visualizzato in notazione scientifica con esattamente quattro cifre significative. Questo è l'intero workflow **set number format excel** in Java.

---

## Conclusione

Abbiamo appena coperto tutto ciò di cui hai bisogno per **set number format excel** da Java: creare una cartella di lavoro, creare uno stile in notazione scientifica che **set significant digits**, **write value to cell**, e infine **export data to xlsx**. L'approccio è leggero, utilizza solo Apache POI e funziona su qualsiasi piattaforma che supporta Java.

Successivamente, potresti voler:

- Aggiungere formattazione condizionale per evidenziare valori fuori intervallo.  
- Generare più fogli con stili numerici diversi (ad esempio, valuta vs. scientifica).  
- Trasmettere grandi dataset con `SXSSFWorkbook` per esportazioni a consumo di memoria efficiente.

Provali e diventerai la persona di riferimento per l'automazione di Excel nel tuo team. Hai domande o un caso d'uso particolare? Lascia un commento qui sotto—buona programmazione! 

*Immagine che illustra il flusso di lavoro (testo alternativo: “diagramma del workflow set number format excel che mostra codice Java, notazione scientifica e export to xlsx”)*

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come impostare una cella attiva in Excel usando Aspose.Cells per Java: Guida completa](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Imposta Cella Attiva Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Imposta Cella Attiva Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}