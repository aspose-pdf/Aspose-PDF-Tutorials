---
title: Σύγκριση PDF ενώ αγνοούνται συγκεκριμένες περιοχές με χρήση του Aspose.Pdf για .NET
weight: 201
limit:
description: Μάθετε να συγκρίνετε PDF πλάι-πλάι και να αγνοείτε επιλεγμένες περιοχές χρησιμοποιώντας το Aspose.Pdf για .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Μάθετε να συγκρίνετε PDF πλάι-πλάι και να αγνοείτε επιλεγμένες περιοχές
    χρησιμοποιώντας το Aspose.Pdf για .NET.
  headline: Σύγκριση PDF ενώ αγνοούνται συγκεκριμένες περιοχές με χρήση του Aspose.Pdf
    για .NET
  type: TechArticle
- description: Μάθετε να συγκρίνετε PDF πλάι-πλάι και να αγνοείτε επιλεγμένες περιοχές
    χρησιμοποιώντας το Aspose.Pdf για .NET.
  name: Σύγκριση PDF ενώ αγνοούνται συγκεκριμένες περιοχές με χρήση του Aspose.Pdf
    για .NET
  steps:
  - name: Ορίστε τις διαδρομές αρχείων για τα δύο πηγαία PDF και το εξαγόμενο diff
      PDF.
    text: Ορίστε τις διαδρομές αρχείων για τα δύο πηγαία PDF και το εξαγόμενο diff
      PDF.
  - name: Ελέγξτε ότι και τα δύο πηγαία αρχεία PDF υπάρχουν και τερματίστε με μήνυμα
      σφάλματος εάν κάποιο λείπει.
    text: Ελέγξτε ότι και τα δύο πηγαία αρχεία PDF υπάρχουν και τερματίστε με μήνυμα
      σφάλματος εάν κάποιο λείπει.
  - name: Δημιουργήστε έναν πίνακα που περιέχει την ορθογώνια περιοχή που θα αγνοηθεί
      στο πρώτο PDF.
    text: Δημιουργήστε έναν πίνακα που περιέχει την ορθογώνια περιοχή που θα αγνοηθεί
      στο πρώτο PDF.
  - name: Δημιουργήστε έναν πίνακα που περιέχει την ορθογώνια περιοχή που θα αγνοηθεί
      στο δεύτερο PDF.
    text: Δημιουργήστε έναν πίνακα που περιέχει την ορθογώνια περιοχή που θα αγνοηθεί
      στο δεύτερο PDF.
  - name: Διαμορφώστε τη σύγκριση πλάι-πλάι, αντιστοιχίζοντας τους πίνακες περιοχών-αγνόησης
      στις κατάλληλες ιδιότητες.
    text: Διαμορφώστε τη σύγκριση πλάι-πλάι, αντιστοιχίζοντας τους πίνακες περιοχών-αγνόησης
      στις κατάλληλες ιδιότητες.
  - name: Φορτώστε και τα δύο PDF και εκτελέστε τη σύγκριση πλάι-πλάι, δημιουργώντας
      το αρχείο diff στη συγκεκριμένη διαδρομή.
    text: Φορτώστε και τα δύο PDF και εκτελέστε τη σύγκριση πλάι-πλάι, δημιουργώντας
      το αρχείο diff στη συγκεκριμένη διαδρομή.
  - name: Εκτυπώστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει ότι η σύγκριση ολοκληρώθηκε
      και πού αποθηκεύτηκε το diff PDF.
    text: Εκτυπώστε ένα μήνυμα επιβεβαίωσης που υποδεικνύει ότι η σύγκριση ολοκληρώθηκε
      και πού αποθηκεύτηκε το diff PDF.
  type: HowTo
- questions:
  - answer: Οι συντεταγμένες είναι σε points (1/72 ίντσα) με το αρχικό σημείο στην
      κάτω‑αριστερή γωνία της σελίδας, έτσι οι δύο πρώτοι αριθμοί είναι το κάτω‑αριστερό
      X/Y και οι δύο τελευταίοι το πάνω‑δεξιό X/Y.
    question: Τι σύστημα συντεταγμένων χρησιμοποιούν οι τιμές `Rectangle` όταν ορίζονται
      ζώνες αγνόησης;
  - answer: Ναι – παρέχετε πολλαπλά αντικείμενα `Aspose.Pdf.Rectangle` στον πίνακα
      `ExcludeAreas1` (ή `ExcludeAreas2`); κάθε ορθογώνιο θα εξαιρείται ανεξάρτητα
      κατά τη σύγκριση.
    question: Μπορώ να αγνοήσω περισσότερες από μία ορθογώνιες περιοχές στο ίδιο έγγραφο;
  - answer: Όχι. Το `ExcludeAreas1` εφαρμόζεται στο πρώτο PDF και το `ExcludeAreas2`
      στο δεύτερο, ώστε μπορείτε να καθορίσετε διαφορετικές συντεταγμένες για κάθε
      έγγραφο.
    question: Πρέπει τα ορθογώνια αγνόησης να είναι πανομοιότυπα και στα δύο PDF;
  - answer: Το Aspose.Pdf αγνοεί σιωπηλά τα ορθογώνια που πέφτουν εντελώς εκτός της
      σελίδας· δεν έχουν καμία επίδραση στο αποτέλεσμα της σύγκρισης.
    question: Τι συμβαίνει αν ένα ορθογώνιο οριστεί εκτός των ορίων της σελίδας;
  - answer: Οι πίνακες `ExcludeAreas` εφαρμόζονται ανά σελίδα, επομένως πρέπει να
      προσθέσετε το ίδιο `Rectangle` στη συλλογή κάθε σελίδας (π.χ., επαναλάβετε μέσω
      `pdf.Pages` και αναθέστε τον πίνακα) πριν καλέσετε το `SideBySidePdfComparer.Compare`.
    question: Πώς μπορώ να εξαιρέσω την ίδια περιοχή σε κάθε σελίδα ενός PDF;
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Αγνόηση περιοχών κατά τη σύγκριση PDF
og_description: Δείτε πώς να παραλείψετε επιλεγμένες περιοχές σε μια σύγκριση PDF πλάι-πλάι και να λάβετε ένα καθαρό diff PDF.
og_image_alt: Οδηγός που δείχνει σύγκριση PDF πλάι-πλάι με εξαιρούμενες ορθογώνιες περιοχές χρησιμοποιώντας το Aspose.Pdf για .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Σύγκριση PDF ενώ αγνοούνται συγκεκριμένες περιοχές με χρήση του Aspose.Pdf για .NET
Αυτό το σεμινάριο δείχνει πώς να συγκρίνετε δύο έγγραφα PDF πλάι-πλάι με το Aspose.Pdf για .NET, εξαιρώντας καθορισμένες ορθογώνιες περιοχές από την ανάλυση. Ορίζοντας περιοχές εξαίρεσης σε κάθε αρχείο, το παραγόμενο diff PDF επισημαίνει μόνο τις αλλαγές που έχουν σημασία, καθιστώντας πιο εύκολο να εστιάσετε στις σχετικές διαφορές.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Τι σύστημα συντεταγμένων χρησιμοποιούν οι τιμές `Rectangle` όταν ορίζονται ζώνες αγνόησης;**  
A: Οι συντεταγμένες είναι σε points (1/72 ίντσα) με το αρχικό σημείο στην κάτω‑αριστερή γωνία της σελίδας, έτσι οι δύο πρώτοι αριθμοί είναι το κάτω‑αριστερό X/Y και οι δύο τελευταίοι το πάνω‑δεξιό X/Y.

**Q: Μπορώ να αγνοήσω περισσότερες από μία ορθογώνιες περιοχές στο ίδιο έγγραφο;**  
A: Ναι – παρέχετε πολλαπλά αντικείμενα `Aspose.Pdf.Rectangle` στον πίνακα `ExcludeAreas1` (ή `ExcludeAreas2`); κάθε ορθογώνιο θα εξαιρείται ανεξάρτητα κατά τη σύγκριση.

**Q: Πρέπει τα ορθογώνια αγνόησης να είναι πανομοιότυπα και στα δύο PDF;**  
A: Όχι. Το `ExcludeAreas1` εφαρμόζεται στο πρώτο PDF και το `ExcludeAreas2` στο δεύτερο, ώστε μπορείτε να καθορίσετε διαφορετικές συντεταγμένες για κάθε έγγραφο.

**Q: Τι συμβαίνει αν ένα ορθογώνιο οριστεί εκτός των ορίων της σελίδας;**  
A: Το Aspose.Pdf αγνοεί σιωπηλά τα ορθογώνια που πέφτουν εντελώς εκτός της σελίδας· δεν έχουν καμία επίδραση στο αποτέλεσμα της σύγκρισης.

**Q: Πώς μπορώ να εξαιρέσω την ίδια περιοχή σε κάθε σελίδα ενός PDF;**  
A: Οι πίνακες `ExcludeAreas` εφαρμόζονται ανά σελίδα, επομένως πρέπει να προσθέσετε το ίδιο `Rectangle` στη συλλογή κάθε σελίδας (π.χ., επαναλάβετε μέσω `pdf.Pages` και αναθέστε τον πίνακα) πριν καλέσετε το `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}