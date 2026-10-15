---
title: Σύγκριση PDF Πλάι‑πλάι με Εξαίρεση Σχολίων με Aspose.Pdf for .NET
weight: 101
limit:
description: Οδηγός βήμα‑βήμα για τη σύγκριση PDF και την εξαίρεση περιοχών σχολίων χρησιμοποιώντας το Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Οδηγός βήμα‑βήμα για τη σύγκριση PDF και την εξαίρεση περιοχών σχολίων
    χρησιμοποιώντας το Aspose.Pdf for .NET.
  headline: Σύγκριση PDF Πλάι‑πλάι με Εξαίρεση Σχολίων με Aspose.Pdf for .NET
  type: TechArticle
- description: Οδηγός βήμα‑βήμα για τη σύγκριση PDF και την εξαίρεση περιοχών σχολίων
    χρησιμοποιώντας το Aspose.Pdf for .NET.
  name: Σύγκριση PDF Πλάι‑πλάι με Εξαίρεση Σχολίων με Aspose.Pdf for .NET
  steps:
  - name: Ορίστε τις διαδρομές αρχείων για το κύριο PDF, το δευτερεύον PDF και το
      PDF diff εξόδου.
    text: Ορίστε τις διαδρομές αρχείων για το κύριο PDF, το δευτερεύον PDF και το
      PDF diff εξόδου.
  - name: Ελέγξτε ότι και τα δύο αρχεία PDF εισόδου υπάρχουν και τερματίστε με μήνυμα
      σφάλματος εάν κάποιο λείπει.
    text: Ελέγξτε ότι και τα δύο αρχεία PDF εισόδου υπάρχουν και τερματίστε με μήνυμα
      σφάλματος εάν κάποιο λείπει.
  - name: Ανοίξτε τα δύο αρχεία PDF ως αντικείμενα Document (pdfA και pdfB) μέσα σε
      ένα using block ώστε να διαγραφούν αυτόματα.
    text: Ανοίξτε τα δύο αρχεία PDF ως αντικείμενα Document (pdfA και pdfB) μέσα σε
      ένα using block ώστε να διαγραφούν αυτόματα.
  - name: Συλλέξτε τα ορθογώνια περιορισμού κάθε σχολίου στο pdfA και αποθηκεύστε
      τα στο ignoredRectsA.
    text: Συλλέξτε τα ορθογώνια περιορισμού κάθε σχολίου στο pdfA και αποθηκεύστε
      τα στο ignoredRectsA.
  - name: Συλλέξτε τα ορθογώνια περιορισμού κάθε σχολίου στο pdfB και αποθηκεύστε
      τα στο ignoredRectsB.
    text: Συλλέξτε τα ορθογώνια περιορισμού κάθε σχολίου στο pdfB και αποθηκεύστε
      τα στο ignoredRectsB.
  - name: Δημιουργήστε ένα αντικείμενο SideBySideComparisonOptions και εκχωρήστε τα
      προηγουμένως συλλεγμένα ορθογώνια σχολίων στα ExcludeAreas1 και ExcludeAreas2
      ώστε αυτές οι περιοχές να αγνοούνται κατά τη σύγκριση.
    text: Δημιουργήστε ένα αντικείμενο SideBySideComparisonOptions και εκχωρήστε τα
      προηγουμένως συλλεγμένα ορθογώνια σχολίων στα ExcludeAreas1 και ExcludeAreas2
      ώστε αυτές οι περιοχές να αγνοούνται κατά τη σύγκριση.
  - name: Εκτελέστε τη σύγκριση PDF πλάι‑πλάι χρησιμοποιώντας τα δύο αντικείμενα Document
      και τις ρυθμισμένες επιλογές, γράφοντας το αποτέλεσμα στο outputPdf.
    text: Εκτελέστε τη σύγκριση PDF πλάι‑πλάι χρησιμοποιώντας τα δύο αντικείμενα Document
      και τις ρυθμισμένες επιλογές, γράφοντας το αποτέλεσμα στο outputPdf.
  - name: Καταργήστε τα αντικείμενα Document και βγείτε από το using block.
    text: Καταργήστε τα αντικείμενα Document και βγείτε από το using block.
  - name: Εκτυπώστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει ότι η σύγκριση ολοκληρώθηκε
      και πού αποθηκεύτηκε το diff PDF.
    text: Εκτυπώστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει ότι η σύγκριση ολοκληρώθηκε
      και πού αποθηκεύτηκε το diff PDF.
  type: HowTo
- questions:
  - answer: Ναι. Ο κώδικας απλώς δεν προσθέτει κανένα ορθογώνιο στη σχετική λίστα
      `ignoredRects`, έτσι τα `ExcludeAreas1`/`ExcludeAreas2` λαμβάνουν έναν κενό
      πίνακα και ο συγκριτής επεξεργάζεται ολόκληρη τη σελίδα.
    question: Τι συμβαίνει αν μια σελίδα PDF δεν έχει σχόλια – θα λειτουργήσει ακόμη
      η σύγκριση;
  - answer: Ορίστε το `ExcludeAreas1` (ή `ExcludeAreas2`) στα συλλεγμένα ορθογώνια
      και αφήστε την άλλη ιδιότητα ως κενό πίνακα· ο συγκριτής θα αγνοήσει περιοχές
      μόνο στο καθορισμένο έγγραφο.
    question: Μπορώ να εξαιρέσω μόνο τα σχόλια από ένα έγγραφο ενώ διατηρώ τα σχόλια
      του άλλου στο diff;
  - answer: Τα επικαλυπτόμενα ορθογώνια συγχωνεύονται εσωτερικά από τον συγκριτή,
      έτσι τα επικαλυπτόμενα όρια σχολίων εξαιρούνται με ασφάλεια χωρίς διπλή καταμέτρηση.
    question: Προκαλούν τα επικαλυπτόμενα ορθογώνια σχολίων προβλήματα με το `ExcludeAreas`;
  - answer: Ναι, ορίστε `compareOpts.ExcludeTables = true;` – αυτή η σημαία λειτουργεί
      μαζί με τα `ExcludeAreas1`/`ExcludeAreas2` για να εξαιρούν επίσης περιοχές πινάκων.
    question: Υπάρχει τρόπος να εξαιρεθούν πίνακες εκτός από σχόλια χρησιμοποιώντας
      το ίδιο αντικείμενο επιλογών;
  - answer: Ο κώδικας ελέγχει `if (a != null && a.Rect != null)` πριν την προσθήκη
      στη λίστα, έτσι τα null ορθογώνια απλώς παραλείπονται και δεν πετιέται εξαίρεση.
    question: Τι γίνεται αν η ιδιότητα `Rect` ενός σχολίου είναι null – θα πετάξει
      ο κώδικας εξαίρεση;
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Σύγκριση PDF χωρίς Σχόλια
og_description: Εκτελέστε ένα diff PDF πλάι‑πλάι που παραλείπει όλα τα σημάδια σχολίων.
og_image_alt: Οδηγός που δείχνει μια σύγκριση PDF πλάι‑πλάι που εξαιρεί περιοχές σχολίων χρησιμοποιώντας το Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Σύγκριση PDF Πλάι‑πλάι με Εξαίρεση Σχολίων με Aspose.Pdf
Αυτό το σεμινάριο δείχνει πώς να συγκρίνετε δύο αρχεία PDF χρησιμοποιώντας το Aspose.Pdf for .NET ενώ αγνοείτε οποιοδήποτε περιεχόμενο σχολίων. Εξάγει τα πλαίσια περιορισμού όλων των σχολίων από κάθε έγγραφο, τα περνά στο SideBySideComparisonOptions και στη συνέχεια εκτελεί μια σύγκριση πλάι‑πλάι. Το αποτέλεσμα είναι ένα diff PDF που επισημαίνει μόνο τις αλλαγές χωρίς σχόλια.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Τι συμβαίνει αν μια σελίδα PDF δεν έχει σχόλια – θα λειτουργήσει ακόμη η σύγκριση;**  
A: Ναι. Ο κώδικας απλώς δεν προσθέτει κανένα ορθογώνιο στη σχετική λίστα `ignoredRects`, έτσι τα `ExcludeAreas1`/`ExcludeAreas2` λαμβάνουν έναν κενό πίνακα και ο συγκριτής επεξεργάζεται ολόκληρη τη σελίδα.

**Q: Μπορώ να εξαιρέσω μόνο τα σχόλια από ένα έγγραφο ενώ διατηρώ τα σχόλια του άλλου στο diff;**  
A: Ορίστε το `ExcludeAreas1` (ή `ExcludeAreas2`) στα συλλεγμένα ορθογώνια και αφήστε την άλλη ιδιότητα ως κενό πίνακα· ο συγκριτής θα αγνοήσει περιοχές μόνο στο καθορισμένο έγγραφο.

**Q: Προκαλούν τα επικαλυπτόμενα ορθογώνια σχολίων προβλήματα με το `ExcludeAreas`;**  
A: Τα επικαλυπτόμενα ορθογώνια συγχωνεύονται εσωτερικά από τον συγκριτή, έτσι τα επικαλυπτόμενα όρια σχολίων εξαιρούνται με ασφάλεια χωρίς διπλή καταμέτρηση.

**Q: Υπάρχει τρόπος να εξαιρεθούν πίνακες εκτός από σχόλια χρησιμοποιώντας το ίδιο αντικείμενο επιλογών;**  
A: Ναι, ορίστε `compareOpts.ExcludeTables = true;` – αυτή η σημαία λειτουργεί μαζί με τα `ExcludeAreas1`/`ExcludeAreas2` για να εξαιρούν επίσης περιοχές πινάκων.

**Q: Τι γίνεται αν η ιδιότητα `Rect` ενός σχολίου είναι null – θα πετάξει ο κώδικας εξαίρεση;**  
A: Ο κώδικας ελέγχει `if (a != null && a.Rect != null)` πριν την προσθήκη στη λίστα, έτσι τα null ορθογώνια απλώς παραλείπονται και δεν πετιέται εξαίρεση.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}