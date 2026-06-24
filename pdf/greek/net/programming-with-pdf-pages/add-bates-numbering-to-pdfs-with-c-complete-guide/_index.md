---
category: general
date: 2026-06-24
description: Προσθέστε αρίθμηση Bates σε αρχεία PDF χρησιμοποιώντας C# και Aspose.PDF.
  Μάθετε προσαρμοσμένους αριθμούς σελίδων, διαδοχική αρίθμηση σελίδων και αρίθμηση
  κεφαλίδας/υποσέλιδου σε λίγα λεπτά.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: el
og_description: Προσθέστε αρίθμηση Bates σε αρχεία PDF χρησιμοποιώντας C# και Aspose.PDF.
  Κατακτήστε την προσαρμοσμένη αρίθμηση σελίδων και την αρίθμηση κεφαλίδων/υποσέλιδων
  σε λίγα εύκολα βήματα.
og_title: Προσθέστε αρίθμηση Bates σε PDF με C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Προσθήκη αρίθμησης Bates σε PDF με C# – Πλήρης οδηγός
url: /el/net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Αρίθμησης σε PDF με C# – Πλήρης Οδηγός

Προσθέστε Bates αρίθμηση στα αρχεία PDF σας με C# με λίγες μόνο γραμμές κώδικα. Αν χρειάζεστε προσαρμοσμένους αριθμούς σελίδας για νομικά έγγραφα ή θέλετε διαδοχικούς αριθμούς σε όλο το πακέτο συμβάσεων, αυτό το tutorial καλύπτει όλα όσα χρειάζεστε.

Στις επόμενες λίγες λεπτά θα περάσουμε από όλα όσα πρέπει να γνωρίζετε: φόρτωση PDF, διαμόρφωση του στυλ αρίθμησης, εφαρμογή των αριθμών και τελικά αποθήκευση του ενημερωμένου αρχείου. Στο τέλος θα μπορείτε να δημιουργήσετε ένα **bates numbering pdf** που φαίνεται επαγγελματικό, είτε επεξεργάζεστε ένα μόνο αρχείο είτε ολόκληρο φάκελο εγγράφων.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

- **.NET 6.0 ή νεότερο** – ο κώδικας στοχεύει στο .NET 6, αλλά λειτουργεί και με παλαιότερες εκδόσεις του .NET Framework.
- **Aspose.PDF for .NET** – εμπορική βιβλιοθήκη (διατίθεται δωρεάν δοκιμαστική έκδοση) που παρέχει τις κλάσεις `Document` και `BatesNumberingOptions` που χρησιμοποιούνται σε αυτόν τον οδηγό.
- Ένα **IDE C#** (Visual Studio, Rider ή VS Code) – οποιοσδήποτε επεξεργαστής που μπορεί να μεταγλωττίσει έργα .NET είναι αποδεκτός.
- Ένα αρχείο PDF εισόδου με όνομα `input.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικά σας.

Τα έχετε όλα; Τέλεια—ας ξεκινήσουμε.

## Προσθήκη Bates Αρίθμησης – Επισκόπηση

Η βασική ιδέα πίσω από την **add bates numbering** είναι να αντιμετωπίσουμε το PDF ως καμβά και να ζωγραφίσουμε μια συμβολοσειρά (π.χ. “DOC‑001”) στην κεφαλίδα ή στο υποσέλιδο κάθε σελίδας. Η Aspose.PDF κάνει το βαριά δουλειά: εσείς απλώς περιγράφετε τη μορφή, το εύρος σελίδων και το οπτικό στυλ, και η βιβλιοθήκη γράφει τους αριθμούς για εσάς.

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή console. Κάθε γραμμή εξηγείται, ώστε να καταλάβετε όχι μόνο *τι* να γράψετε, αλλά και *γιατί* κάθε στοιχείο είναι σημαντικό.

### Βήμα 1: Φόρτωση του Πηγαίου PDF Εγγράφου

Πρώτα χρειάζεται ένα αντικείμενο `Document` που να αντιπροσωπεύει το αρχείο που θέλουμε να τροποποιήσουμε.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Γιατί είναι σημαντικό:** Η κλάση `Document` είναι το σημείο εισόδου για όλες τις λειτουργίες PDF. Φορτώνει το αρχείο στη μνήμη, δίνοντάς σας πρόσβαση στη συλλογή `Pages`, την οποία θα διατρέξουμε αργότερα για την προσθήκη των αριθμών.

### Βήμα 2: Διαμόρφωση των Επιλογών Bates Αρίθμησης (προσαρμοσμένοι αριθμοί σελίδας)

Τώρα δημιουργούμε ένα αντικείμενο `BatesNumberingOptions`. Εδώ ορίζετε **custom page numbers**, τη γραμματοσειρά, τα χρώματα και τα περιθώρια.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – ο δείκτης `{0:D3}` λέει στην Aspose να συμπληρώνει τους αριθμούς με τρία ψηφία.
- **StartNumber** – από πού αρχίζει η ακολουθία· αλλάξτε το αν προσθέτετε αριθμούς σε υπάρχον πακέτο.
- **StartingPage / EndingPage** – ορίζουν το εύρος σελίδων· μπορείτε να το περιορίσετε στα 2‑5 για ένα υποσύνολο, παρέχοντας **sequential page numbers** μόνο όπου τα χρειάζεστε.
- **Font & Colors** – οπτικό στυλ για την **header footer numbering**· η Helvetica λειτουργεί καλά για νομικά έγγραφα επειδή είναι καθαρή και ευανάγνωστη.
- **Margin** – τοποθετεί το κείμενο 20 pts από τις άνω και δεξιές άκρες· προσαρμόστε αυτές τις τιμές για να μετακινήσετε τον αριθμό προς τα κάτω ή αριστερά, αν το επιθυμείτε.

> **Pro tip:** Αν θέλετε τους αριθμούς στο υποσέλιδο αντί για την κεφαλίδα, αλλάξτε τις τιμές του `Margin` σε κάτι όπως `new Margin(0, 0, 20, 20)` (κάτω, αριστερά).

### Βήμα 3: Εφαρμογή της Bates Αρίθμησης σε Ολόκληρο το Έγγραφο

Με τις επιλογές έτοιμες, η πραγματική εισαγωγή γίνεται με μία κλήση μεθόδου.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

Στο παρασκήνιο η Aspose διατρέχει τις επιλεγμένες σελίδες, μορφοποιεί κάθε αριθμό σύμφωνα με το `NumberingFormat` και σχεδιάζει τη συμβολοσειρά στον καμβά της σελίδας. Αυτό είναι το κέντρο της **add bates numbering**—χωρίς χειροκίνητο βρόχο.

### Βήμα 4: Αποθήκευση του PDF με τις Εφαρμοσμένες Bates Αριθμήσεις

Τέλος, γράψτε το τροποποιημένο έγγραφο πίσω στο δίσκο.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

Όταν ανοίξετε το `BatesNumbered.pdf` θα δείτε “DOC‑001”, “DOC‑002”, … τυπωμένα στην επάνω‑δεξιά γωνία κάθε σελίδας. Αυτό είναι ένα πλήρως λειτουργικό **bates numbering pdf** έτοιμο για αρχειοθέτηση ή e‑discovery.

## Αναμενόμενο Αποτέλεσμα

| Σελίδα | Κεφαλίδα (παράδειγμα) |
|--------|----------------------|
| 1      | DOC‑001 |
| 2      | DOC‑002 |
| …      | … |
| N      | DOC‑00N |

Οι αριθμοί εμφανίζονται ακριβώς εκεί που τα τοποθέτησε το `Margin`, χρησιμοποιώντας τη γραμματοσειρά Helvetica Bold 12‑pt. Αν ανοίξετε το αρχείο στο Adobe Acrobat, θα παρατηρήσετε ότι οι αριθμοί είναι μέρος του περιεχομένου της σελίδας—not a separate annotation—οπότε παραμένουν μετά την εκτύπωση και την εξομάλυνση.

## Περιπτώσεις Ορίων & Παραλλαγές

### Περιορισμός του Εύρους Σελίδων

Μερικές φορές θέλετε να αριθμήσετε μόνο ένα υποσύνολο, π.χ. τις σελίδες 3‑10 ενός συμβολαίου 25 σελίδων. Ρυθμίστε τα `StartingPage` και `EndingPage` ανάλογα:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Αλλαγή Τοποθέτησης σε Υποσέλιδο

Αν η ροή εργασίας σας απαιτεί **header footer numbering** στο κάτω αριστερό μέρος, τροποποιήστε το `Margin`:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Χρήση Διαφορετικής Μορφής

Οι νομικές ομάδες μερικές φορές χρησιμοποιούν “2024‑A‑001”. Απλώς αλλάξτε τη συμβολοσειρά μορφής:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Διαχείριση Διαφανών Υποβάθρων

Το `BackgroundColor = Color.Transparent` εξασφαλίζει ότι ο αριθμός δεν καλύπτει το υπάρχον περιεχόμενο. Αν χρειάζεστε ένα ανοιχτό γκρι πλαίσιο πίσω από το κείμενο για καλύτερη αναγνωσιμότητα, αντικαταστήστε το με `Color.LightGray`.

## Συχνές Ερωτήσεις (Απαντημένες)

- **Θα λειτουργήσει με PDF που είναι προστατευμένα με κωδικό;**  
  Ναι—φορτώστε το έγγραφο πρώτα με τον κωδικό (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`) και έπειτα εφαρμόστε τα ίδια βήματα.

- **Μπορώ να προσθέσω διαφορετικούς αριθμούς σε μονές και ζυγές σελίδες;**  
  Μπορείτε να εκτελέσετε το `AddBatesNumbering` δύο φορές με δύο ξεχωριστά `BatesNumberingOptions`, το καθένα να στοχεύει είτε στις μονές (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`) είτε στις ζυγές σελίδες.

- **Χρειάζομαι άδεια για το Aspose.PDF;**  
  Η δοκιμαστική έκδοση λειτουργεί για αξιολόγηση, αλλά προσθέτει υδατογράφημα. Για παραγωγική χρήση θα χρειαστείτε έγκυρη άδεια ώστε να λάβετε ένα καθαρό **bates numbering pdf**.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το αρχείο εξόδου και θα δείτε τους αριθμούς ακριβώς εκεί που ο κώδικας ζήτησε από την Aspose να τους τοποθετήσει. Χωρίς επιπλέον βρόχους, χωρίς χειροκίνητη σχεδίαση—απλώς **add bates numbering** σε τέσσερα συνοπτικά βήματα.

## Συμπέρασμα

Τώρα έχετε έναν ισχυρό, έτοιμο για παραγωγή τρόπο να **add bates numbering** σε οποιοδήποτε PDF χρησιμοποιώντας C# και Aspose.PDF. Από τη φόρτωση του εγγράφου μέχρι τη διαμόρφωση **custom page numbers**, την εφαρμογή **sequential page numbers**, και την αποθήκευση ενός καθαρού **bates numbering pdf**, όλο το workflow χωράει σε μία κλήση μεθόδου.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να συνδυάσετε αυτήν την τεχνική με άλλα χαρακτηριστικά της Aspose—όπως την προσθήκη λογότυπου, τη συγχώνευση πολλαπλών PDF ή την εξαγωγή σελίδων βάσει των αριθμών που μόλις προσθέσατε. Η εξερεύνηση της **header footer numbering** μαζί με υδατογραφήματα μπορεί να προσφέρει ακόμη περισσότερη ευελιξία.

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}