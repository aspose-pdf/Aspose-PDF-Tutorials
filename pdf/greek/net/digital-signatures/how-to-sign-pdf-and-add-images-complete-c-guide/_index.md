---
category: general
date: 2026-03-29
description: Πώς να υπογράψετε PDF με ψηφιακή υπογραφή και να προσθέσετε μια περικομμένη
  εικόνα σε C#. Μάθετε πώς να προσθέτετε ψηφιακή υπογραφή σε PDF, να περικόπτετε εικόνα
  για PDF και να προσθέτετε εικόνα σε PDF εύκολα.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: el
og_description: Πώς να υπογράψετε PDF με ψηφιακή υπογραφή και να ενσωματώσετε μια
  περικομμένη εικόνα χρησιμοποιώντας το Aspose.Pdf σε C#. Ακολουθήστε αυτόν τον οδηγό
  για μια πλήρη λύση.
og_title: Πώς να υπογράψετε PDF και να προσθέσετε εικόνες – Βήμα‑βήμα οδηγός C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Πώς να υπογράψετε PDF και να προσθέσετε εικόνες – Πλήρης οδηγός C#
url: /el/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Υπογράψετε PDF και να Προσθέσετε Εικόνες – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να υπογράψετε PDF** αρχεία προγραμματιστικά ενώ ταυτόχρονα ενσωματώνετε μια προσαρμοσμένη εικόνα; Ίσως χτίζετε μια ροή έγκρισης και χρειάζεστε μια νομικά δεσμευτική υπογραφή *και* μια μικρογραφία της φωτογραφίας του υπογράφοντα στην ίδια σελίδα. Συνοπτικά, θέλετε **να προσθέσετε ψηφιακή υπογραφή pdf** στο περιεχόμενο, να περικόψετε αυτήν τη φωτογραφία και στη συνέχεια **να προσθέσετε εικόνα στο pdf** χωρίς κόπο.  

Αυτό το tutorial σας οδηγεί βήμα‑βήμα—από τη φόρτωση ενός πιστοποιητικού ECDSA PKCS#7 μέχρι το κόψιμο ενός JPEG και την τοποθέτησή του στην υπογεγραμμένη σελίδα. Στο τέλος θα έχετε ένα ενιαίο, εκτελέσιμο αρχείο C# που υπογράφει τη σελίδα 1, περικόπτει μια φωτογραφία σε 400 × 400 px και την τοποθετεί σε ακριβή θέση. Χωρίς εξωτερικά scripts, χωρίς μαγεία, μόνο καθαρός κώδικας και εξηγήσεις.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
- Πακέτο NuGet **Aspose.Pdf for .NET** (έκδοση 23.9 ή νεότερη)
- Πιστοποιητικό ECDSA P‑256 σε μορφή PKCS#7 (`.pfx`) και ο κωδικός του
- Μια εικόνα JPEG που θέλετε να ενσωματώσετε (π.χ. `photo.jpg`)

> **Pro tip:** Κρατήστε το αρχείο πιστοποιητικού εκτός ελέγχου έκδοσης και προστατέψτε τον κωδικό με έναν διαχειριστή μυστικών.

---

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγών

Πρώτα, δημιουργήστε μια εφαρμογή console (ή ενσωματώστε το σε υπάρχουσα υπηρεσία). Προσθέστε την αναφορά Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Στη συνέχεια, συμπεριλάβετε τα απαιτούμενα namespaces:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Αυτές οι δηλώσεις `using` σας δίνουν πρόσβαση στις κλάσεις `Document`, `Signature` και `Rectangle` που θα χρειαστούμε αργότερα.

## Βήμα 2: Φόρτωση του PDF και Προετοιμασία της Υπογραφής

Θα ανοίξουμε ένα υπάρχον PDF (`source.pdf`) και θα δημιουργήσουμε ένα αντικείμενο **digital signature pdf** που χρησιμοποιεί μια αποσπασμένη υπογραφή PKCS#7. Το πιστοποιητικό είναι κλειδί ECDSA P‑256, το οποίο είναι ευρέως αποδεκτό για συμμόρφωση.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Γιατί είναι σημαντικό:** Η χρήση αποσπασμένης υπογραφής PKCS#7 διατηρεί το αρχικό περιεχόμενο του PDF αμετάβλητο ενώ ενσωματώνει ένα κρυπτογραφικό hash. Αυτή είναι η βιομηχανική προδιαγραφή για νομικά δεσμευτικά PDFs.

## Βήμα 3: Εφαρμογή της Ψηφιακής Υπογραφής σε Συγκεκριμένη Σελίδα

Τώρα θα τοποθετήσουμε το ορατό πεδίο υπογραφής στη **σελίδα 1**. Το rectangle ορίζει πού εμφανίζεται το κουτί υπογραφής (συντεταγμένες σε points, όπου 1 inch = 72 points).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Αν δεν χρειάζεστε ορατό κουτί, ορίστε `isVisible` σε `false`. Το `signatureRect` μπορεί να προσαρμοστεί ώστε να ταιριάζει στη διάταξη του εγγράφου σας.

## Βήμα 4: Άνοιγμα του Ροής Εικόνας και Ορισμός Περιοχών Κοπής

Θα διαβάσουμε το αρχείο JPEG σε stream και θα ορίσουμε ένα **source rectangle** που επιλέγει τα πάνω‑αριστερά 400 × 400 pixel. Αυτή είναι η λειτουργία **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** Αν η εικόνα σας είναι μικρότερη από 400 × 400, η κοπή θα περιοριστεί αυτόματα στις πραγματικές διαστάσεις της εικόνας—δεν θα προκληθεί εξαίρεση.

## Βήμα 5: Ορισμός του Προορισμού για την Περικομμένη Εικόνα

Στη συνέχεια, ορίστε το **destination rectangle** στη σελίδα PDF. Στο παράδειγμα τοποθετούμε την εικόνα στο (50, 50) με μέγεθος 200 × 200 points (≈2,78 ίντσες τετράγωνο).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Αισθανθείτε ελεύθεροι να πειραματιστείτε: αλλάξτε τις συντεταγμένες X/Y για να μετακινήσετε τη φωτογραφία ή προσαρμόστε το πλάτος/ύψος για κλιμάκωση.

## Βήμα 6: Εισαγωγή της Περικομμένης Εικόνας στην Υπογεγραμμένη Σελίδα

Τέλος, προσθέτουμε την εικόνα στη **σελίδα 1** (την ίδια σελίδα που τώρα περιέχει την υπογραφή). Η υπερφόρτωση `AddImage` που χρησιμοποιούμε δέχεται τα source και destination rectangles, εκτελώντας ουσιαστικά την κοπή και την τοποθέτηση με μία κλήση.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Στο παρασκήνιο, το Aspose.Pdf εξάγει την περιοχή 400 × 400 pixel, την κλιμακώνει σε 200 × 200 points και την γράφει στο content stream του PDF.

## Βήμα 7: Αποθήκευση του Υπογεγραμμένου και Εμπλουτισμένου με Εικόνα PDF

Μετά από όλες τις τροποποιήσεις, αποθηκεύστε το έγγραφο. Μπορείτε να αντικαταστήσετε το αρχικό ή να γράψετε σε νέο αρχείο.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Όταν ανοίξετε το `output_signed.pdf` σε Adobe Acrobat ή οποιονδήποτε PDF viewer, θα δείτε:

- Ένα ορατό πεδίο υπογραφής στις συντεταγμένες που καθορίσατε.
- Τη περικομμένη φωτογραφία τοποθετημένη στο (50, 50) στη σελίδα 1.
- Την ψηφιακή υπογραφή επαληθευμένη (εφόσον ο viewer εμπιστεύεται το πιστοποιητικό σας).

---

## Συχνές Ερωτήσεις (FAQ)

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να υπογράψω διαφορετική σελίδα;** | Αλλάξτε το όρισμα `pageNumber` στην `signature.Sign` σε οποιονδήποτε έγκυρο αριθμό σελίδας (αριθμός‑βάση‑1). |
| **Τι γίνεται αν χρειάζομαι πολλαπλές υπογραφές;** | Δημιουργήστε ένα νέο αντικείμενο `Signature` για κάθε σελίδα ή θέση, επαναχρησιμοποιώντας το ίδιο `pkcsSignature` αν ισχύει το ίδιο πιστοποιητικό. |
| **Η κοπή εικόνας περιορίζεται σε ορθογώνια;** | Ναι, το `AddImage` του Aspose.Pdf λειτουργεί με ορθογώνιες περιοχές. Για πιο σύνθετα σχήματα χρειάζεται προεπεξεργασία της εικόνας (π.χ. με System.Drawing) πριν την ενσωμάτωση. |
| **Πώς κάνω την υπογραφή αόρατη;** | Ορίστε `isVisible` σε `false` και παραλείψτε το `signatureRect`. Η υπογραφή θα παραμείνει κρυπτογραφικά έγκυρη. |
| **Τι μορφές μπορώ να ενσωματώσω εκτός JPEG;** | Υποστηρίζονται PNG, BMP, GIF και TIFF. Απλώς αλλάξτε τη διαδρομή αρχείου και βεβαιωθείτε ότι το stream διαβάζει τα σωστά bytes. |

---

## Πλήρες Παράδειγμα Εφαρμογής

Ακολουθεί το ολοκληρωμένο, αυτόνομο πρόγραμμα. Αντιγράψτε‑και‑επικολλήστε το στο `Program.cs`, προσαρμόστε τις διαδρομές και τρέξτε.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Το άνοιγμα του `output_signed.pdf` εμφανίζει ένα πεδίο υπογραφής (100 × 100 → 300 × 300 points) και μια εικόνα 200 × 200‑point προερχόμενη από την πάνω‑αριστερή γωνία του `photo.jpg`. Η υπογραφή επαληθεύεται με το παρεχόμενο πιστοποιητικό ECDSA.

---

## Συμπεράσματα

Καλύψαμε **πώς να υπογράψετε PDF** αρχεία, πώς να **προσθέσετε digital signature pdf** σε συγκεκριμένη σελίδα, πώς να **crop image for pdf**, και τελικά πώς να **add image to pdf** χρησιμοποιώντας το Aspose.Pdf σε C#. Η πλήρης ροή—από τη φόρτωση του πιστοποιητικού μέχρι την αποθήκευση του τελικού εγγράφου—συμπεριλαμβάνεται σε ένα μόνο, εύκολο στην ανάγνωση αρχείο πηγαίου κώδικα.

Αν είστε έτοιμοι για την επόμενη πρόκληση, σκεφτείτε:

- Προσθήκη **πολλαπλών υπογραφών** σε διαφορετικές σελίδες (χρησιμοποιήστε την έννοια “digital signature pdf page”).
- Ενσωμάτωση **QR codes** που συνδέουν σε υπηρεσίες επαλήθευσης.
- Αυτοματοποίηση της διαδικασίας σε ASP.NET Core API για δημιουργία PDF «on‑the‑fly».

Θυμηθείτε, το κλειδί για αξιόπιστη αυτοματοποίηση PDF είναι η σαφής διαχωριστική λογική: διαχείριση υπογραφής, επεξεργασία εικόνας και τελική συναρμολόγηση εγγράφου. Παίξτε με τις συντεταγμένες, αλλάξτε τη μορφή εικόνας ή δοκιμάστε χρονική σήμανση—η ροή εργασίας σας είναι πλέον πλήρως επεκτάσιμη.

Έχετε ερωτήσεις, σενάρια άκρων ή ενδιαφέρουσες χρήσεις να μοιραστείτε; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική διασκέδαση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}