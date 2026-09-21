---
category: general
date: 2026-03-03
description: Προσθέστε γρήγορα αριθμήση Bates σε PDF και μάθετε πώς να αριθμείτε τις
  σελίδες PDF ή να προσθέτετε διαδοχικούς αριθμούς PDF χρησιμοποιώντας το Aspose.Pdf
  σε C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: el
og_description: Προσθέστε αριθμολόγηση Bates σε PDF με C# για την αρίθμηση των σελίδων
  PDF και την προσθήκη διαδοχικών αριθμών PDF. Πλήρης κώδικας, εξηγήσεις και βέλτιστες
  πρακτικές.
og_title: Προσθήκη Αρίθμησης Bates σε PDF – Πλήρες Μάθημα C#
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Προσθήκη αριθμησης Bates PDF – Οδηγός βήμα‑βήμα για την αρίθμηση των σελίδων
  PDF
url: /el/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering PDF – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **add bates numbering pdf** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος—νομικές ομάδες, ελεγκτές και αρχειοθέτες αντιμετωπίζουν το ίδιο πρόβλημα. Τα καλά νέα; Με λίγες γραμμές C# και τη βιβλιοθήκη Aspose.Pdf μπορείτε να **number pdf pages** αυτόματα, και θα έχετε ακόμη την ευελιξία να **add sequential pdf numbers** με προσαρμοσμένα πρόθεμα, επίθημα και θέση.

Σε αυτόν τον οδηγό θα περάσουμε από ένα πραγματικό παράδειγμα, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική, και θα σας δείξουμε πώς να προσαρμόσετε τον κώδικα για ειδικές περιπτώσεις όπως διαφορετικά μεγέθη σελίδας ή προσαρμοσμένοι αριθμοί ψηφίων. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση snippet που προσθέτει Bates numbers σε οποιοδήποτε PDF του δώσετε, και θα κατανοήσετε το «γιατί» πίσω από κάθε επιλογή.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Έγκυρη άδεια Aspose.Pdf for .NET (ή δωρεάν κλειδί αξιολόγησης)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή C# προτιμάτε)
- Ένα PDF πηγής με όνομα `source.pdf` σε φάκελο που μπορείτε να αναφέρετε

Αυτό είναι όλο—δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από το Aspose.Pdf.

## Βήμα 1 – Άνοιγμα του PDF Εγγράφου Πηγής

Το πρώτο που πρέπει να κάνετε είναι να φορτώσετε το PDF που θέλετε να σφραγίσετε. Η χρήση ενός μπλοκ `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται σωστά, αποτρέποντας προβλήματα κλειδώματος αργότερα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Γιατί είναι σημαντικό:** Το άνοιγμα του εγγράφου μέσα σε δήλωση `using` εξασφαλίζει καθοριστική απελευθέρωση. Αν το παραλείψετε, το αρχείο μπορεί να παραμείνει κλειδωμένο, και οι επόμενες προσπάθειες αποθήκευσης ή διαγραφής του PDF θα αποτύχουν—κάτι που έχω δει να προκαλεί προβλήματα σε παραγωγικές γραμμές.

## Βήμα 2 – Διαμόρφωση Επιλογών Bates Numbering

Τώρα λέμε στο Aspose πώς θέλουμε να εμφανίζονται οι Bates numbers. Κάθε ιδιότητα αντιστοιχεί άμεσα σε ένα οπτικό στοιχείο στη σελίδα.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Γρήγορες συμβουλές για τις επιλογές

| Ιδιότητα | Τι κάνει | Πότε να το αλλάξετε |
|----------|----------|----------------------|
| **Prefix / Suffix** | Προσθέτει στατικό κείμενο πριν/μετά το αριθμητικό μέρος. | Χρησιμοποιήστε ένα ID υπόθεσης, κωδικό έργου, ή “CONF‑” για εμπιστευτικά έγγραφα. |
| **Start** | Ο πρώτος αριθμός στη σειρά. | Αν συνεχίζετε ένα σχήμα αρίθμησης από προηγούμενο πακέτο, ορίστε το ανάλογα. |
| **NumberOfDigits** | Ελέγχει το μηδενικό padding. | Για νομικές καταχωρίσεις συχνά χρειάζονται ακριβώς 6 ψηφία· ορίστε το σε `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Επιλέξτε με βάση τη διάταξη του εγγράφου· το BottomRight είναι το πιο κοινό για Bates numbers. |

> **Pro tip:** Αν χρειάζεστε να **number pdf pages** σε πολλές στήλες, μπορείτε να καλέσετε το `pdfDocument.AddBatesNumbering` δύο φορές με διαφορετικές τιμές `Placement` και διαφορετικά `Prefix` strings.

## Βήμα 3 – Εφαρμογή του Bates Numbering στο Έγγραφο

Με τις επιλογές έτοιμες, η πραγματική σφράγιση είναι μια ενιαία κλήση μεθόδου. Το Aspose διαχειρίζεται εσωτερικά την σελιδοποίηση, την περιστροφή και τους υπολογισμούς περιθωρίων.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Γιατί λειτουργεί μια ενιαία κλήση:** Στο παρασκήνιο το Aspose διατρέχει το `pdfDocument.Pages`, δημιουργεί ένα `TextFragment` για κάθε σελίδα, και το τοποθετεί βάσει του `Placement` που επιλέξατε. Αυτή η αφαίρεση σας εξοικονομεί το γράψιμο χειροκίνητου βρόχου και την αντιμετώπιση μετασχηματισμών συντεταγμένων.

## Βήμα 4 – Αποθήκευση του Ενημερωμένου PDF

Τέλος, γράψτε το τροποποιημένο αρχείο στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να δημιουργήσετε νέο αρχείο· το παρακάτω παράδειγμα δημιουργεί ένα νέο αντίγραφο.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Αν χρειάζεστε να **add sequential pdf numbers** σε ροή (π.χ., όταν στέλνετε το αρχείο μέσω API), αντικαταστήστε τη διαδρομή αρχείου με ένα `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- Ένα νέο αρχείο `bates_numbered.pdf` εμφανίζεται στο `C:\MyDocs`.
- Κάθε σελίδα εμφανίζει κάτι όπως `2025-05000-A`, `2025-05001-A`, … στην κάτω‑δεξιά γωνία.
- Οι αριθμοί έχουν μηδενική συμπλήρωση σε πέντε ψηφία, ταιριάζοντας με τη ρύθμιση `NumberOfDigits`.

## Διαχείριση Συνηθισμένων Παραλλαγών

### 1. Διαφορετικά Μεγέθη Σελίδας

Αν το PDF σας συνδυάζει σελίδες πορτραίτου και τοπίου, μπορεί να παρατηρήσετε ότι ο αριθμός κόβεται στην πιο πλατιά πλευρά. Για να το διορθώσετε, ενεργοποιήστε την ιδιότητα `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Προσαρμοσμένη Γραμματοσειρά ή Χρώμα

Οι Bates numbers προεπιλογή είναι μαύροι, 12‑pt Times New Roman. Αλλάξτε την εμφάνιση προσπελάζοντας το `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Παράλειψη Σελίδων

Ας υποθέσουμε ότι θέλετε να **number pdf pages** αλλά να παραλείψετε τη σελίδα τίτλου. Χρησιμοποιήστε ένα εύρος σελίδων:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Προσθήκη Πολλαπλών Σχεδίων Αρίθμησης

Οι νομικές ομάδες μερικές φορές απαιτούν τόσο έναν Bates number όσο και ένα υδατογράφημα εμπιστευτικότητας. Εκτελέστε δύο ξεχωριστές κλήσεις `AddBatesNumbering` με διαφορετικές τιμές `Placement`:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με PDF που έχουν ήδη υπάρχον κείμενο;**  
A: Ναι. Το Aspose προσθέτει τον Bates number ως ξεχωριστό στρώμα, έτσι το υπάρχον περιεχόμενο παραμένει αμετάβλητο. Αν χρειάζεστε οι αριθμοί να εμφανίζονται *πίσω* από το υπάρχον κείμενο (σπάνια), θα πρέπει να χειριστείτε τα streams περιεχομένου της σελίδας χειροκίνητα.

**Q: Τι γίνεται αν το PDF είναι προστατευμένο με κωδικό;**  
A: Φορτώστε το πρώτα με τον κωδικό: `new Document(path, new LoadOptions { Password = "secret" })`. Μετά τη σφράγιση, μπορείτε να εφαρμόσετε ξανά κρυπτογράφηση μέσω `pdfDocument.Encrypt(...)`.

**Q: Μπορώ να το χρησιμοποιήσω σε εφαρμογή κονσόλας .NET Core;**  
A: Απόλυτα. Ο ίδιος κώδικας λειτουργεί σε .NET Core, .NET 5+ και .NET Framework. Απλώς αναφέρετε το κατάλληλο πακέτο NuGet Aspose.Pdf.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **add bates numbering pdf** αρχεία, πώς να **number pdf pages**, και πώς να **add sequential pdf numbers** με πλήρη έλεγχο της μορφοποίησης, της θέσης και της διαχείρισης ειδικών περιπτώσεων. Το σύντομο snippet παραπάνω κάνει το σκληρό έργο, ενώ οι επιπλέον επιλογές σας επιτρέπουν να προσαρμόσετε τη λύση σε οποιαδήποτε νομική, αρχειοθετική ή συμμορφωτική ροή εργασίας.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με:

- **Batch processing** – επανάληψη σε φάκελο PDF και εφαρμογή του ίδιου σχήματος αρίθμησης.
- **Dynamic prefixes** – λήψη ID υποθέσεων από βάση δεδομένων και ενσωμάτωση τους ανά έγγραφο.
- **PDF/A compliance** – μετά την αρίθμηση, καλέστε το `pdfDocument.Convert(..., PdfFormat.PdfA2b)` για να εξασφαλίσετε μακροπρόθεσμη διατήρηση.

Νιώστε ελεύθεροι να πειραματιστείτε, να μοιραστείτε τα ευρήματά σας ή να θέσετε ερωτήσεις στα σχόλια. Καλή προγραμματιστική, και εύχομαι τα PDF σας να παραμένουν πάντα τέλεια ευρετηριασμένα!

![Στιγμιότυπο οθόνης μιας σελίδας PDF με Bates numbers στην κάτω‑δεξιά γωνία](https://example.com/images/bates-numbered.png "παράδειγμα add bates numbering pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}