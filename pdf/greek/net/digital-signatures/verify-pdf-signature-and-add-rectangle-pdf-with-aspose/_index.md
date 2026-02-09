---
category: general
date: 2026-02-09
description: Επαλήθευση υπογραφής PDF με το Aspose.PDF σε C#. Μάθετε πώς να προσθέσετε
  ορθογώνιο στο PDF, να αποθηκεύσετε το ενημερωμένο PDF και να χρησιμοποιήσετε τις
  δυνατότητες υπογραφής του Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: el
og_description: Επαληθεύστε την υπογραφή PDF σε C# γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε γραφικά σε PDF, να αποθηκεύσετε το ενημερωμένο PDF και να χρησιμοποιήσετε
  τα APIs υπογραφής Aspose PDF.
og_title: Επαλήθευση υπογραφής PDF και προσθήκη ορθογωνίου PDF – Πλήρης Οδηγός Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Επαλήθευση υπογραφής PDF και προσθήκη ορθογωνίου PDF με το Aspose
url: /el/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# επαλήθευση υπογραφής pdf και προσθήκη ορθογωνίου pdf με Aspose

Κάποτε χρειάστηκε να **επαληθεύσετε την υπογραφή pdf** σε ένα έργο C#, αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος—οι ψηφιακές υπογραφές είναι απαραίτητες για τη συμμόρφωση, αλλά πολλοί προγραμματιστές συναντούν δυσκολίες όταν πρέπει επίσης να τροποποιήσουν το έγγραφο μετά.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **επαληθεύει την υπογραφή pdf**, προσθέτει ένα **ορθογώνιο** στην πρώτη σελίδα, ελέγχει ότι το σχήμα παραμένει εντός των ορίων της σελίδας και τελικά **αποθηκεύει το ενημερωμένο pdf**—όλα χρησιμοποιώντας το σύγχρονο Aspose.PDF API. Στο τέλος θα έχετε ένα ενιαίο, αυτόνομο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιαδήποτε λύση .NET.

## Τι θα μάθετε

- Φόρτωση υπογεγραμμένου PDF με Aspose.PDF.  
- Χρήση των κλάσεων **aspose pdf signature** για επαλήθευση κάθε υπογραφής και ανίχνευση παραβιάσεων.  
- **Προσθήκη ορθογωνίου pdf** γραφικών με ασφάλεια, διασφαλίζοντας ότι ταιριάζουν στη σελίδα.  
- **Αποθήκευση ενημερωμένου pdf** διατηρώντας τις υπάρχουσες υπογραφές.  
- Συμβουλές, διαχείριση edge‑case και κοινά λάθη.

Δεν απαιτούνται εξωτερικά έγγραφα—όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Πακέτο NuGet Aspose.PDF for .NET (≥ 23.10). Εγκατάσταση με:

```bash
dotnet add package Aspose.Pdf
```

- Ένα υπογεγραμμένο αρχείο PDF με όνομα `signed.pdf` τοποθετημένο σε φάκελο που ελέγχετε (αντικαταστήστε το `YOUR_DIRECTORY` στον κώδικα).  
- Βασική εξοικείωση με C# και Visual Studio ή VS Code.

> **Pro tip:** Αν δεν έχετε διαθέσιμο υπογεγραμμένο PDF, η Aspose παρέχει ένα δωρεάν demo αρχείο στην ιστοσελίδα της που μπορείτε να κατεβάσετε για δοκιμές.

---

## επαλήθευση υπογραφής pdf – Βήμα προς Βήμα

Το πρώτο που πρέπει να κάνουμε είναι να ανοίξουμε το έγγραφο και να περάσουμε σε βρόχο κάθε ψηφιακή υπογραφή. Το Aspose.PDF μας παρέχει δύο χρήσιμες μεθόδους: `VerifySignature` σας λέει αν η κρυπτογραφική επαλήθευση περάσει, ενώ η νεότερη `IsSignatureCompromised` σηματοδοτεί τυχόν παραβίαση που μπορεί να συνέβη μετά την υπογραφή.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Γιατί είναι σημαντικό:**  
- Η `VerifySignature` από μόνη της επιβεβαιώνει μόνο ότι το πιστοποιητικό του υπογράφοντα εξακολουθεί να είναι αξιόπιστο.  
- Η `IsSignatureCompromised` εντοπίζει λεπτές αλλαγές—όπως η προσθήκη κρυφού αντικειμένου—ώστε να ξέρετε αν το οπτικό περιεχόμενο του PDF τροποποιήθηκε μετά την υπογραφή.

**Αναμενόμενη έξοδος** (παράδειγμα με δύο υπογραφές):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Αν κάποια υπογραφή επιστρέψει `compromised=True`, θα πρέπει να διακόψετε την περαιτέρω επεξεργασία ή να ειδοποιήσετε τον χρήστη, επειδή η ακεραιότητα του εγγράφου δεν μπορεί να εγγυηθεί.

---

## προσθήκη ορθογωνίου pdf σε σελίδα

Τώρα που έχουμε επιβεβαιώσει ότι οι υπογραφές είναι αμετάβλητες (ή τουλάχιστον γνωρίζουμε τυχόν παραβιάσεις), ας προσθέσουμε ένα απλό ορθογώνιο γραφικό. Αυτό είναι χρήσιμο για σήμανση «Reviewed», επισήμανση τμημάτων ή απλώς για να τραβήξει την προσοχή σε μια περιοχή.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Τι σημαίνουν οι αριθμοί:**  
- Το σύστημα συντεταγμένων του PDF ξεκινά από την κάτω‑αριστερή γωνία.  
- Στο παράδειγμα, το ορθογώνιο καλύπτει 100 points οριζόντια και 100 points κάθετα, τοποθετημένο περίπου στο κέντρο μιας τυπικής σελίδας A4.

> **Σημείωση:** Το Aspose υποστηρίζει επίσης `AddEllipse`, `AddPolygon` κ.λπ., αν χρειάζεστε πιο σύνθετα σχήματα.

---

## έλεγχος ορίων γραφικών – διασφάλιση ότι το ορθογώνιο ταιριάζει

Πριν εφαρμόσουμε τις αλλαγές, είναι σοφό να επαληθεύσουμε ότι τα γραφικά μας παραμένουν εντός της εκτυπώσιμης περιοχής της σελίδας. Η νέα μέθοδος `CheckGraphicsBounds` κάνει ακριβώς αυτό.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Αν η `shapeFits` επιστρέψει `false`, θα πρέπει να προσαρμόσετε τις συντεταγμένες του ορθογωνίου—ίσως να το μικρύνετε ή να το μετακινήσετε πιο χαμηλά στη σελίδα. Αυτό αποτρέπει τυχαία αποκοπή που μπορεί να φαίνεται άπρεπο, ειδικά όταν το PDF εκτυπώνεται αργότερα.

---

## αποθήκευση ενημερωμένου pdf – διατήρηση υπογραφών και νέων γραφικών

Τέλος, γράφουμε το τροποποιημένο έγγραφο πίσω στο δίσκο. Η μέθοδος `Save` σέβεται τις υπάρχουσες υπογραφές· δεν θα τις ακυρώσει εκτός αν το περιεχόμενο έχει αλλάξει πραγματικά (πράγμα που ήδη ελέγξαμε με `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Γιατί να χρησιμοποιήσετε νέο αρχείο;**  
Η αντικατάσταση του αρχικού μπορεί να διαγράψει τις αρχικές υπογραφές, καθιστώντας αδύνατη τη σύγκριση πριν/μετά. Με τη δημιουργία του `output.pdf` διατηρείτε την πηγή για σκοπούς ελέγχου.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console. Όλα τα βήματα είναι συνδυασμένα, τα σχόλια εξηγούν κάθε τμήμα, και θα δείτε την αναμενόμενη έξοδο στην κονσόλα στο τέλος.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος κονσόλας** (υποθέτοντας μία έγκυρη, αμετάβλητη υπογραφή):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Αν μια υπογραφή είναι παραβιασμένη, θα δείτε `compromised=True` και μπορείτε να αποφασίσετε αν θα συνεχίσετε.

---

## Συχνές ερωτήσεις & διαχείριση edge‑case

| Ερώτηση | Απάντηση |
|----------|--------|
| **Τι γίνεται αν το PDF δεν έχει υπογραφές;** | Η `GetSignNames()` επιστρέφει κενή συλλογή· ο βρόχος απλώς παραλείπεται, και μπορείτε ακόμη να προσθέσετε γραφικά. |
| **Μπορώ να προσθέσω πολλαπλά ορθογώνια;** | Ναι—απλώς καλέστε `AddRectangle` επανειλημμένα με διαφορετικά αντικείμενα `Rectangle`. |
| **Τι γίνεται με PDF προστατευμένα με κωδικό;** | Φορτώστε τα με `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` πριν την επαλήθευση. |
| **Θα ακυρώσει η προσθήκη γραφικών μια έγκυρη υπογραφή;** | Μόνο αν η υπογραφή καλύπτει τη σελίδα όπου εισάγετε τα γραφικά. Χρησιμοποιήστε `IsSignatureCompromised` για να το εντοπίσετε· διαφορετικά η υπογραφή παραμένει αμετάβλητη. |
| **Πρέπει να κλείσω πόρους;** | Τα αντικείμενα του Aspose.PDF διαχειρίζονται αυτόματα· το `disposing` είναι προαιρετικό, αλλά μπορείτε να τυλίξετε τον κώδικα σε `using` για επιπλέον ασφάλεια. |

---

## Pro tips για παραγωγική χρήση

- **Batch processing:** Τυλίξτε όλη τη ρουτίνα σε μια μέθοδο που δέχεται διαδρομές εισόδου/εξόδου· μετά περάστε μια λίστα αρχείων σε `Parallel.ForEach` για ταχύτητα.  
- **Logging:** Αντικαταστήστε το `Console.WriteLine` με έναν πραγματικό logger (π.χ. Serilog) για καταγραφή αποτελεσμάτων επαλήθευσης σε audit trails.  
- **Signature policy:** Συνδυάστε `VerifySignature` με έλεγχο ανάκλησης πιστοποιητικού (OCSP/CRL) για αυστηρότερη συμμόρφωση.  
- **Graphics styling:** Χρησιμοποιήστε `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` για να κάνετε το ορθογώνιο πιο εμφανές.  
- **Version lock:** Καρφώστε την έκδοση του Aspose.PDF NuGet ώστε να αποφεύγετε breaking changes όταν η βιβλιοθήκη ενημερώνεται.  

---

## Συμπέρασμα

Τώρα έχετε ένα σταθερό, end‑to‑end παράδειγμα που **επαληθεύει υπογραφή pdf**, **προσθέτει ορθογώνιο pdf**, και **αποθηκεύει ενημερωμένο pdf** χρησιμοποιώντας τα τελευταία APIs του Aspose.PDF. Ο κώδικας ελέγχει για παραβιασμένες υπογραφές, διασφαλίζει ότι τα γραφικά παραμένουν εντός των ορίων της σελίδας και διατηρεί τις αρχικές ψηφιακές υπογραφές—ακριβώς ό,τι απαιτεί μια πραγματική ροή εργασίας συμμόρφωσης.

Επόμενα βήματα, μπορείτε να εξερευνήσετε:

- Προσθήκη **add graphics pdf** όπως υδατογραφήματα ή QR codes.  
- Χρήση του **aspose pdf signature** API για δημιουργία νέων υπογραφών προγραμματιστικά.  
- Αυτοματοποίηση της διαδικασίας σε μια υπηρεσία ASP.NET Core για έλεγχο εγγράφων σε πραγματικό χρόνο.

Δοκιμάστε το, τροποποιήστε τις συντεταγμένες του ορθογωνίου, και δείτε πώς η βιβλιοθήκη αντιδρά σε διαφορετικές δομές PDF. Καλή προγραμματιστική εμπειρία, και να παραμένουν τα PDFs σας τόσο υπογεγραμμένα όσο και στυλιζαρισμένα! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}