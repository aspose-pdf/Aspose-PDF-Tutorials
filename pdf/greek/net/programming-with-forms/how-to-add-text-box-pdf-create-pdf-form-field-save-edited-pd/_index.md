---
category: general
date: 2026-02-20
description: Πώς να προσθέσετε πεδίο κειμένου PDF σε C# – μάθετε πώς να δημιουργήσετε
  πεδίο φόρμας PDF, να μετατρέψετε το Word σε φόρμα PDF και να αποθηκεύσετε γρήγορα
  το επεξεργασμένο έγγραφο PDF.
draft: false
keywords:
- how to add text box pdf
- create pdf form field
- convert word to pdf form
- save edited pdf document
language: el
og_description: Πώς να προσθέσετε πλαίσιο κειμένου σε PDF; Αυτό το σεμινάριο σας δείχνει
  πώς να δημιουργήσετε πεδία φόρμας PDF, να μετατρέψετε το Word σε φόρμα PDF και να
  αποθηκεύσετε επεξεργασμένα έγγραφα PDF χρησιμοποιώντας C#.
og_title: Πώς να προσθέσετε πλαίσιο κειμένου σε PDF – Πλήρης οδηγός για προγραμματιστές
  C#
tags:
- PDF
- C#
- Document Automation
title: Πώς να προσθέσετε πλαίσιο κειμένου σε PDF – Δημιουργία πεδίου φόρμας PDF &
  Αποθήκευση επεξεργασμένου εγγράφου PDF
url: /el/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/
---

πρώτη σελίδα του PDF")

Also the "*Alt text:* *How to add text box PDF – illustration of a text box placed on a PDF page.*" This is a caption. Translate.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Πλαίσιο Κειμένου PDF – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε πλαίσιο κειμένου PDF** χωρίς να ξοδεύετε ώρες με εργαλεία GUI; Δεν είστε μόνοι. Η μετατροπή ενός εγγράφου Word σε διαδραστική φόρμα PDF είναι κάτι που χρειάζονται πολλοί προγραμματιστές, ειδικά όταν δημιουργούν πύλες ενσωμάτωσης ή αυτόματους δημιουργούς αναφορών.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: δημιουργία πεδίου φόρμας PDF, μετατροπή ενός εγγράφου Word σε φόρμα PDF και, τέλος, **αποθήκευση του επεξεργασμένου εγγράφου PDF**. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET—χωρίς εξωτερικό UI.

## Τι Θα Μάθετε

- Φόρτωση αρχείου `.docx` και μετατροπή του σε αντικείμενο PDF.  
- **Δημιουργία αντικειμένων PDF form field** προγραμματιστικά, συμπεριλαμβανομένου ενός πλαισίου κειμένου.  
- Προσθήκη πολλαπλών widget (οπτικών αναπαραστάσεων) για το ίδιο πεδίο σε διαφορετικές σελίδες.  
- **Αποθήκευση του επεξεργασμένου εγγράφου PDF** στον δίσκο.  

Δεν απαιτείται καμία εξωτερική UI τρίτου μέρους· όλα γίνονται μέσω κώδικα, πράγμα που σημαίνει ότι μπορείτε να αυτοματοποιήσετε τη ροή εργασίας σε batch jobs, web services ή desktop εφαρμογές.

> **Pro tip:** Αν ήδη χρησιμοποιείτε τη βιβλιοθήκη Aspose.PDF for .NET (ο κώδικας παρακάτω υποθέτει αυτήν), θα έχετε ενσωματωμένη υποστήριξη για μετατροπή Word‑to‑PDF και διαχείριση φορμών χωρίς επιπλέον εξαρτήσεις.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| .NET 6.0 ή νεότερο (ή .NET Framework 4.7.2+) | Η βιβλιοθήκη που χρησιμοποιούμε στοχεύει σε σύγχρονες εκτελέσεις. |
| Aspose.PDF for .NET (NuGet `Aspose.PDF`) | Παρέχει `Document`, `FormField`, `TextBoxField`, κ.λπ. |
| Ένα δείγμα αρχείου Word (`input.docx`) | Αυτό είναι το πηγαίο αρχείο που θα μετατρέψουμε σε φόρμα PDF. |
| Βασικές γνώσεις C# | Θα καταλάβετε τα αποσπάσματα κώδικα χωρίς να χρειάζεται εκτενής εξήγηση. |

> **Note:** Οι ίδιες έννοιες ισχύουν για άλλες βιβλιοθήκες PDF (iTextSharp, PDFSharp). Αντικαταστήστε τις κλάσεις ανάλογα αν προτιμάτε διαφορετικό stack.

## Βήμα 1 – Φόρτωση του Εγγράφου Word και Μετατροπή σε PDF

Πρώτα χρειαζόμαστε ένα αντικείμενο `Document` που αντιπροσωπεύει την έκδοση PDF του αρχείου Word μας. Η Aspose.PDF μπορεί να διαβάσει `.docx` απευθείας, επομένως δεν υπάρχει ξεχωριστό βήμα μετατροπής.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;

// Load the Word document and automatically convert it to PDF
Document doc = new Document("YOUR_DIRECTORY/input.docx");

// Verify that the conversion succeeded
Console.WriteLine($"Document loaded with {doc.Pages.Count} page(s).");
```

**Γιατί είναι σημαντικό:** Η πρώιμη μετατροπή μας δίνει έναν καμβά PDF όπου μπορούμε να προσθέσουμε πεδία φόρμας. Επίσης εξασφαλίζει ότι οι διαστάσεις της σελίδας ταιριάζουν με το τελικό PDF, κάτι απαραίτητο για ακριβή τοποθέτηση του πλαισίου κειμένου.

## Βήμα 2 – Δημιουργία Πλαισίου Κειμένου Φόρμας στην Πρώτη Σελίδα

Τώρα θα προσθέσουμε ένα **text box PDF** στοιχείο που οι χρήστες μπορούν να συμπληρώσουν. Οι συντεταγμένες του ορθογωνίου εκφράζονται σε points (1/72 ίντσα). Σε αυτό το παράδειγμα το πλαίσιο βρίσκεται κοντά στην επάνω‑αριστερή γωνία της σελίδας 1.

```csharp
// Define the rectangle where the text box will appear (x‑min, y‑min, x‑max, y‑max)
Rectangle headerRect = new Rectangle(50, 750, 200, 770);

// Create the visual widget (TextBoxField) and give it a logical name
TextBoxField headerBox = new TextBoxField(doc.Pages[1], headerRect)
{
    PartialName = "Header" // This is the field’s internal identifier
};

// Add the widget to the document’s form collection and assign a field name
FormField headerField = doc.Form.Add(headerBox, "HeaderField");

// Optional: set default text or appearance properties
headerBox.Value = "Enter title here";
headerBox.Border = new Border(headerBox) { Width = 1, Color = Color.Black };
```

> **Γιατί χρησιμοποιούμε `PartialName` και ξεχωριστό όνομα πεδίου:** Το `PartialName` είναι το αναγνωριστικό που χρησιμοποιεί ο προβολέας PDF, ενώ το όνομα που περνάτε στο `Add` (`"HeaderField"`) είναι το κλειδί που θα αναφέρετε όταν εξάγετε δεδομένα αργότερα.

### Οπτική Υπόδειξη

![Πώς να προσθέσετε πλαίσιο κειμένου PDF](/images/add-textbox-pdf.png "Στιγμιότυπο οθόνης που δείχνει το πλαίσιο κειμένου τοποθετημένο στην πρώτη σελίδα του PDF")

*Alt text:* *Πώς να προσθέσετε πλαίσιο κειμένου PDF – εικονογράφηση ενός πλαισίου κειμένου τοποθετημένου σε σελίδα PDF.*

## Βήμα 3 – Προσθήκη Δεύτερου Widget για το Ίδιο Πεδίο στη Σελίδα 2

Τα πεδία φόρμας PDF μπορούν να έχουν πολλαπλές οπτικές αναπαραστάσεις (widgets). Αυτό είναι χρήσιμο όταν θέλετε το ίδιο σημείο εισαγωγής δεδομένων σε πολλές σελίδες—π.χ. μια κεφαλίδα που επαναλαμβάνεται.

```csharp
// Define a second rectangle on page 2 (different position)
Rectangle secondRect = new Rectangle(50, 50, 200, 70);

// Attach the same logical field to page 2
headerField.AddWidget(secondRect, doc.Pages[2]);
```

**Γιατί είναι χρήσιμο:** Οι χρήστες μπορούν να συμπληρώσουν το πεδίο μία φορά, και η τιμή εμφανίζεται αυτόματα σε κάθε widget. Μειώνει την επανάληψη και διατηρεί τη φόρμα τακτοποιημένη.

## Βήμα 4 – (Προαιρετικό) Μετατροπή Πρόσθετου Περιεχομένου Word σε Στοιχεία Φόρμας PDF

Αν το αρχικό αρχείο Word περιέχει άλλα placeholders (π.χ. `{{Name}}`), μπορείτε προγραμματιστικά να τα αντικαταστήσετε με πεδία φόρμας. Εδώ ένα γρήγορο μοτίβο:

```csharp
// Example: replace a placeholder text with a new text box field
foreach (Page page in doc.Pages)
{
    foreach (TextFragment fragment in page.TextFragments)
    {
        if (fragment.Text.Contains("{{Name}}"))
        {
            // Remove placeholder
            fragment.Text = fragment.Text.Replace("{{Name}}", string.Empty);

            // Create a new text box at the placeholder’s location
            Rectangle nameRect = fragment.Rectangle;
            TextBoxField nameBox = new TextBoxField(page, nameRect) { PartialName = "Name" };
            doc.Form.Add(nameBox, "NameField");
        }
    }
}
```

> **Edge case:** Κάποια PDF αποθηκεύουν το κείμενο ως ξεχωριστά τμήματα ανά χαρακτήρα, οπότε ίσως χρειαστεί να συγχωνεύσετε τα τμήματα ή να χρησιμοποιήσετε πιο ανθεκτικό αλγόριθμο αναζήτησης για πολύπλοκα έγγραφα.

## Βήμα 5 – Αποθήκευση του Επεξεργασμένου Εγγράφου PDF

Τέλος, γράψτε το τροποποιημένο PDF πίσω στον δίσκο. Μπορείτε να επιλέξετε οποιαδήποτε μορφή εξόδου υποστηρίζεται από τη βιβλιοθήκη (PDF, XPS, κ.λπ.). Εδώ παραμένουμε στο PDF.

```csharp
// Save the final PDF that now contains interactive text boxes
doc.Save("YOUR_DIRECTORY/output.pdf");

Console.WriteLine("PDF saved successfully at YOUR_DIRECTORY/output.pdf");
```

**Τι να ελέγξετε:** Ανοίξτε το `output.pdf` σε Adobe Acrobat Reader ή οποιονδήποτε προβολέα PDF που υποστηρίζει φόρμες. Θα πρέπει να δείτε δύο ταυτόσημα πλαίσια κειμένου—ένα στη σελίδα 1 και ένα στη σελίδα 2—και τα δύο είναι επεξεργάσιμα και συγχρονισμένα.

## Πλήρες Παράδειγμα Λειτουργικού Κώδικα

Παρακάτω είναι το ολοκληρωμένο, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή console. Περιλαμβάνει όλα τα παραπάνω βήματα μαζί με ελάχιστο χειρισμό σφαλμάτων.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load Word and convert to PDF
            Document doc = new Document("YOUR_DIRECTORY/input.docx");
            Console.WriteLine($"Loaded document with {doc.Pages.Count} page(s).");

            // 2️⃣ Create a text box on page 1
            Rectangle rect1 = new Rectangle(50, 750, 200, 770);
            TextBoxField txtBox = new TextBoxField(doc.Pages[1], rect1)
            {
                PartialName = "Header"
            };
            FormField headerField = doc.Form.Add(txtBox, "HeaderField");
            txtBox.Value = "Enter header";
            txtBox.Border = new Border(txtBox) { Width = 1, Color = Color.DarkGray };

            // 3️⃣ Add a second widget on page 2
            Rectangle rect2 = new Rectangle(50, 50, 200, 70);
            headerField.AddWidget(rect2, doc.Pages[2]);

            // 4️⃣ (Optional) Replace placeholders with fields – omitted for brevity

            // 5️⃣ Save the edited PDF
            string outputPath = "YOUR_DIRECTORY/output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved successfully at {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, το `output.pdf` περιέχει δύο συγχρονισμένα πλαίσια κειμένου με την ετικέτα “Header”. Κάθε κείμενο που εισάγεται σε ένα πλαίσιο εμφανίζεται αυτόματα και στο άλλο.

## Συχνές Ερωτήσεις & Edge Cases

| Ερώτηση | Απάντηση |
|----------|----------|
| *Μπορώ να προσθέσω πλαίσιο κειμένου σε υπάρχον PDF (χωρίς πηγή Word);* | Ναι—παραλείψτε το βήμα μετατροπής Word και φορτώστε απευθείας το PDF (`new Document("file.pdf")`). |
| *Τι γίνεται αν ο δείκτης σελίδας είναι εκτός εύρους;* | Η Aspose.PDF ρίχνει `IndexOutOfRangeException`. Ελέγχετε πάντα το `doc.Pages.Count` πριν προσπελάσετε `doc.Pages[n]`. |
| *Πρέπει να ορίσω την ιδιότητα `ReadOnly` του πεδίου;* | Μόνο αν θέλετε να αποτρέψετε την επεξεργασία. Ορίστε `txtBox.ReadOnly = true;`. |
| *Πώς εξάγω τα δεδομένα που εισήχθησαν αργότερα;* | Χρησιμοποιήστε `doc.Form["HeaderField"].Value` μετά την αποθήκευση της φόρμας από τον χρήστη. |
| *Το σύστημα συντεταγμένων έχει προέλευση στο κάτω‑αριστερό;* | Σωστά—(0,0) είναι η κάτω‑αριστερή γωνία της σελίδας. Προσαρμόστε τις τιμές Y αναλόγως. |

## Επόμενα Βήματα

Τώρα που ξέρετε **πώς να προσθέσετε πλαίσιο κειμένου PDF** προγραμματιστικά, μπορείτε να εξερευνήσετε:

- **Δημιουργία τύπων PDF form field** πέρα από τα πλαίσια κειμένου (checkboxes, radio buttons, drop‑downs).  
- **Μετατροπή Word σε PDF φόρμα** με πιο σύνθετο χειρισμό διάταξης (πίνακες, εικόνες).  
- **Αποθήκευση επεξεργασμένου PDF** σε υπηρεσία αποθήκευσης cloud (Azure Blob, AWS S3) για κατανεμημένες ροές εργασίας.  
- **Επικύρωση εισόδου φόρμας** στην πλευρά του server πριν από την επεξεργασία.  

Κάθε ένα από αυτά τα θέματα βασίζεται στο θεμέλιο που καλύψαμε εδώ, επιτρέποντάς σας να δημιουργήσετε πλήρως αυτοματοποιημένες λύσεις PDF.

---

*Καλή προγραμματιστική! Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω—ας τα λύσουμε μαζί.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}