---
title: Περιστροφή μιας μόνο σελίδας PDF κατά 180 μοίρες με το Aspose.PDF for .NET
weight: 260
limit:
description: Μάθετε πώς να περιστρέψετε τη τρίτη σελίδα ενός PDF κατά 180° χρησιμοποιώντας το Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Μάθετε πώς να περιστρέψετε τη τρίτη σελίδα ενός PDF κατά 180° χρησιμοποιώντας
    το Aspose.PDF for .NET.
  headline: Περιστροφή μιας μόνο σελίδας PDF κατά 180 μοίρες με το Aspose.PDF for
    .NET
  type: TechArticle
- description: Μάθετε πώς να περιστρέψετε τη τρίτη σελίδα ενός PDF κατά 180° χρησιμοποιώντας
    το Aspose.PDF for .NET.
  name: Περιστροφή μιας μόνο σελίδας PDF κατά 180 μοίρες με το Aspose.PDF for .NET
  steps:
  - name: Το αρχείο περιέχει μόνο επεξηγηματικά σχόλια και κανέναν εκτελέσιμο κώδικα,
      λειτουργώντας ως σύμβολο κράτησης για το αρχικό παράδειγμα.
    text: Το αρχείο περιέχει μόνο επεξηγηματικά σχόλια και κανέναν εκτελέσιμο κώδικα,
      λειτουργώντας ως σύμβολο κράτησης για το αρχικό παράδειγμα.
  type: HowTo
- questions:
  - answer: Χρησιμοποιήστε τη συλλογή σελίδων του SDK με μηδενική αρίθμηση, π.χ.,
      `pdfDocument.Pages[2]`, επειδή ο δείκτης 2 αντιστοιχεί στην τρίτη σελίδα.
    question: Πώς μπορώ να στοχεύσω τη τρίτη σελίδα του PDF για περιστροφή;
  - answer: Η ιδιότητα rotation δέχεται μόνο τις τέσσερις τυπικές τιμές 0, 90, 180
      και 270 μοίρες· οποιαδήποτε άλλη τιμή στρογγυλοποιείται στην πλησιέστερη επιτρεπτή
      γωνία.
    question: Μπορώ να περιστρέψω μια σελίδα με γωνία διαφορετική από 180 μοίρες;
  - answer: Η περιστροφή εφαρμόζεται μόνο στο ενσωματωμένο στη μνήμη `PdfDocument`;
      πρέπει να καλέσετε `pdfDocument.Save("output.pdf")` (ή μια παρόμοια μέθοδο αποθήκευσης)
      για να γράψετε τις αλλαγές σε νέο αρχείο, αφήνοντας το πηγαίο αμετάβλητο.
    question: Η περιστροφή της σελίδας τροποποιεί αυτόματα το αρχικό αρχείο;
  - answer: Το SDK επαναϋπολογίζει αυτόματα τις θέσεις των σημειώσεων και των πεδίων
      φόρμας ώστε να παραμένουν σωστά ευθυγραμμισμένα με τη νέα προσανατολισμό.
    question: Τι συμβαίνει με τις σημειώσεις ή τα πεδία φόρμας μετά την περιστροφή
      της σελίδας;
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Περιστροφή σελίδας PDF κατά 180° με το Aspose.PDF
og_description: Αναστρέψτε γρήγορα τη τρίτη σελίδα του PDF σας ανάποδα με μερικές γραμμές κώδικα Aspose.PDF for .NET.
og_image_alt: Οδηγός που δείχνει κώδικα που περιστρέφει τη τρίτη σελίδα ενός PDF κατά 180 μοίρες χρησιμοποιώντας το Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Περιστροφή μιας μόνο σελίδας PDF κατά 180 μοίρες με το Aspose.PDF
Σε αυτό το σεμινάριο θα μάθετε πώς να περιστρέψετε τη τρίτη σελίδα ενός εγγράφου PDF κατά 180 μοίρες χρησιμοποιώντας το Aspose.PDF for .NET. Το παράδειγμα περιγράφει τη φόρτωση ενός PDF, την επιλογή της σελίδας 3, την εφαρμογή της περιστροφής και την αποθήκευση του ενημερωμένου αρχείου. Αυτή η προσέγγιση σας επιτρέπει να αναστρέψετε μια συγκεκριμένη σελίδα χωρίς να αλλάξετε τον προσανατολισμό των υπόλοιπων σελίδων.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Πώς μπορώ να στοχεύσω τη τρίτη σελίδα του PDF για περιστροφή;**  
A: Χρησιμοποιήστε τη συλλογή σελίδων του SDK με μηδενική αρίθμηση, π.χ., `pdfDocument.Pages[2]`, επειδή ο δείκτης 2 αντιστοιχεί στην τρίτη σελίδα.

**Q: Μπορώ να περιστρέψω μια σελίδα με γωνία διαφορετική από 180 μοίρες;**  
A: Η ιδιότητα rotation δέχεται μόνο τις τέσσερις τυπικές τιμές 0, 90, 180 και 270 μοίρες· οποιαδήποτε άλλη τιμή στρογγυλοποιείται στην πλησιέστερη επιτρεπτή γωνία.

**Q: Η περιστροφή της σελίδας τροποποιεί αυτόματα το αρχικό αρχείο;**  
A: Η περιστροφή εφαρμόζεται μόνο στο ενσωματωμένο στη μνήμη `PdfDocument`; πρέπει να καλέσετε `pdfDocument.Save("output.pdf")` (ή μια παρόμοια μέθοδο αποθήκευσης) για να γράψετε τις αλλαγές σε νέο αρχείο, αφήνοντας το πηγαίο αμετάβλητο.

**Q: Τι συμβαίνει με τις σημειώσεις ή τα πεδία φόρμας μετά την περιστροφή της σελίδας;**  
A: Το SDK επαναϋπολογίζει αυτόματα τις θέσεις των σημειώσεων και των πεδίων φόρμας ώστε να παραμένουν σωστά ευθυγραμμισμένα με τη νέα προσανατολισμό.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}