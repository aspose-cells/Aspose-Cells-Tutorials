---
"date": "2025-04-08"
"description": "Scopri come utilizzare Aspose.Cells per Java per aggiungere caselle di testo e impostare l'interlinea nelle cartelle di lavoro di Excel. Migliora le presentazioni delle tue cartelle di lavoro con forme di testo stilizzate."
"title": "Aggiungi casella di testo e imposta la spaziatura delle linee in Excel utilizzando Aspose.Cells per Java"
"url": "/it/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aggiungere una casella di testo e impostare l'interlinea in Excel utilizzando Aspose.Cells per Java

## Introduzione

La creazione di report Excel dinamici richiede spesso una formattazione personalizzata del testo, ad esempio l'aggiunta di caselle di testo con una specifica interlinea. Con Aspose.Cells per Java, questo diventa semplice ed efficiente. Questo tutorial ti guiderà a migliorare le presentazioni delle tue cartelle di lavoro utilizzando Aspose.Cells per Java per aggiungere forme di testo con stili.

Al termine di questa guida imparerai come:
- Crea una nuova cartella di lavoro di Excel e accedi ai suoi fogli di lavoro
- Aggiungere una forma di casella di testo a un foglio di lavoro
- Imposta la spaziatura personalizzata delle linee all'interno di una forma di testo
- Salva la tua cartella di lavoro formattata in formato XLSX

Cominciamo a configurare l'ambiente.

### Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:
- Java Development Kit (JDK) installato sul tuo computer
- Un IDE o un editor per scrivere codice Java
- Sistema di build Maven o Gradle configurato per gestire le dipendenze

Sarà utile avere una conoscenza di base della programmazione Java e avere familiarità con le strutture dei file Excel.

## Impostazione di Aspose.Cells per Java

Includi Aspose.Cells nella gestione delle dipendenze del tuo progetto utilizzando Maven o Gradle:

**Esperto**

Aggiungi il seguente blocco di dipendenza al tuo `pom.xml` file:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Includi questo nel tuo `build.gradle` file:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Successivamente, puoi acquistare una licenza per Aspose.Cells scegliendo una prova gratuita, richiedendo una licenza temporanea o acquistando una licenza completa.

### Inizializzazione di Aspose.Cells

Una volta inclusa la libreria nel progetto, inizializzala all'interno dell'applicazione Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Inizializza un'istanza di Workbook (rappresenta un file Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Guida all'implementazione

### Creare una cartella di lavoro e un foglio di lavoro di Access

Inizia creando una nuova cartella di lavoro Excel e accedendo al suo primo foglio di lavoro. Qui è dove aggiungerai la tua casella di testo.

#### Panoramica

La creazione di una nuova cartella di lavoro fornisce uno spazio vuoto in cui aggiungere dati, forme e formattazione in base alle esigenze.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Aggiungi casella di testo al foglio di lavoro

Successivamente, aggiungi una forma di casella di testo al foglio di lavoro selezionato. Questa forma può contenere qualsiasi contenuto testuale di cui hai bisogno.

#### Panoramica

Le caselle di testo sono strumenti versatili che consentono di inserire testi personalizzati, come note o istruzioni, direttamente in un foglio Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Aggiungere una forma di casella di testo al foglio di lavoro
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Imposta il testo in forma

Una volta pronta la casella di testo, impostane il contenuto e formatta il testo al suo interno.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Aggiungere una forma di casella di testo al foglio di lavoro
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Imposta il contenuto del testo all'interno della forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Accedi ai paragrafi di testo in formato Shape

È possibile accedere ai singoli paragrafi all'interno di una casella di testo per applicare una formattazione specifica.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Aggiungere una forma di casella di testo al foglio di lavoro
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Imposta il contenuto del testo all'interno della forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accedi al secondo paragrafo nella forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Imposta l'interlinea del paragrafo

Personalizzare l'interlinea può migliorare la leggibilità. Ecco come impostarla:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Aggiungere una forma di casella di testo al foglio di lavoro
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Imposta il contenuto del testo all'interno della forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accedi al secondo paragrafo nella forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Imposta l'interlinea a 20 punti
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configura lo spazio prima e dopo il paragrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Salva cartella di lavoro

Infine, salva la cartella di lavoro con la casella di testo appena aggiunta e formattata.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Crea una nuova cartella di lavoro (file Excel)
        Workbook workbook = new Workbook();
        
        // Accedi al primo foglio di lavoro
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Aggiungere una forma di casella di testo al foglio di lavoro
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Imposta il contenuto del testo all'interno della forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Accedi al secondo paragrafo nella forma
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Imposta l'interlinea a 20 punti
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configura lo spazio prima e dopo il paragrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Salva la cartella di lavoro
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusione

Hai imparato con successo come aggiungere una casella di testo e impostare l'interlinea in una cartella di lavoro di Excel utilizzando Aspose.Cells per Java. Questo migliorerà la tua capacità di creare report dinamici e visivamente accattivanti.

## Consigli per le parole chiave
- "Aspose.Cells per Java"
- "Aggiungi casella di testo in Excel"
- "Impostare l'interlinea in Excel"
- "Cartella di lavoro Excel con testo formattato"
- "Java e Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}