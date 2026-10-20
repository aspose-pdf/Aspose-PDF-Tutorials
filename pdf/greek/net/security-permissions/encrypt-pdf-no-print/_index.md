---
title: Κρυπτογράφηση PDF χωρίς δικαίωμα εκτύπωσης χρησιμοποιώντας Aspose.PDF for .NET
weight: 101
limit:
description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256 και να απενεργοποιήσετε την εκτύπωση χρησιμοποιώντας Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256 και να απενεργοποιήσετε
    την εκτύπωση χρησιμοποιώντας Aspose.PDF for .NET.
  headline: Κρυπτογράφηση PDF χωρίς δικαίωμα εκτύπωσης χρησιμοποιώντας Aspose.PDF
    for .NET
  type: TechArticle
- description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256 και να απενεργοποιήσετε
    την εκτύπωση χρησιμοποιώντας Aspose.PDF for .NET.
  name: Κρυπτογράφηση PDF χωρίς δικαίωμα εκτύπωσης χρησιμοποιώντας Aspose.PDF for
    .NET
  steps:
  - name: Ορίστε τη διαδρομή του πηγαίου PDF, το όνομα του εξαγόμενου προστατευμένου
      αρχείου και τους κωδικούς προβολής και ιδιοκτήτη.
    text: Ορίστε τη διαδρομή του πηγαίου PDF, το όνομα του εξαγόμενου προστατευμένου
      αρχείου και τους κωδικούς προβολής και ιδιοκτήτη.
  - name: Ελέγξτε αν το πηγαίο αρχείο υπάρχει και τερματίστε με μήνυμα σφάλματος εάν
      λείπει.
    text: Ελέγξτε αν το πηγαίο αρχείο υπάρχει και τερματίστε με μήνυμα σφάλματος εάν
      λείπει.
  - name: Ανοίξτε το αρχικό PDF, ορίστε κανένα δικαίωμα, κρυπτογραφήστε το με AES‑256
      χρησιμοποιώντας τους καθορισμένους κωδικούς και αποθηκεύστε το προστατευμένο
      αρχείο.
    text: Ανοίξτε το αρχικό PDF, ορίστε κανένα δικαίωμα, κρυπτογραφήστε το με AES‑256
      χρησιμοποιώντας τους καθορισμένους κωδικούς και αποθηκεύστε το προστατευμένο
      αρχείο.
  - name: Ανοίξτε ξανά το κρυπτογραφημένο PDF με τον κωδικό προβολής και γράψτε τη
      σημαία IsEncrypted στην κονσόλα για να επιβεβαιώσετε την προστασία.
    text: Ανοίξτε ξανά το κρυπτογραφημένο PDF με τον κωδικό προβολής και γράψτε τη
      σημαία IsEncrypted στην κονσόλα για να επιβεβαιώσετε την προστασία.
  - name: Εκτυπώστε ένα τελικό μήνυμα που να υποδεικνύει ότι η κρυπτογράφηση ολοκληρώθηκε
      και το όνομα του εξαγόμενου αρχείου.
    text: Εκτυπώστε ένα τελικό μήνυμα που να υποδεικνύει ότι η κρυπτογράφηση ολοκληρώθηκε
      και το όνομα του εξαγόμενου αρχείου.
  type: HowTo
- questions:
  - answer: '`Permissions` είναι μια enum σημαίας· η ανάθεση του `0` σημαίνει ότι
      δεν έχουν οριστεί bits δικαιωμάτων, έτσι το Aspose.Pdf δεν χορηγεί το δικαίωμα
      PrintDocument και ο προβολέας δεν μπορεί να εκτυπώσει το PDF.'
    question: Γιατί η ρύθμιση `Permissions rights = 0;` απενεργοποιεί την εκτύπωση;
  - answer: Ναι, αντικαταστήστε το `CryptoAlgorithm.AESx256` με `CryptoAlgorithm.AESx128`
      (ή άλλη υποστηριζόμενη τιμή enum) στην κλήση `pdfDoc.Encrypt`; το υπόλοιπο του
      κώδικα παραμένει αμετάβλητο.
    question: Μπορώ να χρησιμοποιήσω διαφορετικό αλγόριθμο κρυπτογράφησης, όπως AES‑128,
      με τον ίδιο κώδικα;
  - answer: Το Aspose.Pdf θα αποδεχτεί τα ίδια κωδικούς, αλλά ο κωδικός ιδιοκτήτη
      δεν θα παρέχει πλέον πρόσθετα προνόμια· το PDF θα παραμείνει κρυπτογραφημένο
      και τα δικαιώματα που καθορίσατε (κανένα) θα ισχύουν.
    question: Τι συμβαίνει αν ο κωδικός προβολής και ο κωδικός κύριος (ιδιοκτήτη)
      είναι οι ίδιοι;
  - answer: Ανοίξτε το προστατευμένο αρχείο με τον κωδικό προβολής (`new Document(securedFile,
      viewerPwd)`) και προσπαθήστε να εκτυπώσετε από έναν προβολέα PDF· επειδή δεν
      έχει οριστεί δικαίωμα `PrintDocument`, ο προβολέας θα απορρίψει την εντολή εκτύπωσης.
    question: Πώς μπορώ να επιβεβαιώσω ότι η εκτύπωση είναι πραγματικά αποκλεισμένη
      μετά την κρυπτογράφηση;
  - answer: Ο κώδικας ελέγχει το `File.Exists(sourceFile)` και γράφει σφάλμα στο `Console.Error`
      πριν επιστρέψει, αποτρέποντας το `FileNotFoundException` να ριχθεί από τον κατασκευαστή
      `Document`.
    question: Τι σφάλμα ρίχνεται αν το `original.pdf` δεν υπάρχει, και πώς πρέπει
      να το διαχειριστώ;
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Κρυπτογράφηση PDF και Αποκλεισμός Εκτύπωσης
og_description: Ασφαλίστε το PDF σας με κρυπτογράφηση AES‑256 και βεβαιωθείτε ότι δεν μπορεί να εκτυπωθεί—οδηγός βήμα‑βήμα.
og_image_alt: Στιγμιότυπο οθόνης που δείχνει κώδικα Aspose.PDF for .NET που κρυπτογραφεί ένα PDF και απενεργοποιεί την εκτύπωση.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Κρυπτογράφηση PDF χωρίς δικαίωμα εκτύπωσης χρησιμοποιώντας Aspose.PDF
Αυτό το σεμινάριο δείχνει πώς να ανοίξετε ένα υπάρχον PDF με Aspose.PDF for .NET, να εφαρμόσετε κρυπτογράφηση AES‑256 χωρίς να χορηγήσετε κανένα δικαίωμα—απενεργοποιώντας ουσιαστικά την εκτύπωση—να αποθηκεύσετε το ασφαλισμένο έγγραφο και να επιβεβαιώσετε την προστασία ανοίγοντάς το με τον κωδικό προβολής. Ακολουθήστε τον κώδικα βήμα‑βήμα για να διασφαλίσετε ότι το PDF σας δεν μπορεί να εκτυπωθεί μετά την κρυπτογράφηση.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Γιατί η ρύθμιση `Permissions rights = 0;` απενεργοποιεί την εκτύπωση;**  
A: `Permissions` είναι μια enum σημαίας· η ανάθεση του `0` σημαίνει ότι δεν έχουν οριστεί bits δικαιωμάτων, έτσι το Aspose.Pdf δεν χορηγεί το δικαίωμα PrintDocument και ο προβολέας δεν μπορεί να εκτυπώσει το PDF.

**Q: Μπορώ να χρησιμοποιήσω διαφορετικό αλγόριθμο κρυπτογράφησης, όπως AES‑128, με τον ίδιο κώδικα;**  
A: Ναι, αντικαταστήστε το `CryptoAlgorithm.AESx256` με `CryptoAlgorithm.AESx128` (ή άλλη υποστηριζόμενη τιμή enum) στην κλήση `pdfDoc.Encrypt`; το υπόλοιπο του κώδικα παραμένει αμετάβλητο.

**Q: Τι συμβαίνει αν ο κωδικός προβολής και ο κωδικός κύριος (ιδιοκτήτη) είναι οι ίδιοι;**  
A: Το Aspose.Pdf θα αποδεχτεί τα ίδια κωδικούς, αλλά ο κωδικός ιδιοκτήτη δεν θα παρέχει πλέον πρόσθετα προνόμια· το PDF θα παραμείνει κρυπτογραφημένο και τα δικαιώματα που καθορίσατε (κανένα) θα ισχύουν.

**Q: Πώς μπορώ να επιβεβαιώσω ότι η εκτύπωση είναι πραγματικά αποκλεισμένη μετά την κρυπτογράφηση;**  
A: Ανοίξτε το προστατευμένο αρχείο με τον κωδικό προβολής (`new Document(securedFile, viewerPwd)`) και προσπαθήστε να εκτυπώσετε από έναν προβολέα PDF· επειδή δεν έχει οριστεί δικαίωμα `PrintDocument`, ο προβολέας θα απορρίψει την εντολή εκτύπωσης.

**Q: Τι σφάλμα ρίχνεται αν το `original.pdf` δεν υπάρχει, και πώς πρέπει να το διαχειριστώ;**  
A: Ο κώδικας ελέγχει το `File.Exists(sourceFile)` και γράφει σφάλμα στο `Console.Error` πριν επιστρέψει, αποτρέποντας το `FileNotFoundException` να ριχθεί από τον κατασκευαστή `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}