---
category: general
date: 2026-03-01
description: Copia la tabella pivot in Java preservando il pivot, poi esporta Excel
  in PPTX, disabilita l'AutoFiltro di Excel e usa Smart Marker per gli array JSON
  – guida completa passo‑passo.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: it
og_description: Copia la tabella pivot in Java, conserva la definizione della pivot,
  esporta in PPTX, disabilita AutoFilter e utilizza Smart Marker – guida completa
  per sviluppatori.
og_title: Copia la tabella pivot in Java – preservala, esportala in PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copia la tabella pivot in Java – Conservala, esportala in PPTX
url: /it/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia Tabella Pivot in Java – Conservala, Esporta in PPTX

Ti è mai capitato di dover **copiare una tabella pivot** da una cartella di lavoro a un'altra senza perdere la definizione della pivot sottostante? Non sei l'unico a grattarsi la testa per questo. In molti progetti reali ti troverai a spostare dati, e l'ultima cosa che desideri è una pivot rotta che genera errori a runtime.  

In questo tutorial percorreremo una soluzione completa che non solo **copia la tabella pivot**, ma ti mostra anche come **preservare la tabella pivot** durante la copia, **esportare Excel in PPTX**, **disabilitare l'AutoFilter di Excel** e **usare smart marker** per inserire un array JSON in una singola cella. Alla fine avrai un unico programma Java eseguibile che copre tutti e quattro gli scenari.

## Prerequisiti

- Java 8 o versioni successive (il codice funziona anche con Java 11)  
- Libreria Aspose.Cells for Java (versione 23.9 o successiva) – puoi scaricarla da Maven Central  
- Familiarità di base con i concetti di Excel come tabelle pivot, tabelle e caselle di testo  

Se ti manca il JAR di Aspose.Cells, aggiungi questo al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Ora, immergiamoci.

## Passo 1: Copia Tabella Pivot – Preservando la Definizione della Pivot

Quando copi semplicemente l'intervallo di celle che contiene una tabella pivot, i metadati della pivot spesso rimangono indietro. Aspose.Cells ci offre un modo pratico per mantenere intatta la definizione usando `copyRange` con un'istanza di `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Perché funziona:** `CopyOptions` indica ad Aspose.Cells di trasferire tutto, inclusa la cache della pivot e le impostazioni dei campi. Senza di esso, otterresti solo valori semplici e perderesti la possibilità di aggiornare la pivot.

**Caso limite:** Se la tua pivot di origine supera l'intervallo hard‑coded `A1:G20`, regola l'intervallo di conseguenza o usa `sourceSheet.getPivotTables().get(0).getDataRange()` per ottenerlo dinamicamente.

![Esempio di copia della tabella pivot](image.png "Copia tabella pivot in Java")

*Testo alternativo dell'immagine: diagramma della copia della tabella pivot in Java*

## Passo 2: Esporta un Foglio di Lavoro con una Casella di Testo Modificabile in PPTX

Spesso è necessario trasformare un foglio Excel in una diapositiva PowerPoint—pensa ai cruscotti settimanali da presentare. Aspose.Cells può salvare direttamente un foglio di lavoro come file PPTX preservando forme come le caselle di testo.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Cosa succede:** Il metodo `save` con `SaveFormat.PPTX` converte l'intero foglio, inclusa qualsiasi TextBox modificabile, in una diapositiva PowerPoint. Il testo all'interno della casella rimane modificabile quando apri il PPTX in PowerPoint.

**Suggerimento:** Se hai più fogli e ne desideri uno specifico, chiama `wb.getWorksheets().removeAt(index)` per gli altri prima di salvare.

## Passo 3: Disabilita AutoFilter di Excel da una Tabella

AutoFilter è comodo per gli utenti finali, ma a volte è necessario disattivarlo programmaticamente—magari prima di esportare dati o quando si genera un report pulito. Ecco come **disabilitare l'autofilter di Excel** su una tabella Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Perché potresti averne bisogno:** Esportare in formati che non supportano AutoFilter (come CSV o PDF) può far apparire icone di filtro residue. Disabilitarlo garantisce un output pulito.

**Errore comune:** Se il foglio non contiene tabelle, `getTables().get(0)` genererà un `IndexOutOfBoundsException`. Controlla sempre prima `sheet.getTables().size()` nel codice di produzione.

## Passo 4: Usa Smart Marker – Inserisci un Array JSON come Valore di una Singola Cell

Smart Marker è il motore di templating di Aspose. Un trucco utile è trattare un intero array JSON come valore di una singola cella, perfetto per il logging o per passare dati strutturati a valle. Vediamo come **usare smart marker** per ottenere questo.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Come funziona:** Il marcatore `${json}` nella cartella di lavoro viene sostituito dall'intera stringa JSON perché abbiamo impostato `ArrayAsSingle`. Senza questa opzione, Aspose tenterebbe di espandere ogni elemento dell'array in righe separate.

**Variazione:** Se hai bisogno che l'array sia suddiviso su più righe, basta omettere `ArrayAsSingle` e lasciare che Smart Marker gestisca l'espansione automaticamente.

## Esempio Completo Funzionante – Tutti i Passi Combinati

Di seguito trovi una singola classe Java che concatena tutte le operazioni trattate. Eseguila come un normale metodo `main`; basta adeguare i percorsi dei file al tuo ambiente.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}