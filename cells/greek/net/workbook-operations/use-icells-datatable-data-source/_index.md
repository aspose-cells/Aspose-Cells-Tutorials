---
title: Χρησιμοποιήστε το ICEllsDataTableDataSource για το Workbook Designer
linktitle: Χρησιμοποιήστε το ICEllsDataTableDataSource για το Workbook Designer
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε να χρησιμοποιείτε το ICEllsDataTableDataSource με το Aspose.Cells για .NET για τη δυναμική συμπλήρωση φύλλων του Excel. Ιδανικό για την αυτοματοποίηση των δεδομένων πελατών σε βιβλία εργασίας.
weight: 21
url: /el/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Χρησιμοποιήστε το ICEllsDataTableDataSource για το Workbook Designer

## Εισαγωγή
 Η δημιουργία προηγμένων υπολογιστικών φύλλων με αυτοματοποιημένη ενοποίηση δεδομένων μπορεί να αλλάξει το παιχνίδι, ειδικά σε επαγγελματικές εφαρμογές. Σε αυτό το σεμινάριο, θα εξετάσουμε τον τρόπο χρήσης`ICellsDataTableDataSource`για σχεδιαστή βιβλίου εργασίας στο Aspose.Cells για .NET. Θα σας καθοδηγήσουμε στη δημιουργία μιας απλής, αναγνώσιμης από τον άνθρωπο λύσης για τη δυναμική φόρτωση προσαρμοσμένων δεδομένων σε ένα αρχείο Excel. Επομένως, εάν εργάζεστε με λίστες πελατών, δεδομένα πωλήσεων ή κάτι παρόμοιο, αυτός ο οδηγός είναι για εσάς!
## Προαπαιτούμενα
Για να ξεκινήσετε, βεβαιωθείτε ότι έχετε τα εξής:
-  Aspose.Cells for .NET Library – Μπορείτε να το κατεβάσετε από[εδώ](https://releases.aspose.com/cells/net/) ή αποκτήστε μια δωρεάν δοκιμαστική έκδοση.
- .NET Development Environment – Το Visual Studio είναι μια εξαιρετική επιλογή.
- Βασική κατανόηση της C# – Η εξοικείωση με τις κλάσεις και τον χειρισμό δεδομένων θα σας βοηθήσει να ακολουθήσετε.
Πριν προχωρήσουμε, βεβαιωθείτε ότι το περιβάλλον ανάπτυξής σας έχει ρυθμιστεί με τα απαραίτητα πακέτα.
## Εισαγωγή πακέτων
Για να χρησιμοποιήσετε αποτελεσματικά το Aspose.Cells, πρέπει να εισάγετε βασικά πακέτα. Ακολουθεί μια γρήγορη αναφορά για τους απαιτούμενους χώρους ονομάτων:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Βήμα 1: Καθορίστε μια κατηγορία δεδομένων πελατών
 Για να ξεκινήσετε, δημιουργήστε ένα απλό`Customer` τάξη. Αυτή η τάξη θα περιέχει βασικά στοιχεία πελατών όπως`FullName` και`Address`Σκεφτείτε το ως έναν τρόπο να ορίσετε το "σχήμα" των δεδομένων σας.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Βήμα 2: Ρύθμιση της κλάσης λίστας πελατών
 Στη συνέχεια, ορίστε α`CustomerList` τάξη που εκτείνεται`ArrayList` . Αυτή η προσαρμοσμένη λίστα θα περιέχει παρουσίες του`Customer` και να επιτρέπεται η ευρετηριασμένη πρόσβαση σε κάθε καταχώρηση.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
Σε αυτό το βήμα, αναδιπλώνουμε τα δεδομένα μας σε μια μορφή που το Aspose.Cells μπορεί να αναγνωρίσει και να επεξεργαστεί.
## Βήμα 3: Δημιουργήστε την κλάση προέλευσης δεδομένων πελάτη
 Εδώ είναι που τα πράγματα γίνονται ενδιαφέροντα. Θα δημιουργήσουμε ένα`CustomerDataSource` εφαρμογή της τάξης`ICellsDataTable` για να κάνουμε τα δεδομένα μας συμβατά με τον σχεδιαστή βιβλίου εργασίας Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 Αυτό το έθιμο`CustomerDataSource` Η κλάση δίνει τη δυνατότητα στα Aspose.Cells να ερμηνεύουν το καθένα`Customer` αντικείμενο ως γραμμή στο αρχείο Excel.
## Βήμα 4: Αρχικοποιήστε τα Δεδομένα Πελάτη
Τώρα, ας προσθέσουμε μερικούς πελάτες στη λίστα μας. Εδώ φορτώνουμε τα δεδομένα που θα εγγραφούν στο βιβλίο εργασίας. Μη διστάσετε να προσθέσετε περισσότερες συμμετοχές όπως απαιτείται.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Σε αυτό το παράδειγμα, εργαζόμαστε με ένα μικρό σύνολο δεδομένων. Ωστόσο, θα μπορούσατε εύκολα να επεκτείνετε αυτήν τη λίστα φορτώνοντας δεδομένα από μια βάση δεδομένων ή άλλες πηγές.
## Βήμα 5: Φορτώστε το βιβλίο εργασίας
Τώρα, ας ανοίξουμε ένα υπάρχον βιβλίο εργασίας του Excel που περιέχει τους απαραίτητους έξυπνους δείκτες. Αυτό το βιβλίο εργασίας θα χρησιμεύσει ως πρότυπό μας και το Aspose.Cells θα αντικαταστήσει δυναμικά τους Έξυπνους δείκτες με τα δεδομένα πελατών.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Βεβαιωθείτε ότι`"SmartMarker1.xlsx"` περιέχει σύμβολα κράτησης θέσης όπως`&=Customer.FullName` και`&=Customer.Address` όπου πρέπει να συμπληρωθούν τα δεδομένα.
## Βήμα 6: Ρύθμιση του Workbook Designer
Τώρα, ας διαμορφώσουμε τον σχεδιαστή βιβλίου εργασίας ώστε να συνδέει την πηγή δεδομένων πελατών μας με τους Έξυπνους δείκτες του βιβλίου εργασίας.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 Ο`SetDataSource` μέθοδος μας δεσμεύει`CustomerDataSource` στους Έξυπνους δείκτες στο βιβλίο εργασίας. Κάθε δείκτης με ετικέτα`&=Customer` στο Excel θα αντικατασταθεί πλέον από τα αντίστοιχα δεδομένα πελάτη.
## Βήμα 7: Επεξεργαστείτε και αποθηκεύστε το βιβλίο εργασίας
Τέλος, ας επεξεργαστούμε το βιβλίο εργασίας για να συμπληρώσουμε τα δεδομένα και να αποθηκεύσουμε τα αποτελέσματα.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Αυτός ο κωδικός ενεργοποιεί την επεξεργασία Smart Marker, αντικαθιστά όλα τα σύμβολα κράτησης θέσης με δεδομένα και αποθηκεύει το αποτέλεσμα ως`dest.xlsx`.
## Σύναψη
 Συγχαρητήρια! Το εφαρμόσατε με επιτυχία`ICellsDataTableDataSource` για έναν σχεδιαστή βιβλίου εργασίας που χρησιμοποιεί το Aspose.Cells για .NET. Αυτή η προσέγγιση είναι ιδανική για την αυτοματοποίηση του πληθυσμού δεδομένων σε υπολογιστικά φύλλα, ειδικά όταν πρόκειται για δυναμικά δεδομένα όπως λίστες πελατών ή αποθέματα προϊόντων. Με αυτές τις δεξιότητες, είστε σε καλό δρόμο για τη δημιουργία εφαρμογών που βασίζονται σε δεδομένα που κάνουν τις αναφορές που βασίζονται στο Excel παιχνιδάκι!
## Συχνές ερωτήσεις
###  Τι είναι`ICellsDataTable` in Aspose.Cells?  
Είναι μια διεπαφή που επιτρέπει τη σύνδεση προσαρμοσμένων πηγών δεδομένων με τους έξυπνους δείκτες Aspose.Cells για δυναμικό πληθυσμό δεδομένων.
### Πώς μπορώ να προσαρμόσω τα δεδομένα στο πρότυπο βιβλίου εργασίας;  
 Placeholders που ονομάζονται Smart Markers, όπως π.χ`&=Customer.FullName`, χρησιμοποιούνται. Αυτοί οι δείκτες αντικαθίστανται με πραγματικά δεδομένα κατά την επεξεργασία.
### Είναι δωρεάν το Aspose.Cells για .NET;  
 Το Aspose.Cells προσφέρει δωρεάν δοκιμή, αλλά η πλήρης πρόσβαση απαιτεί άδεια επί πληρωμή. Ελέγξτε τους[δωρεάν δοκιμή](https://releases.aspose.com/) ή[αγορά](https://purchase.aspose.com/buy) επιλογές.
### Μπορώ να προσθέσω περισσότερα δεδομένα πελατών δυναμικά;  
 Απολύτως! Απλώς συμπληρώστε το`CustomerList`με επιπλέον καταχωρήσεις πριν την εκτέλεση του προγράμματος.
### Πού μπορώ να βρω βοήθεια εάν έχω κολλήσει;  
 Ο Aspose έχει α[φόρουμ υποστήριξης](https://forum.aspose.com/c/cells/9) όπου οι χρήστες μπορούν να κάνουν ερωτήσεις και να λάβουν βοήθεια από την κοινότητα και την ομάδα Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
