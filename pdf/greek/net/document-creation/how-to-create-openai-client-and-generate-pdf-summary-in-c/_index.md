---
category: general
date: 2026-11-25
description: Δημιουργήστε πελάτη OpenAI σε C# και δημιουργήστε μια σύνοψη PDF από
  ένα έγγραφο προέλευσης. Μάθετε πώς να μετατρέψετε το PDF σε σύνοψη, να δημιουργήσετε
  συνοπτικό copilot και να αποθηκεύσετε τη σύνοψη PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- generate pdf summary
- convert pdf to summary
- create summary copilot
- save pdf summary
language: el
lastmod: 2026-11-25
og_description: Δημιουργήστε πελάτη OpenAI σε C# και δημιουργήστε μια σύνοψη PDF από
  ένα πηγαίο έγγραφο. Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να μετατρέψετε το
  PDF σε σύνοψη, να δημιουργήσετε έναν συνοπτικό βοηθό και να αποθηκεύσετε τη σύνοψη
  PDF.
og_image_alt: Screenshot showing C# code that creates an OpenAI client and saves a
  PDF summary
og_title: Δημιουργήστε πελάτη OpenAI και δημιουργήστε σύνοψη PDF σε C#
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create OpenAI client in C# and generate a PDF summary from a source
    document. Learn how to convert PDF to summary, create summary copilot, and save
    PDF summary.
  headline: How to create OpenAI client and generate PDF summary in C#
  type: TechArticle
tags:
- OpenAI
- C#
- PDF summary
- Aspose.Pdf.AI
title: Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε σύνοψη PDF σε C#
url: /el/net/document-creation/how-to-create-openai-client-and-generate-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε σύνοψη PDF σε C#

Αν χρειάζεστε **να δημιουργήσετε πελάτη OpenAI** για εργασίες επεξεργασίας εγγράφων, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, ολοκληρωμένη λύση. Θα δείτε πώς να μετατρέψετε ένα αρχείο PDF σε μια σύντομη σύνοψη, να ανακτήσετε τη σύνοψη τόσο ως απλό κείμενο όσο και ως νέο PDF, και τέλος να αποθηκεύσετε αυτή τη σύνοψη PDF στο δίσκο.

Η δημιουργία σύνοψης PDF είναι μια συνηθισμένη απαίτηση όταν θέλετε να αυτοματοποιήσετε την εξαγωγή αναφορών, να δημιουργήσετε εκτελεστικές περιλήψεις ή απλώς να μειώσετε μεγάλα έγγραφα στα κύρια σημεία τους. Το παρακάτω δείγμα κώδικα χρησιμοποιεί το Aspose.Pdf.AI, το οποίο περιβάλλει το OpenAI API και παρέχει έναν βολικό *summary copilot* για αρχεία PDF.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
- Ένα πακέτο NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) προστιθέμενο στο έργο σας  
- Ένα ενεργό κλειδί API του OpenAI (μπορείτε να το αποκτήσετε από το portal του OpenAI)  
- Ένα αρχείο PDF που θέλετε να συνοψίσετε (π.χ., `input.pdf` τοποθετημένο σε γνωστό φάκελο)

Ο οδηγός υποθέτει ότι χρησιμοποιείτε το Visual Studio, αλλά οποιοδήποτε IDE για C# λειτουργεί.

## Δημιουργία πελάτη OpenAI σε C#

Το πρώτο βήμα είναι να **δημιουργήσετε πελάτη OpenAI** με το κλειδί API σας. Το αντικείμενο πελάτη διαχειρίζεται τον έλεγχο ταυτότητας και τη δρομολόγηση των αιτημάτων για όλες τις επόμενες λειτουργίες AI.

```csharp
// Step 1: Initialize the OpenAI client with your API key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")
    .Build();
```

*Γιατί είναι σημαντικό*: Το `OpenAIClient` ενσωματώνει το επίπεδο HTTP, διαχειρίζεται την ανανέωση του token και διασφαλίζει ότι όλες οι κλήσεις στην υπηρεσία σύνοψης είναι σωστά εξουσιοδοτημένες. Χρησιμοποιώντας `using var`, ο πελάτης διαγράφεται αυτόματα όταν η μέθοδος ολοκληρωθεί, απελευθερώνοντας πόρους άμεσα.

## Διαμόρφωση επιλογών σύνοψης (μετατροπή PDF σε σύνοψη)

Στη συνέχεια, διαμορφώνετε πώς η AI πρέπει να αντιμετωπίζει το πηγαίο έγγραφο. Οι επιλογές σας επιτρέπουν να ορίσετε το *temperature* (που ελέγχει την τυχαιότητα) και να υποδείξετε το PDF που θέλετε να συνοψίσετε.

```csharp
// Step 2: Configure summary options (temperature and source document)
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // Path to the PDF you want to summarise
```

*Γιατί είναι σημαντικό*: Ορίζοντας μια μέτρια θερμοκρασία (0.5) λαμβάνετε μια αξιόπιστη, σύντομη σύνοψη χωρίς τις παρερμηνείες που μπορούν να προκύψουν με υψηλότερες τιμές. Η κλήση `WithDocument` ενημερώνει το copilot ποιο αρχείο να διαβάσει, μετατρέποντας ουσιαστικά **PDF σε σύνοψη**.

## Δημιουργία του summary copilot (δημιουργία summary copilot)

Με τον πελάτη και τις επιλογές έτοιμες, μπορείτε τώρα να **δημιουργήσετε summary copilot**. Το αντικείμενο copilot εκθέτει ασύγχρονες μεθόδους για την ανάκτηση της σύνοψης σε διαφορετικές μορφές.

```csharp
// Step 3: Create the summary copilot using the client and options
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*Γιατί είναι σημαντικό*: Το πρότυπο factory απομονώνει τη λογική δημιουργίας, επιτρέποντάς σας να αντικαταστήσετε υλοποιήσεις αργότερα (π.χ., ένα mock copilot για μονάδες δοκιμών). Το προκύπτον `summaryCopilot` είναι η κύρια πύλη για όλες τις λειτουργίες σύνοψης.

## Ανάκτηση της σύνοψης σε απλό κείμενο

Αν χρειάζεστε μόνο το κειμενικό περιεχόμενο, καλέστε το `GetSummaryAsync`. Αυτή η μέθοδος επιστρέφει μια συμβολοσειρά που μπορείτε να εμφανίσετε, να καταγράψετε ή να επεξεργαστείτε περαιτέρω.

```csharp
// Step 4: Retrieve the plain‑text summary
string plainTextSummary = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Plain‑text summary ===");
Console.WriteLine(plainTextSummary);
```

*Αναμενόμενο αποτέλεσμα*: Μια σύντομη παράγραφος (ή μερικά σημεία λίστας) που αποτυπώνει την ουσία του `input.pdf`. Η ακριβής διατύπωση εξαρτάται από το πηγαίο έγγραφο, αλλά το μήκος είναι συνήθως κάτω από 200 λέξεις για μια τυπική αναφορά 10 σελίδων.

## Ανάκτηση της σύνοψης ως έγγραφο PDF (δημιουργία σύνοψης PDF)

Όταν χρειάζεστε ένα κοινόχρηστο αντικείμενο, ζητήστε από το copilot μια έκδοση PDF της σύνοψης. Αυτό το βήμα **δημιουργεί σύνοψη PDF** απευθείας από την υπηρεσία AI.

```csharp
// Step 5: Retrieve the summary as a PDF document
var pdfSummary = await summaryCopilot.GetSummaryDocumentAsync();
```

`pdfSummary` είναι ένα αντικείμενο `Aspose.Pdf.Document`, έτοιμο για περαιτέρω επεξεργασία (π.χ., προσθήκη εξώφυλλου) ή άμεση αποθήκευση.

## Αποθήκευση της σύνοψης PDF σε αρχείο (αποθήκευση σύνοψης PDF)

Τέλος, αποθηκεύστε το παραγόμενο PDF χρησιμοποιώντας τη βοηθητική μέθοδο του copilot. Αυτό επιδεικνύει τη λειτουργία **αποθήκευσης σύνοψης PDF** σε μία γραμμή.

```csharp
// Step 6: Save the PDF summary to a file
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
```

*Γιατί είναι σημαντικό*: Η μέθοδος `SaveSummaryAsync` γράφει το έγγραφο χρησιμοποιώντας τη υψηλής απόδοσης μηχανή PDF της Aspose, διατηρώντας τις γραμματοσειρές, τη διάταξη και τα μεταδεδομένα. Το αποθηκευμένο αρχείο μπορεί να ανοιχτεί σε οποιονδήποτε προβολέα PDF.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που συνδυάζει όλα τα μέρη. Αντιγράψτε τον κώδικα σε ένα νέο έργο κονσόλας και αντικαταστήστε τις τιμές placeholder (`YOUR_API_KEY`, `YOUR_DIRECTORY`) με πραγματικά δεδομένα.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // Initialize the OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey("YOUR_API_KEY")
            .Build();

        // Configure options for summarizing a PDF
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf");

        // Create the summary copilot
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string plainText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(plainText);

        // Get PDF version of the summary
        var pdfDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF summary
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει τη σύνοψη σε απλό κείμενο στην κονσόλα και δημιουργεί το `Summary_out.pdf` στον προορισμό. Το άνοιγμα του PDF εμφανίζει ένα καθαρό, μορφοποιημένο έγγραφο που περιέχει το ίδιο κείμενο σύνοψης, έτοιμο για διανομή.

![Στιγμιότυπο οθόνης του κώδικα C# που δημιουργεί έναν πελάτη OpenAI και αποθηκεύει μια σύνοψη PDF](openai-pdf-summary.png){.center width="600" alt="Στιγμιότυπο οθόνης του κώδικα C# που δημιουργεί έναν πελάτη OpenAI και αποθηκεύει μια σύνοψη PDF"}

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το πηγαίο PDF είναι προστατευμένο με κωδικό;** | Χρησιμοποιήστε την υπερφόρτωση `WithDocument` που δέχεται ροή (stream) και παρέχετε τον κωδικό μέσω `PdfLoadOptions`. Το copilot θα αποκρυπτογραφήσει το αρχείο πριν το συνοψίσει. |
| **Μπορώ να αλλάξω το μήκος της σύνοψης;** | Ρυθμίστε τη θερμοκρασία ή προσθέστε `WithMaxTokens` στο `summaryOptions`. Τα χαμηλότερα όρια token παράγουν πιο σύντομες εξόδους. |
| **Χρειάζομαι σύνδεση στο διαδίκτυο;** | Ναι. Το copilot καλεί την υπηρεσία OpenAI μέσω HTTPS, επομένως απαιτείται σταθερή σύνδεση. |
| **Πώς να διαχειριστείτε μεγάλα PDF (> 100 σελίδες);** | Διαιρέστε το έγγραφο σε μικρότερα τμήματα και συνοψίστε κάθε τμήμα ξεχωριστά, στη συνέχεια συνδυάστε τα αποτελέσματα. Αυτό αποτρέπει την υπέρβαση των ορίων token. |
| **Είναι το παραγόμενο PDF αναζητήσιμο;** | Το PDF περιέχει κείμενο που μπορεί να επιλεγεί, επειδή η σύνοψη αποδίδεται ως κείμενο, όχι ως εικόνα. |

## Συμβουλές από το πεδίο

- **Pro tip:** Αποθηκεύστε στην κρυφή μνήμη (cache) το αντικείμενο `OpenAIClient` για τη διάρκεια ζωής της εφαρμογής σας εάν συνοψίζετε πολλά έγγραφα. Αυτό μειώνει το κόστος σύνδεσης.  
- **Watch out for:** Η χρήση θερμοκρασίας πάνω από 0.7 μπορεί να εισάγει ψευδείς λεπτομέρειες, κάτι που είναι

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα-βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αρχικοποιήσετε τον πελάτη OpenAI API σε C# με Aspose.Pdf.AI και να συνοψίσετε PDF με AI](/pdf/english/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/)
- [Πώς να μετατρέψετε PDF σε σύνοψη με Aspose.Pdf.AI σε C#](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [Δημιουργία σύνοψης PDF με Aspose.Pdf.AI και OpenAI](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}