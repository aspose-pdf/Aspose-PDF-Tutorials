---
category: general
date: 2026-06-21
description: Δημιουργήστε πεδίο κειμένου PDF με C# και μάθετε πώς να αντιγράψετε πεδίο
  φόρμας PDF ή να προσθέσετε πεδίο κειμένου σε φόρμα PDF με λίγες μόνο γραμμές κώδικα.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: el
og_description: Δημιουργήστε γρήγορα πεδίο κειμένου PDF. Αυτός ο οδηγός δείχνει πώς
  να αντιγράψετε ένα πεδίο φόρμας PDF και να προσθέσετε πεδίο κειμένου σε φόρμα PDF
  χρησιμοποιώντας μια σύγχρονη βιβλιοθήκη PDF C#.
og_title: Δημιουργία πεδίου κειμένου PDF – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Δημιουργία πεδίου κειμένου PDF – Οδηγός βήμα‑προς‑βήμα
url: /el/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Πεδίου Κειμένου PDF – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **create PDF textbox field** αλλά δεν ήσασταν σίγουροι ποιες κλήσεις API να χρησιμοποιήσετε; Δεν είστε μόνοι. Είτε δημιουργείτε μια πύλη υπογραφής συμβάσεων είτε ένα απλό φύλλο συλλογής δεδομένων, η προσθήκη διαδραστικών πεδίων κειμένου σε ένα PDF είναι βασική δεξιότητα για κάθε προγραμματιστή αυτοματοποίησης φορμών.  

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που όχι μόνο **adds textbox to PDF form**, αλλά δείχνει επίσης πώς να **duplicate PDF form field** ώστε η ίδια εισαγωγή να εμφανίζεται σε πολλές σελίδες. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και με .NET Core)  
- Μια σύγχρονη βιβλιοθήκη PDF για C# – το απόσπασμα παρακάτω χρησιμοποιεί **PDFTron SDK**, αλλά οι έννοιες ισχύουν και για iText 7, PdfSharp ή άλλες βιβλιοθήκες.  
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)  

Αυτό είναι όλο – χωρίς επιπλέον υπηρεσίες, χωρίς σπάνιες εξαρτήσεις. Αν έχετε ήδη ένα PDF που θέλετε να επεκτείνετε, απλώς δείξτε τον κώδικα σε αυτό.

---

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή του SDK

Πρώτα, δημιουργήστε μια εφαρμογή console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Προσθέστε το πακέτο PDFTron NuGet:

```bash
dotnet add package PDFTron.NET
```

Τώρα ανοίξτε το `Program.cs` και εισάγετε τα namespaces που θα χρειαστούμε:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη, αντικαταστήστε τις δηλώσεις `using` με τα ισοδύναμα (π.χ., `iText.Kernel.Pdf` για iText 7).

## Βήμα 2: Αρχικοποίηση του PDF Εγγράφου και της Φόρμας

Θα ξεκινήσουμε με ένα νέο PDF που περιέχει δύο σελίδες – τη σελίδα προέλευσης για το αρχικό πεδίο κειμένου και μια σελίδα-στόχο για το αντίγραφο.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Το αντικείμενο `Form` είναι όπου ζουν όλα τα διαδραστικά πεδία. Αν το έγγραφο δεν είχε ήδη φόρμα, το `GetForm()` δημιουργεί μία για εμάς.

## Βήμα 3: **Create PDF Textbox Field** στην Πρώτη Σελίδα

Τώρα έρχεται ο πυρήνας του tutorial – η δημιουργία ενός πεδίου κειμένου. Οι συντεταγμένες του ορθογωνίου εκφράζονται σε points (1 inch = 72 points). Το παράδειγμα τοποθετεί το πλαίσιο κοντά στο επάνω‑κέντρο της πρώτης σελίδας.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Γιατί ορίζουμε το `Value` αμέσως; Η προ‑συμπλήρωση του πεδίου δίνει στους χρήστες μια ένδειξη για το αναμενόμενο εισαγόμενο κείμενο και δείχνει επίσης ότι το πεδίο λειτουργεί πλήρως.

## Βήμα 4: Προσθήκη του Πεδίου στη Φόρμα – **Add Textbox to PDF Form**

Στη συνέχεια, καταχωρούμε το πεδίο στη φόρμα χρησιμοποιώντας ένα λογικό όνομα. Αυτό το όνομα είναι αυτό που θα αναφέρετε αργότερα όταν χρειαστεί να διαβάσετε ή να τροποποιήσετε τα δεδομένα του προγραμματιστικά.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Η επιλογή ενός σαφούς ονόματος (π.χ. `"multiBox"`) κάνει τον κώδικα πιο κατανοητό, ειδικά όταν έχετε δεκάδες πεδία.

## Βήμα 5: **Duplicate PDF Form Field** σε Άλλη Σελίδα

Μια κοινή απαίτηση είναι να εμφανίζεται το ίδιο πεδίο σε πολλές σελίδες – σκεφτείτε ένα πλαίσιο “Όνομα Πελάτη” που εμφανίζεται σε κάθε σελίδα τιμολογίου. Το PDFTron μας επιτρέπει να κλωνοποιήσουμε το widget annotation, που είναι η οπτική αναπαράσταση του πεδίου.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Το κλωνοποιημένο widget μοιράζεται τα ίδια υποκείμενα δεδομένα με το αρχικό πεδίο κειμένου. Όταν ένας χρήστης πληκτρολογεί σε μια εμφάνιση, η άλλη ενημερώνεται αυτόματα – αυτό είναι το μαγικό αποτέλεσμα του **duplicate PDF form field**.

## Βήμα 6: Αποθήκευση του Εγγράφου και Καθαρισμός

Τέλος, γράψτε το PDF στο δίσκο και τερματίστε το runtime του PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Η εκτέλεση του προγράμματος παράγει ένα PDF δύο σελίδων (`output.pdf`). Ανοίξτε το με το Adobe Acrobat Reader, κάντε κλικ στο πεδίο κειμένου στη σελίδα 1, πληκτρολογήστε κάτι, μετά μεταβείτε στη σελίδα 2 – το ίδιο κείμενο εμφανίζεται αμέσως. Αυτό είναι ένα πλήρως λειτουργικό παράδειγμα **create pdf textbox field** με ένα διπλότυπο πεδίο.

---

## Πλήρες Παράδειγμα (Αντιγραφή‑Επικόλληση)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο με όνομα `output.pdf` που περιέχει δύο σελίδες. Και οι δύο σελίδες εμφανίζουν το ίδιο επεξεργάσιμο πεδίο κειμένου με την ετικέτα “Sample”. Η επεξεργασία του ενός ενημερώνει αμέσως και το άλλο.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειάζομαι το πεδίο σε *περισσότερες* από δύο σελίδες;

Απλώς επαναλάβετε τα βήματα κλωνοποίησης‑προσθήκης για κάθε επιπλέον σελίδα. Το υποκείμενο αντικείμενο δεδομένων παραμένει το ίδιο, οπότε όλα τα widgets παραμένουν συγχρονισμένα.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Πώς αλλάζω την εμφάνιση (γραμματοσειρά, περιθώριο, φόντο);

Κάθε `Widget` διαθέτει μεθόδους `SetBorderColor`, `SetBorderWidth` και `SetBackgroundColor`. Μπορείτε επίσης να ορίσετε μια συμβολοσειρά προεπιλεγμένης εμφάνισης (`DA`) για να ελέγξετε τη γραμματοσειρά και το μέγεθος.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Μπορώ να κάνω το πεδίο μόνο‑ανάγνωση μετά τη συμπλήρωση από τον χρήστη;

Ναι. Ορίστε τη σημαία `ReadOnly` στο πεδίο αφού έχετε συλλέξει τα δεδομένα, ή εναλλάξτε την ανάλογα με τη ροή εργασίας σας.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Τι γίνεται με PDF που ήδη περιέχουν φόρμα;

Αν το έγγραφο έχει ήδη AcroForm, το `doc.GetForm()` το επιστρέφει απλώς. Μπορείτε τότε να προσθέσετε νέα πεδία χωρίς να διαταράξετε τα υπάρχοντα. Απλώς προσέξτε να χρησιμοποιήσετε μοναδικά ονόματα πεδίων.

---

## Συμβουλές για Πραγματικά Έργα

- **Συμβατική ονοματοδοσίας:** Προσθέστε πρόθεμα στα ονόματα πεδίων με βάση τη σελίδα ή την ενότητα (π.χ., `invoice_customer_name`) για να αποφύγετε συγκρούσεις.  
- **Επικύρωση:** Χρησιμοποιήστε ενέργειες JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) αν χρειάζεστε επικύρωση στην πλευρά του πελάτη.  
- **Απόδοση:** Όταν εργάζεστε με μεγάλα PDF, καλέστε `doc.Lock()` πριν από μαζικές λειτουργίες για να μειώσετε το I/O overhead.  
- **Πρόσβαση:** Ορίστε την ιδιότητα `AlternateName` ώστε οι αναγνώστες οθόνης να μπορούν να περιγράψουν το πεδίο.

---

## Συμπέρασμα

Μόλις **created a PDF textbox field**, δείξαμε πώς να **duplicate PDF form field** σε πολλές σελίδες και παρουσιάσαμε τον πιο απλό τρόπο να **add textbox to PDF form** χρησιμοποιώντας C#. Ο πλήρης, εκτελέσιμος κώδικας βρίσκεται παραπάνω, και μπορείτε να τον επεκτείνετε με στυλ, επικύρωση ή επιπλέον σελίδες όπως χρειάζεται.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να ενσωματώσετε ένα dropdown (`ChoiceField`) ή ένα widget υπογραφής, ή εξερευνήστε πώς να «flatten» τη φόρμα μετά την εισαγωγή δεδομένων για αρχειοθέτηση. Το PDFTron SDK (ή οποιαδήποτε παρόμοια βιβλιοθήκη) σας παρέχει τα δομικά στοιχεία — η φαντασία σας καθορίζει το τελικό σχήμα.

Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση της βιβλιοθήκης· είναι γεμάτη παραδείγματα που συμπληρώνουν ό,τι καλύψαμε εδώ. Καλό κώδικα και να παραμένουν πάντα συγχρονισμένες οι φόρμες σας!

## Τι Να Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}