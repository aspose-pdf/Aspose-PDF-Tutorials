---
category: general
date: 2026-04-06
description: Προσθέστε γρήγορα ορθογώνιο σε PDF χρησιμοποιώντας C#. Μάθετε να σχεδιάζετε
  ορθογώνιο σε PDF, να φορτώνετε έγγραφο PDF με C# και να χρησιμοποιείτε το Aspose
  PDF για να σχεδιάσετε ορθογώνιο σε αυτό το βήμα‑βήμα tutorial.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- draw shape in pdf
- load pdf document c#
- aspose pdf draw rectangle
language: el
og_description: Προσθέστε ορθογώνιο στο PDF άμεσα. Αυτός ο οδηγός δείχνει πώς να σχεδιάσετε
  ορθογώνιο σε PDF, να φορτώσετε έγγραφο PDF με C# και να χρησιμοποιήσετε το Aspose
  PDF για σχεδίαση ορθογωνίου με σαφή παραδείγματα κώδικα.
og_title: Προσθήκη ορθογωνίου σε PDF με C# – Πλήρης οδηγός Aspose PDF
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Προσθήκη ορθογωνίου σε PDF με C# – Πλήρης οδηγός Aspose PDF
url: /el/net/images-graphics/add-rectangle-to-pdf-with-c-full-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Ορθογωνίου σε PDF – Πλήρης Οδηγός Aspose PDF

Κάποτε χρειάστηκε να **προσθέσετε ορθογώνιο σε PDF** αλλά δεν ήξερες ποια κλήση API κάνει τη δουλειά; Δεν είσαι μόνος· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αυτοματοποιούν αναφορές ή επισημαίνουν τμήματα σε ένα έγγραφο. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για **σχεδίαση ορθογωνίου σε PDF** χρησιμοποιώντας το Aspose.PDF για .NET, και θα δεις ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείς να ενσωματώσεις στο δικό σου έργο.

Θα καλύψουμε επίσης πώς να **φορτώσετε έγγραφο PDF C#**, να επαληθεύσετε ότι το σχήμα χωράει στη σελίδα, και θα συζητήσουμε μερικά κοινά προβλήματα όταν προσπαθείτε να **σχεδιάσετε σχήμα σε PDF**. Στο τέλος θα έχετε ένα πρόγραμμα που προσθέτει ένα φωτεινό κίτρινο ορθογώνιο στην πρώτη σελίδα οποιουδήποτε PDF επιλέγετε.

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Πακέτο NuGet Aspose.PDF για .NET (έκδοση 23.11 ή νεότερη)
- Ένα δείγμα αρχείου PDF (`input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε
- Visual Studio, VS Code ή οποιοδήποτε IDE C# προτιμάτε

Χωρίς επιπλέον αρχεία ρυθμίσεων, χωρίς COM interop, μόνο λίγες δηλώσεις `using` και μερικές γραμμές λογικής.

## Βήμα 1: Φόρτωση Εγγράφου PDF C# – Προετοιμασία του Αρχείου

Το πρώτο που πρέπει να κάνετε είναι να ανοίξετε το υπάρχον PDF ώστε να έχετε κάτι πάνω στο οποίο να σχεδιάσετε. Το Aspose.PDF το κάνει με μία μόνο γραμμή κώδικα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Step 1: Load the PDF document
var inputPath = @"C:\MyPdfs\input.pdf";
using var pdfDocument = new Document(inputPath);
```

**Γιατί είναι σημαντικό:**  
`Document` αντιπροσωπεύει ολόκληρο το αρχείο PDF. Με το να το τυλίξετε σε μπλοκ `using` διασφαλίζετε ότι το χειριστήριο αρχείου απελευθερώνεται αμέσως μετά τη χρήση, αποτρέποντας προβλήματα κλειδώματος αρχείου στα Windows. Αν παραλείψετε το `using`, μπορεί να εμφανιστεί το σφάλμα “cannot access the file because it is being used by another process” όταν προσπαθήσετε να αποθηκεύσετε.

## Βήμα 2: Πρόσβαση στη Σελίδα-Στόχο και Επαλήθευση Ορίων – Σχεδίαση Σχήματος σε PDF με Ασφάλεια

Πριν τοποθετήσετε ένα ορθογώνιο στη σελίδα, χρειάζεστε το αντικείμενο σελίδας και πρέπει να επιβεβαιώσετε ότι το ορθογώνιο χωράει στις διαστάσεις της σελίδας. Αυτό αποτρέπει εξαιρέσεις χρόνου εκτέλεσης και κρατά το PDF σας τακτοποιημένο.

```csharp
// Step 2: Get the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define rectangle bounds: lower‑left X/Y and upper‑right X/Y
var rectangleBounds = new Rectangle(50, 700, 200, 800);

// Verify the rectangle is inside the page limits
bool fits = rectangleBounds.LLX >= 0 &&
            rectangleBounds.URX <= firstPage.PageInfo.Width &&
            rectangleBounds.LLY >= 0 &&
            rectangleBounds.URY <= firstPage.PageInfo.Height;

if (!fits)
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

**Εξήγηση:**  
Ο κατασκευαστής `Rectangle` περιμένει τέσσερις αριθμούς: X αριστερά‑κάτω, Y αριστερά‑κάτω, X δεξιά‑πάνω, Y δεξιά‑πάνω. Οι τιμές μετρώνται σε points (1 pt ≈ 1/72 in). Το βήμα επαλήθευσης είναι ένα μικρό δίχτυ ασφαλείας—ιδιαίτερα χρήσιμο όταν υπολογίζετε τις συντεταγμένες δυναμικά (π.χ. βάσει μεγέθους εικόνας ή μήκους κειμένου).

## Βήμα 3: Προσθήκη Ορθογωνίου σε PDF – Ο Πυρήνας του “Add Rectangle to PDF”

Τώρα το διασκεδαστικό μέρος: η πραγματική εισαγωγή του σχήματος. Το Aspose.PDF παρέχει την κλάση `RectangleShape` που μπορείτε να προσθέσετε στη συλλογή `Paragraphs` της σελίδας.

```csharp
// Step 3: Add a yellow rectangle shape
var rectangleShape = new RectangleShape(rectangleBounds)
{
    FillColor = Color.Yellow,
    Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black) // Optional: thin black border
};

firstPage.Paragraphs.Add(rectangleShape);
```

**Γιατί να χρησιμοποιήσετε το `RectangleShape`;**  
Είναι γραφικό vector, επομένως το ορθογώνιο κλιμακώνεται καθαρά σε οποιαδήποτε συσκευή. Η προσθήκη του στα `Paragraphs` σημαίνει ότι συμπεριφέρεται όπως οποιοδήποτε άλλο στοιχείο περιεχομένου—τοποθετείται σχετικά με τη σελίδα, όχι με το υπάρχον κείμενο. Αν χρειάζεστε διαφανή γέμιση, απλώς ορίστε `FillColor = Color.Transparent`.

> **Συμβουλή:** Αλλάξτε το `FillColor` σε `Color.FromArgb(128, 255, 255, 0)` για ένα ημιδιαφανές κίτρινο που αφήνει το κείμενο κάτω του να φαίνεται.

## Βήμα 4: Αποθήκευση του Ενημερωμένου PDF – Ολοκλήρωση του Κύκλου “Add Rectangle to PDF”

Μόλις το σχήμα είναι στη θέση του, αποθηκεύετε απλώς το έγγραφο σε νέο αρχείο (ή αντικαθιστάτε το αρχικό, αν προτιμάτε).

```csharp
// Step 4: Save the updated PDF
var outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

Και αυτό είναι! Ανοίξτε το `output.pdf` και θα δείτε ένα φωτεινό κίτρινο ορθογώνιο τοποθετημένο ακριβώς στις συντεταγμένες που καθορίσατε.

## Πλήρες Παράδειγμα Εργασίας – Όλα τα Βήματα σε Ένα Αρχείο

Παρακάτω βρίσκεται το πλήρες, αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε όπως είναι. Περιλαμβάνει διαχείριση σφαλμάτων και σχόλια που εξηγούν κάθε γραμμή.

```csharp
// ---------------------------------------------------------------
// AddRectangleToPdf.cs
// Demonstrates how to add rectangle to PDF using Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddRectangleToPdf
{
    static void Main()
    {
        // ----- 1. Load the PDF document -----
        string inputPath = @"C:\MyPdfs\input.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        using var pdfDoc = new Document(inputPath);

        // ----- 2. Access first page and define rectangle bounds -----
        Page page = pdfDoc.Pages[1];
        var rect = new Rectangle(50, 700, 200, 800);

        // Verify rectangle fits the page
        bool fits = rect.LLX >= 0 && rect.URX <= page.PageInfo.Width &&
                    rect.LLY >= 0 && rect.URY <= page.PageInfo.Height;
        if (!fits)
        {
            Console.WriteLine("Rectangle exceeds page dimensions. Adjust coordinates.");
            return;
        }

        // ----- 3. Create and add rectangle shape -----
        var shape = new RectangleShape(rect)
        {
            FillColor = Color.Yellow,
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black)
        };
        page.Paragraphs.Add(shape);

        // ----- 4. Save the modified PDF -----
        string outputPath = @"C:\MyPdfs\output.pdf";
        pdfDoc.Save(outputPath);
        Console.WriteLine($"Rectangle added successfully. Saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Όταν ανοίξετε το `output.pdf`, η πρώτη σελίδα θα εμφανίζει ένα κίτρινο ορθογώνιο του οποίου η κάτω‑αριστερή γωνία ξεκινά στο (50 pt, 700 pt) και η πάνω‑δεξιά γωνία λήγει στο (200 pt, 800 pt). Το ορθογώνιο θα έχει λεπτό μαύρο περίγραμμα, καθιστώντας το σαφώς ορατό ενάντια στα περισσότερα υπόβαθρα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να σχεδιάσω το ορθογώνιο σε διαφορετική σελίδα;

Απλώς αλλάξτε το `pdfDoc.Pages[1]` στον επιθυμητό αριθμό σελίδας (`pdfDoc.Pages[3]` για την τρίτη σελίδα). Θυμηθείτε ότι το Aspose χρησιμοποιεί αρίθμηση που ξεκινά από 1, όχι από 0.

### Μπορώ να σχεδιάσω πολλά ορθογώνια σε βρόχο;

Απολύτως. Τυλίξτε τη λογική δημιουργίας ορθογωνίου σε ένα `foreach` πάνω σε μια συλλογή συντεταγμένων. Να προσέχετε όμως την απόδοση· η προσθήκη χιλιάδων σχημάτων μπορεί να αυξήσει σημαντικά το μέγεθος του αρχείου.

### Πώς διαφέρει αυτό από τη χρήση `Graphics` ή `System.Drawing`;

Το `System.Drawing` δουλεύει με raster εικόνες· η έξοδος ενσωματώνεται σε bitmap, η οποία μπορεί να γίνει θολή όταν μεγεθύνεται. Το `RectangleShape` είναι βασισμένο σε vector, πράγμα που σημαίνει ότι παραμένει καθαρό σε οποιοδήποτε επίπεδο ζουμ—ιδανικό για επαγγελματικά PDF.

### Τι γίνεται αν το PDF είναι προστατευμένο με κωδικό;

Φορτώστε το έγγραφο με ένα αντικείμενο `PdfLoadOptions` που περιλαμβάνει τον κωδικό:

```csharp
var loadOpts = new PdfLoadOptions { Password = "mySecret" };
using var pdfDoc = new Document(inputPath, loadOpts);
```

Στη συνέχεια προχωρήστε κανονικά. Το ορθογώνιο θα προστεθεί μόλις το έγγραφο αποκρυπτογραφηθεί στη μνήμη.

## Οπτική Αναφορά

![Add rectangle to PDF example showing yellow shape on first page](/images/add-rectangle-to-pdf-example.png)

*Alt text: “add rectangle to pdf example with yellow rectangle on first page”*

Το στιγμιότυπο δείχνει ακριβώς το αποτέλεσμα που παράγει ο παραπάνω κώδικας—μια σαφής οπτική ένδειξη ότι το ορθογώνιο τοποθετήθηκε σωστά.

## Περίληψη & Επόμενα Βήματα

Μόλις καλύψαμε πώς να **προσθέσετε ορθογώνιο σε PDF** χρησιμοποιώντας το Aspose.PDF για .NET, από τη φόρτωση του εγγράφου μέχρι την αποθήκευση του τροποποιημένου αρχείου. Τα βασικά σημεία:

1. Φορτώστε το PDF (`load pdf document c#`) με σωστή διαχείριση πόρων.
2. Ορίστε τα όρια του ορθογωνίου και βεβαιωθείτε ότι ταιριάζουν στη σελίδα.
3. Χρησιμοποιήστε το `RectangleShape` για **σχεδίαση ορθογωνίου σε pdf** (ή οποιοδήποτε άλλο **draw shape in pdf** χρειάζεστε).
4. Αποθηκεύστε το αποτέλεσμα και απολαύστε ένα οξύ, vector ορθογώνιο.

Έτοιμοι για περισσότερα; Δοκιμάστε να αντικαταστήσετε το `RectangleShape` με `EllipseShape` ή `PolygonShape` για να δημιουργήσετε προσαρμοσμένες επισημάνσεις. Ή εξερευνήστε τις δυνατότητες εξαγωγής κειμένου του Aspose για να τοποθετείτε σχήματα δυναμικά βάσει θέσεων λέξεων-κλειδιών. Η βιβλιοθήκη είναι τόσο πλούσια που σας επιτρέπει να δημιουργήσετε πλήρη εργαλεία σχολιασμού χωρίς ποτέ να φύγετε από το C#.

Αν αντιμετωπίσατε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω—χάρηκα να βοηθήσω. Και μην ξεχάσετε να δώσετε αστέρι στο πακέτο NuGet Aspose.PDF αν το βρήκατε χρήσιμο. Καλός κώδικας!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}