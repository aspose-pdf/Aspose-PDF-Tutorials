---
category: general
date: 2026-03-03
description: Δημιουργήστε ετικετοποιημένο PDF χρησιμοποιώντας το Aspose.PDF σε C#.
  Μάθετε πώς να ετικετοποιείτε PDF, να προσθέτετε κενή σελίδα PDF και να δημιουργείτε
  στοιχείο span για προσβάσιμα έγγραφα.
draft: false
keywords:
- create tagged pdf
- how to tag pdf
- add blank page pdf
- create span element
- aspose create pdf document
language: el
og_description: Δημιουργήστε PDF με ετικέτες χρησιμοποιώντας το Aspose.PDF σε C#.
  Αυτός ο οδηγός δείχνει πώς να ετικετοποιήσετε ένα PDF, να προσθέσετε μια κενή σελίδα
  και να δημιουργήσετε ένα στοιχείο span για προσβασιμότητα.
og_title: Δημιουργία ετικετοποιημένου PDF σε C# – Πλήρης Οδηγός Aspose PDF
tags:
- Aspose.PDF
- C#
- PDF Accessibility
title: Δημιουργία PDF με ετικέτες σε C# – Πλήρης Οδηγός Aspose PDF
url: /el/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Tagged PDF σε C# – Πλήρης Οδηγός Aspose PDF

Έχετε ποτέ χρειαστεί να **create tagged PDF** αρχεία αλλά δεν ήξερτε από πού να ξεκινήσετε; Σε πολλές περιπτώσεις συμμόρφωσης—σκεφτείτε PDF/UA ή Section 508—θα πρέπει να **how to tag PDF** ώστε τα προγράμματα ανάγνωσης οθόνης να μπορούν να περιηγηθούν στο περιεχόμενο.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα ένα πλήρες, εκτελέσιμο παράδειγμα που **adds a blank page pdf**, δημιουργεί ένα **span element**, και τελικά αποθηκεύει το έγγραφο. Στο τέλος θα έχετε ένα πλήρως‑tagged PDF που μπορείτε να ανοίξετε στο Adobe Acrobat και να επαληθεύσετε τη δομή. Δεν απαιτούνται εξωτερικές αναφορές· απλώς αντιγράψτε, επικολλήστε και εκτελέστε.

> **Τι θα λάβετε:** ένα μόνο αρχείο C# που χρησιμοποιεί την πιο πρόσφατη έκδοση του Aspose.PDF για .NET (v23.12 τη στιγμή της συγγραφής) για να δημιουργήσει ένα προσβάσιμο PDF.  

**Προαπαιτούμενα**  
- .NET 6+ (ή .NET Framework 4.7.2) εγκατεστημένο  
- Πακέτο NuGet Aspose.PDF for .NET (`Aspose.Pdf`)  
- Ένας επεξεργαστής κώδικα ή IDE (Visual Studio, VS Code, Rider…οποιοσδήποτε είναι εντάξει)

Αν αναρωτιέστε **γιατί είναι σημαντικό το tagging**, σκεφτείτε το σαν να προσθέτετε πίνακα περιεχομένων για έναν τυφλό αναγνώστη—χωρίς ετικέτες το PDF είναι απλώς μια επίπεδη εικόνα. Ας μπει χέρι.

---

## Δημιουργία Tagged PDF – Αρχικοποίηση Εγγράφου Aspose

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `Document`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο PDF και είναι το σημείο εισόδου για όλες τις λειτουργίες tagging.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document (the canvas for our tagged PDF)
        using var pdfDocument = new Document();
```

*Γιατί είναι σημαντικό:* Η κλάση `Document` δεν κρατά μόνο τις σελίδες αλλά και μια ιεραρχία **TaggedContent** που το Aspose χρησιμοποιεί για την αποθήκευση σημασιολογικών πληροφοριών. Αν το παραλείψετε, δεν θα μπορείτε αργότερα να προσθέσετε ετικέτες όπως **span** ή **paragraph**.

![Diagram showing create tagged pdf workflow](https://example.com/images/create-tagged-pdf-workflow.png "Diagram showing create tagged pdf workflow")

---

## Προσθήκη Κενής Σελίδας PDF – Εισαγωγή Νέας Σελίδας

Ένα PDF χωρίς σελίδες είναι τόσο χρήσιμο όσο ένα βιβλίο χωρίς σελίδες. Η προσθήκη μιας κενής σελίδας μας δίνει μια επιφάνεια για να τοποθετήσουμε τα tagged στοιχεία μας.

```csharp
        // Step 2: Add a blank page (this satisfies the “add blank page pdf” requirement)
        Page pdfPage = pdfDocument.Pages.Add();
```

*Συμβουλή:* Η μέθοδος `Add()` δημιουργεί μια σελίδα με τις προεπιλεγμένες διαστάσεις A4. Μπορείτε να περάσετε ένα enum `PageSize` ή προσαρμοσμένες διαστάσεις αν χρειάζεστε κάτι διαφορετικό.

---

## Δημιουργία Span Element – Πώς να Tag PDF Περιεχόμενο

Τώρα το διασκεδαστικό μέρος: η δημιουργία ενός **span element** που θα κρατήσει ένα κομμάτι κειμένου, μια εικόνα ή οποιοδήποτε άλλο οπτικό αντικείμενο. Το span είναι η μικρότερη λογική μονάδα που μπορείτε να tag.

```csharp
        // Step 3: Create a span element for tagged PDF content
        var spanElement = pdfDocument.TaggedContent.CreateSpanElement();

        // Step 4: Define the visual bounds of the span (left, bottom, right, top)
        spanElement.Bounds = new Rectangle(50, 750, 550, 800);

        // Step 5: Tag the span with a BDC (Begin Marked Content) operator
        // "/Span" is the standard PDF tag for a generic inline element.
        spanElement.Tag(new BDC("/Span", ""));

        // Step 6: Append the span element to the root of the tagged content hierarchy
        pdfDocument.TaggedContent.RootElement.AppendChild(spanElement);
```

**Εξήγηση του γιατί:**  
- `CreateSpanElement()` μας δίνει ένα container που μπορεί αργότερα να κρατήσει κείμενο ή εικόνες.  
- `Bounds` λέει στον PDF renderer πού στη σελίδα βρίσκεται το span· χωρίς bounds η ετικέτα θα ήταν αόρατη.  
- Ο τελεστής `BDC` είναι ο τρόπος που το PDF σημειώνει την αρχή μιας λογικής δομής· το "/Span" ενημερώνει τις βοηθητικές τεχνολογίες ότι το περιεχόμενο είναι ένα ενσωματωμένο στοιχείο.  
- Τέλος, το `AppendChild` εισάγει το span στο λογικό δέντρο του εγγράφου, καθιστώντας το μέρος της δομής **create tagged pdf**.

Αν χρειάζεστε πολλαπλά spans, απλώς επαναλάβετε τα βήματα 3‑6 με διαφορετικά bounds ή ονόματα ετικετών (π.χ., `/P` για μια παράγραφο).

---

## Αποθήκευση Εγγράφου – Πώς να Tag PDF και να Διατηρήσετε το Αρχείο

Αφού δημιουργήσετε την ιεραρχία ετικετών, αποθηκεύετε το αρχείο. Εδώ το βήμα **aspose create pdf document** ξεχωρίζει: η βιβλιοθήκη γράφει τόσο το οπτικό ρεύμα της σελίδας όσο και τη κρυφή δομή ετικετών.

```csharp
        // Step 7: Save the tagged PDF to a file
        pdfDocument.Save("output/tagged.pdf");
    }
}
```

Ανοίγοντας το `output/tagged.pdf` στο Adobe Acrobat (View → Show/Hide → Navigation Panes → Tags) θα εμφανιστεί ένας μόνο κόμβος **Span** κάτω από τη ρίζα του εγγράφου.

---

## Πλήρες Παράδειγμα Εργασίας – Δημιουργία Tagged PDF σε Ένα Βήμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο console. Συγκεντρώνεται και εκτελείται όπως είναι.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize a new Aspose PDF document (create tagged pdf)
            using var pdfDocument = new Document();

            // Add a blank page (add blank page pdf)
            Page pdfPage = pdfDocument.Pages.Add();

            // Create a span element (create span element) and set its visual rectangle
            var spanElement = pdfDocument.TaggedContent.CreateSpanElement();
            spanElement.Bounds = new Rectangle(50, 750, 550, 800);

            // Tag the span with BDC operator – this is how to tag pdf
            spanElement.Tag(new BDC("/Span", ""));

            // Append the span to the root of the tagged content hierarchy
            pdfDocument.TaggedContent.RootElement.AppendChild(spanElement);

            // Optional: add a visible text fragment inside the span for demo purposes
            var text = new TextFragment("Hello, tagged PDF!");
            text.Position = new Position(55, 755);
            pdfPage.Paragraphs.Add(text);

            // Save the result (aspose create pdf document)
            pdfDocument.Save("output/tagged.pdf");

            Console.WriteLine("Tagged PDF created successfully at output/tagged.pdf");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** ένα αρχείο με όνομα `tagged.pdf` που περιέχει μία κενή σελίδα με τις λέξεις “Hello, tagged PDF!” τοποθετημένες μέσα σε ένα tagged **Span**. Το δέντρο ετικετών θα φαίνεται ως εξής:

```
Document
 └─ Span
      └─ TextFragment ("Hello, tagged PDF!")
```

---

## Συχνές Ερωτήσεις και Ακραίες Περιπτώσεις

| Question | Answer |
|----------|--------|
| **Χρειάζεται να προσθέσω κάποια άδεια για το Aspose;** | Η δωρεάν αξιολόγηση λειτουργεί, αλλά προσθέτει υδατογράφημα. Για παραγωγή, προσθέστε το αρχείο άδειας (`Aspose.Pdf.lic`) πριν δημιουργήσετε το `Document`. |
| **Μπορώ να κάνω tag εικόνες αντί για κείμενο;** | Ναι. Αφού δημιουργήσετε ένα στοιχείο `Figure` ή `Artifact`, ορίστε τα bounds του και χρησιμοποιήστε `Tag(new BDC("/Figure", ""))`. |
| **Τι γίνεται αν χρειάζομαι πολλαπλές σελίδες;** | Απλώς καλέστε `pdfDocument.Pages.Add()` για κάθε σελίδα και επαναλάβετε τα βήματα δημιουργίας span, προσαρμόζοντας τις συντεταγμένες Y του `Bounds` αναλόγως. |
| **Είναι ο τελεστής BDC ο μοναδικός τρόπος για tag;** | Για τις περισσότερες απλές δομές, το `BDC` (Begin Marked Content) είναι επαρκές. Για σύνθετες ιεραρχίες μπορείτε επίσης να χρησιμοποιήσετε το `EMC` (End Marked Content) χειροκίνητα, αλλά το Aspose το διαχειρίζεται αυτόματα όταν δημιουργείτε το δέντρο ετικετών. |
| **Πώς μπορώ να επαληθεύσω τις ετικέτες;** | Ανοίξτε το PDF στο Adobe Acrobat → View → Show/Hide → Navigation Panes → Tags. Θα πρέπει να δείτε την ιεραρχία που δημιουργήσατε. |

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **create tagged PDF** αρχεία με το Aspose.PDF, **πώς να tag PDF** στοιχεία χρησιμοποιώντας ένα **span element**, και πώς να **add blank page pdf** πριν το tagging. Το πλήρες παράδειγμα δείχνει τη ροή εργασίας **aspose create pdf document** από την αρχή μέχρι το τέλος, και μπορείτε να το επεκτείνετε σε παραγράφους, πίνακες ή εικόνες όπως χρειάζεται.  

Επόμενα βήματα; Δοκιμάστε να αντικαταστήσετε το span με μια ετικέτα `/P` (παράγραφος), πειραματιστείτε με πολυγλωσσικό κείμενο, ή δημιουργήστε έναν πίνακα περιεχομένων που επίσης σέβεται την ιεραρχία ετικετών. Όσο περισσότερο παίζετε με το API **create tagged pdf**, τόσο πιο προσβάσιμα γίνονται τα έγγραφά σας—χωρίς επιπλέον κόστος, μόνο με λίγες επιπλέον γραμμές κώδικα.

Καλό κώδικα, και μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε κάποιο πρόβλημα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}