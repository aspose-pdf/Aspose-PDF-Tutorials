---
category: general
date: 2026-03-27
description: Δημιουργήστε στοιχείο span σε C# και μάθετε πώς να προσθέσετε span σε
  μια σελίδα κατά τη μετατροπή DOCX σε PDF και αποθήκευση ως PDF. Οδηγός βήμα‑βήμα
  για προγραμματιστές.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: el
og_description: Δημιουργήστε στοιχείο span σε C# και μάθετε πώς να προσθέσετε span
  σε μια σελίδα κατά τη μετατροπή DOCX σε PDF, στη συνέχεια αποθηκεύστε το ως PDF.
  Περιλαμβάνεται πλήρες παράδειγμα κώδικα.
og_title: Δημιουργήστε στοιχείο span και προσθέστε το στη σελίδα – Μετατροπή DOCX
  σε PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Δημιουργία στοιχείου span και προσθήκη στη σελίδα – Μετατροπή DOCX σε PDF
url: /el/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία στοιχείου span και προσθήκη στη σελίδα – Μετατροπή DOCX σε PDF

Η δημιουργία **στοιχείου span** σε αρχείο DOCX είναι μια συνηθισμένη εργασία όταν χρειάζεστε ακριβή έλεγχο διάταξης. Σε αυτό το tutorial θα σας δείξουμε **πώς να προσθέσετε span** σε μια σελίδα, **να μετατρέψετε DOCX σε PDF**, και **να αποθηκεύσετε ως PDF**—όλα σε λίγα καθαρά βήματα.  

Αν έχετε ποτέ κοίταξει ένα έγγραφο Word και σκεφτείτε, “Εύχομαι να μπορούσα να τοποθετήσω ένα μικρό πλαίσιο κειμένου σε ακριβή συντεταγμένη,” βρίσκεστε στο σωστό μέρος. Θα περάσουμε από όλη τη ροή εργασίας, από τη φόρτωση του αρχικού αρχείου μέχρι την παραγωγή ενός γυαλιστερού PDF.

## Τι θα πετύχετε

Στο τέλος αυτού του οδηγού θα μπορείτε:

* Να φορτώσετε ένα αρχείο `.docx` χρησιμοποιώντας την κλάση `Document` της βιβλιοθήκης εγγράφων.  
* **Να δημιουργήσετε στοιχείο span** με το API `TaggedContent`.  
* Να τοποθετήσετε αυτό το span σε ακριβείς συντεταγμένες X/Y σε μια επιλεγμένη σελίδα.  
* **Να προσθέσετε το στοιχείο στη σελίδα** αξιόπιστα, ακόμη και όταν η σελίδα δεν είναι η πρώτη.  
* **Να μετατρέψετε DOCX σε PDF** και **να αποθηκεύσετε ως PDF** με μία κλήση `Save`.

Χωρίς εξωτερικά εργαλεία, χωρίς μυστικές ρυθμίσεις—απλός κώδικας C# που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο έργο σας.

## Προαπαιτούμενα

* .NET 6+ (ή οποιοδήποτε πρόσφατο .NET runtime υποστηρίζεται από τη βιβλιοθήκη σας).  
* Το SDK επεξεργασίας εγγράφων που παρέχει `Document`, `TaggedContent`, `Position`, κ.λπ.  
* Βασική κατανόηση της σύνταξης C#—αν μπορείτε να γράψετε ένα `Console.WriteLine`, είστε εντάξει.

> **Pro tip:** Κρατήστε την έκδοση του SDK ενημερωμένη· η τελευταία έκδοση (v3.2 όπως του Μαρτίου 2026) περιλαμβάνει βελτιώσεις απόδοσης για λειτουργίες σε επίπεδο σελίδας.

---

![Διάγραμμα που απεικονίζει πώς να δημιουργήσετε στοιχείο span και να το τοποθετήσετε σε μια σελίδα PDF](https://example.com/images/create-span-element.png "Διάγραμμα τοποθέτησης στοιχείου span")

## Δημιουργία στοιχείου span – Τοποθέτηση και προσθήκη στη σελίδα

Παρακάτω βρίσκεται ο πλήρης, εκτελέσιμος κώδικας που κάνει τα πάντα—from τη φόρτωση του αρχικού DOCX μέχρι τη δημιουργία του τελικού PDF. Μπορείτε να τον ενσωματώσετε σε μια εφαρμογή console, να προσαρμόσετε τις διαδρομές και να τον εκτελέσετε.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Εξήγηση βήμα‑βήμα

#### Βήμα 1 – Φόρτωση του εγγράφου DOCX  
Δημιουργούμε ένα αντικείμενο `Document` που δείχνει στο `input.docx`. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Word στη μνήμη, δίνοντάς μας πρόσβαση σε σελίδες, περιεχόμενο και μεταδεδομένα.  

#### Βήμα 2 – Δημιουργία στοιχείου span  
Η κλήση `TaggedContent.CreateSpanElement()` επιστρέφει ένα ελαφρύ ενδιάμεσο κοντέινερ. Σκεφτείτε το ως ένα μικρό, αόρατο κουτί που μπορεί να κρατήσει κείμενο, εικόνες ή άλλα ενδιάμεσα στοιχεία. Η προσθήκη κειμένου (`span.Text`) είναι προαιρετική αλλά χρήσιμη για εντοπισμό σφαλμάτων.

#### Βήμα 3 – Τοποθέτηση του span  
`new Position(50, 750)` ορίζει την πάνω‑αριστερή γωνία του span 50 pts από το αριστερό περιθώριο και 750 pts από το πάνω μέρος της σελίδας. Αυτές οι τιμές είναι απόλυτες, ώστε να μπορείτε να τοποθετήσετε το span οπουδήποτε—ιδανικό για ακριβείς διατάξεις.

#### Βήμα 4 – Προσθήκη του span στη στοχευμένη σελίδα  
`doc.Pages[1].Add(span)` ενσωματώνει το span στη δεύτερη σελίδα. Το API χρησιμοποιεί μηδενική (zero‑based) αρίθμηση, έτσι η σελίδα 0 είναι η πρώτη. Αν θέλετε να το προσθέσετε στην πρώτη σελίδα, χρησιμοποιήστε απλώς `doc.Pages[0]`.

#### Βήμα 5 – Μετατροπή DOCX σε PDF και αποθήκευση ως PDF  
Η κλήση `doc.Save("output.pdf")` κάνει δύο πράγματα: γράφει το τροποποιημένο έγγραφο στο δίσκο **και** μετατρέπει το περιεχόμενο σε PDF λόγω της επέκτασης `.pdf`. Δεν απαιτείται επιπλέον βήμα μετατροπής—αυτή είναι η πιο εύκολη μέθοδος για **αποθήκευση ως PDF**.

---

## Πώς να προσθέσετε span σε διαφορετική σελίδα (προχωρημένο)

Μερικές φορές δεν γνωρίζετε εκ των προτέρων τον δείκτη της σελίδας. Μπορείτε να εντοπίσετε μια σελίδα με βάση τον αριθμό της (φιλικό προς τον χρήστη) ή ψάχνοντας για μια συγκεκριμένη λέξη‑κλειδί.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Γιατί είναι σημαντικό:** Σε αναφορές όπου ο αριθμός των σελίδων μεταβάλλεται, η σκληρή κωδικοποίηση `Pages[1]` μπορεί να σπάσει τη διάταξη. Αυτό το απόσπασμα δείχνει ένα ανθεκτικό μοτίβο για **πώς να προσθέσετε span** δυναμικά.

---

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Τι συμβαίνει | Διόρθωση |
|----------|--------------|----------|
| **Το span δεν είναι ορατό** | Οι συντεταγμένες είναι εκτός σελίδας ή το span έχει μηδενικό πλάτος/ύψος. | Ελέγξτε ξανά τις τιμές `Position`; χρησιμοποιήστε χάρακα στον προβολέα PDF. |
| **Λάθος δείκτης σελίδας** | Προσθέτετε στη σελίδα 0 αλλά περιμένετε να είναι στη σελίδα 2. | Θυμηθείτε ότι το API είναι zero‑based· προσθέστε 1 στον αριθμό σελίδας που βλέπετε. |
| **Η αποθήκευση αντικαθιστά το αρχικό** | `doc.Save("input.docx")` αντικαθιστά το αρχικό αρχείο. | Πάντα αποθηκεύετε σε νέο μονοπάτι (`output.pdf`) όταν κάνετε μετατροπή. |
| **Λείπει η αναφορά SDK** | Σφάλμα μεταγλώττισης στην κλάση `Document`. | Εγκαταστήστε το πακέτο NuGet: `dotnet add package DocumentProcessing.SDK`. |

---

## Επαλήθευση του αποτελέσματος

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε το κείμενο “Hello, world!” τοποθετημένο ακριβώς στο (50, 750) στη δεύτερη σελίδα. Αν το κείμενο εμφανίζεται αλλού, προσαρμόστε τις τιμές `Position` και ξανατρέξτε.  

Για αυτοματοποιημένες δοκιμές, μπορείτε να χρησιμοποιήσετε έναν αναλυτή PDF (π.χ., iTextSharp) για να ελέγξετε προγραμματιστικά τις συντεταγμένες του κειμένου.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Επόμενα βήματα

* **Στυλιζάρετε το span** – εξερευνήστε `span.Font`, `span.Color` και άλλες ιδιότητες στυλ.  
* **Προσθήκη εικόνων** – χρησιμοποιήστε `CreateImageElement()` αντί για span για γραφικά.  
* **Επεξεργασία σε παρτίδες** – κάντε βρόχο πάνω από έναν φάκελο με αρχεία DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}