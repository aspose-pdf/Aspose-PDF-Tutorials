---
category: general
date: 2026-03-14
description: Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#.
  Μάθετε πώς να προσθέτετε αριθμούς Bates και να προσθέτετε αυτόματα διαδοχικούς αριθμούς
  σελίδων για νομικά ή αρχειακά έγγραφα.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: el
og_description: Προσθέστε αρίθμηση Bates σε PDF βήμα‑βήμα. Αυτό το σεμινάριο δείχνει
  πώς να προσθέσετε Bates και διαδοχικούς αριθμούς σελίδων χρησιμοποιώντας το Aspose.Pdf
  για .NET.
og_title: Προσθήκη Bates Numbering σε PDF με C# – Πλήρης Οδηγός
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Προσθήκη Bates Numbering σε PDF με C# – Πλήρης Οδηγός
url: /el/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

")

We translate alt text and title.

Now tables: translate question and answer content.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Αρίθμησης Bates σε PDF – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **προσθέσετε αρίθμηση bates pdf** σε ένα τεράστιο νομικό πακέτο αλλά δεν ήξερες από πού να ξεκινήσεις; Η προσθήκη αριθμών Bates είναι μια συνηθισμένη, αλλά παράξενα επίμονη, διαδικασία στις ροές εργασίας ελέγχου εγγράφων. Το καλό νέο; Με το Aspose.Pdf για .NET μπορείτε να αυτοματοποιήσετε όλο το θέμα με λίγες γραμμές κώδικα.

Σε αυτόν τον οδηγό θα δούμε **πώς να προσθέσετε bates** σε κάθε σελίδα ενός PDF, θα συζητήσουμε τις επιλογές **προσθήκης διαδοχικών αριθμών σελίδας**, και θα σας δείξουμε ένα έτοιμο προς εκτέλεση δείγμα κώδικα. Στο τέλος θα έχετε μια αυτόνομη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C# — χωρίς επιπλέον σκριπτάκια, χωρίς χειροκίνητη σήμανση.

## Τι Θα Χρειαστείτε

- **Aspose.Pdf για .NET** (έκδοση 23.10 ή νεότερη). Η βιβλιοθήκη είναι εμπορική, αλλά μια δωρεάν αξιολόγηση λειτουργεί άψογα για δοκιμές.
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή το `dotnet` CLI).
- Ένα αρχείο PDF εισόδου (`input.pdf`) που θέλετε να επισημάνετε.
- Λίγη υπομονή για τις σπάνιες ειδικές περιπτώσεις (θα τις καλύψουμε).

Αν έχετε ήδη όλα αυτά, τέλεια — ας ξεκινήσουμε.

![Παράδειγμα προσθήκης αρίθμησης Bates σε PDF](/images/bates-numbering-example.png "Στιγμιότυπο οθόνης που δείχνει ένα PDF με εφαρμοσμένη προσθήκη bates numbering pdf")

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose.Pdf

Για να διατηρήσετε τα πράγματα οργανωμένα, ξεκινήστε μια νέα εφαρμογή κονσόλας:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Η εντολή `dotnet add package` κατεβάζει το πιο πρόσφατο πακέτο Aspose.Pdf από το NuGet, ώστε να είστε έτοιμοι να κωδικοποιήσετε.

### Γιατί μια εφαρμογή κονσόλας;

Μια εφαρμογή κονσόλας είναι ελαφριά, τρέχει οπουδήποτε, και σας επιτρέπει να εστιάσετε στη λογική του PDF χωρίς περισπασμούς UI. Φυσικά, μπορείτε αργότερα να μεταφέρετε τον κώδικα σε ένα web API ή σε μια υπηρεσία παρασκηνίου — τίποτα στη βασική λογική δεν σας δεσμεύει στην κονσόλα.

## Βήμα 2: Φόρτωση του Πηγαίου PDF

Το άνοιγμα του εγγράφου είναι απλό. Θα χρησιμοποιήσουμε ένα μπλοκ `using` ώστε η διαχείριση του αρχείου να απελευθερώνεται αυτόματα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**Τι συμβαίνει;** Η κλάση `Document` αντιπροσωπεύει ολόκληρο το αρχείο PDF. Με το `using` εξασφαλίζουμε ότι το `Dispose` εκτελείται, γράφοντας τυχόν εκκρεμείς αλλαγές στο δίσκο.

## Βήμα 3: Ορισμός ενός Bates Number Artifact (Ο Πυρήνας «πώς να προσθέσετε bates»)

Το Aspose.Pdf αντιμετωπίζει τους αριθμούς Bates ως *artifacts* — μεταδεδομένα που μπορούν να αποδοθούν στην οθόνη ή να εκτυπωθούν, αλλά δεν γίνονται μόνιμο ρεύμα περιεχομένου εκτός εάν «ισοπεδώσετε» το PDF. Εδώ είναι το αντικείμενο που θα συνδέσουμε με κάθε σελίδα:

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### Γιατί να χρησιμοποιήσουμε ένα artifact;

- **Απόδοση:** Ο αριθμός αποδίδεται «on‑the‑fly», ώστε να μπορείτε να αλλάξετε το πρόθεμα ή τον αρχικό αριθμό χωρίς να ξαναγράψετε ολόκληρο το PDF.
- **Ευελιξία:** Μπορείτε αργότερα να ισοπεδώσετε το PDF αν χρειάζεστε ένα «σκληρά κωδικοποιημένο» στίγμα για νομική υποβολή.
- **Ακρίβεια:** Η τοποθέτηση χρησιμοποιεί μονάδες points (1/72 ίντσα), προσφέροντας έλεγχο pixel‑perfect.

Αν χρειάζεστε διαφορετικό πρόθεμα ή μεγαλύτερη γραμματοσειρά, απλώς τροποποιήστε τις ιδιότητες. Το πεδίο `Increment` καθορίζει πώς αυξάνεται ο αριθμός από σελίδα σε σελίδα — ιδανικό για την απαίτηση **προσθήκης διαδοχικών αριθμών σελίδας**.

## Βήμα 4: Σύνδεση του Artifact σε Κάθε Σελίδα

Τώρα διατρέχουμε τη συλλογή `Pages` και προσθέτουμε το artifact. Αυτή είναι η πραγματική ενέργεια «προσθήκη αρίθμησης bates pdf».

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### Σημείωση για Ειδικές Περιπτώσεις

Αν το PDF σας περιέχει ήδη Bates artifacts, μπορεί να δημιουργηθούν διπλότυπα. Ένας γρήγορος έλεγχος μπορεί να το αποτρέψει:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

Αυτός ο μικρός έλεγχος σας σώζει από μια ακατάστατη διπλή σήμανση, ειδικά όταν επεξεργάζεστε παρτίδες εγγράφων που έχουν ήδη επισημανθεί.

## Βήμα 5: Αποθήκευση του Ενημερωμένου PDF

Τέλος, γράψτε το αρχείο πίσω στο δίσκο. Μπορείτε είτε να αντικαταστήσετε το αρχικό είτε να δημιουργήσετε νέο αρχείο — εδώ θα παράγουμε ένα φρέσκο αντίγραφο:

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

Όταν ανοίξετε το `output.pdf` σε οποιονδήποτε προβολέα, θα δείτε “CASE‑1000”, “CASE‑1001”, κ.λπ., στην κάτω‑αριστερή γωνία κάθε σελίδας.

### Προαιρετικό: Ισοπέδωση του PDF

Αν ο παραλήπτης απαιτεί ένα μη επεξεργάσιμο PDF (συνηθισμένο στις δικαστικές υποβολές), ισοπεδώστε τις σελίδες:

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

Η ισοπέδωση είναι μια μοναδική ενέργεια· μετά από αυτήν, οι αριθμοί Bates γίνονται μέρος του ρεύματος περιεχομένου της σελίδας και δεν μπορούν να τροποποιηθούν χωρίς νέα επεξεργασία.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs`. Περιλαμβάνει το προαιρετικό βήμα ισοπέδωσης, σχολιασμένο για εύκολη ενεργοποίηση/απενεργοποίηση.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

Τρέξτε το με `dotnet run` και παρακολουθήστε την κονσόλα να επιβεβαιώνει την εκτέλεση.

## Συχνές Ερωτήσεις & Επαγγελματικές Συμβουλές

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να αλλάξω τη θέση ανά σελίδα;** | Ναι. Αντί για ένα ενιαίο `batesArtifact`, δημιουργήστε ένα νέο μέσα στον βρόχο και ορίστε `X`/`Y` βάσει του μεγέθους της σελίδας. |
| **Τι γίνεται αν το PDF είναι προστατευμένο με κωδικό;** | Φορτώστε το με `new Document(sourcePdfPath, new LoadOptions { Password = "mySecret" })`. Η υπόλοιπη ροή παραμένει αμετάβλητη. |
| **Πρέπει να ανησυχήσω για την απόδοση σε τεράστια αρχεία;** | Η προσθήκη artifacts είναι O(N) όπου N = αριθμός σελίδων, και η χρήση μνήμης παραμένει χαμηλή επειδή το Aspose διαχειρίζεται τις σελίδες σε ροές. Για PDFs >10 000 σελίδων, σκεφτείτε επεξεργασία σε παρτίδες για να αποφύγετε μεγάλες παύσεις GC. |
| **Μπορεί η αρίθμηση να επαναρυθμιστεί ανά ενότητα;** | Απόλυτα. Ορίστε `StartNumber` σε νέα τιμή πριν φτάσετε στην πρώτη σελίδα της επόμενης ενότητας, ή δημιουργήστε δεύτερο `BatesNumberArtifact` με διαφορετικό `Prefix`. |
| **Λειτουργεί αυτό σε .NET Core;** | Ναι. Το Aspose.Pdf υποστηρίζει .NET Framework, .NET Core και .NET 5/6+. Απλώς στοχεύστε το κατάλληλο runtime στο csproj σας. |

### Επαγγελματική Συμβουλή

Όταν διαχειρίζεστε **προσθήκη διαδοχικών αριθμών σελίδας** για ένα σύνολο πολλαπλών τόμων, αποθηκεύστε τον τελευταίο χρησιμοποιημένο αριθμό σε ένα μικρό αρχείο JSON. Διαβάστε το πριν ξεκινήσετε, αυξήστε το ανάλογα, και γράψτε το ξανά. Αυτό το μικρό επίπεδο επιμονής αποτρέπει τυχαία επαναχρησιμοποίηση αριθμών μεταξύ εκτελέσεων.

## Επαλήθευση του Αποτελέσματος

Ανοίξτε το `output.pdf` σε Adobe Reader, Foxit ή ακόμη και Chrome. Θα πρέπει να δείτε κάτι όπως:

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

Αν ισοπεδώσατε το PDF, οι αριθμοί γίνονται μέρος των γραφικών της σελίδας — δεξί‑κλικ → “Inspect” θα τα εμφανίσει ως απλά αντικείμενα κειμένου.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **προσθέσετε bates numbering pdf** χρησιμοποιώντας το Aspose.Pdf, εξετάσαμε τους μηχανισμούς **πώς να προσθέσετε bates**, και παρουσιάσαμε έναν καθαρό τρόπο **προσθήκης διαδοχικών αριθμών σελίδας** σε ολόκληρο το έγγραφο. Το απόσπασμα είναι έτοιμο για παραγωγή, διαχειρίζεται διπλότυπα artifacts, και προσφέρει προαιρετικό βήμα ισοπέδωσης για νομική συμμόρφωση.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- Συγχώνευση πολλαπλών PDF ενώ διατηρείται η συνέχεια των Bates (χρησιμοποιήστε `Document.AppendDocument` και προσαρμόστε το `StartNumber` εν κινήσει).
- Προσθήκη κώδικα QR δίπλα στον αριθμό Bates για αυτοματοποιημένη παρακολούθηση.
- Ενσωμάτωση αυτής της λογικής σε ένα ASP.NET Core API ώστε η υπηρεσία σας να επισημαίνει PDFs κατ’ απαίτηση.

Δοκιμάστε το, προσαρμόστε το πρόθεμα, πειραματιστείτε με τις γραμματοσειρές, και αφήστε την αυτοματοποίηση να αφαιρέσει το βαριά δουλειά από τη ροή ελέγχου εγγράφων σας. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}