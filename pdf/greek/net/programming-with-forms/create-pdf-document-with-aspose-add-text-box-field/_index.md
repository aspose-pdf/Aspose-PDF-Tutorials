---
category: general
date: 2026-03-24
description: Δημιουργήστε έγγραφο PDF χρησιμοποιώντας το Aspose.PDF σε C#. Μάθετε
  πώς να προσθέσετε πεδίο κειμένου σε φόρμα PDF και να προσθέσετε γρήγορα πεδίο φόρμας
  PDF.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: el
og_description: Δημιουργήστε έγγραφο PDF με το Aspose.PDF σε C#. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε πεδίο κειμένου σε φόρμα PDF και πώς να προσθέσετε πεδίο φόρμας
  PDF σε λίγα λεπτά.
og_title: Δημιουργία εγγράφου PDF με το Aspose – Προσθήκη πεδίου πλαισίου κειμένου
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Δημιουργία εγγράφου PDF με το Aspose – Προσθήκη πεδίου πλαισίου κειμένου
url: /el/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου PDF με Aspose – Προσθήκη Πεδίου Πλαισίου Κειμένου

Έχετε ποτέ χρειαστεί να **δημιουργήσετε έγγραφο PDF** προγραμματιστικά και αναρωτηθήκατε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν οι εφαρμογές τους πρέπει να συλλέγουν εισροές χρήστη χωρίς να ενσωματώνουν μια βαριά βιβλιοθήκη UI. Τα καλά νέα; Με το Aspose.PDF for .NET μπορείτε να δημιουργήσετε ένα PDF, να τοποθετήσετε ένα πλαίσιο κειμένου σε οποιαδήποτε σελίδα, και ακόμη να συνδέσετε το ίδιο πεδίο σε πολλές σελίδες—όλα σε λίγες γραμμές.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την αρχικοποίηση του PDF, μέχρι **add text box PDF** πεδία φόρμας, μέχρι **add form field PDF** καταχώρηση, και τελικά πώς να επαληθεύσετε ότι όλα λειτουργούν. Στο τέλος θα γνωρίζετε **how to create PDF** αρχεία που είναι διαδραστικά, και θα δείτε επίσης **how to add textbox** ελέγχους που συμπεριφέρονται ακριβώς όπως τα εγγενή πεδία του Acrobat.

---

## Τι Θα Χρειαστείτε

- **ASP.NET Core** ή οποιοδήποτε έργο .NET 6+ (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- **Aspose.PDF for .NET** πακέτο NuGet (έκδοση 23.9 ή νεότερη).  
- Μια μέτρια εμπειρία σε C#—τίποτα περίπλοκο, μόνο τα βασικά.  

Αν έχετε τσεκάρει αυτά τα σημεία, είμαστε έτοιμοι να προχωρήσουμε. Χωρίς επιπλέον εργαλεία, χωρίς εξωτερικές υπηρεσίες, μόνο καθαρός κώδικας C# που μπορείτε να επικολλήσετε σε μια κονσόλα εφαρμογή και να εκτελέσετε.

---

## Δημιουργία Εγγράφου PDF και Προσθήκη Πεδίου Φόρμας Πλαισίου Κειμένου

Το πρώτο βήμα, προφανώς, είναι να **create PDF document**. Σκεφτείτε την κλάση `Document` ως ένα κενό καμβά· μόλις το έχετε, μπορείτε να αρχίσετε να σχεδιάζετε σελίδες, σχήματα και διαδραστικά στοιχεία.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Why this matters:** Η δημιουργία ενός `Document` χωρίς σελίδες προκαλεί εξαίρεση τη στιγμή που προσπαθείτε να τοποθετήσετε ένα widget. Η προσθήκη μιας σελίδας πρώτα εγγυάται έναν έγκυρο δείκτη σελίδας (`Pages[1]`) για τα επόμενα βήματα.

---

## Προσθήκη Πεδίου Φόρμας PDF Πλαισίου Κειμένου στη Σελίδα 1

Τώρα που έχουμε μια σελίδα, ας **add text box PDF** πεδίο φόρμας. Η κλάση `TextBoxField` αντιπροσωπεύει ένα μοναδικό λογικό πεδίο· μπορείτε να το θεωρήσετε ως το “όνομα” της εισόδου που μπορεί να εμφανίζεται σε πολλά σημεία.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Pro tip:** Το ορθογώνιο χρησιμοποιεί μονάδες points (1/72 ίντσα). Προσαρμόστε τις συντεταγμένες ώστε να ταιριάζουν με τη διάταξή σας· το σημείο αρχής (0,0) βρίσκεται στην κάτω‑αριστερή γωνία της σελίδας.

---

## Δημιουργία Δεύτερου Widget σε Άλλη Σελίδα

Ένα μοναδικό λογικό πεδίο μπορεί να έχει πολλαπλά οπτικά widgets—ιδανικό για φόρμες πολλαπλών σελίδων. Εδώ είναι **how to add textbox** σε δεύτερη σελίδα, επαναχρησιμοποιώντας το ίδιο όνομα πεδίου.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Why we do this:** Οι χρήστες συχνά χρειάζονται να συμπληρώσουν τις ίδιες πληροφορίες σε διαφορετικές ενότητες (π.χ., “Name” στην κορυφή και ξανά σε μια σύνοψη). Με το κοινό λογικό όνομα, το Aspose διασφαλίζει ότι και τα δύο widgets παραμένουν συγχρονισμένα.

---

## Καταχώρηση του Πεδίου Φόρμας στο PDF

Η δημιουργία του αντικειμένου πεδίου δεν αρκεί· πρέπει να το προσθέσετε στη συλλογή φορμών του εγγράφου. Αυτό είναι το βήμα όπου **add form field PDF** προστίθεται στη εσωτερική δομή.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **What happens under the hood:** Η `Form.Add` γράφει τον ορισμό του πεδίου στο λεξικό AcroForm, καθιστώντας το PDF διαδραστικό όταν ανοίγει στο Acrobat Reader ή σε οποιονδήποτε προβολέα PDF που υποστηρίζει φόρμες.

---

## Εκτέλεση και Επαλήθευση του Αποτελέσματος

Συγκεντρώστε και εκτελέστε την κονσόλα εφαρμογή. Ανοίξτε το `MultiWidgetExample.pdf` στο Adobe Acrobat (ή σε οποιονδήποτε προβολέα που υποστηρίζει φόρμες) και θα δείτε δύο ταυτόσημα πλαίσια κειμένου στις σελίδες 1 και 2. Πληκτρολογήστε κάτι σε ένα πλαίσιο—παρακολουθήστε το άλλο να ενημερώνεται αμέσως. Αυτή είναι η δύναμη ενός κοινόχρηστου λογικού πεδίου.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Αν δεν βλέπετε τα πλαίσια, ελέγξτε ξανά ότι τα ορθογώνια βρίσκονται εντός των ορίων της σελίδας και ότι έχετε αποθηκεύσει το έγγραφο μετά την προσθήκη του πεδίου.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι αν χρειάζομαι διαφορετική εμφάνιση σε κάθε σελίδα;

Μπορείτε να προσαρμόσετε κάθε widget μετά τη δημιουργία:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Μπορώ να ορίσω προεπιλεγμένη τιμή;

Βεβαίως—απλώς ορίστε το `Value` πριν την αποθήκευση:

```csharp
textBoxField.Value = "Enter your name here";
```

Όλα τα widgets θα εμφανίζουν αυτό το placeholder μέχρι ο χρήστης το αντικαταστήσει.

### Πώς να κάνετε το πεδίο υποχρεωτικό;

```csharp
textBoxField.Required = true;
```

Το Acrobat θα προειδοποιήσει τον χρήστη αν προσπαθήσει να υποβάλει τη φόρμα χωρίς να το συμπληρώσει.

### Λειτουργεί αυτό με τη συμμόρφωση PDF/A;

Το Aspose.PDF υποστηρίζει PDF/A‑1b,‑2b,‑3b. Αφού ολοκληρώσετε τη δημιουργία της φόρμας, μπορείτε να μετατρέψετε:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Αποθηκεύστε το ως `Program.cs` σε ένα .NET console project, προσθέστε το πακέτο NuGet Aspose.PDF, και εκτελέστε.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}