---
category: general
date: 2026-10-07
description: Μάθετε πώς να διαβάσετε ημερομηνίες Excel από κελιά σε Java χρησιμοποιώντας
  το Aspose.Cells και επίσης να γράψετε τιμές πίσω στο Excel αποδοτικά.
draft: false
keywords:
- how to read excel
- write value to excel
- get datetime from excel
- extract datetime from cell
- Aspose.Cells Java date parsing
lastmod: 2026-10-07
og_description: Πώς να διαβάσετε ημερομηνίες Excel από κελιά σε Java χρησιμοποιώντας
  το Aspose.Cells. Αυτός ο οδηγός δείχνει επίσης πώς να γράψετε τιμές σε κελιά Excel
  αποδοτικά.
og_image_alt: 'Developer guide: reading and writing Excel dates with Aspose.Cells
  Java'
og_title: Πώς να διαβάσετε ημερομηνίες Excel από κελιά σε Java χρησιμοποιώντας το
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  headline: How to read Excel dates from cells in Java using Aspose.Cells
  type: TechArticle
- description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  name: How to read Excel dates from cells in Java using Aspose.Cells
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- date parsing
- Excel automation
title: Πώς να διαβάσετε ημερομηνίες Excel από κελιά σε Java χρησιμοποιώντας το Aspose.Cells
url: /el/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαβάσετε ημερομηνίες Excel από κελιά σε Java χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε **πώς να διαβάσετε Excel** τιμές που αποθηκεύονται ως συμβολοσειρές ιαπωνικής εποχής, βρίσκεστε στο σωστό μέρος. Πολλά παλιά βιβλία εργασίας περιέχουν ημερομηνίες όπως “Reiwa 3/04/01”, και η εξαγωγή ενός κατάλληλου `java.time.LocalDateTime` μπορεί να μοιάζει με αποκρυπτογράφηση κώδικα. Το Aspose.Cells for Java καταλαβαίνει αυτές τις σημειώσεις εποχής, και επίσης σας επιτρέπει να **γράψετε τιμή σε excel** κελιά χωρίς να χάσετε τη μορφοποίηση. Σε αυτόν τον οδηγό θα βρείτε μια πλήρη, βήμα‑βήμα περιήγηση που μπορείτε να επικολλήσετε σε οποιοδήποτε έργο Maven σήμερα.

## Σύντομες απαντήσεις
- **Μπορεί το Aspose.Cells να αναλύσει ημερομηνίες ιαπωνικής εποχής;** Ναι – ενεργοποιήστε τη σημαία ημερολογίου ιαπωνικής εποχής και επαναϋπολογίστε τους τύπους.  
- **Χρειάζεται να επαναϋπολογίσω τους τύπους χειροκίνητα;** Απόλυτα· χωρίς μια διαδικασία υπολογισμού η συμβολοσειρά εποχής παραμένει κείμενο.  
- **Πόσες μορφές Excel υποστηρίζει το Aspose.Cells;** Πάνω από 50 μορφές εισόδου και εξόδου, συμπεριλαμβανομένων των XLSX, XLS, CSV και ODS.  
- **Είναι η βιβλιοθήκη συμβατή με Java 8+;** Ναι, λειτουργεί με Java 8 και νεότερες εκδόσεις χρόνου εκτέλεσης.  
- **Μπορώ να γράψω μια Γρηγοριανή ημερομηνία πίσω στο ίδιο κελί;** Χρησιμοποιήστε `putValue` με ένα `LocalDateTime` και ορίστε τη μορφή αριθμού ώστε να εμφανίζει ISO‑8601.

## Τι είναι η ανάγνωση ημερομηνιών Excel από κελιά;
Η φράση **πώς να διαβάσετε Excel** αναφέρεται στην εξαγωγή του περιεχομένου των κελιών—ιδιαίτερα ημερομηνιών—σε εγγενείς τύπους προγραμματισμού όπως `java.time.LocalDateTime`. Το Aspose.Cells αφαιρεί την χαμηλού επιπέδου ανάλυση, επιτρέποντάς σας να εστιάσετε στη λογική της επιχείρησης αντί στις ιδιαιτερότητες του σειριακού αριθμού του Excel. Αυτή η προσέγγιση απλοποιεί τη συντήρηση του κώδικα και μειώνει την πιθανότητα σφαλμάτων μετατροπής όταν εργάζεστε με παλιά λογιστικά φύλλα.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για μετατροπή ιαπωνικής εποχής;
Το Aspose.Cells υποστηρίζει **50+** μορφές αρχείων και μπορεί να επεξεργαστεί βιβλία εργασίας με **εκατοντάδες σελίδες** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η ενεργοποίηση του ημερολογίου ιαπωνικής εποχής προσθέτει μόνο αμελητέο κόστος απόδοσης, καθιστώντας το ιδανικό για επεξεργασία παρτίδας παλαιών λογιστικών φύλλων. Η βιβλιοθήκη επίσης διατηρεί τα στυλ των κελιών και τους τύπους κατά τη μετατροπή, εξασφαλίζοντας ότι το αποτέλεσμα φαίνεται ακριβώς όπως το αρχικό βιβλίο εργασίας.

## Προαπαιτούμενα

* **Java 8+** – τα παραδείγματα χρησιμοποιούν το σύγχρονο API `java.time`.  
* **Aspose.Cells for Java ≥ 23.9.0** – προσθέστε την εξάρτηση Maven/Gradle από το επίσημο αποθετήριο.  
* Βασικές γνώσεις των εννοιών του Excel ( φύλλα εργασίας, κελιά, τύποι).  

Αν σας λείπει η βιβλιοθήκη, κατεβάστε την από το επίσημο αποθετήριο Aspose:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Πώς να δημιουργήσετε ένα βιβλίο εργασίας και να αποκτήσετε πρόσβαση στο πρώτο φύλλο εργασίας;
`Workbook` αντιπροσωπεύει ένα αρχείο Excel που φορτώνεται στη μνήμη. `Worksheet` αντιπροσωπεύει ένα μεμονωμένο φύλλο μέσα σε αυτό το βιβλίο.  
Δημιουργήστε ένα αντικείμενο `Workbook`, το οποίο αντιπροσωπεύει ένα αρχείο Excel στη μνήμη, και στη συνέχεια αποκτήστε το πρώτο `Worksheet`. Αυτό σας δίνει πλήρη έλεγχο πριν οποιαδήποτε δεδομένα αγγίξουν το δίσκο. Αρχικοποιώντας πρώτα το βιβλίο εργασίας μπορείτε να ρυθμίσετε τις ρυθμίσεις—όπως η διαχείριση ημερολογίου—πριν διαβαστούν ή γραφτούν τιμές κελιών.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

## Πώς να γράψετε μια ημερομηνία ιαπωνικής εποχής σε κελί A1;
`Cell` είναι το αντικείμενο που κρατά την τιμή ενός μεμονωμένου κελιού Excel.  
Εισάγετε τη συμβολοσειρά εποχής “Reiwa 3/04/01” στο κελί A1. Αυτό μιμείται μια τιμή που εισήγαγε ο χρήστης, την οποία θα μετατρέψετε αργότερα. Η εγγραφή της συμβολοσειράς πρώτα σας επιτρέπει να δείξετε ολόκληρη τη ροή εργασίας μετατροπής από κείμενο σε κατάλληλο αντικείμενο ημερομηνίας.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

## Πώς να ενεργοποιήσετε το ημερολόγιο ιαπωνικής εποχής για ανάλυση ημερομηνιών;
`WorkbookSettings.setUseJapaneseEraCalendar(boolean)` ενεργοποιεί τη λειτουργία μετατροπής εποχής.  
Ενεργοποιήστε τη σημαία του ημερολογίου ώστε το Aspose.Cells να ξέρει πώς να μεταφράσει τα ονόματα εποχής σε Γρηγοριανά έτη. Η ενεργοποίηση αυτής της σημαίας λέει στη μηχανή υπολογισμού να ερμηνεύσει συμβολοσειρές όπως “Reiwa” ως το αντίστοιχο Γρηγοριανό έτος, κάτι που είναι ουσιώδες για ακριβή ανάλυση ημερομηνιών.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

## Πώς να επαναϋπολογίσετε τους τύπους ώστε η συμβολοσειρά εποχής να μετατραπεί σε Γρηγοριανή ημερομηνία;
`Workbook.calculateFormula()` εξαναγκάζει τη μηχανή υπολογισμού να αξιολογήσει όλους τους τύπους στο βιβλίο εργασίας.  
Τρέξτε τη μηχανή υπολογισμού μία φορά· θα αναγνωρίσει το μοτίβο εποχής, θα το μετατρέψει και θα αποθηκεύσει το Γρηγοριανό αποτέλεσμα εσωτερικά. Μετά από αυτό, το `getDateTime()` επιστρέφει ένα `java.util.Date`, το οποίο μπορείτε να μετατρέψετε σε `java.time`. Αυτό το βήμα είναι απαραίτητο επειδή η συμβολοσειρά εποχής αρχικά θεωρείται απλό κείμενο μέχρι να αξιολογηθούν οι τύποι.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

**Αναμενόμενο αποτέλεσμα**

```
2021-04-01T00:00:00.000+00:00
```

## Πώς να γράψετε μια νέα τιμή πίσω στο ίδιο κελί (ή σε άλλο κελί);
`Cell.putValue(Object)` γράφει μια τιμή σε κελί, διαχειριζόμενο αυτόματα τη μετατροπή τύπου.  
Αντικαταστήστε την αρχική συμβολοσειρά εποχής με μια καθαρή ημερομηνία ISO‑8601 διατηρώντας το στυλ του κελιού. Το `putValue` ανιχνεύει τον τύπο `LocalDateTime` και τον μετατρέπει στην αναπαράσταση σειριακού αριθμού του Excel. Ορίζοντας τη μορφή αριθμού εξασφαλίζετε ότι το κελί εμφανίζει την ημερομηνία ακριβώς όπως περιμένετε όταν ανοίγετε το αρχείο στο Excel.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

## Πλήρες λειτουργικό παράδειγμα

Όλα τα παραπάνω βήματα συνδυάζονται σε μια ενιαία κλάση Java που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Δημιουργεί ένα βιβλίο εργασίας, γράφει μια συμβολοσειρά εποχής, τη μετατρέπει και τελικά αποθηκεύει το αρχείο.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Τρέξτε την κλάση με `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` και ανοίξτε **output.xlsx**. Το κελί A1 θα εμφανίσει τη μετατρεπόμενη Γρηγοριανή ημερομηνία, και η κονσόλα θα καταγράψει την τιμή “2021‑04‑01”.

## Τι γίνεται αν το κελί περιέχει ήδη μια πραγματική ημερομηνία Excel;
Αν το κελί ήδη αποθηκεύει μια εγγενή ημερομηνία Excel, μπορείτε να την διαβάσετε απευθείας χωρίς επιπλέον επεξεργασία. Αυτό εξοικονομεί χρόνο επειδή η μηχανή υπολογισμού δεν χρειάζεται να επανερμηνεύσει την τιμή. Απλώς ελέγξτε τον τύπο του κελιού και ανακτήστε την ημερομηνία.

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

## Πώς να επεξεργαστείτε ολόκληρη στήλη συμβολοσειρών εποχής;
Όταν πολλά κελιά περιέχουν συμβολοσειρές εποχής, επαναλάβετε την επεξεργασία πάνω στην χρησιμοποιούμενη περιοχή και εφαρμόστε την ίδια λογική μετατροπής σε κάθε κελί. Αυτή η προσέγγιση παρτίδας μειώνει το κόστος σε σχέση με την επεξεργασία κελιών μεμονωμένα. Θυμηθείτε να ενεργοποιήσετε το ημερολόγιο ιαπωνικής εποχής πριν το βρόχο και να επαναϋπολογίσετε μία φορά μετά την επεξεργασία.

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

## Μπορώ να απενεργοποιήσω τη διαχείριση ιαπωνικής εποχής αργότερα;
Μπορείτε να απενεργοποιήσετε τη σημαία μετατροπής εποχής μετά το τέλος της επεξεργασίας των σχετικών κελιών. Η απενεργοποίηση επαναφέρει τη προεπιλεγμένη συμπεριφορά ανάλυσης για τυχόν επόμενες λειτουργίες. Αυτό είναι χρήσιμο εάν χρειαστεί να εργαστείτε με τυπικές ημερομηνίες αργότερα στο ίδιο βιβλίο εργασίας.

```java
settings.setUseJapaneseEraCalendar(false);
```

Θυμηθείτε να επαναϋπολογίσετε ξανά εάν αλλάξετε τη ρύθμιση μετά τη γραφή δεδομένων.

## Επαγγελματικές συμβουλές & παγίδες

* **Απόδοση:** Η ενεργοποίηση του ημερολογίου ιαπωνικής εποχής προσθέτει μικρή επιβάρυνση. Ενεργοποιήστε το μόνο για τα κελιά που χρειάζονται μετατροπή, μετά το απενεργοποιήστε.  
* **Ευαισθησία τοπικής ρύθμισης:** Η συμβολοσειρά εποχής πρέπει να ακολουθεί το ακριβές μοτίβο “EraName yy/MM/dd”. Λάθη (π.χ., “Rewa”) αφήνουν το κελί ως απλό κείμενο.  
* **Μορφή αποθήκευσης:** `Workbook.save("output.xlsx")` γράφει αρχείο XLSX. Χρησιμοποιήστε `"output.xls"` για την παλαιότερη δυαδική μορφή, αλλά σημειώστε ότι ορισμένες προηγμένες λειτουργίες—όπως η ανάλυση εποχής—μπορεί να είναι περιορισμένες.

## Συχνές ερωτήσεις

**Ε: Λειτουργεί αυτή η προσέγγιση με άλλα πολιτιστικά ημερολόγια (Thai, Hijri);**  
Α: Ναι—το Aspose.Cells παρέχει παρόμοιες σημαίες για τα Ταϊλανδικά Βουδιστικά και Χιτζρικά ημερολόγια· ενεργοποιήστε τη σχετική ρύθμιση και επαναϋπολογίστε.

**Ε: Μπορώ να διαβάσω ημερομηνίες από βιβλίο εργασίας προστατευμένο με κωδικό;**  
Α: Φορτώστε το βιβλίο εργασίας με την παράμετρο κωδικού, έπειτα ακολουθήστε τα ίδια βήματα· η σημαία ημερολογίου λειτουργεί αμετάβλητη.

**Ε: Υπάρχει όριο στον αριθμό των γραμμών που μπορώ να επεξεργαστώ;**  
Α: Το Aspose.Cells μπορεί να διαχειριστεί εκατομμύρια γραμμές· ρέει δεδομένα για να διατηρεί τη χρήση μνήμης χαμηλή, ειδικά όταν η `setUseJapaneseEraCalendar` εναλλάσσεται ανά παρτίδα.

**Ε: Πώς διατηρώ τα υπάρχοντα στυλ κελιών όταν αντικαθιστώ την ημερομηνία;**  
Α: Ανακτήστε το αντικείμενο `Style` του κελιού πριν καλέσετε `putValue`, έπειτα επαναεφαρμόστε το μετά τη λειτουργία εγγραφής.

**Ε: Χρειάζεται εμπορική άδεια για χρήση σε παραγωγή;**  
Α: Ναι, απαιτείται έγκυρη άδεια Aspose.Cells για παραγωγικές εγκαταστάσεις· διατίθεται δωρεάν δοκιμή για αξιολόγηση.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να διαβάσετε Excel** ημερομηνίες που χρησιμοποιούν σημειώσεις ιαπωνικής εποχής και πώς να **γράψετε τιμή σε excel** κελιά με σωστή μορφοποίηση. Ενεργοποιώντας `setUseJapaneseEraCalendar(true)` και εξαναγκάζοντας επαναϋπολογισμό τύπων, το Aspose.Cells γεφυρώνει τις παλαιές συμβολοσειρές εποχής σε σύγχρονες Γρηγοριανές ημερομηνίες με λίγες μόνο γραμμές Java. Δοκιμάστε να επεκτείνετε αυτό το μοτίβο σε άλλα πολιτιστικά ημερολόγια ή να επεξεργαστείτε μαζικά μεγάλα βιβλία εργασίας—η ίδια ροή ενεργοποίησης‑επαναϋπολογισμού‑ανάγνωσης/εγγραφής ισχύει παντού.

Έχετε κάποιο δύσκολο φορμάτ ημερομηνίας που δεν μπορείτε να σπάσετε; Αφήστε ένα σχόλιο παρακάτω και ας το αντιμετωπίσουμε μαζί. Καλό κώδικα!

![Παράδειγμα λήψης ημερομηνίας από κελί](https://example.com/images/get-datetime-from-cell.png "Παράδειγμα λήψης ημερομηνίας από κελί")
[Παράδειγμα λήψης ημερομηνίας από κελί](https://example.com/images/get-datetime-from-cell.png "Παράδειγμα λήψης ημερομηνίας από κελί")

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω μαθήματα καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε το σύστημα ημερομηνιών 1904 στο Excel χρησιμοποιώντας το Aspose.Cells Java για αποδοτικές λειτουργίες κελιών](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Πώς να υλοποιήσετε αναδρομικό υπολογισμό κελιών στο Aspose.Cells Java για βελτιωμένο αυτοματισμό Excel](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Πώς να μετατρέψετε ονόματα κελιών Excel σε δείκτες χρησιμοποιώντας το Aspose.Cells για Java: Οδηγός βήμα‑βήμα](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

--- 

**Τελευταία ενημέρωση:** 2026-10-07  
**Δοκιμή με:** Aspose.Cells 23.9.0  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [απόδοση aspose cells: Ανάκτηση δεδομένων κελιών Excel με Java](/cells/java/cell-operations/aspose-cells-java-data-retrieval-excel/)
- [Αλλαγή του συστήματος ημερομηνιών 1904 στο Excel με Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Κατακτήστε τη διαχείριση αρχείων Java με Aspose.Cells: Ανάγνωση, γραφή & επεξεργασία δεδομένων αποδοτικά](/cells/java/workbook-operations/java-file-handling-aspose-cells-read-write-process/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}