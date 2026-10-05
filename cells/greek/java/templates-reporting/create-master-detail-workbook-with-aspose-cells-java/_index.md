---
category: general
date: 2026-06-08
description: Δημιουργήστε βιβλίο εργασίας master‑detail σε Java χρησιμοποιώντας το
  Aspose.Cells Smart Marker. Μάθετε βήμα‑βήμα πώς να συνδέσετε τα κύρια δεδομένα με
  ένα φύλλο λεπτομερειών και να εξάγετε το Excel.
draft: false
keywords:
- create master detail workbook
- Aspose.Cells Smart Marker
- Java Excel export
- master‑detail relationship
- Smart Marker data source
language: el
og_description: Δημιουργήστε βιβλίο εργασίας master‑detail σε Java χρησιμοποιώντας
  το Aspose.Cells Smart Marker. Ακολουθήστε αυτόν τον πλήρη οδηγό για να συνδέσετε
  τα κύρια δεδομένα με ένα φύλλο λεπτομερειών και να δημιουργήσετε αρχεία Excel.
og_title: Δημιουργία βιβλίου εργασίας master‑detail με το Aspose.Cells (Java)
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create master detail workbook in Java using Aspose.Cells Smart Marker.
    Learn step‑by‑step how to bind master data to a detail sheet and export Excel.
  headline: Create master detail workbook with Aspose.Cells (Java)
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
title: Δημιουργία βιβλίου εργασίας master‑detail με Aspose.Cells (Java)
url: /el/java/templates-reporting/create-master-detail-workbook-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία βιβλίου εργασίας master‑detail με Aspose.Cells (Java)

Αν χρειάζεστε **να δημιουργήσετε βιβλίο εργασίας master‑detail** σε Java, βρίσκεστε στο σωστό μέρος. Είτε δημιουργείτε έναν πίνακα ελέγχου πωλήσεων, έναν δημιουργό τιμολογίων, ή οποιοδήποτε εργαλείο αναφοράς που απαιτεί προβολή master‑detail, αυτός ο οδηγός θα σας καθοδηγήσει σε όλη τη διαδικασία—χωρίς περιττές πληροφορίες, μόνο σταθερός, εκτελέσιμος κώδικας.

Σε αυτό το tutorial θα χρησιμοποιήσουμε το **Aspose.Cells Smart Marker**, μια ισχυρή δυνατότητα που σας επιτρέπει να ενσωματώσετε δείκτες δεδομένων απευθείας σε ένα πρότυπο Excel. Στο τέλος, θα κατανοήσετε πώς να ρυθμίσετε τη σχέση master‑detail, να συνδέσετε μια λίστα POJO ως πηγή δεδομένων, και να εξάγετε ένα καθαρό αρχείο .xlsx έτοιμο για περαιτέρω χρήση.

## Τι θα μάθετε

- Πώς να αρχικοποιήσετε ένα βιβλίο εργασίας και να προσθέσετε ένα φύλλο λεπτομερειών.  
- Πώς να εισάγετε ένα Smart Marker που συνδέει τις γραμμές master με το φύλλο λεπτομερειών.  
- Πώς να παρέχετε μια λίστα αντικειμένων `Order` ως πηγή δεδομένων για το Smart Marker.  
- Πώς να επαναϋπολογίσετε τύπους που εξαρτώνται από τα εισαχθέντα δεδομένα.  
- Πώς να αποθηκεύσετε το τελικό αρχείο με τη σχέση master‑detail αμετάβλητη.  

**Προαπαιτούμενα:** Java 17 (ή νεότερη), Maven ή Gradle, και μια έγκυρη άδεια Aspose.Cells for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές). Αν δεν έχετε χρησιμοποιήσει ποτέ το Aspose.Cells, μην ανησυχείτε—αυτός ο οδηγός υποθέτει μόνο βασικές γνώσεις Java.

---

![Create master detail workbook diagram](create_master_detail_workbook.png "Diagram showing master‑detail workbook flow")

## Δημιουργία βιβλίου εργασίας master‑detail – Βήμα 1: Αρχικοποίηση του βιβλίου εργασίας

Το πρώτο πράγμα που χρειαζόμαστε είναι μια νέα παρουσία `Workbook`. Σκεφτείτε το βιβλίο εργασίας ως καμβά όπου θα ζουν και τα φύλλα master και detail.

```java
import com.aspose.cells.*;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and add the master and detail worksheets
        Workbook workbook = new Workbook();                 // empty workbook with a default sheet
        Worksheet masterSheet = workbook.getWorksheets().get(0); // the first sheet becomes the master
        Worksheet detailSheet = workbook.getWorksheets().add("Details"); // add a detail sheet
```

*Γιατί είναι σημαντικό:* Το Aspose.Cells δημιουργεί πάντα ένα προεπιλεγμένο φύλλο, οπότε το επαναχρησιμοποιούμε ως master. Η προσθήκη ενός ονομασμένου φύλλου λεπτομερειών (`"Details"`) κάνει την μετέπειτα αναφορά Smart Marker πιο σαφή και διατηρεί το αρχείο τακτοποιημένο.

> **Συμβουλή:** Αν έχετε ήδη ένα αρχείο προτύπου, αντικαταστήστε το `new Workbook()` με το `new Workbook("template.xlsx")`. Τα υπόλοιπα βήματα παραμένουν τα ίδια.

## Εισαγωγή Smart Marker – Βήμα 2: Σύνδεση γραμμών master με το φύλλο λεπτομερειών

Τα Smart Markers είναι δείκτες που το Aspose.Cells αντικαθιστά με δεδομένα κατά την εκτέλεση. Η σύνταξη `${DataSource,DetailSheet=SheetName}` λέει στη μηχανή ποια δεδομένα να πάρει και πού να τοποθετήσει τις γραμμές λεπτομερειών.

```java
        // Step 2: Insert the Smart Marker that links the master data to the detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");
```

*Γιατί είναι σημαντικό:* Η τοποθέτηση του δείκτη στο `A2` σημαίνει ότι η γραμμή master θα ξεκινήσει ακριβώς κάτω από τη γραμμή κεφαλίδας (συνήθως `A1`). Το τμήμα `DetailSheet=Details` δημιουργεί αυτόματα μια **σχέση master‑detail**—κάθε γραμμή master δημιουργεί ένα μπλοκ γραμμών στο φύλλο `Details`.

> **Συχνή ερώτηση:** *Μπορώ να τοποθετήσω το δείκτη σε διαφορετική στήλη;* Απόλυτα. Απλώς προσαρμόστε την αναφορά κελιού (`B2`, `C2`, κλπ.) και βεβαιωθείτε ότι η διάταξη του προτύπου σας ταιριάζει.

## Παροχή πηγής δεδομένων – Βήμα 3: Σύνδεση POJO με το Smart Marker

Τώρα τροφοδοτούμε το Smart Marker με πραγματικά δεδομένα. Σε αυτό το παράδειγμα χρησιμοποιούμε μια λίστα από POJO `Order` που επιστρέφεται από μια βοηθητική κλάση `DataFactory`.

```java
        // Step 3: Provide the data source for the Smart Marker (a list of Order objects)
        List<Order> orders = DataFactory.getOrders();   // your POJO list
        workbook.getSmartMarkers().setDataSource("Orders", orders);
```

*Γιατί είναι σημαντικό:* Το κλειδί `"Orders"` πρέπει να ταιριάζει με το όνομα που χρησιμοποιείται μέσα στο placeholder `${...}`. Το Aspose.Cells θα επαναλάβει τη λίστα, δημιουργώντας μια γραμμή master για κάθε `Order` και θα αντλήσει τα σχετικά δεδομένα παιδιών (αν υπάρχουν) στο φύλλο λεπτομερειών.

> **Ακραία περίπτωση:** Αν η λίστα σας είναι κενή, το Smart Marker θα αφήσει απλώς την περιοχή master κενή—δεν θα ριχθεί εξαίρεση. Ωστόσο, ίσως θελήσετε να ελέγξετε το `orders.isEmpty()` εκ των προτέρων για να αποφασίσετε αν θα δημιουργηθεί το αρχείο.

## Επαναϋπολογισμός τύπων – Βήμα 4: Διατήρηση των υπολογισμών ενημερωμένων

Συχνά τα φύλλα master‑detail περιέχουν τύπους που αθροίζουν ποσότητες, υπολογίζουν σύνολα ή εφαρμόζουν φόρους. Μετά την εισαγωγή δεδομένων από το Smart Marker, χρειάζεται να επαναϋπολογίσουμε αυτούς τους τύπους.

```java
        // Step 4: Recalculate any formulas that may depend on the inserted data
        workbook.calculateFormula();
```

*Γιατί είναι σημαντικό:* Χωρίς αυτήν την κλήση, τα κελιά που αναφέρονται σε νεοεισαχθείσες γραμμές θα εμφανίζουν ακόμα τις παλιές (ή τιμές #DIV/0!). Η `calculateFormula()` διασχίζει ολόκληρο το βιβλίο εργασίας, διασφαλίζοντας ότι κάθε εξαρτημένο κελί αντικατοπτρίζει τα νέα δεδομένα.

> **Σημείωση απόδοσης:** Για τεράστια βιβλία εργασίας μπορείτε να περιορίσετε τον επαναϋπολογισμό σε συγκεκριμένο φύλλο χρησιμοποιώντας `worksheet.calculateFormula()`. Στις περισσότερες περιπτώσεις master‑detail η κλήση για ολόκληρο το βιβλίο εργασίας είναι εντάξει.

## Αποθήκευση αρχείου – Βήμα 5: Εξαγωγή του βιβλίου εργασίας master‑detail

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Μπορείτε να επιλέξετε οποιαδήποτε υποστηριζόμενη μορφή (`.xlsx`, `.xls`, `.csv`, κλπ.)—εδώ παραμένουμε στη σύγχρονη `.xlsx`.

```java
        // Step 5: Save the workbook with the master‑detail relationship applied
        workbook.save("output/master-detail.xlsx"); // adjust path as needed
    }
}
```

*Γιατί είναι σημαντικό:* Το αποθηκευμένο αρχείο περιέχει τώρα δύο φύλλα: **Sheet1** (το master) και **Details** (το detail). Ανοίγοντας το στο Excel θα δείτε μια ωραία μορφοποιημένη προβολή master‑detail, συμπληρωμένη με όλους τους τύπους που επαναϋπολογίσατε.

> **Προειδοποίηση:** Αν ξεχάσετε να καλέσετε τη `calculateFormula()` πριν την αποθήκευση, το Excel θα επαναϋπολογίσει κατά το άνοιγμα, κάτι που μπορεί να είναι πιο αργό και να παράγει διαφορετικά αποτελέσματα αν το βιβλίο εργασίας περιέχει ευμετάβλητους τύπους.

---

## Πλήρης κώδικας (εκτελέσιμος)

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο IDE σας:

```java
import com.aspose.cells.*;
import java.util.List;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize workbook and worksheets
        Workbook workbook = new Workbook();
        Worksheet masterSheet = workbook.getWorksheets().get(0);
        Worksheet detailSheet = workbook.getWorksheets().add("Details");

        // Optional: Add headers to master sheet
        masterSheet.getCells().get("A1").putValue("Order ID");
        masterSheet.getCells().get("B1").putValue("Customer");
        masterSheet.getCells().get("C1").putValue("Total");

        // Step 2: Insert Smart Marker linking to detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");

        // Step 3: Supply data source (list of Order POJOs)
        List<Order> orders = DataFactory.getOrders(); // assume this returns a populated list
        workbook.getSmartMarkers().setDataSource("Orders", orders);

        // Step 4: Recalculate formulas (if any)
        workbook.calculateFormula();

        // Step 5: Save the resulting workbook
        workbook.save("output/master-detail.xlsx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `master-detail.xlsx` και θα δείτε:

- **Sheet1** (master) που εμφανίζει κάθε ID παραγγελίας, όνομα πελάτη και σύνολο.  
- **Details** φύλλο που περιέχει γραμμές που ανήκουν σε κάθε παραγγελία (π.χ., στοιχεία γραμμής).  
- Οποιοσδήποτε τύπος συνόλου ή φόρου είναι σωστά συμπληρωμένος.

---

## Συχνά ζητούμενες παραλλαγές

| Question | Answer |
|----------|--------|
| *Μπορώ να χρησιμοποιήσω ένα πρότυπο αντί για κενό βιβλίο εργασίας;* | Ναι. Φορτώστε το με `new Workbook("template.xlsx")` και τοποθετήστε το Smart Marker στο κατάλληλο κελί. |
| *Τι γίνεται αν τα δεδομένα λεπτομερειών μου βρίσκονται σε ξεχωριστή λίστα;* | Μπορείτε να ενσωματώσετε Smart Markers: `${Orders.Details,DetailSheet=Details}` όπου το `Details` είναι μια ιδιότητα κάθε `Order` που επιστρέφει μια λίστα από στοιχεία γραμμής. |
| *Πώς μπορώ να μορφοποιήσω τις γραμμές λεπτομερειών;* | Εφαρμόστε ένα στυλ στην πρώτη γραμμή λεπτομερειών στο πρότυπο· το Aspose.Cells θα κλωνοποιήσει αυτό το στυλ για κάθε παραγόμενη γραμμή. |
| *Υπάρχει τρόπος να κρύψετε το φύλλο λεπτομερειών μέχρι να επεκταθεί μια γραμμή master;* | Δεν είναι δυνατόν άμεσα μέσω Smart Markers, αλλά μπορείτε να ορίσετε την ιδιότητα `Visible` του φύλλου σε `false` και να το εναλλάξετε με VBA μετά το άνοιγμα. |

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να δημιουργήσετε βιβλίο εργασίας master‑detail** σε Java χρησιμοποιώντας το Aspose.Cells Smart Marker. Από την αρχικοποίηση του βιβλίου εργασίας, την εισαγωγή του Smart Marker, τη σύνδεση μιας λίστας POJO, τον επαναϋπολογισμό τύπων, μέχρι την τελική αποθήκευση του αρχείου—κάθε βήμα εξηγήθηκε με το *γιατί* πίσω από αυτό, ώστε να μπορείτε να προσαρμόσετε το μοτίβο στα δικά σας έργα.

Δοκιμάστε να επεκτείνετε αυτό το παράδειγμα:

- Προσθέστε conditional formatting για να επισημάνετε παραγγελίες υψηλής αξίας.  
- Εξάγετε το βιβλίο εργασίας ως PDF με `workbook.save("report.pdf", SaveFormat.PDF)`.  
- Συνδυάστε πολλαπλές ενότητες master‑detail σε ένα μόνο αρχείο χρησιμοποιώντας διαφορετικά ονόματα Smart Marker.  

Οι έννοιες του **master‑

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία βιβλίου εργασίας Excel χρησιμοποιώντας Aspose.Cells σε Java: Οδηγός βήμα‑βήμα](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Κύρια διαχείριση αρχείων Excel με Aspose.Cells για Java | Οδηγός λειτουργιών βιβλίου εργασίας](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Πώς να δημιουργήσετε και να εξάγετε Excel σε HTML χρησιμοποιώντας Aspose.Cells Java | Οδηγός λειτουργιών βιβλίου εργασίας](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}