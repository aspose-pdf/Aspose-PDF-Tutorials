---
category: general
date: 2026-08-04
description: Προσθήκη ορθογωνίου σε PDF χρησιμοποιώντας C#. Μάθετε πώς να σχεδιάζετε
  σχήμα σε PDF C# με το Aspose.Pdf σε ένα σαφές, πλήρες παράδειγμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: el
lastmod: 2026-08-04
og_description: Προσθέστε ορθογώνιο στο PDF χρησιμοποιώντας C#. Αυτό το σεμινάριο
  δείχνει πώς να σχεδιάσετε σχήμα σε PDF C# γρήγορα και αξιόπιστα.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Προσθήκη ορθογωνίου σε PDF με C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Προσθήκη ορθογωνίου σε PDF με C# – βήμα‑βήμα οδηγός
url: /el/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη ορθογωνίου σε PDF με C# – βήμα‑βήμα οδηγός

Αν χρειάζεστε **add rectangle to PDF** αρχεία από μια εφαρμογή C#, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που σχεδιάζει ένα σχήμα σε PDF C# χρησιμοποιώντας τη βιβλιοθήκη Aspose.Pdf, και θα καταλάβετε γιατί κάθε γραμμή κώδικα έχει σημασία.

Η σχεδίαση σχημάτων σε PDF είναι συχνή απαίτηση για δημιουργούς αναφορών, πρότυπα τιμολογίων και προσαρμοσμένο branding εγγράφων. Στο τέλος αυτού του tutorial, θα μπορείτε να εισάγετε οποιαδήποτε ορθογώνια σημείωση, να αλλάζετε το μέγεθος, το χρώμα ή τη θέση της, και να αποθηκεύετε το τροποποιημένο έγγραφο χωρίς να χάνετε το υπάρχον περιεχόμενο.

**Τι θα μάθετε**

* Πώς να φορτώσετε ένα υπάρχον PDF με Aspose.Pdf.
* Πώς να ορίσετε τα όρια του ορθογωνίου και να δημιουργήσετε ένα σχήμα ορθογωνίου.
* Πώς να προσθέσετε το ορθογώνιο στη συλλογή παραγράφων μιας σελίδας.
* Πώς να αποθηκεύσετε το ενημερωμένο PDF και να επαληθεύσετε το αποτέλεσμα.
* Παραλλαγές για πολλαπλές σελίδες, διαφάνεια και προσαρμοσμένα στυλ γραμμής.

**Προαπαιτούμενα**

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
* Visual Studio 2022 ή οποιοδήποτε IDE για C#.
* Αναφορά NuGet στο `Aspose.Pdf` (δωρεάν δοκιμή ή έκδοση με άδεια).
* Ένα αρχείο PDF εισόδου με όνομα `input.pdf` τοποθετημένο σε φάκελο που ελέγχετε.

---

## Πώς να σχεδιάσετε σχήμα σε PDF C# – ρύθμιση του έργου

1. **Δημιουργήστε ένα νέο έργο console**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Προσθέστε το πακέτο Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Τοποθετήστε το `input.pdf`** στον κατάλογο του έργου (ή σε οποιονδήποτε φάκελο θα αναφέρετε αργότερα).

Το έργο είναι τώρα έτοιμο να μεταγλωττίσει κώδικα που θα **add rectangle to PDF** αρχεία.

---

## Βήμα 1: Φόρτωση του εγγράφου PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*Η κλάση `Document` αναλύει το αρχείο και εκθέτει μια συλλογή `Pages`. Η φόρτωση είναι η πρώτη απαιτούμενη ενέργεια πριν μπορέσει να γίνει οποιαδήποτε σχεδίαση.*

---

## Βήμα 2: Επιλογή της σελίδας-στόχου

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Αν χρειάζεστε να προσθέσετε το ορθογώνιο σε διαφορετική σελίδα, αντικαταστήστε το δείκτη με τον επιθυμητό αριθμό σελίδας. Η βιβλιοθήκη ρίχνει εξαίρεση όταν ο δείκτης είναι εκτός εύρους, οπότε βεβαιωθείτε ότι το PDF περιέχει αρκετές σελίδες.*

---

## Βήμα 3: Ορισμός των ορίων του ορθογωνίου

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Το σύστημα συντεταγμένων χρησιμοποιεί μονάδες points (1 pt = 1/72 inch). Το παράδειγμα δημιουργεί ένα ορθογώνιο 250 pt πλάτους και 100 pt ύψους κοντά στην κορυφή της σελίδας. Προσαρμόστε τους αριθμούς ώστε να ταιριάζουν στο layout σας.*

---

## Βήμα 4: Δημιουργία του σχήματος ορθογωνίου

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*Η κλάση `Rectangle` κληρονομεί από την `GraphicalObject`. Η ρύθμιση του `FillColor` και του `Border` είναι προαιρετική, αλλά δείχνει πώς να ελέγχετε την εμφάνιση όταν **how to draw shape in PDF C#** πέρα από ένα απλό περίγραμμα.*

---

## Βήμα 5: Προσθήκη του ορθογωνίου στη σελίδα

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Οι παράγραφοι είναι το δοχείο για οποιοδήποτε αντικείμενο που μπορεί να σχεδιαστεί. Εισάγοντας το σχήμα στα `Paragraphs`, το Aspose.Pdf το αποδίδει όταν το έγγραφο αποθηκευτεί.*

---

## Βήμα 6: Αποθήκευση του τροποποιημένου PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Η αποθήκευση δημιουργεί νέο αρχείο ώστε το αρχικό `input.pdf` να παραμείνει αμετάβλητο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο περνώντας την ίδια διαδρομή, αλλά η διατήρηση αντιγράφου ασφαλείας είναι καλή πρακτική.*

---

## Πλήρης πηγαίος κώδικας (εκτελέσιμο)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Αναμενόμενο αποτέλεσμα** – Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε ένα μπλε-γεμισμένο ορθογώνιο κοντά στην επάνω‑δεξιά γωνία της πρώτης σελίδας, με σκούρο γκρι περίγραμμα.

---

## Πώς να σχεδιάσετε σχήμα σε PDF C# σε πολλαπλές σελίδες

Αν χρειάζεστε **add rectangle to PDF** σε κάθε σελίδα, κάντε βρόχο στη συλλογή `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Αυτό το πρότυπο επαναχρησιμοποιεί τα ίδια όρια σε κάθε σελίδα. Προσαρμόστε τις συντεταγμένες ανά σελίδα αν χρειάζεστε διαφορετικές θέσεις.*

---

## Συνηθισμένα προβλήματα και συμβουλές βέλτιστης πρακτικής

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Το ορθογώνιο εμφανίζεται εκτός σελίδας | Οι συντεταγμένες μετρώνται από το κάτω‑αριστερό; η χρήση συστήματος συντεταγμένων με προσανατολισμό στην κορυφή μπορεί να προκαλέσει σύγχυση. | Θυμηθείτε ότι ο άξονας Y αυξάνεται προς τα πάνω. Χρησιμοποιήστε τιμές που χωρούν στο μέγεθος της σελίδας (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Το σχήμα είναι αόρατο | Η διαφάνεια γεμίσματος ορίστηκε σε `0` ή το πλάτος περιγράμματος σε `0`. | Βεβαιωθείτε ότι το `FillOpacity` είναι μεγαλύτερο του `0` και το `Border.Width` τουλάχιστον `0.5`. |
| Η αποθήκευση ρίχνει `AccessDeniedException` | Το αρχείο εξόδου είναι ανοιχτό σε άλλο πρόγραμμα. | Κλείστε τυχόν προβολείς πριν τρέξετε τον κώδικα, ή αποθηκεύστε σε διαφορετική διαδρομή. |
| Το ορθογώνιο επικαλύπτει υπάρχον περιεχόμενο | Δεν ορίστηκε έλεγχος στρώσεων. | Χρησιμοποιήστε την ιδιότητα `ZIndex` (υψηλότερες τιμές αποδίδονται πάνω) αν χρειάζεστε έλεγχο στρώσεων. |

---

## Επέκταση του ορθογωνίου – διαβαθμίσεις, περιστροφή και διαφάνεια

Το Aspose.Pdf υποστηρίζει προχωρημένα γραφικά. Για δημιουργία περιστρεφόμενου ορθογωνίου με γραμμική διαβάθμιση:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Το ίδιο πρότυπο κώδικα δείχνει **how to draw shape in PDF C#** με πιο πλούσια οπτικά εφέ.*

---

## Επαλήθευση του αποτελέσματος προγραμματιστικά

Μπορείτε να επιβεβαιώσετε ότι το ορθογώνιο προστέθηκε ελέγχοντας τον αριθμό παραγράφων της σελίδας:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Αν ο αριθμός αυξηθεί κατά ένα μετά την εισαγωγή, η λειτουργία πέτυχε.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **add rectangle to PDF** αρχεία χρησιμοποιώντας C#. Το tutorial κάλυψε τη φόρτωση εγγράφου, τον ορισμό ορίων, τη δημιουργία σχήματος ορθογωνίου, την εισαγωγή του σε μια σελίδα και την αποθήκευση του αποτελέσματος. Επίσης, είδατε πώς να διαχειριστείτε πολλαπλές σελίδες, να αποφύγετε κοινά σφάλματα και να εφαρμόσετε προχωρημένο στυλ.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **how to draw shape in PDF C#** για κύκλους, πολύγωνα ή ελεύθερες γραμμές, και μάθετε να συνδυάζετε σχήματα με κείμενο και εικόνες για τη δημιουργία πλήρων PDF αναφορών.

Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να προσθέσετε σφραγίδες σελίδων σε PDF χρησιμοποιώντας Aspose.PDF for .NET | Οδηγός Υδατογραφιών & Υποβάθρων](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Πώς να προσθέσετε σφραγίδα εικόνας σε PDF χρησιμοποιώντας Aspose.PDF for .NET: Ένας ολοκληρωμένος οδηγός](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Πώς να προσθέσετε περιστρεφόμενη υδατογραφία εικόνας σε PDF χρησιμοποιώντας Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}