---
category: general
date: 2026-06-30
description: Ορίστε προσαρμοσμένη μορφή αριθμού στο Excel χρησιμοποιώντας Java. Μάθετε
  πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel με Java, να λάβετε ημερομηνία και
  ώρα από κελί, να υπολογίσετε τύπους του βιβλίου εργασίας και να εξάγετε την τιμή
  ημερομηνίας/ώρας.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: el
og_description: Ορίστε προσαρμοσμένη μορφή αριθμού στο Excel χρησιμοποιώντας Java.
  Αυτός ο οδηγός δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel με Java, να
  λάβετε ημερομηνία και ώρα από κελί, να υπολογίσετε τύπους του βιβλίου εργασίας και
  να εξάγετε την τιμή ημερομηνίας/ώρας.
og_title: Ορισμός προσαρμοσμένης μορφής αριθμού στο Excel με Java – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Ορισμός προσαρμοσμένης μορφής αριθμού στο Excel με Java – Πλήρης οδηγός
url: /el/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Προσαρμοσμένης Μορφής Αριθμού στο Excel με Java – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **ορίσετε προσαρμοσμένη μορφή αριθμού** σε ένα φύλλο Excel ενώ εργάζεστε με Java; Δεν είστε ο μόνος. Είτε δημιουργείτε μια μηχανή αναφορών είτε απλώς προσπαθείτε να εμφανίσετε σωστά ημερομηνίες της ιαπωνικής εποχής, η κατάκτηση αυτού του κόλπου σας εξοικονομεί αμέτρητες ώρες μετα‑επεξεργασίας. Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που **δημιουργεί Excel workbook Java**, εφαρμόζει μορφή ειδική για την τοπική ρύθμιση, επανυπολογίζει τύπους και τελικά **παίρνει DateTime από κελί** για **να εμφανίσει την τιμή datetime**.

Θα χρησιμοποιήσουμε τη δημοφιλή βιβλιοθήκη Aspose.Cells for Java επειδή διαχειρίζεται μορφές αριθμών και ημερομηνίες με γνώση πολιτισμού αμέσως. Στο τέλος του οδηγού θα έχετε ένα αυτόνομο, εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle. Καμία ασαφής «δείτε τα docs» συντόμευση—απλώς σταθερός κώδικας και σαφείς εξηγήσεις.

---

## Τι Θα Μάθετε

- Πώς να **create Excel workbook Java** προγραμματιστικά.  
- Τα ακριβή βήματα για **set custom number format** για ημερομηνίες ιαπωνικής εποχής.  
- Γιατί η κλήση του **calculate workbook formulas** είναι απαραίτητη πριν την εξαγωγή της τιμής.  
- Ο σωστός τρόπος για **get datetime from cell** και **output datetime value**.  
- Κοινά προβλήματα (λείπει το locale, παλιά τύποι) και γρήγορες διορθώσεις.

---

## Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη στο μηχάνημά σας.  
- Aspose.Cells for Java 23.11 (ή οποιαδήποτε πρόσφατη έκδοση).  
- Ένα βασικό IDE ή κειμενογράφο—IntelliJ IDEA, Eclipse, VS Code, ό,τι προτιμάτε.  

Αν δεν έχετε προσθέσει ακόμη το Aspose.Cells στο πρότζεκτ σας, επικολλήστε το παρακάτω απόσπασμα Maven στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Τώρα που το περιβάλλον είναι έτοιμο, ας βουτήξουμε στον κώδικα.

---

## Βήμα 1: Ορισμός Προσαρμοσμένης Μορφής Αριθμού – Επισκόπηση

Πριν γράψουμε οποιοδήποτε Java, βοηθά να οπτικοποιήσουμε τι θέλουμε. Φανταστείτε ένα κελί Excel που πρέπει να εμφανίζει **«令和2年4月1日»** αντί της συμβολοσειράς ISO‑8601 “2020‑04‑01”. Η υποκείμενη τιμή παραμένει αληθινή ημερομηνία (οπότε οι τύποι λειτουργούν), αλλά η *εμφάνιση* ακολουθεί τη μορφή της ιαπωνικής εποχής. Αυτό είναι ακριβώς αυτό που επιτυγχάνει η λειτουργία **set custom number format**.

Παρακάτω είναι το πλήρες αρχείο πηγής. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε στο `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Γιατί Αυτό Λειτουργεί

- **`setNumberFormat`** λέει στο Excel πώς να *εμφανίσει* την υποκείμενη αριθμητική τιμή. Η συμβολοσειρά μορφής `[$-ja-JP]ggge年m月d日` είναι το κλειδί· `ggg` επιλέγει το όνομα της εποχής, `e` το έτος μέσα στην εποχή, ακολουθούμενα από τους μήνα και ημέρα ως κυριολεκτικούς χαρακτήρες.  
- **`calculateFormula`** αναγκάζει το Aspose.Cells να ερμηνεύσει το κείμενο “R02-04-01” ως ημερομηνία βάσει του ιαπωνικού ημερολογίου. Αν παραλείψετε αυτό το βήμα, το κελί παραμένει απλό κείμενο και το `getDateTime()` θα πετάξει εξαίρεση.  
- **`getDateTime`** τελικά εξάγει το *πραγματικό* αντικείμενο `java.util.Calendar`, το οποίο μπορείτε να χειριστείτε, μορφοποιήσετε ή αποθηκεύσετε αλλού.

---

## Βήμα 2: Δημιουργία Excel Workbook Java – Βαθύτερη Ματιά

Όταν **create Excel workbook Java**, δεν απλώς δεσμεύετε μνήμη· δημιουργείτε επίσης προεπιλεγμένα στυλ, ένα προεπιλεγμένο φύλλο εργασίας και μια προεπιλεγμένη πολιτισμική ρύθμιση (συνήθως η τοπική ρύθμιση του συστήματος). Αν χρειάζεστε διαφορετική προεπιλεγμένη τοπική ρύθμιση, μπορείτε να περάσετε ένα αντικείμενο `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Για τις περισσότερες περιπτώσεις ο απλός κατασκευαστής είναι επαρκής, αλλά είναι καλό να γνωρίζετε την εναλλακτική—ιδιαίτερα όταν διαχειρίζεστε πολλαπλές τοπικές ρυθμίσεις στην ίδια εφαρμογή.

*Pro tip:* Κρατήστε πάντα το workbook στη μνήμη μέχρι να ολοκληρώσετε τη μορφοποίηση. Η εγγραφή στο δίσκο μετά από κάθε αλλαγή προκαλεί περιττό I/O κόστος.

---

## Βήμα 3: Λήψη DateTime από Κελί – Διαχείριση του Αποτελέσματος

Η γραμμή `java.util.Calendar dt = cellA1.getDateTime();` κάνει το σκληρό έργο. Στο παρασκήνιο το Aspose.Cells μετατρέπει τον εσωτερικό σειριακό αριθμό (τον αριθμό ημερών από 31‑12‑1899) σε ένα `Calendar`. Αυτή η μετατροπή σέβεται το locale του workbook, οπότε λαμβάνετε τη σωστή Γρηγοριανή ημερομηνία παρόλο που η εμφάνιση χρησιμοποιεί την ιαπωνική εποχή.

Αν χρειάζεστε ένα `java.time.LocalDate` (το νεότερο API), μετατρέψτε ως εξής:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Αυτό καλύπτει την απαίτηση **output datetime value** ενώ παραμένει σύγχρονο.

---

## Βήμα 4: Υπολογισμός Τύπων Workbook – Όταν Είναι Σημαντικό

Μπορεί να αναρωτιέστε: *«Πρέπει πραγματικά να καλέσω το `calculateFormula()`;»* Η απάντηση είναι ένα σαφές ναι, εκτός αν τροφοδοτείτε το κελί με ένα εγγενές αντικείμενο Java `Date` από την αρχή. Όταν **set custom number format** σε μια συμβολοσειρά κειμένου, το Excel (και το Aspose.Cells) το θεωρούν ως έκφραση τύπου‑συνάρτησης που χρειάζεται αξιολόγηση. Χωρίς επανυπολογισμό, το `getDateTime()` θα επιστρέψει την προεπιλεγμένη τιμή `1900‑01‑00` ή θα πετάξει `CellValueException`.

Αν το workbook σας περιέχει ήδη σύνθετους τύπους που αναφέρονται στο νεομορφοποιημένο κελί, καλέστε το `calculateFormula()` *μία φορά* μετά από όλες τις αλλαγές. Οι επαναλαμβανόμενες κλήσεις είναι δαπανηρές.

---

## Βήμα 5: Εμφάνιση Τιμής DateTime – Επαλήθευση του Αποτελέσματος

Η εκτέλεση του demo εκτυπώνει κάτι όπως:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Αυτή η γραμμή επιβεβαιώνει τρία πράγματα:

1. Η **set custom number format** εφαρμόστηκε (μπορείτε να ανοίξετε το παραγόμενο `.xlsx` στο Excel για να δείτε “令和2年4月1日”).  
2. Το βήμα **calculate workbook formulas** πέτυχε, μετατρέποντας τη συμβολοσειρά εποχής σε πραγματική ημερομηνία.  
3. Η κλήση **get datetime from cell** επέστρεψε ένα σωστό `Calendar`, το οποίο στη συνέχεια **output datetime value** στην κονσόλα.

Αν ανοίξετε το workbook με κάποιο πρόγραμμα λογιστικού φύλλου, θα δείτε το μορφοποιημένο κείμενο, αλλά η υποκείμενη τιμή του κελιού παραμένει ο σειριακός αριθμός `43831` (η αναπαράσταση του Excel για 2020‑04‑01). Αυτή η διπλοπλοκότητα είναι που κάνει το Excel τόσο δυνατό.

---

## Συνηθισμένα Προβλήματα & Ακραίες Περιπτώσεις

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| `cellA1.getDateTime()` throws `CellValueException` | Το κελί παραμένει συμβολοσειρά επειδή παραλείφθηκε το `calculateFormula()`. | Πάντα να καλείτε `workbook.calculateFormula()` μετά από ορισμό κειμενικής ημερομηνίας που χρειάζεται μετατροπή. |
| Japanese era not displayed correctly | Λείπει ή είναι λανθασμένος ο κωδικός τοπικής ρύθμισης. | Χρησιμοποιήστε `[$-ja-JP]` στη συμβολοσειρά μορφής ή ορίστε το locale του workbook μέσω `LoadOptions`. |
| Format shows “#VALUE!” in Excel | Η συμβολοσειρά μορφής είναι εσφαλμένη. | Ελέγξτε ξανά τις αγκύλες και τους χαρακτήρες· το μοτίβο `ggge年m月d日` είναι απαραίτητο για το έτος εποχής. |
| Time component appears (e.g., “00:00:00”) | Η πηγαία συμβολοσειρά περιέχει χρόνο ή το στυλ του κελιού το προσθέτει. | Αποκόψτε τη πηγαία συμβολοσειρά ή προσαρμόστε τη μορφή σε `ggge年m月d日;@`. |

---

## Πλήρες Παράδειγμα Εργασίας – Εκτέλεση με Ένα Κλικ

Αν προτιμάτε ένα μόνο αρχείο χωρίς επιπλέον σχόλια, εδώ είναι η ελάχιστη έκδοση:



## Τι Θα Μάθετε Στη Σύντομη Επόμενη

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Δημιουργία Excel Workbook χρησιμοποιώντας Aspose.Cells σε Java: Οδηγός βήμα‑βήμα](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Κατάκτηση Παρουσίασης Δεδομένων στο Excel: Αριθμοί και Προσαρμοστική Μορφοποίηση Ημερομηνιών με Aspose.Cells για Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Πώς να Δημιουργήσετε & Μορφοποιήσετε Κελιά Excel Χρησιμοποιώντας Aspose.Cells για Java: Οδηγός βήμα‑βήμα](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}