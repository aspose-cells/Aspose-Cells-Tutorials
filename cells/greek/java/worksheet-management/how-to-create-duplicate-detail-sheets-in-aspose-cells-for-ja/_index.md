---
category: general
date: 2026-08-17
description: Μάθετε πώς να δημιουργείτε διπλότυπα φύλλα λεπτομερειών με το Aspose.Cells
  για Java και να επιτρέπετε διπλότυπα ονόματα φύλλων χρησιμοποιώντας το SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: el
lastmod: 2026-08-17
og_description: Δημιουργήστε αντίγραφα φύλλων λεπτομερειών στο Aspose.Cells για Java
  και επιτρέψτε διπλότυπα ονόματα φύλλων. Ακολουθήστε αυτό το πλήρες σεμινάριο για
  άμεσα αποτελέσματα.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Δημιουργήστε αντίγραφα φύλλων λεπτομερειών στο Aspose.Cells for Java – οδηγός
  βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Πώς να δημιουργήσετε αντίγραφα φύλλα λεπτομερειών στο Aspose.Cells για Java
url: /el/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε αντίγραφα φύλλων λεπτομερειών στο Aspose.Cells για Java

Εάν χρειάζεται να **δημιουργήσετε αντίγραφα φύλλων λεπτομερειών** σε ένα βιβλίο εργασίας Excel, το Aspose.Cells για Java το καθιστά απλό. Αυτό το σεμινάριο δείχνει ακριβώς πώς να επιτρέψετε διπλότυπα ονόματα φύλλων κατά τη δημιουργία φύλλων λεπτομερειών με το SmartMarkerProcessor, ώστε να μπορείτε να παραγάγετε ένα βιβλίο εργασίας που περιέχει πολλά φύλλα με το ίδιο όνομα.

Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα, ανάλυση κάθε επιλογής διαμόρφωσης και συμβουλές για την αντιμετώπιση κοινών περιπτώσεων όπως συγκρούσεις ονομάτων και μεγάλα σύνολα δεδομένων. Δεν απαιτούνται εξωτερικές αναφορές — όλα όσα χρειάζεστε περιλαμβάνονται στον κώδικα παρακάτω.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Java Development Kit (JDK) 8 ή νεότερο.
* Maven ή Gradle για τη διαχείριση εξαρτήσεων.
* Βιβλιοθήκη Aspose.Cells για Java (έκδοση 23.9 ή νεότερη). Προσθέστε την ακόλουθη εξάρτηση Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Ένα κύριο πρότυπο βιβλίου εργασίας (`master_template.xlsx`) που περιέχει μια περιοχή Smart Marker για τα δεδομένα λεπτομερειών.

## Επισκόπηση της λύσης

Η λύση ακολουθεί τέσσερα λογικά βήματα:

1. Φόρτωση του κύριου προτύπου βιβλίου εργασίας.
2. Διαμόρφωση του `SmartMarkerProcessor` ώστε **να επιτρέπει διπλότυπα ονόματα φύλλων**.
3. Επεξεργασία του βιβλίου εργασίας ώστε να δημιουργείται ένα νέο φύλλο λεπτομερειών για κάθε ομάδα δεδομένων.
4. Αποθήκευση του προκύπτοντος βιβλίου εργασίας που τώρα περιέχει διπλότυπα φύλλα λεπτομερειών.

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω, και το πλήρες αρχείο πηγαίου κώδικα παρέχεται στο τέλος του οδηγού.

## Βήμα 1: Φόρτωση του κύριου προτύπου βιβλίου εργασίας

Η πρώτη ενέργεια δημιουργεί μια παρουσία `Workbook` που αντιπροσωπεύει το αρχείο προτύπου. Το πρότυπο πρέπει να περιέχει έναν placeholder Smart Marker (π.χ., `&=DetailData`) που υποδεικνύει στον επεξεργαστή πού να εισάγει τα δεδομένα.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του προτύπου απομονώνει τη διάταξη και τη μορφοποίηση από τη λογική δημιουργίας δεδομένων, διατηρώντας τον κώδικά σας καθαρό και επιτρέποντας την επαναχρησιμοποίηση του ίδιου προτύπου για διαφορετικά σύνολα δεδομένων.

## Βήμα 2: Διαμόρφωση SmartMarkerProcessor για να επιτρέπει διπλότυπα ονόματα φύλλων

Από προεπιλογή, το Aspose.Cells δημιουργεί μοναδικά ονόματα φύλλων όταν παράγει φύλλα λεπτομερειών. Για να **επιτρέψετε διπλότυπα ονόματα φύλλων**, ορίστε την επιλογή `DetailSheetNewName` σε μια σταθερή τιμή. Ο επεξεργαστής θα επαναχρησιμοποιήσει αυτό το όνομα για κάθε παραγόμενο φύλλο.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Γιατί είναι σημαντικό:** Η ρύθμιση του `DetailSheetNewName` λέει στη μηχανή να χρησιμοποιεί το ίδιο όνομα για κάθε φύλλο λεπτομερειών, ικανοποιώντας άμεσα την απαίτηση για **επιτρέψιμα διπλότυπα ονόματα φύλλων**. Αυτή η προσέγγιση είναι χρήσιμη όταν τα επόμενα εργαλεία αναγνωρίζουν τα φύλλα με βάση τη θέση τους αντί για το όνομα.

## Βήμα 3: Επεξεργασία του βιβλίου εργασίας για τη δημιουργία των φύλλων λεπτομερειών

Μετά τη διαμόρφωση, καλέστε `process` στο βιβλίο εργασίας. Ο επεξεργαστής διαβάζει την περιοχή Smart Marker, δημιουργεί ένα νέο φύλλο για κάθε ομάδα δεδομένων και το γεμίζει με τις αντίστοιχες γραμμές.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Γιατί είναι σημαντικό:** Η κλήση `process` εκτελεί το βαρέως τύπου έργο — την ανάλυση των Smart Markers, την κλωνοποίηση του φύλλου προτύπου και την εισαγωγή των δεδομένων. Επειδή η επιλογή `DetailSheetNewName` είναι ήδη ορισμένη, κάθε νέο φύλλο λαμβάνει το ίδιο όνομα, δημιουργώντας διπλότυπα ονόματα φύλλων στο τελικό αρχείο.

## Βήμα 4: Αποθήκευση του προκύπτοντος βιβλίου εργασίας

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας σε νέο αρχείο. Το αρχείο εξόδου θα περιέχει τόσες καρτέλες “DetailSheet” όσα είναι τα σύνολα δεδομένων.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Γιατί είναι σημαντικό:** Η αποθήκευση του αρχείου ολοκληρώνει τις αλλαγές που έκαναν ο επεξεργαστής. Το προκύπτον βιβλίο εργασίας μπορεί να ανοιχθεί στο Microsoft Excel, LibreOffice ή οποιαδήποτε άλλη εφαρμογή υπολογιστικών φύλλων που υποστηρίζει τη μορφή XLSX.

## Πλήρης πηγαίος κώδικας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Αναμενόμενη έξοδος

Όταν ανοίξετε το `duplicate_detail.xlsx`, θα δείτε πολλαπλές καρτέλες με όνομα **DetailSheet**. Κάθε καρτέλα περιέχει το σύνολο δεδομένων που αντιστοιχούσε σε μια συγκεκριμένη ομάδα Smart Marker στο πρότυπο. Η διάταξη, η μορφοποίηση και οι τύποι από το κύριο πρότυπο διατηρούνται σε κάθε αντίγραφο φύλλου.

## Αντιμετώπιση κοινών προβλημάτων

| Πρόβλημα | Εξήγηση | Λύση |
|----------|---------|------|
| Το Excel εμφανίζει προειδοποίηση για διπλότυπα ονόματα φύλλων | Το Excel επιτρέπει διπλότυπα ονόματα αλλά μπορεί να εμφανίσει προειδοποίηση κατά το άνοιγμα του αρχείου. | Η προειδοποίηση είναι αβλαβής· το βιβλίο εργασίας λειτουργεί σωστά. Εάν προτιμάτε να την καταστέλλετε, μετονομάστε τα φύλλα μετά την επεξεργασία χρησιμοποιώντας `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Μεγάλα σύνολα δεδομένων προκαλούν υψηλή χρήση μνήμης | Κάθε αντίγραφο φύλλου δημιουργεί ένα πλήρες αντίγραφο του προτύπου, κάτι που μπορεί να καταναλώσει RAM. | Ενεργοποιήστε τη λειτουργία streaming με `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` πριν φορτώσετε το πρότυπο. |
| Δεν βρέθηκε η περιοχή Smart Marker | Ο επεξεργαστής δεν μπορεί να εντοπίσει το `&=DetailData` στο πρότυπο. | Βεβαιωθείτε ότι η σύνταξη του placeholder ταιριάζει με την πηγή δεδομένων και ότι το φύλλο προτύπου δεν είναι κρυφό. |

## Επαγγελματική συμβουλή: προσαρμογή του σχήματος ονοματοδοσίας των διπλότυπων

Εάν χρειάζεστε ένα προβλέψιμο μοτίβο ονοματοδοσίας ενώ εξακολουθείτε να επιτρέπετε διπλότυπα, συνδυάστε ένα βασικό όνομα με έναν δείκτη:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Ο placeholder `{0}` αντικαθίσταται από τον δείκτη του φύλλου, παράγοντας ονόματα όπως `DetailSheet_1`, `DetailSheet_2`, κ.λπ. Αυτό εξακολουθεί να ικανοποιεί την απαίτηση **να επιτρέπονται διπλότυπα ονόματα φύλλων** επειδή το βασικό όνομα παραμένει σταθερό.

## Επόμενα βήματα

Τώρα που μπορείτε να **δημιουργήσετε αντίγραφα φύλλων λεπτομερειών**, μπορείτε να εξερευνήσετε τα παρακάτω θέματα:

* **Γέμισμα φύλλων λεπτομερειών με εικόνες** – χρησιμοποιήστε αντικείμενα `Picture` για την ενσωμάτωση λογοτύπων ή διαγραμμάτων.
* **Εφαρμογή υπό συνθήκη μορφοποίησης** – προσθέστε κανόνες `FormatCondition` για την επισήμανση γραμμών βάσει τιμών.
* **Εξαγωγή σε PDF** – καλέστε `workbook.save("output.pdf", SaveFormat.PDF);` για να δημιουργήσετε μια έκδοση PDF των διπλότυπων φύλλων.

Κάθε μία από αυτές τις επεκτάσεις βασίζεται στην ίδια ροή εργασίας Smart Marker που παρουσιάστηκε εδώ, επιτρέποντάς σας να αυτοματοποιήσετε σύνθετες εργασίες αναφοράς σε Excel με σιγουριά.

---

*Έχετε μάθει πώς να δημιουργήσετε αντίγραφα φύλλων λεπτομερειών στο Aspose.Cells για Java και πώς να επιτρέψετε διπλότυπα ονόματα φύλλων χρησιμοποιώντας το SmartMarkerProcessor. Εφαρμόστε τον κώδικα, προσαρμόστε το πρότυπο και ενσωματώστε την τεχνική στις διαδικασίες αναφοράς σας.*

## Τι θα μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}