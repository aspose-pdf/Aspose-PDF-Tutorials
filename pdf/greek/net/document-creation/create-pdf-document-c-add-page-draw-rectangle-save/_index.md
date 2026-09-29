---
category: general
date: 2026-02-14
description: 'Δημιουργήστε γρήγορα έγγραφο PDF με C#: προσθέστε σελίδα στο PDF, σχεδιάστε
  ένα σχήμα ορθογωνίου και αποθηκεύστε το PDF σε αρχείο χρησιμοποιώντας το Aspose.Pdf
  σε λίγες γραμμές κώδικα.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: el
og_description: Δημιουργήστε έγγραφο PDF C# σε λίγα λεπτά. Μάθετε πώς να προσθέσετε
  σελίδα σε PDF, να σχεδιάσετε ορθογώνιο, να προσθέσετε σχήμα σε PDF και να αποθηκεύσετε
  το PDF σε αρχείο με σαφή παραδείγματα κώδικα.
og_title: Δημιουργία εγγράφου PDF C# – Οδηγός βήμα‑προς‑βήμα
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Δημιουργία PDF Εγγράφου C# – Προσθήκη Σελίδας, Σχεδίαση Ορθογωνίου & Αποθήκευση
url: /el/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

markdown links: none.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου PDF C# – Προσθήκη σελίδας, Σχεδίαση ορθογωνίου & Αποθήκευση

Έχετε ποτέ χρειαστεί να **create PDF document C#** από το μηδέν και να αναρωτηθείτε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο εμπόδιο όταν προσπαθούν για πρώτη φορά να δημιουργήσουν PDF προγραμματιστικά. Τα καλά νέα; Με λίγες γραμμές κώδικα Aspose.Pdf μπορείτε να προσθέσετε μια σελίδα σε PDF, να σχεδιάσετε ένα ορθογώνιο και **save PDF to file** χωρίς καμία δυσκολία.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε: την αρχικοποίηση του PDF, την εισαγωγή μιας νέας σελίδας, τη σχεδίαση ενός ορθογωνίου σχήματος και, τέλος, την αποθήκευση του αρχείου στο δίσκο. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή console που παράγει ένα καθαρό μπλε‑περιγραμμένο ορθογώνιο μέσα σε μια νέα σελίδα PDF.

## Τι Θα Χρειαστεί

- **.NET 6 ή νεότερο** (το παράδειγμα χρησιμοποιεί top‑level statements, αλλά οποιαδήποτε πρόσφατη έκδοση .NET λειτουργεί)
- **Aspose.Pdf for .NET** πακέτο NuGet  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- Ένας φάκελος όπου έχετε δικαίωμα εγγραφής – το tutorial θα αποθηκεύσει το αρχείο στο `YOUR_DIRECTORY/shapes.pdf`.

Καμία επιπλέον ρύθμιση, χωρίς XML, μόνο απλό C#.

## Δημιουργία εγγράφου PDF C# – Επισκόπηση

Το πρώτο βήμα είναι η δημιουργία ενός αντικειμένου `Document`. Σκεφτείτε το ως το κενό καμβά σας· όλα όσα προσθέτετε αργότερα—σελίδες, κείμενο, σχήματα—συνδέονται με αυτή τη μοναδική παρουσία.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **Γιατί `using var`?**  
> Η κλάση `Document` υλοποιεί το `IDisposable`. Η τοποθέτησή της σε δήλωση `using` εξασφαλίζει ότι όλοι οι μη διαχειριζόμενοι πόροι (χειριστήρια αρχείων, εγγενείς buffers) απελευθερώνονται αμέσως μόλις τελειώσουμε, κάτι που είναι ιδιαίτερα σημαντικό σε υπηρεσίες μακράς διάρκειας.

## Προσθήκη Σελίδας σε PDF

Ένα PDF χωρίς σελίδες είναι σαν ένα βιβλίο χωρίς σελίδες—αχρείαστο. Η προσθήκη μιας σελίδας είναι μια κλήση μεθόδου, αλλά σας δίνει επίσης ένα αντικείμενο `Page` που μπορείτε αργότερα να χειριστείτε.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Συμβουλή:** Η νεοπροστέθεισα σελίδα υιοθετεί αυτόματα το προεπιλεγμένο μέγεθος (A4). Αν χρειάζεστε προσαρμοσμένο μέγεθος, μπορείτε να ορίσετε `pdfPage.PageInfo.Width` και `Height` πριν προσθέσετε οποιοδήποτε περιεχόμενο.

## Πώς να Σχεδιάσετε Ορθογώνιο

Τώρα για το διασκεδαστικό μέρος: τη σχεδίαση ενός ορθογωνίου. Το Aspose.Pdf χρησιμοποιεί την κλάση `RectangleShape`, η οποία αναμένει ένα `Rectangle` (x, y, width, height) που ορίζει τα όρια. Οι συντεταγμένες ξεκινούν από την κάτω‑αριστερή γωνία της σελίδας.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Ακραία περίπτωση:** Αν το `x + width` υπερβαίνει το πλάτος της σελίδας ή το `y + height` υπερβαίνει το ύψος της σελίδας, το Aspose ρίχνει ένα `ArgumentException`. Πάντα ελέγχετε ξανά τις διαστάσεις σας, ειδικά όταν δημιουργείτε PDF για διαφορετικά μεγέθη σελίδας.

## Προσθήκη Σχήματος σε PDF

Με τα όρια έτοιμα, δημιουργούμε το σχήμα, του δίνουμε μια μπλε γραμμή περιγράμματος και το προσθέτουμε στη συλλογή παραγράφων της σελίδας.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **Γιατί να το προσθέσετε στα `Paragraphs`;**  
> Στο Aspose.Pdf, τα οπτικά στοιχεία όπως τα σχήματα αντιμετωπίζονται ως “παράγραφοι” επειδή καταλαμβάνουν μια ορθογώνια περιοχή στη σελίδα. Αυτός ο σχεδιασμός διατηρεί τη μηχανή διάταξης συνεπή μεταξύ κειμένου και γραφικών.

## Αποθήκευση PDF σε Αρχείο

Η τελική ενέργεια είναι η αποθήκευση του εγγράφου. Δώστε μια πλήρη διαδρομή, και το Aspose αναλαμβάνει το δύσκολο μέρος—συμπίεση, ροές αντικειμένων και πίνακες αναφοράς διασυνδέονται αυτόματα.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Pro tip:** Χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` αν θέλετε το αρχείο δίπλα στο εκτελέσιμο σας, ή δημιουργήστε τον φάκελο με `Directory.CreateDirectory` εκ των προτέρων για να αποφύγετε ένα `DirectoryNotFoundException`.

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `shapes.pdf` με οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε μια μοναδική σελίδα μεγέθους A4 με ένα **blue‑bordered rectangle** τοποθετημένο 50 σημεία από τις αριστερές και κάτω άκρες, με διαστάσεις 200 × 150 σημεία. Χωρίς κείμενο, μόνο το σχήμα—τέλειο για υδατογραφήματα, πεδία φόρμας ή οπτικούς placeholders.

![Έγγραφο PDF με ένα μπλε ορθογώνιο που δημιουργήθηκε χρησιμοποιώντας create pdf document c#](https://example.com/images/pdf-rectangle.png "Έγγραφο PDF με ένα μπλε ορθογώνιο που δημιουργήθηκε χρησιμοποιώντας create pdf document c#")

*Alt text:* *Έγγραφο PDF με ένα μπλε ορθογώνιο που δημιουργήθηκε χρησιμοποιώντας create pdf document c#.*

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Συγκεντρώνεται ως εφαρμογή console (`dotnet new console`) και εκτελείται χωρίς καμία επιπλέον ρύθμιση πέρα από το πακέτο NuGet.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο, και θα δείτε το σχήμα ακριβώς όπου το ορίσαμε.

## Συχνές Ερωτήσεις & Προβλήματα

- **Q:** *Τι γίνεται αν χρειαστώ γεμάτο ορθογώνιο;*  
  **A:** Απενεργοποιήστε το σχόλιο στη γραμμή `FillColor` στον αρχικοποιητή `RectangleShape`. Το Aspose υποστηρίζει συμπαγή χρώματα, διαβαθμίσεις και ακόμη γεμίσματα εικόνας.

- **Q:** *Μπορώ να σχεδιάσω πολλαπλά σχήματα στην ίδια σελίδα;*  
  **A:** Απόλυτα. Απλώς δημιουργήστε επιπλέον αντικείμενα `RectangleShape`, `Ellipse` ή `Polygon` και προσθέστε τα στο `pdfPage.Paragraphs`.

- **Q:** *Είναι το σύστημα συντεταγμένων πάντα κάτω‑αριστερό;*  
  **A:** Ναι, το Aspose ακολουθεί την προδιαγραφή PDF όπου το αρχικό σημείο (0,0) βρίσκεται στην κάτω‑αριστερή γωνία. Αν προτιμάτε αρχικό σημείο πάνω‑αριστερά, θα πρέπει να υπολογίσετε `y = pageHeight - desiredY`.

- **Q:** *Τι συμβαίνει αν ο φάκελος προορισμού δεν υπάρχει;*  
  **A:** Το `pdfDocument.Save` θα ρίξει ένα `DirectoryNotFoundException`. Δημιουργήστε εκ των προτέρων το φάκελο με `Directory.CreateDirectory`.

## Επόμενα Βήματα

Τώρα που ξέρετε πώς να **add page to PDF**, **how to draw rectangle**, **add shape to PDF**, και **save PDF to file**, μπορείτε να επεκτείνετε αυτή τη βάση:

- Εισαγωγή κειμένου, εικόνων ή πινάκων μαζί με τα σχήματα.  
- Χρήση του `Graphics` για ελεύθερη σχεδίαση (γραμμές, τόξα, προσαρμοσμένα μονοπάτια).  
- Εξερεύνηση κρυπτογράφησης PDF ή ψηφιακών υπογραφών εάν η ασφάλεια αποτελεί πρόβλημα.

Κάθε ένα από αυτά τα θέματα βασίζεται άμεσα στον κώδικα που καλύψαμε, οπότε νιώστε άνετα να πειραματιστείτε.

---

**Bottom line:** Μόλις μάθατε τη πλήρη ροή εργασίας για **create PDF document C#** με το Aspose.Pdf—αρχικοποίηση, προσθήκη σελίδας, σχεδίαση ορθογωνίου σχήματος και αποθήκευση του αρχείου. Είναι ένα σταθερό δομικό στοιχείο για τιμολόγια, αναφορές, πιστοποιητικά ή οποιοδήποτε αυτοματοποιημένο έγγραφο χρειάζεται να δημιουργήσετε άμεσα. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}