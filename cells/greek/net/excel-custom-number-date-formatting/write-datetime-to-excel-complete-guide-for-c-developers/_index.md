---
category: general
date: 2026-04-07
description: Γράψτε ημερομηνία/ώρα στο Excel με C#. Μάθετε πώς να εισάγετε ημερομηνία
  σε φύλλο εργασίας, να διαχειριστείτε την τιμή ημερομηνίας σε κελί του Excel και
  να μετατρέψετε ημερομηνία του ιαπωνικού ημερολογίου σε λίγα μόνο βήματα.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: el
og_description: Γράψτε ημερομηνία/ώρα στο Excel γρήγορα. Αυτός ο οδηγός δείχνει πώς
  να εισάγετε ημερομηνία σε φύλλο εργασίας, να διαχειριστείτε την τιμή ημερομηνίας
  ενός κελιού στο Excel και να μετατρέψετε ημερομηνία του ιαπωνικού ημερολογίου με
  C#.
og_title: Γράψτε ημερομηνία/ώρα στο Excel – Βήμα‑βήμα C# Οδηγός
tags:
- C#
- Excel automation
- Aspose.Cells
title: Γράψτε ημερομηνία/ώρα στο Excel – Πλήρης οδηγός για προγραμματιστές C#
url: /el/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εγγραφή datetime σε Excel – Πλήρης Οδηγός για Προγραμματιστές C#

Έχετε ποτέ χρειαστεί να **γράψετε datetime σε Excel** αλλά δεν ήσασταν σίγουροι ποια κλήση API αποθηκεύει πραγματικά μια σωστή ημερομηνία Excel; Δεν είστε ο μόνος. Σε πολλά εταιρικά εργαλεία πρέπει να τοποθετήσουμε ένα C# `DateTime` σε ένα φύλλο εργασίας, και το αποτέλεσμα πρέπει να συμπεριφέρεται ως μια πραγματική ημερομηνία Excel—να μπορεί να ταξινομηθεί, να φιλτραριστεί και να είναι έτοιμη για πίνακες Pivot.  

Σε αυτό το tutorial θα περάσουμε βήμα προς βήμα τις ακριβείς ενέργειες για να *εισάγετε ημερομηνία σε φύλλο εργασίας* χρησιμοποιώντας το Aspose.Cells, θα εξηγήσουμε γιατί η ρύθμιση του πολιτισμού είναι σημαντική, και ακόμη θα δείξουμε πώς να **μετατρέψετε ημερομηνία ιαπωνικού ημερολογίου** σε ένα κανονικό `DateTime` πριν τη γράψετε. Στο τέλος θα έχετε ένα αυτόνομο κομμάτι κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστεί

- **.NET 6+** (ή οποιαδήποτε πρόσφατη έκδοση .NET· ο κώδικας λειτουργεί και σε .NET Framework)  
- **Aspose.Cells for .NET** – ένα πακέτο NuGet που σας επιτρέπει να χειρίζεστε αρχεία Excel χωρίς εγκατεστημένο Office.  
- Βασική κατανόηση του C# `DateTime` και των πολιτισμών.  

Δεν απαιτούνται πρόσθετες βιβλιοθήκες, δεν χρειάζεται COM interop και δεν απαιτείται εγκατάσταση του Excel. Αν έχετε ήδη μια παρουσία φύλλου εργασίας (`ws`), είστε έτοιμοι.

## Βήμα 1: Ρύθμιση του Ιαπωνικού Πολιτισμού (Μετατροπή Ημερομηνίας Ιαπωνικού Ημερολογίου)

Όταν λαμβάνετε μια ημερομηνία όπως `"R02/05/01"` (Reiwa 2, 1 Μαΐου) πρέπει να πείτε στο .NET πώς να ερμηνεύσει τα σύμβολα της εποχής. Το ιαπωνικό ημερολόγιο δεν είναι το προεπιλεγμένο Γρηγοριανό, γι' αυτό δημιουργούμε ένα `CultureInfo` που αντικαθιστά το ημερολόγιό του με `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Γιατί είναι σημαντικό:**  
Αν αναλύσετε τη συμβολοσειρά με τον προεπιλεγμένο πολιτισμό, το .NET θα πετάξει μια εξαίρεση μορφής επειδή δεν μπορεί να αντιστοιχίσει το `R` (την εποχή Reiwa) σε ένα έτος. Αντικαθιστώντας με `JapaneseCalendar`, ο αναλυτής καταλαβαίνει τα σύμβολα της εποχής και τα μετατρέπει στο σωστό Γρηγοριανό έτος.

## Βήμα 2: Ανάλυση της Συμβολοσειράς Βασισμένης στην Εποχή σε `DateTime`

Τώρα που ο πολιτισμός είναι έτοιμος, μπορούμε με ασφάλεια να καλέσουμε το `DateTime.ParseExact`. Η συμβολοσειρά μορφής `"ggyy/MM/dd"` λέει στον αναλυτή:

- `gg` – προσδιοριστής εποχής (π.χ., `R` για Reiwa)  
- `yy` – διψήφιο έτος μέσα στην εποχή  
- `MM/dd` – μήνας και ημέρα.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Συμβουλή:** Αν μπορεί να λάβετε ημερομηνίες σε άλλες μορφές (π.χ., `"Heisei 30/12/31"`), τυλίξτε την ανάλυση σε `try/catch` και επιστρέψτε σε `DateTime.TryParseExact`. Αυτό αποτρέπει το κατάρρευση ολόκληρης της εργασίας εισαγωγής λόγω μιας μόνο λανθασμένης γραμμής.

## Βήμα 3: Εγγραφή του `DateTime` σε Κελί Excel (Τιμή Ημερομηνίας Κελιού Excel)

Το Aspose.Cells αντιμετωπίζει ένα .NET `DateTime` ως εγγενή ημερομηνία Excel όταν χρησιμοποιείτε το `PutValue`. Η βιβλιοθήκη αυτόματα μετατρέπει τα ticks σε σειριακό αριθμό του Excel (ο αριθμός ημερών από την 1900‑01‑00). Αυτό σημαίνει ότι το κελί θα εμφανίσει μια σωστή **τιμή ημερομηνίας κελιού Excel** και μπορείτε να το μορφοποιήσετε αργότερα χρησιμοποιώντας τα ενσωματωμένα στυλ ημερομηνίας του Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Τι θα δείτε στο Excel:**  
Το κελί C1 περιέχει τώρα τον σειριακό αριθμό `44796`, ο οποίος εμφανίζεται από το Excel ως `2020‑05‑01` (ή όποια μορφή έχετε εφαρμόσει). Η υποκείμενη τιμή είναι πραγματική ημερομηνία, όχι συμβολοσειρά, έτσι η ταξινόμηση λειτουργεί όπως αναμένεται.

## Βήμα 4: Αποθήκευση του Workbook (Συμπέρασμα)

Αν δεν έχετε ήδη αποθηκεύσει το workbook, κάντε το τώρα. Αυτό το βήμα δεν αφορά άμεσα την εγγραφή της ημερομηνίας, αλλά ολοκληρώνει τη ροή εργασίας.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Αυτό ήταν—τέσσερα σύντομα βήματα, και έχετε επιτυχώς **γράψει datetime σε Excel**, διαχειριζόμενοι μια ημερομηνία ιαπωνικής εποχής κατά τη διαδικασία.

---

![παράδειγμα εγγραφής datetime σε excel](/images/write-datetime-to-excel.png "Στιγμιότυπο που δείχνει ένα έργο C# να γράφει ένα DateTime σε κελί Excel C1")

*Η παραπάνω εικόνα απεικονίζει το τελικό αρχείο Excel με την ημερομηνία να εμφανίζεται σωστά στο κελί C1.*

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η μεταβλητή worksheet δεν είναι ακόμη έτοιμη;

Μπορείτε να δημιουργήσετε ένα νέο workbook άμεσα:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Πώς μπορώ να διατηρήσω την αρχική συμβολοσειρά ιαπωνικής εποχής στο φύλλο;

Αν χρειάζεστε τόσο την αρχική συμβολοσειρά όσο και την αναλυμένη ημερομηνία, γράψτε τις σε γειτονικά κελιά:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Λειτουργεί αυτό με παλαιότερες εκδόσεις .NET;

Ναι. Το `JapaneseCalendar` υπάρχει από το .NET 2.0, και το Aspose.Cells υποστηρίζει .NET Framework 4.5+. Απλώς βεβαιωθείτε ότι κάνετε αναφορά στη σωστή συναρμολόγηση.

### Τι γίνεται με τις ζώνες ώρας;

Το `DateTime.ParseExact` επιστρέφει ένα **Kind** τύπου `Unspecified`. Αν οι πηγαίες ημερομηνίες είναι σε UTC, μετατρέψτε τις πρώτα:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Μπορώ να ορίσω προσαρμοσμένη μορφή ημερομηνίας (π.χ., “yyyy年MM月dd日”);

Απολύτως. Χρησιμοποιήστε την ιδιότητα `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Τώρα το Excel θα εμφανίζει `2020年05月01日` ενώ εξακολουθεί να αποθηκεύει μια πραγματική τιμή ημερομηνίας.

## Σύνοψη

Έχουμε καλύψει όλα όσα χρειάζεστε για να **γράψετε datetime σε Excel** από C#:

1. **Διαμορφώστε** έναν Ιαπωνικό πολιτισμό με `JapaneseCalendar` για να **μετατρέψετε συμβολοσειρές ιαπωνικού ημερολογίου**.  
2. **Αναλύστε** τη συμβολοσειρά βασισμένη στην εποχή χρησιμοποιώντας το `DateTime.ParseExact`.  
3. **Εισάγετε** το προκύπτον `DateTime` σε ένα κελί, εξασφαλίζοντας μια σωστή **τιμή ημερομηνίας κελιού Excel**.  
4. **Αποθηκεύστε** το workbook ώστε τα δεδομένα να παραμείνουν.

Με αυτά τα τέσσερα βήματα μπορείτε με ασφάλεια να **εισάγετε ημερομηνία σε φύλλο εργασίας** ανεξάρτητα από τη μορφή προέλευσης. Ο κώδικας είναι πλήρως εκτελέσιμος, απαιτεί μόνο το Aspose.Cells και λειτουργεί σε οποιοδήποτε σύγχρονο .NET runtime.

## Τι Ακολουθεί;

- **Μαζική εισαγωγή:** Επανάληψη πάνω σε γραμμές ενός CSV, ανάλυση κάθε ιαπωνικής ημερομηνίας και εγγραφή τους σε διαδοχικά κελιά.  
- **Μορφοποίηση:** Εφαρμογή conditional formatting για επισήμανση ληγμένων ημερομηνιών.  
- **Απόδοση:** Χρήση `WorkbookDesigner` ή caching του `CellStyle` όταν εργάζεστε με χιλιάδες γραμμές.  

Μη διστάσετε να πειραματιστείτε—αντικαταστήστε την ιαπωνική εποχή με το Γρηγοριανό ημερολόγιο, αλλάξτε το κελί-στόχο, ή εξάγετε σε διαφορετική μορφή αρχείου (CSV, ODS). Η βασική ιδέα παραμένει η ίδια: ανάλυση, μετατροπή και **εγγραφή datetime σε Excel** με σιγουριά.

Καλό προγραμματισμό, και εύχομαι τα φύλλα εργασίας σας να ταξινομούνται πάντα σωστά!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}