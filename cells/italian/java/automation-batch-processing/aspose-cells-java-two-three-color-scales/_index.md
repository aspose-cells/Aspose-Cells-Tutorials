---
date: '2026-01-03'
description: Impara a creare cartelle di lavoro Excel, automatizzare i report Excel
  e aggiungere formattazione condizionale usando Aspose.Cells per Java con scale a
  due e tre colori.
keywords:
- automate Excel reports
- add conditional formatting
- generate excel file
- conditional formatting tutorial
- save excel workbook
title: Crea cartella di lavoro Excel e automatizza i report con Aspose.Cells
url: /it/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizzare i report Excel con Aspose.Cells Java

## Introduzione
Nel mondo odierno guidato dai dati, **creare un workbook Excel** che non solo memorizzi i dati ma li visualizzi efficacemente è una competenza chiave. Applicare manualmente la formattazione a fogli di grandi dimensioni richiede tempo ed è soggetto a errori. Questo tutorial ti mostra come **automatizzare i report Excel**, aggiungere formattazione condizionale e generare un file Excel rifinito usando Aspose.Cells per Java. Alla fine, avrai un workbook completamente funzionale con scale a due e tre colori che evidenziano le tendenze istantaneamente.

### Risposte rapide
- **Cosa significa “create excel workbook”?** Indica la generazione programmatica di un file .xlsx da zero.  
- **Quale libreria gestisce la formattazione condizionale?** Aspose.Cells per Java fornisce un'API ricca per le scale di colore.  
- **È necessaria una licenza?** È disponibile una licenza di prova gratuita per la valutazione.  
- **Posso salvare il workbook in altri formati?** Sì, Aspose.Cells supporta XLS, CSV, PDF e altro.  
- **Questo approccio è adatto a grandi dataset?** Assolutamente—Aspose.Cells è ottimizzato per le prestazioni.

## Che cos'è creare un workbook Excel?
Creare un workbook Excel in modo programmatico ti consente di costruire fogli di calcolo al volo, incorporare dati, applicare stili e salvare il file senza mai aprire Excel. È ideale per pipeline di reporting automatizzate, esportazioni di dati programmate e dashboard in tempo reale.

## Perché usare Aspose.Cells per Java?
- **Full control** over worksheets, cells, and formatting.  
- **No dependency on Microsoft Office** – works on any server.  
- **High performance** with large files and complex formulas.  
- **Rich feature set** including charts, pivots, and conditional formatting.

## Prerequisiti
- **Java Development Kit (JDK)** 8 o superiore.  
- **IDE** come IntelliJ IDEA o Eclipse.  
- **Aspose.Cells library** – aggiungi via Maven o Gradle (vedi sotto).  

### Configurazione di Aspose.Cells per Java
#### Installazione via Maven:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
#### Installazione via Gradle:
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
Aspose.Cells offre una licenza di prova gratuita, che ti permette di testare tutte le sue funzionalità prima dell'acquisto. Puoi ottenerla visitando la [free trial page](https://releases.aspose.com/cells/java/).

### Inizializzazione di base
```java
import com.aspose.cells.Workbook;

public class ExcelAutomation {
    public static void main(String[] args) {
        // Initialize a new Workbook
        Workbook workbook = new Workbook();
        
        // Your code to manipulate the workbook goes here
    }
}
```

## Come creare un workbook Excel con Aspose.Cells Java
Ora che l'ambiente è pronto, seguiamo passo passo ogni fase necessaria per **create excel workbook**, popolare i dati e applicare le scale di colore.

### Creare e accedere a Workbook e Worksheet
**Overview:**  
Inizia creando un nuovo workbook e recuperando il foglio di lavoro predefinito dove verrà applicata la formattazione.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize a new Workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Aggiungere dati alle celle
**Overview:**  
Popola il foglio con numeri di esempio in modo che la formattazione condizionale abbia qualcosa da valutare.

```java
import com.aspose.cells.Cells;

Cells cells = worksheet.getCells();
cells.get("A1").putValue("2-Color Scale");
cells.get("D1").putValue("3-Color Scale");

// Add sequential numbers from 2 to 15 in columns A and D
for (int i = 2; i <= 15; i++) {
    cells.get("A" + i).putValue(i);
    cells.get("D" + i).putValue(i);
}
```

### Aggiungere formattazione condizionale a scala a due colori
**Overview:**  
Applica una scala a due colori alla colonna A per evidenziare valori bassi rispetto a quelli alti.

```java
import com.aspose.cells.CellArea;
import com.aspose.cells.FormatConditionType;
import com.aspose.cells.FormatConditionCollection;
import com.aspose.cells.FormatCondition;
import com.aspose.cells.Color;

CellArea ca = CellArea.createCellArea("A2", "A15");
int idx = worksheet.getConditionalFormattings().add();
FormatConditionCollection fcc = worksheet.getConditionalFormattings().get(idx);
fcc.addCondition(FormatConditionType.COLOR_SCALE);
fcc.addArea(ca);

// Configure the two-color scale
FormatCondition fc = fcc.get(0);
fc.getColorScale().setIs3ColorScale(false); // Enable two-color scale
fc.getColorScale().setMaxColor(Color.getLightBlue());
fc.getColorScale().setMinColor(Color.getLightGreen());
```

### Aggiungere formattazione condizionale a scala a tre colori
**Overview:**  
Una scala a tre colori offre una visuale più sfumata dei dati nella colonna D.

```java
ca = CellArea.createCellArea("D2", "D15");
idx = worksheet.getConditionalFormattings().add();
fcc = worksheet.getConditionalFormattings().get(idx);
fcc.addCondition(FormatConditionType.COLOR_SCALE);
fcc.addArea(ca);

// Configure the three-color scale
fc = fcc.get(0);
fc.getColorScale().setIs3ColorScale(true); // Enable three-color scale
fc.getColorScale().setMaxColor(Color.getLightBlue());
fc.getColorScale().setMidColor(Color.getYellow()); 
fc.getColorScale().setMinColor(Color.getLightGreen());
```

### Salvare il workbook
**Overview:**  
Infine, **save excel workbook** su disco nel moderno formato XLSX.

```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATAThreeColorScale_out.xlsx", SaveFormat.XLSX);
```

## Applicazioni pratiche
Usando Aspose.Cells per Java, puoi **automate Excel reports** in numerosi scenari reali:

- **Sales Reports:** Evidenzia gli obiettivi raggiunti o mancati con scale a due colori.  
- **Financial Analysis:** Visualizza i margini di profitto usando gradienti a tre colori.  
- **Inventory Management:** Segnala immediatamente gli articoli a basso stock.  

Queste tecniche si integrano perfettamente con le piattaforme BI, consentendo insight in tempo reale.

## Considerazioni sulle prestazioni
Quando si lavora con dataset di grandi dimensioni:

- Elabora i dati a blocchi per mantenere basso l'uso di memoria.  
- Sfrutta le API di streaming di Aspose.Cells per I/O efficiente.  
- Assicurati che la JVM disponga di sufficiente heap (es. `-Xmx2g` per file molto grandi).

## Conclusione
Hai appena imparato come **create excel workbook**, popolarlo e applicare sia la formattazione condizionale a scala a due colori che a tre colori usando Aspose.Cells per Java. Questa automazione non solo accelera la generazione dei report, ma rende i dati immediatamente comprensibili.

Successivamente, esplora altre funzionalità di Aspose.Cells come la creazione di grafici, tabelle pivot o l'esportazione in PDF per arricchire ulteriormente i tuoi report automatizzati.

## Sezione FAQ
1. **How do I obtain a free trial license for Aspose.Cells?**  
   - Visit [Aspose's free trial page](https://releases.aspose.com/cells/java/).  
2. **Can I apply conditional formatting to multiple sheets at once?**  
   - Currently, you need to configure each sheet individually.  
3. **What if my Excel file is very large? Does Aspose.Cells handle it efficiently?**  
   - Yes, Aspose.Cells is optimized for performance with large datasets.  
4. **How do I change the colors used in the color scale?**  
   - Modify `setMaxColor`, `setMidColor`, and `setMinColor` methods as needed.  
5. **What are some common issues when using Aspose.Cells Java?**  
   - Ensure all dependencies are correctly configured, and verify version compatibility.

### Domande aggiuntive
**Q: Can I generate the Excel file in other formats like CSV or PDF?**  
A: Absolutely—use `SaveFormat.CSV` or `SaveFormat.PDF` in the `workbook.save` call.

**Q: Is it possible to apply the same conditional formatting to a dynamic range?**  
A: Yes, you can calculate the range at runtime and pass it to `CellArea.createCellArea`.

**Q: How do I embed a license key programmatically?**  
A: Call `License license = new License(); license.setLicense("Aspose.Cells.lic");` before creating the workbook.

## Risorse
Per informazioni più dettagliate:

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- [Download Aspose.Cells](https://releases.aspose.com/cells/java/)  
- Purchase or obtain a temporary license at [Aspose's purchase page](https://purchase.aspose.com/buy)  
- For support, visit the [Aspose Forum](https://forum.aspose.com/c/cells/9)

---

**Last Updated:** 2026-01-03  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}