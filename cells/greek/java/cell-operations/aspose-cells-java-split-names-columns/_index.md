---
date: '2026-03-15'
description: Μάθετε πώς να χωρίζετε τα ονόματα σε ξεχωριστές στήλες και να αποθηκεύετε
  το βιβλίο εργασίας xlsx χρησιμοποιώντας το Aspose.Cells Java σε έναν βήμα‑βήμα οδηγό.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Διαχωρισμός Ονομάτων σε Στήλες
url: /el/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Κατακτώντας το **aspose cells java**: Διαχωρισμός Ονομάτων σε Στήλες

Καλώς ήρθατε στο ολοκληρωμένο μας **aspose cells java** tutorial. Σε αυτόν τον οδηγό θα μάθετε **πώς να διαχωρίζετε ονόματα** που αποθηκεύονται σε μία στήλη του Excel σε δύο ξεχωριστές στήλες—όνομα και επώνυμο—χρησιμοποιώντας τη δυνατότητα text‑to‑columns. Είτε καθαρίζετε μια λίστα επαφών, προετοιμάζετε δεδομένα για εισαγωγή σε CRM, είτε απλώς χρειάζεστε έναν γρήγορο τρόπο για να αναδιαρθρώσετε τα φύλλα εργασίας, αυτό το tutorial σας δείχνει ακριβώς πώς να **save workbook xlsx** μετά τον μετασχηματισμό.

## Γρήγορες Απαντήσεις
- **Τι καλύπτει αυτό το tutorial;** Διαχωρισμός αλφαριθμητικών πλήρων ονομάτων σε στήλες ονόματος και επωνύμου με το Aspose.Cells for Java.  
- **Ποια έκδοση της βιβλιοθήκης χρησιμοποιείται;** Η πιο πρόσφατη σταθερή έκδοση (από το 2026).  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να διαχωρίζω με άλλους διαχωριστές;** Ναι—απλώς αλλάξτε το διαχωριστικό στο `TxtLoadOptions`.  
- **Η έξοδος είναι αρχείο .xlsx;** Απόλυτα, το βιβλίο εργασίας αποθηκεύεται σε μορφή XLSX.

## Τι είναι το **aspose cells java**;
**Aspose.Cells java** είναι ένα υψηλής απόδοσης Java API που επιτρέπει στους προγραμματιστές να δημιουργούν, τροποποιούν, μετατρέπουν και αποδίδουν αρχεία Excel χωρίς την ανάγκη του Microsoft Office. Υποστηρίζει όλες τις κύριες μορφές Excel και παρέχει προηγμένες λειτουργίες όπως τύπους, διαγράμματα και διαχείριση δεδομένων.

## Γιατί να χρησιμοποιήσετε το **aspose cells java** για διαχωρισμό ονομάτων;
- **Zero‑install**: Λειτουργεί σε οποιοδήποτε περιβάλλον Java στο διακομιστή.  
- **Speed**: Διαχειρίζεται μεγάλα φύλλα εργασίας πιο γρήγορα από το εγγενές Excel interop.  
- **Precision**: Πλήρης έλεγχος πάνω στους διαχωριστές, τις περιοχές στήλης και τις μορφές εξόδου.  
- **Reliability**: Χωρίς εξαρτήσεις COM ή Office, καθιστώντας το ιδανικό για cloud ή container deployments.

## Προαπαιτούμενα
- Java Development Kit (JDK) 8 ή νεότερο.  
- Ένα IDE όπως IntelliJ IDEA ή Eclipse (προαιρετικό αλλά συνιστάται).  
- Maven ή Gradle για διαχείριση εξαρτήσεων.  

### Ρύθμιση Maven
Προσθέστε την εξάρτηση Aspose.Cells στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Ρύθμιση Gradle
Προσθέστε τη βιβλιοθήκη στο `build.gradle` σας:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Συμβουλή:** Χρησιμοποιήστε μια προσωρινή άδεια από το portal της Aspose για να ξεκλειδώσετε πλήρη λειτουργικότητα κατά την ανάπτυξη.

## Υλοποίηση Βήμα‑Βήμα

### Βήμα 1: Δημιουργία Βιβλίου Εργασίας και Πρόσβαση στο Πρώτο Φύλλο
Αρχικά, εισάγετε τις βασικές κλάσεις και δημιουργήστε ένα νέο βιβλίο εργασίας. Αυτό σας παρέχει ένα καθαρό αρχείο Excel έτοιμο για εισαγωγή δεδομένων.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Βήμα 2: Συμπλήρωση του Φύλλου με Δείγμα Ονομάτων
Στη συνέχεια, προσθέστε μερικά αλφαριθμητικά πλήρων ονομάτων στη στήλη **A**. Σε ένα πραγματικό έργο θα τα διαβάζατε από μια βάση δεδομένων ή αρχείο CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Βήμα 3: Ρύθμιση Text Load Options για Διαχωρισμό Στήλης
Η κλάση `TxtLoadOptions` ενημερώνει το Aspose.Cells πώς να ερμηνεύσει το κείμενο. Εδώ χρησιμοποιούμε ένα κενό (`' '`) ως διαχωριστικό.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Βήμα 4: Διαχωρισμός του Κειμένου σε Δύο Στήλες
Τώρα καλέστε τη μέθοδο `textToColumns()` στην περιοχή κελιών που περιέχει τα ονόματα. Οι παράμετροι `(0, 0, 5, opts)` σημαίνουν *αρχή στη γραμμή 0, στήλη 0, επεξεργασία 5 γραμμών, χρησιμοποιώντας τις επιλογές που ορίσαμε*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Μετά από αυτή την κλήση, η στήλη A περιέχει τα ονόματα και η στήλη B τα επώνυμα.

### Βήμα 5: Αποθήκευση του Βιβλίου Εργασίας ως Αρχείο XLSX
Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας στο δίσκο. Η απαρίθμηση `SaveFormat` εξασφαλίζει ότι το αρχείο αποθηκεύεται στη σύγχρονη μορφή XLSX.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Γιατί είναι σημαντικό:** Χρησιμοποιώντας το **save workbook xlsx**, εξασφαλίζετε συμβατότητα με τις πιο πρόσφατες εκδόσεις του Excel, του Google Sheets και άλλων εργαλείων λογιστικών φύλλων.

## Πρακτικές Εφαρμογές
- **Data Cleaning:** Γρήγορος διαχωρισμός συγκερασμένων πεδίων πριν τη φόρτωση σε pipelines ανάλυσης.  
- **CRM Integration:** Μετατροπή μιας επίπεδης λίστας επαφών σε δομημένο πίνακα για εισαγωγή.  
- **HR Systems:** Διαχωρισμός πλήρων ονομάτων υπαλλήλων για μισθοδοσία ή επεξεργασία παροχών.

## Παραμέτρους Απόδοσης
Κατά την εργασία με χιλιάδες γραμμές:

1. **Batch Updates:** Χρησιμοποιήστε `ws.getCells().setRowHeight()` ή παρόμοιες μεθόδους batch για μείωση του φόρτου.  
2. **Memory Management:** Καλέστε `wb.calculateFormula()` μόνο όταν είναι απαραίτητο και απελευθερώστε μεγάλα αντικείμενα άμεσα.  
3. **Garbage Collection:** Εκτελέστε το JVM με κατάλληλες ρυθμίσεις heap (`-Xmx2g` για μεγάλα αρχεία) για να αποφύγετε σφάλματα OutOfMemory.

## Κοινά Προβλήματα και Λύσεις

| Πρόβλημα | Λύση |
|----------|------|
| **Τα ονόματα περιέχουν μεσαία αρχικά** (π.χ., “John A. Doe”) | Προσαρμόστε το διαχωριστικό ή επεξεργαστείτε τη δεύτερη στήλη για να εξάγετε το επώνυμο. |
| **Απρόσμενα κενά κελιά** | Επαληθεύστε ότι η πηγή περιοχής (`textToColumns` parameters) ταιριάζει με τις πραγματικές γραμμές δεδομένων. |
| **Δεν βρέθηκε άδεια** | Τοποθετήστε το προσωρινό αρχείο άδειας (`Aspose.Cells.lic`) στη ρίζα του έργου ή ορίστε την άδεια προγραμματιστικά. |

## Συχνές Ερωτήσεις

**Ε: Τι είναι το Aspose.Cells Java;**  
A: Μια ισχυρή βιβλιοθήκη που σας επιτρέπει να δημιουργείτε, τροποποιείτε και μετατρέπετε αρχεία Excel προγραμματιστικά χρησιμοποιώντας Java.

**Ε: Μπορώ να διαχωρίζω στήλες βάσει διαχωριστών διαφορετικών από κενά;**  
A: Ναι, προσαρμόστε το διαχωριστικό του `TxtLoadOptions` όπως απαιτείται για τα δεδομένα σας.

**Ε: Πώς να διαχειριστώ μεγάλα σύνολα δεδομένων με το Aspose.Cells;**  
A: Βελτιστοποιήστε την απόδοση διαχειριζόμενοι τη μνήμη και ελαχιστοποιώντας τις λειτουργίες στο βιβλίο εργασίας, όπως περιγράφηκε παραπάνω.

**Ε: Υπάρχει υποστήριξη εάν αντιμετωπίσω προβλήματα;**  
A: Επισκεφθείτε το [Aspose Forum](https://forum.aspose.com/c/cells/9) για βοήθεια από την κοινότητα ή επικοινωνήστε απευθείας με την ομάδα υποστήριξης της Aspose.

**Ε: Σε ποιες μορφές μπορεί το Aspose.Cells να αποθηκεύει βιβλία εργασίας;**  
A: Υποστηρίζει μια ευρεία γκάμα μορφών αρχείων Excel, συμπεριλαμβανομένων των XLSX, XLS, CSV και άλλων.

## Πόροι

- **Τεκμηρίωση**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Λήψη**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Αγορά**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Δωρεάν Δοκιμή**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Προσωρινή Άδεια**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Καλή προγραμματιστική, και απολαύστε την αξιοποίηση της πλήρους δύναμης του **aspose cells java** στα έργα σας!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Τελευταία Ενημέρωση:** 2026-03-15  
**Δοκιμή Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose