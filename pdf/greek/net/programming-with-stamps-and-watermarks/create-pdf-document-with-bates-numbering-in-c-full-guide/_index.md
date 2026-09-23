---
category: general
date: 2026-03-06
description: Δημιουργήστε έγγραφο PDF σε C# και προσθέστε εύκολα αριθμό Bates. Μάθετε
  πώς να προσθέσετε κενή σελίδα PDF, να τοποθετήσετε σφραγίδα στη σελίδα και να υλοποιήσετε
  την αρίθμηση Bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: el
og_description: Δημιουργήστε έγγραφο PDF σε C# και προσθέστε αριθμό Bates. Αυτός ο
  οδηγός δείχνει πώς να προσθέσετε κενή σελίδα PDF, να τοποθετήσετε σφραγίδα στη σελίδα
  και να εφαρμόσετε αρίθμηση Bates.
og_title: Δημιουργία εγγράφου PDF με αριθμητική Bates – Οδηγός C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Δημιουργία εγγράφου PDF με αριθμήσεις Bates σε C# – Πλήρης οδηγός
url: /el/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου PDF με αρίθμηση Bates σε C#

Έχετε ποτέ χρειαστεί να **create PDF document** σε C# και αναρωτηθήκατε πώς να προσθέσετε έναν αριθμό Bates χωρίς να τρελαθείτε; Δεν είστε οι μόνοι—γραφεία δικηγόρων, δικαστήρια και ακόμη ορισμένες ομάδες εταιρικής συμμόρφωσης αντιμετωπίζουν ακριβώς αυτό το πρόβλημα καθημερινά. Τα καλά νέα; Με μερικές γραμμές κώδικα Aspose.Pdf μπορείτε να δημιουργήσετε ένα ολοκαίνουργιο PDF, να προσθέσετε μια κενή σελίδα και να σφραγίσετε έναν σωστό αριθμό Bates σε μία ομαλή ροή.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη ρύθμιση του έργου, στην προσθήκη ενός κενό PDF σελίδας, στην κατανόηση του **how to add bates numbering**, και τέλος στο **place stamp on page** και την αποθήκευση του αποτελέσματος. Στο τέλος θα έχετε ένα έτοιμο προς χρήση snippet που μπορείτε να ενσωματώσετε σε οποιαδήποτε εφαρμογή .NET. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα.

## Τι θα χρειαστείτε

- **.NET 6+** (ή .NET Framework 4.6+ – το Aspose.Pdf λειτουργεί και με τα δύο)
- **Aspose.Pdf for .NET** πακέτο NuGet (`Install-Package Aspose.Pdf`)
- Ένα καλό IDE (Visual Studio, Rider ή VS Code με επέκταση C#)

Αυτό είναι όλο. Χωρίς επιπλέον DLLs, χωρίς εξωτερικές υπηρεσίες. Ας βουτήξουμε.

## Βήμα 1: Δημιουργία PDF Εγγράφου – Αρχική Ρύθμιση

Πρώτα απ' όλα, χρειαζόμαστε ένα νέο αντικείμενο `Document`. Σκεφτείτε το ως το κενό καμβά όπου θα ζήσει ό,τι άλλο.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Why this matters:** Η κλάση `Document` είναι το σημείο εισόδου για κάθε λειτουργία του Aspose. Η δημιουργία της σας δίνει πρόσβαση στη συλλογή `Pages`, τα μεταδεδομένα και τις ρυθμίσεις ασφαλείας—όλα τα δομικά στοιχεία για ένα επαγγελματικό PDF.

## Βήμα 2: Προσθήκη κενής σελίδας PDF

Ένα PDF χωρίς σελίδες είναι σαν ένα βιβλίο χωρίς σελίδες—αρκετά άχρηστο. Η προσθήκη μιας κενής σελίδας είναι απλή και μας παρέχει μια επιφάνεια για να σφραγίσουμε τον αριθμό Bates.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Pro tip:** Αν χρειάζεστε πολλαπλές σελίδες, απλώς καλέστε `pdfDocument.Pages.Add()` σε βρόχο. Κάθε κλήση επιστρέφει ένα νέο αντικείμενο `Page` που μπορείτε να προσαρμόσετε ανεξάρτητα.

## Βήμα 3: Πώς να προσθέσετε αρίθμηση Bates – Δημιουργία του TextStamp

Τώρα έρχεται η ουσία: ο **Bates number**. Στο Aspose.Pdf είναι απλώς ένα `TextStamp` με ειδική σημαία artifact.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Why we set `Artifact`**: Ορισμένα προγράμματα ανάγνωσης PDF εκθέτουν τους αριθμούς Bates ως αναζητήσιμα μεταδεδομένα. Η σημαία του σφραγίσματος ως artifact `BatesNumbering` εξασφαλίζει ότι τα επόμενα εργαλεία θα το αναγνωρίσουν αυτόματα.

## Βήμα 4: Τοποθέτηση σφραγίσματος στη σελίδα

Με το σφραγίδιο έτοιμο, τώρα **place stamp on page**. Αυτό είναι το βήμα όπου ο οπτικός αριθμός εμφανίζεται πραγματικά στο PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Edge case:** Αν χρειάζεστε τον αριθμό να αυξάνεται σε κάθε σελίδα, θα επαναλάβετε το `pdfDocument.Pages` και θα ενημερώσετε το `batesStamp.Value` πριν καλέσετε το `AddStamp`. Το παράδειγμα εδώ το κρατά απλό με ένα στατικό “Bates‑001”.

## Βήμα 5: Αποθήκευση και επαλήθευση του αποτελέσματος

Τέλος, αποθηκεύουμε το PDF στο δίσκο. Επιλέξτε έναν φάκελο στον οποίο έχετε δικαίωμα εγγραφής· διαφορετικά, θα αντιμετωπίσετε `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Όταν ανοίξετε το `BatesStamped.pdf` σε οποιονδήποτε προβολέα, θα πρέπει να δείτε ένα μικρό “Bates‑001” τοποθετημένο κομψά στην κάτω‑δεξιά γωνία της κενής σελίδας.

> **Expected output:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Κείμενο alt: PDF με σφραγίδα αριθμού Bates στην κάτω‑δεξιά γωνία.*

Αν ο αριθμός δεν εμφανίζεται, ελέγξτε ξανά τις τιμές περιθωρίων και βεβαιωθείτε ότι το μέγεθος της σελίδας δεν είναι πολύ μικρό (το προεπιλεγμένο A4 λειτουργεί καλά). Επίσης, επιβεβαιώστε ότι η σημαία `Artifact` δεν αφαιρείται από κανένα εργαλείο μετα-επεξεργασίας.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα. Περιλαμβάνει όλες τις οδηγίες `using` και σχόλια για να παραμείνετε προσανατολισμένοι.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το PDF, και θα δείτε τον αριθμό Bates ακριβώς εκεί που του είχαμε πει να τοποθετηθεί. 🎉

## Συνηθισμένες παραλλαγές & παγίδες

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Multiple pages, incrementing numbers** | Loop through `pdfDocument.Pages`, set `batesStamp.Value = $"Bates-{i:D3}"` before `AddStamp` | Δίνει σε κάθε σελίδα ένα μοναδικό αναγνωριστικό, τυπικό για νομικά πακέτα |
| **Different placement (top‑left)** | Change `HorizontalAlignment = HorizontalAlignment.Left` and `VerticalAlignment = VerticalAlignment.Top` | Κάποιες οργανώσεις προτιμούν τον αριθμό στην κεφαλίδα αντί στο υποσέλιδο |
| **Custom font or color** | Set `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Βελτιώνει την αναγνωσιμότητα ή συμμορφώνεται με τις οδηγίες branding |
| **Adding an existing PDF as a background** | Load the source PDF with `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Χρήσιμο όταν χρειάζεται να σφραγίσετε πάνω σε μια προ‑δημιουργημένη φόρμα |

## Συμπεράσματα

Μόλις δείξαμε πώς να **create PDF document**, **add blank page pdf**, και **add bates number** χρησιμοποιώντας το Aspose.Pdf για .NET, στη συνέχεια **place stamp on page** και να αποθηκεύσετε το αρχείο. Ο κώδικας είναι σκόπιμα συνοπτικός ώστε να μπορείτε να τον προσαρμόσετε σε μεγαλύτερες ροές εργασίας—είτε επεξεργάζεστε δεκάδες αρχεία είτε το ενσωματώνετε σε μια υπηρεσία web.

Αν είστε έτοιμοι να προχωρήσετε παραπέρα, σκεφτείτε:

- Αυτοματοποίηση της λογικής αύξησης για μεγάλα αρχεία υποθέσεων.
- Ενσωμάτωση της δημιουργίας PDF σε ένα ASP.NET Core API.
- Προσθήκη ασφαλείας (προστασία με κωδικό) με `pdfDocument.Encrypt(...)`.

Μη διστάσετε να πειραματιστείτε, να σπάσετε πράγματα, και να θέσετε ερωτήσεις στα σχόλια. Καλή προγραμματιστική, και εύχομαι τα PDF σας να είναι πάντα τέλεια σφραγισμένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}