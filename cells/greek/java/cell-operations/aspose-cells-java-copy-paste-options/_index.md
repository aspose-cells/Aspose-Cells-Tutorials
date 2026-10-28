---
date: '2026-10-28'
description: Μάθετε πώς να επικολλήσετε τιμές χρησιμοποιώντας τις επιλογές αντιγραφής
  και επικόλλησης του Aspose.Cells στη Java, με κώδικα βήμα‑βήμα, ρύθμιση εξαρτήσεων
  Maven και συμβουλές αδειοδότησης.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Μάθετε πώς να επικολλήσετε τιμές χρησιμοποιώντας τις επιλογές αντιγραφής
  και επικόλλησης του Aspose.Cells στη Java, με κώδικα βήμα‑βήμα, ρύθμιση εξαρτήσεων
  Maven και συμβουλές αδειοδότησης.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Πώς να επικολλήσετε τιμές με τις επιλογές αντιγραφής και επικόλλησης του
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Πώς να επικολλήσετε τιμές με τις επιλογές αντιγραφής και επικόλλησης του Aspose.Cells
url: /el/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να επικολλήσετε τιμές με τις επιλογές αντιγραφής και επικόλλησης του Aspose.Cells

Η αυτοματοποίηση της αναφοράς Excel σε Java σημαίνει ότι μπορείτε να δημιουργήσετε, ενοποιήσετε και μορφοποιήσετε βιβλία εργασίας χωρίς ποτέ να ανοίξετε το Excel χειροκίνητα. Με το **Aspose.Cells** έχετε πλήρη έλεγχο των τύπων, των κρυφών γραμμών και των τιμών κελιών, ώστε οι αναφορές σας να παραμένουν ακριβείς και ελαφριές. Σε αυτό το σεμινάριο θα μάθετε πώς να χρησιμοποιείτε το **CopyOptions.ReferToDestinationSheet** για να διατηρείτε σωστούς τους τύπους και το **PasteOptions** για να επικολλάτε μόνο τις ορατές τιμές που χρειάζεστε.

## Γρήγορες απαντήσεις
- **What does `CopyOptions.ReferToDestinationSheet` do?** Επαναγράφει τους τύπους ώστε να δείχνουν στο φύλλο προορισμού μετά από μια λειτουργία αντιγραφής.  
- **How can I paste only visible cells?** Καλέστε `PasteOptions.setOnlyVisibleCells(true)` μαζί με `PasteType.VALUES`.  
- **Which library version is required?** Aspose.Cells 25.3 ή νεότερη.  
- **Do I need a license for production?** Ναι – μια μόνιμη ή προσωρινή άδεια αφαιρεί τους περιορισμούς αξιολόγησης.  
- **Can I use Maven or Gradle?** Και τα δύο υποστηρίζονται· δείτε τα αποσπάσματα εξαρτήσεων παρακάτω.

## Τι σημαίνει «αυτοματοποίηση αναφοράς Excel»;
Η αυτοματοποίηση της αναφοράς Excel σημαίνει τη δημιουργία και ενημέρωση βιβλίων εργασίας Excel προγραμματιστικά, επιτρέποντάς σας να δημιουργείτε, συγχωνεύετε και μορφοποιείτε αναφορές χωρίς χειροκίνητη αντιγραφή‑επικόλληση, κάτι που μειώνει τα λάθη και εξοικονομεί ώρες επαναλαμβανόμενης εργασίας. Αυτή η προσέγγιση είναι ιδανική για προγραμματισμένες παρτίδες εργασιών, πίνακες ελέγχου που βασίζονται σε δεδομένα και αγωγούς οικονομικής ενοποίησης.

## Γιατί να χρησιμοποιήσετε CopyOptions και PasteOptions για αναφορές;
Αυτές οι δύο κλάσεις σας επιτρέπουν να διατηρείτε αμετάβλητες τις αναφορές τύπων κατά την αντιγραφή δεδομένων **και** να εξάγετε μόνο τα κελιά που είναι ορατά μετά από φιλτράρισμα ή απόκρυψη γραμμών. Η ταυτόχρονη χρήση τους μειώνει την ποσότητα των μεταφερόμενων δεδομένων έως και 80 % σε τυπικά σενάρια φιλτραρισμένων πινάκων και εγγυάται ότι οι τύποι συνεχίζουν να υπολογίζονται σωστά στο φύλλο προορισμού.

## Προαπαιτούμενα
- Java 8 ή νεότερη.  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  
- Aspose.Cells 25.3+ (δοκιμαστική, προσωρινή ή μόνιμη άδεια).  

## Ρύθμιση Aspose.Cells για Java

Προσθέστε τη βιβλιοθήκη στο έργο σας με μία από τις παρακάτω επιλογές:

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
implementation 'com.aspose:aspose-cells:25.3'
```

### Απόκτηση άδειας
- **Free trial** – πλήρες σύνολο λειτουργιών για αξιολόγηση.  
- **Temporary license** – αφαιρεί τους περιορισμούς της δοκιμής ενώ δοκιμάζετε.  
- **Permanent license** – συνιστάται για παραγωγικά φορτία εργασίας.

Αρχικοποιήστε το Aspose.Cells στον κώδικα Java:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Οδηγός βήμα‑βήμα

### 1. copyOptions με referToDestinationSheet

#### Επισκόπηση
`CopyOptions` είναι το αντικείμενο διαμόρφωσης του Aspose.Cells που ελέγχει πώς οι τύποι και οι αναφορές κελιών διαχειρίζονται κατά τη διάρκεια μιας λειτουργίας αντιγραφής. Ορίζοντας το `CopyOptions.ReferToDestinationSheet` σε `true` επαναγράφει τις αναφορές τύπων ώστε να δείχνουν στο νέο φύλλο μετά την αντιγραφή.

#### Βήμα 1: αρχικοποίηση βιβλίου εργασίας και φύλλων εργασίας  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Βήμα 2: διαμόρφωση copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Βήμα 3: εκτέλεση λειτουργίας αντιγραφής  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Γιατί είναι σημαντικό*: Οι τύποι που αρχικά αναφέρονταν στο `Sheet1` θα αναφέρονται τώρα σωστά στο `DestSheet`, διατηρώντας τις αυτοματοποιημένες αναφορές σας αξιόπιστες.

**Συμβουλή αντιμετώπισης προβλημάτων**: Εάν οι τύποι εξακολουθούν να αναφέρονται στο παλιό φύλλο, βεβαιωθείτε ότι το `setReferToDestinationSheet(true)` καλείται **πριν** την αντιγραφή.

### 2. pasteOptions για τιμές‑μόνο από ορατά κελιά

#### Επισκόπηση
`PasteOptions` είναι το αντικείμενο ρυθμίσεων του Aspose.Cells που ορίζει τι θα επικολληθεί. Χρησιμοποιώντας το `PasteType.VALUES` μαζί με `onlyVisibleCells=true` αντιγράφει μόνο τις εμφανιζόμενες τιμές, αγνοώντας κρυφές γραμμές/στήλες και μορφοποίηση.

#### Βήμα 1: αρχικοποίηση βιβλίου εργασίας και φύλλων εργασίας  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Βήμα 2: διαμόρφωση pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Βήμα 3: εκτέλεση λειτουργίας επικόλλησης  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Γιατί είναι σημαντικό*: Ιδανικό για εξαγωγή φιλτραρισμένων δεδομένων ή δημιουργία καθαρών αναφορών χωρίς κρυφές γραμμές ή θόρυβο μορφοποίησης.

**Συμβουλή αντιμετώπισης προβλημάτων**: Επαληθεύστε ότι οι γραμμές/στήλες είναι πραγματικά κρυμμένες στο Excel πριν την αντιγραφή· διαφορετικά, θα συμπεριληφθούν.

## Πρακτικές εφαρμογές
1. **Financial consolidation** – συγχωνεύστε μηνιαία φύλλα σε ένα κύριο βιβλίο εργασίας διατηρώντας όλους τους τύπους ακριβείς.  
2. **Filtered data export** – εξάγετε μόνο τις ορατές γραμμές από έναν φιλτραρισμένο πίνακα σε ένα φύλλο σύνοψης.  
3. **Scheduled report generation** – αυτοματοποιήστε τη νυχτερινή δημιουργία αναφορών Excel με ακριβείς τιμές κελιών και σωστές αναφορές.

## Σκέψεις απόδοσης
- **Dispose of workbooks** when done (`wb.dispose();`) to free native resources.  
- **Batch operations** – group multiple copy/paste calls to reduce overhead.  
- **Monitor memory** – large workbooks may require increased heap (`-Xmx2g`).  
- Aspose.Cells supports **50+ input and output formats** and can process workbooks with **up to 2 million rows** without loading the entire file into memory, delivering high‑throughput performance for enterprise workloads.

## Συχνές ερωτήσεις

**Q: What is `CopyOptions.ReferToDestinationSheet` used for?**  
A: Επαναγράφει τις αναφορές τύπων ώστε να δείχνουν στο φύλλο προορισμού μετά από αντιγραφή, διασφαλίζοντας ότι οι τύποι αναφοράς παραμένουν σωστοί.

**Q: How do I paste only visible cells?**  
A: Ορίστε `PasteOptions.setOnlyVisibleCells(true)` και επιλέξτε `PasteType.VALUES`.

**Q: Can I use Aspose.Cells without purchasing a license?**  
A: Ναι, είναι διαθέσιμη δοκιμαστική ή προσωρινή άδεια για αξιολόγηση, αλλά απαιτείται μόνιμη άδεια για παραγωγή.

**Q: Why are some references still wrong after copying?**  
A: Ελέγξτε ξανά ότι το `ReferToDestinationSheet` είναι ενεργοποιημένο **πριν** τη λειτουργία αντιγραφής και ότι οι τύποι προέλευσης δεν περιέχουν εξωτερικές συνδέσεις βιβλίου εργασίας.

**Q: What memory‑management best practices should I follow?**  
A: Αποδεσμεύστε τα αντικείμενα `Workbook` όταν τελειώσετε, επεξεργαστείτε μεγάλα αρχεία σε τμήματα και παρακολουθήστε τη χρήση της μνήμης heap της JVM.

**Q: Is it possible to combine CopyOptions and PasteOptions in one operation?**  
A: Ναι, μπορείτε να τα συνδυάσετε πρώτα κάνοντας αντιγραφή με `CopyOptions` και στη συνέχεια εφαρμόζοντας `PasteOptions` στην περιοχή προορισμού.

## Πόροι
- **Τεκμηρίωση**: [Αναφορά Aspose.Cells Java](https://reference.aspose.com/cells/java/)  
- **Λήψη**: [Ανακοινώσεις Aspose.Cells για Java](https://releases.aspose.com/cells/java/)  
- **Αγορά**: [Αγορά Aspose.Cells](https://purchase.aspose.com/buy)  
- **Δωρεάν δοκιμή**: [Δωρεάν δοκιμή Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Προσωρινή άδεια**: [Αίτηση για προσωρινή άδεια](https://purchase.aspose.com/temporary-license/)  
- **Φόρουμ υποστήριξης**: [Υποστήριξη Aspose](https://forum.aspose.com/c/cells)

---

**Τελευταία ενημέρωση:** 2026-10-28  
**Δοκιμή με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose

## Σχετικά Σεμινάρια

- [Διαβάστε αρχείο Excel Java – Διαχείριση κελιών κύριου βιβλίου εργασίας με Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Προσθήκη δεδομένων σε κελί στο Excel χρησιμοποιώντας Aspose.Cells για Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Μετατροπή δεικτών γραμμής-στήλης κελιού Excel με Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}