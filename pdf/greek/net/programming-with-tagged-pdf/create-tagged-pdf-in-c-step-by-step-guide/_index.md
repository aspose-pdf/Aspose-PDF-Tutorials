---
category: general
date: 2026-02-12
description: Δημιουργήστε PDF με ετικέτες χρησιμοποιώντας το Aspose.Pdf σε C#. Μάθετε
  πώς να προσθέσετε παράγραφο σε PDF, να προσθέσετε ετικέτα παραγράφου, να προσθέσετε
  κείμενο στην παράγραφο και να δημιουργήσετε ένα προσβάσιμο PDF.
draft: false
keywords:
- create tagged pdf
- add paragraph to pdf
- add paragraph tag
- add text to paragraph
- create accessible pdf
language: el
og_description: Δημιουργία ετικετοποιημένου PDF σε C# με το Aspose.Pdf. Αυτό το σεμινάριο
  δείχνει πώς να προσθέσετε παράγραφο σε PDF, να ορίσετε ετικέτες και να δημιουργήσετε
  ένα προσβάσιμο PDF.
og_title: Δημιουργία PDF με ετικέτες σε C# – Πλήρης Οδηγός Προγραμματισμού
tags:
- Aspose.Pdf
- C#
- PDF accessibility
title: Δημιουργία PDF με ετικέτες σε C# – Οδηγός βήμα‑βήμα
url: /el/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Tagged PDF σε C# – Οδηγός Βήμα‑βήμα

Αν χρειάζεστε να **create tagged PDF** γρήγορα, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Αντιμετωπίζετε δυσκολίες με την προσθήκη μιας παραγράφου σε PDF ενώ διατηρείτε το έγγραφο προσβάσιμο; Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε μέρος είναι σημαντικό, και θα καταλήξουμε με ένα έτοιμο‑για‑εκτέλεση παράδειγμα που μπορείτε να ενσωματώσετε στο έργο σας.

Σε αυτό το tutorial θα μάθετε πώς να **add paragraph to PDF**, να επισυνάψετε ένα κατάλληλο **paragraph tag**, να εισάγετε **text to paragraph**, και τελικά να **create accessible PDF** αρχεία που περνούν ελέγχους αναγνώστη οθόνης. Δεν απαιτείται επιπλέον PDF‑tooling—μόνο Aspose.Pdf for .NET και μερικές γραμμές C#.

## Τι Θα Χρειαστεί

- .NET 6.0 ή νεότερο (το API λειτουργεί το ίδιο στο .NET Framework 4.6+)
- Aspose.Pdf for .NET (πακέτο NuGet `Aspose.Pdf`)
- Ένα βασικό IDE C# (Visual Studio, Rider ή VS Code)

Αυτό είναι όλο. Χωρίς εξωτερικά βοηθήματα, χωρίς ασαφή αρχεία ρυθμίσεων. Ας βουτήξουμε.

![Στιγμιότυπο οθόνης ενός tagged PDF εγγράφου που εμφανίζει το κείμενο της παραγράφου](/images/create-tagged-pdf.png "παράδειγμα δημιουργίας tagged pdf")

*(Κείμενο alt εικόνας: “παράδειγμα δημιουργίας tagged pdf που εμφανίζει μια παράγραφο με το σωστό tag”)*

## Πώς να δημιουργήσετε Tagged PDF – Βασικές Έννοιες

Πριν ξεκινήσουμε τον κώδικα, αξίζει να κατανοήσουμε *γιατί* η σήμανση είναι σημαντική. PDF/UA (Universal Accessibility) απαιτεί ένα λογικό δέντρο δομής ώστε οι βοηθητικές τεχνολογίες να μπορούν να διαβάσουν το έγγραφο με τη σωστή σειρά. Δημιουργώντας ένα **paragraph tag** και τοποθετώντας **text to paragraph**, δίνετε στους αναγνώστες οθόνης ένα σαφές σήμα ότι το περιεχόμενο είναι μια παράγραφος, όχι απλώς μια τυχαία σειρά χαρακτήρων.

### Βήμα 1: Ρυθμίστε το Project και Εισάγετε Namespaces

Δημιουργήστε μια νέα εφαρμογή console (ή ενσωματώστε την σε υπάρχουσα) και προσθέστε την αναφορά Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the code lives here
        }
    }
}
```

> **Pro tip:** Αν χρησιμοποιείτε .NET 6 top‑level statements, μπορείτε να παραλείψετε εντελώς την κλάση `Program`—απλώς τοποθετήστε τον κώδικα απευθείας στο αρχείο. Η λογική παραμένει η ίδια.

### Βήμα 2: Δημιουργήστε ένα Νέο PDF Έγγραφο

Ξεκινάμε με ένα κενό `Document`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο PDF, συμπεριλαμβανομένου του εσωτερικού δέντρου δομής.

```csharp
// Step 2: Create a new PDF document (the canvas)
using (var pdfDocument = new Document())
{
    // All subsequent operations happen inside this block
}
```

Η δήλωση `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται αυτόματα, κάτι που είναι ιδιαίτερα χρήσιμο όταν εκτελείτε τη demo πολλές φορές.

### Βήμα 3: Πρόσβαση στη Δομή Tagged Content

Ένα tagged PDF έχει ένα *structure tree* που βρίσκεται κάτω από το `TaggedContent`. Πιέζοντας το, μπορούμε να αρχίσουμε να δημιουργούμε λογικά στοιχεία όπως παραγράφους.

```csharp
// Step 3: Get the tagged content object
var taggedContent = pdfDocument.TaggedContent;
```

Αν παραλείψετε αυτό το βήμα, οποιοδήποτε κείμενο προσθέσετε αργότερα θα είναι **unstructured**, πράγμα που σημαίνει ότι η βοηθητική τεχνολογία θα το διαβάσει ως μια επίπεδη αλφαριθμητική σειρά.

### Βήμα 4: Δημιουργήστε ένα Στοιχείο Paragraph και Ορίστε τη Θέση του

Τώρα προσθέτουμε πραγματικά **add paragraph to PDF**. Ένα στοιχείο paragraph είναι ένας container που μπορεί να περιέχει ένα ή περισσότερα τμήματα κειμένου.

```csharp
// Step 4: Create a paragraph element
var paragraph = taggedContent.CreateParagraphElement();

// Define where the paragraph appears on the page (in points)
paragraph.Bounds = new Rectangle(0, 700, 500, 720);
```

Το `Rectangle` χρησιμοποιεί το σύστημα συντεταγμένων PDF όπου (0,0) είναι η κάτω‑αριστερή γωνία. Προσαρμόστε τις συντεταγμένες Y αν χρειάζεστε την παράγραφο πιο ψηλά ή πιο χαμηλά στη σελίδα.

### Βήμα 5: Εισάγετε Κείμενο στην Paragraph

Εδώ είναι το μέρος όπου **add text to paragraph**. Η ιδιότητα `Text` είναι ένας wrapper ευκολίας που δημιουργεί εσωτερικά ένα μοναδικό `TextFragment`.

```csharp
// Step 5: Set the visible text of the paragraph
paragraph.Text = "Chapter 1 – Introduction";
```

Αν χρειάζεστε πιο πλούσια μορφοποίηση (γραμματοσειρές, χρώματα, συνδέσμους), μπορείτε να δημιουργήσετε ένα `TextFragment` χειροκίνητα και να το προσθέσετε στο `paragraph.Segments`.

### Βήμα 6: Συνδέστε την Paragraph στο Structure Tree

Το structure tree χρειάζεται ένα *root element* για να κρεμάσει τα παιδικά στοιχεία. Προσθέτοντας την paragraph, προσθέτουμε αποτελεσματικά **add paragraph tag** στο PDF.

```csharp
// Step 6: Append the paragraph to the root element of the structure tree
taggedContent.RootElement.AppendChild(paragraph);
```

Σε αυτό το σημείο το PDF έχει έναν λογικό κόμβο paragraph που δείχνει στο οπτικό κείμενο που μόλις τοποθετήσαμε.

### Βήμα 7: Αποθηκεύστε το Έγγραφο ως Accessible PDF

Τέλος, γράφουμε το αρχείο στο δίσκο. Το αποτέλεσμα θα είναι ένα πλήρως **create accessible pdf** έτοιμο για δοκιμές αναγνώστη οθόνης.

```csharp
// Step 7: Save the tagged PDF to a file
pdfDocument.Save("tagged.pdf");
```

Μπορείτε να ανοίξετε το `tagged.pdf` στο Adobe Acrobat και να ελέγξετε *File → Properties → Tags* για να επαληθεύσετε τη δομή.

### Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1‑7: Create a tagged PDF with a single paragraph
            using (var pdfDocument = new Document())
            {
                // Access tagged content
                var taggedContent = pdfDocument.TaggedContent;

                // Create paragraph element
                var paragraph = taggedContent.CreateParagraphElement();

                // Position the paragraph on the first page
                paragraph.Bounds = new Rectangle(0, 700, 500, 720);

                // Add visible text
                paragraph.Text = "Chapter 1 – Introduction";

                // Append paragraph to the root of the structure tree
                taggedContent.RootElement.AppendChild(paragraph);

                // Save the result
                pdfDocument.Save("tagged.pdf");
            }

            Console.WriteLine("Tagged PDF created successfully at: tagged.pdf");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, ένα αρχείο με όνομα `tagged.pdf` εμφανίζεται στον φάκελο εργασίας του εκτελέσιμου. Ανοίγοντάς το στο Adobe Acrobat εμφανίζει το κείμενο “Chapter 1 – Introduction” τοποθετημένο κοντά στην κορυφή της σελίδας, και ο πίνακας *Tags* εμφανίζει ένα μόνο στοιχείο `<P>` (paragraph) συνδεδεμένο με αυτό το κείμενο.

## Προσθήκη Περισσότερου Περιεχομένου – Συνηθισμένες Παραλλαγές

### Πολλαπλές Paragraphs

Αν χρειάζεστε να **add paragraph to PDF** περισσότερες από μία φορές, απλώς επαναλάβετε τα Βήματα 4‑6 με νέες περιοριστικές τιμές και κείμενο. Θυμηθείτε να μειώνετε τη συντεταγμένη Y ώστε οι παράγραφοι να μην επικαλύπτονται.

```csharp
var secondParagraph = taggedContent.CreateParagraphElement();
secondParagraph.Bounds = new Rectangle(0, 660, 500, 680);
secondParagraph.Text = "This is the second paragraph.";
taggedContent.RootElement.AppendChild(secondParagraph);
```

### Μορφοποίηση Κειμένου

Για πιο πλούσια μορφοποίηση, δημιουργήστε ένα `TextFragment` και προσθέστε το στη συλλογή `Segments` της paragraph:

```csharp
var tf = new TextFragment("Bold heading")
{
    TextState = { FontSize = 14, FontStyle = FontStyles.Bold }
};
paragraph.Segments.Add(tf);
```

### Διαχείριση Σελίδων

Το παράδειγμα δημιουργεί αυτόματα ένα PDF μιας σελίδας. Αν χρειάζεστε περισσότερες σελίδες, προσθέστε τις μέσω `pdfDocument.Pages.Add()` και ορίστε το `paragraph.Bounds` στη σωστή σελίδα χρησιμοποιώντας `paragraph.PageNumber = 2;`.

## Δοκιμή Προσβασιμότητας

Ένας γρήγορος τρόπος για να επαληθεύσετε ότι πραγματικά **create accessible pdf** είναι:

1. Ανοίξτε το αρχείο στο Adobe Acrobat Pro.
2. Επιλέξτε *View → Tools → Accessibility → Full Check*.
3. Ανασκοπήστε το δέντρο *Tags*· κάθε παράγραφος πρέπει να εμφανίζεται ως κόμβος `<P>`.

Αν ο έλεγχος επισημάνει ελλιπή tags, ελέγξτε ξανά ότι κάλεσατε `taggedContent.RootElement.AppendChild(paragraph);` για κάθε στοιχείο που δημιουργείτε.

## Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

- **Ξεχάσατε να ενεργοποιήσετε τη σήμανση:** Η απλή δημιουργία ενός `Document` **δεν** προσθέτει δέντρο δομής. Πάντα προσπελάστε το `TaggedContent` πριν προσθέσετε στοιχεία.
- **Περιορισμοί εκτός ορίων σελίδας:** Το rectangle πρέπει να χωράει στο μέγεθος της σελίδας (προεπιλογή A4 ≈ 595 × 842 points). Τα rectangles εκτός ορίων αγνοούνται σιωπηρά.
- **Αποθήκευση πριν από την προσθήκη:** Αν καλέσετε `Save` πριν από `AppendChild`, το PDF θα είναι χωρίς σήμανση.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create tagged PDF** χρησιμοποιώντας Aspose.Pdf for .NET, πώς να **add paragraph to PDF**, να επισυνάψετε το κατάλληλο **paragraph tag**, και να εισάγετε **text to paragraph** ώστε το τελικό αρχείο να είναι ένα **create accessible pdf** έτοιμο για δοκιμές συμμόρφωσης. Το πλήρες δείγμα κώδικα παραπάνω μπορεί να αντιγραφεί σε οποιοδήποτε έργο C# και να εκτελεστεί χωρίς τροποποίηση.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με πίνακες, εικόνες ή προσαρμοσμένα heading tags για να δημιουργήσετε μια πλήρως δομημένη αναφορά. Ή εξερευνήστε το *PdfConverter* της Aspose για να μετατρέψετε υπάρχοντα PDFs σε tagged εκδόσεις αυτόματα.

Καλό κώδικα, και εύχομαι τα PDFs σας να είναι τόσο όμορφα **και** προσβάσιμα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}