---
category: general
date: 2026-06-30
description: Πώς να προσθέσετε σφραγίδα PDF χρησιμοποιώντας το Aspose.PDF και να προσαρμόσετε
  αυτόματα το κείμενο σε PDF. Αναλυτικό tutorial βήμα‑βήμα με πλήρες κώδικα, εξηγήσεις
  και συμβουλές.
draft: false
keywords:
- how to add stamp pdf
- adjust font size to fit
- auto‑fit text in pdf
language: el
og_description: Πώς να προσθέσετε σφραγίδα PDF εύκολα. Μάθετε πώς να προσαρμόζετε
  το μέγεθος γραμματοσειράς ώστε να ταιριάζει και να προσαρμόζει αυτόματα το κείμενο
  σε PDF με το Aspose.PDF σε λίγα λεπτά.
og_title: Πώς να προσθέσετε σφραγίδα PDF – Εκπαίδευση Αυτόματης Προσαρμογής Κειμένου
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  headline: How to add stamp pdf – Complete guide with auto‑fit text
  type: TechArticle
- description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  name: How to add stamp pdf – Complete guide with auto‑fit text
  steps:
  - name: Expected Output
    text: Open `autoFontStamp.pdf` in any PDF viewer. You should see a rectangular
      label on the first page, **exactly 300 × 100 points**, containing the phrase
      “Long text that must fit”. If the original string is longer than the rectangle
      can accommodate at the default font size, you’ll notice the text has sh
  - name: 1. Multiple Stamps on One Page
    text: If you need several annotations, simply repeat the `AddStamp` call with
      different `TextStamp` instances. Remember to adjust `XIndent` and `YIndent`
      to position each stamp.
  - name: 2. Changing Font Family or Color
    text: 'You can customize the appearance via the `TextState` property:'
  - name: 3. Using Images Instead of Text
    text: Aspose also supports `ImageStamp`. The same auto‑fit logic doesn’t apply,
      but you can manually size the image to the stamp rectangle.
  type: HowTo
tags:
- pdf
- aspnet
- stamp
- font-size
title: Πώς να προσθέσετε σφραγίδα PDF – Πλήρης οδηγός με αυτόματη προσαρμογή κειμένου
url: /el/net/programming-with-stamps-and-watermarks/how-to-add-stamp-pdf-complete-guide-with-auto-fit-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε σφραγίδα PDF – Πλήρης Οδηγός με Αυτόματη Προσαρμογή Κειμένου

Το πώς να προσθέσετε σφραγίδα PDF είναι συχνή ερώτηση όποτε χρειάζεται να σχολιάσετε ένα έγγραφο χωρίς να ανοίξετε έναν επεξεργαστή GUI. Έχετε προσπαθήσει ποτέ να τοποθετήσετε μια μακριά ετικέτα σε μια σελίδα PDF και να δείτε ότι υπερβαίνει τα άκρα; Σε αυτό το tutorial θα λύσουμε αυτό το πρόβλημα χρησιμοποιώντας το **Aspose.PDF for .NET** και θα σας δείξουμε πώς να **προσαρμόζετε αυτόματα το μέγεθος της γραμματοσειράς**.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε γιατί κάθε ρύθμιση είναι σημαντική και θα ολοκληρώσουμε με ένα πλήρως λειτουργικό PDF που αποδεικνύει ότι η σφραγίδα πραγματικά συρρικνώνεται (ή επεκτείνεται) ώστε να παραμείνει μέσα στο ορθογώνιο της. Χωρίς ασαφείς αναφορές—απλώς μια συγκεκριμένη λύση copy‑and‑paste που μπορείτε να τρέξετε σήμερα.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
* Το πακέτο NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`).  
* Ένα αρχείο PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (θα τον ονομάσουμε `YOUR_DIRECTORY`).  
* Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider ή ακόμη και VS Code.

Αυτό είναι όλο. Χωρίς εξωτερικές υπηρεσίες, χωρίς κόλπα αδειοδότησης (η Aspose προσφέρει ένα δωρεάν κλειδί δοκιμής που μπορείτε να ενσωματώσετε για δοκιμές). Έτοιμοι; Ας ξεκινήσουμε.

## Πώς να προσθέσετε σφραγίδα PDF – Βήμα 1: Φόρτωση του Πηγαίου Εγγράφου

Το πρώτο πράγμα που πρέπει να κάνετε είναι να ανοίξετε το PDF που θέλετε να τροποποιήσετε. Το Aspose.PDF αντιμετωπίζει ένα αρχείο ως αντικείμενο `Document`, το οποίο σας δίνει πρόσβαση σε σελίδες, σημειώσεις και, φυσικά, σφραγίδες.

```csharp
using Aspose.Pdf;

// Step 1: Open the source PDF document
using (var document = new Document(@"YOUR_DIRECTORY\input.pdf"))
{
    // The using‑statement ensures the file is closed properly.
```

> **Γιατί αυτό είναι σημαντικό:**  
> Το άνοιγμα του εγγράφου μέσα σε ένα μπλοκ `using` εγγυάται ότι όλα τα handles αρχείων απελευθερώνονται, αποτρέποντας σφάλματα “αρχείο κλειδωμένο” όταν αργότερα προσπαθήσετε να αποθηκεύσετε ή να διαγράψετε το PDF.

## Προσαρμογή μεγέθους γραμματοσειράς για να ταιριάζει – Διαμόρφωση του TextStamp

Τώρα δημιουργούμε ένα αντικείμενο `TextStamp`. Αυτό είναι το κομμάτι που θα εμφανιστεί στην σελίδα. Η μαγεία συμβαίνει όταν ενεργοποιούμε το **AutoAdjustFontSizeToFitStampRectangle** και ορίζουμε μια τιμή ακρίβειας.

```csharp
    // Step 2: Create a text stamp and enable automatic font size adjustment
    var stamp = new TextStamp("Long text that must fit")
    {
        // Shrink or expand text to fit the stamp area automatically
        AutoAdjustFontSizeToFitStampRectangle = true,

        // Precision for the size calculation (0.01 = 1% tolerance)
        AutoAdjustFontSizePrecision = 0.01f,

        // Define the rectangle that the stamp must stay inside
        Width = 300,   // points (approx 4.2 inches)
        Height = 100,  // points (approx 1.4 inches)

        // Keep the original text scaling; we only want font size to change
        Scale = false
    };
```

> **Συμβουλή επαγγελματία:** Αν εργάζεστε με πολυγλωσσικό κείμενο, ορίστε επίσης `stamp.TextState.Font = FontRepository.FindFont("Arial Unicode MS");` για να αποφύγετε προβλήματα με ελλείποντα γλύφους.

> **Γιατί αυτό λειτουργεί:**  
> Το `AutoAdjustFontSizeToFitStampRectangle` λέει στο Aspose να υπολογίσει το μεγαλύτερο δυνατό μέγεθος γραμματοσειράς που εξακολουθεί να χωράει μέσα στο ορθογώνιο που ορίζεται από `Width` και `Height`. Η `AutoAdjustFontSizePrecision` ελέγχει πόσο λεπτομερής είναι αυτή η εκτίμηση—μικρότερο αριθμό σημαίνει πιο στενή προσαρμογή αλλά ελαφρώς μεγαλύτερο χρόνο επεξεργασίας.

## Αυτόματη προσαρμογή κειμένου σε PDF – Προσθήκη της Σφραγίδας σε Σελίδα

Με τη σφραγίδα διαμορφωμένη, το επόμενο βήμα είναι να την τοποθετήσουμε σε μια συγκεκριμένη σελίδα. Στο παράδειγμά μας θα χρησιμοποιήσουμε την πρώτη σελίδα, αλλά μπορείτε να στοχεύσετε οποιοδήποτε δείκτη (`document.Pages[3]` για την τρίτη σελίδα, για παράδειγμα).

```csharp
    // Step 3: Add the stamp to the first page of the PDF
    document.Pages[1].AddStamp(stamp);
```

> **Συχνή ερώτηση:** *Τι γίνεται αν το PDF δεν έχει σελίδες;*  
> Το Aspose θα ρίξει μια εξαίρεση `ArgumentOutOfRangeException`. Μια γρήγορη προστατευτική δήλωση (`if (document.Pages.Count == 0) throw new InvalidOperationException("PDF is empty.");`) κάνει τον κώδικα πιο ανθεκτικό.

## Αποθήκευση του PDF – Επαλήθευση του Αποτελέσματος

Τέλος, γράφουμε τις αλλαγές πίσω στο δίσκο. Το όνομα του αρχείου εξόδου καθιστά σαφές ότι το μέγεθος γραμματοσειράς της σφραγίδας προσαρμόστηκε αυτόματα.

```csharp
    // Step 4: Save the modified PDF with the auto‑adjusted stamp
    document.Save(@"YOUR_DIRECTORY\autoFontStamp.pdf");
} // End of using block – document is disposed here
```

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `autoFontStamp.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε μια ορθογώνια ετικέτα στην πρώτη σελίδα, **ακριβώς 300 × 100 points**, που περιέχει τη φράση “Long text that must fit”. Αν η αρχική συμβολοσειρά είναι μεγαλύτερη από ό,τι μπορεί να χωρέσει το ορθογώνιο στο προεπιλεγμένο μέγεθος γραμματοσειράς, θα παρατηρήσετε ότι το κείμενο έχει συρρικνωθεί ακριβώς όσο χρειάζεται για να παραμείνει μέσα—χωρίς αποκοπή, χωρίς υπερχείλιση.

![Στιγμιότυπο οθόνης PDF με αυτόματη προσαρμογή σφραγίδας](https://example.com/auto-fit-stamp.png "παράδειγμα αυτόματης προσαρμογής κειμένου σε PDF")  
*Alt text: Στιγμιότυπο οθόνης PDF με αυτόματη προσαρμογή σφραγίδας που δείχνει το προσαρμοσμένο μέγεθος γραμματοσειράς.*

## Περιπτώσεις Άκρων & Παραλλαγές

### 1. Πολλαπλές Σφραγίδες σε Μία Σελίδα

Αν χρειάζεστε πολλές σημειώσεις, απλώς επαναλάβετε την κλήση `AddStamp` με διαφορετικά αντικείμενα `TextStamp`. Θυμηθείτε να προσαρμόσετε τα `XIndent` και `YIndent` για να τοποθετήσετε κάθε σφραγίδα.

```csharp
stamp.XIndent = 50;   // horizontal offset from the left edge
stamp.YIndent = 150;  // vertical offset from the bottom edge
document.Pages[1].AddStamp(stamp);
```

### 2. Αλλαγή Οικογένειας Γραμματοσειράς ή Χρώματος

Μπορείτε να προσαρμόσετε την εμφάνιση μέσω της ιδιότητας `TextState`:

```csharp
stamp.TextState.Font = FontRepository.FindFont("Times New Roman");
stamp.TextState.FontSize = 12; // base size; auto‑adjust will override if needed
stamp.TextState.ForegroundColor = Color.FromRgb(255, 0, 0); // red text
```

### 3. Χρήση Εικόνων Αντί Κειμένου

Το Aspose υποστηρίζει επίσης `ImageStamp`. Η ίδια λογική αυτόματης προσαρμογής δεν ισχύει, αλλά μπορείτε να ορίσετε χειροκίνητα το μέγεθος της εικόνας ώστε να ταιριάζει στο ορθογώνιο της σφραγίδας.

```csharp
var imgStamp = new ImageStamp(@"YOUR_DIRECTORY\logo.png")
{
    Width = 200,
    Height = 80,
    XIndent = 20,
    YIndent = 20
};
document.Pages[1].AddStamp(imgStamp);
```

## Πρακτικές Συμβουλές από το Πεδίο

* **Μην κωδικοποιείτε σκληρά διαδρομές** – χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "input.pdf")` για φορητότητα.  
* **Επεξεργασία κατά παρτίδες** – τυλίξτε ολόκληρη τη διαδικασία σε βρόχο `foreach (var file in Directory.GetFiles(...))` για να σφραγίσετε δεκάδες PDF αυτόματα.  
* **Απόδοση** – εάν επεξεργάζεστε μεγάλα PDF, σκεφτείτε να απενεργοποιήσετε το `AutoAdjustFontSizePrecision` (ορίστε το σε `0.05f`) για να επιταχύνετε τον υπολογισμό με αμελητέο οπτικό αποτέλεσμα.  
* **Δοκιμή** – πάντα ανοίξτε το παραγόμενο PDF μετά την πρώτη εκτέλεση για να επιβεβαιώσετε ότι οι διαστάσεις του ορθογωνίου είναι όπως περιμένετε. Μια γρήγορη οπτική επιθεώρηση εξοικονομεί ώρες εντοπισμού σφαλμάτων αργότερα.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, copy‑and‑paste λύση για **πώς να προσθέσετε σφραγίδα PDF** ενώ αυτόματα **προσαρμόζετε το μέγεθος της γραμματοσειράς για να ταιριάζει** και επιτυγχάνετε **αυτόματη προσαρμογή κειμένου σε PDF** χρησιμοποιώντας το Aspose.PDF. Φορτώνοντας το έγγραφο, διαμορφώνοντας ένα `TextStamp` με ενεργοποιημένη την αυτόματη προσαρμογή, τοποθετώντας το στη ζητούμενη σελίδα και αποθηκεύοντας το αρχείο, μπορείτε να σχολιάζετε PDF προγραμματιστικά χωρίς να ανησυχείτε για υπερβολικό κείμενο.

Τι ακολουθεί; Δοκιμάστε να συνδυάσετε αυτήν την τεχνική με ροές εργασίας που βασίζονται σε δεδομένα—τραβήξτε ονόματα πελατών από μια βάση δεδομένων και σφραγίστε κάθε τιμολόγιο σε βρόχο. Ή πειραματιστείτε με διαφορετικά μεγέθη ορθογωνίου για να δείτε πώς αλγόριθμος αυτόματης προσαρμογής συμπεριφέρεται σε πολύ σύντομες έναντι εξαιρετικά μεγάλων συμβολοσειρών.

Έχετε κάποιο δικό σας κόλπο που θέλετε να μοιραστείτε; Αφήστε ένα σχόλιο, ή ξεκινήστε ένα νέο project και αφήστε τη μαγεία της αυτόματης προσαρμογής να κάνει τη δουλειά της. Καλό προγραμματισμό!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Προσθέσετε Σφραγίδα Κειμένου σε PDF Χρησιμοποιώντας το Aspose.PDF for .NET](/pdf/english/net/document-manipulation/add-text-stamp-pdf-aspose-dotnet/)
- [Πώς να Προσθέσετε και να Ευθυγραμμίσετε Σφραγίδες Κειμένου σε PDF Χρησιμοποιώντας το Aspose.PDF for .NET | Υδατογραφήματα & Υπόβαθρα](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Πώς να Προσθέσετε Σφραγίδα Εικόνας σε PDF Χρησιμοποιώντας το Aspose.PDF for .NET: Ένας Πλήρης Οδηγός](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}