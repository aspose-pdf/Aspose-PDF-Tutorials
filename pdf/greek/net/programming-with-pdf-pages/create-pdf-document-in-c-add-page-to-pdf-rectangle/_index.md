---
category: general
date: 2026-02-10
description: Δημιουργήστε έγγραφο PDF σε C# με το Aspose.Pdf. Μάθετε πώς να προσθέτετε
  σελίδα σε PDF και πώς να προσθέτετε ορθογώνιο στο PDF με ασφάλεια, χρησιμοποιώντας
  έλεγχο ορίων.
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: el
og_description: Δημιουργήστε έγγραφο PDF σε C# με το Aspose.Pdf. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε σελίδα σε PDF και πώς να προσθέσετε ορθογώνιο σε PDF ελέγχοντας
  τα όρια.
og_title: Δημιουργία εγγράφου PDF σε C# – Προσθήκη σελίδας σε PDF & ορθογώνιο
tags:
- pdf
- csharp
- aspose
title: Δημιουργία εγγράφου PDF σε C# – Προσθήκη σελίδας στο PDF & Ορθογώνιο
url: /el/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF Εγγράφου σε C# – Προσθήκη Σελίδας σε PDF & Ορθογώνιο

Ποτέ χρειάστηκε να **δημιουργήσετε pdf έγγραφο** σε C# και δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο εμπόδιο όταν πειραματίζονται για πρώτη φορά με βιβλιοθήκες δημιουργίας PDF. Το καλό νέο είναι ότι με το Aspose.Pdf μπορείς να δημιουργήσεις ένα PDF, να προσθέσεις σελίδα σε PDF και ακόμη να σχεδιάσεις σχήματα όπως ένα ορθογώνιο χωρίς καμία δυσκολία.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που όχι μόνο **δημιουργεί ένα PDF έγγραφο** αλλά επίσης δείχνει **πώς να προσθέσετε ορθογώνια PDF** αντικείμενα με ασφάλεια ενεργοποιώντας τον παγκόσμιο έλεγχο ορίων. Στο τέλος θα έχεις μια σταθερή κατανόηση του API, θα ξέρεις γιατί κάθε βήμα είναι σημαντικό και θα δεις το ακριβές αποτέλεσμα που πρέπει να περιμένεις.

## Τι Θα Χρειαστείς

- .NET 6+ (ή .NET Framework 4.6+). Ο κώδικας λειτουργεί το ίδιο και στα δύο.
- Πακέτο NuGet Aspose.Pdf for .NET (`Aspose.Pdf`) – εγκατέστησέ το με `dotnet add package Aspose.Pdf`.
- Οποιοσδήποτε επεξεργαστής C# (Visual Studio, VS Code, Rider… όπως προτιμάς).

Δεν απαιτείται καμία επιπλέον ρύθμιση· η βιβλιοθήκη περιλαμβάνει όλα όσα χρειάζεσαι για να αρχίσεις να παράγεις PDF αμέσως.

## Βήμα 1: Δημιουργία PDF Εγγράφου και Ενεργοποίηση Ελέγχου Ορίων

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `Document`. Σκέψου το ως το κενό καμβά για την περιπέτειά σου **create pdf document**. Αμέσως μετά ενεργοποιούμε μια παγκόσμια ρύθμιση που αναγκάζει τη βιβλιοθήκη να ελέγχει ότι κάθε γραφικό αντικείμενο παραμένει εντός της περιοχής της σελίδας. Αυτό είναι κρίσιμο όταν αργότερα προσπαθήσεις να σχεδιάσεις σχήματα που μπορεί να ξεπεράσουν τις άκρες.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*Γιατί να ενεργοποιήσουμε τον έλεγχο ορίων;*  
Αν τοποθετήσεις κατά λάθος ένα ορθογώνιο εκτός της σελίδας, το Aspose θα ρίξει ένα `PdfException`. Η έγκαιρη σύλληψή του σε εξοικονομεί από κατεστραμμένα PDF που ορισμένοι προβολείς αρνούνται να ανοίξουν.

## Βήμα 2: Προσθήκη Σελίδας σε PDF

Ένα PDF χωρίς σελίδες είναι σαν ένα βιβλίο χωρίς φύλλα—αχρείαστο. Η προσθήκη σελίδας είναι τόσο απλή όσο η κλήση του `Pages.Add()`. Η μέθοδος επιστρέφει ένα αντικείμενο `Page` που θα χρησιμοποιήσεις για να τοποθετήσεις περιεχόμενο.

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **Pro tip:** Το προεπιλεγμένο μέγεθος σελίδας στο Aspose είναι 595 × 842 points (A4). Αν χρειάζεσαι διαφορετικό μέγεθος, μπορείς να ορίσεις `page.PageInfo.Width` και `page.PageInfo.Height` πριν προσθέσεις περιεχόμενο.

## Βήμα 3: Ορισμός του Ορθογωνίου που Θα Βγεί Εκτός Ορίων

Τώρα φτάνουμε στον πυρήνα του **how to add rectangle pdf**. Δημιουργούμε σκόπιμα ένα ορθογώνιο που υπερβαίνει τις διαστάσεις της σελίδας για να δούμε την εξαίρεση σε δράση. Ο κατασκευαστής `Rectangle` δέχεται τέσσερα ορίσματα: *κάτω‑αριστερό X, κάτω‑αριστερό Y, πάνω‑δεξιό X, πάνω‑δεξιό Y*.

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

Αν τρέξεις τον κώδικα με τον έλεγχο ορίων απενεργοποιημένο, το ορθογώνιο θα αποκοπεί απλώς. Με τον έλεγχο ενεργό, το Aspose θα εγείρει σφάλμα, που είναι ακριβώς αυτό που θέλουμε για αξιόπιστες αλυσίδες παραγωγής PDF.

## Βήμα 4: Δημιουργία του Σχήματος και Προσθήκη Ορατού Περιγράμματος

Ένα ορθογώνιο από μόνο του είναι αόρατο εκτός αν προσθέσεις περίγραμμα ή γέμισμα. Εδώ τυλίγουμε το `Rectangle` σε ένα αντικείμενο σχήματος `Rectangle` (ναι, το όνομα της κλάσης είναι λίγο παραπλανητικό) και του αναθέτουμε ένα λεπτό μαύρο περίγραμμα.

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*Γιατί ένα περίγραμμα;*  
Χωρίς περίγραμμα δεν θα δεις τίποτα στη σελίδα, κάνοντας το debugging πιο δύσκολο. Ένα λεπτό περίγραμμα κάνει επίσης προφανές πότε το σχήμα είναι εκτός ορίων.

## Βήμα 5: Προσθήκη του Σχήματος στη Σελίδα – Αναμενόμενη Εξαίρεση

Τώρα τοποθετούμε πραγματικά το σχήμα στη σελίδα. Επειδή το ορθογώνιο υπερβαίνει τα όρια της σελίδας και έχουμε ενεργοποιήσει τον έλεγχο ορίων, το Aspose θα ρίξει ένα `PdfException`. Τυλίγουμε την κλήση σε μπλοκ `try/catch` για να δείξουμε ευγενική διαχείριση σφαλμάτων.

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

Αν σχολιάσεις τη γραμμή `CheckGraphicsObjectBoundaries` στο Βήμα 1, ο κώδικας θα ολοκληρωθεί επιτυχώς και το ορθογώνιο θα αποκοπεί στα άκρα της σελίδας. Αυτή η συμπεριφορά είναι χρήσιμη για γρήγορα πρωτότυπα, αλλά για παραγωγή συνήθως θέλεις το δίχτυ ασφαλείας.

## Βήμα 6: Αποθήκευση του PDF

Τέλος, αποθηκεύουμε το έγγραφο στο δίσκο. Το αρχείο θα δημιουργηθεί στο φάκελο που θα ορίσεις· βεβαιώσου ότι η διαδρομή υπάρχει ή χρησιμοποίησε `Path.Combine` με `Environment.CurrentDirectory`.

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Όταν ανοίξεις το `checked_shapes.pdf` θα δεις μια κενή σελίδα (επειδή το ορθογώνιο απορρίφθηκε). Αν είχες αφαιρέσει τον έλεγχο ορίων, θα έβλεπες ένα μερικώς σχεδιασμένο ορθογώνιο αποκομμένο στα δεξιά και πάνω άκρα.

---

![Δημιουργία PDF Εγγράφου παράδειγμα που δείχνει έλεγχο ορίων ορθογωνίου](https://example.com/images/checked_shapes.png "Δημιουργία PDF Εγγράφου παράδειγμα με έλεγχο ορίων ορθογωνίου")

*Το παραπάνω στιγμιότυπο δείχνει το PDF μετά την εκτέλεση του tutorial με απενεργοποιημένο έλεγχο ορίων (το ορθογώνιο αποκόπτεται). Με ενεργοποιημένο έλεγχο, το σχήμα παραλείπεται και καταγράφεται εξαίρεση.*

## Ανακεφαλαίωση: Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα πάντα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

Τρέξε το πρόγραμμα και θα δεις την έξοδο της κονσόλας που επιβεβαιώνει αν η εξαίρεση πιάστηκε. Άνοιξε το παραγόμενο PDF για να επαληθεύσεις το αποτέλεσμα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν χρειάζομαι διαφορετικό μέγεθος σελίδας;**  
  Ορίστε `page.PageInfo.Width` και `page.PageInfo.Height` πριν προσθέσετε σχήματα. Ο ελεγκτής ορίων θα χρησιμοποιήσει αυτόματα τις νέες διαστάσεις.

- **Μπορώ να απενεργοποιήσω τον έλεγχο ορίων για ένα μόνο σχήμα;**  
  Όχι άμεσα. Η ρύθμιση είναι παγκόσμια, αλλά μπορείτε προσωρινά να την απενεργοποιήσετε, να προσθέσετε το σχήμα, και μετά να την ενεργοποιήσετε ξανά—να θυμάστε ότι χάνετε το δίχτυ ασφαλείας για αυτή τη λειτουργία.

- **Είναι το μήνυμα της εξαίρεσης χρήσιμο;**  
  Ναι, το Aspose περιλαμβάνει τις εσφαλμένες συντεταγμένες, ώστε να μπορείτε προγραμματιστικά να προσαρμόσετε το ορθογώνιο ή να καταγράψετε λεπτομερή διάγνωση.

- **Θα λειτουργήσει σε .NET Core σε Linux;**  
  Απόλυτα. Το Aspose.Pdf είναι πλατφόρμα‑ανεξάρτητο· απλώς βεβαιωθείτε ότι τα αρχεία γραμματοσειρών που αναφέρετε είναι διαθέσιμα στο λειτουργικό σύστημα-στόχο.

## Επόμενα Βήματα

Τώρα που ξέρεις **πώς να προσθέσετε ορθογώνια pdf** αντικείμενα και **πώς να προσθέσετε σελίδα σε pdf**, μπορείς να εξερευνήσεις:

- Προσθήκη άλλων τύπων γραφικών (έλλειψες, γραμμές) με τους ίδιους ελέγχους ορίων.
- Εισαγωγή κειμένου, εικόνων ή πινάκων—το Aspose προσφέρει πλούσια API για καθένα.
- Χρήση των υπερφορτώσεων `Document.Save` για έξοδο απευθείας σε `MemoryStream` για web APIs.

Μην διστάσεις να πειραματιστείς με διαφορετικές συντεταγμένες ορθογωνίου, περιγράμματα και χρώματα γεμίσματος. Όσο περισσότερο παίζεις, τόσο καλύτερα θα κατανοήσεις πώς λειτουργεί το Aspose.P

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}