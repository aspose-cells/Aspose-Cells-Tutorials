---
date: 2026-08-21
description: Μάθετε πώς να προσθέσετε tooltips, data labels και να αλλάξετε chart
  type σε διαγράμματα Excel χρησιμοποιώντας Aspose.Cells for Java – βήμα‑βήμα οδηγός
  με διαδραστικά παραδείγματα.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Αλλαγή chart type Excel
og_description: Μάθετε πώς να προσθέσετε tooltips, data labels και να αλλάξετε chart
  type σε διαγράμματα Excel χρησιμοποιώντας Aspose.Cells for Java – βήμα‑βήμα οδηγός
  με διαδραστικά παραδείγματα.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Πώς να προσθέσετε tooltips και data labels σε διαγράμματα Excel σε Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Πώς να προσθέσετε tooltips και data labels σε διαγράμματα Excel σε Java
url: /el/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη ετικετών δεδομένων σε γράφημα Excel και αλλαγή τύπου γραφήματος – Aspose.Cells Java

Τα διαδραστικά γραφήματα δίνουν στις αναφορές Excel σας ένα νέο επίπεδο κατανόησης, και **πώς να προσθέσετε υποδείξεις** κάνουν τις πληροφορίες άμεσα αναγνώσιμες. Σε αυτό το σεμινάριο θα μάθετε πώς να **προσθέσετε ετικέτες δεδομένων σε γράφημα Excel**, **αλλάξετε τον τύπο του γραφήματος**, και να δημιουργήσετε διαδραστικές λύσεις Java με το Aspose.Cells. Θα σας δείξουμε επίσης πώς να προσθέσετε υποδείξεις και έναν απλό υπερσύνδεσμο drill‑down ώστε το κοινό σας να μπορεί να εξερευνήσει τα δεδομένα σε βάθος.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose.Cells for Java  
- **Μπορώ να αλλάξω τον τύπο του γραφήματος;** Ναι – απλώς τροποποιήστε το enum `ChartType` όταν δημιουργείτε το γράφημα.  
- **Πώς να προσθέσω υποδείξεις σε ένα γράφημα;** Χρησιμοποιήστε το API ετικετών δεδομένων (`setHasDataLabels(true)`) και ενεργοποιήστε την εμφάνιση τιμής.  
- **Υποστηρίζεται η δυνατότητα drill‑down;** Μπορείτε να συνδέσετε υπερσυνδέσμους σε σημεία δεδομένων για βασική λειτουργία drill‑down.  
- **Προαπαιτούμενα;** Java IDE, Aspose.Cells JAR, και ένα αρχείο Excel με δείγμα δεδομένων.

## Τι είναι η προσθήκη υποδείξεων;
**Η προσθήκη υποδείξεων** αναφέρεται στη διαδικασία ενεργοποίησης κειμένου κατά το πέρασμα του ποντικιού που εμφανίζει την τιμή ενός σημείου δεδομένων ή προσαρμοσμένες πληροφορίες σε ένα γράφημα Excel. Στο Aspose.Cells αυτό επιτυγχάνεται μέσω των ρυθμίσεων ετικετών δεδομένων του γραφήματος. Οι υποδείξεις βοηθούν τους χρήστες να κατανοούν γρήγορα τα δεδομένα χωρίς να γεμίζουν το γράφημα, και μπορούν να προσαρμοστούν για γραμματοσειρά, χρώμα και μορφή.

## Γιατί να χρησιμοποιήσετε διαδραστικά γραφήματα με το Aspose.Cells;
Το Aspose.Cells υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** — συμπεριλαμβανομένων των XLSX, CSV, PDF και HTML — και μπορεί να επεξεργαστεί βιβλία εργασίας με **πάνω από 1 000 φύλλα** χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, παρέχοντας γρήγορη δημιουργία γραφημάτων στον διακομιστή για επιχειρησιακή αναφορά. Τα διαδραστικά γραφήματα επιτρέπουν επίσης την ενσωμάτωση υπερσυνδέσμων, δυναμικές ενημερώσεις δεδομένων και εξαγωγή σε μορφές φιλικές για το web, καθιστώντας τα ιδανικά για πίνακες ελέγχου και πύλες αναφορών.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- Περιβάλλον Ανάπτυξης Java (συνιστάται JDK 8+)  
- Βιβλιοθήκη Aspose.Cells for Java (κατεβάστε από τη [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- Ένα δείγμα βιβλίου εργασίας (`data.xlsx`) που περιέχει τα δεδομένα που θέλετε να οπτικοποιήσετε  

## Βήμα 1: ρύθμιση του έργου Java σας

1. Δημιουργήστε ένα νέο έργο Java στο αγαπημένο σας IDE (IntelliJ IDEA, Eclipse κ.λπ.).  
2. Προσθέστε το Aspose.Cells JAR στη διαδρομή κατασκευής του έργου ή στις εξαρτήσεις Maven/Gradle.

## Βήμα 2: φόρτωση δεδομένων

Για να εργαστείτε με γραφήματα, πρώτα χρειάζεστε ένα βιβλίο εργασίας φορτωμένο στη μνήμη.

Η κλάση `Workbook` αντιπροσωπεύει ένα αρχείο Excel, και η `Worksheet` αντιπροσωπεύει ένα μοναδικό φύλλο εντός αυτού του αρχείου.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Πώς να αλλάξετε τον τύπο γραφήματος στο Aspose.Cells;

Δημιουργήστε ένα νέο γράφημα με το επιθυμητό enum `ChartType`; το Aspose.Cells δεν τροποποιεί τον τύπο ενός υπάρχοντος γραφήματος επί τόπου, επομένως πρέπει να προσθέσετε ένα νέο γράφημα του σωστού τύπου και προαιρετικά να αφαιρέσετε το παλιό. Αυτή η προσέγγιση εγγυάται ότι όλες οι σειρές και οι άξονες θα ξαναχτιστούν σωστά για τη νέα οπτική αναπαράσταση.

## Βήμα 3: δημιουργία γραφήματος (και αλλαγή του τύπου του)

Μπορείτε να επιλέξετε οποιονδήποτε τύπο γραφήματος που ταιριάζει στην ανάλυσή σας. Παρακάτω δημιουργούμε ένα **γράφημα στήλης**, αλλά μπορείτε εύκολα να μεταβείτε σε γραμμικό, πίτας ή ραβδόγραμμα αλλάζοντας το enum `ChartType`.

Το αντικείμενο `Chart` παρέχει μεθόδους για τη διαμόρφωση της οπτικής αναπαράστασης των δεδομένων στο φύλλο εργασίας.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Συμβουλή:** Για **αλλαγή τύπου γραφήματος Excel**, αντικαταστήστε το `ChartType.COLUMN` με `ChartType.LINE`, `ChartType.PIE`, κ.λπ.

## Πώς να προσθέσετε υποδείξεις σε ένα γράφημα Excel;

Φορτώστε το γράφημα σας, ενεργοποιήστε τις ετικέτες δεδομένων και ορίστε τη σημαία `showValue`. Η υπόδειξη θα εμφανίζει τότε την υποκείμενη τιμή του κελιού όποτε ο χρήστης περνάει το ποντίκι πάνω από ένα σημείο δεδομένων στο αποδοθέν αρχείο Excel ή στην προβολή HTML. Μπορείτε επίσης να προσαρμόσετε τη γραμματοσειρά, το χρώμα και το φόντο της υπόδειξης ώστε να ταιριάζει με το στυλ της αναφοράς σας.

Η κλάση `DataLabel` ελέγχει την εμφάνιση και το περιεχόμενο των ετικετών δεδομένων, οι οποίες λειτουργούν επίσης ως υποδείξεις.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Βήμα 4: προσθήκη διαδραστικότητας

### 4.1. Προσθήκη υποδείξεων (add tooltips to chart)

Οι υποδείξεις εμφανίζονται όταν ο χρήστης περνάει το ποντίκι πάνω από ένα σημείο δεδομένων. Ο παρακάτω κώδικας ενεργοποιεί τις ετικέτες δεδομένων και εμφανίζει την τιμή ως υπόδειξη.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Προσθήκη ετικετών δεδομένων – **add data labels to excel chart**

Οι ετικέτες δεδομένων παρέχουν μια μόνιμη οπτική ένδειξη στο ίδιο το γράφημα. Μπορείτε να τις εμφανίσετε ως κλήσεις για καλύτερη αναγνωσιμότητα.

Η κλάση `DataLabel` ελέγχει την εμφάνιση των ετικετών σε κάθε σειρά. Καλώντας το `setHasDataLabels(true)` και ρυθμίζοντας ιδιότητες όπως `setShowValue(true)`, ενσωματώνετε την αριθμητική τιμή απευθείας στο γράφημα, κάνοντάς την άμεσα ορατή χωρίς καμία αλληλεπίδραση. Επιπλέον επιλογές σας επιτρέπουν να εμφανίσετε ονόματα σειρών, ποσοστά ή προσαρμοσμένο κείμενο για πιο πλούσιο περιεχόμενο.

> **Γιατί να προσθέσετε ετικέτες δεδομένων;** Η ένταξη ετικετών δεδομένων απευθείας στο γράφημα εξαλείφει την ανάγκη των χρηστών να περνούν το ποντίκι ή να μαντεύουν τιμές, βελτιώνοντας την σαφήνεια της αναφοράς.

### 4.3. Υλοποίηση drill‑down (hyperlink on a data point)

Ένας απλός τρόπος για να προσθέσετε δυνατότητα drill‑down είναι να συνδέσετε έναν υπερσύνδεσμο σε ένα συγκεκριμένο σημείο. Κάνοντας κλικ στο σημείο ανοίγει μια ιστοσελίδα με λεπτομερείς πληροφορίες.

Η κλάση `Hyperlink` προσθέτει έναν κλικ-συνδέσιμο σύνδεσμο σε στοιχείο γραφήματος, επιτρέποντας πλοήγηση drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Πώς να προσθέσετε ετικέτες δεδομένων σε ένα γράφημα Excel;

Η κλάση `DataLabel` ελέγχει την εμφάνιση των ετικετών σε κάθε σειρά. Καλώντας το `setHasDataLabels(true)` και ρυθμίζοντας ιδιότητες όπως `setShowValue(true)`, ενσωματώνετε την αριθμητική τιμή απευθείας στο γράφημα, κάνοντάς την άμεσα ορατή χωρίς καμία αλληλεπίδραση. Επιπλέον επιλογές σας επιτρέπουν να εμφανίσετε ονόματα σειρών, ποσοστά ή προσαρμοσμένο κείμενο για πιο πλούσιο περιεχόμενο.

## Βήμα 5: αποθήκευση του βιβλίου εργασίας

Μετά τη διαμόρφωση του γραφήματος, αποθηκεύστε το βιβλίο εργασίας ώστε οι διαδραστικές λειτουργίες να αποθηκευτούν στο αρχείο εξόδου.

Η κλήση `workbook.save` γράφει το τροποποιημένο βιβλίο εργασίας σε αρχείο στην επιλεγμένη μορφή.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Συχνά προβλήματα & λύσεις

| Πρόβλημα | Λύση |
|-------|----------|
| **Οι υποδείξεις δεν εμφανίζονται** | Βεβαιωθείτε ότι το `setHasDataLabels(true)` καλείται πριν τη ρύθμιση του `setShowValue(true)`. |
| **Ο υπερσύνδεσμος δεν είναι κλικ-δυνατός** | Επαληθεύστε ότι η μορφή εξόδου υποστηρίζει υπερσυνδέσμους (π.χ., XLSX, όχι CSV). |
| **Ο τύπος γραφήματος δεν αλλάζει** | Ελέγξτε ξανά ότι τροποποιήσατε το σωστό enum `ChartType` κατά την προσθήκη του γραφήματος. |

## Συχνές ερωτήσεις

**Q: Πώς μπορώ να αλλάξω τον τύπο του γραφήματος μετά τη δημιουργία του;**  
A: Πρέπει να δημιουργήσετε ένα νέο γράφημα με το επιθυμητό `ChartType`. Το Aspose.Cells δεν παρέχει μετατροπή τύπου επί τόπου, επομένως αφαιρέστε το παλιό γράφημα και προσθέστε ένα νέο.

**Q: Μπορώ να προσαρμόσω την εμφάνιση των υποδείξεων;**  
A: Ναι. Χρησιμοποιήστε τις ιδιότητες της `DataLabel` όπως `setFontSize`, `setFontColor` και `setBackgroundColor` για να μορφοποιήσετε το κείμενο της υπόδειξης.

**Q: Πώς διαχειρίζομαι τις αλληλεπιδράσεις των χρηστών σε μια web εφαρμογή;**  
A: Εξάγετε το βιβλίο εργασίας σε αρχείο HTML ή XLSX και χρησιμοποιήστε JavaScript στην πλευρά του πελάτη για να καταγράψετε τα κλικ σε στοιχεία γραφήματος.

**Q: Πού μπορώ να βρω περισσότερα παραδείγματα και τεκμηρίωση;**  
A: Επισκεφθείτε το [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) για πλήρη λίστα των κλάσεων και μεθόδων σχετικών με τα γραφήματα.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **προσθέσετε ετικέτες δεδομένων σε γράφημα Excel**, **αλλάξετε τον τύπο γραφήματος Excel**, **δημιουργήσετε διαδραστικές λύσεις Java για γραφήματα**, και να τα εμπλουτίσετε με υποδείξεις, ετικέτες δεδομένων και υπερσυνδέσμους drill‑down χρησιμοποιώντας το Aspose.Cells for Java. Αυτές οι βελτιώσεις κάνουν τις αναφορές Excel σας πολύ πιο ελκυστικές και περιεκτικές για τους τελικούς χρήστες.

---

**Τελευταία ενημέρωση:** 2026-08-21  
**Δοκιμή με:** Aspose.Cells for Java 24.12  
**Συγγραφέας:** Aspose

## Σχετικά Σεμινάρια

- [Πώς να τροποποιήσετε τα γραφήματα Excel και τις ετικέτες δεδομένων χρησιμοποιώντας Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Εξαγωγή ετικετών άξονα γραφήματος Excel χρησιμοποιώντας Aspose.Cells Java: Ένας ολοκληρωμένος οδηγός](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Δημιουργία γραφημάτων φυσαλίδων σε Excel χρησιμοποιώντας Aspose.Cells for Java: Οδηγός βήμα‑βήμα](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}