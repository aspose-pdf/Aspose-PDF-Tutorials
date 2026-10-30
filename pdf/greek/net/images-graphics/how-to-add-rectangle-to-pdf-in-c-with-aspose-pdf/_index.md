---
category: general
date: 2026-09-27
description: Μάθετε πώς να προσθέσετε ένα ορθογώνιο σε PDF με C# ενώ φορτώνετε το
  έγγραφο PDF σε C# και έχετε πρόσβαση στην πρώτη σελίδα του PDF με το Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- access first page pdf
- load pdf document c#
- add graphics pdf c#
language: el
lastmod: 2026-09-27
og_description: Προσθέστε ορθογώνιο σε PDF με C# φορτώνοντας το έγγραφο PDF με C#
  και προσπερνώντας την πρώτη σελίδα του PDF. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό
  για αξιόπιστα αποτελέσματα.
og_image_alt: Code editor showing how to add rectangle to PDF using C#
og_title: Προσθήκη ορθογωνίου σε PDF σε C# – πλήρης οδηγός Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to add rectangle to PDF in C# while you load PDF document
    C# and access first page PDF with Aspose.Pdf.
  headline: How to add rectangle to PDF in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Πώς να προσθέσετε ένα ορθογώνιο σε PDF σε C# με το Aspose.Pdf
url: /el/net/images-graphics/how-to-add-rectangle-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε ορθογώνιο σε PDF σε C# με Aspose.Pdf

Αν χρειάζεστε **προσθήκη ορθογωνίου σε PDF** σε μια εφαρμογή C#, αυτός ο οδηγός δείχνει τα ακριβή βήματα. Θα φορτώσετε ένα έγγραφο PDF, θα αποκτήσετε πρόσβαση στην πρώτη σελίδα, θα δημιουργήσετε ένα σχήμα ορθογωνίου και θα γράψετε τις αλλαγές πίσω στο δίσκο. Η λύση λειτουργεί με Aspose.Pdf .NET 2024‑R2 και δεν απαιτεί εξωτερικά εργαλεία.

Η προσθήκη ορθογωνίου σε αρχεία PDF είναι συχνή απαίτηση για επισήμανση τμημάτων, δημιουργία επικάλυψης τύπου φόρμας ή κατασκευή απλών γραφικών. Ακολουθώντας τον παρακάτω κώδικα αποκτάτε ένα επαναχρησιμοποιήσιμο μοτίβο που μπορείτε να επεκτείνετε με άλλα σχήματα, χρώματα ή ρυθμίσεις διαφάνειας.

## Τι θα μάθετε

* Πώς να **φορτώσετε έγγραφο PDF C#** χρησιμοποιώντας Aspose.Pdf.  
* Πώς να **προσπελάσετε την πρώτη σελίδα PDF** με ασφάλεια.  
* Πώς να δημιουργήσετε ένα ορθογώνιο και **να προσθέσετε ορθογώνιο σε PDF**.  
* Πώς να επαληθεύσετε ότι το ορθογώνιο ταιριάζει μέσα στα όρια της σελίδας.  
* Πώς να αποθηκεύσετε το ενημερωμένο αρχείο χωρίς να χάσετε το υπάρχον περιεχόμενο.

Το tutorial υποθέτει ότι έχετε ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio 2022 ή νεότερο) και μια έγκυρη άδεια Aspose.Pdf. Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από `Aspose.Pdf`.

## Βήμα 1: Φόρτωση εγγράφου PDF C#  

Η φόρτωση του αρχικού αρχείου είναι η πρώτη ενέργεια. Το Aspose.Pdf διαβάζει ολόκληρο το PDF στη μνήμη, επιτρέποντάς σας να χειριστείτε σελίδες, σημειώσεις και γραφικά.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // for Color

// Load the PDF document
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

*Γιατί είναι σημαντικό αυτό το βήμα* – Το αντικείμενο `Document` αντιπροσωπεύει ολόκληρο το PDF. Αν το αρχείο δεν μπορεί να ανοιχθεί, ρίχνεται εξαίρεση, επομένως πρέπει να ελέγχετε τη διαδρομή πριν καλέσετε τον κατασκευαστή σε κώδικα παραγωγής.

## Βήμα 2: Πρόσβαση στην πρώτη σελίδα PDF  

Οι σελίδες στο Aspose.Pdf είναι 1‑βασισμένες, έτσι η πρώτη σελίδα ανακτάται με δείκτη 1. Αυτό το βήμα δείχνει τη φράση **πρόσβαση στην πρώτη σελίδα PDF**.

```csharp
// Access the first page (pages are 1‑based)
Page page = doc.Pages[1];
```

*Γιατί είναι σημαντικό* – Η επεξεργασία της σωστής σελίδας αποτρέπει τυχαίες αλλαγές σε μεταγενέστερες σελίδες. Αν το PDF δεν περιέχει σελίδες, το `doc.Pages[1]` προκαλεί `ArgumentOutOfRangeException`, το οποίο μπορείτε να πιάσετε για να εμφανίσετε φιλικό μήνυμα σφάλματος.

## Βήμα 3: Δημιουργία του σχήματος ορθογωνίου  

Τώρα ορίζετε τη γεωμετρία του ορθογωνίου που θέλετε να προσθέσετε. Οι παράμετροι του κατασκευαστή είναι `(x, y, width, height)` όπου το σημείο προέλευσης `(0,0)` είναι η κάτω‑αριστερή γωνία της σελίδας.

```csharp
// Define a rectangle shape (x, y, width, height)
Rectangle rect = new Rectangle(10, 10, 200, 200);

// Optional: customize the appearance
rect.GraphInfo = new GraphInfo
{
    Color = Color.Black,   // stroke color
    LineWidth = 2          // thickness in points
};
```

*Γιατί είναι σημαντικό* – Η ρύθμιση του `GraphInfo` ελέγχει πώς αποδίδεται το ορθογώνιο. Χωρίς αυτό, το σχήμα θα ήταν αόρατο επειδή η προεπιλεγμένη γραμμή είναι διαφανής.

## Βήμα 4: Επαλήθευση ότι το ορθογώνιο χωράει στα όρια της σελίδας  

Πριν προσθέσετε το σχήμα, πρέπει να βεβαιωθείτε ότι δεν υπερβαίνει το μέγεθος της σελίδας. Αυτό αποτρέπει ελαττώματα απόδοσης και διασφαλίζει τη συμμόρφωση με το πρότυπο PDF.

```csharp
// Verify the rectangle fits within the page boundaries
if (page.Rect.Contains(rect))
{
    // Step 5 will run here
}
else
{
    // Adjust rectangle or log a warning
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Γιατί είναι σημαντικό* – Ο έλεγχος `Contains` εγγυάται ότι το ορθογώνιο βρίσκεται πλήρως μέσα στην εκτυπώσιμη περιοχή. Αν παραλείψετε αυτό το βήμα και το ορθογώνιο υπερβεί τα όρια, ορισμένοι προβολείς μπορεί να κόψουν το σχήμα ή να εμφανίσουν σφάλματα.

## Βήμα 5: Προσθήκη ορθογωνίου σε PDF  

Όταν ο έλεγχος ορίων περάσει, προσθέτετε το ορθογώνιο στη σελίδα. Αυτή είναι η κύρια ενέργεια που ικανοποιεί την απαίτηση **προσθήκη ορθογωνίου σε PDF**.

```csharp
// Add the rectangle to the page
page.Add(rect);
```

*Γιατί είναι σημαντικό* – Η `page.Add` εισάγει το σχήμα στο ρεύμα περιεχομένου της σελίδας. Το ορθογώνιο γίνεται μέρος του οπτικού επιπέδου και θα εμφανίζεται σε οποιονδήποτε προβολέα PDF.

## Βήμα 6: Αποθήκευση του ενημερωμένου PDF  

Τέλος, γράψτε το τροποποιημένο έγγραφο πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε νέο.

```csharp
// Save the updated PDF
doc.Save("YOUR_DIRECTORY/output.pdf");
```

*Γιατί είναι σημαντικό* – Η αποθήκευση ολοκληρώνει όλες τις αλλαγές. Αν χρειάζεται να διατηρήσετε το αρχικό, επιλέξτε διαφορετική διαδρομή εξόδου όπως φαίνεται.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα κονσόλας που ενσωματώνει κάθε βήμα. Αντιγράψτε τον κώδικα σε ένα νέο έργο C#, προσαρμόστε τις διαδρομές αρχείων και τρέξτε το.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;

class AddRectangleExample
{
    static void Main()
    {
        // Load the PDF document (load pdf document c#)
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // Access first page PDF
        Page page = doc.Pages[1];

        // Create a rectangle shape
        Rectangle rect = new Rectangle(10, 10, 200, 200);
        rect.GraphInfo = new GraphInfo
        {
            Color = Color.Black,
            LineWidth = 2
        };

        // Verify bounds before adding
        if (page.Rect.Contains(rect))
        {
            // Add rectangle to PDF
            page.Add(rect);
        }
        else
        {
            System.Console.WriteLine("Rectangle does not fit on the page.");
            return;
        }

        // Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Rectangle added successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα** – Μετά την εκτέλεση, το `output.pdf` περιέχει το αρχικό περιεχόμενο συν ένα ορθογώνιο με μαύρο περίγραμμα, τοποθετημένο 10 pt από την κάτω‑αριστερή γωνία. Ανοίγοντας το αρχείο σε Adobe Acrobat ή οποιονδήποτε προβολέα PDF θα δείτε την επικάλυψη ορθογωνίου στην πρώτη σελίδα.

## Διαχείριση κοινών παραλλαγών

| Κατάσταση | Συνιστώμενη αλλαγή |
|-----------|--------------------|
| Το μέγεθος σελίδας διαφέρει (π.χ., A4 vs. Letter) | Χρησιμοποιήστε `page.Rect.Width` και `page.Rect.Height` για να υπολογίσετε ένα ορθογώνιο που ταιριάζει δυναμικά. |
| Χρειάζεστε γεμάτο ορθογώνιο | Ορίστε `rect.GraphInfo.FillColor = Color.LightGray;` και προαιρετικά `rect.GraphInfo.IsFilled = true;`. |
| Πολλές σελίδες απαιτούν το ίδιο ορθογώνιο | Κάντε βρόχο πάνω από `doc.Pages` και επαναλάβετε την προσθήκη για κάθε σελίδα. |
| Απαιτείται διαφάνεια | Ορίστε `rect.GraphInfo.Transparency = 0.5;` (εύρος 0–1). |

Αυτές οι παραλλαγές δείχνουν πώς η προσέγγιση **add graphics pdf c#** κλιμακώνεται πέρα από ένα μόνο σχήμα.

## Pro tips

* **Συμβουλή απόδοσης** – Όταν επεξεργάζεστε μεγάλα PDF, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Document` και αποφύγετε την κλήση `Save` μέσα σε βρόχο. Κάντε αποθήκευση μία φορά μετά την επεξεργασία όλων των σελίδων.  
* **Διαχείριση σφαλμάτων** – Τυλίξτε όλη τη ροή σε ένα `try/catch` μπλοκ για να πιάσετε `FileNotFoundException`, `InvalidOperationException` και το ειδικό Aspose `PdfException`.  
* **Άδεια** – Καταχωρίστε την άδεια Aspose.Pdf πριν δημιουργήσετε ένα `Document` για να αποφύγετε το υδατογράφημα αξιολόγησης.

## Συμπέρασμα

Τώρα ξέρετε πώς να **προσθέσετε ορθογώνιο σε PDF** σε C# φορτώνοντας ένα


## Τι πρέπει να μάθετε στη συνέχεια;


Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην δική σας υλοποίηση.

- [Create PDF Document in C# – Add Page to PDF & Rectangle](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/)
- [Create PDF Document C# – Add Blank Page & Draw Rectangle](/pdf/english/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/)
- [Create PDF Document C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}