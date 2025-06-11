---
"date": "2025-04-08"
"description": "Μάθετε πώς να χρησιμοποιείτε το Aspose.Cells για Java για να προσθέτετε πλαίσια κειμένου και να ορίζετε απόσταση μεταξύ γραμμών σε βιβλία εργασίας του Excel. Βελτιώστε τις παρουσιάσεις των βιβλίων εργασίας σας με στυλιζαρισμένα σχήματα κειμένου."
"title": "Προσθήκη πλαισίου κειμένου και ορισμός απόστασης μεταξύ γραμμών στο Excel χρησιμοποιώντας το Aspose.Cells για Java"
"url": "/el/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Προσθήκη πλαισίου κειμένου και ορισμός απόστασης γραμμών στο Excel χρησιμοποιώντας το Aspose.Cells για Java

## Εισαγωγή

Η δημιουργία δυναμικών αναφορών Excel συχνά απαιτεί προσαρμοσμένη μορφοποίηση κειμένου, όπως η προσθήκη πλαισίων κειμένου με συγκεκριμένη απόσταση μεταξύ γραμμών. Με το Aspose.Cells για Java, αυτό γίνεται απλό και αποτελεσματικό. Αυτό το σεμινάριο θα σας καθοδηγήσει στη βελτίωση των παρουσιάσεων του βιβλίου εργασίας σας χρησιμοποιώντας το Aspose.Cells για Java για την προσθήκη στυλιζαρισμένων σχημάτων κειμένου.

Μέχρι το τέλος αυτού του οδηγού, θα μάθετε πώς να:
- Δημιουργήστε ένα νέο βιβλίο εργασίας του Excel και αποκτήστε πρόσβαση στα φύλλα εργασίας του
- Προσθήκη σχήματος πλαισίου κειμένου σε ένα φύλλο εργασίας
- Ορισμός προσαρμοσμένης απόστασης γραμμών μέσα σε ένα σχήμα κειμένου
- Αποθηκεύστε το μορφοποιημένο βιβλίο εργασίας σας σε μορφή XLSX

Ας ξεκινήσουμε ρυθμίζοντας το περιβάλλον σας.

### Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τα εξής:
- Κιτ ανάπτυξης Java (JDK) εγκατεστημένο στον υπολογιστή σας
- Ένα IDE ή πρόγραμμα επεξεργασίας για τη σύνταξη κώδικα Java
- Σύστημα δημιουργίας Maven ή Gradle διαμορφωμένο για διαχείριση εξαρτήσεων

Η βασική κατανόηση του προγραμματισμού Java και η εξοικείωση με τις δομές αρχείων Excel θα είναι επωφελής.

## Ρύθμιση του Aspose.Cells για Java

Συμπεριλάβετε το Aspose.Cells στη διαχείριση εξαρτήσεων του έργου σας χρησιμοποιώντας το Maven ή το Gradle:

**Maven**

Προσθέστε το ακόλουθο μπλοκ εξάρτησης στο `pom.xml` αρχείο:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Γκράντλ**

Συμπεριλάβετε αυτό στο δικό σας `build.gradle` αρχείο:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Στη συνέχεια, αποκτήστε μια άδεια χρήσης για το Aspose.Cells επιλέγοντας μια δωρεάν δοκιμαστική περίοδο, ζητώντας μια προσωρινή άδεια χρήσης ή αγοράζοντας μια πλήρη άδεια χρήσης.

### Αρχικοποίηση του Aspose.Cells

Μόλις η βιβλιοθήκη συμπεριληφθεί στο έργο σας, αρχικοποιήστε την μέσα στην εφαρμογή Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Αρχικοποίηση μιας παρουσίας του Βιβλίου Εργασίας (αντιπροσωπεύει ένα αρχείο Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Οδηγός Εφαρμογής

### Δημιουργία βιβλίου εργασίας και φύλλου εργασίας της Access

Ξεκινήστε δημιουργώντας ένα νέο βιβλίο εργασίας του Excel και αποκτώντας πρόσβαση στο πρώτο φύλλο εργασίας του. Εδώ θα προσθέσετε το πλαίσιο κειμένου σας.

#### Επισκόπηση

Η δημιουργία ενός νέου βιβλίου εργασίας παρέχει μια κενή καρτέλα για την προσθήκη δεδομένων, σχημάτων και μορφοποίησης, όπως απαιτείται.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Προσθήκη πλαισίου κειμένου σε φύλλο εργασίας

Στη συνέχεια, προσθέστε ένα σχήμα πλαισίου κειμένου στο επιλεγμένο φύλλο εργασίας σας. Αυτό το σχήμα μπορεί να περιέχει οποιοδήποτε κείμενο χρειάζεστε.

#### Επισκόπηση

Τα πλαίσια κειμένου είναι ευέλικτα εργαλεία για την συμπερίληψη προσαρμοσμένων κειμένων, όπως σημειώσεων ή οδηγιών, απευθείας μέσα σε ένα φύλλο Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Προσθήκη σχήματος πλαισίου κειμένου στο φύλλο εργασίας
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Ορισμός κειμένου σε σχήμα

Μόλις το πλαίσιο κειμένου σας είναι έτοιμο, ορίστε το περιεχόμενό του και μορφοποιήστε το κείμενο μέσα σε αυτό.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Προσθήκη σχήματος πλαισίου κειμένου στο φύλλο εργασίας
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ορισμός περιεχομένου κειμένου μέσα στο σχήμα
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Παράγραφοι κειμένου Access σε σχήμα

Μπορείτε να αποκτήσετε πρόσβαση σε μεμονωμένες παραγράφους μέσα σε ένα πλαίσιο κειμένου για να εφαρμόσετε συγκεκριμένη μορφοποίηση.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Προσθήκη σχήματος πλαισίου κειμένου στο φύλλο εργασίας
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ορισμός περιεχομένου κειμένου μέσα στο σχήμα
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Πρόσβαση στη δεύτερη παράγραφο του σχήματος
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Ορισμός απόστασης μεταξύ γραμμών παραγράφου

Η προσαρμογή της απόστασης μεταξύ των γραμμών μπορεί να βελτιώσει την αναγνωσιμότητα. Δείτε πώς μπορείτε να την ορίσετε:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Προσθήκη σχήματος πλαισίου κειμένου στο φύλλο εργασίας
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ορισμός περιεχομένου κειμένου μέσα στο σχήμα
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Πρόσβαση στη δεύτερη παράγραφο του σχήματος
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ορισμός απόστασης γραμμών σε 20 σημεία
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Ρύθμιση παραμέτρων χώρου πριν και μετά την παράγραφο
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Αποθήκευση βιβλίου εργασίας

Τέλος, αποθηκεύστε το βιβλίο εργασίας σας με το νέο πλαίσιο κειμένου που προστέθηκε και μορφοποιήθηκε.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Δημιουργία νέου βιβλίου εργασίας (αρχείο Excel)
        Workbook workbook = new Workbook();
        
        // Πρόσβαση στο πρώτο φύλλο εργασίας
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Προσθήκη σχήματος πλαισίου κειμένου στο φύλλο εργασίας
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Ορισμός περιεχομένου κειμένου μέσα στο σχήμα
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Πρόσβαση στη δεύτερη παράγραφο του σχήματος
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Ορισμός απόστασης γραμμών σε 20 σημεία
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Ρύθμιση παραμέτρων χώρου πριν και μετά την παράγραφο
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Αποθήκευση του βιβλίου εργασίας
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Σύναψη

Μάθατε με επιτυχία πώς να προσθέτετε ένα πλαίσιο κειμένου και να ορίζετε την απόσταση μεταξύ γραμμών σε ένα βιβλίο εργασίας του Excel χρησιμοποιώντας το Aspose.Cells για Java. Αυτό βελτιώνει την ικανότητά σας να δημιουργείτε δυναμικές, οπτικά ελκυστικές αναφορές.

## Προτάσεις λέξεων-κλειδιών
- "Aspose.Cells για Java"
- "Προσθήκη πλαισίου κειμένου στο Excel"
- "Ορισμός απόστασης γραμμών στο Excel"
- "Βιβλίο εργασίας Excel με κείμενο με στυλ"
- "Java και Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}