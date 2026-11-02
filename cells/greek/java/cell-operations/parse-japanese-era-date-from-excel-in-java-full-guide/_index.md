---
category: general
date: 2026-10-07
description: Ανάγνωση ημερομηνίας από το Excel σε Java με Aspose.Cells. Αυτός ο οδηγός
  σας δείχνει πώς να αναλύσετε ημερομηνίες ιαπωνικής εποχής, να διαβάσετε ημερομηνία
  από κελιά του Excel και να εξάγετε datetime από κελιά του Excel γρήγορα.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Ανάγνωση ημερομηνίας από το Excel σε Java με Aspose.Cells. Αυτός ο
  οδηγός σας δείχνει πώς να αναλύσετε ημερομηνίες ιαπωνικής εποχής, να διαβάσετε ημερομηνία
  από κελιά του Excel και να εξάγετε datetime από κελιά του Excel σε λίγα μόνο βήματα.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Ανάγνωση ημερομηνίας από το Excel σε Java με Aspose.Cells – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Ανάγνωση ημερομηνίας από το Excel σε Java με Aspose.Cells – πλήρης οδηγός
url: /el/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανάγνωση ημερομηνίας από το Excel σε Java με Aspose.Cells – πλήρης οδηγός

Αν χρειάζεστε να **διαβάσετε ημερομηνία από το Excel** φύλλα εργασίας που περιέχουν ιαπωνικές συμβολοσειρές εποχής, βρίσκεστε στο σωστό μέρος. Σε πολλά παλιά λογιστικά ή κυβερνητικά υπολογιστικά φύλλα η ημερομηνία αποθηκεύεται ως “令和3年5月10日”, και η μετατροπή της σε ένα τυπικό Γρηγοριανό `LocalDateTime` μπορεί να είναι επιρρεπής σε σφάλματα. Αυτό το tutorial σας δείχνει, βήμα προς βήμα, πώς να ενεργοποιήσετε την ανάλυση με γνώση εποχής, να διαβάσετε την τιμή του κελιού, και **να εξάγετε datetime από το Excel** χρησιμοποιώντας το Aspose.Cells για Java.

## Γρήγορες απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται ημερομηνίες ιαπωνικής εποχής;** Aspose.Cells for Java.
- **Ποια έκδοση Java απαιτείται;** Java 17 ή νεότερη (Java 8 λειτουργεί επίσης).
- **Χρειάζομαι άδεια για δοκιμές;** Μια δωρεάν δοκιμή είναι επαρκής για ανάπτυξη.
- **Μπορεί ο ίδιος κώδικας να διαβάσει Γρηγοριανές ημερομηνίες;** Ναι, το API ανιχνεύει αυτόματα τη μορφή.
- **Διατηρείται η πληροφορία ώρας;** Απόλυτα – οι ώρες, τα λεπτά και τα δευτερόλεπτα διατηρούνται μετά τη μετατροπή.

## Τι είναι η ανάγνωση ημερομηνίας από το Excel;
Η φράση “read date from Excel” αναφέρεται στην ανάκτηση της τιμής ημερομηνίας ενός κελιού και τη μετατροπή της σε ένα αντικείμενο ημερομηνίας‑ώρας Java, όπως το `java.time.LocalDateTime`. Το Aspose.Cells αφαιρεί την πολυπλοκότητα του χαμηλού επιπέδου δυαδικού φορμάτ του Excel, ώστε να μπορείτε να εργάζεστε με ημερομηνίες χωρίς χειροκίνητη ανάλυση συμβολοσειρών.

## Γιατί να χρησιμοποιήσετε το Aspose.Cells για ανάλυση ιαπωνικής εποχής;
Το Aspose.Cells υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί βιβλία εργασίας πολλαπλών εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Ο ενσωματωμένος parser με γνώση εποχής μετατρέπει κάθε ιαπωνική εποχή (Meiji, Taishō, Shōwa, Heisei, Reiwa) σε Γρηγοριανές ημερομηνίες με μία κλήση API, εξαλείφοντας τον ασταθή κώδικα κανονικών εκφράσεων.

## Προαπαιτούμενα
- Java 17 (ή Java 8+) εγκατεστημένο στον υπολογιστή σας.
- Σύστημα κατασκευής Maven ή Gradle.
- Βασική εξοικείωση με αρχεία Excel.
- Βιβλιοθήκη Aspose.Cells for Java (έκδοση δοκιμής ή με άδεια).

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—θα δείτε ακριβώς πώς να προσθέσετε τη βιβλιοθήκη στο επόμενο βήμα.

## Πώς να διαβάσετε ημερομηνία από το Excel σε Java;

Φορτώστε το βιβλίο εργασίας σας, ενεργοποιήστε την ανάλυση με γνώση εποχής, και ζητήστε από το κελί την τιμή `DateTime`. Ολόκληρη η διαδικασία απαιτεί **δύο γραμμές λειτουργικού κώδικα** μόλις η βιβλιοθήκη είναι στο classpath.

### Βήμα 1: προσθέστε το Aspose.Cells στο έργο σας

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Μετά την επίλυση της εξάρτησης, μπορείτε να αρχίσετε να χρησιμοποιείτε το API για **να διαβάσετε ημερομηνία από το Excel** στα κελιά.

### Βήμα 2: δημιουργήστε ένα βιβλίο εργασίας και στοχεύστε το πρώτο φύλλο εργασίας

Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη. Η δημιουργία μιας νέας στιγμής εγγυάται ένα καθαρό περιβάλλον για τα επόμενα βήματα ανάλυσης.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Βήμα 3: τοποθετήστε μια συμβολοσειρά ημερομηνίας ιαπωνικής εποχής στο κελί A1

Για επίδειξη γράφουμε τη συμβολοσειρά εποχής εμείς· στην παραγωγή θα φορτώνατε ένα υπάρχον `.xlsx`.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Το κείμενο ακολουθεί το συμβατικό ιαπωνικό μοτίβο: *Εποχή* + *Έτος* + *Μήνας* + *Ημέρα*.

### Βήμα 4: ενεργοποιήστε την ανάλυση ημερομηνίας με γνώση εποχής

Ενημερώστε το Aspose.Cells να αντιμετωπίζει τις συμβολοσειρές εποχής ως ημερομηνίες ορίζοντας τη σημαία `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` είναι μια ιδιότητα που, όταν είναι true, ενεργοποιεί την αυτόματη μετατροπή των ιαπωνικών συμβολοσειρών εποχής σε Γρηγοριανές ημερομηνίες.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Χωρίς αυτή τη σημαία, η βιβλιοθήκη θα αντιμετωπίζει το “令和3年5月10日” ως απλό κείμενο, και θα χάνατε την αυτόματη μετατροπή.

### Βήμα 5: ανακτήστε την αναλυμένη τιμή DateTime

Τώρα ζητήστε από το κελί την αναπαράσταση της ημερομηνίας του. `cell.getDateTime()` επιστρέφει την τιμή του κελιού ως αντικείμενο `java.util.Date`. Η μέθοδος επιστρέφει ένα `java.util.Date`, το οποίο μετατρέπουμε αμέσως στη σύγχρονη `java.time.LocalDateTime`. Η `LocalDateTime` είναι μια κλάση Java που αντιπροσωπεύει ημερομηνία και ώρα χωρίς ζώνη ώρας.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Αυτό ικανοποιεί την απαίτηση **εξαγωγής datetime από το Excel** με ασφαλή τύπο.

### Βήμα 6: επαληθεύστε το αποτέλεσμα

Εκτυπώστε τη Γρηγοριανή ημερομηνία για να επιβεβαιώσετε ότι η μετατροπή πέτυχε.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε:

```
2021-05-10T00:00
```

Η έξοδος αποδεικνύει ότι διαβάσαμε επιτυχώς **ημερομηνία από το Excel**, αναλύσαμε την ιαπωνική εποχή, και **εξάγαμε datetime από το Excel** σε μια ενιαία ροή.

## Διαχείριση πραγματικών περιπτώσεων άκρων

### Πολλαπλές εποχές

Η Ιαπωνία έχει πολλές εποχές (Meiji, Taishō, Shōwa, Heisei, Reiwa). Η σημαία `setParseDateUsingJapaneseEra(true)` καλύπτει όλες αυτόματα, αλλά να γνωρίζετε ότι παλαιότερες ημερομηνίες μπορεί να βρίσκονται εκτός του υποστηριζόμενου εύρους της βιβλιοθήκης (συνήθως 1868‑σήμερα). Αν συναντήσετε μια ημερομηνία όπως “昭和45年12月31日”, ο ίδιος κώδικας θα τη μετατρέψει σε 1970‑12‑31.

### Κενά ή μη έγκυρα κελιά

Αν ένα κελί είναι κενό ή περιέχει εσφαλμένη συμβολοσειρά, το `cell.getDateTime()` ρίχνει ένα `CellsException`. Προστατέψτε το με έναν απλό έλεγχο:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Στοιχείο ώρας

Το παράδειγμα περιλαμβάνει μόνο ημερομηνία, αλλά αν το αρχείο Excel σας αποθηκεύει επίσης ώρα (π.χ., “令和3年5月10日 14:30”), το Aspose.Cells θα διατηρήσει το τμήμα ώρας. Η `LocalDateTime` που λαμβάνετε θα περιλαμβάνει ώρες, λεπτά και δευτερόλεπτα.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα έτοιμο για αντιγραφή‑επικόλληση:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Αποθηκεύστε το ως `JapaneseEraDateParser.java`, μεταγλωττίστε με `javac`, και εκτελέστε με `java`. Αν όλα είναι ρυθμισμένα σωστά, θα δείτε τη Γρηγοριανή ημερομηνία να εκτυπώνεται στην κονσόλα.

## Επαγγελματικές συμβουλές & κοινά λάθη

- **Συμβουλή:** Ενεργοποιήστε το `setParseDateUsingJapaneseEra(true)` **πριν** διαβάσετε οποιεσδήποτε τιμές κελιών. Η αλλαγή της σημαίας αργότερα δεν θα μετατρέψει εκ των προτέρων τα ήδη διαβασμένα κελιά.
- **Σημείωση τοπικής ρύθμισης:** Ο parser λειτουργεί με τους ίδιους χαρακτήρες Unicode, επομένως δεν χρειάζεται να ορίσετε ιαπωνική τοπική ρύθμιση ρητά.
- **Απόδοση:** Η ανάλυση εποχής προσθέτει αμελητέο κόστος. Αν τη χρειάζεστε μόνο για λίγα κελιά, ενεργοποιήστε τη σημαία μόνο για αυτές τις αναγνώσεις.
- **Δοκιμή:** Χρησιμοποιήστε τη δωρεάν δοκιμή του Aspose για να επικυρώσετε έναν πραγματικό βιβλίο εργασίας που συνδυάζει Γρηγοριανές και ημερομηνίες εποχής. Αυτό εξασφαλίζει ότι ο κώδικας παραγωγής λειτουργεί όπως αναμένεται.

## Συχνές ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτή τη μέθοδο με ένα υπάρχον αρχείο .xlsx;**  
A: Ναι. Φορτώστε το αρχείο με `new Workbook("path/to/file.xlsx")` και η ίδια σημαία θα αναλύσει τυχόν συμβολοσειρές εποχής που θα βρει.

**Q: Τι συμβαίνει αν το κελί περιέχει μια Γρηγοριανή ημερομηνία;**  
A: Η βιβλιοθήκη επιστρέφει την Γρηγοριανή τιμή αμετάβλητη· η ανάλυση εποχής επηρεάζει μόνο τις συμβολοσειρές που ταιριάζουν στο μοτίβο εποχής.

**Q: Υποστηρίζει το Aspose.Cells ημερομηνίες προγενέστερες από τη Meiji (1868);**  
A: Όχι. Οι ημερομηνίες πριν το 1868 είναι εκτός του υποστηριζόμενου εύρους και θα αντιμετωπίζονται ως απλό κείμενο.

**Q: Πώς να διαχειριστώ μεγάλα βιβλία εργασίας χωρίς να εξαντλήσω τη μνήμη;**  
A: Χρησιμοποιήστε τον κατασκευαστή `Workbook` που δέχεται `LoadOptions` με `setMemorySetting(MemorySetting.MemoryPreference)` για να ρέετε τα δεδομένα αντί να φορτώνετε τα πάντα ταυτόχρονα.

**Q: Απαιτείται εμπορική άδεια για χρήση σε παραγωγή;**  
A: Ναι, μια έγκυρη άδεια Aspose.Cells αφαιρεί τους περιορισμούς αξιολόγησης και ενεργοποιεί την πλήρη απόδοση.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Κατακτήστε το σύστημα ημερομηνίας 1904 στο Excel χρησιμοποιώντας το Aspose.Cells Java για αποτελεσματικές λειτουργίες κελιών](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Αποτελεσματική μετατροπή Excel σε PDF με προσαρμοσμένες μορφές ημερομηνίας χρησιμοποιώντας το Aspose.Cells για Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Πώς να επιλέξετε περιοχές κελιών στο Excel χρησιμοποιώντας το Aspose.Cells για Java (οδηγός 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Τελευταία ενημέρωση:** 2026-10-07  
**Δοκιμάστηκε με:** Aspose.Cells 24.12 for Java  
**Συγγραφέας:** Aspose

## Σχετικά tutorials

- [Ανάλυση ημερομηνίας ιαπωνικής εποχής από το Excel σε Java – πλήρης οδηγός](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Ανάγνωση αρχείου Excel σε Java με Aspose.Cells – πλήρης οδηγός](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Αποθήκευση βιβλίου εργασίας Excel με Aspose.Cells για Java – πλήρης οδηγός](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}