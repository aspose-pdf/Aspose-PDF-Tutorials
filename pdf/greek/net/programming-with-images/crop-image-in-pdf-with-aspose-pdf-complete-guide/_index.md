---
category: general
date: 2026-06-08
description: Περικοπή εικόνας σε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Μάθετε πώς
  να δημιουργήσετε PDF με εικόνα, να αποθηκεύσετε PDF με εικόνα και να προσθέσετε
  εικόνα σε PDF με λίγες μόνο γραμμές.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: el
og_description: Κόψτε εικόνα σε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Αυτό το σεμινάριο
  δείχνει πώς να δημιουργήσετε PDF με εικόνα, να αποθηκεύσετε PDF με εικόνα και να
  προσθέσετε εικόνα σε PDF γρήγορα.
og_title: Περικοπή εικόνας σε PDF με το Aspose.PDF – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Περικοπή εικόνας σε PDF με το Aspose.PDF – Πλήρης οδηγός
url: /el/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Κόψιμο εικόνας σε PDF με Aspose.PDF – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ πώς να **crop image in PDF** χωρίς να βγείτε από έναν επεξεργαστή γραφικών; Δεν είστε μόνος/μόνη. Σε πολλές αναφορές, τιμολόγια ή e‑books χρειάζεστε μόνο ένα κομμάτι μιας εικόνας — ίσως τη γωνία του λογότυπου ή ένα τμήμα διαγράμματος — και θέλετε να το έχετε απευθείας μέσα στο PDF.  

Αυτός ο οδηγός σας δείχνει ακριβώς αυτό: θα **create PDF with image**, **add image to PDF**, και στη συνέχεια **crop image in PDF** χρησιμοποιώντας τη βιβλιοθήκη Aspose.PDF για C#. Στο τέλος θα γνωρίζετε επίσης πώς να **save PDF with image** ώστε να μπορείτε να στέλνετε το αρχείο σε οποιονδήποτε.

---

## Τι Θα Χρειαστεί

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)  
- Μια αδειοδοτημένη ή δοκιμαστική έκδοση του **Aspose.PDF for .NET** (εγκατάσταση μέσω NuGet `Install-Package Aspose.PDF`)  
- Ένα αρχείο εικόνας (JPEG/PNG) στο δίσκο – θα το ονομάσουμε `image.jpg`  
- Οποιοδήποτε IDE προτιμάτε (Visual Studio, Rider, VS Code)

Αυτό είναι όλο. Χωρίς επιπλέον υπηρεσίες, χωρίς εξωτερικά εργαλεία.

---

## Βήμα 1: Ρύθμιση του Έργου και των Εισαγωγών

Πρώτα, δημιουργήστε μια εφαρμογή κονσόλας και εισάγετε τα namespaces που θα χρησιμοποιήσουμε. Οι δηλώσεις `using` διατηρούν τον κώδικα καθαρό και κάνουν τα επόμενα βήματα πιο ευανάγνωστα.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε “Aspose.PDF” και εγκαταστήστε. Η βιβλιοθήκη διαχειρίζεται εσωτερικά τόσο την τοποθέτηση εικόνας όσο και το κόψιμο, οπότε δεν θα χρειαστείτε εξωτερικές βιβλιοθήκες εικόνας.

---

## Βήμα 2: Δημιουργία PDF με Εικόνα

Τώρα δημιουργούμε πραγματικά **create pdf with image**. Το παρακάτω απόσπασμα κώδικα δημιουργεί ένα νέο `Document`, προσθέτει μια κενή σελίδα και προετοιμάζει ένα ρεύμα εικόνας.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Η εκτέλεση αυτού του κώδικα θα σας δώσει ένα PDF με ολόκληρη την εικόνα τεντωμένη στις διαστάσεις που καθορίσατε. Είναι ένας καλός έλεγχος πριν ξεκινήσετε το κόψιμο.

---

## Βήμα 3: Πώς να Προσθέσετε Εικόνα σε PDF (και να Προετοιμαστείτε για Κόψιμο)

Αν ήδη γνωρίζετε την ακριβή περιοχή που θέλετε, μπορείτε να παραλείψετε το βήμα πλήρους μεγέθους και να μεταβείτε κατευθείαν στο τμήμα **how to add image to pdf**. Η μέθοδος `AddImage` δέχεται τρία παραμέτρους:

1. **Image stream** – τα ακατέργαστα bytes της εικόνας σας.  
2. **Placement rectangle** – η θέση στη σελίδα όπου βρίσκεται η εικόνα.  
3. **Crop rectangle** – το τμήμα της εικόνας που θέλετε πραγματικά να αποδοθεί.

Παρακάτω είναι η συμπαγής έκδοση που κάνει τόσο την τοποθέτηση **and** το κόψιμο με μία κλήση.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Η Aspose.PDF εσωτερικά αντιστοιχίζει το crop rectangle στις διαστάσεις pixel της εικόνας, και στη συνέχεια αποδίδει μόνο αυτό το τμήμα μέσα στην περιοχή `placement`. Δεν απαιτείται επιπλέον επεξεργασία bitmap, κάτι που σημαίνει ότι διατηρείτε το μέγεθος του PDF μικρό.

---

## Βήμα 4: Πώς να Κόψετε Εικόνα σε PDF – Προχωρημένες Επιλογές

Μερικές φορές το quarter‑crop δεν είναι αρκετό. Ίσως χρειάζεστε ένα προσαρμοσμένο ορθογώνιο ή θέλετε να διατηρήσετε την αναλογία διαστάσεων της εικόνας. Εδώ είναι μια πιο ευέλικτη προσέγγιση:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Edge case handling:**  
- **Null streams** – πάντα τυλίξτε το `FileStream` σε ένα μπλοκ `using`, όπως φαίνεται, για να αποφύγετε διαρροές.  
- **Large images** – αν η πηγή εικόνας είναι τεράστια, σκεφτείτε να μειώσετε το ορθογώνιο `placement`; η Aspose θα κάνει αυτόματα downsample.  
- **Transparent PNGs** – η βιβλιοθήκη σέβεται τα κανάλια άλφα, έτσι η περικομμένη περιοχή θα διατηρήσει τη διαφάνεια.

---

## Βήμα 5: Αποθήκευση PDF με Εικόνα (και Επαλήθευση)

Τέλος, κάνουμε **save pdf with image**. Η μέθοδος `Save` γράφει το έγγραφο στο δίσκο. Μπορείτε επίσης να το μεταφέρετε ως ροή σε έναν web client αν χτίζετε ένα API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Όταν ανοίξετε το `output.pdf`, θα πρέπει να δείτε μόνο το περικομμένο τμήμα του `image.jpg` τοποθετημένο ακριβώς όπου το ορίσατε. Αν η εικόνα φαίνεται τεντωμένη, προσαρμόστε το πλάτος/ύψος του ορθογωνίου `placement` ώστε να ταιριάζει με την αναλογία διαστάσεων του crop rectangle.

---

## Συχνές Ερωτήσεις & Προβλήματα

| Question | Answer |
|----------|--------|
| **Μπορώ να κόψω πολλές εικόνες στην ίδια σελίδα;** | Absolutely. Call `page.AddImage` for each image with its own placement and crop rectangles. |
| **Τι γίνεται αν η εικόνα μου είναι σε διαφορετική μορφή (π.χ., BMP);** | Η Aspose.PDF υποστηρίζει JPEG, PNG, BMP, GIF και TIFF έτοιμη προς χρήση. Απλώς αλλάξτε την επέκταση του αρχείου. |
| **Χρειάζομαι άδεια για παραγωγική χρήση;** | A trial works for up to 5 pages. For real deployments, purchase a license to remove the watermark. |
| **Πώς μπορώ να περιστρέψω την περικομμένη εικόνα;** | After adding the image, retrieve the `Image` object and set its `Rotate` property (`Rotate = RotationAngle.Rotate90`). |
| **Υπάρχει τρόπος να κόψετε χρησιμοποιώντας ποσοστά αντί για απόλυτα σημεία;** | Yes—calculate the rectangle dimensions based on `image.Width * 0.25` etc., then convert to points as shown in Step 4. |

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `output.pdf` και θα δείτε μόνο το πάνω‑αριστερό τέταρτο του `image.jpg` να αποδίδεται στην πάνω‑αριστερή γωνία της σελίδας. Αλλάξτε τις τιμές του ορθογωνίου `crop` για να πειραματιστείτε με διαφορετικά τμήματα.

---

## Συμπέρασμα

Διασχίσαμε όλη τη διαδικασία του **crop image in pdf** χρησιμοποιώντας το Aspose.PDF για C#. Ξεκινώντας από ένα νέο έγγραφο, **create pdf with image**, δείχνουμε το **how to add image to pdf**, εφαρμόζουμε ένα προσαρμοσμένο ορθογώνιο **how to crop image pdf** και τελικά **save pdf with image**.  

Τώρα μπορείτε να ενσωματώσετε ακριβώς κομμένες εικόνες σε οποιοδήποτε PDF δημιουργείτε — ιδανικό για τιμολόγια, διαφημιστικά φυλλάδια ή αυτοματοποιημένες αναφορές. Στο επόμενο βήμα, σκεφτείτε να προσθέσετε λεζάντες κειμένου (`TextFragment`) ή να σχεδιάσετε σχήματα γύρω από την περικομμένη εικόνα για να την τονίσετε περαιτέρω.  

Έχετε περισσότερα σενάρια που σας ενδιαφέρουν; Αφήστε ένα σχόλιο και καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Ορίσετε το Μέγεθος Εικόνας σε PDF Χρησιμοποιώντας Aspose.PDF για .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Πώς να Προσθέσετε Σφραγίδα Εικόνας σε PDF Χρησιμοποιώντας Aspose.PDF για .NET&#58; Ένας Πλήρης Οδηγός](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Πώς να Εξάγετε Πληροφορίες Εικόνας από PDFs Χρησιμοποιώντας Aspose.PDF για .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}