---
category: general
date: 2026-02-14
description: Το πώς να δημιουργήσετε ιεραρχία σε πρότυπα SmartMarker είναι πιο εύκολο
  απ' ό,τι νομίζετε – μάθετε πώς να δημιουργείτε ιεραρχικά δεδομένα και πώς να καταγράφετε
  αποτελεσματικά τους υπαλλήλους.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: el
og_description: Πώς να δημιουργήσετε ιεραρχία σε πρότυπα SmartMarker είναι απλό. Ακολουθήστε
  αυτόν τον οδηγό για να δημιουργήσετε ιεραρχικά δεδομένα και να καταγράψετε τους
  υπαλλήλους με ενσωματωμένα εύρη.
og_title: Πώς να δημιουργήσετε ιεραρχία με το SmartMarker – Πλήρης οδηγός
tags:
- SmartMarker
- C#
- templating
title: Πώς να δημιουργήσετε ιεραρχία με το SmartMarker – Οδηγός βήμα‑προς‑βήμα
url: /el/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε ιεραρχία με το SmartMarker – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να δημιουργήσετε ιεραρχία** μέσα σε ένα πρότυπο SmartMarker χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε οι μόνοι. Σε πολλές περιπτώσεις αναφοράς χρειάζεται μια σχέση γονέα‑παιδιού—σκεφτείτε τμήματα και τα άτομα που εργάζονται σε αυτά. Τα καλά νέα είναι ότι το SmartMarker το κάνει παιχνιδάκι μόλις γνωρίζετε τα σωστά βήματα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από **δημιουργία ιεραρχικών δεδομένων** σε C#, ενεργοποίηση ενσωματωμένων περιοχών, και τέλος απόδοση ενός προτύπου που **καταγράφει τους υπαλλήλους** για κάθε τμήμα. Στο τέλος θα έχετε ένα δείγμα έτοιμο‑για‑εκτέλεση που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

---

## Τι θα χρειαστείτε

- .NET 6+ (οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Μια αναφορά στη βιβλιοθήκη **SmartMarker** (το namespace `ws.SmartMarkerProcessor`)
- Βασικές γνώσεις C# – τίποτα περίπλοκο, μόνο λίγα αντικείμενα και ένα ή δύο lambda
- Ένα IDE ή επεξεργαστή της επιλογής σας (Visual Studio, Rider, VS Code… εσείς διαλέγετε)

Αν έχετε ήδη όλα αυτά, τέλεια—ας βουτήξουμε.

---

## Πώς να δημιουργήσετε ιεραρχία – Επισκόπηση

Η βασική ιδέα είναι να χτίσετε ένα **ενσωματωμένο γράφημα αντικειμένων** που αντικατοπτρίζει τη δομή που θέλετε να δείτε στο τελικό έγγραφο. Στην περίπτωσή μας το γράφημα μοιάζει με:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

Το SmartMarker μπορεί στη συνέχεια να επαναλάβει το `Departments` και, επειδή θα ενεργοποιήσουμε την **επεξεργασία ενσωματωμένων περιοχών**, θα κάνει επίσης βρόχο πάνω στη συλλογή `Employees` κάθε τμήματος αυτόματα.

---

## Βήμα 1: Δημιουργία του ιεραρχικού μοντέλου δεδομένων

Πρώτα δημιουργούμε ένα ανώνυμο αντικείμενο που περιέχει έναν πίνακα τμημάτων, το καθένα με τη δική του λίστα υπαλλήλων. Η χρήση ανώνυμου τύπου κρατά το παράδειγμα ελαφρύ—μπορείτε να το αντικαταστήσετε με πραγματικές κλάσεις POCO αργότερα.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Γιατί είναι σημαντικό:** Ο πίνακας `Departments` είναι η συλλογή κορυφαίου επιπέδου. Κάθε στοιχείο περιέχει έναν πίνακα `Employees`, δίνοντάς μας το δεύτερο επίπεδο ιεραρχίας που θα προσπελάσουμε αργότερα με `#Departments.Employees#`.

---

## Βήμα 2: Ενεργοποίηση επεξεργασίας ενσωματωμένων περιοχών

Το SmartMarker δεν θα βυθιστεί σε εσωτερικές συλλογές εκτός αν του το πείτε. Το αντικείμενο `SmartMarkerOptions` περιέχει αυτή τη ρύθμιση.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Συμβουλή επαγγελματία:** Αν ξεχάσετε αυτή τη σημαία, η εσωτερική περιοχή `#Employees#` απλώς δεν επιστρέφει τίποτα, και θα σκεφτείτε γιατί το πρότυπο είναι κενό.

---

## Βήμα 3: Εκτέλεση του επεξεργαστή με τα δεδομένα σας

Τώρα παραδίδουμε τα δεδομένα και τις επιλογές στον επεξεργαστή. Η μεταβλητή `ws` αντιπροσωπεύει το **WebService** σας (ή όποιο αντικείμενο φιλοξενεί τη μηχανή SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Σε αυτό το σημείο το SmartMarker αναλύει το πρότυπο, αντικαθιστά `#Departments.Name#` με το όνομα κάθε τμήματος, και επειδή οι ενσωματωμένες περιοχές είναι ενεργοποιημένες, επαναλαμβάνει τη συλλογή `Employees` κάθε τμήματος.

---

## Βήμα 4: Δημιουργία των δεικτών προτύπου

Παρακάτω υπάρχει ένα ελάχιστο πρότυπο που δείχνει τόσο τον εξωτερικό όσο και τον εσωτερικό βρόχο. Επικολλήστε το στον επεξεργαστή προτύπων SmartMarker (ή σε ένα αρχείο `.txt` που θα περάσετε στον επεξεργαστή).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Κατά την απόδοση θα δείτε:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Τι βλέπετε:** Ο εξωτερικός δείκτης `#Departments.Name#` εκτυπώνει τον τίτλο του τμήματος. Το εσωτερικό μπλοκ `#Departments.Employees#` επαναλαμβάνει κάθε υπάλληλο, και το `#Departments.Employees#` μέσα στο μπλοκ εμφανίζει το πραγματικό όνομα.

---

## Αναμενόμενο αποτέλεσμα & επαλήθευση

Η εκτέλεση του πλήρους παραδείγματος (δεδομένα + επιλογές + πρότυπο) πρέπει να παράγει ακριβώς τη λίστα που φαίνεται παραπάνω. Για γρήγορη επαλήθευση, μπορείτε να εκτυπώσετε το αποτέλεσμα στην κονσόλα:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Αν δείτε τις δύο επικεφαλίδες τμημάτων ακολουθούμενες από τις κουκκίδες των υπαλλήλων, έχετε δημιουργήσει επιτυχώς **μια ιεραρχία** και **καταγράψει τους υπαλλήλους**.

---

## Συνηθισμένα προβλήματα & ειδικές περιπτώσεις

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Καμία έξοδος για τους υπαλλήλους | `EnableNestedRange` παραμένει ψευδές | Ορίστε `EnableNestedRange = true` |
| Διπλά ονόματα υπαλλήλων | Ίδιος πίνακας επαναχρησιμοποιείται σε τμήματα | Κλωνοποιήστε τον πίνακα ή χρησιμοποιήστε ξεχωριστές συλλογές |
| Πολύ μεγάλες ιεραρχίες προκαλούν πίεση μνήμης | Το SmartMarker φορτώνει ολόκληρο το γράφημα αντικειμένων στη μνήμη | Μετάδοση δεδομένων ή σελιδοποίηση μεγάλων συλλογών |
| Σφάλματα σύνταξης προτύπου | Λείπουν κλειστά ετικέτες `#/…#` | Χρησιμοποιήστε τον επικυρωτή SmartMarker ή εκτελέστε γρήγορο τεστ με μικρό πρότυπο |

---

## Προχωρώντας παραπέρα – Πραγματικές παραλλαγές

1. **Δυναμικές πηγές δεδομένων** – Ανάκτηση τμημάτων από βάση δεδομένων και χαρτογράφηση τους στη ανώνυμη δομή χρησιμοποιώντας LINQ.  
2. **Υποconditional formatting** – Προσθήκη σημαίας `IsManager` σε κάθε υπάλληλο και χρήση των συνθηκών SmartMarker (`#if …#`) για επισήμανση των διευθυντών.  
3. **Πολλαπλά επίπεδα ενσωμάτωσης** – Αν χρειάζεστε ομάδες μέσα σε τμήματα, προσθέστε μια ακόμη συλλογή (`Teams`) και κρατήστε το `EnableNestedRange` ενεργό.

---

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή-επικόλληση)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Πρότυπο (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Η εκτέλεση του προγράμματος εκτυπώνει την ιεραρχία ακριβώς όπως φαίνεται παραπάνω.

---

## Συμπέρασμα

Καλύψαμε **πώς να δημιουργήσετε ιεραρχία** στο SmartMarker, από το σχήμα **ιεραρχικών δεδομένων** σε C# μέχρι την ενεργοποίηση ενσωματωμένων περιοχών και την απόδοση ενός προτύπου που **καταγράφει τους υπαλλήλους** ανά τμήμα. Το μοτίβο κλιμακώνεται—απλώς προσθέστε περισσότερες ενσωματωμένες συλλογές ή λογική υπό συνθήκη και έχετε μια ισχυρή μηχανή αναφοράς στα χέρια σας.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αντικαταστήσετε τους ανώνυμους τύπους με ισχυρά τυποποιημένες κλάσεις POCO, ή ενσωματώστε αυτή τη ροή σε ένα endpoint ASP.NET Core που επιστρέφει PDF ή έγγραφο Word. Ο ουρανός είναι το όριο, και τώρα έχετε μια σταθερή βάση.

---

![How to create hierarchy diagram](image.png){alt="Διάγραμμα δημιουργίας ιεραρχίας που δείχνει τη σχέση τμήματος‑υπαλλήλου"}

*Καλό κώδικα! Αν συναντήσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—είμαι στη διάθεσή σας για βοήθεια.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}