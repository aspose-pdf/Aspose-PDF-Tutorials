---
title: Προσθήκη Tagged External Link με Tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET
weight: 440
limit:
description: Μάθετε πώς να προσθέσετε έναν εξωτερικό υπερσύνδεσμο με ετικέτα, κείμενο εμφάνισης και tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Μάθετε πώς να προσθέσετε έναν εξωτερικό υπερσύνδεσμο με ετικέτα, κείμενο
    εμφάνισης και tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET.
  headline: Προσθήκη Tagged External Link με Tooltip σε PDF χρησιμοποιώντας Aspose.Pdf
    για .NET
  type: TechArticle
- description: Μάθετε πώς να προσθέσετε έναν εξωτερικό υπερσύνδεσμο με ετικέτα, κείμενο
    εμφάνισης και tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET.
  name: Προσθήκη Tagged External Link με Tooltip σε PDF χρησιμοποιώντας Aspose.Pdf
    για .NET
  steps:
  - name: Ορίστε τις διαδρομές για το πηγαίο PDF και το αρχείο αποτελέσματος.
    text: Ορίστε τις διαδρομές για το πηγαίο PDF και το αρχείο αποτελέσματος.
  - name: Ελέγξτε ότι το πηγαίο PDF υπάρχει και τερματίστε εάν δεν μπορεί να βρεθεί.
    text: Ελέγξτε ότι το πηγαίο PDF υπάρχει και τερματίστε εάν δεν μπορεί να βρεθεί.
  - name: Ανοίξτε το PDF έγγραφο μέσα σε ένα μπλοκ using για να εξασφαλίσετε σωστή
      απελευθέρωση.
    text: Ανοίξτε το PDF έγγραφο μέσα σε ένα μπλοκ using για να εξασφαλίσετε σωστή
      απελευθέρωση.
  - name: Αποκτήστε τον διαχειριστή tagged‑content για το ανοικτό έγγραφο.
    text: Αποκτήστε τον διαχειριστή tagged‑content για το ανοικτό έγγραφο.
  - name: Ορίστε τη γλώσσα του εγγράφου στα Αγγλικά (US) και δώστε στο PDF έναν τίτλο
      που προέρχεται από το όνομα του αρχείου.
    text: Ορίστε τη γλώσσα του εγγράφου στα Αγγλικά (US) και δώστε στο PDF έναν τίτλο
      που προέρχεται από το όνομα του αρχείου.
  - name: Ανακτήστε το στοιχείο ρίζας του δέντρου λογικής δομής στο οποίο θα προστεθούν
      νέα στοιχεία.
    text: Ανακτήστε το στοιχείο ρίζας του δέντρου λογικής δομής στο οποίο θα προστεθούν
      νέα στοιχεία.
  - name: Δημιουργήστε ένα στοιχείο συνδέσμου, ορίστε το κείμενο εμφάνισης, τη διεύθυνση
      URL προορισμού και τον τίτλο tooltip, και στη συνέχεια εισάγετέ το στη δομή
      του εγγράφου.
    text: Δημιουργήστε ένα στοιχείο συνδέσμου, ορίστε το κείμενο εμφάνισης, τη διεύθυνση
      URL προορισμού και τον τίτλο tooltip, και στη συνέχεια εισάγετέ το στη δομή
      του εγγράφου.
  - name: Αποθηκεύστε το ενημερωμένο PDF στο καθορισμένο αρχείο αποτελέσματος.
    text: Αποθηκεύστε το ενημερωμένο PDF στο καθορισμένο αρχείο αποτελέσματος.
  - name: Εμφανίστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει πού αποθηκεύτηκε το τροποποιημένο
      PDF.
    text: Εμφανίστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει πού αποθηκεύτηκε το τροποποιημένο
      PDF.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` επιστρέφει το υπάρχον περιεχόμενο με ετικέτες
      εάν το έγγραφο είναι ήδη ετικετοποιημένο· δεν δημιουργεί διπλό δέντρο.'
    question: Τι γίνεται αν το πηγαίο PDF είναι ήδη ετικετοποιημένο – θα δημιουργήσει
      το `pdfDoc.TaggedContent` νέο δέντρο ετικετών ή θα χρησιμοποιήσει το υπάρχον;
  - answer: Ναι – εντοπίστε το επιθυμητό `StructureElement` (π.χ., ένα `Div` ή `Paragraph`
      σε μια σελίδα) μέσω του δέντρου λογικής δομής και καλέστε `AppendChild(externalLink)`
      σε αυτό το στοιχείο.
    question: Μπορώ να τοποθετήσω τον υπερσύνδεσμο σε συγκεκριμένη σελίδα αντί να
      τον προσαρτήσω στο στοιχείο ρίζας;
  - answer: Το tooltip εμφανίζεται μόνο εάν το `externalLink.Title` οριστεί πριν από
      το `pdfDoc.Save`; η ρύθμιση του μετά την αποθήκευση δεν έχει καμία επίδραση
      στο ήδη‑γραμμένο PDF.
    question: Απαιτείται η ιδιότητα `Title` του `LinkElement` για να εμφανιστεί το
      tooltip, και μπορεί να οριστεί μετά την κλήση του `Save`;
  - answer: Αναθέστε ένα `FileSpecification` (π.χ., `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      στο `externalLink.Hyperlink` αντί να χρησιμοποιήσετε `WebHyperlink`.
    question: Πώς μπορώ να δημιουργήσω σύνδεσμο σε τοπικό αρχείο αντί για διεύθυνση
      web;
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Εισαγωγή Tagged External Link με Tooltip σε PDF
og_description: Ενσωματώστε έναν προσβάσιμο υπερσύνδεσμο με ορατό κείμενο και tooltip στο PDF σας χρησιμοποιώντας Aspose.Pdf για .NET.
og_image_alt: Οδηγός που δείχνει πώς να προσθέσετε έναν εξωτερικό υπερσύνδεσμο με ετικέτα και tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Tagged External Link με Tooltip σε PDF χρησιμοποιώντας Aspose.Pdf για .NET
Αυτό το εκπαιδευτικό υλικό δείχνει πώς να ανοίξετε ένα υπάρχον PDF με Aspose.Pdf για .NET, να δημιουργήσετε έναν εξωτερικό υπερσύνδεσμο με ετικέτα που περιλαμβάνει ορατό κείμενο εμφάνισης και τίτλο tooltip, να εισάγετε τον σύνδεσμο στη λογική δομή του εγγράφου και να αποθηκεύσετε το ενημερωμένο αρχείο. Ακολουθώντας τα βήματα, θα παραγάγετε ένα προσβάσιμο PDF όπου ο σύνδεσμος αποτελεί μέρος της ιεραρχίας ετικετών και παρέχει επιπλέον συμφραζόμενα στους αναγνώστες.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Τι γίνεται αν το πηγαίο PDF είναι ήδη ετικετοποιημένο – θα δημιουργήσει το `pdfDoc.TaggedContent` νέο δέντρο ετικετών ή θα χρησιμοποιήσει το υπάρχον;**  
A: `pdfDoc.TaggedContent` επιστρέφει το υπάρχον περιεχόμενο με ετικέτες εάν το έγγραφο είναι ήδη ετικετοποιημένο· δεν δημιουργεί διπλό δέντρο.

**Q: Μπορώ να τοποθετήσω τον υπερσύνδεσμο σε συγκεκριμένη σελίδα αντί να τον προσαρτήσω στο στοιχείο ρίζας;**  
A: Ναι – εντοπίστε το επιθυμητό `StructureElement` (π.χ., ένα `Div` ή `Paragraph` σε μια σελίδα) μέσω του δέντρου λογικής δομής και καλέστε `AppendChild(externalLink)` σε αυτό το στοιχείο.

**Q: Απαιτείται η ιδιότητα `Title` του `LinkElement` για να εμφανιστεί το tooltip, και μπορεί να οριστεί μετά την κλήση του `Save`;**  
A: Το tooltip εμφανίζεται μόνο εάν το `externalLink.Title` οριστεί πριν από το `pdfDoc.Save`; η ρύθμιση του μετά την αποθήκευση δεν έχει καμία επίδραση στο ήδη‑γραμμένο PDF.

**Q: Πώς μπορώ να δημιουργήσω σύνδεσμο σε τοπικό αρχείο αντί για διεύθυνση web;**  
A: Αναθέστε ένα `FileSpecification` (π.χ., `new FileSpecification("file:///C:/Docs/manual.pdf")`) στο `externalLink.Hyperlink` αντί να χρησιμοποιήσετε `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}