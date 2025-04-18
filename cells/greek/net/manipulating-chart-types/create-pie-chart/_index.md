---
title: Δημιουργία γραφήματος πίτας
linktitle: Δημιουργία γραφήματος πίτας
second_title: Aspose.Cells .NET Excel Processing API
description: Μάθετε πώς να δημιουργείτε ένα γράφημα πίτας στο Excel χρησιμοποιώντας το Aspose.Cells για .NET με αυτόν τον οδηγό βήμα προς βήμα. Οπτικοποιήστε τα δεδομένα σας χωρίς κόπο.
weight: 12
url: /el/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία γραφήματος πίτας

## Εισαγωγή

Η δημιουργία γραφημάτων είναι απαραίτητη για την οπτική αναπαράσταση δεδομένων και τα γραφήματα πίτας είναι ένας από τους πιο δημοφιλείς τρόπους απεικόνισης του τρόπου με τον οποίο τα μέρη συνθέτουν ένα σύνολο. Με το Aspose.Cells για .NET, μπορείτε εύκολα να αυτοματοποιήσετε τη δημιουργία γραφημάτων πίτας σε αρχεία Excel. Σε αυτό το σεμινάριο, θα εξετάσουμε πώς να δημιουργήσετε ένα γράφημα πίτας από την αρχή χρησιμοποιώντας το Aspose.Cells για .NET, με έναν οδηγό βήμα προς βήμα για να κάνετε τη διαδικασία ομαλή και απλή. Είτε είστε νέος στο εργαλείο είτε θέλετε να βελτιώσετε τις δεξιότητές σας στον αυτοματισμό του Excel, αυτός ο οδηγός σας καλύπτει!

## Προαπαιτούμενα

Πριν βουτήξετε στον κώδικα, βεβαιωθείτε ότι έχετε ρυθμίσει τις ακόλουθες ρυθμίσεις:

1.  Aspose.Cells for .NET Library: Βεβαιωθείτε ότι έχετε εγκαταστήσει το Aspose.Cells στο έργο σας. Εάν δεν το έχετε εγκαταστήσει ακόμα, μπορείτε να το κατεβάσετε από[εδώ](https://releases.aspose.com/cells/net/).
2. .NET Development Environment: Βεβαιωθείτε ότι το έργο σας έχει ρυθμιστεί για χρήση .NET Framework ή .NET Core.
3. Βασικές γνώσεις C#: Θα πρέπει να είστε άνετοι με τον προγραμματισμό C#, ιδιαίτερα τον αντικειμενοστραφή προγραμματισμό (OOP).

 Για προχωρημένους χρήστες, μπορεί να εφαρμοστεί μια προσωρινή άδεια χρήσης για το ξεκλείδωμα όλων των δυνατοτήτων του Aspose.Cells. Μπορείτε να ζητήσετε ένα από[εδώ](https://purchase.aspose.com/temporary-license/).

## Εισαγωγή πακέτων

Για να ξεκινήσετε, εισαγάγετε τους απαραίτητους χώρους ονομάτων και τα πακέτα που απαιτούνται για αυτό το σεμινάριο. Αυτές περιλαμβάνουν βασικές λειτουργίες I/O και το πακέτο Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Βήμα 1: Δημιουργήστε ένα νέο βιβλίο εργασίας

 Πρώτα, πρέπει να δημιουργήσουμε ένα παράδειγμα του`Workbook` κλάση, η οποία αντιπροσωπεύει το αρχείο Excel. Ένα βιβλίο εργασίας περιέχει πολλά φύλλα και για το παράδειγμά μας, θα εργαστούμε με δύο φύλλα — ένα για δεδομένα και ένα για το γράφημα πίτας.

```csharp
Workbook workbook = new Workbook();
```

Αυτό ξεκινά ένα νέο βιβλίο εργασίας του Excel. Πού πάνε όμως τα δεδομένα; Ας το φροντίσουμε στο επόμενο βήμα.

## Βήμα 2: Προσθήκη δεδομένων στο φύλλο εργασίας

Μόλις δημιουργηθεί το βιβλίο εργασίας, πρέπει να αποκτήσουμε πρόσβαση στο πρώτο φύλλο εργασίας και να του δώσουμε ένα όνομα. Εδώ θα εισαγάγουμε τα δεδομένα που απαιτούνται για το γράφημα πίτας.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Τώρα, μπορούμε να εισαγάγουμε ορισμένα εικονικά δεδομένα πωλήσεων που αντιπροσωπεύουν διαφορετικές περιοχές:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Εδώ, προσθέτουμε δύο στήλες: μία για τις περιοχές και μία για τα στοιχεία πωλήσεων. Αυτά τα δεδομένα θα αναπαρασταθούν στο γράφημα πίτας.

## Βήμα 3: Προσθέστε ένα φύλλο γραφήματος

Στη συνέχεια, ας προσθέσουμε ένα ξεχωριστό φύλλο εργασίας για να διατηρήσουμε το γράφημα πίτας.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Αυτό το νέο φύλλο θα φιλοξενεί το γράφημα πίτας. Δίνοντάς του ένα όνομα όπως "Διάγραμμα" διασφαλίζει ότι οι χρήστες γνωρίζουν τι να περιμένουν όταν ανοίγουν το αρχείο.

## Βήμα 4: Δημιουργήστε το γράφημα πίτας

Τώρα ήρθε η ώρα να δημιουργήσετε το πραγματικό γράφημα. Θα καθορίσουμε ότι θέλουμε ένα γράφημα πίτας και θα ορίσουμε τη θέση του στο φύλλο.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Η μέθοδος`Add()`δέχεται παραμέτρους για τον τύπο γραφήματος (στην περίπτωση αυτή,`ChartType.Pie`), και τη θέση του στο φύλλο εργασίας. Οι αριθμοί αντιπροσωπεύουν θέσεις σειρών και στηλών.

## Βήμα 5: Προσαρμόστε την εμφάνιση του γραφήματος

Ένα γράφημα πίτας δεν θα ήταν πλήρες χωρίς κάποια προσαρμογή! Ας κάνουμε το γράφημά μας οπτικά ελκυστικό, τροποποιώντας τα χρώματα, τις ετικέτες και τον τίτλο.

### Ορισμός τίτλου γραφήματος
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Προσαρμόστε την περιοχή του οικοπέδου
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Ρυθμίζουμε το ντεγκραντέ γέμισμα για την περιοχή του οικοπέδου και κρύβουμε το περίγραμμα για πιο καθαρή εμφάνιση.

## Βήμα 6: Ορισμός δεδομένων γραφήματος

 Ήρθε η ώρα να συνδέσουμε το γράφημα με τα δεδομένα μας. Ο`NSeries` Η ιδιότητα του γραφήματος συνδέει τα στοιχεία και τις περιοχές πωλήσεων στο γράφημα πίτας.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 Η πρώτη γραμμή προσδιορίζει ότι χρησιμοποιούμε τα δεδομένα πωλήσεων από κελιά`B2:B8` . Λέμε επίσης στο γράφημα να χρησιμοποιεί τα ονόματα των περιοχών από`A2:A8` ως ετικέτες κατηγορίας.

## Βήμα 7: Προσθήκη ετικετών δεδομένων

Η προσθήκη ετικετών απευθείας στα τμήματα του γραφήματος μπορεί να διευκολύνει την κατανόηση. Ας συμπεριλάβουμε τα ονόματα των περιοχών και τις τιμές πωλήσεων στα τμήματα του γραφήματος πίτας.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Βήμα 8: Προσαρμόστε την περιοχή γραφήματος και το υπόμνημα

Τέλος, ας δώσουμε στην περιοχή του γραφήματος και ας γράψουμε μερικές τελευταίες πινελιές. Αυτό βελτιώνει τη συνολική παρουσίαση του γραφήματος.

### Περιοχή γραφήματος
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Θρύλος
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Βήμα 9: Αποθηκεύστε το βιβλίο εργασίας

Τέλος, αποθηκεύουμε το βιβλίο εργασίας σε αρχείο Excel. Μπορείτε να καθορίσετε τον κατάλογο εξόδου και το όνομα αρχείου όπως απαιτείται.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Σύναψη

Η δημιουργία ενός γραφήματος πίτας με το Aspose.Cells για .NET είναι μια απλή και προσαρμόσιμη διαδικασία. Ακολουθώντας αυτόν τον οδηγό, μπορείτε να δημιουργήσετε ένα γράφημα με επαγγελματική εμφάνιση που μεταφέρει πολύτιμες πληροφορίες σε λίγα μόλις βήματα. Είτε για επιχειρηματική αναφορά είτε για εκπαιδευτικούς σκοπούς, η εξοικείωση με τη δημιουργία γραφημάτων θα βελτιώσει τις δεξιότητές σας στον αυτοματισμό του Excel. Θυμηθείτε, το Aspose.Cells παρέχει την ευελιξία που χρειάζεστε για να δημιουργήσετε εκπληκτικά αρχεία Excel που βασίζονται σε δεδομένα χωρίς κόπο.

## Συχνές ερωτήσεις

### Μπορώ να δημιουργήσω άλλους τύπους γραφημάτων χρησιμοποιώντας το Aspose.Cells για .NET;
Ναί! Το Aspose.Cells υποστηρίζει διάφορους τύπους γραφημάτων, συμπεριλαμβανομένων γραφημάτων ράβδων, γραμμικών γραφημάτων και γραφημάτων διασποράς.

### Χρειάζομαι άδεια επί πληρωμή για να χρησιμοποιήσω το Aspose.Cells για .NET;
Μπορείτε να χρησιμοποιήσετε τη δωρεάν έκδοση με ορισμένους περιορισμούς. Για πλήρεις δυνατότητες, θα χρειαστείτε μια άδεια, την οποία μπορείτε να αγοράσετε[εδώ](https://purchase.aspose.com/buy).

### Μπορώ να εξαγάγω το γράφημα σε μορφές όπως PDF ή εικόνες;
Απολύτως! Το Aspose.Cells σάς επιτρέπει να εξάγετε γραφήματα σε διάφορες μορφές, συμπεριλαμβανομένων των PDF και PNG.

### Είναι δυνατόν να διαμορφώσετε κάθε φέτα πίτας με διαφορετικά χρώματα;
 Ναι, μπορείτε να εφαρμόσετε διαφορετικά χρώματα σε κάθε φέτα ρυθμίζοντας το`IsColorVaried` ιδιοκτησία σε`true`, όπως φαίνεται στο σεμινάριο.

### Μπορώ να αυτοματοποιήσω τη δημιουργία πολλών γραφημάτων σε ένα μόνο βιβλίο εργασίας;
Ναι, μπορείτε να δημιουργήσετε και να προσαρμόσετε όσα γραφήματα χρειάζονται σε ένα μόνο αρχείο Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
