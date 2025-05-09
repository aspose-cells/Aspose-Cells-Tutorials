---
"description": "Μάθετε να χρησιμοποιείτε το ICellsDataTableDataSource με το Aspose.Cells για .NET για τη δυναμική συμπλήρωση φύλλων Excel. Ιδανικό για την αυτοματοποίηση δεδομένων πελατών σε βιβλία εργασίας."
"linktitle": "Χρήση του ICellsDataTableDataSource για το Workbook Designer"
"second_title": "API επεξεργασίας Excel Aspose.Cells .NET"
"title": "Χρήση του ICellsDataTableDataSource για το Workbook Designer"
"url": "/el/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Χρήση του ICellsDataTableDataSource για το Workbook Designer

## Εισαγωγή
Η δημιουργία προηγμένων υπολογιστικών φύλλων με αυτοματοποιημένη ενσωμάτωση δεδομένων μπορεί να αλλάξει τα δεδομένα, ειδικά σε επιχειρηματικές εφαρμογές. Σε αυτό το σεμινάριο, θα εμβαθύνουμε στον τρόπο χρήσης `ICellsDataTableDataSource` για έναν σχεδιαστή βιβλίων εργασίας στο Aspose.Cells για .NET. Θα σας καθοδηγήσουμε στη δημιουργία μιας απλής, αναγνώσιμης από τον άνθρωπο λύσης για τη δυναμική φόρτωση προσαρμοσμένων δεδομένων σε ένα αρχείο Excel. Επομένως, εάν εργάζεστε με λίστες πελατών, δεδομένα πωλήσεων ή οτιδήποτε παρόμοιο, αυτός ο οδηγός είναι για εσάς!
## Προαπαιτούμενα
Για να ξεκινήσετε, βεβαιωθείτε ότι έχετε τα εξής:
- Aspose.Cells για τη βιβλιοθήκη .NET – Μπορείτε να το κατεβάσετε από [εδώ](https://releases.aspose.com/cells/net/) ή αποκτήστε μια δωρεάν δοκιμαστική έκδοση.
- Περιβάλλον ανάπτυξης .NET – Το Visual Studio είναι μια εξαιρετική επιλογή.
- Βασική Κατανόηση της C# – Η εξοικείωση με τις κλάσεις και την επεξεργασία δεδομένων θα σας βοηθήσει να παρακολουθήσετε.
Πριν προχωρήσουμε, βεβαιωθείτε ότι το περιβάλλον ανάπτυξής σας έχει ρυθμιστεί με τα απαραίτητα πακέτα.
## Εισαγωγή πακέτων
Για να χρησιμοποιήσετε αποτελεσματικά το Aspose.Cells, πρέπει να εισαγάγετε απαραίτητα πακέτα. Παρακάτω είναι μια γρήγορη αναφορά για τους απαιτούμενους χώρους ονομάτων:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Βήμα 1: Ορισμός μιας Κλάσης Δεδομένων Πελάτη
Για να ξεκινήσετε, δημιουργήστε ένα απλό `Customer` τάξη. Αυτή η τάξη θα περιέχει βασικές πληροφορίες πελατών όπως `FullName` και `Address`Σκεφτείτε το ως έναν τρόπο για να ορίσετε το "σχήμα" των δεδομένων σας.
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
## Βήμα 2: Ρύθμιση της Κλάσης Λίστας Πελατών
Στη συνέχεια, ορίστε ένα `CustomerList` τάξη που επεκτείνεται `ArrayList`Αυτή η προσαρμοσμένη λίστα θα περιέχει παρουσίες του `Customer` και να επιτρέπεται η πρόσβαση με ευρετήριο σε κάθε καταχώρηση.
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
Σε αυτό το βήμα, τυλίγουμε τα δεδομένα μας σε μια μορφή που το Aspose.Cells μπορεί να αναγνωρίσει και να επεξεργαστεί.
## Βήμα 3: Δημιουργήστε την κλάση προέλευσης δεδομένων πελάτη
Εδώ είναι που τα πράγματα γίνονται ενδιαφέροντα. Θα δημιουργήσουμε ένα `CustomerDataSource` υλοποίηση κλάσης `ICellsDataTable` για να κάνουμε τα δεδομένα μας συμβατά με τον σχεδιαστή βιβλίων εργασίας του Aspose.Cells.
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
Αυτό το έθιμο `CustomerDataSource` Η κλάση επιτρέπει στο Aspose.Cells να ερμηνεύει κάθε `Customer` αντικείμενο ως γραμμή στο αρχείο Excel.
## Βήμα 4: Αρχικοποίηση των Δεδομένων Πελάτη
Τώρα, ας προσθέσουμε μερικούς πελάτες στη λίστα μας. Εδώ φορτώνουμε τα δεδομένα που θα εγγραφούν στο βιβλίο εργασίας. Μπορείτε να προσθέσετε περισσότερες καταχωρήσεις, όπως απαιτείται.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Σε αυτό το παράδειγμα, εργαζόμαστε με ένα μικρό σύνολο δεδομένων. Ωστόσο, θα μπορούσατε εύκολα να επεκτείνετε αυτήν τη λίστα φορτώνοντας δεδομένα από μια βάση δεδομένων ή άλλες πηγές.
## Βήμα 5: Φόρτωση του βιβλίου εργασίας
Τώρα, ας ανοίξουμε ένα υπάρχον βιβλίο εργασίας του Excel που περιέχει τους απαραίτητους Έξυπνους Δείκτες. Αυτό το βιβλίο εργασίας θα χρησιμεύσει ως πρότυπό μας και το Aspose.Cells θα αντικαταστήσει δυναμικά τους Έξυπνους Δείκτες με τα δεδομένα πελατών.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Βεβαιωθείτε ότι `"SmartMarker1.xlsx"` περιέχει placeholders όπως `&=Customer.FullName` και `&=Customer.Address` όπου πρέπει να συμπληρωθούν τα δεδομένα.
## Βήμα 6: Ρύθμιση του Σχεδιαστή Βιβλίου Εργασίας
Τώρα, ας ρυθμίσουμε τις παραμέτρους του σχεδιαστή βιβλίου εργασίας για να συνδέσουμε την προέλευση δεδομένων πελατών μας με τους Έξυπνους Δείκτες του βιβλίου εργασίας.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
Ο `SetDataSource` η μέθοδος μας δεσμεύει `CustomerDataSource` στους Έξυπνους Δείκτες στο βιβλίο εργασίας. Κάθε δείκτης με ετικέτα `&=Customer` στο Excel θα αντικατασταθούν πλέον από τα αντίστοιχα δεδομένα πελατών.
## Βήμα 7: Επεξεργασία και αποθήκευση του βιβλίου εργασίας
Τέλος, ας επεξεργαστούμε το βιβλίο εργασίας για να συμπληρώσουμε τα δεδομένα και να αποθηκεύσουμε τα αποτελέσματα.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Αυτός ο κώδικας ενεργοποιεί την επεξεργασία του Έξυπνου Δείκτη, αντικαθιστά όλα τα placeholders με δεδομένα και αποθηκεύει το αποτέλεσμα ως `dest.xlsx`.
## Σύναψη
Συγχαρητήρια! Η εφαρμογή έγινε με επιτυχία `ICellsDataTableDataSource` για έναν σχεδιαστή βιβλίων εργασίας που χρησιμοποιεί Aspose.Cells για .NET. Αυτή η προσέγγιση είναι ιδανική για την αυτοματοποίηση της συμπλήρωσης δεδομένων σε υπολογιστικά φύλλα, ειδικά όταν πρόκειται για δυναμικά δεδομένα όπως λίστες πελατών ή αποθέματα προϊόντων. Με αυτές τις δεξιότητες, είστε σε καλό δρόμο για τη δημιουργία εφαρμογών που βασίζονται σε δεδομένα και κάνουν την αναφορά που βασίζεται στο Excel παιχνιδάκι!
## Συχνές ερωτήσεις
### Τι είναι `ICellsDataTable` στο Aspose.Cells;  
Είναι μια διεπαφή που επιτρέπει τη σύνδεση προσαρμοσμένων πηγών δεδομένων με τους έξυπνους δείκτες Aspose.Cells για δυναμική συμπλήρωση δεδομένων.
### Πώς μπορώ να προσαρμόσω δεδομένα στο πρότυπο βιβλίου εργασίας;  
Σημειωτές θέσης που ονομάζονται Έξυπνοι Δείκτες, όπως π.χ. `&=Customer.FullName`, χρησιμοποιούνται. Αυτοί οι δείκτες αντικαθίστανται με πραγματικά δεδομένα κατά την επεξεργασία.
### Είναι το Aspose.Cells για .NET δωρεάν;  
Το Aspose.Cells προσφέρει δωρεάν δοκιμαστική περίοδο, αλλά η πλήρης πρόσβαση απαιτεί άδεια χρήσης επί πληρωμή. Ελέγξτε τα [δωρεάν δοκιμή](https://releases.aspose.com/) ή [αγορά](https://purchase.aspose.com/buy) επιλογές.
### Μπορώ να προσθέσω περισσότερα δεδομένα πελατών δυναμικά;  
Απολύτως! Απλώς συμπληρώστε το `CustomerList` με πρόσθετες καταχωρήσεις πριν από την εκτέλεση του προγράμματος.
### Πού μπορώ να βρω βοήθεια αν έχω κολλήσει;  
Η Άσπο έχει ένα [φόρουμ υποστήριξης](https://forum.aspose.com/c/cells/9) όπου οι χρήστες μπορούν να κάνουν ερωτήσεις και να λάβουν βοήθεια από την κοινότητα και την ομάδα Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}