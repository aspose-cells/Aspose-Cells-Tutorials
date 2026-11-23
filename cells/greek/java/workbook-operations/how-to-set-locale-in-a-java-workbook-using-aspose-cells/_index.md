---
category: general
date: 2026-11-22
description: Μάθετε πώς να ορίζετε το locale σε ένα βιβλίο εργασίας Java, να αλλάζετε
  τη γλώσσα του βιβλίου εργασίας και να ορίζετε το ημερολόγιο στα Ιαπωνικά με σαφή
  παραδείγματα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: el
lastmod: 2026-11-22
og_description: Πώς να ορίσετε την τοπική ρύθμιση σε ένα βιβλίο εργασίας Java γρήγορα.
  Ακολουθήστε αυτό το σεμινάριο για να αλλάξετε τη γλώσσα του βιβλίου εργασίας, να
  ορίσετε την τοπική ρύθμιση στα Ιαπωνικά και να διαμορφώσετε το ιαπωνικό ημερολόγιο.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Πώς να ορίσετε το locale σε ένα βιβλίο εργασίας Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Πώς να ορίσετε την τοπική ρύθμιση σε ένα βιβλίο εργασίας Java χρησιμοποιώντας
  το Aspose.Cells
url: /el/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε το locale σε ένα βιβλίο εργασίας Java χρησιμοποιώντας το Aspose.Cells

Η ρύθμιση του locale σε ένα βιβλίο εργασίας Java είναι μια συνηθισμένη απαίτηση όταν χρειάζεται να προσαρμόσετε το λογιστικό φύλλο σας σε διαφορετικές περιοχές. Σε αυτόν τον οδηγό θα μάθετε πώς να ορίσετε το locale, να αλλάξετε τη γλώσσα του βιβλίου εργασίας και να ορίσετε το ημερολόγιο στα Ιαπωνικά χρησιμοποιώντας το API του Aspose.Cells.

Η διεθνοποίηση ενός βιβλίου εργασίας υπερβαίνει τη μετάφραση του κειμένου· επηρεάζει επίσης τις μορφές αριθμών, την ανάλυση ημερομηνιών και το προεπιλεγμένο σύστημα ημερολογίου. Στο τέλος αυτού του tutorial θα μπορείτε να:

* Διαμορφώσετε το locale του βιβλίου εργασίας σε Ιαπωνικά (Ιαπωνία) – **set locale to japanese**.  
* Αλλάξετε τη γλώσσα του βιβλίου εργασίας ώστε οι τύποι και τα UI strings να σέβονται τον στόχο πολιτισμού – **change workbook language**.  
* Αλλάξετε το ημερολόγιο στο ιαπωνικό αυτοκρατορικό ημερολόγιο – **how to set calendar**.  

Τα βήματα λειτουργούν με οποιαδήποτε πρόσφατη έκδοση του Aspose.Cells for Java (v23.9 ή νεότερη) και απαιτούν μόνο ένα τυπικό περιβάλλον ανάπτυξης Java.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|-------------|--------|
| Java 8 ή νεότερη | Η βιβλιοθήκη στοχεύει σε Java 8+. |
| Aspose.Cells for Java (v23.9+) | Παρέχει `Workbook`, `WorkbookSettings` και εργαλεία locale. |
| IDE (IntelliJ IDEA, Eclipse, ή VS Code) | Για τη μεταγλώττιση και εκτέλεση του παραδείγματος. |
| Βασικές γνώσεις Java | Απαιτούνται για την κατανόηση των αποσπασμάτων κώδικα. |

Προσθέστε την εξάρτηση Maven του Aspose.Cells στο `pom.xml` σας (ή κατεβάστε το JAR χειροκίνητα):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Πώς να ορίσετε locale και ημερολόγιο σε ένα βιβλίο εργασίας

Το πρώτο βήμα είναι να δημιουργήσετε μια παρουσία του workbook και να αποκτήσετε το αντικείμενο ρυθμίσεων του. Το αντικείμενο ρυθμίσεων εκθέτει τα API για locale και ημερολόγιο.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Γιατί κάθε γραμμή είναι σημαντική

* **`new Workbook()`** – Δημιουργεί ένα κενό workbook που μπορείτε να επεξεργαστείτε πριν το αποθηκεύσετε.  
* **`getSettings()`** – Επιστρέφει ένα αντικείμενο `WorkbookSettings`; όλες οι περιφερειακές επιλογές βρίσκονται εδώ.  
* **`setCalendar(...)`** – Αντικαθιστά το προεπιλεγμένο Γρηγοριανό ημερολόγιο με το ιαπωνικό αυτοκρατορικό ημερολόγιο, επηρεάζοντας τον τρόπο απόδοσης και ανάλυσης των ημερομηνιών.  
* **`setLocale(new Locale("ja","JP"))`** – Αλλάζει τη γλώσσα και τις περιφερειακές συμβάσεις (π.χ. μήνες, διαχωριστικά δεκαδικών). Αυτό αποτελεί τον πυρήνα του **how to set locale** για το workbook.  

Η εκτέλεση του προγράμματος δημιουργεί το `LocaleDemo.xlsx`. Ανοίξτε το στο Excel ή στο LibreOffice και θα δείτε τα ονόματα των μηνών στα Ιαπωνικά, τα σύμβολα νομίσματος Ιαπωνικού Γιεν και ημερομηνίες μορφοποιημένες σύμφωνα με το Ιαπωνικό ημερολόγιο.

## Αλλαγή γλώσσας βιβλίου εργασίας (ορισμός locale σε Ιαπωνικά)

Αν ο κύριος στόχος σας είναι η **αλλαγή γλώσσας του βιβλίου εργασίας**, μπορείτε να εστιάσετε μόνο στην κλήση `setLocale`. Το παρακάτω απόσπασμα απομονώνει αυτό το βήμα:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Τι αλλάζει;**

* Οι αλφαριθμητικές μορφές κελιών μεταβαίνουν στα Ιαπωνικά (π.χ., `#,##0.00` γίνεται `#,##0.00` με σύμβολο γιεν).  
* Τα ενσωματωμένα ονόματα συναρτήσεων (όπως `SUM`) παραμένουν στα Αγγλικά επειδή το locale των συναρτήσεων του Excel είναι ανεξάρτητο, αλλά οι συμβολοσειρές ημερομηνιών και τα μηνύματα σφάλματος ακολουθούν τις Ιαπωνικές συμβάσεις.  

**Πότε να το χρησιμοποιήσετε;**

* Όταν χρειάζεστε ένα λογιστικό φύλλο που εμφανίζει αριθμούς και ημερομηνίες για Ιαπωνικό κοινό, αλλά το υποκείμενο ημερολόγιο μπορεί να παραμείνει Γρηγοριανό.  
* Για αναφορές που εξάγονται σε PDF ή εκτυπώνονται, διασφαλίζοντας ότι η οπτική γλώσσα ταιριάζει με την αγορά-στόχο.

## Πώς να ορίσετε το ημερολόγιο στο Ιαπωνικό ημερολόγιο

Μερικές φορές η απαίτηση **how to set calendar** είναι ξεχωριστή από το locale. Για παλαιά συστήματα που αποθηκεύουν ημερομηνίες στην Ιαπωνική αυτοκρατορική εποχή, πρέπει να ορίσετε ρητά το ημερολόγιο ενώ διατηρείτε προαιρετικά το προεπιλεγμένο locale.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Κύρια σημεία:**

* `Calendar.getInstance(Locale.JAPAN)` επιστρέφει ένα `java.util.Calendar` διαμορφωμένο για την Ιαπωνική εποχή.  
* Το workbook τώρα θα εμφανίζει ημερομηνίες χρησιμοποιώντας σύμβολα εποχής (R για Reiwa, H για Heisei κ.λπ.).  
* Αυτή η ρύθμιση **δεν** επηρεάζει τη μορφοποίηση αριθμών ή τη γλώσσα UI· συνδυάστε την με `setLocale` εάν χρειάζεστε και τα δύο.

## Πλήρες παράδειγμα από την αρχή μέχρι το τέλος

Παρακάτω βρίσκεται ένα πλήρες, εκτελέσιμο πρόγραμμα που επιδεικνύει **how to set locale**, **change workbook language** και **set the calendar** σε μια ενιαία ροή. Προσθέτει επίσης ένα δείγμα κελιού για να απεικονίσει το αποτέλεσμα.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίγοντας το `FullJapaneseLocale.xlsx` εμφανίζεται το πρώτο κελί με ημερομηνία όπως `R3/04/01` (Reiwa 3) και το δεύτερο κελί μορφοποιημένο ως `¥1,234,567.89`. Αυτό επιβεβαιώνει ότι **how to set locale**, **change workbook language**, και **how to set calendar** λειτουργούν μαζί.

## Συνηθισμένα λάθη και πώς να τα αποφύγετε

| Παγίδα | Γιατί συμβαίνει | Διόρθωση |
|---------|----------------|-----|
| Χρήση του `Locale.CHINA` αντί του `new Locale("ja","JP")` | Το `Locale.CHINA` ορίζει τη γλώσσα στα Κινέζικα, όχι Ιαπωνικά. | Πάντα να δημιουργείτε το `Locale` με `"ja", "JP"` για Ιαπωνικά. |
| Ξέχνατε να καλέσετε `settings.setCalendar(...)` μετά το `setLocale` | Το ημερολόγιο προεπιλέγεται ως Γρηγοριανό, έτσι οι ημερομηνίες εμφανίζονται στην λάθος εποχή. | Καλέστε `setCalendar` **μετά** το `setLocale`, ή ορίστε και τα δύο μαζί όπως φαίνεται. |
| Αποθήκευση του workbook πριν την εφαρμογή των ρυθμίσεων | Οι ρυθμίσεις εφαρμόζονται στο αντικείμενο στη μνήμη· η πρόωρη αποθήκευση γράφει το προεπιλεγμένο locale. | Εφαρμόστε όλες τις αλλαγές locale/ημερολογίου **πριν** καλέσετε `workbook.save()`. |
| Χρήση παλιάς έκδοσης του Aspose.Cells | Οι παλαιότερες εκδόσεις δεν έχουν υπερφορτώσεις `setCalendar`. | Αναβαθμίστε στην έκδοση v23.9+ ή ελέγξτε τις σημειώσεις έκδοσης για υποστήριξη locale. |

## Δοκιμή της διαμόρφωσής σας

1. Εκτελέστε την κλάση **FullLocaleExample**.  
2. Ανοίξτε το παραγόμενο `FullJapaneseLocale.xlsx` στο Excel.  
3. Επαληθεύστε ότι:  
   * Η στήλη ημερομηνίας εμφανίζει σύμβολα Ιαπωνικής εποχής (`R`, `H`, κ.λπ.).  
   * Η στήλη αριθμών χρησιμοποιεί το σύμβολο Γιεν και διαχωριστικά κόμμα.  
   * Οποιαδήποτε ενσωματωμένα μηνύματα σφάλματος (π.χ., `#DIV/0!`) εμφανίζονται στα Ιαπωνικά εάν το workbook περιέχει σφάλματα.  

Εάν κάποιο από αυτά τα ελέγξιμα αποτύχει, ελέγξτε ξανά ότι το αντικείμενο `WorkbookSettings` που τροποποιήσατε είναι η ίδια παρουσία που χρησιμοποιείται κατά την αποθήκευση.

## Επόμενα βήματα

* **Τοπικοποίηση τύπων** – Ενώ το locale ελέγχει τη μορφοποίηση, μπορείτε επίσης να μεταφράσετε προσαρμοσμένα ονόματα συναρτήσεων χρησιμοποιώντας το `FormulaParser`.  
* **Εφαρμογή locale σε υπάρχοντα βιβλία εργασίας** – Φορτώστε ένα βιβλίο εργασίας με `new Workbook

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική Περίοδο;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose Cells Date Format: Πώς να ορίσετε προσαρμοσμένη μορφή ημερομηνίας σε Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Πώς να ορίσετε γλώσσα σε αρχεία Excel χρησιμοποιώντας Aspose.Cells .NET για πολυγλωσσική υποστήριξη](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Πώς να ορίσετε μορφή αριθμού κελιού και να μετατρέψετε Ιαπωνικές ημερομηνίες σε C# χρησιμοποιώντας Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}