---
category: general
date: 2026-10-07
description: Μάθετε πώς να προσθέτετε αρίθμηση Bates σε ένα PDF χρησιμοποιώντας C#.
  Αυτός ο βήμα‑βήμα οδηγός καλύπτει επίσης την αρίθμηση σελίδων PDF και άλλα κόλπα
  αρίθμησης.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: el
lastmod: 2026-10-07
og_description: Προσθέστε γρήγορα αρίθμηση Bates σε ένα PDF. Ακολουθήστε αυτό το σεμινάριο
  για να κατακτήσετε την αρίθμηση σελίδων PDF, να αριθμήσετε τις σελίδες PDF και να
  αυτοματοποιήσετε την παρακολούθηση εγγράφων.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Προσθήκη αρίθμησης Bates σε PDF με C# – πλήρης οδηγός Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Πώς να προσθέσετε αρίθμηση Bates σε ένα PDF με το Aspose.Pdf
url: /el/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε αρίθμηση bates σε ένα PDF με το Aspose.Pdf

Αν χρειάζεστε **προσθήκη αρίθμησης bates** σε ένα PDF, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε σε C#. Είτε ετοιμάζετε νομικά πακέτα, διαχειρίζεστε φακέλους υποθέσεων, είτε απλώς θέλετε αξιόπιστη **αρίθμηση σελίδων pdf**, τα παρακάτω βήματα σας παρέχουν μια πλήρη, εκτελέσιμη λύση.

Σε αυτό το tutorial θα μάθετε πώς να:

* Φορτώσετε ένα υπάρχον αρχείο PDF.
* Διαμορφώσετε τις επιλογές αρίθμησης Bates όπως πρόθεμα, αριθμό εκκίνησης, πλήθος ψηφίων, διαχωριστικό και επίθημα.
* Εφαρμόσετε την αρίθμηση σε κάθε σελίδα.
* Αποθηκεύσετε το ενημερωμένο έγγραφο.

Δεν απαιτούνται εξωτερικά εργαλεία πέρα από τη βιβλιοθήκη Aspose.Pdf for .NET, και ο κώδικας λειτουργεί με .NET 6+ καθώς και με .NET Framework 4.7.2+.  

---

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Παρέχει τις κλάσεις `Document` και `BatesNumberingOptions` που χρησιμοποιούνται στον κώδικα. |
| **.NET SDK** (6.0 or later recommended) | Σας επιτρέπει να μεταγλωττίσετε και να εκτελέσετε την εφαρμογή κονσόλας C#. |
| **A source PDF** you want to number | Ο οδηγός χρησιμοποιεί το `source.pdf` ως παράδειγμα· αντικαταστήστε τη διαδρομή με το δικό σας αρχείο. |
| **Write permission** to the output folder | Η κλήση `Save` χρειάζεται να γράψει το νέο αρχείο. |

Μπορείτε να εγκαταστήσετε τη βιβλιοθήκη με την ακόλουθη εντολή CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Βήμα 1: Δημιουργία νέου έργου κονσόλας

Ανοίξτε ένα τερματικό και εκτελέστε:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Αυτό δημιουργεί ένα ελάχιστο έργο C# που θα γεμίσουμε με τον κώδικα που απαιτείται για **προσθήκη αρίθμησης bates**.

---

## Βήμα 2: Προσθήκη των απαιτούμενων `using` δηλώσεων

Ανοίξτε το `Program.cs` και προσθέστε τα namespaces στην κορυφή του αρχείου:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` σας δίνει πρόσβαση στην κλάση `Document` για τη φόρτωση και αποθήκευση PDF.  
* `Aspose.Pdf.Text` περιέχει το `BatesNumberingOptions`, το αντικείμενο που ορίζει πώς εμφανίζονται οι αριθμοί.

---

## Βήμα 3: Φόρτωση του πηγαίου PDF

Η πρώτη ενεργή γραμμή φορτώνει το PDF που θέλετε να αριθμήσετε. Αντικαταστήστε `"YOUR_DIRECTORY/source.pdf"` με την πραγματική διαδρομή του αρχείου σας.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα `FileNotFoundException`. Για να το αποφύγετε, ίσως θέλετε να επικυρώσετε τη διαδρομή εκ των προτέρων:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Βήμα 4: Ορισμός επιλογών αρίθμησης Bates

`BatesNumberingOptions` σας επιτρέπει να ελέγξετε κάθε οπτικό στοιχείο της αρίθμησης. Το παρακάτω παράδειγμα δείχνει μια τυπική διαμόρφωση για νομικά αρχεία υποθέσεων:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Γιατί κάθε ιδιότητα είναι σημαντική**

| Ιδιότητα | Σκοπός |
|----------|--------|
| `Prefix` | Σας βοηθά να ομαδοποιήσετε έγγραφα ανά έργο, πελάτη ή υπόθεση. |
| `StartNumber` | Ορίζει τον αρχικό μετρητή· χρήσιμο όταν έχετε ήδη υπάρχοντα αριθμημένα αρχεία. |
| `Digits` | Εγγυάται ομοιόμορφο πλάτος, διευκολύνοντας την ταξινόμηση. |
| `Separator` | Βελτιώνει την αναγνωσιμότητα, ειδικά όταν συνδυάζετε πρόθεμα και επίθημα. |
| `Suffix` | Σας επιτρέπει να προσθέσετε έτος, έκδοση ή οποιοδήποτε επίθεμα. |

Μπορείτε επίσης να ελέγξετε τη θέση (πάνω, κάτω, αριστερά, δεξιά) και το στυλ γραμματοσειράς προσπερνώντας τα `batesOptions.Position` και `batesOptions.Font`. Για τις περισσότερες περιπτώσεις, οι προεπιλογές (κάτω‑δεξιά, 12‑pt Times New Roman) λειτουργούν καλά.

---

## Βήμα 5: Εφαρμογή της αρίθμησης σε κάθε σελίδα

Καλώντας το `pdf.BatesNumbering.Add` εισάγει τους αριθμούς σε κάθε σελίδα με τη σειρά που εμφανίζονται.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Αν χρειάζεται να **αριθμήσετε pdf σελίδες** μόνο σε ένα υποσύνολο (π.χ., να παραλείψετε τη σελίδα εξώφυλλου), μπορείτε να περάσετε ένα `PageCollection` αντί αυτού:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Βήμα 6: Αποθήκευση του ενημερωμένου PDF

Τέλος, γράψτε το τροποποιημένο έγγραφο στο δίσκο. Το όνομα του αρχείου συνήθως υποδεικνύει ότι το PDF περιέχει τώρα αριθμούς Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Αν ο φάκελος εξόδου δεν υπάρχει, το Aspose το δημιουργεί αυτόματα. Ωστόσο, θα πρέπει να βεβαιωθείτε ότι έχετε δικαιώματα εγγραφής για να αποφύγετε ένα `UnauthorizedAccessException`.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα** (κονσόλα):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Ανοίξτε το `bates_numbered.pdf` και θα δείτε κάθε σελίδα να έχει ετικέτα κάτι όπως `CASE-001000-2025`, `CASE-001001-2025`, κ.λπ., τοποθετημένη στην προεπιλεγμένη κάτω‑δεξιά γωνία.

---

## Συχνές ερωτήσεις (FAQ)

### 1. Μπορώ να αλλάξω τη θέση των αριθμών;
Ναι. Ορίστε `batesOptions.Position = new Position(10, 10, 10, 10);` όπου οι τέσσερις τιμές αντιπροσωπεύουν τα περιθώρια από την κορυφή, το κάτω μέρος, αριστερά και δεξιά. Το Aspose παρέχει επίσης προορισμένους enum όπως `BatesNumberingPosition.BottomCenter`.

### 2. Τι γίνεται αν το PDF μου περιέχει ήδη αριθμούς σελίδας;
Η προσθήκη αριθμών Bates θα **στοίβαξει** πάνω από τους υπάρχοντες αριθμούς. Για να αποφύγετε την οπτική ακαταστασία, είτε αποκρύψτε τους αρχικούς αριθμούς (αν είναι μέρος ενός επιπέδου κειμένου) είτε προσαρμόστε το μέγεθος γραμματοσειράς και τη θέση του `batesOptions`.

### 3. Λειτουργεί αυτό με κρυπτογραφημένα PDFs;
Το Aspose μπορεί να ανοίξει PDF προστατευμένα με κωδικό πρόσβασης αν παρέχετε τον κωδικό:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Η αρίθμηση Bates εφαρμόζεται στη συνέχεια με τον ίδιο τρόπο.

### 4. Πώς μπορώ να **αριθμήσω pdf σελίδες** με έναν απλό διαδοχικό μετρητή (χωρίς πρόθεμα/επίθημα);
Απλώς ορίστε `Prefix = string.Empty` και `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση σε ASP.NET Core για να σερβίρω PDFs on‑the‑fly;
Απολύτως. Φορτώστε το έγγραφο, εφαρμόστε την αρίθμηση, έπειτα γράψτε το ρεύμα στην HTTP απόκριση:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Περιπτώσεις άκρων και συμβουλές βέλτιστης πρακτικής

| Κατάσταση | Συνιστώμενη προσέγγιση |
|-----------|------------------------|
| **Μεγάλα PDFs (εκατοντάδες σελίδες)** | Καλέστε `pdf.BatesNumbering.Add` **μετά** από τις μετατροπές επιπέδου σελίδας ώστε να αποφύγετε την επανεπεξεργασία των ίδιων σελίδων πολλές φορές. |
| **Προσαρμοσμένες γραμματοσειρές** | Ορίστε `batesOptions.Font = FontRepository.FindFont("Arial")` και προσαρμόστε το `batesOptions.FontSize` για καλύτερη αναγνωσιμότητα σε σαρωμένα έγγραφα. |
| **Δουλειές παρτίδας με κρίσιμη απόδοση** | Επαναχρησιμοποιήστε ένα μόνο αντικείμενο `Document` όταν επεξεργάζεστε πολλά αρχεία σε βρόχο· απελευθερώστε το μετά από κάθε επανάληψη για να ελευθερώσετε μνήμη. |
| **Διεθνή χαρακτήρες** | Χρησιμοποιήστε γραμματοσειρές συμβατές με Unicode (π.χ., `Times New Roman Unicode`) ώστε το πρόθεμα ή το επίθημα να εμφανίζονται σωστά. |
| **Συμβατότητα έκδοσης** | Ο κώδικας λειτουργεί με Aspose.Pdf 23.10 και νεότερες. Αν στοχεύετε σε παλαιότερη έκδοση, ελέγξτε την τεκμηρίωση API για τυχόν αλλαγές ονομάτων ιδιοτήτων. |

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **προσθέσετε αρίθμηση bates** σε ένα PDF χρησιμοποιώντας το Aspose.Pdf for .NET. Ο οδηγός κάλυψε τη φόρτωση PDF, τη διαμόρφωση του `BatesNumberingOptions`, την εφαρμογή των αριθμών σε κάθε σελίδα και την αποθήκευση του αποτελέσματος. Με αυτά τα δομικά στοιχεία μπορείτε επίσης να υλοποιήσετε γενική **αρίθμηση σελίδων pdf**, **αριθμήσετε pdf σελίδες** με προσαρμοσμένες μορφές, και να ενσωματώσετε τη διαδικασία σε μεγαλύτερα pipelines αυτοματοποίησης.

**Επόμενα βήματα**

* Εξερευνήστε περαιτέρω το API **bates numbering pdf** για προσαρμογή γραμματοσειράς, χρώματος και τοποθέτησης.  
* Συνδυάστε αυτήν την τεχνική με **ψηφιακές υπογραφές** για τη δημιουργία νομικών πακέτων με ανίχνευση παραποίησης.  
* Δείτε τις δυνατότητες **συγχώνευσης PDF** του Aspose αν χρειάζεται να ενώσετε πολλά αρχεία υποθέσεων πριν την αρίθμηση.

Πειραματιστείτε με διαφορετικά προθέματα, επιθήματα και μήκη ψηφίων για να ταιριάζουν με τα πρότυπα αρχειοθέτησης του οργανισμού σας. Καλή προγραμματιστική δουλειά!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Δημιουργία PDF Εγγράφου C# – Οδηγός Προσθήκης Αρίθμησης Bates](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [Πώς να Προσθέσετε Αρίθμηση Bates σε PDF με C# – Πλήρης Οδηγός](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Εισαγωγή Κενής Σελίδας και Ενημέρωση Αρίθμησης Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}