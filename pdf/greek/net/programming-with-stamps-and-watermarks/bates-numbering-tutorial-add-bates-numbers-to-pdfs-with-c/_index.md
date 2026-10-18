---
category: general
date: 2026-02-25
description: Εκπαιδευτικό Bates numbering – μάθετε πώς να προσθέτετε αριθμούς σελίδων
  σε PDF και να εφαρμόζετε προσαρμοσμένη αρίθμηση Bates χρησιμοποιώντας το Aspose.Pdf
  σε C#. Οδηγός βήμα‑βήμα με πλήρη κώδικα.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: el
og_description: Το tutorial Bates numbering σας δείχνει πώς να προσθέσετε αριθμούς
  σελίδων PDF και προσαρμοσμένη αρίθμηση Bates σε C#. Πλήρης κώδικας, εξηγήσεις και
  συμβουλές.
og_title: Οδηγός αριθμολόγησης Bates – Προσθήκη αριθμών Bates σε PDF με C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Μάθημα αρίθμησης Bates: Προσθήκη αριθμών Bates σε PDF με C#'
url: /el/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# bates numbering tutorial – Adding Bates Numbers to PDFs in C#

Έχετε αναρωτηθεί ποτέ πώς να προσθέσετε αριθμούς σελίδας σε PDF ενώ ταυτόχρονα ενσωματώνετε έναν νομικό‑στυλ αριθμό Bates; Δεν είστε μόνοι. Σε αυτό το **bates numbering tutorial** θα περάσουμε από όλα όσα χρειάζεται να γνωρίζετε για να σφραγίσετε κάθε σελίδα ενός PDF με προσαρμοσμένο πρόθεμα, μηδενικά μπροστά και ακριβή τοποθέτηση — χρησιμοποιώντας το Aspose.Pdf για .NET.

Τα καλά νέα; Είναι αρκετά απλό μόλις κατανοήσετε τις βασικές έννοιες. Στο τέλος αυτού του οδηγού θα έχετε ένα εκτελέσιμο πρόγραμμα που παίρνει το *input.pdf* και παράγει το *bates_out.pdf* με μια κομψή ετικέτα τύπου “ABC‑01000” σε κάθε σελίδα. Ας βουτήξουμε.

## What You’ll Need

- **Aspose.Pdf for .NET** (έκδοση 23.10 ή νεότερη). Η βιβλιοθήκη είναι εμπορική, αλλά μια δωρεάν δοκιμή λειτουργεί τέλεια για εκμάθηση.
- .NET 6+ SDK (οποιαδήποτε πρόσφατη έκδοση αρκεί).
- Ένα βασικό περιβάλλον ανάπτυξης C# — Visual Studio, VS Code ή Rider.
- Ένα PDF εισόδου για πειραματισμό (οποιοδήποτε πολυ‑σελιδικό έγγραφο θα δείξει το αποτέλεσμα).

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το Aspose.Pdf, και ο κώδικας εκτελείται σε Windows, Linux ή macOS χωρίς τροποποίηση.

## Step 1: Load the Source PDF Document (bates numbering tutorial – initialization)

Πρώτα δημιουργούμε ένα αντικείμενο `Document` που αντιπροσωπεύει το PDF που θέλουμε να τροποποιήσουμε. Σκεφτείτε το ως φόρτωση ενός κεννού καμβά που μπορείτε να σχεδιάσετε.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Why this matters:** Χωρίς τη φόρτωση του αρχείου, δεν υπάρχει τίποτα προς σχολιασμό. Ο έλεγχος εγκυρότητας αποτρέπει μια σιωπηλή αποτυχία αργότερα όταν προσπαθήσετε να προσθέσετε αντικείμενα σε μια μη‑υπάρχουσα συλλογή σελίδων.

## Step 2: Define the Bates Numbering Artifact (how to add bates)

Ένα *BatesNumberingArtifact* λέει στο Aspose πού και πώς να σχεδιάσει το αναγνωριστικό. Μπορείτε να ελέγξετε το πρόθεμα, τον αριθμό εκκίνησης, την προσθήκη μηδενικών, το μέγεθος γραμματοσειράς και τις ακριβείς συντεταγμένες X/Y.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Why this matters:** Η ιδιότητα `LeadingZeros` εξασφαλίζει ότι κάθε ετικέτα έχει το ίδιο μήκος, κάτι κρίσιμο για νομικά έγγραφα όπου η στοίχιση μετράει. Ρυθμίστε το `X` και το `Y` για να μετακινήσετε τη σφραγίδα στην πάνω‑δεξιά, κάτω‑αριστερά ή όπου απαιτεί η ροή εργασίας σας.

## Step 3: Attach the Artifact to Every Page (add page numbers pdf)

Τώρα κάνουμε βρόχο σε κάθε σελίδα και προσθέτουμε το ίδιο αντικείμενο. Εδώ εκπληρώνεται η απαίτηση *add page numbers pdf* — κάθε σελίδα λαμβάνει τη δική της διαδοχική ετικέτα αυτόματα.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Why this matters:** Προσθέτοντας το αντικείμενο στη συλλογή `Artifacts` αντί να σχεδιάζετε κείμενο χειροκίνητα, αφήνουμε το Aspose να διαχειριστεί τη λογική αρίθμησης, τα μηδενικά μπροστά και την απόδοση. Αυτό μειώνει σφάλματα και κρατά τον κώδικα σύντομο.

## Step 4: Save the Modified PDF (add bates numbering)

Τέλος, αποθηκεύουμε τις αλλαγές σε νέο αρχείο. Είναι καλή πρακτική να γράφετε σε διαφορετικό όνομα αρχείου ώστε το πρωτότυπο να παραμένει άθικτο.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Why this matters:** Η μέθοδος `Save` γράφει ολόκληρο το PDF, ενσωματώνοντας τα αντικείμενα ως μέρος του ρεύματος περιεχομένου της σελίδας. Το παραγόμενο αρχείο μπορεί να ανοιχθεί σε οποιονδήποτε προβολέα PDF και θα εμφανίζει τους αριθμούς Bates ακριβώς όπως ορίστηκαν.

## Full Working Example (All Steps Combined)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το σε ένα έργο κονσόλας, αντικαταστήστε τις διαδρομές placeholder και πατήστε **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Expected Result

Ανοίξτε το *bates_out.pdf* στο Adobe Reader, Foxit ή οποιονδήποτε προβολέα. Θα πρέπει να δείτε μια ετικέτα όπως **ABC‑01000** στην πρώτη σελίδα, **ABC‑01001** στη δεύτερη, κ.ο.κ., τοποθετημένη 50 pts από την αριστερή άκρη και 30 pts από το κάτω μέρος. Οι αριθμοί είναι δεξιά‑στοιχισμένοι λόγω των μηδενικών μπροστά, δίνοντας στο έγγραφο μια καθαρή, επαγγελματική εμφάνιση.

## Common Variations & Edge Cases

| Scenario | How to Adjust |
|----------|---------------|
| **Different prefix** | Change `Prefix = "XYZ"` in the artifact definition. |
| **Start at a custom number** | Set `Start = 5000` (or any integer). |
| **Place the number in the top‑right corner** | Use `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Change font size for larger documents** | Modify `FontSize = 12` (or any size). |
| **Add a background rectangle** | Create a `RectangleArtifact` and add it before the `BatesNumberingArtifact`. |
| **Skip certain pages** | Inside the `foreach` loop, add an `if (page.Number % 2 == 0) continue;` to skip even pages. |

**Pro tip:** Πάντα δοκιμάζετε πρώτα με ένα μικρό PDF. Είναι πιο γρήγορο να επαληθεύσετε τη θέση πριν τρέξετε το σενάριο σε ένα αρχείο 200‑σελίδων.

## Frequently Asked Questions

- **Does this work with encrypted PDFs?**  
  Aspose.Pdf can open password‑protected files if you provide the password via `Document(string, string)`. The Bates artifact will still be applied after decryption.

- **Can I add both Bates numbers and regular page numbers?**  
  Yes. Add a `PageNumberArtifact` alongside the `BatesNumberingArtifact`. Each artifact maintains its own counter.

- **What if my PDF has different page sizes?**  
  The `Position` values are absolute points. For mixed‑size documents, compute the position per page inside the loop using `page.PageInfo.Width` and `page.PageInfo.Height`.

## Next Steps & Related Topics

Τώρα που έχετε κατακτήσει το **bates numbering tutorial**, ίσως θέλετε να εξερευνήσετε:

- **Adding watermarks** – similar artifact approach with `TextArtifact`.
- **Merging multiple PDFs** – use `Document.AppendDocument`.
- **Extracting text for search indexing** – `TextAbsorber` class.
- **Automating batch processing** – loop over a folder of PDFs and apply the same artifact.

Όλα αυτά τα θέματα βασίζονται στις ίδιες έννοιες που μόλις μάθατε, οπότε είστε έτοιμοι να επεκτείνετε το σύνολο εργαλείων αυτοματοποίησης PDF σας.

---

*Happy coding! If you hit any snags or have ideas for further customization, feel free to drop a comment below. The world of PDF manipulation is vast, but with a solid **bates numbering tutorial** under your belt, you’re already ahead of the curve.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}