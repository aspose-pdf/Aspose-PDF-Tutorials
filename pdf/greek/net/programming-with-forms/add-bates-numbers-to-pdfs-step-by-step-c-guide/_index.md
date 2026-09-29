---
category: general
date: 2026-02-12
description: Προσθέστε γρήγορα αριθμούς Bates σε αρχεία PDF. Μάθετε πώς να προσθέσετε
  πεδίο κειμένου PDF, πεδίο φόρμας PDF και αριθμούς σελίδων PDF χρησιμοποιώντας το
  Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: el
og_description: Προσθέστε αριθμούς Bates σε έγγραφα PDF με C#. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε πεδίο κειμένου PDF, πεδίο φόρμας PDF και αριθμούς σελίδων PDF
  με το Aspose.PDF.
og_title: Προσθήκη αριθμών Bates σε PDF – Πλήρες σεμινάριο C#
tags:
- PDF
- C#
- Aspose.PDF
title: Προσθήκη αριθμών Bates σε PDF – Οδηγός C# βήμα‑βήμα
url: /el/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbers σε PDFs – Πλήρης Οδηγός C# 

Έχετε ποτέ χρειαστεί να **προσθέσετε bates numbers** σε μια στοίβα νομικών PDF αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι. Σε πολλά γραφεία δικηγόρων και έργα e‑discovery, η σήμανση κάθε σελίδας με ένα μοναδικό αναγνωριστικό είναι καθημερινή εργασία, και η χειροκίνητη εκτέλεσή της είναι εφιάλτης.  

Τα καλά νέα; Με λίγες γραμμές C# και Aspose.PDF μπορείτε να αυτοματοποιήσετε όλο το έργο. Σε αυτό το σεμινάριο θα σας δείξουμε **πώς να προσθέσετε bates** numbers, θα προσθέσουμε ένα πεδίο κειμένου σε κάθε σελίδα και θα αποθηκεύσουμε ένα καθαρό, αναζητήσιμο PDF—χωρίς καν κόπο.

> **Τι θα πάρετε:** ένα πλήρως εκτελέσιμο δείγμα κώδικα, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, συμβουλές για ειδικές περιπτώσεις, και μια γρήγορη λίστα ελέγχου για την επαλήθευση του αποτελέσματός σας.  

Θα αγγίξουμε επίσης συναφή εργασίες όπως **add text field pdf**, **add form field pdf**, και **add page numbers pdf**, ώστε να έχετε ένα κουτί εργαλείων έτοιμο για οποιαδήποτε πρόκληση αυτοματοποίησης εγγράφων.

---

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)  
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)  
- Ένα έγκυρο license Aspose.PDF for .NET (η δωρεάν δοκιμή λειτουργεί για δοκιμές)  
- Ένα PDF πηγής με όνομα `source.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, απλώς κάντε παύση και εγκαταστήστε το απαραίτητο στοιχείο πριν προχωρήσετε. Τα παρακάτω βήματα υποθέτουν ότι έχετε ήδη προσθέσει το πακέτο NuGet Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Πώς να προσθέσετε bates numbers σε PDF με Aspose.PDF

Παρακάτω είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα. Φορτώνει ένα PDF, δημιουργεί ένα **text box field** σε κάθε σελίδα, γράφει έναν μορφοποιημένο Bates number και τελικά αποθηκεύει το τροποποιημένο αρχείο.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Γιατί λειτουργεί αυτό

- `Document` είναι το σημείο εισόδου· αντιπροσωπεύει ολόκληρο το αρχείο PDF.  
- `Rectangle` ορίζει πού βρίσκεται το πεδίο στη σελίδα. Οι αριθμοί είναι σε points (1 pt ≈ 1/72 in). Προσαρμόστε τις συντεταγμένες αν χρειάζεστε τον αριθμό σε διαφορετική γωνία.  
- `TextBoxField` είναι ένα *form field* που μπορεί να περιέχει οποιαδήποτε συμβολοσειρά. Αναθέτοντας `Value` προσθέτουμε ουσιαστικά **add page numbers pdf** με προσαρμοσμένο πρόθεμα.  
- `pdfDocument.Form.Add` καταχωρεί το πεδίο στο AcroForm του PDF, κάνοντάς το ορατό σε προβολείς όπως το Adobe Acrobat.  

Αν χρειαστεί ποτέ να αλλάξετε την εμφάνιση (γραμματοσειρά, χρώμα, μέγεθος) μπορείτε να τροποποιήσετε τις ιδιότητες του `TextBoxField`—δείτε την τεκμηρίωση Aspose για `DefaultAppearance` και `Border`.

---

## Προσθήκη πεδίου κειμένου σε κάθε σελίδα PDF (βήμα “add text field pdf”)

Μερικές φορές θέλετε μόνο μια ορατή ετικέτα, όχι ένα διαδραστικό πεδίο φόρμας. Σε αυτήν την περίπτωση μπορείτε να αντικαταστήσετε το `TextBoxField` με ένα `TextFragment` και να το προσθέσετε απευθείας στη συλλογή `Paragraphs` της σελίδας. Εδώ είναι μια γρήγορη εναλλακτική:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Η προσέγγιση **add text field pdf** είναι χρήσιμη όταν το τελικό έγγραφο θα είναι μόνο για ανάγνωση, ενώ η μέθοδος **add form field pdf** διατηρεί τους αριθμούς επεξεργάσιμους αργότερα.

---

## Αποθήκευση του PDF με Bates numbers (στιγμή “add page numbers pdf”)

Μετά το τέλος του βρόχου, η κλήση `pdfDocument.Save` γράφει τα πάντα στο δίσκο. Αν χρειάζεται να διατηρήσετε το αρχικό αρχείο, απλώς αλλάξτε τη διαδρομή εξόδου ή χρησιμοποιήστε τις υπερφορτώσεις του `pdfDocument.Save` για να μεταφέρετε το αποτέλεσμα απευθείας σε απάντηση σε web API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Αυτό είναι το καλό μέρος—χωρίς προσωρινά αρχεία, χωρίς επιπλέον βιβλιοθήκες, μόνο το Aspose που αναλαμβάνει το βαρέως φορτίου.

---

## Αναμενόμενο Αποτέλεσμα & Γρήγορη Επαλήθευση

Ανοίξτε το `bates.pdf` σε οποιοδήποτε πρόγραμμα προβολής PDF. Θα πρέπει να δείτε ένα μικρό κουτάκι στην κάτω‑αριστερή γωνία κάθε σελίδας που διαβάζει:

```
BATES-00001
BATES-00002
…
```

Αν ελέγξετε τις ιδιότητες του εγγράφου, θα δείτε ένα AcroForm που περιέχει πεδία με ονόματα `Bates_1`, `Bates_2`, κ.λπ. Αυτό επιβεβαιώνει ότι το βήμα **add form field pdf** ολοκληρώθηκε με επιτυχία.

---

## Συνηθισμένα Προβλήματα & Επαγγελματικές Συμβουλές

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι αριθμοί εμφανίζονται εκτός κέντρου | Οι συντεταγμένες του Rectangle είναι σχετικές με την κάτω‑αριστερή γωνία της σελίδας. | Αναστρέψτε την τιμή Y (`pageHeight - marginTop`) ή χρησιμοποιήστε `page.PageInfo.Height` για να υπολογίσετε θέση με άνω περιθώριο. |
| Τα πεδία είναι αόρατα στο Adobe Reader | Το προεπιλεγμένο περιθώριο είναι ορισμένο σε “No”. | Ορίστε `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Τα μεγάλα PDF προκαλούν πίεση μνήμης | `using` απελευθερώνει το έγγραφο μόνο μετά το τέλος του βρόχου. | Επεξεργαστείτε τις σελίδες σε τμήματα ή χρησιμοποιήστε `pdfDocument.Save` με `SaveOptions` που επιτρέπουν ροή. |
| Η άδεια δεν εφαρμόστηκε | Το Aspose εκτυπώνει υδατογράφημα στην πρώτη σελίδα. | Καταχωρίστε την άδειά σας νωρίς: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Επέκταση της Λύσης

- **Προσαρμοσμένα πρόθεμα:** Αντικαταστήστε `"BATES-"` με οποιαδήποτε συμβολοσειρά (`"DOC-"`, `"CASE-"`, …).  
- **Μήκος μηδενικού padding:** Αλλάξτε `{pageNumber:D5}` σε `{pageNumber:D3}` για τρία ψηφία.  
- **Δυναμική τοποθέτηση:** Χρησιμοποιήστε `pdfDocument.Pages[pageNumber].PageInfo.Width` για να τοποθετήσετε το πεδίο στη δεξιά πλευρά.  
- **Αριθμολόγηση υπό όρους:** Παραλείψτε κενές σελίδες ελέγχοντας `pdfDocument.Pages[pageNumber].IsBlank`.  

Όλες αυτές οι παραλλαγές διατηρούν το βασικό μοτίβο των **add bates numbers**, **add text field pdf**, και **add form field pdf** αμετάβλητο.

---

## Πλήρες Παράδειγμα Εργασίας (All‑in‑One)

Παρακάτω είναι το τελικό, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει τις παραπάνω συμβουλές. Αντιγράψτε το σε μια νέα εφαρμογή κονσόλας και πατήστε F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Τρέξτε το, ανοίξτε το αποτέλεσμα, και θα δείτε ένα επαγγελματικό αναγνωριστικό σε κάθε σελίδα—ακριβώς αυτό που θα περιμένατε από έναν ειδικό υποστήριξης διαδίκων.

---

## Συμπέρασμα

Μόλις δείξαμε **πώς να προσθέσετε bates numbers** σε οποιοδήποτε PDF χρησιμοποιώντας C# και Aspose.PDF. Δημιουργώντας ένα **text box field** σε κάθε σελίδα προσθέτουμε ταυτόχρονα **add text field pdf**, **add form field pdf**, και **add page numbers pdf** σε μία μόνο διεργασία. Η προσέγγιση είναι γρήγορη, κλιμακώσιμη και εύκολη στην προσαρμογή για προσαρμοσμένα πρόθεμα, διαφορετικές διατάξεις ή λογική υπό όρους.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να ενσωματώσετε έναν κώδικα QR που συνδέεται με το αρχικό αρχείο της υπόθεσης, ή δημιουργήστε μια ξεχωριστή σελίδα ευρετηρίου που καταγράφει όλους τους Bates numbers με τους αντίστοιχους τίτλους σελίδων. Το ίδιο API σας επιτρέπει να συγχωνεύετε PDF, να εξάγετε σελίδες και ακόμη να αφαιρείτε ευαίσθητα δεδομένα—οπότε το όριο είναι το ουρανό.

Αν αντιμετωπίσετε πρόβλημα, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση του Aspose για πιο λεπτομερείς πληροφορίες. Καλή προγραμματιστική, και εύχομαι τα PDF σας να παραμένουν πάντα τέλεια αριθμημένα!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}