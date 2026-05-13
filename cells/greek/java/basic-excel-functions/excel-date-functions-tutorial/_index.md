---
date: 2026-01-22
description: Μάθετε πώς να υπολογίζετε τις ημέρες μεταξύ ημερομηνιών χρησιμοποιώντας
  τις συναρτήσεις ημερομηνίας του Excel και το Aspose.Cells για Java. Περιλαμβάνει
  κώδικα βήμα‑βήμα, εφαρμογή μορφής ημερομηνίας στο Excel και μορφοποίηση κελιών ως
  dd‑mm‑yyyy.
linktitle: How to Calculate Days Between Dates with Excel Date Functions
second_title: Aspose.Cells Java Excel Processing API
title: Πώς να υπολογίσετε τις ημέρες μεταξύ ημερομηνιών με τις συναρτήσεις ημερομηνίας
  του Excel
url: /el/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Υπολογίσετε τις Ημέρες Μεταξύ Ημερομηνιών με τις Συναρτήσεις Ημερομηνίας του Excel

Σε αυτό το ολοκληρωμένο σεμινάριο, θα μάθετε πώς να **υπολογίζετε τις ημέρες μεταξύ ημερομηνιών** χρησιμοποιώντας τις ενσωματωμένες συναρτήσεις ημερομηνίας του Excel και το ισχυρό Aspose.Cells API για Java. Είτε χρειάζεστε να υπολογίσετε χρονοδιαγράμματα έργων, να δημιουργήσετε αναφορές ή απλώς να μορφοποιήσετε ημερομηνίες με συνέπεια, αυτός ο οδηγός σας καθοδηγεί μέσα από τις έννοιες, τις πραγματικές περιπτώσεις χρήσης και τα έτοιμα προς εκα. Αςμηνία;** `TODAY()`  
- **Πώς υπολογίζετε τη διαφορά μεταξύ δύο ημερομηνιών;** Χρησιμοποιήστε `DATEDIF` ή αφαιρέστε τις ημερομηνίες απευθείας.  
- **Μπορώ να μορφοποιήσω κελιά ως dd‑mm‑yyyy;** Ναι, εφαρμόστε ένα προσαρμοσμένο στυλ με `Style.set- **Χρειάζεται άδεια για το Aspose.Cells;** Απαιτείται έγκυρη άδεια για παραγωγική χρήση.  
- **Ποια έκδοση του Aspose.Cells λειτουργεί με Java 11;** Η πιο πρόσφατη έκδοση (ως το μηνιών” στο Excel;
Το Excel αποθηκεύει τις ημερομηνίες ως σειριακούς αριθμούς, επιτρέποντας απλή αριθose.Cells Δημιουργβεια** – Εξαρτάστε από τη φυσική μηχανή ημερομηνίας του Excel για ακριβείς υπολογισμούς.  
- **Ευελιξία** – Συνδυάστε πολλαπλές συναρτήσεις (π.χ., `EOMONTH`, `DATEDIF`) σε έναν τύπο.  
- **Κλιμακωσιμότητα** – Επεξεργασία χιλιάδων γραμμών γρήγορα, ιδανικό για εκθέσεις μεγάλης κλίμακας.

## Προαπαιτούμενα
- Java 8 ή νεότερη εγκατεστημένη.  
- Βιβλιοθήκη Aspose.Cells for Java (λήψη από τον επίσημο ιστότοπο).  
- Έγκυρη άδεια Aspose.Cells για παραγωγική χρήση.

## Ρύθμιση του Aspose.Cells

Πριν γράψετε κώδικα, βεβαιωθείτε ότι το Aspose.Cells έχει προστεθεί στο έργο σας.

1. **Λήψη και Εγκατάσταση Aspose.Cells** – Επισκεφθείτε [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) και κατεβάστε το πιο πρόσφατο JAR.  
2. **Προσθήκη του JAR στο Build Path** – Συμπεριλάβετε το στο `pom.xml` (θετήστε το αρχείο άδειας στο έργο και φορτώστε το κατά την εκτέλεση.

## Χρήση της Συνάρτησης DATE

Η συνάρτηση `DATE` δημιουργεί μια ημερομηνία από τα στοιχεία έτους, μήνα και ημέρας. Παρακάτω υπάρχει ένα έτοιμο παράδειγμα που εισάγει μια συγκεκριμένη ημερομηνία στο κελί **A1**.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

**Γιατί είναι σημαντικό:** Η χρήση του `DATE` διασφατική τιμή ημερομηνίας του Excel, την οποία άλλοι τύποι (όπως `DATEDIF`) μπορούν να αναφερθούν αξιόπιστα.

## Εργασία με τη Συνάρτηση TODAY

`TODAY()` επιστρέφει πάντα την τρέχουσα ημερομηνία του συστήματος. Αυτό είναι χρήσιμο για δυναμικές αναφορές που χρειάζονται “ημερομηνία κατά την ώρα”.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

**Συμβουλή:** Επειδή το `TODAY()` ενημερώνεται κάθε φορά που το βιβλίο εργασίας επαναϋπολογίζεται, μπορείτε να το χρησιμοποιήσετε για να παρακολουθείτε πότε τα δεδομένα ενημερώθηκαν τελευταία φορά.

## Υπολογισμός Διαφοράς Ημερομηνιών με DATEDIF

Η συνάρτηση `DATEDIF` υπολογίζει τη διαφορά μεταξύ δύο ημερομηνιών σε ημέρες, μήνες ή χρόνια. Αυτό ανταποκρίνεται άμεσα στην απαίτηση **υπολογίστε τις ημέρες μεταξύ ημερομηνιών**.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

**Κύριο σημείο:** Το `DATEDIF` λειτουργεί τόσο με απόλυτες ημερομηνίες όσο και με τύπους, καθιστώντας το ευέλικτο για αναφορές διαστημάτων, υπολογισμούς ηλικίας ή χρονοδιαγράμματα έργων.

## Εύρεση του Τέλους του Μήνα με EOMONTH

`EOMONTH` επιστρέφει την τελευταία ημέρα του μήνα για μια δεδομένη ημερομηνία, χρήσιμο για οικονομικά κλείσιμο.

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

## Πώς να Εφαρμόσετε Μορφή Ημερομηνίας στο Excel

Η συνεπής μορφοποίηση βελτιώνει την αναγνωσιμότητα. Παρακάτω φαίνεται πώς μπορείτε να **εφαρμόσετε μορφή ημερομηνίας στο Excel** χρησιμοποιώντας το Aspose.Cells.

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```

Ορίζοντας το προσαρμοσμένο μοτίβο `"dd-MM-yyyy"` εξασφαλίζετε ότι κάθε ημερομηνία εμφανίζεται ως **ημέρα‑μήνας‑έτος**, σύμφωνα με πολλά τοπικά πρότυπα.

## Συνηθισμένα Προβλήματα και Λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Ο τύπος δεν επαναϋπολογίζεται | Το βιβ να υπολογίζει αυτόματα | Κλήση `workbook.calculateFormula()` μετά τον ορισμό των ως κείμενοValue` με συμβολοσειρά ημερομηνίαςDATE`). |

## Συχνές Ερωτήσεις

### Πώς να μορφοποιήσω κελιά ως dd‑mm‑yyyy;
Μπορείτε να χρησιμοποιήσετε τη μέθοδο `Style.setCustom` για να ορίσετε το μοτίβο `"dd‑mm‑yyyy"` και να εφαρμόσετε το στυλ στα επιθυμητά κελιά (δείτε το παράδειγμα “εφαρμόστε μορφή ημερομηνίας στο Excel” παραπάνω).

### Πώς να υπολογίσω τη διαφορά ημερομηνιών χρησιμοποιώντας DATEDIF;
Χρησιμοποιήστε τον τύπο `=DATEDIF(start_date, end_date, "d")` όπου το `"d"` υποδεικνύει ημέρες. Το απόσπασμα κώδικα στην ενότητα **Υπολογισμός Διαφοράς Ημερομηνιών με DATEDIF** το δείχνει σε Java.

### Μπορώ να χρησιμοποιήσω αυτές τις συναρτήσεις σε μεγάλα φύλλα εργασίας;
Ναι. Το Aspose.Cells έχει σχεδιαστεί για υψηλή απόδοση. Για πολύ μεγάλα αρχεία, εξετάστε το ενδεχόμενο κλήσης του `workbook.calculateFormula()` μόνο μία φορά μετά τον ορισμό όλων των τύπων, ώστε να μειωθεί το κόστος επαναϋπολογισμού.

### Πού μπορώ να βρω περισσότερους πόρους για το Aspose.Cells;
Μπορείτε να έχετε πρόσβαση σε εκτενή τεκμηρίωση και παραδείγματα στο [εδώ](https://reference.aspose.com/cells/java/).

### Πώς μπορώ να ξεκινήσω με το Aspose.Cells for Java;
Για να ξεκινήσετε, κατεβάστε τη βιβλιοθήκη από [εδώ](https://releases.aspose.com/cells/java/) και ακολουθήστε τα βήματα εγκατάστασης που περιγράφονται στην ενότητα **Ρύθμιση του Aspose.Cells**.

---

**Τελευταία ενημέρωση:** 2026-01-22  
**Δοκιμασμένο με:** Aspose.Cells for Java (τελευταία έκδοση 2026)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}