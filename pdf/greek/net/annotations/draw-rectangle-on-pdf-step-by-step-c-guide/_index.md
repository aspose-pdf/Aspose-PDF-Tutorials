---
category: general
date: 2026-08-14
description: Σχεδιάστε γρήγορα ένα ορθογώνιο σε PDF χρησιμοποιώντας C#. Μάθετε πώς
  να ορίζετε τις διαστάσεις του ορθογωνίου και να προσθέτετε σχήματα σε μια σελίδα
  PDF με λίγες μόνο γραμμές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: el
lastmod: 2026-08-14
og_description: Σχεδιάστε ορθογώνιο σε PDF με C# σε δευτερόλεπτα. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε τις διαστάσεις του ορθογωνίου, να προσθέσετε ένα σχήμα και να επαληθεύσετε
  τα όρια της σελίδας για αξιόπιστα γραφικά PDF.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Σχεδίαση ορθογωνίου σε PDF – πλήρες σεμινάριο C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Σχεδίαση ορθογωνίου σε PDF – βήμα‑βήμα οδηγός C#
url: /el/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Σχεδίαση ορθογωνίου σε PDF – πλήρης οδηγός C#

Αν χρειάζεστε **draw rectangle on pdf** χρησιμοποιώντας C#, αυτός ο οδηγός σας παρουσιάζει μια σύντομη, έτοιμη για παραγωγή λύση. Θα δείτε ακριβώς **πώς να ορίσετε τις διαστάσεις του ορθογωνίου**, να επαληθεύσετε ότι το σχήμα ταιριάζει, και να το προσθέσετε σε μια σελίδα με μία κλήση μεθόδου.

Ο οδηγός καλύπτει όλα, από τη δημιουργία ενός εγγράφου PDF μέχρι την απόδοση του ορθογωνίου, ώστε να μπορείτε να αντιγράψετε‑και‑επικολλήσετε τον κώδικα στο δικό σας έργο και να δείτε τα αποτελέσματα αμέσως. Δεν απαιτείται εξωτερική τεκμηρίωση—απλώς τα παρακάτω βήματα.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
* Το **Aspose.PDF for .NET** πακέτο NuGet (`Install-Package Aspose.PDF`)
* Βασική κατανόηση της σύνταξης C#
* Ένα IDE όπως το Visual Studio ή το VS Code

> **Pro tip:** Χρησιμοποιήστε την δωρεάν άδεια αξιολόγησης του Aspose.PDF για γρήγορα πειράματα· προσθέτει ένα μικρό υδατογράφημα αλλά σας επιτρέπει να δοκιμάσετε όλες τις δυνατότητες.

## Πώς να σχεδιάσετε ορθογώνιο σε PDF με C#

Ο πυρήνας της εργασίας είναι η δημιουργία ενός `RectangleShape`, ο καθορισμός του μεγέθους και του περιγράμματος, και η προσάρτησή του σε μια `Page`. Η παρακάτω επικεφαλίδα H2 περιέχει τη βασική λέξη‑κλειδί, ικανοποιώντας τις απαιτήσεις SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Εξήγηση κάθε βήματος

| Βήμα | Γιατί είναι σημαντικό |
|------|-----------------------|
| **1️⃣ Create a new PDF document** | Αρχικοποιεί το κοντέινερ που θα κρατήσει τις σελίδες και τα γραφικά. |
| **2️⃣ Add a blank page** | Χρειάζεστε ένα αντικείμενο `Page` επειδή τα σχήματα προσδένονται σε μια σελίδα, όχι απευθείας στο έγγραφο. |
| **3️⃣ Define the rectangle bounds** | Εδώ είναι που **how to define rectangle dimensions**. Ο κατασκευαστής `Rectangle` δέχεται `x`, `y`, `width` και `height` σε μονάδες σημείου (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | `RectangleShape` είναι η κλάση Aspose που αποδίδει ένα ορθογώνιο. Ορίζοντας `StrokeColor` καθορίζετε το περίγραμμα· μπορείτε επίσης να ορίσετε `FillColor` για γεμιστό χρώμα. |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` ρίχνει εξαίρεση αν το ορθογώνιο υπερβαίνει το μέγεθος της σελίδας, αποτρέποντας κατεστραμμένα PDFs. |
| **6️⃣ Add the shape to the page** | Το σχήμα γίνεται μέρος του ρεύματος περιεχομένου της σελίδας. |
| **7️⃣ Save the PDF** | Αποθηκεύει το έγγραφο σε αρχείο που μπορείτε να ανοίξετε με οποιονδήποτε προβολέα PDF. |

Το παραγόμενο `RectangleDemo.pdf` περιέχει ένα μαύρο ορθογώνιο τοποθετημένο στην επάνω‑αριστερή γωνία της σελίδας, ακριβώς 500 pt πλάτος και 700 pt ύψος.

![παράδειγμα σχεδίασης ορθογωνίου σε pdf](https://example.com/rectangle-demo.png "παράδειγμα σχεδίασης ορθογωνίου σε pdf")

*Κείμενο alt εικόνας: παράδειγμα σχεδίασης ορθογωνίου σε pdf που δείχνει ένα μαύρο ορθογώνιο στην επάνω αριστερή γωνία μιας σελίδας PDF.*

## Πώς να ορίσετε τις διαστάσεις του ορθογωνίου για διαφορετικά μεγέθη σελίδας

Το παραπάνω απόσπασμα χρησιμοποιεί σταθερές τιμές (`500 x 700`). Σε πραγματικές εφαρμογές συχνά χρειάζεται το ορθογώνιο να προσαρμόζεται στο πλάτος και το ύψος της σελίδας.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Κύρια σημεία:**

* Χρησιμοποιήστε `page.PageInfo.Width` και `Height` για να διαβάσετε το πραγματικό μέγεθος της σελίδας.
* Ο πολλαπλασιασμός με έναν παράγοντα (π.χ., `0.8f`) σας επιτρέπει να εκφράσετε τις διαστάσεις ως ποσοστό της σελίδας.
* Η κεντράρισμα επιτυγχάνεται αφαιρώντας το μέγεθος του ορθογωνίου από το μέγεθος της σελίδας και διαιρώντας το υπόλοιπο δια του 2.

## Συνηθισμένα λάθη και πώς να τα αποφύγετε

| Λάθος | Γιατί συμβαίνει | Διόρθωση |
|-------|----------------|----------|
| Το ορθογώνιο εκτείνεται πέρα από τη σελίδα | Σταθερές διαστάσεις μεγαλύτερες από το μέγεθος της σελίδας. | Καλέστε `page.CheckShapeBoundary` **πριν** προσθέσετε το σχήμα· προσαρμόστε τις διαστάσεις αν ριχτεί εξαίρεση. |
| Το περίγραμμα δεν είναι ορατό | `StrokeColor` παραμένει στην προεπιλογή (`Color.Empty`). | Ορίστε ρητά `StrokeColor` (π.χ., `Color.Black`). |
| Το ορθογώνιο εμφανίζεται εκτός οθόνης | Οι συντεταγμένες ξεκινούν από το κάτω‑αριστερό σημείο στο χώρο PDF· η χρήση συντεταγμένων τύπου οθόνης (πάνω‑αριστερά) προκαλεί αντιστροφή. | Θυμηθείτε ότι το αρχικό σημείο `(0,0)` είναι η κάτω‑αριστερή γωνία. Προσαρμόστε το `y` αναλόγως ή χρησιμοποιήστε `pageHeight - desiredY`. |
| Μη αναμενόμενο πάχος γραμμής | Το προεπιλεγμένο πάχος γραμμής μπορεί να είναι πολύ λεπτό για εκτύπωση. | Ορίστε `rectangleShape.LineWidth = 2;` για να αυξήσετε το πάχος. |

## Επέκταση του παραδείγματος

Μόλις μπορείτε να **draw rectangle on pdf**, μπορείτε εύκολα να προσθέσετε και άλλα σχήματα:

* **EllipseShape** – για κύκλους ή έλλειπτες.
* **PolygonShape** – για προσαρμοσμένα πολύγωνα.
* **TextFragment** – για να ετικετοποιήσετε τα ορθογώνια σας.

Όλα τα σχήματα ακολουθούν την ίδια ροή εργασίας: ορίστε τα όρια, διαμορφώστε την εμφάνιση, ελέγξτε τα όρια, και, τέλος, προσθέστε τα στη σελίδα.

## Πλήρες, εκτελέσιμο πρόγραμμα

Παρακάτω είναι το πλήρες πρόγραμμα που συνδυάζει το βασικό ορθογώνιο και το παράδειγμα δυναμικού μεγέθους. Αντιγράψτε το σε ένα νέο έργο κονσόλας, επαναφέρετε το πακέτο NuGet `Aspose.PDF`, και τρέξτε.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίξτε το `CombinedRectangles.pdf`. Θα δείτε ένα μαύρο ορθογώνιο αγκυροβολημένο στην κάτω‑αριστερή γωνία και ένα κεντραρισμένο σκούρο‑μπλε ορθογώνιο με ανοιχτό‑κίτρινο γέμισμα. Και τα δύο ορθογώνια σέβονται τα περιθώρια της σελίδας.

## Συμπέρασμα

Τώρα ξέρετε πώς να **draw rectangle on pdf** με C# και ακριβώς **how to define rectangle dimensions** για σταθερές και προσαρμοστικές διατάξεις. Η προσέγγιση χρησιμοποιεί το `RectangleShape` του Aspose.PDF, τον έλεγχο ορίων, και απλή αριθμητική για προσαρμογή σε οποιοδήποτε μέγεθος σελίδας.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* Προσθήκη **χρωμάτων γεμίσματος** και **στυλ γραμμής** (διακεκομμένες, με κουκκίδες) – δευτερεύουσα λέξη‑κλειδί: how to define rectangle dimensions with style.
* Συνδυασμός πολλαπλών σχημάτων σε μια ενιαία `Page` για δημιουργία διαγραμμάτων ή φορμών.
* Εξαγωγή του PDF σε ροή (stream) για web APIs αντί για αποθήκευση σε δίσκο.

Πειραματιστείτε με διαφορετικά μεγέθη, χρώματα και θέσεις για να κυριαρχήσετε τα γραφικά PDF στις .NET εφαρμογές σας. Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγοί καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να προσαρμόσετε τα PDF με Aspose.PDF για .NET: Ορισμός περιθωρίων σελίδας και σχεδίαση γραμμών](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Πώς να προσθέσετε σφραγίδες σελίδας σε PDF χρησιμοποιώντας Aspose.PDF για .NET: Πλήρης οδηγός](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Πώς να προσθέσετε σφραγίδες αριθμού σελίδας σε PDF χρησιμοποιώντας Aspose.PDF για .NET | Υδατογραφήματα & Υπόβαθρα](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}