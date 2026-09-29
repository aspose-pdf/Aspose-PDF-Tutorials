---
category: general
date: 2026-04-10
description: Δημιουργήστε έγγραφο PDF C# με σαφή παράδειγμα. Μάθετε πώς να προσθέσετε
  πολλαπλές σελίδες PDF, να προσθέσετε πεδίο κειμενικού πλαισίου, πώς να προσθέσετε
  widget και να αποθηκεύσετε το PDF με τη φόρμα.
draft: false
keywords:
- create pdf document c#
- add multiple pages pdf
- save pdf with form
- how to add widget
- add text box field
language: el
og_description: Δημιουργήστε γρήγορα έγγραφο PDF με C#. Αυτός ο οδηγός δείχνει πώς
  να προσθέσετε πολλαπλές σελίδες PDF, να προσθέσετε πεδίο πλαισίου κειμένου, πώς
  να προσθέσετε widget και να αποθηκεύσετε το PDF με φόρμα.
og_title: Δημιουργία εγγράφου PDF C# – Πλήρες σεμινάριο για φόρμα πολλαπλών σελίδων
tags:
- C#
- PDF
- Form handling
title: Δημιουργία εγγράφου PDF C# – Οδηγός βήμα‑προς‑βήμα για πολυσελίδες φόρμες
url: /el/net/programming-with-forms/create-pdf-document-c-step-by-step-guide-to-multi-page-forms/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου PDF C# – Οδηγός Βήμα‑βήμα για Φόρμες Πολλών Σελίδων

Έχετε αναρωτηθεί ποτέ πώς να **create PDF document C#** που εκτείνεται σε πολλές σελίδες και περιέχει διαδραστικά πεδία; Ίσως δημιουργείτε έναν γεννήτρια τιμολογίων, μια φόρμα εγγραφής ή μια απλή αναφορά που οι χρήστες θα συμπληρώσουν αργότερα. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — από την αρχικοποίηση ενός PDF, την προσθήκη πολλαπλών σελίδων, την εισαγωγή ενός πεδίου text box, την προσθήκη μιας widget annotation, μέχρι τελικά το **save PDF with form** δεδομένα. Χωρίς περιττές πληροφορίες, μόνο ένα πρακτικό παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

Θα προσθέσουμε επίσης πρακτικές συμβουλές όπως *πώς να προσθέσετε widget* σωστά και γιατί μπορεί να θέλετε να επαναχρησιμοποιήσετε ένα πεδίο σε διαφορετικές σελίδες. Στο τέλος θα έχετε ένα λειτουργικό `multibox.pdf` που δείχνει ένα κοινόχρηστο text box σε δύο σελίδες.

## Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.7 ή νεότερο) – οποιοδήποτε πρόσφατο runtime λειτουργεί.
- Μια βιβλιοθήκη διαχείρισης PDF που παρέχει τις κλάσεις `Document`, `TextBoxField` και `WidgetAnnotation`. Ο κώδικας παρακάτω χρησιμοποιεί το δημοφιλές **Aspose.PDF for .NET**, αλλά οι έννοιες μεταφράζονται σε iTextSharp, PdfSharp ή άλλες βιβλιοθήκες.
- Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε.
- Βασική εξοικείωση με C# – δεν χρειάζεται να γνωρίζετε σε βάθος τις εσωτερικές λειτουργίες του PDF, μόνο τις κλήσεις API.

> **Pro tip:** Αν δεν έχετε εγκαταστήσει ακόμη τη βιβλιοθήκη, εκτελέστε `dotnet add package Aspose.PDF` από το τερματικό.

## Βήμα 1: Create PDF Document C# – Αρχικοποίηση του Document

Πρώτα απ' όλα, χρειαζόμαστε έναν κενό καμβά. Το αντικείμενο `Document` αντιπροσωπεύει ολόκληρο το αρχείο PDF.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Create a new PDF document
using (var document = new Document())
{
    // The rest of the code lives inside this using block
}
```

Γιατί τυλίγουμε το έγγραφο σε δήλωση `using`; Εξασφαλίζει ότι όλες οι μη διαχειριζόμενες πόροι απελευθερώνονται και το αρχείο αποθηκεύεται στο δίσκο όταν καλούμε `Save`. Αυτό το πρότυπο είναι η συνιστώμενη μέθοδος εργασίας με PDF σε C#.

## Βήμα 2: Add Multiple Pages PDF

Ένα PDF χωρίς σελίδες είναι, λοιπόν, αόρατο. Ας προσθέσουμε δύο σελίδες — η μία θα φιλοξενήσει το ίδιο το πεδίο, η άλλη θα κρατήσει ένα widget που δείχνει στο ίδιο πεδίο.

```csharp
// Step 2: Add two pages – one for the field, one for the widget
var firstPage = document.Pages.Add();
var secondPage = document.Pages.Add();
```

> **Γιατί δύο σελίδες;** Όταν θέλετε η ίδια είσοδο να εμφανίζεται σε πολλές σελίδες, δημιουργείτε ένα *field* μία φορά και στη συνέχεια το αναφέρετε με *widget annotations* στις άλλες σελίδες. Αυτό διατηρεί τα δεδομένα συγχρονισμένα αυτόματα.

Παρακάτω υπάρχει ένα απλό διάγραμμα που οπτικοποιεί τη σχέση (το alt text περιλαμβάνει τη βασική λέξη-κλειδί για προσβασιμότητα).

![Δημιουργία εγγράφου PDF C# διάγραμμα που δείχνει το πεδίο στη σελίδα 1 και το widget στη σελίδα 2](image.png)

*Alt text: διάγραμμα create pdf document c# που απεικονίζει ένα κοινόχρηστο πεδίο text box σε δύο σελίδες.*

## Βήμα 3: Add Text Box Field to Your PDF

Τώρα τοποθετούμε ένα text box στην πρώτη σελίδα. Το rectangle ορίζει τη θέση και το μέγεθός του (συντεταγμένες σε points, 72 pts = 1 inch).

```csharp
// Step 3: Create a text box field on the first page and give it a shared name and value
var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
sharedTextBox.PartialName = "MultiBox";
sharedTextBox.Value = "Shared value";
```

- **PartialName** είναι το αναγνωριστικό που μοιράζονται τόσο το πεδίο όσο και οποιοδήποτε widget.
- Ορίζοντας `Value` εδώ δίνει στο πεδίο μια προεπιλεγμένη εμφάνιση, η οποία θα εμφανιστεί επίσης στη σελίδα του widget.

## Βήμα 4: How to Add Widget – Αναφορά του Ίδιου Πεδίου σε Άλλη Σελίδα

Ένα widget είναι ουσιαστικά ένας οπτικός δείκτης που παραπέμπει πίσω στο αρχικό πεδίο. Χρησιμοποιώντας το ίδιο rectangle, το widget φαίνεται ταυτόσημο με το πεδίο, αλλά βρίσκεται σε διαφορετική σελίδα.

```csharp
// Step 4: Create a widget annotation on the second page that references the same field rectangle
var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
sharedWidget.PartialName = sharedTextBox.PartialName;
secondPage.Annotations.Add(sharedWidget);
```

> **Κοινό λάθος:** Η παράλειψη προσθήκης του widget στο `secondPage.Annotations`. Χωρίς αυτή τη γραμμή το widget δεν εμφανίζεται, παρόλο που το αντικείμενο υπάρχει.

## Βήμα 5: Register the Field and Save PDF with Form

Τώρα ενημερώνουμε τη συλλογή φορμών του εγγράφου για το νέο μας πεδίο. Η μέθοδος `Add` παίρνει το αντικείμενο του πεδίου και το όνομά του. Τέλος, γράφουμε το αρχείο στο δίσκο.

```csharp
// Step 5: Register the field with the document form
document.Form.Add(sharedTextBox, "MultiBox");

// Step 6: Save the PDF containing the multi‑page field
document.Save("YOUR_DIRECTORY/multibox.pdf");
```

Όταν ανοίξετε το `multibox.pdf` στο Adobe Acrobat ή σε οποιονδήποτε PDF viewer που υποστηρίζει φόρμες, θα δείτε το ίδιο text box και στις δύο σελίδες. Η επεξεργασία του σε μια σελίδα ενημερώνει αμέσως την άλλη επειδή μοιράζονται το ίδιο υποκείμενο πεδίο.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας τα παραπάνω, ορίστε το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var document = new Document())
        {
            // Step 2: Add two pages – one for the field, one for the widget
            var firstPage = document.Pages.Add();
            var secondPage = document.Pages.Add();

            // Step 3: Create a text box field on the first page and give it a shared name and value
            var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
            sharedTextBox.PartialName = "MultiBox";
            sharedTextBox.Value = "Shared value";

            // Step 4: Create a widget annotation on the second page that references the same field rectangle
            var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
            sharedWidget.PartialName = sharedTextBox.PartialName;
            secondPage.Annotations.Add(sharedWidget);

            // Step 5: Register the field with the document form
            document.Form.Add(sharedTextBox, "MultiBox");

            // Step 6: Save the PDF containing the multi‑page field
            document.Save("multibox.pdf");
        }

        Console.WriteLine("PDF created successfully! Check the file 'multibox.pdf'.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- **Δύο σελίδες**: Η Σελίδα 1 εμφανίζει ένα text box με το προεπιλεγμένο κείμενο “Shared value”.  
- **Σελίδα 2** αντικατοπτρίζει το ίδιο κουτί. Πληκτρολογώντας σε μία ενημερώνει αμέσως την άλλη.  
- Το μέγεθος του αρχείου είναι μικρό (μερικά kilobytes) επειδή προσθέσαμε μόνο απλά αντικείμενα φόρμας.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να προσθέσω περισσότερα από ένα widget για το ίδιο πεδίο;

Απολύτως. Απλώς επαναλάβετε το βήμα δημιουργίας widget για κάθε επιπλέον σελίδα, χρησιμοποιώντας το ίδιο `PartialName`. Αυτό είναι χρήσιμο για συμβάσεις πολλαπλών σελίδων όπου το ίδιο πεδίο υπογραφής εμφανίζεται στο κάτω μέρος κάθε σελίδας.

### Τι γίνεται αν χρειάζομαι διαφορετικό μέγεθος ή θέση στη δεύτερη σελίδα;

Μπορείτε να δημιουργήσετε ένα νέο `Rectangle` για το widget διατηρώντας το ίδιο `PartialName`. Η τιμή του πεδίου θα συγχρονίζεται, αλλά η οπτική διάταξη μπορεί να διαφέρει ανά σελίδα.

### Λειτουργεί αυτό με PDF προστατευμένα με κωδικό;

Ναι, αλλά πρέπει πρώτα να ανοίξετε το έγγραφο με τον σωστό κωδικό:

```csharp
var document = new Document("protected.pdf", "ownerPassword");
```

Στη συνέχεια συνεχίστε με τα ίδια βήματα. Η βιβλιοθήκη θα διατηρήσει την κρυπτογράφηση όταν καλέσετε `Save`.

### Πώς μπορώ να ανακτήσω την εισαχθείσα τιμή προγραμματιστικά;

Αφού ένας χρήστης συμπληρώσει τη φόρμα και εσείς φορτώσετε ξανά το PDF:

```csharp
var loaded = new Document("multibox.pdf");
var field = loaded.Form["MultiBox"] as TextBoxField;
Console.WriteLine("User entered: " + field.Value);
```

### Τι γίνεται αν θέλω να «flatten» τη φόρμα (να κάνω τα πεδία μη‑επεξεργάσιμα);

Καλέστε `document.Form.Flatten()` πριν αποθηκεύσετε. Αυτό μετατρέπει τα διαδραστικά πεδία σε στατικό περιεχόμενο, χρήσιμο για τελικά τιμολόγια.

## Συμπεράσματα

Μόλις **create PDF document C#** που εκτείνεται σε πολλαπλές σελίδες, προσθέσαμε ένα επαναχρησιμοποιήσιμο πεδίο text box, δείξαμε **πώς να προσθέσετε widget** annotations, και τέλος **save PDF with form** δεδομένα. Το βασικό συμπέρασμα είναι ότι ένα μόνο πεδίο μπορεί να οπτικοποιηθεί σε οποιονδήποτε αριθμό σελίδων μέσω widgets, διατηρώντας την είσοδο του χρήστη συνεπή σε όλο το έγγραφο.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε:

- Προσθήκη **checkbox** ή **dropdown** χρησιμοποιώντας το ίδιο μοτίβο.  
- Συμπλήρωση του PDF με δεδομένα από βάση δεδομένων αντί για στατική τιμή.  
- Εξαγωγή του συμπληρωμένου PDF σε byte array για λήψη μέσω HTTP σε ASP.NET Core API.

Πειραματιστείτε, σπάστε πράγματα και μετά διορθώστε τα — έτσι μαθαίνετε πραγματικά τη δημιουργία PDF σε C#. Αν αντιμετωπίσετε δυσκολίες, αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση της βιβλιοθήκης για πιο λεπτομερείς πληροφορίες.

Καλή προγραμματιστική, και καλή δημιουργία έξυπνων PDF!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}