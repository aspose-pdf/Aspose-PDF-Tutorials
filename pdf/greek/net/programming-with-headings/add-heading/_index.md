---
title: Προσθήκη Επικεφαλίδας, Γλώσσας και Τίτλου σε PDF χρησιμοποιώντας το Aspose.PDF for .NET
weight: 110
limit:
description: Δημιουργήστε ένα PDF, ορίστε τη γλώσσα και τον τίτλο του, και προσθέστε μια επικεφαλίδα επιπέδου‑1 με το Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Δημιουργήστε ένα PDF, ορίστε τη γλώσσα και τον τίτλο του, και προσθέστε
    μια επικεφαλίδα επιπέδου‑1 με το Aspose.PDF for .NET.
  headline: Προσθήκη Επικεφαλίδας, Γλώσσας και Τίτλου σε PDF χρησιμοποιώντας το Aspose.PDF
    for .NET
  type: TechArticle
- description: Δημιουργήστε ένα PDF, ορίστε τη γλώσσα και τον τίτλο του, και προσθέστε
    μια επικεφαλίδα επιπέδου‑1 με το Aspose.PDF for .NET.
  name: Προσθήκη Επικεφαλίδας, Γλώσσας και Τίτλου σε PDF χρησιμοποιώντας το Aspose.PDF
    for .NET
  steps:
  - name: Ορίστε το όνομα του αρχείου εξόδου για το παραγόμενο PDF.
    text: Ορίστε το όνομα του αρχείου εξόδου για το παραγόμενο PDF.
  - name: Δημιουργήστε ένα νέο κενό στιγμιότυπο εγγράφου PDF (`pdfDoc`) μέσα σε ένα
      μπλοκ `using`.
    text: Δημιουργήστε ένα νέο κενό στιγμιότυπο εγγράφου PDF (`pdfDoc`) μέσα σε ένα
      μπλοκ `using`.
  - name: Αποκτήστε τη διεπαφή `ITaggedContent` για εργασία με δομές PDF με ετικέτες.
    text: Αποκτήστε τη διεπαφή `ITaggedContent` για εργασία με δομές PDF με ετικέτες.
  - name: Ορίστε τη προεπιλεγμένη γλώσσα του εγγράφου σε English (US) και εκχωρήστε
      μεταδεδομένα τίτλου.
    text: Ορίστε τη προεπιλεγμένη γλώσσα του εγγράφου σε English (US) και εκχωρήστε
      μεταδεδομένα τίτλου.
  - name: Ανακτήστε το στοιχείο ρίζας του δέντρου λογικής δομής.
    text: Ανακτήστε το στοιχείο ρίζας του δέντρου λογικής δομής.
  - name: Δημιουργήστε ένα στοιχείο επικεφαλίδας επιπέδου‑1, ορίστε το εμφανιζόμενο
      κείμενό του και καθορίστε τη γλώσσα του.
    text: Δημιουργήστε ένα στοιχείο επικεφαλίδας επιπέδου‑1, ορίστε το εμφανιζόμενο
      κείμενό του και καθορίστε τη γλώσσα του.
  - name: Προσθέστε το στοιχείο επικεφαλίδας στη ρίζα, ώστε η επικεφαλίδα να εμφανιστεί
      στο PDF.
    text: Προσθέστε το στοιχείο επικεφαλίδας στη ρίζα, ώστε η επικεφαλίδα να εμφανιστεί
      στο PDF.
  - name: Αποθηκεύστε το PDF στο καθορισμένο αρχείο και κλείστε το πεδίο του εγγράφου.
    text: Αποθηκεύστε το PDF στο καθορισμένο αρχείο και κλείστε το πεδίο του εγγράφου.
  - name: Εκτυπώστε ένα μήνυμα επιβεβαίωσης στην κονσόλα.
    text: Εκτυπώστε ένα μήνυμα επιβεβαίωσης στην κονσόλα.
  type: HowTo
- questions:
  - answer: '`SetLanguage` ορίζει τη προεπιλεγμένη γλώσσα για ολόκληρη τη λογική δομή
      του εγγράφου· οποιοδήποτε στοιχείο που δεν έχει ορισμένη τη δική του γλώσσα
      θα κληρονομήσει το "en-US".'
    question: Ποιο είναι το αποτέλεσμα της κλήσης `tagContent.SetLanguage("en-US")`
      στο PDF;
  - answer: Η ρύθμιση του `header.Language` είναι προαιρετική· η επικεφαλίδα θα κληρονομήσει
      τη προεπιλεγμένη γλώσσα του εγγράφου εκτός αν ορίσετε διαφορετική τιμή, όπως
      φαίνεται στο παράδειγμα.
    question: Χρειάζεται να ορίσω το `header.Language` αν έχω ήδη καλέσει το `SetLanguage`
      στο έγγραφο;
  - answer: Χρησιμοποιήστε το `tagContent.CreateHeaderElement(2)` για να δημιουργήσετε
      μια επικεφαλίδα επιπέδου‑2· το αριθμητικό όρισμα καθορίζει το επίπεδο της επικεφαλίδας
      που θα αντικατοπτρίζεται στο δέντρο δομής του PDF.
    question: Πώς μπορώ να δημιουργήσω μια επικεφαλίδα επιπέδου‑2 αντί για επικεφαλίδα
      επιπέδου‑1;
  - answer: '`SetTitle` γράφει τη δοθείσα συμβολοσειρά στο πεδίο τίτλου των μεταδεδομένων
      του εγγράφου PDF, το οποίο μπορεί να προβληθεί σε αναγνώστες PDF και να χρησιμοποιηθεί
      για αναζήτηση ή ευρετηρίαση.'
    question: Τι κάνει η `tagContent.SetTitle("PDF Example with Header")`;
  - answer: Το στοιχείο επικεφαλίδας δεν θα προστεθεί στο δέντρο λογικής δομής, επομένως
      δεν θα εμφανιστεί στην έξοδο του PDF ούτε θα αναγνωριστεί ως επικεφαλίδα από
      εργαλεία προσβασιμότητας.
    question: Τι συμβαίνει αν παραλείψω το `rootElement.AppendChild(header)`;
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Εισαγωγή Επικεφαλίδας και Ορισμός Γλώσσας σε PDF
og_description: Μάθετε να δημιουργείτε ένα PDF, να ορίζετε τη γλώσσα και τον τίτλο του, και στη συνέχεια να προσθέτετε μια επικεφαλίδα επιπέδου‑1 με λίγες γραμμές κώδικα .NET.
og_image_alt: Οδηγός που δείχνει πώς να προσθέσετε μια επικεφαλίδα, να ορίσετε τη γλώσσα και τον τίτλο σε PDF χρησιμοποιώντας το Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Επικεφαλίδας, Γλώσσας και Τίτλου σε PDF χρησιμοποιώντας το Aspose.PDF
Αυτό το σεμινάριο σας καθοδηγεί στη δημιουργία ενός νέου εγγράφου PDF με το Aspose.PDF for .NET, στην ανάθεση προεπιλεγμένης γλώσσας και τίτλου εγγράφου, και στην εισαγωγή μιας επικεφαλίδας επιπέδου‑1. Θα δείτε πώς να εργάζεστε με τις κλάσεις Document, ITaggedContent, StructureElement και HeaderElement για να παραγάγετε ένα σωστά ετικετοποιημένο PDF κατάλληλο για εργαλεία προσβασιμότητας.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


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

**Q: Ποιο είναι το αποτέλεσμα της κλήσης `tagContent.SetLanguage("en-US")` στο PDF;**  
A: `SetLanguage` ορίζει τη προεπιλεγμένη γλώσσα για ολόκληρη τη λογική δομή του εγγράφου· οποιοδήποτε στοιχείο που δεν έχει ορισμένη τη δική του γλώσσα θα κληρονομήσει το "en-US".

**Q: Χρειάζεται να ορίσω το `header.Language` αν έχω ήδη καλέσει το `SetLanguage` στο έγγραφο;**  
A: Η ρύθμιση του `header.Language` είναι προαιρετική· η επικεφαλίδα θα κληρονομήσει τη προεπιλεγμένη γλώσσα του εγγράφου εκτός αν ορίσετε διαφορετική τιμή, όπως φαίνεται στο παράδειγμα.

**Q: Πώς μπορώ να δημιουργήσω μια επικεφαλίδα επιπέδου‑2 αντί για επικεφαλίδα επιπέδου‑1;**  
A: Χρησιμοποιήστε το `tagContent.CreateHeaderElement(2)` για να δημιουργήσετε μια επικεφαλίδα επιπέδου‑2· το αριθμητικό όρισμα καθορίζει το επίπεδο της επικεφαλίδας που θα αντικατοπτρίζεται στο δέντρο δομής του PDF.

**Q: Τι κάνει η `tagContent.SetTitle("PDF Example with Header")`;**  
A: `SetTitle` γράφει τη δοθείσα συμβολοσειρά στο πεδίο τίτλου των μεταδεδομένων του εγγράφου PDF, το οποίο μπορεί να προβληθεί σε αναγνώστες PDF και να χρησιμοποιηθεί για αναζήτηση ή ευρετηρίαση.

**Q: Τι συμβαίνει αν παραλείψω το `rootElement.AppendChild(header)`;**  
A: Το στοιχείο επικεφαλίδας δεν θα προστεθεί στο δέντρο λογικής δομής, επομένως δεν θα εμφανιστεί στην έξοδο του PDF ούτε θα αναγνωριστεί ως επικεφαλίδα από εργαλεία προσβασιμότητας.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}