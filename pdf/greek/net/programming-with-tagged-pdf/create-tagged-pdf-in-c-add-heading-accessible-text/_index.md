---
category: general
date: 2026-01-15
description: Δημιουργήστε ετικετοποιημένο PDF με το Aspose.Pdf σε C#. Μάθετε πώς να
  προσθέσετε τίτλο σε PDF, να ορίσετε προσβάσιμο κείμενο και να προσθέσετε σελίδα
  σε PDF σε έναν οδηγό βήμα‑βήμα.
draft: false
keywords:
- create tagged pdf
- add heading to pdf
- how to add heading
- add page to pdf
- set accessible text
language: el
og_description: Δημιουργία ετικετοποιημένου PDF με το Aspose.Pdf σε C#. Αυτός ο οδηγός
  δείχνει πώς να προσθέσετε τίτλο σε PDF, να ορίσετε προσβάσιμο κείμενο και να προσθέσετε
  σελίδα σε PDF.
og_title: Δημιουργία Tagged PDF σε C# – Προσθήκη Επικεφαλίδας & Προσβάσιμου Κειμένου
tags:
- Aspose.Pdf
- C#
- PDF accessibility
title: Δημιουργία Tagged PDF σε C# – Προσθήκη Επικεφαλίδας & Προσβάσιμου Κειμένου
url: /el/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-add-heading-accessible-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Tagged PDF σε C# – Προσθήκη Επικεφαλίδας & Προσβάσιμου Κειμένου

Έχετε ποτέ χρειαστεί να **create tagged PDF** αρχεία αλλά δεν ήξερες από πού να ξεκινήσεις; Σε αυτό το οδηγό θα περάσουμε βήμα‑βήμα τις ακριβείς ενέργειες για να προσθέσετε επικεφαλίδα σε PDF, να ορίσετε προσβάσιμο κείμενο, και ακόμη να προσθέσετε μια νέα σελίδα σε PDF—όλα χρησιμοποιώντας το Aspose.Pdf για .NET.  

Αν έχετε ποτέ αναρωτηθεί *πώς να προσθέσετε επικεφαλίδα* που οι αναγνώστες οθόνης μπορούν να καταλάβουν, βρίσκεστε στο σωστό μέρος. Στο τέλος θα έχετε ένα πλήρως‑tagged, προσβάσιμο PDF που μπορείτε να παραδώσετε σε πελάτες που απαιτούν συμμόρφωση ή σε εσωτερικούς ελεγκτές.

## Τι Θα Μάθετε

- Πώς να **create tagged pdf** από την αρχή με Aspose.Pdf  
- Ο ακριβής κώδικας για **add heading to pdf** και ενσωμάτωση μιας παραγράφου κάτω από αυτήν  
- Τρόποι για **set accessible text** ώστε οι βοηθητικές τεχνολογίες να διαβάζουν το σωστό περιεχόμενο  
- Ένα γρήγορο tip για **add page to pdf** όταν χρειάζεστε περισσότερο χώρο  
- Παγίδες βέλτιστων πρακτικών που πρέπει να αποφύγετε (και μερικά pro tips)

> **Prerequisite:** .NET 6+ (ή .NET Framework 4.6+) και έγκυρη άδεια Aspose.Pdf ή δοκιμαστικό DLL. Δεν απαιτούνται άλλες βιβλιοθήκες.

![Παράδειγμα δημιουργίας Tagged PDF](image.png "Στιγμιότυπο που δείχνει ένα Tagged PDF με επικεφαλίδα και παράγραφο – create tagged pdf")

## Create Tagged PDF – Επισκόπηση

Πριν βουτήξουμε στα επιμέρους βήματα, ας κατανοήσουμε τη μεγάλη εικόνα. Ένα **tagged PDF** περιέχει ένα λογικό δέντρο δομής που περιγράφει τη σειρά ανάγνωσης και τη σημασιολογία (επικεφαλίδες, παράγραφοι, πίνακες κ.λπ.). Αυτό το δέντρο είναι αυτό που χρησιμοποιούν οι αναγνώστες οθόνης για να μεταφέρουν νόημα σε χρήστες με προβλήματα όρασης.  

Το Aspose.Pdf εκθέτει ένα αντικείμενο `TaggedContent` που σας επιτρέπει να χτίσετε αυτό το δέντρο προγραμματιστικά. Σκεφτείτε το ως σετ LEGO: δημιουργείτε κομμάτια (επικεφαλίδα, παράγραφος) και τα συνδέετε στη σωστή σειρά.

### Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a page (add page to pdf)
            Document pdfDocument = new Document();
            Page pdfPage = pdfDocument.Pages.Add();

            // 2️⃣ Access the tagged content and create a level‑1 heading (add heading to pdf)
            TaggedContent taggedContent = pdfDocument.TaggedContent;
            HeadingElement heading = taggedContent.CreateHeadingElement(1);
            heading.Position = new Position { X = 50, Y = 750 }; // coordinates in points

            // 3️⃣ Create a paragraph and set its accessible text (set accessible text)
            ParagraphElement paragraph = taggedContent.CreateParagraphElement();
            paragraph.Text = "This is an accessible paragraph.";

            // 4️⃣ Build the hierarchy – heading contains the paragraph
            heading.AppendChild(paragraph);
            taggedContent.RootElement.AppendChild(heading);

            // 5️⃣ Save the tagged PDF to disk
            pdfDocument.Save("tagged_out.pdf");
        }
    }
}
```

Εκτελέστε το πρόγραμμα και ανοίξτε το `tagged_out.pdf` σε έναν αναγνώστη PDF που εμφανίζει ετικέτες (π.χ., Adobe Acrobat → View → Show/Hide → Navigation Panes → Tags). Θα πρέπει να δείτε μια **Heading 1** ακολουθούμενη από μια παράγραφο—ακριβώς όπως προοριζόμασταν.

Παρακάτω διασπάμε κάθε βήμα, εξηγούμε *γιατί* είναι σημαντικό, και προσθέτουμε μερικές επιπλέον επιλογές.

## Προσθήκη Σελίδας σε PDF

Ακόμη και ένα έγγραφο μίας σελίδας μπορεί να είναι tagged, αλλά τα περισσότερα πραγματικά PDFs χρειάζονται περισσότερο χώρο. Η προσθήκη μιας σελίδας είναι τετριμμένη:

```csharp
// Add a new page – this is the “add page to pdf” step
Page newPage = pdfDocument.Pages.Add();
```

> **Why add a page?**  
> Οι ετικέτες συνδέονται με συγκεκριμένες συντεταγμένες σελίδας. Αν προσπαθήσετε να τοποθετήσετε μια επικεφαλίδα σε συντεταγμένες Y που υπερβαίνουν το ύψος της σελίδας, το κείμενο θα κοπεί. Η προσθήκη μιας νέας σελίδας σας δίνει καθαρό καμβά και εξασφαλίζει ότι η διάταξή σας παραμένει συνεπής.

**Pro tip:** Αν χρειάζεστε οριζόντια σελίδα, ορίστε `newPage.PageInfo.Orientation = PageOrientation.Landscape;` πριν τοποθετήσετε τα στοιχεία.

## Προσθήκη Επικεφαλίδας σε PDF

Οι επικεφαλίδες δίνουν δομή. Στον παραπάνω κώδικα χρησιμοποιήσαμε το `CreateHeadingElement(1)` για να δημιουργήσουμε μια **Level‑1** επικεφαλίδα. Μπορείτε να δημιουργήσετε βαθύτερα επίπεδα (2, 3, …) για υποενότητες.

```csharp
HeadingElement heading = taggedContent.CreateHeadingElement(1);
heading.Position = new Position { X = 50, Y = 750 };
```

- **X** και **Y** μετρώνται σε points (1 pt = 1/72 in).  
- Προσαρμόστε το `Y` για να μετακινήσετε την επικεφαλίδα πάνω ή κάτω· χαμηλότερες τιμές την ωθούν προς το κάτω μέρος της σελίδας.

> **Common mistake:** Ξεχάσατε να ορίσετε το `heading.Position`. Χωρίς συντεταγμένες η επικεφαλίδα υπάρχει στο δέντρο ετικετών αλλά δεν εμφανίζεται στη σελίδα, αφήνοντας τους αναγνώστες οθόνης σε σύγχυση.

Αν χρειάζεστε έντονο στυλ, μπορείτε να προσθέσετε ένα `TextState`:

```csharp
heading.TextState = new TextState { FontSize = 18, FontStyle = FontStyles.Bold };
```

## Ορισμός Προσβάσιμου Κειμένου για Παράγραφο

Οι παράγραφοι περιέχουν το μεγαλύτερο μέρος του περιεχομένου σας. Για να είναι αναγνώσιμες από τις βοηθητικές τεχνολογίες, πρέπει να παρέχετε *accessible text*:

```csharp
ParagraphElement paragraph = taggedContent.CreateParagraphElement();
paragraph.Text = "This is an accessible paragraph.";
```

Η ιδιότητα `Text` είναι αυτό που θα αναγγείλει ένας αναγνώστης οθόνης. Μπορείτε επίσης να ενσωματώσετε χαρακτήρες Unicode, emojis ή ακόμη και δεξιά‑προς‑αριστερά σενάρια—το Aspose.Pdf τα διαχειρίζεται άψογα.

**Edge case:** Αν χρειάζεστε μια παράγραφο που περιέχει υπερσύνδεσμο, χρησιμοποιήστε `LinkElement` μέσα στην παράγραφο και ορίστε το χαρακτηριστικό `Alt` για μια περιγραφική ετικέτα.

## Αποθήκευση του Tagged PDF

```csharp
pdfDocument.Save("tagged_out.pdf");
```

Μπορείτε επίσης να μεταφέρετε το PDF απευθείας σε μια απάντηση web:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    pdfDocument.Save(ms);
    // return File(ms.ToArray(), "application/pdf", "report.pdf");
}
```

> **Why not `pdfDocument.Save("output.pdf")` alone?**  
> Επειδή όταν σκοπεύετε να σερβίρετε PDFs μέσω HTTP, η ροή αποφεύγει τη δημιουργία προσωρινών αρχείων στο δίσκο και μειώνει το φόρτο I/O.

## Επαλήθευση της Δομής Ετικετών (Προαιρετικό αλλά Συνιστώμενο)

Μετά τη δημιουργία του αρχείου, ανοίξτε το στο Adobe Acrobat:

1. **View → Show/Hide → Navigation Panes → Tags**  
2. Επεκτείνετε το δέντρο· θα πρέπει να δείτε `H1` (η επικεφαλίδα σας) με ένα παιδί `P` (η παράγραφος).  

Αν η ιεραρχία φαίνεται σωστή, έχετε δημιουργήσει επιτυχώς **create[d] tagged pdf** που πληροί τις απαιτήσεις WCAG 2.1 AA για προσβασιμότητα εγγράφων.

## Συνηθισμένες Παγίδες & Pro Tips

| Παγίδα | Πώς να Αποφύγετε |
|---------|--------------|
| Forgetting to call `AppendChild` on the root element | Always end with `taggedContent.RootElement.AppendChild(heading);` |
| Using coordinates outside page bounds | Use `pdfPage.PageInfo.Width/Height` to calculate safe ranges |
| Not setting `TextState` for readability | Define a default font size (12‑14 pt) and sufficient contrast |
| Over‑tagging (adding unnecessary elements) | Stick to semantic tags: heading, paragraph, list, table |
| Ignoring language metadata | Set `pdfDocument.Language = "en-US";` for better screen‑reader detection |

## Επόμενα Βήματα

- **Add more content types:** tables (`TableElement`), images (`ImageElement`), and lists (`ListElement`).  
- **Internationalization:** change `pdfDocument.Language` and supply Unicode text.  
- **Digital signatures:** secure your tagged PDF with `SignatureField`.  

Όλα αυτά βασίζονται στο θεμέλιο που έχετε τώρα για **create tagged pdf** αρχεία που είναι τόσο μηχανικά αναγνώσιμα όσο και φιλικά προς τον άνθρωπο.

---

### TL;DR

Τώρα γνωρίζετε πώς να **create tagged pdf** χρησιμοποιώντας το Aspose.Pdf, **add heading to pdf**, **set accessible text**, και **add page to pdf** όταν χρειάζεται. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω είναι έτοιμο να ενσωματωθεί σε οποιοδήποτε .NET project. Πειραματιστείτε με διαφορετικά επίπεδα επικεφαλίδας, γραμματοσειρές και επιπλέον ετικέτες—το επόμενο προσβάσιμο PDF σας είναι μόλις μερικές γραμμές μακριά. Καλή κωδικοποίηση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}