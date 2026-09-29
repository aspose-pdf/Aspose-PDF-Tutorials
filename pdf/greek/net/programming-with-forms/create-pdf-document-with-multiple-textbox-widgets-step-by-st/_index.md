---
category: general
date: 2026-02-12
description: Δημιουργήστε ένα έγγραφο PDF και προσθέστε μια κενή σελίδα PDF ενώ δημιουργείτε
  ένα πεδίο φόρμας – μάθετε πώς να προσθέτετε γρήγορα πλαίσια κειμένου PDF σε C#.
draft: false
keywords:
- create pdf document
- add blank page pdf
- create pdf form field
- how to create pdf form
- how to add textbox pdf
language: el
og_description: Δημιουργήστε έγγραφο PDF με μια κενή σελίδα και πολλαπλά widget πεδίων
  κειμένου. Ακολουθήστε αυτόν τον οδηγό για να μάθετε πώς να προσθέτετε πεδία κειμένου
  PDF χρησιμοποιώντας το Aspose.Pdf.
og_title: Δημιουργία εγγράφου PDF – Προσθήκη στοιχείων TextBox σε C#
tags:
- pdf
- csharp
- aspose
- form-fields
title: Δημιουργία εγγράφου PDF με πολλαπλά widgets TextBox – Οδηγός βήμα‑βήμα
url: /el/net/programming-with-forms/create-pdf-document-with-multiple-textbox-widgets-step-by-st/
---

keep them unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου PDF με πολλαπλά Widgets TextBox – Πλήρης Εκπαίδευση

Έχετε ποτέ χρειαστεί να **create pdf document** που περιέχει μια φόρμα με περισσότερα από ένα widget TextBox; Δεν είστε μόνοι—οι προγραμματιστές συχνά ρωτούν, *«πώς να προσθέσω πεδία pdf textbox που εμφανίζονται σε δύο θέσεις;»* Τα καλά νέα είναι ότι το Aspose.Pdf το κάνει παιχνιδάκι. Σε αυτόν τον οδηγό θα περάσουμε από τη δημιουργία ενός PDF, την προσθήκη μιας κενής σελίδας pdf, τη δημιουργία ενός πεδίου φόρμας, και τελικά θα δείξουμε **how to add textbox pdf** widgets προγραμματιστικά.

Θα καλύψουμε όλα όσα χρειάζεστε: από την αρχικοποίηση του εγγράφου μέχρι την αποθήκευση του τελικού αρχείου. Στο τέλος θα έχετε ένα έτοιμο‑για‑χρήση PDF που δείχνει **how to create pdf form** στοιχεία με πολλαπλά widgets, και θα καταλάβετε τις μικρές λεπτομέρειες που διατηρούν τη φόρμα αξιόπιστη σε διάφορους προβολείς PDF.

## Τι Θα Χρειαστεί

- **Aspose.Pdf for .NET** (οποιαδήποτε πρόσφατη έκδοση· το API που χρησιμοποιείται εδώ λειτουργεί με 23.x και νεότερες).  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή ακόμη και VS Code με την επέκταση C#).  
- Βασική εξοικείωση με τη σύνταξη C#—δεν απαιτείται βαθιά γνώση PDF.

Αν έχετε τσεκάρει όλα τα παραπάνω, ας ξεκινήσουμε.

## Βήμα 1: Create PDF Document – Αρχικοποίηση και Προσθήκη Κενής Σελίδας

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο **create pdf document** και να του δώσουμε έναν καθαρό καμβά. Η προσθήκη μιας κενής σελίδας pdf είναι τόσο απλή όσο η κλήση του `Pages.Add()`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

public class MultiWidgetExample
{
    public static void Main()
    {
        // Step 1: Create a new PDF document (the canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a blank page pdf to the document
            var pdfPage = pdfDocument.Pages.Add();

            // The rest of the steps follow...
```

*Γιατί είναι σημαντικό:* Η κλάση `Document` αντιπροσωπεύει ολόκληρο το αρχείο. Χωρίς σελίδα, δεν υπάρχει που να τοποθετηθούν τα πεδία φόρμας, έτσι η κενή σελίδα pdf αποτελεί τη βάση κάθε φόρμας που θα δημιουργήσετε.

## Βήμα 2: Create PDF Form Field – Ορισμός TextBox που Μπορεί να Φιλοξενήσει Πολλαπλά Widgets

Τώρα δημιουργούμε το πραγματικό **create pdf form field**. Το Aspose το ονομάζει `TextBoxField`. Η ρύθμιση `MultipleWidgets = true` λέει στη μηχανή ότι αυτό το πεδίο μπορεί να εμφανιστεί περισσότερες από μία φορές.

```csharp
            // Step 3: Create a TextBox field that supports multiple widgets
            var multiWidgetTextBox = new TextBoxField(
                pdfPage,
                new Rectangle(50, 700, 250, 730)); // position on the first page
            multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
            multiWidgetTextBox.Value = "First widget";
```

*Συμβουλή:* Οι συντεταγμένες του ορθογωνίου εκφράζονται σε points (1 pt = 1/72 in). Προσαρμόστε τις ώστε να ταιριάζουν στο layout σας· το παράδειγμα τοποθετεί το κουτί κοντά στην επάνω‑αριστερή γωνία.

## Βήμα 3: Προσθήκη του Πρώτου Widget στη Φόρμα

Με το πεδίο ορισμένο, το συνδέουμε με τη συλλογή φορμών του εγγράφου. Αυτό είναι το βήμα **how to add textbox pdf** για το κύριο widget.

```csharp
            // Step 4: Add the TextBox field to the form (first widget)
            pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);
```

Το τρίτο όρισμα (`1`) είναι ο δείκτης του widget—αρχίζει από 1 επειδή ήδη έχουμε ένα widget στη σελίδα που δημιουργήσαμε στο προηγούμενο βήμα.

## Βήμα 4: Προσθήκη Δεύτερου Widget Προγραμματιστικά – Η Πραγματική Δύναμη των Πολλαπλών Widgets

Αν ποτέ αναρωτηθήκατε **how to create pdf form** στοιχεία που επαναλαμβάνονται, εδώ συμβαίνει η μαγεία. Δημιουργούμε ένα `WidgetAnnotation` και το προσθέτουμε στη συλλογή `Widgets` του πεδίου.

```csharp
            // Step 5: Create and attach a second widget programmatically
            var secondWidget = new WidgetAnnotation(
                new Rectangle(300, 700, 500, 730)); // position on the same page
            multiWidgetTextBox.Widgets.Add(secondWidget);
```

*Γιατί να προσθέσουμε δεύτερο widget;* Οι χρήστες μπορεί να χρειαστεί να συμπληρώσουν την ίδια τιμή σε δύο θέσεις—σκεφτείτε ένα πεδίο “Customer Name” που εμφανίζεται στην κορυφή μιας φόρμας και ξανά σε ένα μπλοκ υπογραφής. Με το ίδιο όνομα πεδίου (`MultiTB`), οποιαδήποτε αλλαγή σε ένα σημείο ενημερώνει αυτόματα το άλλο.

## Βήμα 5: Αποθήκευση του PDF – Επαλήθευση ότι Εμφανίζονται Και Τα Δύο Widgets

Τέλος, γράφουμε το έγγραφο στο δίσκο. Το αρχείο θα περιέχει δύο συγχρονισμένα widgets textbox.

```csharp
            // Step 6: Save the PDF with both widgets
            pdfDocument.Save("multiWidget.pdf");
        }
    }
}
```

Όταν ανοίξετε το `multiWidget.pdf` στο Adobe Acrobat, Foxit ή ακόμη και σε προβολέα PDF του προγράμματος περιήγησης, θα δείτε δύο πλαίσια κειμένου δίπλα-δίπλα. Η πληκτρολόγηση σε ένα ενημερώνει το άλλο αμέσως—απόδειξη ότι ολοκληρώσαμε επιτυχώς **how to add textbox pdf** με πολλαπλά widgets.

### Αναμενόμενο Αποτέλεσμα

- Ένα PDF μονοσέλιδου με όνομα `multiWidget.pdf`.  
- Δύο widgets textbox με ετικέτα “First widget”.  
- Και τα δύο κουτιά μοιράζονται το ίδιο όνομα πεδίου, έτσι αντικατοπτρίζουν το περιεχόμενο το ένα του άλλου.

![Δημιουργία εγγράφου PDF με πολλαπλά widgets TextBox](https://example.com/images/multi-widget.png "Παράδειγμα δημιουργίας εγγράφου PDF")

*Image alt text:* create pdf document showing two textbox widgets

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να τοποθετήσω widgets σε διαφορετικές σελίδες;

Απολύτως. Απλώς δημιουργήστε ένα νέο αντικείμενο `Page` για το δεύτερο widget και χρησιμοποιήστε τις συντεταγμένες του. Το πεδίο θα παραμείνει συνδεδεμένο επειδή το όνομα (`"MultiTB"`) παραμένει το ίδιο.

```csharp
var secondPage = pdfDocument.Pages.Add();
var thirdWidget = new WidgetAnnotation(new Rectangle(50, 700, 250, 730));
multiWidgetTextBox.Widgets.Add(thirdWidget);
```

### Τι γίνεται αν χρειάζομαι διαφορετική προεπιλεγμένη τιμή για κάθε widget;

Η ιδιότητα `Value` εφαρμόζεται σε ολόκληρο το πεδίο, όχι σε μεμονωμένα widgets. Αν χρειάζεστε διαφορετικές προεπιλογές, θα πρέπει να δημιουργήσετε ξεχωριστά πεδία αντί να χρησιμοποιήσετε `MultipleWidgets`.

### Λειτουργεί αυτό με συμμόρφωση PDF/A ή PDF/UA;

Ναι, αλλά ίσως χρειαστεί να ορίσετε πρόσθετες ιδιότητες εγγράφου (π.χ., `pdfDocument.ConvertToPdfA()`) μετά την προσθήκη των πεδίων φόρμας. Η σύνδεση των widgets παραμένει αμετάβλητη.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Απλώς τοποθετήστε το σε ένα πρότζεκτ κονσόλας, αναφέρετε το πακέτο NuGet Aspose.Pdf, και πατήστε **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace AsposePdfMultiWidget
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Add a blank page pdf
                var pdfPage = pdfDocument.Pages.Add();

                // Create a TextBox field that can contain multiple widgets
                var multiWidgetTextBox = new TextBoxField(
                    pdfPage,
                    new Rectangle(50, 700, 250, 730));
                multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
                multiWidgetTextBox.Value = "First widget";

                // Add the TextBox field to the form (first widget)
                pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);

                // Create and attach a second widget programmatically
                var secondWidget = new WidgetAnnotation(
                    new Rectangle(300, 700, 500, 730));
                multiWidgetTextBox.Widgets.Add(secondWidget);

                // Save the PDF with both widgets
                pdfDocument.Save("multiWidget.pdf");
            }
        }
    }
}
```

Εκτελέστε το πρόγραμμα και ανοίξτε το `multiWidget.pdf`. Θα δείτε δύο συγχρονισμένα πλαίσια κειμένου—ακριβώς αυτό που θέλατε όταν ρωτήσατε **how to create pdf form** με πολλαπλές καταχωρήσεις.

## Ανακεφαλαίωση & Επόμενα Βήματα

Μόλις περάσαμε από το πώς να **create pdf document**, να προσθέσουμε μια **blank page pdf**, να ορίσουμε ένα **create pdf form field**, και τελικά να απαντήσουμε **how to add textbox pdf** widgets που μοιράζονται δεδομένα. Η βασική ιδέα είναι ότι ένα μοναδικό όνομα πεδίου μπορεί να αποδοθεί πολλές φορές, προσφέροντάς σας ευέλικτες διατάξεις φόρμας χωρίς επιπλέον κώδικα.

Θέλετε να προχωρήσετε παραπέρα; Δοκιμάστε αυτές τις ιδέες:

- **Style the textbox** – αλλάξτε το χρώμα του περιγράμματος, το φόντο ή τη γραμματοσειρά χρησιμοποιώντας τις ιδιότητες `TextBoxField`.  
- **Add validation** – χρησιμοποιήστε ενέργειες JavaScript (`TextBoxField.Actions.OnValidate`) για την επιβολή μορφών.  
- **Combine with other fields** – προσθέστε checkboxes, radio buttons ή ψηφιακές υπογραφές για να δημιουργήσετε μια πλήρη φόρμα.  
- **Export form data** – καλέστε το `pdfDocument.Form.ExportFields()` για να εξάγετε τα δεδομένα εισόδου του χρήστη ως JSON ή XML.

Κάθε ένα από αυτά βασίζεται στην ίδια βάση που καλύψαμε, έτσι είστε καλά προετοιμασμένοι να δημιουργήσετε εξελιγμένες φόρμες PDF για τιμολόγια, συμβάσεις, έρευνες ή οποιαδήποτε άλλη επιχειρηματική ανάγκη.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω ή εξερευνήστε την τεκμηρίωση του Aspose.Pdf για πιο βαθιές πληροφορίες. Θυμηθείτε, ο καλύτερος τρόπος να κυριαρχήσετε στη δημιουργία PDF είναι η πειραματική δοκιμή—έτσι, τροποποιήστε τις συντεταγμένες, προσθέστε περισσότερα widgets, και δείτε τη φόρμα σας να ζωντανεύει.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}