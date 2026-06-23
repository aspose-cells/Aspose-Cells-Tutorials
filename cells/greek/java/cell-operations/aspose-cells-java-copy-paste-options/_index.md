---
date: '2026-02-22'
description: Μάθετε πώς να αυτοματοποιήσετε την αναφορά Excel με το Aspose.Cells σε
  Java χρησιμοποιώντας τις CopyOptions και PasteOptions για να διατηρήσετε τις φόρμουλες
  ακριβείς και να επικολλήσετε μόνο τις ορατές τιμές.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Αυτοματοποιήστε την αναφορά Excel – Κατακτώντας τις CopyOptions και PasteOptions
  σε Java με το Aspose.Cells
url: /el/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Αυτοματοποιήστε την Αναφορά Excel με Aspose.Cells: CopyOptions & PasteOptions σε Java

Αναζητάτε να **αυτοματοποιήσετε την αναφορά Excel** χρησιμοποιώντας Java; Με το Aspose.Cells μπορείτε προγραμματιστικά να αντιγράψετε, να επικολλήσετε και να προσαρμόσετε τύπους ώστε οι αναφορές σας να παραμένουν ακριβείς και να μεταφέρονται μόνο τα δεδομένα που χρειάζεστε. Σε αυτό το tutorial θα εξετάσουμε δύο βασικές λειτουργίες — **CopyOptions.ReferToDestinationSheet** και **PasteOptions** — που σας επιτρέπουν να διατηρήσετε τις αναφορές τύπων και να επικολλήσετε τιμές μόνο από ορατά κελιά.

## Γρήγορες Απαντήσεις
- **Τι κάνει το `CopyOptions.ReferToDestinationSheet`;** Προσαρμόζει τους τύπους ώστε να δείχνουν στο φύλλο προορισμού κατά την αντιγραφή δεδομένων.  
- **Πώς μπορώ να επικολλήσω μόνο ορατά κελιά;** Ορίστε `PasteOptions.setOnlyVisibleCells(true)` μαζί με `PasteType.VALUES`.  
- **Ποια έκδοση της βιβλιοθήκης απαιτείται;** Aspose.Cells 25.3 ή νεότερη.  
- **Χρειάζομαι άδεια για παραγωγική χρήση;** Ναι, μια μόνιμη ή προσωρινή άδεια αφαιρεί τους περιορισμούς αξιολόγησης.  
- **Μπορώ να χρησιμοποιήσω Maven ή Gradle;** Και οι δύο υποστηρίζονται· δείτε τα αποσπάσματα εξαρτήσεων παρακάτω.

## Τι σημαίνει “αυτοματοποιήστε την αναφορά Excel”;
Η αυτοματοποίηση της αναφοράς Excel σημαίνει τη δημιουργία, ενοποίηση και μορφοποίηση βιβλίων εργασίας Excel προγραμματιστικά, εξαλείφοντας τα χειροκίνητα βήματα αντιγραφής‑επικόλλησης και μειώνοντας τα σφάλματα. Το Aspose.Cells παρέχει ένα πλούσιο API που επιτρέπει στους προγραμματιστές Java να διαχειρίζονται λογιστικά φύλλα σε μεγάλη κλίμακα.

## Γιατί να χρησιμοποιήσετε CopyOptions και PasteOptions για αναφορές;
- **Διατήρηση της ακεραιότητας των τύπων** κατά τη μετακίνηση δεδομένων μεταξύ φύλλων.  
- **Αποκλεισμός κρυφών γραμμών/στηλών** για καθαρές και εστιασμένες αναφορές.  
- **Βελτίωση απόδοσης** αντιγράφοντας μόνο τα απαραίτητα δεδομένα αντί για ολόκληρες περιοχές.

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

### Απόκτηση Άδειας
- **Δωρεάν Δοκιμή** – Πλήρες σύνολο λειτουργιών για αξιολόγηση.  
- **Προσωρινή Άδεια** – Αφαιρεί τους περιορισμούς της δοκιμής ενώ δοκιμάζετε.  
- **Μόνιμη Άδεια** – Συνιστάται για παραγωγικά φορτία εργασίας.

Αρχικοποιήστε το Aspose.Cells στον κώδικά σας Java:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Οδηγός Βήμα‑Βήμα

### 1. CopyOptions με ReferToDestinationSheet

#### Επισκόπηση
Ορίζοντας το `CopyOptions.ReferToDestinationSheet` σε `true` επανεγγράφει τις αναφορές τύπων ώστε να δείχνουν στο νέο φύλλο μετά την ενέργεια αντιγραφής.

#### Βήμα 1: Αρχικοποίηση Workbook και Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Βήμα 2: Διαμόρφωση CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Βήμα 3: Εκτέλεση Λειτουργίας Αντιγραφής
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Γιατί είναι σημαντικό*: Οι τύποι που αρχικά αναφερόνταν στο `Sheet1` θα αναφέρονται τώρα σωστά στο `DestSheet`, διατηρώντας τις αυτοματοποιημένες αναφορές αξιόπιστες.

**Συμβουλή Επίλυσης Προβλήματος**: Εάν οι τύποι εξακολουθούν να αναφέρονται στο παλιό φύλλο, βεβαιωθείτε ότι το `setReferToDestinationSheet(true)` κλήθηκε **πριν** την αντιγραφή.

### 2. PasteOptions για Τιμές‑Μόνο από Ορατά Κελιά

#### Επισκόπηση
Το `PasteOptions` σας επιτρέπει να ορίσετε τι θα επικολληθεί. Χρησιμοποιώντας `PasteType.VALUES` μαζί με `onlyVisibleCells=true` αντιγράφει μόνο τις εμφανιζόμενες τιμές, αγνοώντας κρυφές γραμμές/στήλες και μορφοποίηση.

#### Βήμα 1: Αρχικοποίηση Workbook και Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Βήμα 2: Διαμόρφωση PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Βήμα 3: Εκτέλεση Λειτουργίας Επικόλλησης
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Γιατί είναι σημαντικό*: Ιδανικό για εξαγωγή φιλτραρισμένων δεδομένων ή δημιουργία καθαρών αναφορών χωρίς κρυφές γραμμές ή θόρυβο μορφοποίησης.

**Συμβουλή Επίλυσης Προβλήματος**: Βεβαιωθείτε ότι οι γραμμές/στήλες είναι πράγματι κρυμμένες στο Excel πριν την αντιγραφή· διαφορετικά θα συμπεριληφθούν.

## Πρακτικές Εφαρμογές
1. **Οικονομική Ενοποίηση** – Συγχώνευση μηνιαίων φύλλων σε ένα κύριο βιβλίο εργασίας διατηρώντας όλους τους τύπους ακριβείς.  
2. **Εξαγωγή Φιλτραρισμένων Δεδομένων** – Ανάκτηση μόνο των ορατών γραμμών από έναν φιλτραρισμένο πίνακα σε ένα φύλλο σύνοψης.  
3. **Προγραμματισμένη Δημιουργία Αναφορών** – Αυτοματοποιήστε τη νυχτερινή δημιουργία αναφορών Excel με ακριβείς τιμές κελιών και σωστές αναφορές.

## Σκέψεις για την Απόδοση
- **Καταστροφή Workbooks** όταν τελειώσετε (`wb.dispose();`) για απελευθέρωση εγγενών πόρων.  
- **Ομαδικές Λειτουργίες** – Ομαδοποιήστε πολλαπλές κλήσεις copy/paste για μείωση του κόστους.  
- **Παρακολούθηση Μνήμης** – Μεγάλα βιβλία εργασίας μπορεί να απαιτούν αυξημένο heap (`-Xmx2g`).

## Συχνές Ερωτήσεις

**Q1: Για τι χρησιμοποιείται το `CopyOptions.ReferToDestinationSheet`;**  
A: Επανεγγράφει τις αναφορές τύπων ώστε να δείχνουν στο φύλλο προορισμού μετά την αντιγραφή, διασφαλίζοντας ότι οι τύποι αναφοράς παραμένουν σωστοί.

**Q2: Πώς επικολλώ μόνο ορατά κελιά;**  
A: Ορίστε `PasteOptions.setOnlyVisibleCells(true)` και επιλέξτε `PasteType.VALUES`.

**Q3: Μπορώ να χρησιμοποιήσω το Aspose.Cells χωρίς αγορά άδειας;**  
A: Ναι, υπάρχει δωρεάν δοκιμή ή προσωρινή άδεια για αξιολόγηση, αλλά απαιτείται μόνιμη άδεια για παραγωγική χρήση.

**Q4: Γιατί κάποιες αναφορές παραμένουν λανθασμένες μετά την αντιγραφή;**  
A: Ελέγξτε ξανά ότι το `ReferToDestinationSheet` είναι ενεργοποιημένο **πριν** την αντιγραφή και ότι οι τύποι πηγής δεν περιέχουν εξωτερικούς συνδέσμους βιβλιοθηκών.

**Q5: Ποιες βέλτιστες πρακτικές διαχείρισης μνήμης πρέπει να ακολουθήσω;**  
A: Καταστρέψτε τα αντικείμενα `Workbook` όταν τελειώσετε, επεξεργαστείτε μεγάλα αρχεία σε τμήματα και παρακολουθείτε τη χρήση heap της JVM.

**Q6: Είναι δυνατόν να συνδυάσω CopyOptions και PasteOptions σε μία λειτουργία;**  
A: Ναι, μπορείτε να τα αλυσίδετε πρώτα με την αντιγραφή χρησιμοποιώντας `CopyOptions` και στη συνέχεια να εφαρμόσετε `PasteOptions` στην περιοχή προορισμού.

## Πόροι
- **Τεκμηρίωση**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Λήψη**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Αγορά**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Δωρεάν Δοκιμή**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Προσωρινή Άδεια**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Φόρουμ Υποστήριξης**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Τελευταία Ενημέρωση:** 2026-02-22  
**Δοκιμάστηκε Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose