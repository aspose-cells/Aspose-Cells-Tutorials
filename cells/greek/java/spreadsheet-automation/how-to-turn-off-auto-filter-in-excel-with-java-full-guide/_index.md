---
category: general
date: 2026-06-18
description: Πώς να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel χρησιμοποιώντας
  Java. Μάθετε πώς να αφαιρέσετε το αυτόματο φίλτρο στο Excel, να απενεργοποιήσετε
  το φίλτρο πίνακα του Excel και να διαγράψετε τα αναπτυσσόμενα μενού του πίνακα σε
  δευτερόλεπτα.
draft: false
keywords:
- how to turn off auto filter
- remove auto filter excel
- excel workbook disable filter
- disable excel table filter
- remove excel table dropdowns
language: el
og_description: Πώς να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel με Java. Αυτός
  ο οδηγός βήμα‑βήμα σας δείχνει πώς να αφαιρέσετε το αυτόματο φίλτρο στο Excel, να
  απενεργοποιήσετε το φίλτρο πίνακα του Excel και να καθαρίσετε τις αναπτυσσόμενες
  λίστες.
og_title: Πώς να απενεργοποιήσετε το Αυτόματο Φίλτρο στο Excel – Εκμάθηση Java
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to turn off auto filter in Excel using Java. Learn to remove auto
    filter excel, disable excel table filter, and erase table dropdowns in seconds.
  headline: How to Turn Off Auto Filter in Excel with Java – Full Guide
  type: TechArticle
- description: How to turn off auto filter in Excel using Java. Learn to remove auto
    filter excel, disable excel table filter, and erase table dropdowns in seconds.
  name: How to Turn Off Auto Filter in Excel with Java – Full Guide
  steps:
  - name: Open `noFilter.xlsx` in Excel.
    text: Open `noFilter.xlsx` in Excel.
  - name: Verify that **no auto‑filter dropdowns** appear on any table.
    text: Verify that **no auto‑filter dropdowns** appear on any table.
  - name: Check that all data, formulas, and formatting remain unchanged.
    text: Check that all data, formulas, and formatting remain unchanged.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells auto‑detects the format, so the same code works
      for both `.xlsx` and legacy `.xls`.
    question: Does this work with `.xls` files?
  - answer: Use `table.getAutoFilter().clearFilter();` instead of `setShowAutoFilter(false)`.
      This **remove excel table dropdowns** only clears the applied filter, leaving
      the UI intact.
    question: What if I need to keep the filter but just clear the criteria?
  - answer: Yes. Aspose.Cells is a pure Java library and does not require Excel to
      be installed. --- That’s it! You now know **how to turn off auto filter** in
      Excel, how to **remove auto filter excel**, and how to **excel workbook disable
      filter** programmatically. Go ahead, integrate it into your next reporti
    question: Can I run this on a server without a GUI?
  type: FAQPage
tags:
- Excel
- Java
- Aspose.Cells
- Automation
title: Πώς να απενεργοποιήσετε το Auto Filter στο Excel με Java – Πλήρης Οδηγός
url: /el/java/spreadsheet-automation/how-to-turn-off-auto-filter-in-excel-with-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Απενεργοποιήσετε το Αυτόματο Φίλτρο στο Excel με Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να απενεργοποιήσετε το αυτόματο φίλτρο** σε ένα βιβλίο εργασίας του Excel χωρίς να ανοίξετε το αρχείο χειροκίνητα; Δεν είστε ο μόνος. Σε πολλές αυτοματοποιημένες διαδικασίες χρειάζεται να *αφαιρέσουμε τις γραμμές με αυτόματο φίλτρο στο Excel*, να καθαρίσουμε τα βέλη των πτυσσόμενων λιστών ή απλώς να παραδώσουμε ένα καθαρό αντίγραφο μιας αναφοράς. Τα καλά νέα; Με λίγες γραμμές Java μπορείτε να απενεργοποιήσετε το φίλτρο σε οποιονδήποτε πίνακα, και το αποτέλεσμα είναι ένα τακτοποιημένο φύλλο εργασίας έτοιμο για διανομή.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **να απενεργοποιήσετε το αυτόματο φίλτρο** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells for Java. Θα καλύψουμε επίσης πώς να **αφαιρέσετε τα πτυσσόμενα μενού των πινάκων Excel**, γιατί μπορεί να θέλετε να **απενεργοποιήσετε το φίλτρο σε ένα βιβλίο εργασίας Excel** πριν τη δημοσίευση, και μερικά κόλπα για ειδικές περιπτώσεις. Χωρίς περιττές πληροφορίες—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο έργο σας σήμερα.

> **Συμβουλή επαγγελματία:** Αν ήδη χρησιμοποιείτε Maven ή Gradle, η προσθήκη του Aspose.Cells είναι παιχνιδάκι—απλώς προσθέστε την εξάρτηση και είστε έτοιμοι.

---

## Τι Θα Χρειαστεί

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) – ο κώδικας λειτουργεί και σε παλαιότερες εκδόσεις, αλλά η Java 17 είναι η ιδανική.
- **Aspose.Cells for Java** – μια ισχυρή βιβλιοθήκη που σας επιτρέπει να χειρίζεστε αρχεία Excel χωρίς το Microsoft Office. Μπορείτε να την αποκτήσετε από το Maven Central:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

- Ένα δείγμα βιβλίου εργασίας (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα με εφαρμοσμένο αυτόματο φίλτρο.
- Ένα IDE ή έναν απλό επεξεργαστή κειμένου—Visual Studio Code, IntelliJ IDEA, Eclipse, ό,τι προτιμάτε.

Αυτό είναι. Είστε έτοιμοι; Ας ξεκινήσουμε.

---

## Πώς να Απενεργοποιήσετε το Αυτόματο Φίλτρο στο Excel – Βήμα‑Βήμα

Παρακάτω βρίσκεται το **πλήρες, αυτόνομο πρόγραμμα Java** που φορτώνει ένα βιβλίο εργασίας, απενεργοποιεί το φίλτρο στον πρώτο πίνακα και αποθηκεύει ένα καθαρό αντίγραφο. Μπορείτε ελεύθερα να το αντιγράψετε σε ένα αρχείο `Main.java` και να το εκτελέσετε.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Load the workbook (replace YOUR_DIRECTORY with your path)
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // ---------------------------------------------------------------
        // Step 2: Grab the first worksheet and then the first table inside it
        // ---------------------------------------------------------------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Table table = sheet.getTables().get(0);

        // -----------------------------------------------------------------
        // Step 3: Disable the auto‑filter (removes dropdown arrows)
        // -----------------------------------------------------------------
        // This call turns off the filter UI and also clears any applied filter criteria.
        table.setShowAutoFilter(false);

        // -----------------------------------------------------------------
        // Step 4: Save the modified workbook to a new file
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("Auto‑filter removed successfully!");
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **`Workbook`** είναι το σημείο εισόδου για οποιοδήποτε αρχείο Excel. Αποτυπώνει ολόκληρη τη δομή του βιβλίου εργασίας, καθιστώντας εύκολη την πλοήγηση σε φύλλα, πίνακες και κελιά.
- Τα αντικείμενα **`Table`** αντιπροσωπεύουν πίνακες Excel (το δομημένο εύρος που λαμβάνετε όταν πατάτε **Ctrl + T**). Η μέθοδος `setShowAutoFilter(false)` κρύβει τα πτυσσόμενα μενού του φίλτρου *και* αφαιρεί τυχόν ενεργά κριτήρια φίλτρου, εκτελώντας ουσιαστικά μια λειτουργία **απενεργοποίησης φίλτρου πίνακα Excel**.
- Η **αποθήκευση** σε νέο αρχείο διασφαλίζει ότι τα αρχικά σας δεδομένα παραμένουν αμετάβλητα—μια βέλτιστη πρακτική κατά την αυτοματοποίηση αναφορών.

> **Σημείωση:** Αν το βιβλίο εργασίας σας περιέχει πολλούς πίνακες και θέλετε να καθαρίσετε μόνο έναν συγκεκριμένο, απλώς προσαρμόστε το δείκτη στο `getTables().get(index)` ή επαναλάβετε τη συλλογή.

---

## Αφαίρεση Αυτόματου Φίλτρου στο Excel – Εργασία με Πολλαπλούς Πίνακες

Σε πραγματικά σενάρια μπορεί να έχετε πολλούς πίνακες ανά φύλλο. Εδώ είναι ένας γρήγορος βρόχος που απενεργοποιεί τα φίλτρα σε **όλους** τους πίνακες σε **όλα** τα φύλλα εργασίας:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet ws = workbook.getWorksheets().get(i);
    for (int j = 0; j < ws.getTables().getCount(); j++) {
        ws.getTables().get(j).setShowAutoFilter(false);
    }
}
```

Αυτό το απόσπασμα απαντά στην κοινή ερώτηση «τι γίνεται αν έχω περισσότερους από έναν πίνακα;», διασφαλίζοντας ότι η **απενεργοποίηση φίλτρου σε βιβλίο εργασίας Excel** λειτουργεί καθολικά.

---

## Απενεργοποίηση Φίλτρου σε Βιβλίο Εργασίας Excel – Διατήρηση Άλλης Μορφοποίησης

Μερικές φορές θέλετε να κρατήσετε τα πτυσσόμενα μενού του φίλτρου κρυμμένα **αλλά** να διατηρήσετε άλλα χαρακτηριστικά του πίνακα όπως εναλλασσόμενες γραμμές ή δομημένες αναφορές. Η μέθοδος `setShowAutoFilter` επηρεάζει μόνο το στοιχείο UI, αφήνοντας τα υπόλοιπα αμετάβλητα. Αυτό σημαίνει ότι μπορείτε με ασφάλεια να **αφαιρέσετε τα πτυσσόμενα μενού των πινάκων Excel** χωρίς να σπάσετε τύπους που αναφέρονται στον πίνακα.

Αν χρειαστεί να **ενεργοποιήσετε ξανά** το φίλτρο αργότερα, απλώς αλλάξτε τη σημαία πίσω σε `true`:

```java
table.setShowAutoFilter(true);
```

---

## Ακραίες Περιπτώσεις & Πιθανά Προβλήματα

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Δεν υπάρχουν πίνακες στο φύλλο** | `getTables().get(0)` προκαλεί `IndexOutOfBoundsException` | Ελέγξτε `sheet.getTables().getCount() > 0` πριν την πρόσβαση. |
| **Το βιβλίο εργασίας είναι προστατευμένο με κωδικό** | Η φόρτωση θα αποτύχει αν δεν παρέχετε τον κωδικό. | Use `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("secret"); }});` |
| **Μεγάλα αρχεία (>100 MB)** | Η κατανάλωση μνήμης μπορεί να αυξηθεί. | Ενεργοποιήστε τις **επιλογές φόρτωσης** με `setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`. |
| **Θέλετε μόνο να καθαρίσετε το φίλτρο, όχι να κρύψετε το πτυσσόμενο μενού** | `setShowAutoFilter(false)` αφαιρεί εντελώς το UI. | Καλέστε `table.getAutoFilter().clearFilter();` αντί αυτού (διατηρεί το πτυσσόμενο μενού). |

Η διαχείριση αυτών των σεναρίων κάνει την αυτοματοποίηση σας ανθεκτική και έτοιμη για παραγωγή.

---

## Οπτική Επιβεβαίωση (Προαιρετικό)

Αν θέλετε να δείτε ένα στιγμιότυπο πριν‑και‑μετά, εισάγετε μια εικόνα όπως η παρακάτω. Το κείμενο alt είναι βελτιστοποιημένο για SEO:

![Πώς να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel – στιγμιότυπο πριν και μετά](/images/turn-off-auto-filter.png "Πώς να απενεργοποιήσετε το αυτόματο φίλτρο στο Excel")

*Η εικόνα δείχνει τα βέλη φίλτρου να εξαφανίζονται μετά την εκτέλεση του κώδικα.*

---

## Δοκιμή των Αλλαγών Σας

Μετά την εκτέλεση του προγράμματος:

1. Ανοίξτε το `noFilter.xlsx` στο Excel.
2. Επαληθεύστε ότι **δεν εμφανίζονται πτυσσόμενα μενού αυτόματου φίλτρου** σε κανέναν πίνακα.
3. Ελέγξτε ότι όλα τα δεδομένα, οι τύποι και η μορφοποίηση παραμένουν αμετάβλητα.

Αν όλα φαίνονται σωστά, έχετε επιτυχώς **αφαιρέσει το αυτόματο φίλτρο στο Excel** και μπορείτε να διανείμετε το αρχείο με σιγουριά.

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Συζητήσαμε **πώς να απενεργοποιήσετε το αυτόματο φίλτρο** στο Excel χρησιμοποιώντας Java, παρουσιάσαμε προσεγγίσεις για έναν ή πολλούς πίνακες και επισημάναμε κοινά προβλήματα. Συνοπτικά:

- Φορτώστε το βιβλίο εργασίας με Aspose.Cells.  
- Προσπελάστε τον(ους) στόχο(υς) πίνακα(ες).  
- Καλέστε `setShowAutoFilter(false)` για **απενεργοποίηση φίλτρου πίνακα Excel**.  
- Αποθηκεύστε το αποτέλεσμα.

Από εδώ μπορείτε να εξερευνήσετε:

- **Προσθήκη υπό συνθήκη μορφοποίησης** μετά την αφαίρεση του φίλτρου.  
- **Εξαγωγή του καθαρισμένου βιβλίου εργασίας σε PDF** για διανομή.  
- **Αυτοματοποίηση ολόκληρης της διαδικασίας** με εργασία CI/CD που δημιουργεί αναφορές καθημερινά.

Μη διστάσετε να πειραματιστείτε—ίσως δοκιμάσετε να ενεργοποιήσετε ξανά το φίλτρο για μια διαφορετική έκδοση της αναφοράς, ή να συνδυάσετε αυτό με καθαρισμό επικύρωσης δεδομένων. Οι δυνατότητες είναι ατελείωτες, και τώρα έχετε μια σταθερή βάση.

### Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με αρχεία `.xls`;**  
Α: Απόλυτα. Το Aspose.Cells ανιχνεύει αυτόματα τη μορφή, έτσι ο ίδιος κώδικας λειτουργεί τόσο για `.xlsx` όσο και για παλαιά `.xls`.

**Ε: Τι κάνω αν χρειάζεται να διατηρήσω το φίλτρο αλλά απλώς να καθαρίσω τα κριτήρια;**  
Α: Χρησιμοποιήστε `table.getAutoFilter().clearFilter();` αντί για `setShowAutoFilter(false)`. Αυτό **αφαιρεί τα πτυσσόμενα μενού των πινάκων Excel** και καθαρίζει μόνο το εφαρμοσμένο φίλτρο, αφήνοντας το UI αμετάβλητο.

**Ε: Μπορώ να το τρέξω σε διακομιστή χωρίς GUI;**  
Α: Ναι. Το Aspose.Cells είναι μια καθαρή βιβλιοθήκη Java και δεν απαιτεί την εγκατάσταση του Excel.

Αυτό ήταν! Τώρα ξέρετε **πώς να απενεργοποιήσετε το αυτόματο φίλτρο** στο Excel, πώς να **αφαιρέσετε το αυτόματο φίλτρο στο Excel**, και πώς να **απενεργοποιήσετε το φίλτρο σε βιβλίο εργασίας Excel** προγραμματιστικά. Προχωρήστε, ενσωματώστε το στο επόμενο εργαλείο αναφορών σας, και απολαύστε ένα πιο καθαρό, επαγγελματικό αποτέλεσμα.

Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Φιλτράρετε Κενά Κελιά στο Excel Χρησιμοποιώντας Aspose.Cells for Java: Ένας Πλήρης Οδηγός](/cells/english/java/data-analysis/filter-blank-cells-excel-aspose-java/)
- [Πώς να Φιλτράρετε Αποτελεσματικά Δεδομένα Κατά τη Φόρτωση Βιβλίων Εργασίας Excel Χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)
- [Λήψη Δεικτών Κρυφών Γραμμών μετά την Ανανέωση του Αυτόματου Φίλτρου στο Excel](/cells/english/net/excel-hidden-rows-data-duplication-management/get-all-hidden-row-indices-after-refreshing-auto-filter-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}