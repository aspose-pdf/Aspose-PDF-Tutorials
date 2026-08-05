---
category: general
date: 2026-08-04
description: Δημιουργήστε AI Copilot για τη δημιουργία περιγραφής εικόνας για αρχεία
  PDF. Μάθετε πώς να ρυθμίσετε τις επιλογές εικόνας του OpenAI και να εξάγετε περιγραφή
  εικόνας αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: el
lastmod: 2026-08-04
og_description: Δημιουργήστε AI Copilot για τη δημιουργία περιγραφής εικόνας για αρχεία
  PDF. Αυτός ο οδηγός δείχνει πώς να ρυθμίσετε τις επιλογές εικόνας του OpenAI, να
  εκτελέσετε το copilot και να εξάγετε την περιγραφή εικόνας σε C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Δημιουργήστε AI Copilot για περιγραφή εικόνων PDF – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Δημιουργήστε AI Copilot για περιγραφή εικόνων PDF – βήμα‑βήμα οδηγός
url: /el/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία AI Copilot για περιγραφή εικόνας PDF – πλήρης οδηγός

Αν χρειάζεστε **να δημιουργήσετε AI Copilot** που αυτόματα γράφει περιγραφές για τις εικόνες ενσωματωμένες σε ένα PDF, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να ρυθμίζετε τις επιλογές εικόνας του OpenAI, να εκτελείτε το copilot και **να εξάγετε περιγραφή εικόνας** χωρίς να βγείτε από το έργο C#.

Η δημιουργία κειμενικού περιεχομένου για εικόνες PDF είναι μια κοινή απαίτηση για προσβασιμότητα, ευρετηρίαση περιεχομένου και αυτοματοποιημένες αναφορές. Στο τέλος αυτού του tutorial θα έχετε ένα επαναχρησιμοποιήσιμο στοιχείο που **δημιουργεί περιγραφή εικόνας** για οποιοδήποτε PDF έγγραφο στο οποίο το κατευθύνετε.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Άδεια Aspose.Pdf.AI (ή δωρεάν δοκιμή)  
* Κλειδί API του OpenAI που μπορεί να χρησιμοποιήσει ο πελάτης Aspose  
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#)  

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από `Aspose.Pdf.AI`.

## Βήμα 1: Ρύθμιση του πελάτη Aspose.Pdf.AI

Το πρώτο βήμα είναι η δημιουργία του AI πελάτη με τα στοιχεία πιστοποίησής σας. Ο πελάτης διαχειρίζεται την επικοινωνία με την υπηρεσία OpenAI στο παρασκήνιο.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Γιατί είναι σημαντικό:** Το `AiClient` ενσωματώνει όλες τις ρυθμίσεις επιπέδου αιτήματος (κλειδί API, χρονικό όριο, πολιτική επανάληψης). Η δημιουργία του μία φορά και η επαναχρησιμοποίησή του σε πολλαπλές παρουσίες copilot μειώνει το φορτίο και εξασφαλίζει συνεπή πιστοποίηση.

## Βήμα 2: Δημιουργία Copilot για Περιγραφή Εικόνας

Τώρα δημιουργείτε το **AI copilot** που θα διαβάσει το PDF και θα παράγει μια περιγραφή για κάθε εικόνα. Η μέθοδος `CreateImageDescriptionCopilot` δέχεται τον πελάτη και ένα σύνολο επιλογών που ορίζουν πώς δημιουργείται η περιγραφή.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Γιατί είναι σημαντικό:**  
* Το `OpenAIImageDescriptionOptions` (οι **επιλογές εικόνας OpenAI**) σας επιτρέπουν να ρυθμίσετε λεπτομερώς το μοντέλο γλώσσας. Η προσαρμογή της θερμοκρασίας ή του μοντέλου μπορεί να βελτιώσει τη σχετικότητα για τεχνικά διαγράμματα έναντι φυσικών φωτογραφιών.  
* Η καθορισμένη διαδρομή του εγγράφου λέει στο copilot ποιο PDF πρέπει να σαρώσει. Το copilot εξάγει κάθε raster εικόνα, την στέλνει στο μοντέλο και επιστρέφει μια περιγραφή κατανοητή από άνθρωπο.

## Βήμα 3: Ανάκτηση της παραγόμενης περιγραφής ασύγχρονα

Το copilot λειτουργεί ασύγχρονα επειδή μπορεί να χρειαστεί να ανεβάσει αρκετά megabytes δεδομένων εικόνας και να περιμένει την απόκριση του μοντέλου. Χρησιμοποιήστε `await` για να εξασφαλίσετε ότι η κλήση ολοκληρώνεται πριν προσπελάσετε το αποτέλεσμα.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Γιατί είναι σημαντικό:** Η μέθοδος επιστρέφει ένα `Dictionary<int, string>` που αντιστοιχίζει κάθε σελίδα (ή δείκτη εικόνας) στην περιγραφή της. Η διαχείριση του `AiException` σας επιτρέπει να εμφανίζετε σφάλματα δικτύου ή ορίου αντί να καταρρέει η εφαρμογή.

## Βήμα 4: Εμφάνιση ή αποθήκευση της περιγραφής

Μπορείτε να γράψετε τις περιγραφές στην κονσόλα, σε αρχείο καταγραφής ή να τις ενσωματώσετε ξανά στο PDF ως alt‑text για προσβασιμότητα. Παρακάτω υπάρχει ένα γρήγορο παράδειγμα που γράφει το αποτέλεσμα σε αρχείο JSON για μελλοντική χρήση.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Γιατί είναι σημαντικό:** Η αποθήκευση του αποτελέσματος ως JSON διατηρεί τη συσχέτιση μεταξύ κάθε σελίδας και της περιγραφής της, καθιστώντας εύκολο για επόμενες διαδικασίες (ευρετηρίαση, απόδοση UI κ.λπ.) να καταναλώσουν τα δεδομένα.

## Διαχείριση πολλαπλών εικόνων ανά σελίδα

Αν μια σελίδα περιέχει πολλές εικόνες, το copilot επιστρέφει μια ενωμένη περιγραφή χωρισμένη με αλλαγές γραμμής. Για να τις διαχωρίσετε, εξετάστε το ακατέργαστο αποτέλεσμα και χωρίστε το με `\n\n` (διπλή νέα γραμμή). Εδώ είναι μια βοηθητική μέθοδος:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Μπορείτε στη συνέχεια να επαναλάβετε πάνω σε κάθε μεμονωμένη περιγραφή εικόνας και να τις αποθηκεύσετε ξεχωριστά εάν χρειάζεται.

## Edge case: Μεγάλα PDFs και διαχείριση χρονικού ορίου

Η επεξεργασία ενός PDF μεγαλύτερου από 100 MB μπορεί να υπερβεί τα προεπιλεγμένα χρονικά όρια HTTP. Προσαρμόστε τη ρύθμιση του χρονικού ορίου του πελάτη όταν δημιουργείτε το `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Η αύξηση του χρονικού ορίου αποτρέπει την πρόωρη διακοπή ενώ η υπηρεσία επεξεργάζεται πολλές εικόνες υψηλής ανάλυσης.

## Pro tip: Cache αποτελεσμάτων για μείωση κόστους

Το OpenAI χρεώνει ανά token, και η περιγραφή εικόνας μπορεί να είναι επαναλαμβανόμενη σε εκδόσεις της ίδιας αναφοράς. Αποθηκεύστε την έξοδο JSON στην cache και επαναχρησιμοποιήστε την όταν το hash του PDF ταιριάζει με ένα προηγουμένως επεξεργασμένο αρχείο. Αυτή η πρακτική εξοικονομεί χρήματα και επιταχύνει τις επόμενες εκτελέσεις.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Αποθηκεύστε το hash μαζί με το αρχείο JSON· αν το hash ταιριάζει σε μια μετέπειτα εκτέλεση, παραλείψτε την κλήση AI.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να επικολλήσετε σε ένα νέο .NET project.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα (κομμένο)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Το πρόγραμμα διαβάζει το `AnnualReport.pdf`, δημιουργεί ένα **AI copilot** και γράφει ένα αρχείο JSON που αντιστοιχίζει κάθε σελίδα στην παραγόμενη περιγραφή της.

## Συχνές ερωτήσεις

* **Λειτουργεί αυτό με κρυπτογραφημένα PDFs;**  
  Ναι, αλλά πρέπει να παρέχετε τον κωδικό πρόσβασης όταν δημιουργείτε το copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Μπορώ να περιορίσω την επεξεργασία σε συγκεκριμένες σελίδες;**  
  Χρησιμοποιήστε `imageOptions.WithPageRange(1, 10)` για να περιορίσετε το copilot στις σελίδες 1‑10.

* **Τι γίνεται αν μια εικόνα περιέχει κείμενο;**  
  Το μοντέλο προσπαθεί να περιγράψει το οπτικό περιεχόμενο· για εξαγωγή κειμένου τύπου OCR θα πρέπει να χρησιμοποιήσετε το `CreateTextExtractionCopilot` αντί αυτού.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε AI Copilot** που **δημιουργεί περιγραφή εικόνας** για αρχεία PDF, να ρυθμίσετε **επιλογές εικόνας OpenAI** και να **εξάγετε περιγραφή εικόνας** προγραμματιστικά σε C#. Το πλήρες παράδειγμα δείχνει βέλτιστες πρακτικές όπως η ασύγχρονη διαχείριση, η διαχείριση σφαλμάτων και η cache αποτελεσμάτων.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη των παραγόμενων περιγραφών πίσω στο PDF ως alt‑text για βελτιωμένη προσβασιμότητα (`PdfDocument` → `PdfImage.AlternativeText`).  
* Χρήση του ίδιου μοτίβου copilot για **δημιουργία PDF αναφορών περιγραφής εικόνας** σε μαζική επεξεργασία.  
* Πειραματισμός με διαφορετικά μοντέλα OpenAI ή ρυθμίσεις θερμοκρασίας για λεπτομερή προσαρμογή του στυλ περιγραφής.

Νιώστε ελεύθεροι να προσαρμόσετε τον κώδικα, να πειραματιστείτε με μεγαλύτερα έγγραφα και να ενσωματώσετε το αποτέλεσμα στη διαδικασία ευρετηρίασής σας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία PDF με Ετικεταρισμένη Εικόνα σε Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Δημιουργία PDF με Ετικεταρισμένη Εικόνα](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Δημιουργία Ετικεταρισμένης Εικόνας PDF σε .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}