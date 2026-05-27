---
category: general
date: 2026-03-22
description: Πώς να εκτελέσετε OCR σε αρχεία PDF χρησιμοποιώντας το Aspose.Pdf σε
  C#. Μάθετε πώς να μετατρέψετε σαρωμένα PDF, να κάνετε το PDF αναζητήσιμο και να
  φορτώνετε έγγραφο PDF χωρίς κόπο.
draft: false
keywords:
- how to run OCR
- run OCR on pdf
- convert scanned pdf
- make pdf searchable
- load pdf document
language: el
og_description: Πώς να εκτελέσετε OCR σε αρχεία PDF με το Aspose.Pdf. Αυτό το σεμινάριο
  σας δείχνει πώς να μετατρέψετε σαρωμένα PDF, να κάνετε το PDF αναζητήσιμο και να
  φορτώσετε έγγραφο PDF σε C#.
og_title: Πώς να εκτελέσετε OCR σε PDF – Πλήρης οδηγός C#
tags:
- OCR
- Aspose.Pdf
- C#
- PDF processing
title: Πώς να εκτελέσετε OCR σε PDF με το Aspose.Pdf – Πλήρης οδηγός C#
url: /el/net/advanced-features/how-to-run-ocr-on-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε PDF – Πλήρης Οδηγός C#

Η εκτέλεση OCR σε αρχεία PDF είναι ένα κοινό εμπόδιο όταν εργάζεστε με σαρωμένα έγγραφα. Έχετε προσπαθήσει ποτέ να αναζητήσετε ένα σαρωμένο τιμολόγιο και να συναντήσετε πρόβλημα; Δεν είστε μόνοι. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **run OCR on PDF** χρησιμοποιώντας το Aspose.Pdf, μετατρέποντας μια θολή σάρωση σε ένα πλήρως αναζητήσιμο έγγραφο. Στο τέλος θα γνωρίζετε επίσης πώς να **convert scanned PDF**, **make PDF searchable**, και φυσικά **load PDF document** αντικείμενα χωρίς καμία δυσκολία.

Θα καλύψουμε τα πάντα, από τη ρύθμιση του έργου μέχρι την επαλήθευση του αποτελέσματος. Χωρίς χέρια‑απλωμένα, χωρίς συντομεύσεις «δείτε τα docs»—απλώς ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να επικολλήσετε στο Visual Studio σήμερα. Αν αναρωτιέστε αν αυτό λειτουργεί με .NET 6 ή .NET Framework 4.8, η απάντηση είναι ναι· το Aspose.Pdf υποστηρίζει και τις δύο, και ο κώδικας παρακάτω προσαρμόζεται αυτόματα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- **Aspose.Pdf for .NET** (τελευταία έκδοση έως Μάρτιο 2026). Μπορείτε να το κατεβάσετε από το NuGet: `Install-Package Aspose.Pdf`.
- Ένα **scanned PDF** που θέλετε να επεξεργαστείτε (τοποθετήστε το σε φάκελο που μπορείτε να αναφέρετε, π.χ., `YOUR_DIRECTORY/input.pdf`).
- .NET 6 SDK ή νεότερο (η σύνταξη χρησιμοποιεί `using var` που υποστηρίζεται από C# 8 και μετά).
- Ένα IDE της επιλογής σας—Visual Studio, Rider ή VS Code λειτουργούν εξίσου καλά.

Αυτό είναι όλο. Χωρίς επιπλέον μηχανές OCR, χωρίς εξωτερικές υπηρεσίες. Το ενσωματωμένο `OcrPlugin` του Aspose κάνει όλη τη βαριά δουλειά.

## Πώς να Εκτελέσετε OCR – Κύρια Βήματα

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα. Αποθηκεύστε το ως `Program.cs` και τρέξτε το· η κονσόλα θα τερματίσει σιωπηλά, και θα βρείτε ένα αναζητήσιμο PDF δίπλα στο αρχείο εισόδου.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Plugins;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document you want to OCR
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Step 2: Create a PluginManager – this is the hub for all PDF plugins
        var pluginManager = new PluginManager();

        // Step 3: Register the built‑in OCR plugin (the one that actually reads the image)
        pluginManager.RegisterPlugin(new OcrPlugin());

        // Step 4: Prepare execution options – here we set English as the language.
        // You can add more languages by comma‑separating them, e.g., "eng,spa".
        var ocrOptions = new PluginExecutionOptions
        {
            Parameters = { ["Language"] = "eng" }
        };

        // Step 5: Execute the OCR plugin on the loaded document.
        // This mutates pdfDocument in‑place, turning each scanned page into searchable text.
        pluginManager.Execute(pdfDocument, ocrOptions);

        // Step 6: Save the OCR‑processed PDF to a new file.
        pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");

        Console.WriteLine("OCR complete! Output saved to ocr-output.pdf");
    }
}
```

### Τι κάνει ο κώδικας, βήμα προς βήμα

1. **Load PDF Document** – Ο κατασκευαστής `Document` διαβάζει το αρχείο στη μνήμη. Αυτό ικανοποιεί την απαίτηση «load pdf document» και μας δίνει ένα μεταβλητό αντικείμενο για εργασία.
2. **Plugin Manager** – Το Aspose απομονώνει προαιρετικές λειτουργίες (όπως OCR) πίσω από έναν διαχειριστή. Σκεφτείτε το ως κουτί εργαλείων όπου διαλέγετε το σωστό σφυρί.
3. **Register OCR Plugin** – Καλώντας `RegisterPlugin(new OcrPlugin())` λέμε στο Aspose ότι σκοπεύουμε να εκτελέσουμε οπτική αναγνώριση χαρακτήρων.
4. **Execution Options** – Το `PluginExecutionOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς τη διαδικασία. Ορίζοντας `Language` σε `"eng"` λέτε στη μηχανή να ψάξει για αγγλικούς χαρακτήρες. Μπορείτε επίσης να προσθέσετε `"spa"` για ισπανικά ή `"deu"` για γερμανικά.
5. **Run the OCR** – `pluginManager.Execute` διασχίζει κάθε σελίδα, εξάγει την εικόνα raster, τρέχει τη μηχανή OCR και προσθέτει ένα αόρατο στρώμα κειμένου. Αυτό είναι το βασικό μέρος του **run OCR on pdf**.
6. **Save the Result** – Το τελικό PDF περιέχει τώρα ένα κρυφό στρώμα κειμένου, κάνοντάς το **make PDF searchable**. Ανοίγοντας το σε Adobe Reader και χρησιμοποιώντας το εργαλείο Find, θα βρείτε οποιαδήποτε λέξη πληκτρολογήσατε.

## Βήμα 1: Load PDF Document

Μπορεί να αναρωτιέστε γιατί χρησιμοποιούμε `using var` αντί για ένα απλό `new Document()`. Η δήλωση `using` εγγυάται ότι το χειριστήριο αρχείου απελευθερώνεται αμέσως μόλις τελειώσουμε, κάτι κρίσιμο όταν αργότερα προσπαθείτε να αντικαταστήσετε το ίδιο αρχείο στα Windows.

```csharp
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Αν η διαδρομή είναι λανθασμένη, το Aspose ρίχνει `FileNotFoundException`. Ελέγξτε ξανά τα δικαιώματα του φακέλου—ιδιαίτερα σε Linux όπου η ευαισθησία σε πεζά‑κεφαλαία μπορεί να προκαλέσει προβλήματα.

## Βήμα 2: Register and Configure the OCR Plugin

Το OCR plugin δεν φορτώνεται από προεπιλογή για να κρατήσει τη βασική βιβλιοθήκη ελαφριά. Η καταχώρησή του γίνεται με μία γραμμή, αλλά μπορείτε επίσης να αλυσίδα πολλαπλά plugins (π.χ., έναν αφαιρετή υδατογραφήματος) αν η ροή εργασίας σας το απαιτεί.

```csharp
var pluginManager = new PluginManager();
pluginManager.RegisterPlugin(new OcrPlugin());
```

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε εκατοντάδες PDF σε batch, δημιουργήστε το `PluginManager` μία φορά και επαναχρησιμοποιήστε το. Η δημιουργία του ανά αρχείο προσθέτει περιττό φορτίο.

## Βήμα 3: Execute the OCR Process (Convert Scanned PDF)

Τώρα έρχεται η βαριά δουλειά. Η μέθοδος `Execute` σαρώνει κάθε σελίδα, τρέχει OCR και γράφει το κείμενο πίσω στο PDF. Είναι αποδοτική—το Aspose μεταδίδει τα δεδομένα εικόνας σε ροή, ώστε να μην εξαντλήσετε τη μνήμη ακόμη και με σαρώσεις 200 σελίδων.

```csharp
var ocrOptions = new PluginExecutionOptions
{
    Parameters = { ["Language"] = "eng" }
};

pluginManager.Execute(pdfDocument, ocrOptions);
```

**Γιατί να ορίσετε τη γλώσσα;** Η ακρίβεια του OCR εξαρτάται σε μεγάλο βαθμό από το μοντέλο γλώσσας. Η παροχή του `"eng"` λέει στη μηχανή να δώσει προτεραιότητα στα αγγλικά σχήματα χαρακτήρων, μειώνοντας τα ψευδώς θετικά.

## Βήμα 4: Save and Verify a Searchable PDF

Η αποθήκευση είναι απλή, αλλά η επαλήθευση είναι το σημείο όπου πολλοί προγραμματιστές κολλάνε. Μετά την εκτέλεση, ανοίξτε το αποτέλεσμα σε οποιονδήποτε προβολέα PDF και δοκιμάστε τη συντόμευση **Ctrl + F**. Αν μπορείτε να βρείτε λέξεις που αρχικά ήταν μόνο εικόνες, έχετε επιτυχώς **make PDF searchable**.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");
```

![Αναζητήσιμο PDF μετά το OCR – πώς να εκτελέσετε OCR σε PDF](/images/ocr-searchable.png "Αποτέλεσμα αναζητήσιμου PDF μετά το πώς να εκτελέσετε OCR σε PDF")

*Το παραπάνω στιγμιότυπο δείχνει το κρυφό στρώμα κειμένου να επισημαίνεται όταν ψάχνετε έναν όρο.*

## Συνηθισμένα Προβλήματα & Pro Tips

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Blank output** | Λείπει η παράμετρος γλώσσας ή έχει οριστεί κωδικός που δεν υποστηρίζεται. | Βεβαιωθείτε ότι `["Language"] = "eng"` (ή άλλος κωδικός ISO‑639‑2). |
| **Slow processing** | Μεγάλες εικόνες χωρίς down‑sampling. | Προσθέστε `["Resolution"] = "300"` στα `Parameters` ώστε το OCR να δουλεύει σε χαμηλότερο DPI. |
| **Missing fonts** | Το OCR δημιουργεί κείμενο αλλά ο προβολέας δεν μπορεί να αποδώσει τη γραμματοσειρά. | Ενσωματώστε τις γραμματοσειρές ορίζοντας `pdfDocument.FontEmbeddingMode = FontEmbeddingMode.Always`. |
| **Memory leaks** | Δεν γίνεται διαχείριση του αντικειμένου `Document`. | Χρησιμοποιήστε `using var` όπως φαίνεται, ή καλέστε `pdfDocument.Dispose()` χειροκίνητα. |

### Edge Cases

- **Multi‑language PDFs:** Περνάτε μια λίστα χωρισμένη με κόμμα όπως `"eng,spa,fra"` για να διαχειριστείτε μεικτό περιεχόμενο.
- **Password‑protected files:** Φορτώστε με `new Document("file.pdf", new LoadOptions { Password = "secret" })`.
- **Selective OCR:** Αν χρειάζεστε OCR μόνο σε συγκεκριμένες σελίδες, δημιουργήστε ένα αντικείμενο `PageRange` και περάστε το μέσω `Parameters["Pages"] = "1-3,5"`.

## Recap: What We Achieved

- **How to run OCR on PDF** χρησιμοποιώντας το ενσωματωμένο plugin του Aspose.Pdf.
- **Convert scanned PDF** σε μια αναζητήσιμη έκδοση χωρίς εξωτερικές υπηρεσίες.
- **Make PDF searchable** ώστε οι τελικοί χρήστες να μπορούν να βρουν κείμενο άμεσα.
- **Load PDF document** με ασφάλεια και να απελευθερώνετε πόρους άμεσα.

Όλα αυτά σε λιγότερο από 30 γραμμές καθαρού C#.

## What to Try Next

- Πειραματιστείτε με διαφορετικές γλώσσες για OCR πολυγλωσσικών συμβάσεων.
- Συνδυάστε OCR με **text extraction** (`pdfDocument.Pages[i].ExtractText()`) για αυτοματοποιημένη εισαγωγή δεδομένων.
- Χρησιμοποιήστε το **Redaction plugin** για να αφαιρέσετε ευαίσθητες πληροφορίες πριν το OCR, εξασφαλίζοντας συμμόρφωση.
- Αναπτύξτε τον κώδικα ως μικροϋπηρεσία πίσω από ένα API endpoint ώστε μη‑προγραμματιστές να μπορούν να ανεβάζουν σάρωσες και να λαμβάνουν αμέσως αναζητήσιμα PDF.

Έχετε ερωτήσεις σχετικά με την κλιμάκωση στο cloud ή την ενσωμάτωση με Azure Functions; Αφήστε ένα σχόλιο και θα εξερευνήσουμε μαζί αυτά τα σενάρια. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}