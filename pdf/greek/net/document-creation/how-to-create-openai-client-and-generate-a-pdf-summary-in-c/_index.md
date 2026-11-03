---
category: general
date: 2026-10-10
description: Δημιουργήστε πελάτη OpenAI σε C# και μάθετε πώς να συνοψίζετε ένα PDF,
  να μετατρέπετε το PDF σε σύνοψη και να αποθηκεύετε τη δημιουργημένη σύνοψη PDF με
  το Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: el
lastmod: 2026-10-10
og_description: Δημιουργήστε πελάτη OpenAI σε C# και μάθετε αμέσως πώς να συνοψίσετε
  ένα PDF, να μετατρέψετε το PDF σε σύνοψη και να αποθηκεύσετε τη δημιουργημένη σύνοψη
  PDF.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Δημιουργία πελάτη OpenAI και δημιουργία περίληψης PDF σε C# – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
- description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  name: How to create OpenAI client and generate a PDF summary in C#
  steps:
  - name: '**Console output** – the plain‑text summary displayed on the screen.'
    text: '**Console output** – the plain‑text summary displayed on the screen.'
  - name: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
    text: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
  - name: Lower the `WithTemperature` to 0.2 for more deterministic output.
    text: Lower the `WithTemperature` to 0.2 for more deterministic output.
  - name: Increase the
    text: Increase the
  type: HowTo
tags:
- OpenAI
- C#
- PDF processing
- Aspose.Pdf.AI
title: Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε μια σύνοψη PDF σε C#
url: /el/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε σύνοψη PDF σε C#

Αν χρειάζεστε **create OpenAI client** σε μια εφαρμογή .NET, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε και πώς να μετατρέψετε οποιοδήποτε PDF σε μια σύντομη, AI‑γεννημένη σύνοψη. Θα δείτε πώς να **convert PDF to summary**, να ανακτήσετε το κείμενο και να **save the summary** ως νέο αρχείο PDF — όλα με το Aspose.Pdf.AI.

Η σύνοψη PDF είναι μια κοινή απαίτηση για ροές εργασίας με πολλά έγγραφα, όπως νομική ανασκόπηση, συγκέντρωση έρευνας ή αυτόματη δημιουργία αναφορών. Στο τέλος αυτού του οδηγού θα μπορείτε να **generate PDF summary** προγραμματιστικά, χωρίς να αφήσετε το περιβάλλον C#.

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (το παράδειγμα στοχεύει στο .NET 6, αλλά οποιαδήποτε πρόσφατη έκδοση .NET λειτουργεί)
- Ένα πακέτο NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) – αυτό το wrapper απλοποιεί τις κλήσεις OpenAI για περιεχόμενο PDF
- Ένα έγκυρο κλειδί OpenAI API (μπορείτε να αποκτήσετε ένα από το portal OpenAI)
- Ένα δείγμα αρχείου PDF που θέλετε να συνοψίσετε (π.χ., `SampleDocument.pdf`)
- Visual Studio 2022, VS Code ή οποιοδήποτε IDE που υποστηρίζει ανάπτυξη C#

> **Pro tip:** Διατηρήστε το κλειδί API σας σε ασφαλή τοποθεσία όπως [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) ή Azure Key Vault. Ποτέ μην το κωδικοποιείτε σκληρά στον κώδικα ελέγχου.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.Pdf.AI

Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.Pdf.AI
```

Το πακέτο φέρνει τον απαραίτητο HTTP client, εργαλεία χειρισμού PDF και ένα ελαφρύ wrapper γύρω από το OpenAI API. Μετά την εγκατάσταση, επαναφέρετε το έργο για να διασφαλίσετε ότι όλες οι εξαρτήσεις είναι διαθέσιμες:

```bash
dotnet restore
```

## Βήμα 2: **Create OpenAI client** με το κλειδί API σας

Η δημιουργία του πελάτη είναι το πρώτο βήμα για οποιαδήποτε λειτουργία PDF με τεχνητή νοημοσύνη. Το `OpenAIClient` διαχειρίζεται τον έλεγχο ταυτότητας, τον περιορισμό αιτήσεων και την ομαδοποίηση συνδέσεων για εσάς.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    // Replace with your real key – never commit it to source control
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // ---- Step 2: create OpenAI client ----
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // The client is now ready for any Aspose.Pdf.AI operation.
        await SummarizePdfAsync(openAiClient);
    }
}
```

> **Why this matters:** Η δήλωση `using` εγγυάται ότι ο πελάτης θα απορριφθεί σωστά, απελευθερώνοντας πόρους δικτύου και αποφεύγοντας την εξάντληση των υποδοχών σε υπηρεσίες μακράς διάρκειας.

## Βήμα 3: Διαμόρφωση επιλογών σύνοψης – **convert PDF to summary**

Το αντικείμενο `OpenAISummaryCopilotOptions` λέει στην AI τι πρέπει να κάνει. Μπορείτε να ρυθμίσετε τη θερμοκρασία, να περιορίσετε τη χρήση token και, το πιο σημαντικό, να υποδείξετε το πηγαίο PDF.

```csharp
private static async Task SummarizePdfAsync(OpenAIClient client)
{
    // ---- Step 3: set up summary options (convert PDF to summary) ----
    var summaryOptions = OpenAISummaryCopilotOptions
        .Create()
        .WithTemperature(0.5)                     // Balanced creativity vs. factuality
        .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

    // The options are immutable; each call returns a new instance.
```

### Γιατί θερμοκρασία 0.5;

Μια θερμοκρασία 0.5 παράγει σύντομη, ακριβή γλώσσα ενώ εξακολουθεί να επιτρέπει στο μοντέλο να επαναδιατυπώνει προτάσεις. Υψηλότερες τιμές (π.χ., 0.9) κάνουν το αποτέλεσμα πιο δημιουργικό αλλά μπορεί να απομακρυνθεί από το αρχικό νόημα — κάτι ανεπιθύμητο για νομικές ή τεχνικές συνόψεις.

## Βήμα 4: **How to summarize PDF** – δημιουργία του copilot και λήψη του κειμένου

Τώρα που ο πελάτης και οι επιλογές είναι έτοιμες, δημιουργήστε ένα summary copilot. Αυτό το αντικείμενο οργανώνει το αίτημα προς το OpenAI και επιστρέφει το αποτέλεσμα σε πολλαπλές μορφές.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

Η μέθοδος `GetSummaryAsync` επιστρέφει μια καθαρή, απλή κειμενική έκδοση που μπορείτε να ενσωματώσετε σε UI, να στείλετε μέσω email ή να αποθηκεύσετε σε βάση δεδομένων.

## Βήμα 5: Ανάκτηση της σύνοψης ως έγγραφο PDF

Αν χρειάζεστε μια φορητή, εκτυπώσιμη έκδοση, ζητήστε από το copilot ένα έγγραφο PDF. Αυτό το βήμα δείχνει **generate PDF summary** απευθείας από το μοντέλο AI.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

Το επιστρεφόμενο `Aspose.Pdf.Document` συμπεριφέρεται όπως οποιοδήποτε άλλο αντικείμενο PDF στο οικοσύστημα Aspose, πράγμα που σημαίνει ότι μπορείτε να επεξεργαστείτε περαιτέρω τις σελίδες, να προσθέσετε μεταδεδομένα ή να συγχωνεύσετε με άλλα PDF.

## Βήμα 6: **How to save summary** – αποθήκευση του PDF στο δίσκο

Τέλος, αποθηκεύστε τη δημιουργημένη σύνοψη στο σύστημα αρχείων. Η βοηθητική μέθοδος `SaveSummaryAsync` συνδυάζει την ανάκτηση και την αποθήκευση σε μία κλήση, αλλά θα δείξουμε επίσης την ρητή αποθήκευση για πληρότητα.

```csharp
    // ---- Step 6: save the summary PDF (how to save summary) ----
    const string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";

    // Direct helper method
    await summaryCopilot.SaveSummaryAsync(outputPath);

    // Or, save the Document object manually
    // summaryDocument.Save(outputPath);
    Console.WriteLine($"Summary PDF saved to: {outputPath}");
}
```

> **Tip:** Αν χρειάζεται να επιβάλετε μια σύμβαση ονοματοδοσίας (π.χ., αρχεία με χρονική σήμανση), δημιουργήστε τη διαδρομή προγραμματιστικά με `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα μαζί, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να εκτελέσετε:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // Create OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Configure summary options (convert PDF to summary)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Instantiate the copilot (how to summarize PDF)
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Text Summary ===");
        Console.WriteLine(summaryText);

        // Get PDF version (generate PDF summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF (how to save summary)
        const string outPath = "YOUR_DIRECTORY/Summary_out.pdf";
        await summaryCopilot.SaveSummaryAsync(outPath);
        Console.WriteLine($"Summary PDF saved to: {outPath}");
    }
}
```

Η εκτέλεση του προγράμματος παράγει δύο αποτελέσματα:

1. **Console output** – η απλή κειμενική σύνοψη που εμφανίζεται στην οθόνη.
2. `Summary_out.pdf` – ένα PDF που μπορεί να ληφθεί, περιέχοντας την ίδια σύνοψη, έτοιμο για διανομή.

## Κοινές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Μεγάλα PDF (> 10 MB)** | Διαιρέστε το έγγραφο σε μικρότερα τμήματα (π.χ., ανά κεφάλαιο) και συνοψίστε κάθε τμήμα ξεχωριστά. Συνδυάστε τα αποτελέσματα με `Document.AppendDocument`. |
| **Απαιτείται προσαρμοσμένο prompt** | Χρησιμοποιήστε `WithPrompt("Summarize the following legal contract in bullet points:")` πριν καλέσετε το `CreateSummaryCopilot`. |
| **PDF πηγής μη‑Αγγλική** | Ορίστε `WithLanguage("es")` (ή τον κατάλληλο κωδικό ISO) για να καθοδηγήσετε τη διαχείριση γλώσσας του μοντέλου. |
| **Σφάλματα περιορισμού ρυθμού** | Αυξήστε το `WithRetryCount` ή προσθέστε ένα `Task.Delay` μεταξύ των κλήσεων. |
| **Αποθήκευση σε αποθήκευση cloud** | Αντικαταστήστε τη διαδρομή του συστήματος αρχείων με ένα stream (`MemoryStream`) και ανεβάστε το stream στο Azure Blob Storage ή στο AWS S3. |

## Επαλήθευση του αποτελέσματος

Μετά το τέλος του προγράμματος, ανοίξτε το `Summary_out.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε ένα καθαρό, μονοσέλιδο (ή πολυσέλιδο, ανάλογα με το μήκος) έγγραφο που καταγράφει τις κύριες ιδέες του `SampleDocument.pdf`. Συγκρίνετε τη σύνοψη κειμένου που εκτυπώθηκε στην κονσόλα με την έκδοση PDF — και οι δύο πρέπει να ταιριάζουν ακριβώς.

Αν η σύνοψη φαίνεται ελλιπής:

1. Μειώστε το `WithTemperature` σε 0.2 για πιο καθοριστική έξοδο.
2. Αυξήστε το

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε PDF σε C# – Προσθήκη σελίδας, Σχεδίαση ορθογωνίου & Αποθήκευση](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Μάθετε πώς να δημιουργείτε έγγραφα PDF με το Aspose.PDF για .NET](/pdf/english/net/document-creation/)
- [Πώς να δημιουργήσετε Tagged PDFs με το Aspose.PDF για .NET – Βελτιώστε την προσβασιμότητα](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}