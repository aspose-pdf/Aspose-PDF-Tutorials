---
category: general
date: 2026-06-21
description: Σχεδιάστε ορθογώνιο σε PDF χρησιμοποιώντας C#. Μάθετε πώς να φορτώνετε
  ένα έγγραφο PDF, να δημιουργείτε μαύρη σημείωση ορθογωνίου και να αποθηκεύετε αποδοτικά
  το τροποποιημένο PDF.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: el
og_description: Σχεδιάστε ένα ορθογώνιο σε PDF με C# φορτώνοντας ένα έγγραφο PDF,
  δημιουργώντας μια μαύρη σημείωση ορθογωνίου και αποθηκεύοντας το τροποποιημένο PDF.
  Περιλαμβάνεται πλήρης κώδικας.
og_title: Σχεδίαση ορθογωνίου σε PDF με C# – Πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Σχεδίαση ορθογωνίου σε PDF με C# – Οδηγός βήμα‑βήμα
url: /el/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Σχεδίαση Ορθογωνίου σε PDF με C# – Πλήρες Εγχειρίδιο Προγραμματισμού

Κάποτε χρειάστηκε να **σχεδιάσετε ορθογώνιο σε PDF** αρχεία από μια εφαρμογή .NET αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος. Είτε πρόκειται για επισήμανση τμήματος, διαγραφή ευαίσθητων δεδομένων, είτε απλώς για προσθήκη οπτικού σήματος, η εκμάθηση του πώς να *σχεδιάσετε ορθογώνιο σε PDF* προγραμματιστικά μπορεί να σας εξοικονομήσει ώρες χειροκίνητης επεξεργασίας.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πρακτικό παράδειγμα που **φορτώνει ένα PDF έγγραφο**, **δημιουργεί ένα μαύρο ορθογώνιο**, και στη συνέχεια **αποθηκεύει το τροποποιημένο PDF**. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#—χωρίς μυστήριο, μόνο καθαρός κώδικας και εξηγήσεις.

## Τι Καλύπτει Αυτό το Εγχειρίδιο

- Πώς να **φορτώσετε pdf έγγραφο** χρησιμοποιώντας τη βιβλιοθήκη Aspose.PDF for .NET  
- Ορισμός των συντεταγμένων ενός ορθογωνίου και διασφάλιση ότι παραμένει εντός των ορίων της σελίδας  
- Χρήση της μεθόδου **add black rectangle** για την επισήμανση της σελίδας  
- **Αποθήκευση τροποποιημένου pdf** σε νέα τοποθεσία αρχείου  
- Διαχείριση edge‑case (πολλές σελίδες, ορθογώνια εκτός ορίων, προσαρμοσμένα χρώματα)  

Καμία εξωτερική εργαλειοθήκη, καμία ασαφής αναφορά—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

---

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

1. .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένο  
2. Αναφορά στη **Aspose.PDF for .NET** (διαθέσιμη μέσω NuGet: `Install-Package Aspose.PDF`)  
3. Ένα υπάρχον PDF αρχείο (`input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να διαβάσετε/γράψετε  

Αυτό είναι όλο. Αν είστε άνετοι με τη βασική σύνταξη C#, είστε έτοιμοι να προχωρήσετε.

---

## Βήμα 1: Φόρτωση PDF Εγγράφου

Το πρώτο που χρειάζεται είναι μια κλήση **load pdf document**. Η κλάση `Document` της Aspose.PDF παίρνει τη διαδρομή του αρχείου και διαβάζει ολόκληρο το αρχείο στη μνήμη.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του PDF σας δίνει πρόσβαση στις σελίδες, τα μεταδεδομένα και την επιφάνεια σχεδίασης. Χωρίς αυτό το βήμα δεν μπορείτε να τοποθετήσετε κανένα σχήμα.

---

## Βήμα 2: Επιλογή της Στόχου Σελίδας

Οι σελίδες PDF είναι 1‑based στην Aspose, επομένως η πρώτη σελίδα έχει δείκτη 1. Πάρτε τη σελίδα που θέλετε να επισυνάψετε—συνήθως η πρώτη για μια γρήγορη επίδειξη.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

Αν χρειάζεται να εργαστείτε σε διαφορετική σελίδα, απλώς αλλάξτε τον δείκτη. Θυμηθείτε να ελέγξετε ότι ο δείκτης υπάρχει για να αποφύγετε `ArgumentOutOfRangeException`.

---

## Βήμα 3: Ορισμός Γεωμετρίας του Ορθογωνίου

Ένα ορθογώνιο ορίζεται από τις κάτω‑αριστερές (X,Y) και άνω‑δεξιές (X,Y) συντεταγμένες. Η δομή `Rectangle` αποθηκεύει αυτές ως `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Αλλάξτε ελεύθερα αυτούς τους αριθμούς—`100,100` τοποθετεί την κάτω‑αριστερή γωνία 100 μονάδες από τα αριστερά και το κάτω άκρο, ενώ `300,300` θέτει την άνω‑δεξιά γωνία 300 μονάδες από τις άκρες.

---

## Βήμα 4: Επαλήθευση ότι το Ορθογώνιο Περικλείεται στη Σελίδα

Η προσπάθεια σχεδίασης εκτός των ορίων της σελίδας είτε αγνοείται είτε προκαλεί εξαίρεση, ανάλογα με την έκδοση της βιβλιοθήκης. Μια γρήγορη επαλήθευση κρατά τον κώδικά σας ανθεκτικό.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Pro tip*: Αν σκοπεύετε να υποστηρίξετε PDFs διαφορετικών μεγεθών, μπορείτε να υπολογίσετε το ορθογώνιο βάσει ποσοστού του πλάτους/ύψους της σελίδας αντί για απόλυτες μονάδες.

---

## Βήμα 5: Προσθήκη Μαύρης Σχόλιας Ορθογωνίου

Τώρα το διασκεδαστικό μέρος—**add black rectangle** στη σελίδα. Η Aspose παρέχει τη μέθοδο `AddRectangle` που δέχεται τη γεωμετρία και ένα `Color`. Θα χρησιμοποιήσουμε το `Color.Black` για **create black rectangle**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

Αυτή η μία γραμμή κάνει το βάρος: δημιουργεί ένα αντικείμενο σχολίου, ορίζει το χρώμα περιγράμματος σε μαύρο, και το εισάγει στη συλλογή σχολίων της σελίδας.

Αν χρειαστείτε διαφορετικό γέμισμα ή στυλ περιγράμματος, εξερευνήστε την υπερφόρτωση που δέχεται ένα αντικείμενο `Annotation` όπου μπορείτε να ρυθμίσετε το πάχος γραμμής, το μοτίβο παύλας ή ακόμη και την αδιαφάνεια.

---

## Βήμα 6: Αποθήκευση Τροποποιημένου PDF

Τέλος, αποθηκεύστε τις αλλαγές με **save modified pdf**. Μπορείτε να αντικαταστήσετε το αρχικό ή να γράψετε σε νέο αρχείο—εδώ θα δημιουργήσουμε ένα αρχείο εξόδου.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

Αυτή είναι η πλήρης ροή εργασίας. Εκτελέστε το πρόγραμμα και ανοίξτε το `output.pdf`; θα πρέπει να δείτε ένα συμπαγές μαύρο ορθογώνιο όπου το ορίσατε.

---

## Πλήρες Παράδειγμα Εφαρμογής

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που ενώνει όλα τα βήματα. Αντιγράψτε το σε ένα νέο `.csproj` και πατήστε **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Αναμενόμενη έξοδος** στην κονσόλα:

```
Successfully drew rectangle on PDF and saved the file.
```

Ανοίξτε το `output.pdf` και θα δείτε ένα μαύρο ορθογώνιο τοποθετημένο στις συντεταγμένες που καθορίσατε.

---

## Διαχείριση Συνηθισμένων Παραλλαγών

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Multiple pages** | Loop through `pdfDocument.Pages` and apply the same logic to each `Page` object. | Allows batch annotation across a whole document. |
| **Different colors** | Replace `Color.Black` with `Color.Red` or any `System.Drawing.Color`. | Useful for highlighting rather than redacting. |
| **Transparent fill** | Use `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Gives a semi‑transparent overlay instead of a solid block. |
| **Dynamic rectangle size** | Compute `URX` and `URY` based on `PageInfo.Width * 0.5` etc. | Makes the rectangle adapt to various page dimensions. |
| **Error handling** | Wrap the whole block in `try…catch` and log `Aspose.Pdf.IOException`. | Prevents crashes when the source file is missing or locked. |

Αυτές οι προσαρμογές δείχνουν πώς μπορείτε να **create black rectangle** σχολιασμούς σε πολλές συνθήκες χωρίς να ξαναγράψετε τον βασικό κώδικα.

---

## Pro Tips & Pitfalls

- **Dispose the Document**: Παρόλο που η Aspose.PDF υλοποιεί το `IDisposable`, το pattern `using` δεν είναι αυστηρά απαραίτητο για κονσόλες μικρής διάρκειας. Σε υπηρεσίες που τρέχουν πολύ, τυλίξτε το `Document` σε `using` block για άμεση απελευθέρωση των εγγενών πόρων.  
- **Coordinate System**: Οι συντεταγμένες PDF ξεκινούν από την κάτω‑αριστερή γωνία. Αν είστε εξοικειωμένοι με σύστημα προέλευσης πάνω‑αριστερά (όπως WinForms), πρέπει να αντιστρέψετε τον άξονα Y: `pageHeight - y`.  
- **Performance**: Η προσθήκη σχολίων σε πολύ μεγάλα PDFs μπορεί να καταναλώσει μνήμη. Σκεφτείτε επεξεργασία σε τμήματα ή χρήση του `PdfFileEditor` για πιο ελαφριές επεμβάσεις.  
- **Legal**: Βεβαιωθείτε ότι έχετε δικαιώματα να τροποποιήσετε το πηγαίο PDF—ορισμένα έγγραφα είναι προστατευμένα από επεξεργασία.

---

## Συμπέρασμα

Δείξαμε πώς να **draw rectangle on PDF** χρησιμοποιώντας C#—από το **load pdf document**, τον ορισμό γεωμετρίας, το **add black rectangle**, και τέλος το **save modified pdf**. Το παράδειγμα είναι πλήρες, εκτελέσιμο και προσαρμόσιμο σε πραγματικές περιπτώσεις όπως η επεξεργασία πολλαπλών αρχείων ή η προσαρμοσμένη μορφοποίηση.

Στο επόμενο βήμα, μπορείτε να εξερευνήσετε την προσθήκη άλλων τύπων σχολίων (κείμενο, επισήμανση) ή τη συγχώνευση πολλαπλών PDFs μετά το σχολιασμό. Τα βήματα **load pdf document** και **save modified pdf** παραμένουν τα ίδια, ώστε να επεκτείνετε αυτό το μοτίβο με σιγουριά.

Έχετε δοκιμάσει κάποια παραλλαγή; Μοιραστείτε τη στα σχόλια, και καλή κωδικοποίηση!

## Τι Θα Μάθεις Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Δημιουργία γεμισμένου αντικειμένου ορθογωνίου σε PDF χρησιμοποιώντας Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Δημιουργία γεμισμένου αντικειμένου ορθογωνίου σε PDF χρησιμοποιώντας Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Δημιουργία γεμισμένου αντικειμένου ορθογωνίου σε PDF χρησιμοποιώντας Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}