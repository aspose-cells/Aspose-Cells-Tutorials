---
category: general
date: 2026-06-30
description: Ενεργοποιήστε τον ορθογραφικό έλεγχο στο GridJs και μάθετε πώς να ενεργοποιήσετε
  τον έλεγχο σύνταξης, να ορίσετε τη γλώσσα ορθογραφίας και να ανακτήσετε τη διαμόρφωση
  του πελάτη σε έναν ενιαίο οδηγό.
draft: false
keywords:
- enable spell check
- how to enable spell check
- how to enable syntax check
- how to set spell language
- retrieve client config
language: el
og_description: Ενεργοποιήστε τον ορθογραφικό έλεγχο στο GridJs και δείτε πώς να ενεργοποιήσετε
  τον έλεγχο σύνταξης, να ορίσετε τη γλώσσα ορθογραφίας και να ανακτήσετε τη διαμόρφωση
  του πελάτη σε ένα ενιαίο οδηγό.
og_title: Ενεργοποίηση ορθογραφικού ελέγχου στο GridJs – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Enable spell check in GridJs and learn how to enable syntax check,
    set spell language, and retrieve client config in a single walkthrough.
  headline: Enable Spell Check in GridJs – Complete Programming Guide
  type: TechArticle
- description: Enable spell check in GridJs and learn how to enable syntax check,
    set spell language, and retrieve client config in a single walkthrough.
  name: Enable Spell Check in GridJs – Complete Programming Guide
  steps:
  - name: '**Creating the `GridJs` instance** gives you a fresh context where all
      settings start from defaults.'
    text: '**Creating the `GridJs` instance** gives you a fresh context where all
      settings start from defaults.'
  - name: '**Binding the worksheet** (`set_worksheet`) tells GridJs which sheet the
      helpers should monitor. Without this, the helpers have nothing to act upon.'
    text: '**Binding the worksheet** (`set_worksheet`) tells GridJs which sheet the
      helpers should monitor. Without this, the helpers have nothing to act upon.'
  - name: '**Enabling syntax check** (`how to enable syntax check`) adds a lightweight
      parser that underlines malformed formulas, saving you from runtime errors later.'
    text: '**Enabling syntax check** (`how to enable syntax check`) adds a lightweight
      parser that underlines malformed formulas, saving you from runtime errors later.'
  - name: '**Turning on spell check** (`enable spell check`) highlights misspelled
      words in cell comments and plain‑text cells. Setting the language (`how to set
      spell language`) ensures the dictionary matches your locale—critical for non‑English
      sheets.'
    text: '**Turning on spell check** (`enable spell check`) highlights misspelled
      words in cell comments and plain‑text cells. Setting the language (`how to set
      spell language`) ensures the dictionary matches your locale—critical for non‑English
      sheets.'
  - name: '**Retrieving the client config** (`retrieve client config`) gives you a
      JSON snapshot of all active settings. You can store this JSON in a database,
      send it to a front‑end, or simply log it for debugging.'
    text: '**Retrieving the client config** (`retrieve client config`) gives you a
      JSON snapshot of all active settings. You can store this JSON in a database,
      send it to a front‑end, or simply log it for debugging.'
  type: HowTo
tags:
- GridJs
- Python
- Spreadsheet Automation
title: Ενεργοποίηση ορθογραφικού ελέγχου στο GridJs – Πλήρης οδηγός προγραμματισμού
url: /el/python/integration-and-interoperability/enable-spell-check-in-gridjs-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ενεργοποίηση ορθογραφικού ελέγχου στο GridJs – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε τον ορθογραφικό έλεγχο** για ένα φύλλο εργασίας GridJs χωρίς να σκάβετε μέσα σε ατελείωτη τεκμηρίωση; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε βήμα-βήμα τις ακριβείς ενέργειες για να ενεργοποιήσετε τον ορθογραφικό έλεγχο, να ενεργοποιήσετε τον συντακτικό έλεγχο, να ορίσετε τη γλώσσα του ορθογραφικού ελέγχου και, τέλος, να εξάγετε το JSON διαμόρφωσης του πελάτη ώστε να μπορείτε να το ελέγξετε ή να το αποθηκεύσετε.

Και ναι, θα καλύψουμε επίσης **πώς να ενεργοποιήσετε τον συντακτικό έλεγχο**, επειδή οι περισσότεροι προγραμματιστές καταλήγουν να χρειάζονται και τους δύο βοηθούς ταυτόχρονα. Στο τέλος αυτού του οδηγού θα έχετε ένα έτοιμο‑για‑εκτέλεση script που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο χρησιμοποιεί το GridJs Python API.

## Τι θα μάθετε

- Αρχικοποίηση ενός αντικειμένου `GridJs` και σύνδεσή του με ένα φύλλο εργασίας.  
- Ενεργοποίηση του βοηθού **ορθογραφικού ελέγχου** (`enable spell check`).  
- Ενεργοποίηση του βοηθού **συντακτικού ελέγχου** (`how to enable syntax check`).  
- Αλλαγή της γλώσσας ορθογραφικού ελέγχου (`how to set spell language`).  
- Ανάκτηση της πλήρους διαμόρφωσης πελάτη (`retrieve client config`).  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες εκτός του GridJs, και ο κώδικας λειτουργεί με Python 3.9+.

---

## Προαπαιτούμενα

- Python 3.9 ή νεότερη έκδοση εγκατεστημένη στον υπολογιστή σας.  
- Ένα έγκυρο άδεια GridJs ή μια δωρεάν δοκιμή που σας επιτρέπει να δημιουργήσετε ένα αντικείμενο `gridjs.GridJs`.  
- Βασική εξοικείωση με συναρτήσεις και αντικείμενα Python.  

Αν ήδη έχετε ένα αντικείμενο φύλλου εργασίας (`ws`) από το spreadsheet σας, είστε έτοιμοι. Διαφορετικά, δημιουργήστε ένα χρησιμοποιώντας το API του workbook του GridJs – αυτό το κομμάτι βρίσκεται εκτός του παρόντος οδηγού, αλλά καλύπτεται στην επίσημη τεκμηρίωση.

---

## Ενεργοποίηση Ορθογραφικού και Συντακτικού Ελέγχου στο GridJs

Παρακάτω βρίσκεται το **πλήρες, εκτελέσιμο script** που δείχνει όλες τις δυνατότητες που συζητήσαμε. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε ένα νέο αρχείο με όνομα `gridjs_helpers.py` και να το εκτελέσετε.

```python
# gridjs_helpers.py
import json
import gridjs  # Make sure the GridJs Python package is installed

def configure_gridjs(worksheet):
    """
    Sets up spell‑check and syntax‑check helpers for a given worksheet,
    then returns the client configuration as a formatted JSON string.
    """
    # Step 1: Create a GridJs instance
    grid = gridjs.GridJs()

    # Step 2: Associate the worksheet you want to work with
    grid.set_worksheet(worksheet)

    # Step 3: Enable the syntax‑check helper to underline formula errors
    grid.settings.syntax_check.enabled = True

    # Step 4: Enable the spell‑check helper and optionally set its language
    grid.settings.spell_check.enabled = True                # how to enable spell check
    grid.settings.spell_check.language = "en-US"            # how to set spell language

    # Step 5: Retrieve the client configuration JSON and display it
    config_json = grid.get_client_config()
    # Pretty‑print for readability
    formatted = json.dumps(config_json, indent=2)
    print("=== GridJs Client Configuration ===")
    print(formatted)

    # Return the raw dict in case the caller needs to process it
    return config_json

# ----------------------------------------------------------------------
# Example usage – replace this with your actual worksheet object
if __name__ == "__main__":
    # Mock worksheet for demonstration; in real code, fetch from your workbook
    ws = gridjs.Worksheet(name="DemoSheet")
    configure_gridjs(ws)
```

### Γιατί Κάθε Βήμα Είναι Σημαντικό

1. **Η δημιουργία του αντικειμένου `GridJs`** σας παρέχει ένα νέο περιβάλλον όπου όλες οι ρυθμίσεις ξεκινούν από τις προεπιλογές.  
2. **Η σύνδεση του φύλλου εργασίας** (`set_worksheet`) ενημερώνει το GridJs ποιο φύλλο πρέπει να παρακολουθούν οι βοηθοί. Χωρίς αυτό, οι βοηθοί δεν έχουν τίποτα πάνω στο οποίο να δράσουν.  
3. **Η ενεργοποίηση του συντακτικού ελέγχου** (`how to enable syntax check`) προσθέτει έναν ελαφρύ parser που υπογραμμίζει λανθασμένες φόρμουλες, εξοικονομώντας σας σφάλματα χρόνου εκτέλεσης αργότερα.  
4. **Η ενεργοποίηση του ορθογραφικού ελέγχου** (`enable spell check`) επισημαίνει λανθασμένες λέξεις σε σχόλια κελιών και σε κελιά απλού κειμένου. Η ρύθμιση της γλώσσας (`how to set spell language`) εξασφαλίζει ότι το λεξικό ταιριάζει με την περιοχή σας — κρίσιμο για φύλλα που δεν είναι στα Αγγλικά.  
5. **Η ανάκτηση της διαμόρφωσης πελάτη** (`retrieve client config`) σας παρέχει ένα στιγμιότυπο JSON με όλες τις ενεργές ρυθμίσεις. Μπορείτε να αποθηκεύσετε αυτό το JSON σε μια βάση δεδομένων, να το στείλετε στο front‑end, ή απλώς να το καταγράψετε για εντοπισμό σφαλμάτων.

> **Pro tip:** Αν χρειάζεστε μόνο ορθογραφικό έλεγχο για μια συγκεκριμένη γλώσσα, απενεργοποιήστε την προεπιλεγμένη εναλλακτική γλώσσα ορίζοντας `grid.settings.spell_check.fallback = False`. Αυτό αποτρέπει τον βοηθό από το να αλλάζει σιωπηλά σε Αγγλικά όταν δεν βρίσκει αντιστοιχία.

---

## Πώς να Ενεργοποιήσετε Ξεχωριστά τον Συντακτικό Έλεγχο

Μερικές φορές μπορεί να σας ενδιαφέρει μόνο η επικύρωση των τύπων. Το παρακάτω απόσπασμα απομονώνει αυτή τη λειτουργία:

```python
def enable_only_syntax_check(grid):
    """
    Turns on syntax checking while leaving spell‑check disabled.
    """
    grid.settings.syntax_check.enabled = True
    grid.settings.spell_check.enabled = False   # Explicitly turn off spell‑check
    return grid.get_client_config()
```

**Πότε να το χρησιμοποιήσετε;** Αν το spreadsheet σας είναι καθαρά αριθμητικό ή έχετε ήδη μια ξεχωριστή διαδικασία ορθογραφικού ελέγχου, η απενεργοποίηση του βοηθού ορθογραφικού ελέγχου μειώνει το φορτίο CPU.

---

## Πώς να Ορίσετε τη Γλώσσα Ορθογραφικού Ελέγχου Δυναμικά

Μπορείτε να επιτρέψετε στους τελικούς χρήστες να επιλέγουν τη γλώσσα που προτιμούν κατά την εκτέλεση. Εδώ είναι ένας μικρός βοηθός που αλλάζει τη γλώσσα βάσει παραμέτρου:

```python
def set_spell_language(grid, lang_code="en-US"):
    """
    Updates the spell‑check language. Accepts any IETF language tag
    supported by GridJs (e.g., 'fr-FR', 'es-ES', 'de-DE').
    """
    if not isinstance(lang_code, str):
        raise TypeError("Language code must be a string")
    grid.settings.spell_check.language = lang_code
    # Re‑fetch config to confirm the change
    return grid.get_client_config()
```

**Ακραία περίπτωση:** Αν παρέχετε έναν μη υποστηριζόμενο κωδικό γλώσσας, το GridJs θα επιστρέψει στην προεπιλογή (`en-US`). Για να αποφύγετε σιωπηλές εναλλακτικές, μπορείτε να ελέγξετε το `grid.supported_languages` πριν εφαρμόσετε την αλλαγή.

---

## Ανάκτηση JSON Διαμόρφωσης Πελάτη – Τι να Περιμένετε

Η κλήση `grid.get_client_config()` επιστρέφει ένα λεξικό Python που αντικατοπτρίζει το JSON που αποστέλλεται στον πελάτη front‑end. Ένα τυπικό αποτέλεσμα μοιάζει με αυτό:

```json
{
  "worksheetId": "ws_12345",
  "settings": {
    "syntax_check": {
      "enabled": true
    },
    "spell_check": {
      "enabled": true,
      "language": "en-US",
      "fallback": true
    }
  },
  "version": "2.4.1"
}
```

Μπορείτε να δείτε τις σημαίες `enabled`, τη επιλεγμένη γλώσσα, ακόμη και την έκδοση της βιβλιοθήκης. Αυτό είναι ακριβώς αυτό που υποδεικνύει η λέξη‑κλειδί **retrieve client config**, και είναι χρήσιμο για εντοπισμό σφαλμάτων ή αποθήκευση προτιμήσεων χρήστη μεταξύ συνεδριών.

---

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Σύμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Καμία υπογράμμιση σε σφάλματα φόρμουλας | Το `syntax_check.enabled` είναι ακόμα `False` | Βεβαιωθείτε ότι καλέσατε `grid.settings.syntax_check.enabled = True` πριν από οποιαδήποτε εισαγωγή φόρμουλας. |
| Ο ορθογραφικός έλεγχος επισημαίνει κάθε λέξη | Η γλώσσα δεν έχει οριστεί ή το fallback είναι ενεργό | Ορίστε `grid.settings.spell_check.language` σε έναν έγκυρο κωδικό και προαιρετικά απενεργοποιήστε το fallback. |
| `grid.get_client_config()` επιστρέφει κενό λεξικό | Το φύλλο εργασίας δεν είναι συνδεδεμένο (`set_worksheet` λείπει) | Καλέστε `grid.set_worksheet(ws)` με ένα έγκυρο αντικείμενο φύλλου εργασίας πρώτα. |
| Η εξαγωγή JSON προκαλεί `TypeError` | Μη-σειριοποιήσιμα αντικείμενα στη διαμόρφωση | Χρησιμοποιήστε `json.dumps(..., default=str)` ή φιλτράρετε τα προσαρμοσμένα αντικείμενα πριν την εκτύπωση. |

---

## Συνοπτικό Παράδειγμα Πλήρους Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το τελικό script που μπορείτε να τρέξετε αμέσως:

```python
import json
import gridjs

def main():
    # Create a demo worksheet – replace with your actual worksheet
    ws = gridjs.Worksheet(name="DemoSheet")

    # Initialize GridJs and configure helpers
    grid = gridjs.GridJs()
    grid.set_worksheet(ws)

    # Enable both helpers
    grid.settings.syntax_check.enabled = True          # how to enable syntax check
    grid.settings.spell_check.enabled = True           # enable spell check
    grid.settings.spell_check.language = "en-US"       # how to set spell language

    # Retrieve and display the client configuration
    config = grid.get_client_config()
    print("\n=== Client Config ===")
    print(json.dumps(config, indent=2))

if __name__ == "__main__":
    main()
```

Τρέξτε το με:

```bash
python gridjs_helpers.py
```

Θα πρέπει να δείτε το ωραία μορφοποιημένο JSON να εκτυπώνεται στην κονσόλα, επιβεβαιώνοντας ότι και οι δύο βοηθοί είναι ενεργοί και ότι η γλώσσα είναι ορισμένη σε `en-US`.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Διατήρηση προτιμήσεων χρήστη:** Αποθηκεύστε το JSON από `retrieve client config` σε μια βάση δεδομένων και επαναφορτώστε το κατά την έναρξη της συνεδρίας.  
- **Προσαρμοσμένα λεξικά:** Μάθετε πώς να προσθέτετε όρους ειδικούς για το πεδίο στο λεξικό ορθογραφικού ελέγχου του GridJs (`grid.settings.spell_check.custom_words`).  
- **Προηγμένη διάγνωση φόρμουλας:** Συνδυάστε τον συντακτικό έλεγχο με το API `formula_audit` του GridJs για πιο βαθιά ανάλυση σφαλμάτων.  
- **Διεθνοποίηση:** Εξερευνήστε το `grid.settings.spell_check.language` με τοπικές ρυθμίσεις όπως `fr-FR` ή `ja-JP` για υποστήριξη πολυγλωσσικών ομάδων.

Πειραματιστείτε — απενεργοποιήστε έναν βοηθό, αλλάξτε γλώσσες, ή συνδέστε τη διαμόρφωση σε ένα UI component. Η ευελιξία του GridJs το καθιστά παιχνιδάκι.

---

## Συμπέρασμα

Καλύψαμε **την ενεργοποίηση του ορθογραφικού ελέγχου** στο GridJs από την αρχή μέχρι το τέλος, δείξαμε **πώς να ενεργοποιήσετε τον συντακτικό έλεγχο**, παρουσιάσαμε **πώς να ορίσετε τη γλώσσα ορθογραφικού ελέγχου**, και τελικά εξηγήσαμε **πώς να ανακτήσετε τη διαμόρφωση πελάτη** για έλεγχο ή αποθήκευση. Με το πλήρες παράδειγμα κώδικα παραπάνω, μπορείτε να ενσωματώσετε αυτούς τους βοηθούς σε οποιαδήποτε ροή εργασίας GridJs βασισμένη σε Python μέσα σε λίγα λεπτά.

Αν αντιμετωπίσατε δυσκολίες ή έχετε ιδέες για επέκταση της λειτουργικότητας, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και εύχομαι τα spreadsheets σας να παραμείνουν χωρίς σφάλματα!

![Στιγμιότυπο του πίνακα ρυθμίσεων του GridJs με ενεργοποιημένο ορθογραφικό έλεγχο](https://example.com/images/enable-spell-check.png "Ενεργοποίηση ορθογραφικού ελέγχου στις ρυθμίσεις του GridJs")

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να Ορίσετε τη Γλώσσα σε Αρχεία Excel Χρησιμοποιώντας Aspose.Cells .NET για Πολυγλωσσική Υποστήριξη](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Πώς να Ελέγξετε την Προστασία Κωδικού Φύλλου Εργασίας σε Excel χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/security-protection/aspose-cells-dotnet-check-excel-worksheet-password-protection/)
- [Πώς να Ελέγξετε τα Κλειδώματα Έργου VBA σε Αρχεία Excel Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/security-protection/check-vba-project-locks-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}