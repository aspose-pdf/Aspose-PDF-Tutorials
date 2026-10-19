---
category: general
date: 2026-08-04
description: Πώς να χρησιμοποιήσετε το Aspose για την εξαγωγή κειμένου από σαρωμένα
  PDF και τη μετατροπή PDF σε κείμενο με C#. Μάθετε να διαβάζετε σαρωμένα αρχεία PDF
  και να λαμβάνετε αξιόπιστα αποτελέσματα OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: el
lastmod: 2026-08-04
og_description: Πώς να χρησιμοποιήσετε το Aspose για να διαβάσετε σαρωμένα αρχεία
  PDF, να εξάγετε το κείμενο από σαρωμένα PDF και να μετατρέψετε το PDF σε κείμενο
  με ένα πλήρες, εκτελέσιμο παράδειγμα.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Πώς να χρησιμοποιήσετε το Aspose – εξαγωγή κειμένου από σαρωμένα PDF σε
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Πώς να χρησιμοποιήσετε το Aspose για την εξαγωγή κειμένου από ένα σαρωμένο
  PDF – βήμα‑βήμα οδηγός
url: /el/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το Aspose για εξαγωγή κειμένου από σαρωμένο PDF – βήμα‑βήμα οδηγός

Αν χρειάζεστε **how to use Aspose** για OCR, αυτός ο οδηγός σας δείχνει πώς να εξάγετε κείμενο από σαρωμένο PDF με λίγες γραμμές C#. Είτε δημιουργείτε μια υπηρεσία αρχειοθέτησης εγγράφων είτε ένα ευρετήριο αναζήτησης για παλαιά έγγραφα, η λύση λειτουργεί με οποιοδήποτε σαρωμένο PDF που παρέχετε στην υπηρεσία Aspose.Pdf.AI.

Σε αυτό το tutorial θα:

* Δημιουργήσετε έναν OCR copilot που διαβάζει ένα σαρωμένο PDF.
* Εξάγετε το αναγνωρισμένο κείμενο ασύγχρονα.
* Εμφανίσετε ή επεξεργαστείτε περαιτέρω το εξαγόμενο string.

Η μόνη προϋπόθεση είναι μια ενεργή συνδρομή Aspose.Pdf.AI και ένα περιβάλλον ανάπτυξης .NET 6 (ή νεότερο).

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| .NET 6 SDK ή νεότερο | Παρέχει `async Main` και σύγχρονα χαρακτηριστικά της γλώσσας. |
| Aspose.Pdf.AI NuGet package (`Aspose.Pdf.AI`) | Περιέχει το `AICopilotFactory` και τις επιλογές OCR. |
| Ένα έγκυρο Aspose.Pdf.AI `client` instance (API key) | Αυθεντικοποιεί τα αιτήματά σας στην υπηρεσία cloud. |
| Ένα σαρωμένο PDF αρχείο (π.χ., `Scanned.pdf`) | Το πηγαίο έγγραφο από το οποίο θα εξαχθεί το κείμενο. |

Εγκαταστήστε το πακέτο με το .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Βήμα 1: Ρύθμιση του Aspose.Pdf.AI client

Πριν καλέσετε οποιοδήποτε OCR endpoint, πρέπει να δημιουργήσετε έναν client που κρατά τα διαπιστευτήρια του API σας. Ο client είναι thread‑safe και μπορεί να επαναχρησιμοποιηθεί για πολλαπλά έγγραφα.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Γιατί απαιτείται αυτό το βήμα** – Η υπηρεσία Aspose επικυρώνει κάθε αίτημα έναντι της συνδρομής σας. Η δημιουργία του client μία φορά αποφεύγει επαναλαμβανόμενα network handshakes και διατηρεί τον κώδικα καθαρό.

## Βήμα 2: Δημιουργία OCR copilot για το σαρωμένο PDF έγγραφο

Το `AICopilotFactory` δημιουργεί έναν εξειδικευμένο OCR copilot που γνωρίζει πώς να επεξεργαστεί το αρχείο που ορίζετε. Περνάτε το `client` και ένα αντικείμενο `OpenAIOcrOptions` που δείχνει στη διαδρομή του PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Επεξήγηση** – Το `CreateOcrCopilot` ενσωματώνει όλες τις χαμηλού επιπέδου κλήσεις HTTP. Η μέθοδος `WithDocument` λέει στην υπηρεσία ποιο αρχείο να αναλύσει· μπορείτε επίσης να παρέχετε ένα `Stream` αν το PDF βρίσκεται στη μνήμη.

## Βήμα 3: Εξαγωγή του αναγνωρισμένου κειμένου ασύγχρονα

Η κλήση `GetTextAsync` εκτελεί την OCR λειτουργία στο cloud και επιστρέφει το αποτέλεσμα ως plain‑text. Επειδή η λειτουργία μπορεί να διαρκέσει μερικά δευτερόλεπτα, η μέθοδος είναι ασύγχρονη.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Γιατί ασύγχρονα;** – Η καθυστέρηση δικτύου και ο χρόνος επεξεργασίας OCR είναι απρόβλεπτοι. Η χρήση `await` αποτρέπει το μπλοκάρισμα του κύριου νήματος της εφαρμογής, κάτι που είναι ιδιαίτερα σημαντικό για UI ή σενάρια web‑service.

## Βήμα 4: Χρήση του εξαγόμενου κειμένου

Σε αυτό το σημείο έχετε ένα κανονικό .NET `string` που περιέχει τη πλήρη απομαγνητοφώνηση του σαρωμένου PDF. Μπορείτε να το γράψετε στην κονσόλα, να το αποθηκεύσετε σε βάση δεδομένων ή να το στείλετε σε μηχανή αναζήτησης.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Αναμενόμενη έξοδος

Αν το `Scanned.pdf` περιέχει μια σελίδα με τη φράση “Hello, world!”, η κονσόλα θα εμφανίσει:

```
=== OCR Result ===
Hello, world!
```

Για έγγραφα πολλαπλών σελίδων η έξοδος ενώνει το κείμενο κάθε σελίδας, διατηρώντας τις αλλαγές γραμμής.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο console project (`dotnet new console`). Δείχνει **how to use Aspose** από την αρχή μέχρι το τέλος, συμπεριλαμβανομένου του χειρισμού σφαλμάτων για κοινά προβλήματα.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Κύρια σημεία στο παράδειγμα**

* `await` εξασφαλίζει μη‑μπλοκαριστική εκτέλεση.
* Το μπλοκ `try/catch` εμφανίζει σφάλματα δικτύου ή υπηρεσίας, κάτι που είναι απαραίτητο όταν **reading scanned PDF** αρχεία σε μεγάλη κλίμακα.
* Αντικαταστήστε το `YOUR_API_KEY` και το `YOUR_DIRECTORY/Scanned.pdf` με πραγματικές τιμές πριν τρέξετε.

## Διαχείριση ακραίων περιπτώσεων και συμβουλές βέλτιστων πρακτικών

| Κατάσταση | Συνιστώμενη προσέγγιση |
|-----------|----------------------|
| **Μεγάλα PDFs ( > 50 MB )** | Διαχωρίστε το έγγραφο σε μικρότερα κομμάτια στην πλευρά του client και επεξεργαστείτε κάθε κομμάτι με ξεχωριστό copilot. Αυτό μειώνει την πίεση μνήμης και βελτιώνει την αξιοπιστία. |
| **Σαρώσεις χαμηλής ποιότητας** | Ρυθμίστε την ποιότητα OCR προσθέτοντας `.WithLanguage("eng")` ή `.WithEnhanceImage(true)` στις `OpenAIOcrOptions`. Η υπηρεσία υποστηρίζει γλωσσικές υποδείξεις που βελτιώνουν την ακρίβεια. |
| **Πολλαπλές γλώσσες** | Παρέχετε λίστα χωρισμένη με κόμμα, π.χ., `.WithLanguage("eng,spa")`. Η μηχανή OCR θα εντοπίσει και θα απομαγνητοφωνήσει και τις δύο γλώσσες. |
| **Αρχεία εικόνας μη‑PDF** | Μετατρέψτε την εικόνα σε PDF πρώτα (βιβλιοθήκη `Aspose.Pdf`) ή χρησιμοποιήστε `OpenAIOcrOptions.WithImage` για να στείλετε την εικόνα απευθείας. |
| **Υπέρβαση ορίου ρυθμού** | Εφαρμόστε λογική exponential back‑off και επαναπροσπάθειας· το Aspose API επιστρέφει HTTP 429 όταν ξεπεράσετε το quota. |

### Συμβουλή επαγγελματία

Αποθηκεύστε στην cache το αποτέλεσμα `ocrText` αν σκοπεύετε να το χρησιμοποιήσετε ξανά αργότερα. Η λειτουργία OCR είναι το πιο δαπανηρό μέρος της ροής εργασίας, και η επαναχρησιμοποίηση του string αποφεύγει διπλές κλήσεις API και εξοικονομεί credits.

## Συχνές ερωτήσεις

**Ε: Λειτουργεί αυτό με PDF προστατευμένα με κωδικό;**  
Α: Ναι. Προσθέστε `.WithPassword("yourPassword")` στον builder των options πριν δημιουργήσετε τον copilot.

**Ε: Μπορώ να εξάγω κείμενο σε δομημένη μορφή (π.χ., JSON με αριθμούς σελίδων);**  
Α: Χρησιμοποιήστε `GetTextStructureAsync()` αντί για `GetTextAsync()`. Η μέθοδος επιστρέφει ένα JSON payload που περιλαμβάνει δείκτες σελίδων, bounding boxes και confidence scores.

**Ε: Τι γίνεται αν το PDF περιέχει πίνακες;**  
Α: Η εξαγωγή plain‑text ισοπεδώνει τους πίνακες σε σειρές χωρισμένες με αλλαγές γραμμής. Για πιο πλούσια δεδομένα, ζητήστε τη μετατροπή PDF‑to‑HTML (`GetHtmlAsync`) και αναλύστε τα HTML στοιχεία των πινάκων.

## Συμπέρασμα

Τώρα ξέρετε **how to use Aspose** για ανάγνωση σαρωμένου PDF, εξαγωγή κειμένου από σαρωμένο PDF, και **convert PDF to text** με ένα ελάχιστο πρόγραμμα C#. Η διαδικασία αποτελείται από τη δημιουργία ενός OCR copilot, την κλήση `GetTextAsync` και τον χειρισμό του προκύπτοντος string. Ακολουθώντας τις προτάσεις για ακραίες περιπτώσεις, μπορείτε να κλιμακώσετε τη λύση σε μεγάλες παρτίδες εγγράφων, πολυγλωσσικό περιεχόμενο και ασφαλή PDFs.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **How to extract text** με διατήρηση διάταξης (`GetHtmlAsync`).
* Χρήση Aspose.Pdf.AI για **extract tables** και εξαγωγή τους σε CSV.
* Ενσωμάτωση του OCR output με Azure Cognitive Search για ευρετήρια αναζητήσιμων αρχείων.

Καλή προγραμματιστική δουλειά, και απολαύστε την ακρίβεια που φέρνει το AI‑powered OCR του Aspose στις ροές εργασίας σας με σαρωμένα PDF!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή κειμένου από αρχεία PDF χρησιμοποιώντας Aspose.PDF για .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [Πώς να εξάγετε κείμενο από συγκεκριμένες περιοχές σε PDF χρησιμοποιώντας Aspose.PDF για .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [Πώς να εξάγετε επισημασμένο κείμενο από PDF χρησιμοποιώντας Aspose.PDF για .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}