---
title: Περιστροφή κάθε σελίδας PDF κατά 180° χρησιμοποιώντας το Aspose.Pdf for .NET
weight: 260
limit:
description: Οδηγός βήμα‑βήμα για την περιστροφή όλων των σελίδων ενός PDF κατά 180 μοίρες με το Aspose.Pdf for .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Οδηγός βήμα‑βήμα για την περιστροφή όλων των σελίδων ενός PDF κατά
    180 μοίρες με το Aspose.Pdf for .NET.
  headline: Περιστροφή κάθε σελίδας PDF κατά 180° χρησιμοποιώντας το Aspose.Pdf for
    .NET
  type: TechArticle
- description: Οδηγός βήμα‑βήμα για την περιστροφή όλων των σελίδων ενός PDF κατά
    180 μοίρες με το Aspose.Pdf for .NET.
  name: Περιστροφή κάθε σελίδας PDF κατά 180° χρησιμοποιώντας το Aspose.Pdf for .NET
  steps:
  - name: Δηλώστε τις διαδρομές αρχείων πηγής και προορισμού για το PDF.
    text: Δηλώστε τις διαδρομές αρχείων πηγής και προορισμού για το PDF.
  - name: Ελέγξτε αν το αρχείο πηγής υπάρχει και τερματίστε με μήνυμα σφάλματος αν
      δεν υπάρχει.
    text: Ελέγξτε αν το αρχείο πηγής υπάρχει και τερματίστε με μήνυμα σφάλματος αν
      δεν υπάρχει.
  - name: Δημιουργήστε ένα αντικείμενο Document για το PDF πηγής μέσα σε ένα μπλοκ
      using για τη διαχείριση πόρων.
    text: Δημιουργήστε ένα αντικείμενο Document για το PDF πηγής μέσα σε ένα μπλοκ
      using για τη διαχείριση πόρων.
  - name: Επανάληψη σε κάθε Page στο pdfDoc.Pages και ορίστε την ιδιότητα Rotate σε
      Rotation.on180, κάνοντας κάθε σελίδα ανάποδη.
    text: Επανάληψη σε κάθε Page στο pdfDoc.Pages και ορίστε την ιδιότητα Rotate σε
      Rotation.on180, κάνοντας κάθε σελίδα ανάποδη.
  - name: Αποθηκεύστε το τροποποιημένο Document στο αρχείο προορισμού, διατηρώντας
      τις περιστροφές.
    text: Αποθηκεύστε το τροποποιημένο Document στο αρχείο προορισμού, διατηρώντας
      τις περιστροφές.
  - name: Γράψτε ένα μήνυμα επιβεβαίωσης στην κονσόλα που να υποδεικνύει ότι η λειτουργία
      ολοκληρώθηκε.
    text: Γράψτε ένα μήνυμα επιβεβαίωσης στην κονσόλα που να υποδεικνύει ότι η λειτουργία
      ολοκληρώθηκε.
  type: HowTo
- questions:
  - answer: Ο κώδικας ελέγχει `File.Exists(sourceFile)` και γράφει ένα σφάλμα στο
      `Console.Error` πριν επιστρέψει, έτσι δεν ρίχνεται εξαίρεση και το πρόγραμμα
      τερματίζει ομαλά.
    question: Τι συμβαίνει αν το αρχείο PDF πηγής δεν υπάρχει;
  - answer: Ναι, αντικαταστήστε το `Rotation.on180` με άλλη τιμή enum όπως `Rotation.on90`
      (δεξιόστροφα) ή `Rotation.on270` (αριστερόστροφα) για να εφαρμόσετε διαφορετική
      περιστροφή.
    question: Μπορώ να περιστρέψω τις σελίδες με διαφορετική γωνία, π.χ., 90° δεξιόστροφα;
  - answer: Η συλλογή `Pages` του Aspose.Pdf είναι 1‑βάση, αλλά ο iterator `foreach`
      το αφαιρεί, επαναλαμβάνοντας κάθε αντικείμενο `Page` ανεξάρτητα από το υποκείμενο
      ευρετήριο.
    question: Η συλλογή σελίδων είναι μηδενική βάση; Πώς λειτουργεί ο βρόχος `foreach`;
  - answer: Η κλήση `pdfDoc.Save(destinationFile)` θα αντικαταστήσει οποιοδήποτε υπάρχον
      αρχείο με αυτό το όνομα, οπότε χρησιμοποιήστε διαφορετικό όνομα αρχείου ή δημιουργήστε
      αντίγραφο ασφαλείας του αρχικού αν χρειάζεται να το διατηρήσετε.
    question: Θα αντικατασταθεί το αρχικό PDF αν χρησιμοποιήσω το ίδιο όνομα αρχείου
      για το `destinationFile`;
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Περιστροφή κάθε σελίδας PDF κατά 180°
og_description: Μάθετε πώς να αναποδογυρίσετε όλες τις σελίδες ενός PDF ανάποδα με λίγες μόνο γραμμές κώδικα C#.
og_image_alt: Οδηγός που δείχνει πώς να περιστρέψετε κάθε σελίδα ενός PDF κατά 180 μοίρες χρησιμοποιώντας το Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Περιστροφή κάθε σελίδας PDF κατά 180° χρησιμοποιώντας το Aspose.Pdf
Αυτό το σεμινάριο δείχνει πώς να περιστρέψετε κάθε σελίδα ενός υπάρχοντος εγγράφου PDF κατά 180 μοίρες με την κλάση Aspose.Pdf Document. Εφαρμόζοντας μια πλήρη περιστροφή σελίδας, μπορείτε γρήγορα να διορθώσετε σάρωση ανάποδα ή να επαναπροσανατολίσετε έγγραφα χωρίς να τα δημιουργήσετε ξανά. Το παράδειγμα είναι γραμμένο σε C# και λειτουργεί στην πλατφόρμα .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Τι συμβαίνει αν το αρχείο PDF πηγής δεν υπάρχει;**  
A: Ο κώδικας ελέγχει `File.Exists(sourceFile)` και γράφει ένα σφάλμα στο `Console.Error` πριν επιστρέψει, έτσι δεν ρίχνεται εξαίρεση και το πρόγραμμα τερματίζει ομαλά.

**Q: Μπορώ να περιστρέψω τις σελίδες με διαφορετική γωνία, π.χ., 90° δεξιόστροφα;**  
A: Ναι, αντικαταστήστε το `Rotation.on180` με άλλη τιμή enum όπως `Rotation.on90` (δεξιόστροφα) ή `Rotation.on270` (αριστερόστροφα) για να εφαρμόσετε διαφορετική περιστροφή.

**Q: Η συλλογή σελίδων είναι μηδενική βάση; Πώς λειτουργεί ο βρόχος `foreach`;**  
A: Η συλλογή `Pages` του Aspose.Pdf είναι 1‑βάση, αλλά ο iterator `foreach` το αφαιρεί, επαναλαμβάνοντας κάθε αντικείμενο `Page` ανεξάρτητα από το υποκείμενο ευρετήριο.

**Q: Θα αντικατασταθεί το αρχικό PDF αν χρησιμοποιήσω το ίδιο όνομα αρχείου για το `destinationFile`;**  
A: Η κλήση `pdfDoc.Save(destinationFile)` θα αντικαταστήσει οποιοδήποτε υπάρχον αρχείο με αυτό το όνομα, οπότε χρησιμοποιήστε διαφορετικό όνομα αρχείου ή δημιουργήστε αντίγραφο ασφαλείας του αρχικού αν χρειάζεται να το διατηρήσετε.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}