---
category: general
date: 2026-03-22
description: Προσθέστε γρήγορα αρίθμηση Bates σε PDF με το Aspose.Pdf. Μάθετε πώς
  να προσθέσετε Bates, να προσθέσετε διαδοχικούς αριθμούς σελίδων, να προσθέσετε προσαρμοσμένο
  υποσέλιδο σε PDF και να προσθέσετε αντικείμενο (artifact) σε PDF σε λίγα λεπτά.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: el
og_description: Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.Pdf. Αυτός
  ο οδηγός δείχνει πώς να προσθέσετε αρίθμηση Bates, διαδοχικούς αριθμούς σελίδων,
  προσαρμοσμένο υποσέλιδο PDF και αντικείμενο στο PDF.
og_title: Προσθήκη Bates Numbering σε PDF – Βήμα‑βήμα C# Οδηγός
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Προσθήκη αριθμησης Bates σε PDF – Πλήρης οδηγός C#
url: /el/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering σε PDF – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **add bates numbering pdf** σε μια δέσμη νομικών εγγράφων αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε οι πρώτοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δημιουργούν εργαλεία διαχείρισης υποθέσεων. Τα καλά νέα; Με το Aspose.Pdf μπορείτε να **add bates**, **add sequential page numbers**, και ακόμη **add custom footer pdf** στοιχεία με λίγες μόνο γραμμές κώδικα.  

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την εγκατάσταση της βιβλιοθήκης μέχρι την αποθήκευση του τελικού αρχείου, και θα προσθέσουμε συμβουλές για το πώς να **add artifact to pdf** αρχεία χωρίς να διασπάτε το υπάρχον περιεχόμενο. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Χρειαστείτε

- .NET 6+ (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework)  
- Ένα έγκυρο license Aspose.Pdf for .NET (μπορείτε να ξεκινήσετε με δωρεάν evaluation)  
- Ένα αρχείο PDF εισόδου (`input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε  
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή C# προτιμάτε  

Αυτό είναι όλο—δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από το Aspose.Pdf.

## Βήμα 1: Εγκατάσταση Aspose.Pdf μέσω NuGet

Πρώτα απ' όλα—ας φέρουμε τη βιβλιοθήκη στον υπολογιστή σας. Ανοίξτε ένα τερματικό στο φάκελο του project και εκτελέστε:

```bash
dotnet add package Aspose.Pdf
```

Ή, αν χρησιμοποιείτε το Package Manager Console του Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Μετά την εγκατάσταση, ελέγξτε διπλά ότι ο φάκελος `Aspose.Pdf` εμφανίζεται κάτω από `Dependencies → Packages` στον εξερευνητή λύσης.

## Βήμα 2: Φόρτωση του Πηγαίου PDF Εγγράφου

Τώρα δημιουργούμε ένα αντικείμενο `Document` που αντιπροσωπεύει το PDF που θέλουμε να σφραγίσουμε. Η χρήση της δήλωσης `using` εξασφαλίζει ότι ο χειριστής του αρχείου απελευθερώνεται αυτόματα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Γιατί να χρησιμοποιήσετε `using var`; Εγγυάται την απελευθέρωση ακόμη και αν προκύψει εξαίρεση, αποτρέποντας προβλήματα κλειδώματος αρχείου όταν προσπαθήσετε να αντικαταστήσετε το ίδιο αρχείο.

## Βήμα 3: Δημιουργία και Διαμόρφωση Bates Numbering Artifact

Ένας αριθμός Bates είναι ουσιαστικά ένα κείμενο artifact που βρίσκεται στη λογική δομή του PDF. Μπορείτε να το αντιμετωπίσετε όπως ένα **custom footer pdf** επειδή εμφανίζεται σε κάθε σελίδα χωρίς να αποτελεί μέρος του ρεύματος περιεχομένου της σελίδας.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Γιατί Αυτές οι Ρυθμίσεις Είναι Σημαντικές

- **Prefix**: Χρήσιμο για τη διάκριση τύπων εγγράφων (π.χ., “INV‑” για τιμολόγια).  
- **Start**: Ορίζει τον πρώτο αριθμό· μπορείτε να τον πάρετε από μια βάση δεδομένων αν χρειάζεστε συνέχεια μεταξύ αρχείων.  
- **Format**: `"0000"` εξαναγκάζει την εμφάνιση τεσσάρων ψηφίων, εξασφαλίζοντας ευθυγράμμιση όταν οι αριθμοί μεγαλώνουν.  
- **X/Y**: Οι συντεταγμένες μετρώνται από την κάτω‑αριστερή γωνία, έτσι `Y = 20` τοποθετεί το κείμενο ακριβώς πάνω από το περιθώριο της σελίδας. Ρυθμίστε το `X` αν θέλετε τον αριθμό αριστερά ή κεντραρισμένο.

Αν χρειάζεστε να **add sequential page numbers** αντί για αριθμούς Bates, απλώς παραλείψτε το `Prefix` και προσαρμόστε το `Format` σε `"###"` ή οποιοδήποτε μοτίβο προτιμάτε.

## Βήμα 4: Εφαρμογή του Artifact σε Όλες τις Σελίδες

Το Aspose.Pdf σας επιτρέπει να συνδέσετε ένα artifact σε ολόκληρο το έγγραφο με μία κλήση. Αυτός είναι ο πιο αποδοτικός τρόπος να **add artifact to pdf** χωρίς να κάνετε βρόχο σε κάθε σελίδα χειροκίνητα.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Πίσω από τη σκηνή, το Aspose προσθέτει το artifact στο λεξικό σελίδας κάθε σελίδας, πράγμα που σημαίνει ότι η αρίθμηση γίνεται μέρος της λογικής δομής του PDF—ιδανικό για μελλοντική εξαγωγή ή αναζήτηση.

## Βήμα 5: Αποθήκευση του Ενημερωμένου PDF

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να αποθηκεύσετε σε νέο αρχείο· το δεύτερο είναι πιο ασφαλές κατά την ανάπτυξη.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Όταν ανοίξετε το `output.pdf` σε έναν προβολέα, θα δείτε “INV‑1000”, “INV‑1001”, … στο κάτω‑δεξιό μέρος κάθε σελίδας.

### Επαλήθευση του Αποτελέσματος

Ανοίξτε το PDF σε Adobe Acrobat ή οποιονδήποτε προβολέα και ψάξτε για τους αριθμούς. Αν χρειάζεται να το επιβεβαιώσετε προγραμματιστικά, μπορείτε να διαβάσετε ξανά το artifact:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

## Περιπτώσεις Ορίων & Συχνές Ερωτήσεις

### Τι γίνεται αν το PDF μου έχει ήδη Footer;

Η προσθήκη ενός artifact δεν θα αντικαταστήσει υπάρχοντα footers επειδή τα artifacts βρίσκονται σε ξεχωριστό επίπεδο. Ωστόσο, αν η οπτική επικάλυψη είναι πρόβλημα, προσαρμόστε τη συντεταγμένη `Y` ή αυξήστε το offset `X` για να μετακινήσετε τον αριθμό Bates μακριά.

### Μπορώ να χρησιμοποιήσω διαφορετική γραμματοσειρά ή χρώμα;

Απολύτως. Το `BatesNumberingArtifact` κληρονομεί από το `Artifact`, έτσι μπορείτε να ορίσετε `Font`, `FontColor` και ακόμη `Opacity`. Παράδειγμα:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Πώς Επαναφέρω τον Μετρητή για Νέο Έγγραφο;

Απλώς αλλάξτε το `Start` πριν καλέσετε το `AddArtifact`. Αν δημιουργείτε πολλά PDFs σε βρόχο, διατηρήστε έναν τρέχοντα μετρητή στη λογική της εφαρμογής σας.

### Είναι Αυτή η Προσέγγιση Συμβατή με Κρυπτογραφημένα PDFs;

Το Aspose.Pdf μπορεί να ανοίξει κρυπτογραφημένα PDFs αν παρέχετε τον κωδικό πρόσβασης:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Μετά την αποκρυπτογράφηση, τα ίδια βήματα προσθήκης artifact λειτουργούν άψογα.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Επικολλήστε το σε μια console app, προσαρμόστε τις διαδρομές και πατήστε **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει “Bates numbering added successfully!” και το `output.pdf` περιέχει διαδοχικές ετικέτες όπως `INV‑1000`, `INV‑1001`, κ.λπ., τοποθετημένες στο κάτω‑δεξιό μέρος κάθε σελίδας.

## Σύντομη Ανακεφαλαίωση

- **Primary goal:** **add bates numbering pdf** using Aspose.Pdf.  
- Καλύψαμε **how to add bates**, **add sequential page numbers**, και **add custom footer pdf** στοιχεία μέσω ενός μόνο artifact.  
- Το tutorial έδειξε πώς να **add artifact to pdf**, να αντιμετωπίσετε edge cases, και να επαληθεύσετε το αποτέλεσμα.  

## Τι Ακολουθεί;

- **Dynamic prefixes:** Αντλήστε τιμές από μια βάση δεδομένων για να δημιουργήσετε “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Conditional placement:** Χρησιμοποιήστε ανίχνευση μεγέθους σελίδας (`page.MediaBox`) για να κεντράρετε τους αριθμούς σε οριζόντιες σελίδες.  
- **Combine with watermarks:** Προσθέστε ένα ημιδιαφανές λογότυπο δίπλα στον αριθμό Bates για branding.  

Νιώστε ελεύθεροι να πειραματιστείτε—ίσως ανακαλύψετε έναν πιο έξυπνο τρόπο για να επεξεργαστείτε χιλιάδες αρχεία μαζικά. Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο ή ελέγξτε τα επίσημα docs του Aspose (είναι εκπληκτικά σαφή). Καλή προγραμματιστική!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}