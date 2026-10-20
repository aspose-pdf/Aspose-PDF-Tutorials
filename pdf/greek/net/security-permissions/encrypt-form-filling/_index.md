---
title: Κρυπτογράφηση PDF μόνο για Συμπλήρωση Φορμών με AES‑256 χρησιμοποιώντας το Aspose.Pdf for .NET
weight: 201
limit:
description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256, να το περιορίσετε μόνο στη συμπλήρωση φορμών και να ορίσετε κωδικούς προβολής/ιδιοκτήτη χρησιμοποιώντας το Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, PDF encryption .NET, restrict PDF permissions, form filling permission PDF, AES-256 PDF encryption, set PDF passwords .NET]
url: /net/security-permissions/encrypt-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256, να το περιορίσετε
    μόνο στη συμπλήρωση φορμών και να ορίσετε κωδικούς προβολής/ιδιοκτήτη χρησιμοποιώντας
    το Aspose.Pdf for .NET.
  headline: Κρυπτογράφηση PDF μόνο για Συμπλήρωση Φορμών με AES‑256 χρησιμοποιώντας
    το Aspose.Pdf for .NET
  type: TechArticle
- description: Μάθετε πώς να κρυπτογραφήσετε ένα PDF με AES‑256, να το περιορίσετε
    μόνο στη συμπλήρωση φορμών και να ορίσετε κωδικούς προβολής/ιδιοκτήτη χρησιμοποιώντας
    το Aspose.Pdf for .NET.
  name: Κρυπτογράφηση PDF μόνο για Συμπλήρωση Φορμών με AES‑256 χρησιμοποιώντας το
    Aspose.Pdf for .NET
  steps:
  - name: Δηλώστε τη διαδρομή του πηγαίου PDF, τη διαδρομή εξόδου και τους κωδικούς
      προβολής και ιδιοκτήτη.
    text: Δηλώστε τη διαδρομή του πηγαίου PDF, τη διαδρομή εξόδου και τους κωδικούς
      προβολής και ιδιοκτήτη.
  - name: Ελέγξτε αν το πηγαίο αρχείο υπάρχει· αν δεν υπάρχει, γράψτε ένα μήνυμα σφάλματος
      και τερματίστε.
    text: Ελέγξτε αν το πηγαίο αρχείο υπάρχει· αν δεν υπάρχει, γράψτε ένα μήνυμα σφάλματος
      και τερματίστε.
  - name: Εισάγετε ένα μπλοκ try και ανοίξτε το έγγραφο PDF με μια δήλωση `using`,
      δημιουργώντας τη μεταβλητή `pdfDoc`.
    text: Εισάγετε ένα μπλοκ try και ανοίξτε το έγγραφο PDF με μια δήλωση `using`,
      δημιουργώντας τη μεταβλητή `pdfDoc`.
  - name: Δημιουργήστε ένα αντικείμενο `Permissions` που επιτρέπει μόνο τη συμπλήρωση
      φορμών.
    text: Δημιουργήστε ένα αντικείμενο `Permissions` που επιτρέπει μόνο τη συμπλήρωση
      φορμών.
  - name: Κρυπτογραφήστε το `pdfDoc` με τους κωδικούς προβολής και κύριου (master),
      εφαρμόζοντας το σύνολο δικαιωμάτων και χρησιμοποιώντας AES‑256.
    text: Κρυπτογραφήστε το `pdfDoc` με τους κωδικούς προβολής και κύριου (master),
      εφαρμόζοντας το σύνολο δικαιωμάτων και χρησιμοποιώντας AES‑256.
  - name: Αποθηκεύστε το κρυπτογραφημένο PDF στο καθορισμένο αρχείο εξόδου και κλείστε
      το μπλοκ `using`.
    text: Αποθηκεύστε το κρυπτογραφημένο PDF στο καθορισμένο αρχείο εξόδου και κλείστε
      το μπλοκ `using`.
  - name: Γράψτε ένα μήνυμα επιβεβαίωσης στην κονσόλα και κλείστε το μπλοκ try.
    text: Γράψτε ένα μήνυμα επιβεβαίωσης στην κονσόλα και κλείστε το μπλοκ try.
  - name: Πιάστε οποιαδήποτε εξαίρεση, εκτυπώστε το μήνυμά της στη ροή σφαλμάτων και
      κλείστε το μπλοκ catch.
    text: Πιάστε οποιαδήποτε εξαίρεση, εκτυπώστε το μήνυμά της στη ροή σφαλμάτων και
      κλείστε το μπλοκ catch.
  type: HowTo
- questions:
  - answer: '`Permissions.FillForm` επιτρέπει στους χρήστες να συμπληρώνουν διαδραστικά
      πεδία φόρμας, αλλά απενεργοποιεί όλες τις άλλες ενέργειες όπως εκτύπωση, εξαγωγή
      περιεχομένου ή τροποποίηση της δομής του εγγράφου.'
    question: Τι επιτρέπει και τι αποκλείει στην κρυπτογραφημένη PDF η σημαία `Permissions.FillForm`;
  - answer: Ναι, αντικαταστήστε το `CryptoAlgorithm.AESx256` με το `CryptoAlgorithm.AESx128`
      (ή άλλη υποστηριζόμενη τιμή enum) στη μέθοδο `pdfDoc.Encrypt` για να αλλάξετε
      την ισχύ της κρυπτογράφησης.
    question: Μπορώ να χρησιμοποιήσω διαφορετικό αλγόριθμο κρυπτογράφησης, όπως AES‑128,
      με την ίδια κλήση `Encrypt`;
  - answer: Ο κωδικός προβολής (`readPass`) απαιτείται για το άνοιγμα του PDF και
      την επιβολή των καθορισμένων δικαιωμάτων, ενώ ο κωδικός ιδιοκτήτη (`fullPass`)
      παρέχει πλήρη απεριόριστη πρόσβαση και μπορεί να χρησιμοποιηθεί για την αλλαγή
      δικαιωμάτων ή την αφαίρεση της κρυπτογράφησης.
    question: Ποια είναι η διαφορά μεταξύ του κωδικού προβολής (`viewerPwd`) και του
      κωδικού ιδιοκτήτη (`masterPwd`);
  - answer: Η χρήση του `Permissions.None` (ή η παράλειψη του ορίσματος) δημιουργεί
      ένα PDF χωρίς ειδικούς περιορισμούς, πράγμα που σημαίνει ότι ο κωδικός προβολής
      εξακολουθεί να προστατεύει το αρχείο, αλλά οι χρήστες μπορούν να εκτελούν όλες
      τις τυπικές ενέργειες όπως εκτύπωση και αντιγραφή.
    question: Αν παραλείψω το όρισμα `permissionSet` ή περάσω `Permissions.None`,
      ποια δικαιώματα θα έχει το PDF μετά την κρυπτογράφηση;
  type: FAQPage
images:
- /net/security-permissions/encrypt-form-filling/og-image.png
og_title: Κρυπτογράφηση PDF μόνο για Συμπλήρωση Φορμών με AES‑256
og_description: Ασφαλίστε το PDF σας ώστε οι χρήστες να μπορούν μόνο να συμπληρώνουν φόρμες, χρησιμοποιώντας κρυπτογράφηση AES‑256 και κωδικούς στο Aspose.Pdf for .NET.
og_image_alt: Στιγμιότυπο οθόνης που δείχνει τα βήματα για την κρυπτογράφηση ενός PDF και τον περιορισμό του στη συμπλήρωση φορμών χρησιμοποιώντας το Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Κρυπτογράφηση PDF μόνο για Συμπλήρωση Φορμών με AES‑256 χρησιμοποιώντας το Aspose.Pdf
Αυτό το σεμινάριο δείχνει πώς να προστατεύσετε ένα υπάρχον PDF ώστε οι χρήστες να μπορούν μόνο να συμπληρώνουν τις φόρμες του. Περιγράφει το άνοιγμα του εγγράφου με το Aspose.Pdf for .NET, τον περιορισμό των δικαιωμάτων στη συμπλήρωση φορμών, την εφαρμογή κρυπτογράφησης AES‑256, τον ορισμό κωδικών προβολής και ιδιοκτήτη, και τελικά την αποθήκευση του ασφαλισμένου αρχείου.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-form-filling" >}}


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

**Q: Τι επιτρέπει και τι αποκλείει στην κρυπτογραφημένη PDF η σημαία `Permissions.FillForm`;**  
A: `Permissions.FillForm` επιτρέπει στους χρήστες να συμπληρώνουν διαδραστικά πεδία φόρμας, αλλά απενεργοποιεί όλες τις άλλες ενέργειες όπως εκτύπωση, εξαγωγή περιεχομένου ή τροποποίηση της δομής του εγγράφου.

**Q: Μπορώ να χρησιμοποιήσω διαφορετικό αλγόριθμο κρυπτογράφησης, όπως AES‑128, με την ίδια κλήση `Encrypt`;**  
A: Ναι, αντικαταστήστε το `CryptoAlgorithm.AESx256` με το `CryptoAlgorithm.AESx128` (ή άλλη υποστηριζόμενη τιμή enum) στη μέθοδο `pdfDoc.Encrypt` για να αλλάξετε την ισχύ της κρυπτογράφησης.

**Q: Ποια είναι η διαφορά μεταξύ του κωδικού προβολής (`viewerPwd`) και του κωδικού ιδιοκτήτη (`masterPwd`);**  
A: Ο κωδικός προβολής (`readPass`) απαιτείται για το άνοιγμα του PDF και την επιβολή των καθορισμένων δικαιωμάτων, ενώ ο κωδικός ιδιοκτήτη (`fullPass`) παρέχει πλήρη απεριόριστη πρόσβαση και μπορεί να χρησιμοποιηθεί για την αλλαγή δικαιωμάτων ή την αφαίρεση της κρυπτογράφησης.

**Q: Αν παραλείψω το όρισμα `permissionSet` ή περάσω `Permissions.None`, ποια δικαιώματα θα έχει το PDF μετά την κρυπτογράφηση;**  
A: Η χρήση του `Permissions.None` (ή η παράλειψη του ορίσματος) δημιουργεί ένα PDF χωρίς ειδικούς περιορισμούς, πράγμα που σημαίνει ότι ο κωδικός προβολής εξακολουθεί να προστατεύει το αρχείο, αλλά οι χρήστες μπορούν να εκτελούν όλες τις τυπικές ενέργειες όπως εκτύπωση και αντιγραφή.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}