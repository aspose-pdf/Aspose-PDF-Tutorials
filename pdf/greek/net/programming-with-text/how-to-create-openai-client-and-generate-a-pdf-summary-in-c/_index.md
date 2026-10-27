---
category: general
date: 2026-10-26
description: Μάθετε πώς να δημιουργήσετε πελάτη OpenAI, να μετατρέψετε PDF σε περίληψη
  και να αποθηκεύσετε την περίληψη PDF χρησιμοποιώντας το Aspose.Pdf.AI σε λίγα εύκολα
  βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- generate pdf summary
- create summary copilot
- save summary pdf
language: el
lastmod: 2026-10-26
og_description: Δημιουργήστε πελάτη OpenAI και μετατρέψτε οποιοδήποτε PDF σε σύντομη
  περίληψη. Αυτός ο οδηγός σας δείχνει πώς να δημιουργήσετε περίληψη PDF και να αποθηκεύσετε
  το PDF περίληψης χρησιμοποιώντας το Aspose.Pdf.AI.
og_image_alt: C# code displaying creation of OpenAI client and PDF summary generation
og_title: Δημιουργήστε πελάτη OpenAI και δημιουργήστε σύνοψη PDF με C# – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create OpenAI client, convert PDF to summary and save
    summary PDF using Aspose.Pdf.AI in a few easy steps.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
tags:
- openai
- pdf
- csharp
- summary
- ai
title: Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε μια σύνοψη PDF σε C#
url: /el/net/programming-with-text/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε πελάτη OpenAI και να δημιουργήσετε σύνοψη PDF σε C#

Αν χρειάζεστε **να δημιουργήσετε πελάτη OpenAI** που μπορεί να διαβάσει ένα PDF και να επιστρέψει μια σύντομη σύνοψη, αυτό το tutorial σας δείχνει ακριβώς πώς να το κάνετε. Στο τέλος του οδηγού θα μπορείτε να **μετατρέψετε PDF σε σύνοψη**, να παράγετε ένα **έγγραφο σύνοψης PDF** και να **αποθηκεύσετε τη σύνοψη PDF** στο δίσκο—όλα με το Aspose.Pdf.AI.

Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, και συμβουλές για την αντιμετώπιση κοινών προβλημάτων όπως μεγάλα αρχεία ή προσαρμοσμένες ρυθμίσεις θερμοκρασίας. Δεν απαιτείται εξωτερική τεκμηρίωση· όλα όσα χρειάζεστε περιλαμβάνονται εδώ.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη.
* Άδεια Aspose.Pdf for .NET (ή δωρεάν δοκιμή) που περιλαμβάνει το AI module.
* Κλειδί API του OpenAI με αρκετά credits για το αίτημα σύνοψης.
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET).

Ο κώδικας παρακάτω στοχεύει σε C# 10, αλλά οι ίδιες έννοιες ισχύουν και για παλαιότερες εκδόσεις με μικρές αλλαγές σύνταξης.

## Βήμα 1: Δημιουργία πελάτη OpenAI

Η δημιουργία του πελάτη OpenAI είναι το θεμέλιο κάθε λειτουργίας PDF με AI. Ο πελάτης περιλαμβάνει την αυθεντικοποίηση, τη διαχείριση HTTP και τον έλεγχο ρυθμού αιτήσεων, ώστε να χρειάζεται να παρέχετε το κλειδί API μόνο μία φορά.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

// Replace with your real key – never hard‑code it in production code.
const string ApiKey = "YOUR_OPENAI_API_KEY";

await using var openAiClient = OpenAIClient
    .CreateWithApiKey(ApiKey)   // supply your OpenAI key
    .Build();                    // builds a reusable HttpClient internally
```

**Γιατί είναι σημαντικό:**  
* `CreateWithApiKey` ελέγχει τη μορφή του κλειδιού νωρίς, αποτρέποντας σφάλματα 401 κατά την εκτέλεση.  
* `Build()` επιστρέφει ένα `IAsyncDisposable` ώστε οι υποκείμενες συνδέσεις HTTP να απελευθερώνονται αυτόματα όταν λήγει το μπλοκ `using`.  
* Η χρήση `await using` εξασφαλίζει ασύγχρονη αποδέσμευση, κάτι απαραίτητο για σενάρια υψηλής απόδοσης.

> **Pro tip:** Αποθηκεύστε το κλειδί API σε μεταβλητή περιβάλλοντος (`OPENAI_API_KEY`) και διαβάστε το με `Environment.GetEnvironmentVariable`. Αυτό κρατά τα μυστικά μακριά από τον έλεγχο έκδοσης.

## Βήμα 2: Διαμόρφωση επιλογών copilot σύνοψης

Το copilot σύνοψης καθορίζει πώς το AI επεξεργάζεται το PDF. Μπορείτε να ρυθμίσετε τη δημιουργικότητα με την παράμετρο *temperature* και να υποδείξετε το πηγαίο έγγραφο.

```csharp
var summaryOptions = OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.5)                     // 0 = deterministic, 1 = very creative
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to the PDF you want to summarise
```

**Γιατί είναι σημαντικό:**  
* Μια θερμοκρασία `0.5` δίνει ισορροπημένο αποτέλεσμα—αρκετή ποικιλία για φυσικό ήχο, αλλά παραμένει πιστό στην πηγή.  
* `WithDocument` φορτώνει το αρχείο στον εσωτερικό parser PDF του Aspose, ο οποίος εξάγει κείμενο, εικόνες και πληροφορίες διάταξης πριν το στείλει στο OpenAI.  
* Αν το PDF είναι μεγαλύτερο από 5 MB, σκεφτείτε να το χωρίσετε σε ενότητες και να συνοψίσετε κάθε μέρος ξεχωριστά για να παραμείνετε εντός των ορίων token.

## Βήμα 3: Δημιουργία copilot σύνοψης

Τώρα που έχετε πελάτη και επιλογές, δημιουργήστε το copilot. Το copilot αφαιρεί την πολυπλοκότητα του κύκλου αίτη‑απάντη και προσφέρει βοηθητικές μεθόδους για αποτελέσματα τόσο σε plain‑text όσο και σε PDF.

```csharp
ISummaryCopilot summaryCopilot = AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

**Γιατί είναι σημαντικό:**  
* `AICopilotFactory` εγγυάται ότι το copilot χρησιμοποιεί το ίδιο HTTP pipeline με τον πελάτη, διατηρώντας το pooling των συνδέσεων.  
* Η επιστρεφόμενη διεπαφή `ISummaryCopilot` σας επιτρέπει να αλλάξετε υλοποιήσεις αργότερα (π.χ. mock για unit testing) χωρίς να τροποποιήσετε τον υπόλοιπο κώδικα.

## Βήμα 4: Ανάκτηση της σύνοψης ως plain text

Αν χρειάζεστε μόνο τη λεκτική σύνοψη—για logging, εμφάνιση UI ή περαιτέρω επεξεργασία—καλέστε `GetSummaryAsync`.

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Summary ===");
Console.WriteLine(summaryText);
```

**Τι θα δείτε:**  
Μια σύντομη παράγραφο (ή μερικά bullet points) που αποτυπώνει τις κύριες ιδέες του πηγαίου PDF. Το μήκος εξαρτάται από το αρχικό έγγραφο και το προϋπολογισμό token του μοντέλου.

### Διαχείριση μεγάλων εξόδων

Αν η σύνοψη είναι μεγαλύτερη από ό,τι περιμένατε, μπορείτε να περιορίσετε τον αριθμό token με `WithMaxTokens` κατά τη δημιουργία του `summaryOptions`. Για παράδειγμα:

```csharp
summaryOptions = summaryOptions.WithMaxTokens(300);
```

## Βήμα 5: Δημιουργία σύνοψης PDF (convert PDF to summary)

Όταν χρειάζεστε ένα οπτικό αποτέλεσμα—π.χ. για να το μοιραστείτε με μη‑τεχνικούς ενδιαφερόμενους—χρησιμοποιήστε τη μέθοδο δημιουργίας PDF. Αυτό το βήμα **convert pdf to summary** και **generate pdf summary** σε μία κλήση.

```csharp
Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();
```

Το αντικείμενο `Document` που επιστρέφεται είναι ένα πλήρως λειτουργικό έγγραφο Aspose.Pdf που περιέχει το κείμενο της σύνοψης, προαιρετικές επικεφαλίδες και τα μεταδεδομένα του αρχικού PDF (αν τα διατηρήσετε).

**Γιατί είναι σημαντικό:**  
* Το PDF διατηρεί διανυσματική ποιότητα, καθιστώντας το κατάλληλο για εκτύπωση ή ενσωμάτωση σε άλλες αναφορές.  
* Το Aspose προσθέτει αυτόματα μια σελίδα τίτλου με το όνομα του πηγαίου αρχείου και χρονική σήμανση, κάτι που βοηθά στα audit trails.

## Βήμα 6: Αποθήκευση PDF σύνοψης (save summary pdf)

Τέλος, γράψτε το παραγόμενο PDF στο δίσκο. Η βοηθητική μέθοδος `SaveSummaryAsync` συνδυάζει τα βήματα 5 και 6, αλλά θα δείξουμε την ρητή αποθήκευση για να επισημάνουμε ζητήματα συστήματος αρχείων.

```csharp
string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";
await summaryCopilot.SaveSummaryAsync(outputPath);
Console.WriteLine($"Summary PDF saved to {outputPath}");
```

**Καλές πρακτικές για αποθήκευση αρχείων:**

| Κατάσταση                               | Σύσταση                                           |
|----------------------------------------|---------------------------------------------------|
| Εκτέλεση σε Windows και Linux          | Χρησιμοποιήστε `Path.Combine` για δημιουργία διαδρομών ανεξάρτητων από το OS. |
| Πολλαπλές ταυτόχρονες συνόψεις          | Προσθέστε GUID ή χρονική σήμανση στο όνομα αρχείου. |
| Υπηρεσία μεγάλης διάρκειας (π.χ., web API) | Αποθηκεύστε τα PDFs σε αφιερωμένο blob storage αντί για το τοπικό σύστημα αρχείων. |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο console project (`dotnet new console`). Περιλαμβάνει όλες τις απαιτούμενες δηλώσεις `using` και δείχνει τη συνολική ροή από **create openai client** μέχρι **save summary pdf**.

```csharp
// Program.cs
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    // Replace with your actual OpenAI key or read from env variables.
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    static async Task Main()
    {
        // 1️⃣ Create OpenAI client
        await using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // 2️⃣ Configure summary copilot options
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to source PDF

        // 3️⃣ Create the summary copilot
        ISummaryCopilot summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Get plain‑text summary (optional)
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(summaryText);
        Console.WriteLine();

        // 5️⃣ Generate PDF summary (convert pdf to summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // 6️⃣ Save the generated PDF (save summary pdf)
        string outputPath = Path.Combine("YOUR_DIRECTORY", "Summary_out.pdf");
        await summaryCopilot.SaveSummaryAsync(outputPath);
        Console.WriteLine($"✅ PDF summary saved at: {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα**

```
=== Plain‑text summary ===
This document outlines the quarterly performance metrics, highlighting a 12% increase in revenue and a 5% reduction in operational costs...

✅ PDF summary saved at: YOUR_DIRECTORY\Summary_out.pdf
```

Ανοίξτε το παραγόμενο `Summary_out.pdf` και θα δείτε μια καλοσχεδιασμένη σελίδα που περιέχει το ίδιο κείμενο, καθώς και μια κεφαλίδα με το όνομα του αρχικού αρχείου και χρονική σήμανση.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|----------|
| *Τι γίνεται αν το PDF περιέχει σαρωμένες εικόνες;* | Το Aspose.Pdf.AI εκτελεί αυτόματα OCR όταν κληθεί το `WithDocument`, αλλά μπορείτε να βελτιώσετε την ακρίβεια ορίζοντας `WithOcrLanguage("eng")`. |
| *Μπορώ να συνοψίσω πολλαπλά PDFs σε μία κλήση;* | Δεν απευθείας. Δημιουργήστε ξεχωριστό `summaryCopilot` για κάθε αρχείο ή ενώστε τα PDFs πριν τη σύνοψη. |
| *Πώς αλλάζω τη γλώσσα εξόδου;* | Χρησιμοποιήστε `summaryOptions.WithLanguage("fr")` για να ζητήσετε από το μοντέλο να επιστρέψει κείμενο στα Γαλλικά. |
| *Τι γίνεται αν το αίτημα υπερβεί τα όρια token;* | Μειώστε το `WithMaxTokens` ή χωρίστε το PDF σε ενότητες και συνοψίστε κάθε μέρος ξεχωριστά. |
| *Το παραγόμενο PDF είναι αναζητήσιμο;* | Ναι. Το κείμενο της σύνοψης ενσωματώνεται ως επιλέξιμο κείμενο, όχι μόνο ως εικόνα. |

## Συμπέρασμα

Τώρα ξέρετε πώς να **create OpenAI client**, να διαμορφώσετε ένα **create summary copilot**, να **convert PDF to summary**, να **generate PDF summary** και τέλος να **save summary pdf** χρησιμοποιώντας το Aspose.Pdf.AI σε C#. Αυτή η ολοκληρωμένη ροή σας επιτρέπει να προσθέσετε AI‑βασισμένη σύνοψη σε οποιαδήποτε εφαρμογή .NET με λίγες μόνο γραμμές κώδικα.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* **Προσαρμογή prompt engineering** με `WithPrompt("Summarise in three bullet points.")`.  
* **Ενσωμάτωση με ASP.NET Core** για να εκθέσετε ένα REST endpoint που επιστρέφει τη σύνοψη PDF κατόπιν αιτήματος.  
* **Συνδυασμός με άλλες υπηρεσίες AI** (π.χ. μετάφραση) για παραγωγή πολυγλωσσικών συνόψεων.

Μη διστάσετε να πειραματιστείτε με τις ρυθμίσεις θερμοκρασίας, max‑token και OCR ώστε να ταιριάζουν στις συγκεκριμένες ανάγκες του έργου σας. Καλό coding!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση.

- [Generate PDF summary with Aspose.Pdf.AI and OpenAI](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)
- [How to convert PDF to summary with Aspose.Pdf.AI in C#](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [How to Create a PDF Booklet Using Aspose.PDF .NET: A Comprehensive Guide](/pdf/english/net/printing-rendering/create-pdf-booklet-using-asposepdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}