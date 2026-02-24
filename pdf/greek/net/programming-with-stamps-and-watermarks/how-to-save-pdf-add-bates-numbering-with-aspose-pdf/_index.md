---
category: general
date: 2026-02-23
description: Πώς να αποθηκεύσετε αρχεία PDF προσθέτοντας αρίθμηση Bates και τεχνικά
  αντικείμενα χρησιμοποιώντας το Aspose.Pdf σε C#. Οδηγός βήμα‑βήμα για προγραμματιστές.
draft: false
keywords:
- how to save pdf
- how to add bates
- how to add artifact
- create pdf document
- add bates numbering
language: el
og_description: Πώς να αποθηκεύσετε αρχεία PDF προσθέτοντας αριθμήσεις Bates και στοιχεία
  με το Aspose.Pdf σε C#. Μάθετε τη πλήρη λύση σε λίγα λεπτά.
og_title: Πώς να αποθηκεύσετε PDF — Προσθέστε αρίθμηση Bates με το Aspose.Pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Πώς να αποθηκεύσετε PDF — Προσθήκη αρίθμησης Bates με το Aspose.Pdf
url: /el/net/programming-with-stamps-and-watermarks/how-to-save-pdf-add-bates-numbering-with-aspose-pdf/
---

If" keep as is? It's incomplete. Keep as is.

Now ensure we keep all shortcodes at start and end.

Let's construct final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αποθηκεύσετε PDF — Προσθήκη Αρίθμησης Bates με Aspose.Pdf

Σας έχει τύχει ποτέ να αναρωτηθείτε **how to save PDF** αρχεία μετά την σήμανσή τους με αριθμό Bates; Δεν είστε ο μόνος. Σε νομικά γραφεία, δικαστήρια και ακόμη και σε εσωτερικές ομάδες συμμόρφωσης, η ανάγκη ενσωμάτωσης ενός μοναδικού αναγνωριστικού σε κάθε σελίδα αποτελεί καθημερινό πρόβλημα. Τα καλά νέα; Με το Aspose.Pdf για .NET μπορείτε να το κάνετε σε λίγες γραμμές, και θα έχετε ένα τέλεια αποθηκευμένο PDF που περιέχει την αρίθμηση που απαιτείτε.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση ενός υπάρχοντος PDF, προσθήκη ενός *artifact* αρίθμησης Bates, και τέλος **how to save PDF** σε νέα τοποθεσία. Καθ' όλη τη διάρκεια θα αγγίξουμε επίσης **how to add bates**, **how to add artifact**, και θα συζητήσουμε το ευρύτερο θέμα του **create PDF document** προγραμματιστικά. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Πακέτο NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Ένα δείγμα PDF (`input.pdf`) τοποθετημένο σε φάκελο με δικαιώματα ανάγνωσης/εγγραφής
- Βασική εξοικείωση με τη σύνταξη C# — δεν απαιτείται βαθιά γνώση PDF

> **Συμβουλή:** Αν χρησιμοποιείτε Visual Studio, ενεργοποιήστε *nullable reference types* για μια πιο καθαρή εμπειρία κατά τη μεταγλώττιση.

---

## Πώς να Αποθηκεύσετε PDF με Αρίθμηση Bates

Ο πυρήνας της λύσης χωρίζεται σε τρία απλά βήματα. Κάθε βήμα είναι περιτυλιγμένο σε δικό του H2 τίτλο ώστε να μπορείτε να μεταβείτε απευθείας στο τμήμα που χρειάζεστε.

### Βήμα 1 – Φόρτωση του Πηγαίου PDF Εγγράφου

Πρώτα, πρέπει να φέρουμε το αρχείο στη μνήμη. Η κλάση `Document` του Aspose.Pdf αντιπροσωπεύει ολόκληρο το PDF, και μπορείτε να την δημιουργήσετε απευθείας από διαδρομή αρχείου.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

namespace BatesNumberDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the source PDF document
            string inputPdfPath = @"C:\MyDocs\input.pdf";

            // The Document constructor throws if the file is missing, so wrap it in a try/catch if you need resilience.
            using (var pdfDocument = new Document(inputPdfPath))
            {
                // The rest of the workflow continues inside this using block.
```

**Γιατί αυτό είναι σημαντικό:** Η φόρτωση του αρχείου είναι το μόνο σημείο όπου μπορεί να αποτύχει η I/O. Διατηρώντας τη δήλωση `using` εξασφαλίζουμε ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα — κρίσιμο όταν αργότερα **how to save pdf** ξαναγράψετε το αρχείο στον δίσκο.

### Βήμα 2 – Πώς να Προσθέσετε Αρίθμηση Bates Artifact

Οι αριθμοί Bates τοποθετούνται συνήθως στην κεφαλίδα ή στο υποσέλιδο κάθε σελίδας. Το Aspose.Pdf παρέχει την κλάση `BatesNumberArtifact`, η οποία αυξάνει αυτόματα τον αριθμό για κάθε σελίδα στην οποία την προσθέτετε.

```csharp
                // 👉 Step 2: Add a Bates number artifact to the first page (you could loop for all pages)
                var batesArtifact = new BatesNumberArtifact
                {
                    // The Text property can contain a format string. "{0}" will be replaced by the page number.
                    Text = "Case-2026-{0}",
                    Position = new Position(50, 50), // X=50pt, Y=50pt from the bottom‑left corner
                    Font = FontRepository.FindFont("Helvetica"),
                    FontSize = 12,
                    // Optional: set color, opacity, etc.
                };

                // Attach the artifact to the first page; Aspose will replicate it on subsequent pages automatically.
                pdfDocument.Pages[1].Artifacts.Add(batesArtifact);
```

**Πώς να προσθέσετε bates** σε όλο το έγγραφο; Αν θέλετε το artifact σε *κάθε* σελίδα, απλώς προσθέστε το στην πρώτη σελίδα όπως φαίνεται — το Aspose διαχειρίζεται την εξάπλωση. Για πιο λεπτομερή έλεγχο μπορείτε να επαναλάβετε το `pdfDocument.Pages` και να προσθέσετε ένα προσαρμοσμένο `TextFragment`, αλλά το ενσωματωμένο artifact είναι το πιο σύντομο.

### Βήμα 3 – Πώς να Αποθηκεύσετε PDF σε Νέα Τοποθεσία

Τώρα που το PDF περιέχει την αρίθμηση Bates, ήρθε η ώρα να το γράψετε ξανά. Εδώ ξαναφαίνεται η κύρια λέξη‑κλειδί: **how to save pdf** μετά τις τροποποιήσεις.

```csharp
                // 👉 Step 3: Save the updated PDF to the desired location
                string outputPdfPath = @"C:\MyDocs\output.pdf";

                // Overwrite if the file already exists; you can also check File.Exists first.
                pdfDocument.Save(outputPdfPath);
                Console.WriteLine($"PDF saved successfully to {outputPdfPath}");
            } // using block disposes the Document
        }
    }
}
```

Όταν ολοκληρωθεί η μέθοδος `Save`, το αρχείο στον δίσκο περιέχει τον αριθμό Bates σε κάθε σελίδα, και μόλις μάθατε **how to save pdf** με ένα προσαρτημένο artifact.

---

## Πώς να Προσθέσετε Artifact σε PDF (Πέρα από Bates)

Μερικές φορές χρειάζεστε ένα γενικό υδατογράφημα, ένα λογότυπο ή μια προσαρμοσμένη σημείωση αντί για αριθμό Bates. Η ίδια συλλογή `Artifacts` λειτουργεί για οποιοδήποτε οπτικό στοιχείο.

```csharp
// Example: Adding a simple text watermark artifact
var watermark = new TextArtifact
{
    Text = "CONFIDENTIAL",
    Position = new Position(200, 400),
    Font = FontRepository.FindFont("Arial"),
    FontSize = 36,
    Color = Color.FromRgb(255, 0, 0),
    Opacity = 0.3
};
pdfDocument.Pages[1].Artifacts.Add(watermark);
```

**Γιατί να χρησιμοποιήσετε artifact;** Τα artifacts είναι αντικείμενα *μη‑περιεχομένου*, που σημαίνει ότι δεν παρεμβαίνουν στην εξαγωγή κειμένου ή στις δυνατότητες προσβασιμότητας του PDF. Γι' αυτό είναι η προτιμώμενη μέθοδος για ενσωμάτωση αριθμών Bates, υδατογραφημάτων ή οποιουδήποτε επικάλυψης που πρέπει να παραμένει αόρατη στις μηχανές αναζήτησης.

---

## Δημιουργία PDF Εγγράφου από το Μηδέν (Αν Δεν Έχετε Είσοδο)

Τα προηγούμενα βήματα υποθέτουν υπάρχον αρχείο, αλλά μερικές φορές χρειάζεται να **create PDF document** από το μηδέν πριν μπορέσετε να **add bates numbering**. Εδώ είναι ένα μινιμαλιστικό παράδειγμα εκκίνησης:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a fresh PDF document
var newDoc = new Document();
Page page = newDoc.Pages.Add();

// Add a simple paragraph
var paragraph = new TextFragment("Hello, this is a newly created PDF.");
page.Paragraphs.Add(paragraph);

// Save it
newDoc.Save(@"C:\MyDocs\newfile.pdf");
```

Από εδώ μπορείτε να επαναχρησιμοποιήσετε το snippet **how to add bates** και τη ρουτίνα **how to save pdf** για να μετατρέψετε έναν κενό καμβά σε πλήρως σημειωμένο νομικό έγγραφο.

---

## Συχνές Περιπτώσεις & Συμβουλές

| Κατάσταση | Τι να προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|-------------------|---------------|
| **Το εισερχόμενο PDF δεν έχει σελίδες** | `pdfDocument.Pages[1]` πετάει εξαίρεση εκτός ορίων. | Επαληθεύστε ότι `pdfDocument.Pages.Count > 0` πριν προσθέσετε artifacts, ή δημιουργήστε πρώτα μια νέα σελίδα. |
| **Πολλές σελίδες χρειάζονται διαφορετικές θέσεις** | Ένα artifact εφαρμόζει τις ίδιες συντεταγμένες σε κάθε σελίδα. | Επαναλάβετε το `pdfDocument.Pages` και προσθέστε `Artifacts.Add` ανά σελίδα με προσαρμοσμένη `Position`. |
| **Μεγάλα PDF (εκατοντάδες MB)** | Πίεση μνήμης ενώ το έγγραφο παραμένει στη RAM. | Χρησιμοποιήστε `PdfFileEditor` για τροποποιήσεις εντός του αρχείου, ή επεξεργαστείτε τις σελίδες σε παρτίδες. |
| **Προσαρμοσμένη μορφή Bates** | Θέλετε πρόθεμα, επίθημα ή αριθμούς με μηδενικά. | Ορίστε `Text = "DOC-{0:0000}"` — το `{0}` σέβεται τις μορφές .NET. |
| **Αποθήκευση σε φάκελο μόνο για ανάγνωση** | `Save` πετάει `UnauthorizedAccessException`. | Βεβαιωθείτε ότι ο προορισμός έχει δικαιώματα εγγραφής, ή ζητήστε από τον χρήστη εναλλακτική διαδρομή. |

---

## Αναμενόμενο Αποτέλεσμα

Μετά την εκτέλεση του πλήρους προγράμματος:

1. Το `output.pdf` εμφανίζεται στο `C:\MyDocs\`.
2. Ανοίγοντάς το σε οποιονδήποτε προβολέα PDF, εμφανίζεται το κείμενο **“Case-2026-1”**, **“Case-2026-2”**, κ.λπ., τοποθετημένο 50 pt από τα αριστερά και κάτω άκρα σε κάθε σελίδα.
3. Αν προσθέσατε το προαιρετικό artifact υδατογραφήματος, η λέξη **“CONFIDENTIAL”** εμφανίζεται ημιδιαφανής πάνω από το περιεχόμενο.

Μπορείτε να επαληθεύσετε τους αριθμούς Bates επιλέγοντας το κείμενο (είναι επιλέξιμο επειδή είναι artifacts) ή χρησιμοποιώντας ένα εργαλείο επιθεώρησης PDF.

---

## Ανακεφαλαίωση – Πώς να Αποθηκεύσετε PDF με Αρίθμηση Bates σε Ένα Βήμα

- **Φορτώστε** το πηγαίο αρχείο με `new Document(path)`.
- **Προσθέστε** ένα `BatesNumberArtifact` (ή οποιοδήποτε άλλο artifact) στην πρώτη σελίδα.
- **Αποθηκεύστε** το τροποποιημένο έγγραφο χρησιμοποιώντας `pdfDocument.Save(destinationPath)`.

Αυτή είναι η πλήρης απάντηση στο **how to save pdf** ενώ ενσωματώνετε ένα μοναδικό αναγνωριστικό. Χωρίς εξωτερικά scripts, χωρίς χειροκίνητη επεξεργασία σελίδων — μόνο μια καθαρή, επαναχρησιμοποιήσιμη μέθοδος C#.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Προσθήκη αρίθμησης Bates σε κάθε σελίδα χειροκίνητα** – επαναλάβετε το `pdfDocument.Pages` για προσαρμογές ανά σελίδα.
- **Πώς να προσθέσετε artifact** για εικόνες: αντικαταστήστε το `TextArtifact` με `ImageArtifact`.
- **Create PDF document** με πίνακες, διαγράμματα ή πεδία φόρμας χρησιμοποιώντας το πλούσιο API του Aspose.Pdf.
- **Αυτοματοποίηση επεξεργασίας παρτίδας** – διαβάστε έναν φάκελο PDF, εφαρμόστε την ίδια αρίθμηση Bates, και αποθηκεύστε τα μαζικά.

Πειραματιστείτε με διαφορετικές γραμματοσειρές, χρώματα και θέσεις. Η βιβλιοθήκη Aspose.Pdf είναι εξαιρετικά ευέλικτη, και μόλις κυριαρχήσετε στο **how to add bates** και **how to add artifact**, οι δυνατότητες είναι απεριόριστες.

---

### Γρήγορος Κώδικας Αναφοράς (Όλα τα Βήματα σε Ένα Block)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

class BatesDemo
{
    static void Main()
    {
        string inputPath = @"C:\MyDocs\input.pdf";
        string outputPath = @"C:\MyDocs\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var bates = new BatesNumberArtifact
            {
                Text = "Case-2026-{0}",
                Position = new Position(50, 50),
                Font = FontRepository.FindFont("Helvetica"),
                FontSize = 12
            };
            pdf.Pages[1].Artifacts.Add(bates);
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Saved PDF with Bates number to {outputPath}");
    }
}
```

Εκτελέστε αυτό το snippet και θα έχετε μια σταθερή βάση για οποιοδήποτε μελλοντικό έργο αυτοματοποίησης PDF.

---

*Happy coding! If

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}