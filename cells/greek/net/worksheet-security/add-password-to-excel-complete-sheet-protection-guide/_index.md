---
category: general
date: 2026-03-27
description: Προσθέστε κωδικό πρόσβασης στο Excel και ασφαλίστε τα δεδομένα σας με
  τις επιλογές προστασίας φύλλου, επιτρέποντας την επιλογή ξεκλείδωτων κελιών ενώ
  αποθηκεύετε εύκολα το προστατευμένο βιβλίο εργασίας.
draft: false
keywords:
- add password to excel
- excel sheet protection options
- allow select unlocked cells
- save protected workbook
- enable sheet protection
language: el
og_description: Προσθέστε κωδικό πρόσβασης στο Excel και προστατέψτε τα φύλλα σας
  με ενσωματωμένες επιλογές, επιτρέποντας την επιλογή ξεκλείδωτων κελιών και την αποθήκευση
  ενός προστατευμένου βιβλίου εργασίας σε λίγα λεπτά.
og_title: Προσθήκη κωδικού στο Excel – Ολοκληρωμένος οδηγός προστασίας φύλλων
tags:
- Aspose.Cells
- C#
- Excel security
title: Προσθήκη κωδικού στο Excel – Πλήρης οδηγός προστασίας φύλλου
url: /el/net/worksheet-security/add-password-to-excel-complete-sheet-protection-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη κωδικού πρόσβασης στο Excel – Οδηγός Πλήρους Προστασίας Φύλλου

Έχετε αναρωτηθεί ποτέ πώς να **προσθέσετε κωδικό πρόσβασης σε αρχεία Excel** χωρίς να τρελαίνεστε; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει να κλειδώσουν ευαίσθητα δεδομένα σε υπολογιστικά φύλλα. Το καλό νέο; Με λίγες γραμμές C# και Aspose.Cells μπορείτε να ενεργοποιήσετε την προστασία φύλλου, να επιλέξετε τις ακριβείς επιλογές προστασίας Excel που χρειάζεστε, και ακόμη να επιτρέψετε επιλεγμένα ξεκλείδωτα κελιά για πιο ομαλή εμπειρία χρήστη.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη δημιουργία ενός workbook, την εγγραφή εμπιστευτικών τιμών, την εφαρμογή κωδικού SHA‑256, τη ρύθμιση των επιλογών προστασίας, και τέλος το **αποθήκευση προστατευμένου workbook** στο δίσκο. Στο τέλος θα ξέρετε ακριβώς πώς να προσθέσετε κωδικό πρόσβασης στο Excel, γιατί κάθε επιλογή είναι σημαντική, και πώς να προσαρμόσετε τον κώδικα στα δικά σας έργα.

## Προαπαιτούμενα

- .NET 6 ή νεότερο (ο κώδικας λειτουργεί τόσο με .NET Core όσο και με .NET Framework)
- Aspose.Cells for .NET εγκατεστημένο μέσω NuGet (`dotnet add package Aspose.Cells`)
- Βασική κατανόηση της σύνταξης C# (δεν απαιτούνται προχωρημένα κόλπα)

Αν κάτι από τα παραπάνω σας είναι άγνωστο, κάντε παύση εδώ και εγκαταστήστε το πακέτο—αφού είστε έτοιμοι, μπορούμε να προχωρήσουμε.

## Βήμα 1 – Δημιουργία Νέου Workbook (Ενεργοποίηση Προστασίας Φύλλου)

Πριν μπορέσουμε να **προσθέσουμε κωδικό πρόσβασης στο Excel**, χρειαζόμαστε ένα αντικείμενο workbook για να δουλέψουμε. Αυτό το βήμα θέτει επίσης τη βάση για τις μετέπειτα ρυθμίσεις προστασίας.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Create a fresh workbook – think of it as a blank Excel file
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:* Η δημιουργία ενός `Workbook` σας δίνει ένα καθαρό φύλλο. Αν άνοιγετε ένα υπάρχον αρχείο, θα χρησιμοποιούσατε `new Workbook("path.xlsx")`. Η αναφορά `Worksheet` είναι όπου θα γράψουμε δεδομένα και αργότερα θα εφαρμόσουμε την προστασία.

## Βήμα 2 – Εγγραφή Ευαίσθητων Δεδομένων (Τι Θα Προστατεύσουμε)

Τώρα θα εισάγουμε κάτι που ο χρήστης σίγουρα δεν πρέπει να επεξεργαστεί—ίσως έναν κωδικό, ένα οικονομικό ποσό ή προσωπικό αναγνωριστικό.

```csharp
        // Write confidential text into cell A1
        worksheet.Cells["A1"].PutValue("Sensitive Information");
```

*Συμβουλή:* Αν χρειάζεται να κλειδώσετε μόνο μέρος του φύλλου, μπορείτε να σημειώσετε συγκεκριμένα κελιά ως ξεκλείδωτα αργότερα. Από προεπιλογή, όλα τα κελιά κλειδώνουν όταν ενεργοποιηθεί η προστασία, οπότε θα το αντιμετωπίσουμε στο επόμενο βήμα.

## Βήμα 3 – Ενεργοποίηση Προστασίας Φύλλου & Προσθήκη Κωδικού SHA‑256

Αυτή είναι η καρδιά του tutorial: τελικά **προσθέτουμε κωδικό πρόσβασης στο Excel** ενεργοποιώντας την προστασία και ορίζοντας ένα ισχυρό hash.

```csharp
        // Access the protection object for the worksheet
        WorksheetProtection protection = worksheet.Protection;

        // Turn on protection – this is the “enable sheet protection” flag
        protection.IsProtected = true;

        // Set a SHA‑256 hashed password (much stronger than plain text)
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);
```

*Γιατί χρησιμοποιούμε SHA‑256;* Οι κωδικοί σε απλό κείμενο μπορούν να σπάσουν με εργαλεία brute‑force, ενώ ένα hash SHA‑256 προσθέτει ένα κρυπτογραφικό στρώμα που διαχειρίζεται το Aspose.Cells για εσάς. Αν προτιμάτε το παλαιότερο hash συμβατό με Excel, αντικαταστήστε το `PasswordType.SHA256` με `PasswordType.Standard`.

## Βήμα 4 – Λεπτομερής Ρύθμιση Επιλογών Προστασίας Φύλλου Excel

Τώρα που το φύλλο είναι κλειδωμένο, αποφασίζουμε τις **επιλογές προστασίας φύλλου Excel** όπως το αν οι χρήστες μπορούν να επιλέγουν κλειδωμένα κελιά, να επεξεργάζονται αντικείμενα, ή, κρίσιμο για πολλές ροές εργασίας, **να επιτρέπεται η επιλογή ξεκλείδωτων κελιών**.

```csharp
        // Allow users to click on unlocked cells (useful for data entry)
        protection.AllowSelectUnlockedCells = true;

        // Disallow editing of embedded objects like charts or shapes
        protection.AllowEditObject = false;

        // You can also restrict formatting, inserting rows, etc.
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;
```

*Επεξήγηση:*  
- `AllowSelectUnlockedCells` επιτρέπει στους τελικούς χρήστες να περιηγηθούν στο φύλλο χωρίς να εμφανίζεται η προειδοποίηση “φύλλο προστατευμένο”. Αυτό είναι χρήσιμο όταν εκθέτετε μια περιοχή τύπου φόρμας.  
- `AllowEditObject = false` εμποδίζει αλλαγές σε γραφήματα, εικόνες ή άλλα ενσωματωμένα αντικείμενα, ενισχύοντας την ασφάλεια.  
- Υπάρχουν επιπλέον σημαίες για λεπτομερή έλεγχο—ενεργοποιήστε ό,τι απαιτεί το σενάριό σας.

## Βήμα 5 – Αποθήκευση του Προστατευμένου Workbook (Save Protected Workbook)

Η τελική ενέργεια είναι η αποθήκευση του αρχείου. Εδώ **αποθηκεύουμε το προστατευμένο workbook** στο δίσκο, και θα δείτε την προστασία κωδικού σε δράση όταν το ανοίξετε στο Excel.

```csharp
        // Persist the workbook with all protection settings applied
        workbook.Save("ProtectedSheet.xlsx");

        // Optional: let the console know we’re done
        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

Όταν κάνετε διπλό κλικ στο `ProtectedSheet.xlsx`, το Excel θα ζητήσει τον κωδικό που ορίσατε (`MyStrongPwd!`). Αν προσπαθήσετε να επεξεργαστείτε ένα κλειδωμένο κελί, θα εμποδιστεί· ωστόσο, μπορείτε ακόμη να επιλέξετε τα ξεκλείδωτα κελιά χάρη στην προηγούμενη επιλογή.

### Αναμενόμενο Αποτέλεσμα

- **Αρχείο:** `ProtectedSheet.xlsx` εμφανίζεται στο φάκελο εξόδου του έργου σας.  
- **Συμπεριφορά:** Το άνοιγμα του αρχείου ζητά τον κωδικό. Μετά την εισαγωγή του, το κελί A1 παραμένει μόνο για ανάγνωση, ενώ τυχόν ξεκλείδωτα κελιά (αν τα δημιουργήσατε) μπορούν να επεξεργαστούν.  
- **Επαλήθευση:** Δοκιμάστε να επεξεργαστείτε το A1—το Excel θα αρνηθεί. Κάντε κλικ σε ένα ξεκλείδωτο κελί (αν δημιουργήσατε κάποιο); θα πρέπει να είναι επιλέξιμο χωρίς σφάλμα.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Σενάριο | Τι να Αλλάξετε | Γιατί |
|----------|----------------|-----|
| **Διαφορετικός αλγόριθμος κωδικού** | Χρησιμοποιήστε `PasswordType.Standard` | Για συμβατότητα με παλαιότερες εκδόσεις Excel που δεν υποστηρίζουν SHA‑256. |
| **Προστασία υπάρχοντος workbook** | Φορτώστε μέσω `new Workbook("Existing.xlsx")` | Σας επιτρέπει να προσθέσετε προστασία σε αρχείο που ήδη έχετε. |
| **Κλείδωμα μόνο μιας περιοχής** | Ορίστε `worksheet.Cells["B2:C5"].Style.Locked = false;` πριν την προστασία | Ξεκλειδώνει μια συγκεκριμένη περιοχή ενώ το υπόλοιπο παραμένει κλειδωμένο. |
| **Επιτρέψτε στους χρήστες μορφοποίηση κελιών** | `protection.AllowFormatCells = true;` | Χρήσιμο για dashboards όπου οι χρήστες μπορούν να αλλάζουν χρώματα αλλά όχι δεδομένα. |
| **Αποθήκευση σε ροή (π.χ., web response)** | `workbook.Save(stream, SaveFormat.Xlsx);` | Ιδανικό για ASP.NET APIs που επιστρέφουν το αρχείο απευθείας στον περιηγητή. |

*Προσοχή:* μην ξεχάσετε να ορίσετε `IsProtected = true`—ο κωδικός μόνος του δεν κλειδώνει το φύλλο. Επίσης, δοκιμάζετε πάντα με πραγματικό πελάτη Excel, επειδή ορισμένες σημαίες προστασίας συμπεριφέρονται ελαφρώς διαφορετικά ανάλογα με την έκδοση του Office.

## Πλήρες Παράδειγμα Εργασίας (Copy‑Paste Ready)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή console. Δεν λείπει τίποτα.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write some sensitive information into a cell
        worksheet.Cells["A1"].PutValue("Sensitive Information");

        // Optional: Unlock a range for user input (e.g., B1:C5)
        worksheet.Cells["B1:C5"].Style.Locked = false;

        // Step 3: Enable sheet protection and set a SHA‑256 hashed password
        WorksheetProtection protection = worksheet.Protection;
        protection.IsProtected = true;                     // enable sheet protection
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);

        // Step 4: Restrict actions – allow selecting unlocked cells only
        protection.AllowSelectUnlockedCells = true;
        protection.AllowEditObject = false;               // disallow editing objects
        // Additional options you might need:
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;

        // Step 5: Save the protected workbook to a file
        workbook.Save("ProtectedSheet.xlsx");

        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο, και θα δείτε την προστασία σε δράση.

## Οπτική Αναφορά

![Add password to Excel sheet protection screenshot](https://example.com/images/add-password-to-excel.png "add password to excel")

*Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για SEO.*

## Ανακεφαλαίωση & Επόμενα Βήματα

Μόλις σας δείξαμε **πώς να προσθέσετε κωδικό πρόσβασης στο Excel** χρησιμοποιώντας το Aspose.Cells, καλύψαμε τις βασικές **επιλογές προστασίας φύλλου Excel**, παρουσιάσαμε τη σημαία **allow select unlocked cells**, και αποθηκεύσαμε ένα **προστατευμένο workbook** που σέβεται αυτές τις ρυθμίσεις. Συνοπτικά, η ροή είναι:

1. Δημιουργήστε ή φορτώστε ένα workbook.  
2. Γράψτε τα δεδομένα που θέλετε να προστατεύσετε.  
3. Ενεργοποιήστε την προστασία, ορίστε έναν ισχυρό κωδικό, και ρυθμίστε τις επιλογές.  
4. Αποθηκεύστε το workbook.

Τώρα που έχετε τα βασικά, σκεφτείτε τις παρακάτω ιδέες:

- **Προγραμματιστικές προτροπές κωδικού:** εμφανίστε τον κωδικό μέσω ασφαλούς UI αντί για σκληρή ενσωμάτωση.  
- **Ομαδική προστασία:** επαναλάβετε τη διαδικασία για πολλά φύλλα και εφαρμόστε τις ίδιες ρυθμίσεις.  
- **Ενσωμάτωση με ASP.NET Core:** επιστρέψτε το προστατευμένο αρχείο ως απόκριση λήψης.  

Πειραματιστείτε—ίσως κλειδώσετε ολόκληρη τη σειρά αναφορών ή μόνο ένα μεμονωμένο εμπιστευτικό φύλλο. Σε κάθε περίπτωση, έχετε τώρα το εργαλείο για να προστατεύσετε τα δεδομένα του Excel με τον σωστό τρόπο.

---

*Καλή προγραμματιστική! Αν αυτός ο οδηγός σας βοήθησε να προσθέσετε κωδικό πρόσβασης στο Excel, ενημερώστε μας στα σχόλια ή μοιραστείτε τις δικές σας προσαρμογές. Όσο περισσότερο μαθαίνουμε μαζί, τόσο πιο ασφαλή γίνονται τα υπολογιστικά μας φύλλα.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}