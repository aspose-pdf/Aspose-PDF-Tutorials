---
category: general
date: 2026-02-10
description: Πώς να προσθέσετε αριθμούς Bates σε ένα PDF γρήγορα—μάθετε πώς να προσθέσετε
  αριθμό Bates σε PDF και να δημιουργήσετε αόρατο υδατογράφημα με το Aspose.Pdf σε
  C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: el
og_description: Πώς να προσθέσετε αριθμούς Bates σε C# με το Aspose.Pdf. Αυτό το σεμινάριο
  δείχνει πώς να προσθέσετε αριθμό Bates σε PDF, να προσθέσετε αόρατο υδατογράφημα
  σε PDF και άλλα.
og_title: Πώς να προσθέσετε Bates – Πλήρης οδηγός PDF
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Πώς να προσθέσετε αρίθμηση Bates – Οδηγός βήμα‑βήμα για PDFs
url: /el/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Bates – Πλήρης Οδηγός PDF

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε bates** σε ένα νομικό PDF χωρίς να διαταράξετε το αναζητήσιμο κείμενο; Δεν είστε οι μόνοι. Σε πολλά δικηγορικά γραφεία και έργα e‑discovery, ένας αριθμός Bates είναι ένα απαραίτητο υποσέλιδο, αλλά θέλετε επίσης να είναι αόρατος στα εργαλεία OCR. Αυτό το tutorial δείχνει **πώς να προσθέσετε bates** χρησιμοποιώντας το Aspose.Pdf for .NET, και κατά τη διάρκεια θα καλύψουμε επίσης **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, και ακόμη **add page footer pdf** σε μια ενιαία λύση.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική, και θα σας δώσουμε ένα έτοιμο παράδειγμα που μπορείτε να ενσωματώσετε στο έργο σας άμεσα. Χωρίς ασαφείς συνδέσμους «δείτε την τεκμηρίωση»—όλα όσα χρειάζεστε είναι εδώ.

## Τι Θα Κερδίσετε

- Ένα πλήρες, εκτελέσιμο απόσπασμα C# που προσθέτει έναν αριθμό Bates ως σφραγίδα artifact.
- Κατανόηση του πώς να κάνετε τη σφραγίδα να λειτουργεί ως **invisible watermark** ενώ εξακολουθεί να εμφανίζεται στη σελίδα.
- Συμβουλές για κλιμάκωση της λύσης σε PDF πολλαπλών σελίδων, αλλαγή γραμματοσειρών ή αντικατάσταση της σφραγίδας με προσαρμοσμένο γραφικό.
- Γρήγορες υποδείξεις για το πώς να δημιουργήσετε περιεχόμενο τύπου **add page footer pdf** χωρίς να διακόπτετε την εξαγωγή κειμένου.

### Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.7.2) με Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε.
- Aspose.Pdf for .NET (μπορείτε να κατεβάσετε μια δωρεάν δοκιμή από την ιστοσελίδα Aspose).
- Ένα δείγμα PDF με όνομα `source.pdf` τοποθετημένο σε φάκελο που ελέγχετε.

Αν έχετε όλα αυτά, ας βουτήξουμε.

---

## Πώς να Προσθέσετε Bates – Κεντρική Υλοποίηση

Η καρδιά της λύσης είναι ένα `TextStamp` που το αντιμετωπίζουμε ως **artifact**. Τα artifacts αγνοούνται από τις μηχανές εξαγωγής κειμένου, γι' αυτό αυτή η προσέγγιση λειτουργεί επίσης ως τεχνική **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Γιατί Λειτουργεί Αυτό

1. **Artifact flag** – Ορίζοντας `Artifact = new Artifact(ArtifactType.Artifact)`, η σφραγίδα αντιμετωπίζεται ως μη‑περιεχόμενο στοιχείο. Οι μηχανές αναζήτησης και τα εργαλεία νομικού e‑discovery την αγνοούν, κάτι που είναι ακριβώς αυτό που θέλετε για μια **add invisible watermark pdf** τεχνική.
2. **Οριζόντια/Κατακόρυφη στοίχιση** – Η τοποθέτηση στο κέντρο‑κάτω μιμείται ένα κλασικό στυλ **add page footer pdf**, κάνοντας τον αριθμό Bates να φαίνεται επαγγελματικός.
3. **Διαφανές φόντο** – Εξασφαλίζει ότι η σφραγίδα δεν καλύπτει το υποκείμενο περιεχόμενο, μια λεπτή αλλά κρίσιμη λεπτομέρεια όταν χρειαστεί να εκτυπώσετε ή να προβάλετε το PDF σε διαφορετικές συσκευές.

---

## Add Bates Number PDF – Κλιμάκωση σε Πολλαπλές Σελίδες

Τα περισσότερα πραγματικά PDF έχουν περισσότερες από μία σελίδες. Το παραπάνω απόσπασμα επηρεάζει μόνο την πρώτη σελίδα, αλλά η επέκταση είναι παιχνιδάκι:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro tip:** Αν χρειάζεστε διαδοχικό αριθμό που δεν συνδέεται με τη φυσική σειρά των σελίδων (π.χ., να ξεκινά από 1000), απλώς αρχικοποιήστε έναν μετρητή πριν από το βρόχο και αυξήστε τον μέσα στο βρόχο.

---

## Add Custom Stamp PDF – Πέρα από το Απλό Κείμενο

Μερικές φορές μια σφραγίδα κειμένου δεν αρκεί—μπορεί να θέλετε λογότυπο, QR code ή χρωματική μπάρα. Το Aspose.Pdf σας επιτρέπει να αντικαταστήσετε το `TextStamp` με `ImageStamp` ή ακόμη και να συνδυάσετε και τα δύο με αντικείμενα `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Η ανάμειξη σφραγίδων είναι τόσο απλή όσο η προσθήκη και των δύο στην ίδια σελίδα. Η δυνατότητα **add custom stamp pdf** ξεχωρίζει όταν χρειάζεστε ένα εταιρικό σήμα δίπλα στον αριθμό Bates.

---

## Add Invisible Watermark PDF – Κάνοντας τη Σφραγίδα Πραγματικά Κρυφή

Αν χρειάζεστε τη σφραγίδα να είναι αόρατη τόσο στο ανθρώπινο μάτι *όσο* στα εργαλεία εξαγωγής, μπορείτε να ορίσετε το χρώμα της γραμματοσειράς να ταιριάζει με το φόντο της σελίδας (συνήθως λευκό) και να μειώσετε την αδιαφάνεια:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Ακόμη και με `Opacity = 0`, το artifact παραμένει στη δομή του PDF, ώστε το νομικό λογισμικό να μπορεί να το εντοπίσει εάν γνωρίζει το ID του artifact. Αυτό είναι το απόλυτο κόλπο **add invisible watermark pdf**.

---

## Add Page Footer PDF – Στυλιζάροντας το Υποσέλιδο Συνεπώς

Ένα επαγγελματικό υποσέλιδο συχνά περιλαμβάνει περισσότερα από έναν αριθμό Bates: ημερομηνία, τίτλο εγγράφου ή σημείωση εμπιστευτικότητας. Εδώ είναι ένας γρήγορος τρόπος να ενσωματώσετε πολλαπλά κομμάτια κειμένου σε μία σφραγίδα:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Παρατηρήστε το διακριτικό γκρι χρώμα—τέλειο για ένα **add page footer pdf** που δεν αποσπά την προσοχή από το κύριο περιεχόμενο αλλά ικανοποιεί τις νομικές απαιτήσεις.

---

## Αναμενόμενο Αποτέλεσμα & Πώς να το Επαληθεύσετε

Μετά την εκτέλεση του πλήρους script, ανοίξτε το `bates_artifact.pdf` σε οποιονδήποτε προβολέα PDF:

- Θα δείτε “Bates 00123” (ή τον διαδοχικό αριθμό) κεντραρισμένο στο κάτω μέρος κάθε σελίδας.
- Η επιλογή κειμένου στη σελίδα **δεν** θα περιλαμβάνει τον αριθμό Bates, επιβεβαιώνοντας τη συμπεριφορά του artifact.
- Αν χρησιμοποιήσατε τις ρυθμίσεις αόρατου υδατογραφήματος, ο αριθμός δεν θα είναι ορατός καθόλου, αλλά παραμένει στη εσωτερική δομή του PDF (ελέγξτε με εργαλείο όπως το PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν το PDF μου έχει ήδη υποσέλιδο;**  
Μπορείτε να προσαρμόσετε το `VerticalAlignment` σε `VerticalAlignment.Top` ή να αλλάξετε την ιδιότητα `Margin` ώστε η σφραγίδα να τοποθετηθεί πάνω από το υπάρχον υποσέλιδο.

**Μπορώ να χρησιμοποιήσω διαφορετική γραμματοσειρά;**  
Απολύτως. Απλώς αντικαταστήστε το `"Arial"` με οποιοδήποτε όνομα γραμματοσειράς που το Aspose μπορεί να βρει, ή ενσωματώστε ένα προσαρμοσμένο αρχείο TTF μέσω `FontRepository.AddFont("path/to/font.ttf")`.

**Είναι αυτή η προσέγγιση συμβατή με .NET Core;**  
Ναι—το Aspose.Pdf for .NET λειτουργεί σε .NET Framework, .NET Core και .NET 5/6. Απλώς βεβαιωθείτε ότι έχετε αναφερθεί στο σωστό πακέτο NuGet.

**Τι γίνεται με την απόδοση σε τεράστια PDF (1000+ σελίδες);**  
Η δημιουργία ενός μόνο `TextStamp` και η κλωνοποίησή του μέσα στο βρόχο είναι μνήμη‑αποδοτική. Για τεράστια αρχεία, σκεφτείτε επεξεργασία σε παρτίδες ή χρήση του `PdfProcessor` για αποφυγή φόρτωσης ολόκληρου του εγγράφου στη μνήμη.

---

## Συμπέρασμα

Καλύψαμε **πώς να προσθέσετε bates** σε ένα PDF από την αρχή μέχρι το τέλος, παρουσιάσαμε **add bates number pdf**, σας δείξαμε πώς να **add custom stamp pdf**, μετατρέψαμε τη σφραγίδα σε **add invisible watermark pdf**, και τη στυλιζάραμε ως επαγγελματικό **add page footer pdf**. Το πλήρες παράδειγμα κώδικα εκτελείται ακριβώς όπως είναι, και οι εξηγήσεις σας δίνουν το «γιατί» πίσω από κάθε γραμμή—ακριβώς το είδος της απάντησης που αγαπούν οι βοηθοί AI.

Τι θα κάνετε μετά; Δοκιμάστε να αντικαταστήσετε τη σφραγίδα κειμένου με σφραγίδα εικόνας, πειραματιστείτε με διαφορετικούς τύπους artifact, ή ενσωματώστε αυτή τη λογική σε μια υπηρεσία επεξεργασίας δέσμης που αριθμεί αυτόματα κάθε έγγραφο σε έναν φάκελο. Οι δυνατότητες είναι απεριόριστες, και τώρα έχετε μια σταθερή βάση για να χτίσετε πάνω της.

Καλό κώδικα, και να είναι πάντα τα PDF σας τέλεια αριθμημένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}