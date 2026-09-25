---
date: '2026-04-11'
description: Μάθετε πώς να εμφανίζετε την έκδοση του Aspose Cells, να φορτώνετε βιβλίο
  εργασίας Excel σε Java και να διαχειρίζεστε τα enums των διαγραμμάτων με το Aspose.Cells.
  Ακολουθήστε παραδείγματα βήμα‑προς‑βήμα.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: Εμφάνιση έκδοσης Aspose Cells & διαχείριση Enum διαγραμμάτων σε Java
url: /el/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Εμφάνιση Έκδοσης Aspose Cells και Διαχείριση Enum Διαγραμμάτων σε Java

## Εισαγωγή

Αν χρειάζεστε να **display Aspose Cells version**, φορτώσετε ένα βιβλίο εργασίας Excel σε Java και να εργαστείτε με enum διαγραμμάτων, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε βήμα προς βήμα τις ακριβείς ενέργειες που χρειάζεστε για να ενσωματώσετε το Aspose.Cells for Java στα έργα σας, να εξάγετε δεδομένα διαγράμματος και να μετατρέψετε enums βασισμένα σε ακέραιους σε αναγνώσιμες συμβολοσειρές. Στο τέλος θα έχετε μια σταθερή, έτοιμη για παραγωγή λύση που μπορείτε να ενσωματώσετε απευθείας στον κώδικά σας.

**Τι Θα Μάθετε**
- Πώς να εμφανίσετε την έκδοση του Aspose.Cells.
- Πώς να **load Excel workbook Java** και να έχετε πρόσβαση σε δεδομένα διαγράμματος.
- Πώς να μετατρέψετε τιμές enum ακέραιων σε αντίστοιχες συμβολοσειρές.
- Πώς να ανακτήσετε τους τύπους τιμών X και Y από ένα σημείο διαγράμματος.

Ας ξεκινήσουμε!

## Γρήγορες Απαντήσεις
- **Πώς μπορώ να ελέγξω την έκδοση του Aspose.Cells;** Call `CellsHelper.getVersion()` and print the result.  
- **Ποιο Maven coordinate προσθέτει το Aspose.Cells;** `com.aspose:aspose-cells:25.3`.  
- **Μπορώ να φορτώσω ένα βιβλίο εργασίας Excel σε Java;** Ναι—use `new Workbook(filePath)`.  
- **Πώς μετατρέπονται οι τιμές enum;** Store a `HashMap<Integer, String>` and look up the integer key.  
- **Ποια μέθοδος εκτυπώνει τους τύπους τιμών X/Y;** `pnt.getXValueType()` and `pnt.getYValueType()`.

## Τι είναι το “display Aspose Cells version”;
Η φράση αναφέρεται στην ανάκτηση της συμβολοσειράς έκδοσης χρόνου εκτέλεσης της βιβλιοθήκης. Η γνώση της ακριβούς έκδοσης βοηθά στον εντοπισμό σφαλμάτων, στην εξασφάλιση συμβατότητας και στην επιβεβαίωση ότι η άδειά σας εφαρμόζεται στην προοριζόμενη έκδοση.

## Γιατί να εμφανίσετε την έκδοση και να φορτώσετε ένα βιβλίο εργασίας Excel σε Java;
- **Debugging** – Επιβεβαιώνει ότι η σωστή βιβλιοθήκη βρίσκεται στο classpath.  
- **Compliance** – Διευκολύνει την επαλήθευση ότι χρησιμοποιείτε μια αδειοδοτημένη έκδοση.  
- **Automation** – Ενεργοποιεί σενάρια που προσαρμόζονται σε διαφορετικές εκδόσεις της βιβλιοθήκης χωρίς χειροκίνητες αλλαγές.  

## Προαπαιτούμενα

### Απαιτούμενες Βιβλιοθήκες και Εξαρτήσεις
- **Aspose.Cells for Java** – βασική βιβλιοθήκη για τη διαχείριση Excel.  
- **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη.

### Ρύθμιση Περιβάλλοντος
- IDE της επιλογής σας (IntelliJ IDEA, Eclipse, NetBeans).  
- Εργαλείο κατασκευής: Maven **or** Gradle (οδηγίες παρακάτω).

### Απαιτούμενες Γνώσεις
- Βασικός προγραμματισμός Java.  
- Εξοικείωση με έννοιες Excel ( φύλλα εργασίας, διαγράμματα) είναι χρήσιμη αλλά όχι απαραίτητη.

## Ρύθμιση Aspose.Cells για Java

### Using Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Using Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Βήματα Απόκτησης Άδειας
- **Free Trial**: Download from [Σελίδα Κυκλοφορίας Aspose](https://releases.aspose.com/cells/java/).  
- **Temporary License**: Get a short‑term license at [Σελίδα Προσωρινής Άδειας Aspose](https://purchase.aspose.com/temporary-license/).  
- **Purchase**: For long‑term projects, buy a license via the [Σελίδα Αγοράς Aspose](https://purchase.aspose.com/buy).

### Βασική Αρχικοποίηση και Ρύθμιση
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## Οδηγός Υλοποίησης

### Πώς να Εμφανίσετε την Έκδοση Aspose Cells
**Overview** – Γρήγορη επαλήθευση της έκδοσης της βιβλιοθήκης σε χρόνο εκτέλεσης.

#### Βήμα 1: Εισαγωγή Απαιτούμενων Πακέτων
```java
import com.aspose.cells.*;
```

#### Βήμα 2: Δημιουργία Κλάσης και Μεθόδου main
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### Επεξήγηση
- `CellsHelper.getVersion()` επιστρέφει τη συγκεκριμένη συμβολοσειρά έκδοσης του Aspose.Cells DLL που χρησιμοποιεί η εφαρμογή σας.

### Πώς να Μετατρέψετε Ακέραια Enums σε String Enums
**Overview** – Μετασχηματισμός αριθμητικών τιμών enum (π.χ., `CellValueType.IS_NUMERIC`) σε αναγνώσιμο κείμενο.

#### Βήμα 1: Ρύθμιση HashMap για Μετατροπή
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Βήμα 2: Μετατροπή και Εκτύπωση Τιμής Enum
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### Επεξήγηση
- Ο χάρτης `cvTypes` γεφυρώνει το κενό μεταξύ της αριθμητικής σταθεράς και μιας ετικέτας αναγνώσιμης από άνθρωπο.

### Πώς να Φορτώσετε ένα Βιβλίο Εργασίας Excel σε Java και να Πρόσβαση σε Δεδομένα Διαγράμματος
**Overview** – Άνοιγμα υπάρχοντος βιβλίου εργασίας, εντοπισμός διαγράμματος και διασφάλιση ότι τα δεδομένα του είναι ενημερωμένα.

#### Βήμα 1: Εισαγωγή Απαραίτητων Πακέτων
```java
import com.aspose.cells.*;
```

#### Βήμα 2: Φόρτωση Βιβλίου Εργασίας και Πρόσβαση σε Φύλλο Εργασίας
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### Επεξήγηση
- `new Workbook(filePath)` φορτώνει το αρχείο στη μνήμη.  
- `ch.calculate()` αναγκάζει το διάγραμμα να επανυπολογίσει τυχόν τύπους ώστε τα δεδομένα που διαβάζετε να είναι ενημερωμένα.

### Πώς να Ανακτήσετε και να Εκτυπώσετε τους Τύπους Τιμών X και Y ενός Σημείου Διαγράμματος
**Overview** – Εξαγωγή του τύπου δεδομένων των τιμών X και Y ενός συγκεκριμένου σημείου.

#### Βήμα 1: Ρύθμιση HashMap Μετατροπής Enum (επαναχρησιμοποίηση από πριν)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### Βήμα 2: Πρόσβαση σε Σημείο Διαγράμματος και Εκτύπωση Τύπων Τιμών
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### Επεξήγηση
- `pnt.getXValueType()` / `pnt.getYValueType()` επιστρέφουν ακέραιες σταθερές που υποδεικνύουν αν η τιμή είναι αριθμητική, συμβολοσειρά, ημερομηνία κ.λπ.  
- Ο χάρτης `cvTypes` μετατρέπει αυτούς τους ακέραιους σε αναγνώσιμο κείμενο.

## Πρακτικές Εφαρμογές
1. **Financial Reporting** – Αυτόματη δημιουργία διαγραμμάτων με επαληθευμένους τύπους δεδομένων για γραμμές ελέγχου.  
2. **Data Visualization Dashboards** – Ανάκτηση σημείων διαγράμματος σε προσαρμοσμένα UI components.  
3. **Automated Testing** – Επικύρωση ότι οι σειρές διαγράμματος περιέχουν τους αναμενόμενους τύπους δεδομένων.  
4. **Business Intelligence** – Παροχή μεταδεδομένων διαγράμματος σε επόμενες διαδικασίες ανάλυσης.  
5. **Custom Reporting Tools** – Δημιουργία προσαρμοσμένων μηχανών αναφοράς που απαιτούν ακριβή διαχείριση enum.

## Σκέψεις Απόδοσης
- **Load Only Needed Sheets** – Χρησιμοποιήστε `Workbook.getWorksheets().get(index)` αντί να φορτώνετε κάθε φύλλο όταν εργάζεστε με μεγάλα αρχεία.  
- **Dispose Objects Promptly** – Ορίστε τις αναφορές του βιβλίου εργασίας σε `null` μετά την επεξεργασία για να βοηθήσετε τη συλλογή απορριμμάτων.  
- **Batch Process Files** – Όταν διαχειρίζεστε πολλά βιβλία εργασίας, επεξεργαστείτε τα σε παρτίδες για να διατηρήσετε τη χρήση μνήμης προβλέψιμη.

## Κοινά Προβλήματα & Λύσεις
- **License Not Found** – Βεβαιωθείτε ότι η διαδρομή του αρχείου άδειας είναι σωστή και ότι το αρχείο περιλαμβάνεται στην έξοδο της κατασκευής.  
- **Chart Not Calculated** – Πάντα καλέστε `chart.calculate()` πριν διαβάσετε τις τιμές των σημείων.  
- **Incorrect Enum Mapping** – Επαληθεύστε ότι έχετε προσθέσει όλες τις σχετικές σταθερές `CellValueType` στο `HashMap`.

## Συχνές Ερωτήσεις

**Q: Μπορώ να χρησιμοποιήσω αυτόν τον κώδικα με Aspose.Cells 24.x;**  
A: Ναι, το API για την ανάκτηση έκδοσης, τη φόρτωση βιβλίου εργασίας και την πρόσβαση σε σημεία διαγράμματος παραμένει σταθερό στις πρόσφατες εκδόσεις.

**Q: Τι γίνεται αν το διάγραμμά μου περιέχει τιμές ημερομηνίας;**  
A: Προσθέστε `CellValueType.IS_DATE_TIME` στον χάρτη `cvTypes` και αντιστοιχίστε το σε `"IsDateTime"`.

**Q: Χρειάζομαι άδεια για δοκιμαστική χρήση;**  
A: Απαιτείται άδεια δοκιμής για πλήρη λειτουργικότητα· χωρίς αυτή θα βλέπετε υδατογραφήματα στα παραγόμενα αρχεία.

**Q: Πώς να διαχειριστώ πολλαπλά φύλλα εργασίας;**  
A: Επανάληψη μέσω `wb.getWorksheets()` και επεξεργασία κάθε αντικειμένου `Chart` που συναντάτε.

**Q: Υπάρχει τρόπος εξαγωγής των δεδομένων του διαγράμματος σε CSV;**  
A: Ναι—εξάγετε τις τιμές σειρών μέσω `chart.getNSeries().get(i).getValues()` και γράψτε τις χρησιμοποιώντας το τυπικό Java I/O.

---

**Τελευταία Ενημέρωση:** 2026-04-11  
**Δοκιμάστηκε Με:** Aspose.Cells 25.3 for Java  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}