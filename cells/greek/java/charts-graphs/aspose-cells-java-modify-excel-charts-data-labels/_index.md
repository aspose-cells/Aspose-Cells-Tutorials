---
date: '2026-06-22'
description: Μάθετε πώς να αλλάξετε τα chart data labels και να προσαρμόσετε τα data
  labels στο Excel με το Aspose.Cells for Java. Αυτός ο οδηγός καλύπτει την τροποποίηση
  του chart, το font formatting και πρακτικά παραδείγματα.
keywords:
- change chart data labels
- customize data labels excel
- format data label fonts
- Aspose.Cells Java chart modification
- Excel automation Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  headline: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  type: TechArticle
- description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  name: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  steps:
  - name: Create a Workbook
    text: This line creates the `Workbook` instance, giving you full access to worksheets,
      charts, and cells.
  - name: Save the Modified Workbook
    text: After you finish editing, call `save` to write the changes to disk.
  - name: Access First Worksheet
    text: The `Worksheet` class represents a single sheet; accessing it via `getWorksheets().get(0)`
      gives you the first sheet.
  - name: Access First Chart
    text: The `Chart` class encapsulates all chart‑related properties. Once you have
      a reference, you can modify series, axes, and data labels.
  - name: Modify Data Label Text
    text: Use `setText("Your custom label")` on the `DataLabel` object to replace
      the default value.
  - name: Customize Font
    text: The `Font` class lets you set `setBold(true)`, `setColor(Color.getRed())`,
      and other attributes for precise visual control.
  type: HowTo
- questions:
  - answer: Yes, the free trial provides full functionality for development and testing;
      a commercial license is required for production deployments.
    question: Can I use Aspose.Cells for Java without a paid license?
  - answer: It can process files with over 500 MB and 100 + worksheets using less
      than 300 MB of RAM when memory‑optimized settings are enabled.
    question: How does Aspose.Cells handle large Excel files?
  - answer: Absolutely – iterate over `worksheet.getCharts()` and apply the same label‑changing
      logic to each chart object.
    question: Is it possible to modify multiple charts in one workbook?
  - answer: Forgetting to call `setShowValue(true)` on the series, or not disposing
      of the workbook, can lead to missing labels or memory leaks.
    question: What are the most common pitfalls when customizing data labels?
  - answer: Yes, simply add the Maven/Gradle dependency and inject the workbook handling
      code into a Spring service component.
    question: Can Aspose.Cells be integrated with Spring Boot?
  type: FAQPage
title: Πώς να αλλάξετε τα chart data labels και να τροποποιήσετε τα Excel charts χρησιμοποιώντας
  το Aspose.Cells for Java
url: /el/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αλλάξετε τις Ετικέτες Δεδομένων Γραφήματος και να Τροποποιήσετε τα Διαγράμματα Excel Χρησιμοποιώντας το Aspose.Cells για Java

## Εισαγωγή

Η αλλαγή των ετικετών δεδομένων γραφήματος προγραμματιστικά μπορεί να εξοικονομήσει ώρες χειροκίνητης ρύθμισης, ειδικά όταν χρειάζεται να δημιουργήσετε δεκάδες οικονομικές αναφορές αυτόματα. Σε αυτό το tutorial θα μάθετε πώς να **αλλάξετε τις ετικέτες δεδομένων γραφήματος** σε ένα βιβλίο εργασίας Excel χρησιμοποιώντας το Aspose.Cells για Java, καθώς και πώς να προσαρμόσετε τις γραμματοσειρές των ετικετών για ένα επαγγελματικό αποτέλεσμα. Στο τέλος του οδηγού θα μπορείτε να φορτώσετε ένα βιβλίο εργασίας, να εντοπίσετε ένα γράφημα και να εφαρμόσετε μορφοποίηση πλούσιου κειμένου σε οποιαδήποτε ετικέτα δεδομένων — χωρίς να ανοίξετε το Excel.

**Τι Θα Μάθετε**
- Πρόσβαση και τροποποίηση βιβλίων εργασίας Excel
- Περιήγηση φύλλων εργασίας και γραφημάτων
- Αλλαγή ετικετών δεδομένων γραφήματος και προσαρμογή της εμφάνισής τους
- Μορφοποίηση γραμματοσειρών ετικετών δεδομένων για οπτικό αντίκτυπο

Ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε πριν βυθιστούμε στον κώδικα.

## Γρήγορες Απαντήσεις
- **Μπορώ να τροποποιήσω τις ετικέτες δεδομένων γραφήματος χωρίς να ανοίξω το Excel;** Ναι, το Aspose.Cells σας επιτρέπει να αλλάξετε τις ετικέτες απευθείας στο αρχείο.
- **Ποια έκδοση της βιβλιοθήκης υποστηρίζει αυτή τη δυνατότητα;** Όλες οι εκδόσεις του Aspose.Cells for Java 20.10 και νεότερες.
- **Χρειάζομαι πληρωμένη άδεια για να εκτελέσω το παράδειγμα;** Η δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται άδεια για παραγωγή.
- **Είναι η Java 8 επαρκής;** Ναι, η Java 8 ή νεότερη υποστηρίζεται πλήρως.
- **Μπορώ να μορφοποιήσω τις γραμματοσειρές των ετικετών (χρώμα, έντονη, μέγεθος);** Απόλυτα – το API παρέχει πλήρη έλεγχο στυλ γραμματοσειράς.

## Τι είναι το Aspose.Cells για Java;
Το Aspose.Cells for Java είναι ένα ισχυρό API που επιτρέπει τη δημιουργία, τη διαχείριση και τη μετατροπή λογιστικών φύλλων Excel χωρίς το Microsoft Excel. Υποστηρίζει **50+** μορφές αρχείων — συμπεριλαμβανομένων των XLSX, CSV, PDF και HTML — και μπορεί να επεξεργαστεί βιβλία εργασίας πολλαπλών εκατοντάδων σελίδων χρησιμοποιώντας λιγότερο από 200 MB μνήμης.

## Γιατί να Αλλάξετε τις Ετικέτες Δεδομένων Γραφήματος;
Η προγραμματιστική αλλαγή των ετικετών δεδομένων γραφήματος μειώνει τα χειροκίνητα σφάλματα, εξασφαλίζει τη συνέπεια μεταξύ των αναφορών και επιτρέπει δυναμικές ενημερώσεις βάσει δεδομένων σε πραγματικό χρόνο. Με το Aspose.Cells μπορείτε να ενημερώσετε χιλιάδες γραφήματα σε δευτερόλεπτα, μια εργασία που διαφορετικά θα απαιτούσε ημέρες αν γινόταν χειροκίνητα.

## Προαπαιτούμενα

- **Βιβλιοθήκη Aspose.Cells** – προσθέστε το JAR μέσω Maven ή Gradle (δείτε παρακάτω).
- **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη.
- **IDE** – IntelliJ IDEA, Eclipse ή οποιονδήποτε επεξεργαστή συμβατό με Java.

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Απόκτηση Άδειας

Το Aspose.Cells προσφέρει δωρεάν δοκιμή, προσωρινές άδειες για αξιολόγηση και πλήρεις εμπορικές άδειες. Για να ξεκινήσετε με τη δωρεάν δοκιμή:

1. Επισκεφθείτε τη σελίδα [Aspose's Free Trial](https://releases.aspose.com/cells/java/).
2. Κατεβάστε τη βιβλιοθήκη και εφαρμόστε την δοκιμαστική άδεια στο έργο σας.

Για παραγωγική χρήση, αποκτήστε προσωρινή ή μόνιμη άδεια από τη [Purchase Page](https://purchase.aspose.com/buy).

### Βασική Αρχικοποίηση

Η κλάση `Workbook` είναι το βασικό αντικείμενο του Aspose.Cells που αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Αρχικοποιήστε το με τη διαδρομή προς το πηγαίο βιβλίο εργασίας:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```

## Ρύθμιση του Aspose.Cells για Java

Μonce η βιβλιοθήκη προστεθεί στο έργο σας, διαμορφώστε το περιβάλλον ώστε να μπορείτε να αλληλεπιδράτε με αρχεία Excel άψογα.

### Απαιτήσεις Ρύθμισης Περιβάλλοντος

- JDK 8+
- Προτιμώμενο IDE (IntelliJ IDEA, Eclipse)
- Maven ή Gradle για διαχείριση εξαρτήσεων

## Οδηγός Υλοποίησης

Θα περάσουμε από κάθε βήμα που απαιτείται για να **αλλάξετε τις ετικέτες δεδομένων γραφήματος** και να εφαρμόσετε προσαρμοσμένη μορφοποίηση γραμματοσειράς.

### Πρόσβαση και Τροποποίηση Βιβλίου Εργασίας Excel

**Επισκόπηση**: Φορτώστε ένα υπάρχον βιβλίο εργασίας, κάντε αλλαγές και αποθηκεύστε ένα νέο αντίγραφο.

#### Πώς να Φορτώσετε και να Αποθηκεύσετε ένα Βιβλίο Εργασίας

Φορτώστε το βιβλίο εργασίας σας με `new Workbook("input.xlsx")` και αποθηκεύστε το χρησιμοποιώντας `workbook.save("output.xlsx")`. Αυτό το μοτίβο δύο γραμμών αποτελεί τη βάση για όλες τις επόμενες λειτουργίες.

#### Step 1: Create a Workbook  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```  
Αυτή η γραμμή δημιουργεί το αντικείμενο `Workbook`, παρέχοντάς σας πλήρη πρόσβαση σε φύλλα εργασίας, γραφήματα και κελιά.

#### Step 2: Save the Modified Workbook  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ModifiedData_out.xlsx");
```  
Αφού ολοκληρώσετε τις επεμβάσεις, καλέστε `save` για να γράψετε τις αλλαγές στο δίσκο.

### Πρόσβαση σε Φύλλο Εργασίας σε Βιβλίο Εργασίας Excel

**Επισκόπηση**: Ανακτήστε το συγκεκριμένο φύλλο εργασίας που περιέχει το γράφημα που θέλετε να επεξεργαστείτε.

#### Step 1: Access First Worksheet  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```  
Η κλάση `Worksheet` αντιπροσωπεύει ένα μόνο φύλλο· η πρόσβαση σε αυτή μέσω `getWorksheets().get(0)` σας δίνει το πρώτο φύλλο.

### Πρόσβαση και Τροποποίηση Γραφήματος σε Φύλλο Εργασίας

**Επισκόπηση**: Εντοπίστε το αντικείμενο γραφήματος μέσα στο φύλλο εργασίας και προετοιμάστε το για αλλαγές ετικετών.

#### Step 1: Access First Chart  
```java
Chart chart = worksheet.getCharts().get(0);
```  
Η κλάση `Chart` περιλαμβάνει όλες τις ιδιότητες σχετικές με το γράφημα. Μonce έχετε μια αναφορά, μπορείτε να τροποποιήσετε σειρές, άξονες και ετικέτες δεδομένων.

### Τροποποίηση Ετικετών Δεδομένων σε Σημείο Σειράς Γραφήματος

**Επισκόπηση**: Αλλάξτε το ορατό κείμενο μιας ετικέτας δεδομένων ώστε να εμφανίζει προσαρμοσμένες πληροφορίες.

`DataLabel` αντιπροσωπεύει την ετικέτα κειμένου που συνδέεται με ένα σημείο δεδομένων σε ένα γράφημα.

#### Step 1: Modify Data Label Text  
```java
DataLabels dlbls = chart.getNSeries().get(0).getPoints().get(0).getDataLabels();
dlbls.setText("Rich Text Label");
```  
Χρησιμοποιήστε `setText("Your custom label")` στο αντικείμενο `DataLabel` για να αντικαταστήσετε την προεπιλεγμένη τιμή.

### Προσαρμογή Ρυθμίσεων Γραμματοσειράς των Ετικετών Δεδομένων

**Επισκόπηση**: Εφαρμόστε έντονο στυλ, αλλαγές χρώματος και ρυθμίσεις μεγέθους γραμματοσειράς για να ξεχωρίζουν οι ετικέτες.

#### Step 1: Customize Font  
```java
FontSetting fntSetting = dlbls.characters(0, 10);
fntSetting.getFont().setColor(Color.getRed());
fntSetting.getFont().setBold(true);
```  
Η κλάση `Font` σας επιτρέπει να ορίσετε `setBold(true)`, `setColor(Color.getRed())` και άλλα χαρακτηριστικά για ακριβή οπτικό έλεγχο.

## Πώς να Αλλάξετε τις Ετικέτες Δεδομένων Γραφήματος σε Excel Χρησιμοποιώντας το Aspose.Cells;

Φορτώστε το βιβλίο εργασίας, ανακτήστε το επιθυμητό γράφημα, στη συνέχεια επαναλάβετε τα σημεία των σειρών του και καλέστε `setText` σε κάθε `DataLabel`. Τέλος, προσαρμόστε τις ιδιότητες `Font` της ετικέτας για να πετύχετε την επιθυμητή εμφάνιση. Αυτή η προσέγγιση λειτουργεί για οποιονδήποτε τύπο γραφήματος — στήλη, γραμμή, πίτα ή ραντάρ — και ενημερώνει όλες τις ετικέτες σε μία μόνο διεργασία.

## Συνηθισμένες Περιπτώσεις Χρήσης

- **Οικονομικοί Πίνακες Ελέγχου** – Ενημέρωση τριμηνιαίων στοιχείων αυτόματα καθώς φτάνουν νέα δεδομένα.  
- **Αναφορές Πωλήσεων** – Επισημάνετε τα κορυφαία προϊόντα με έντονη μορφή των ετικετών δεδομένων.  
- **Διαχείριση Έργων** – Εμφανίστε τα ποσοστά ολοκλήρωσης εργασιών απευθείας σε γραφήματα τύπου Gantt.  

## Σκέψεις Απόδοσης

Κατά την επεξεργασία μεγάλων βιβλίων εργασίας (200 + σελίδες), λάβετε υπόψη τις παρακάτω συμβουλές:

- Χρησιμοποιήστε `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` για να περιορίσετε τη χρήση RAM.  
- Κλείστε άμεσα το αντικείμενο `Workbook` με `workbook.dispose()` μετά την αποθήκευση.  
- Για λειτουργίες παρτίδας, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Workbook` όπου είναι δυνατόν για μείωση του φόρτου του GC.  

## Συχνές Ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω το Aspose.Cells για Java χωρίς πληρωμένη άδεια;**  
Α: Ναι, η δωρεάν δοκιμή παρέχει πλήρη λειτουργικότητα για ανάπτυξη και δοκιμές· απαιτείται εμπορική άδεια για παραγωγικές εγκαταστάσεις.

**Ε: Πώς το Aspose.Cells διαχειρίζεται μεγάλα αρχεία Excel;**  
Α: Μπορεί να επεξεργαστεί αρχεία άνω των 500 MB και πάνω από 100 + φύλλα εργασίας χρησιμοποιώντας λιγότερο από 300 MB RAM όταν ενεργοποιηθούν οι ρυθμίσεις βελτιστοποίησης μνήμης.

**Ε: Είναι δυνατόν να τροποποιήσω πολλαπλά γραφήματα σε ένα βιβλίο εργασίας;**  
Α: Απόλυτα – επαναλάβετε πάνω στο `worksheet.getCharts()` και εφαρμόστε την ίδια λογική αλλαγής ετικετών σε κάθε αντικείμενο γραφήματος.

**Ε: Ποια είναι τα πιο κοινά προβλήματα κατά την προσαρμογή ετικετών δεδομένων;**  
Α: Η παράλειψη κλήσης `setShowValue(true)` στη σειρά, ή η μη απελευθέρωση του βιβλίου εργασίας, μπορεί να οδηγήσει σε ελλιπείς ετικέτες ή διαρροές μνήμης.

**Ε: Μπορεί το Aspose.Cells να ενσωματωθεί με το Spring Boot;**  
Α: Ναι, απλώς προσθέστε την εξάρτηση Maven/Gradle και ενσωματώστε τον κώδικα διαχείρισης βιβλίου εργασίας σε ένα Spring service component.

## Πόροι

- [Aspose Documentation](https://reference.aspose.com/cells/java/)
- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase Aspose.Cells](https://purchase.aspose.com/buy)
- [Free Trial License](https://releases.aspose.com/cells/java/)
- [Temporary License Acquisition](https://purchase.aspose.com/temporary-license/)
- [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

Εξερευνήστε αυτούς τους συνδέσμους για να εμβαθύνετε τις γνώσεις σας και να ανακαλύψετε επιπλέον API σχετιζόμενα με γραφήματα.

---

**Last Updated:** 2026-06-22  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Πώς να Αυτο-Αλλάξετε το Μέγεθος των Ετικετών Δεδομένων Γραφήματος σε Excel Χρησιμοποιώντας το Aspose.Cells για Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Πώς να Προσθέσετε Ετικέτες σε Γραφήματα Excel Χρησιμοποιώντας το Aspose.Cells για Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Κατακτήστε το Aspose.Cells Java για Προσαρμογή Γραφημάτων Excel: Ένας Πλήρης Οδηγός](/cells/java/charts-graphs/aspose-cells-java-excel-charts-customization/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}