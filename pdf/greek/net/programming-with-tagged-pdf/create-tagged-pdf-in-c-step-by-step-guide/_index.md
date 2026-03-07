---
category: general
date: 2026-03-06
description: Δημιουργήστε PDF με ετικέτες χρησιμοποιώντας το Aspose.Pdf σε C#. Μάθετε
  πώς να προσθέσετε εικόνα σε PDF, να ορίσετε τη θέση της εικόνας και να ετικετοποιήσετε
  το PDF για προσβασιμότητα.
draft: false
keywords:
- create tagged pdf
- add image to pdf
- set figure position
- how to tag pdf
- how to add image
language: el
og_description: Δημιουργήστε PDF με ετικέτες χρησιμοποιώντας το Aspose.Pdf. Αυτός
  ο οδηγός δείχνει πώς να προσθέσετε εικόνα σε PDF, να ορίσετε τη θέση της εικόνας
  και να ετικετοποιήσετε το PDF για προσβασιμότητα.
og_title: Δημιουργία PDF με ετικέτες σε C# – Πλήρης οδηγός
tags:
- Aspose.Pdf
- C#
- PDF Accessibility
title: Δημιουργία PDF με ετικέτες σε C# – Οδηγός βήμα‑βήμα
url: /el/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Tagged PDF σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **create tagged PDF** σε C# αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· η προσβασιμότητα είναι απαραίτητη αυτές τις μέρες, και ένα tagged PDF είναι η ραχοκοκαλιά ενός συμμορφωμένου εγγράφου. Σε αυτόν τον οδηγό θα περάσουμε από ένα πραγματικό παράδειγμα που **adds image to PDF**, ορίζει τη θέση του figure και δείχνει **how to tag PDF** χρησιμοποιώντας το Aspose.Pdf. Στο τέλος θα έχετε ένα πλήρως tagged PDF που μπορείτε να στείλετε σε οποιονδήποτε.

Θα καλύψουμε τα πάντα, από τη φόρτωση ενός υπάρχοντος αρχείου μέχρι την αποθήκευση του τελικού αποτελέσματος, ώστε να μην χρειάζεται να ψάχνετε για “how to add image” αλλού. Χωρίς περιττές πληροφορίες—μόνο μια σαφής, εκτελέσιμη λύση που λειτουργεί με το Aspose.Pdf 23.8 (η πιο πρόσφατη έκδοση τη στιγμή της συγγραφής). Πάρτε το IDE σας και ας ξεκινήσουμε.

---

## Τι Θα Χρειαστείτε

- **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`).  
- .NET 6+ (or .NET Framework 4.7.2+).  
- Ένα αρχείο PDF εισόδου που ήδη έχει λογική δομή (δηλαδή είναι ήδη tagged) – αν όχι, μπορείτε να ενεργοποιήσετε την ετικετοποίηση μέσω `pdfDocument.TaggedContent = true`.  
- Ένα αρχείο εικόνας (`image.png`) που θέλετε να ενσωματώσετε.  

Αυτό είναι όλο. Δεν χρειάζονται επιπλέον βιβλιοθήκες, ούτε περίπλοκα αρχεία ρυθμίσεων.

---

## Βήμα 1: Φόρτωση του Υπάρχοντος Εγγράφου PDF (Δημιουργία Βάσης Tagged PDF)

Το πρώτο που κάνουμε είναι να ανοίξουμε το PDF που θέλουμε να βελτιώσουμε. Η φόρτωση του αρχείου μας δίνει πρόσβαση στη λογική του δομή, η οποία είναι απαραίτητη για τις ροές εργασίας **create tagged pdf**.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.LogicalStructure;

// Load the source PDF – make sure the path points to a real file.
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Verify that the document has a tag tree; if not, enable it.
if (!pdfDocument.TaggedContent.IsTagged)
{
    pdfDocument.TaggedContent.IsTagged = true;
    Console.WriteLine("Tagging enabled on the document.");
}
```

*Γιατί είναι σημαντικό:* Χωρίς δέντρο ετικετών το PDF δεν θα μεταδίδει δομικές πληροφορίες σε προγράμματα ανάγνωσης οθόνης. Η ενεργοποίηση της ετικετοποίησης εξασφαλίζει ότι οποιαδήποτε νέα στοιχεία προσθέτουμε (όπως ένα figure) κληρονομούν τη σωστή ιεραρχία.

---

## Βήμα 2: Πρόσβαση στη Ρίζα της Λογικής Δομής (How to Tag PDF)

Τώρα προσεγγίζουμε τη λογική δομή του PDF. Το στοιχείο ρίζας είναι ο container για όλες τις ετικέτες—σκεφτείτε το ως το περίγραμμα του εγγράφου.

```csharp
// Grab the root of the logical structure.
var logicalRoot = pdfDocument.TaggedContent.RootElement;

// Optional: print existing children count for debugging.
Console.WriteLine($"Root has {logicalRoot.ChildElements.Count} child elements.");
```

*Εξήγηση:* Το `logicalRoot` μας επιτρέπει να προσθέσουμε νέες ετικέτες όπως `<Figure>` ή `<Table>`. Αυτό είναι ο πυρήνας του **how to tag PDF** προγραμματιστικά.

---

## Βήμα 3: Δημιουργία Ετικέτας Figure και Ορισμός Θέσης (Set Figure Position)

Μια ετικέτα *Figure* ομαδοποιεί οπτικό περιεχόμενο με προαιρετική λεζάντα. Θα δημιουργήσουμε μία, θα ορίσουμε τη θέση της και θα την επισυνάψουμε στη ρίζα.

```csharp
// Create a new Figure element.
var figureTag = logicalRoot.CreateFigureElement();

// Define where the figure appears on the page.
figureTag.Position = new Position
{
    // X/Y are measured from the bottom‑left corner (points).
    X = 100,   // 100 points from the left edge
    Y = 150,   // 150 points from the bottom edge
    Width = 300,
    Height = 200
};

// Append the Figure to the logical structure.
logicalRoot.AppendChild(figureTag);

Console.WriteLine("Figure tag created and positioned.");
```

*Γιατί ορίζουμε θέση:* Το βήμα **set figure position** καθορίζει πού θα τοποθετηθεί το οπτικό στοιχείο στη σελίδα. Αν το παραλείψετε, το figure μπορεί να εμφανιστεί σε απροσδόκητη θέση ή να είναι αόρατο για τις βοηθητικές τεχνολογίες.

---

## Βήμα 4: Προσθήκη Οπτικής Αναπαράστασης – Εισαγωγή Εικόνας (Add Image to PDF)

Με την ετικέτα στη θέση της, χρειαζόμαστε μια πραγματική εικόνα. Αυτό είναι το τμήμα που απαντά στο **add image to pdf**.

```csharp
// Grab the first page (pages are 1‑based in Aspose.Pdf).
var firstPage = pdfDocument.Pages[1];

// Create an Image object that points to the file stream.
var image = new Image
{
    ImageStream = File.OpenRead("YOUR_DIRECTORY/image.png"),
    // The rectangle defines the same area we set for the Figure.
    Rect = new Rectangle(100, 150, 400, 350) // X, Y, Width, Height
};

// Add the image to the page's paragraph collection.
firstPage.Paragraphs.Add(image);

Console.WriteLine("Image added to the first page.");
```

*Κύριο σημείο:* Οι συντεταγμένες του rectangle πρέπει να ταιριάζουν με το `figureTag.Position` που ορίσαμε νωρίτερα· διαφορετικά το figure και το οπτικό του περιεχόμενο θα είναι ασύγχρονα, διασπώντας την προσβασιμότητα.

---

## Βήμα 5: Αποθήκευση του Ενημερωμένου PDF (Ολοκλήρωση Δημιουργίας Tagged PDF)

Τέλος, αποθηκεύουμε τις αλλαγές σε νέο αρχείο. Η διατήρηση του αρχικού αμετάβλητου είναι καλή πρακτική.

```csharp
// Save the modified document.
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

Console.WriteLine("Tagged PDF saved as output.pdf");
```

Σε αυτό το στάδιο έχετε ένα αρχείο **create tagged pdf** που περιέχει μια σωστά τοποθετημένη εικόνα τυλιγμένη σε ετικέτα `<Figure>`. Ανοίξτε το `output.pdf` στο Adobe Acrobat και ελέγξτε το πάνελ *Tags* – θα πρέπει να δείτε έναν κόμβο `Figure` κάτω από τη ρίζα.

---

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Όλα τα βήματα είναι ήδη στη σωστή σειρά.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.LogicalStructure;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF.
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (!pdfDocument.TaggedContent.IsTagged)
            {
                pdfDocument.TaggedContent.IsTagged = true;
                Console.WriteLine("Tagging enabled.");
            }

            // 2️⃣ Access the logical structure root.
            var logicalRoot = pdfDocument.TaggedContent.RootElement;

            // 3️⃣ Create a Figure tag and set its position.
            var figureTag = logicalRoot.CreateFigureElement();
            figureTag.Position = new Position
            {
                X = 100,
                Y = 150,
                Width = 300,
                Height = 200
            };
            logicalRoot.AppendChild(figureTag);
            Console.WriteLine("Figure tag added.");

            // 4️⃣ Add the image to the first page.
            var firstPage = pdfDocument.Pages[1];
            var image = new Image
            {
                ImageStream = File.OpenRead("YOUR_DIRECTORY/image.png"),
                Rect = new Rectangle(100, 150, 400, 350)
            };
            firstPage.Paragraphs.Add(image);
            Console.WriteLine("Image inserted.");

            // 5️⃣ Save the result.
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved – tagging complete.");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- `output.pdf` ανοίγει με την εικόνα να εμφανίζεται στο (100, 150) points, με μέγεθος 300 × 200 points.  
- Το πάνελ *Tags* δείχνει ένα στοιχείο `Figure` που περιβάλλει την εικόνα.  
- Τα εργαλεία ανάγνωσης οθόνης αναγγέλλουν “Figure” πριν περιγράψουν την εικόνα, ικανοποιώντας τα βασικά πρότυπα προσβασιμότητας.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το PDF προέλευσης δεν είναι ήδη tagged;

Το Aspose.Pdf σας επιτρέπει να ενεργοποιήσετε την ετικετοποίηση ορίζοντας `pdfDocument.TaggedContent.IsTagged = true;`. Η βιβλιοθήκη θα δημιουργήσει ένα προεπιλεγμένο δέντρο ετικετών, μετά το οποίο μπορείτε να προσθέσετε προσαρμοσμένες ετικέτες όπως φαίνεται.

### Μπορώ να προσθέσω λεζάντα στο figure;

Ναι. Μετά τη δημιουργία του `figureTag`, μπορείτε να επισυνάψετε ένα `Paragraph` με ένα `TextFragment` και να ορίσετε το `Tag` του σε `Caption`. Παράδειγμα:

```csharp
var caption = new Paragraph(new TextFragment("Figure 1: Sample diagram"));
caption.Tag = figureTag.CreateCaptionElement();
logicalRoot.AppendChild(caption);
```

### Πώς τοποθετώ το figure σε διαφορετική σελίδα;

Αντικαταστήστε το `var firstPage = pdfDocument.Pages[1];` με τον επιθυμητό δείκτη σελίδας, π.χ., `pdfDocument.Pages[3]`. Θυμηθείτε να προσαρμόσετε τις συντεταγμένες `Position` αν το μέγεθος της σελίδας διαφέρει.

### Τι γίνεται αν χρειαστεί να ετικετοποιήσω πολλές εικόνες;

Δημιουργήστε ένα νέο `Figure` για κάθε εικόνα, δώστε σε κάθε ένα μοναδική `Position` και προσθέστε το αντίστοιχο αντικείμενο `Image` στη σωστή σελίδα. Η επανάληψη πάνω σε μια συλλογή εικόνων λειτουργεί καλά.

### Λειτουργεί αυτό με συμμόρφωση PDF/A;

Το Aspose.Pdf υποστηρίζει PDF/A‑1b, PDF/A‑2b και PDF/A‑3b. Κατά τη δημιουργία εγγράφου PDF/A, βεβαιωθείτε ότι έχετε ορίσει τη λειτουργία συμμόρφωσης πριν την αποθήκευση:

```csharp
pdfDocument.Convert(ConvertFormat.PdfA1b);
```

Η λογική ετικετοποίησης παραμένει η ίδια.

---

## Επαγγελματικές Συμβουλές & Πιθανά Προβλήματα

- **Pro tip:** Χρησιμοποιείτε πάντα απόλυτες διαδρομές ή `Path.Combine` για να αποφύγετε σφάλματα αρχείου‑δεν‑βρέθηκε κατά την εκτέλεση.  
- **Watch out for:** Ασυμφωνία συντεταγμένων μεταξύ της ετικέτας `Figure` και του rectangle `Image`—οι βοηθητικές τεχνολογίες βασίζονται σε αυτή τη στοίχιση.  
- **Performance note:** Αν επεξεργάζεστε πολλές σελίδες, τυλίξτε το stream της εικόνας σε ένα μπλοκ `using` για να ελευθερώσετε γρήγορα τους πόρους.  
- **Version check:** Το API που φαίνεται λειτουργεί με Aspose.Pdf 23.8+. Παλαιότερες εκδόσεις μπορεί να έχουν ελαφρώς διαφορετικά ονόματα κλάσεων (π.χ., `LogicalStructureElement` αντί για `FigureElement`).

---

## Συμπέρασμα

Μόλις **create tagged pdf** από την αρχή μέχρι το τέλος, παρουσιάσαμε **add image to pdf**, και δείξαμε πώς να **set figure position** ενώ απαντήσαμε στο **how to tag pdf** και **how to add image** σε ένα ενιαίο, συνεκτικό παράδειγμα. Ο κώδικας είναι έτοιμος για εκτέλεση, οι εξηγήσεις καλύπτουν το «γιατί» κάθε βήματος, και τώρα έχετε μια σταθερή βάση για τη δημιουργία προσβάσιμων PDF σε C#.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε πίνακες με ετικέτες `<Table>`, ή να ενσωματώσετε ένα επίπεδο συμμόρφωσης PDF/A‑2b για αρχειοθέτηση. Το ίδιο μοτίβο—φόρτωση, πρόσβαση στη λογική δομή, δημιουργία ετικέτας, προσθήκη οπτικού περιεχομένου, αποθήκευση—εφαρμόζεται σε πολλές εργασίες προσβασιμότητας PDF.

Αν αντιμετωπίσετε πρόβλημα ή έχετε μια περίπτωση χρήσης που δεν καλύπτεται εδώ, αφήστε ένα σχόλιο παρακάτω. Καλή ετικετοποίηση και απολαύστε τη δημιουργία PDF που μπορεί να διαβάσει όλοι!

![Διάγραμμα που δείχνει ένα PDF με ετικέτα Figure και εικόνα – απεικονίζει πώς να δημιουργήσετε tagged pdf](placeholder-image.png "παράδειγμα create tagged pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}