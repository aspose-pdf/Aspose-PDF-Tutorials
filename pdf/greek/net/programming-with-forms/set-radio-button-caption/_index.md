---
"description": "Μάθετε πώς να ορίζετε λεζάντες για κουμπιά επιλογής σε PDF χρησιμοποιώντας το Aspose.PDF για .NET. Αυτός ο οδηγός βήμα προς βήμα σας καθοδηγεί στη φόρτωση, την τροποποίηση και την αποθήκευση των φορμών PDF."
"linktitle": "Ορισμός υπότιτλου κουμπιού ραδιοφώνου"
"second_title": "Aspose.PDF για αναφορά API .NET"
"title": "Ορισμός υπότιτλου κουμπιού ραδιοφώνου"
"url": "/el/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός υπότιτλου κουμπιού ραδιοφώνου

## Εισαγωγή

Αν ασχολείστε με τον χειρισμό PDF με το Aspose.PDF για .NET, σας περιμένει μια εξαιρετική εμπειρία! Σήμερα, εστιάζουμε σε μια πρακτική λειτουργία: τον ορισμό λεζάντων κουμπιών επιλογής στις φόρμες PDF. Τα κουμπιά επιλογής είναι απαραίτητα για τις φόρμες χρήστη όπου χρειάζεστε μια επιλογή από ένα σύνολο επιλογών. Φανταστείτε τα ως ερωτήσεις πολλαπλής επιλογής όπου επιτρέπεται μόνο μία απάντηση. Αυτό το σεμινάριο θα σας καθοδηγήσει στη διαδικασία ενημέρωσης λεζάντων κουμπιών επιλογής σε μια μορφή PDF, ώστε τα έγγραφά σας να είναι διαδραστικά και φιλικά προς το χρήστη. 

## Προαπαιτούμενα

Πριν εμβαθύνετε στον κώδικα, υπάρχουν μερικά πράγματα που θα πρέπει να βεβαιωθείτε ότι έχετε:

1. Aspose.PDF για .NET: Βεβαιωθείτε ότι έχετε εγκαταστήσει τη βιβλιοθήκη Aspose.PDF. Αυτή η βιβλιοθήκη θα σας βοηθήσει να χειρίζεστε αρχεία PDF μέσω προγραμματισμού.
2. Περιβάλλον Ανάπτυξης: Θα πρέπει να έχετε ρυθμίσει ένα περιβάλλον ανάπτυξης .NET, όπως το Visual Studio.
3. Δείγμα φόρμας PDF: Για αυτό το σεμινάριο, θα χρειαστείτε ένα δείγμα φόρμας PDF με κουμπιά επιλογής. Μπορείτε να χρησιμοποιήσετε οποιαδήποτε υπάρχουσα φόρμα PDF ή να δημιουργήσετε μια νέα με κουμπιά επιλογής.
4. Βασικές γνώσεις C#: Αυτός ο οδηγός προϋποθέτει ότι έχετε βασική κατανόηση των εννοιών προγραμματισμού C# και .NET.

Εάν δεν έχετε εγκαταστήσει ακόμη το Aspose.PDF για .NET ή χρειάζεστε μια προσωρινή άδεια χρήσης, μπορείτε να [κατεβάστε το εδώ](https://releases.aspose.com/pdf/net/) ή [να λάβω προσωρινή άδεια](https://purchase.aspose.com/temporary-license/).

## Εισαγωγή πακέτων

Για να ξεκινήσετε, πρέπει να εισαγάγετε τα απαραίτητα πακέτα στο έργο σας σε C#. Δείτε πώς μπορείτε να συμπεριλάβετε τη βιβλιοθήκη Aspose.PDF:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Βεβαιωθείτε ότι έχετε προσθέσει αυτά τα πακέτα στο έργο σας μέσω του NuGet ή της προτιμώμενης μεθόδου σας.

## Βήμα 1: Φόρτωση της φόρμας PDF

Αρχικά, πρέπει να φορτώσετε τη φόρμα PDF που περιέχει τα κουμπιά επιλογής. `Aspose.Pdf.Facades.Form` Η κλάση χρησιμοποιείται για αυτόν τον σκοπό. Δείτε πώς το κάνετε:

```csharp
// Ορίστε τη διαδρομή προς τον κατάλογο εγγράφων σας
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Φόρτωση της φόρμας PDF πηγής
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

Σε αυτό το απόσπασμα κώδικα:
- `dataDir` Καθορίζει τη διαδρομή όπου βρίσκεται το PDF σας.
- `Form` Η κλάση χρησιμοποιείται για την αλληλεπίδραση με τα πεδία της φόρμας μέσα στο PDF.
- `Document` Η κλάση παρέχει πρόσβαση στις σελίδες του εγγράφου PDF.

## Βήμα 2: Επανάληψη μέσω πεδίων κουμπιών επιλογής

Στη συνέχεια, θα χρειαστεί να επαναλάβετε τα πεδία στη φόρμα σας για να εντοπίσετε και να χειριστείτε τα πεδία του κουμπιού επιλογής:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

Σε αυτόν τον βρόχο:
- `FieldNames` παρέχει μια λίστα με όλα τα ονόματα πεδίων στο PDF.
- `GetButtonOptionValues(item)` ανακτά τις διαθέσιμες επιλογές για κάθε κουμπί επιλογής.

## Βήμα 3: Τροποποίηση επιλογών κουμπιού επιλογής

Μόλις εντοπίσετε τα πεδία των κουμπιών επιλογής, μπορείτε να τροποποιήσετε τις επιλογές τους. Για αυτό, πρέπει να μετατρέψετε το πεδίο σε `RadioButtonField` και ενημερώστε τις επιλογές του:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Εδώ:
- Ελέγχουμε αν το όνομα πεδίου περιέχει τον όρο "radio1" για να προσδιορίσουμε το συγκεκριμένο πεδίο κουμπιού επιλογής που θέλουμε να τροποποιήσουμε.
- `RadioButtonField` μεταδίδεται από τα πεδία της φόρμας για να κάνει συγκεκριμένες τροποποιήσεις.

## Βήμα 4: Ορίστε τον υπότιτλο για το κουμπί ραδιοφώνου

Για να ορίσετε ή να ενημερώσετε τη λεζάντα για το κουμπί επιλογής, θα χρειαστεί να δημιουργήσετε ένα `TextFragment` και χρήση `TextBuilder` για να το τοποθετήσετε στην επιθυμητή θέση:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Δημιουργία αντικειμένου TextParagraph
        TextParagraph par = new TextParagraph();
        // Ορισμός θέσης παραγράφου
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Καθορισμός λειτουργίας αναδίπλωσης λέξεων
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Προσθήκη νέου TextFragment στην παράγραφο
        par.AppendLine(updatedFragment);
        // Προσθήκη του TextParagraph χρησιμοποιώντας το TextBuilder
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

Σε αυτό το μέρος:
- `TextFragment` Χρησιμοποιείται για να ορίσει το κείμενο και την εμφάνισή του.
- `TextParagraph` βοηθά στην τοποθέτηση και μορφοποίηση του κειμένου.
- `TextBuilder` προσθέτει το κείμενο στην καθορισμένη σελίδα του PDF.

## Βήμα 5: Αποθηκεύστε το ενημερωμένο PDF

Τέλος, αποθηκεύστε το ενημερωμένο PDF σε ένα νέο αρχείο:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Αυτό θα διασφαλίσει ότι:
- Οι αλλαγές εφαρμόζονται στο PDF.
- Η αρχική επιλογή του κουμπιού επιλογής καταργείται όπως καθορίζεται.

## Σύναψη

Η τροποποίηση λεζάντων κουμπιών επιλογής σε μια μορφή PDF χρησιμοποιώντας το Aspose.PDF για .NET μπορεί να βελτιώσει σημαντικά την διαδραστικότητα και τη χρηστικότητα των εγγράφων σας. Με τα βήματα που περιγράφονται σε αυτό το σεμινάριο, μπορείτε εύκολα να φορτώσετε ένα PDF, να ενημερώσετε τις επιλογές κουμπιών επιλογής και να αποθηκεύσετε τις αλλαγές σας. Αυτή η προσέγγιση είναι χρήσιμη για τη διαχείριση φορμών και διασφαλίζει ότι τα PDF σας ανταποκρίνονται στις ακριβείς ανάγκες των χρηστών σας. Βυθιστείτε στο Aspose.PDF και εξερευνήστε τις δυνατότητές του για άλλους χειρισμούς PDF!

## Συχνές ερωτήσεις

### Μπορώ να ενημερώσω πολλά πεδία κουμπιών επιλογής ταυτόχρονα;
Ναι, μπορείτε να επαναλάβετε όλα τα πεδία των κουμπιών επιλογής και να εφαρμόσετε αλλαγές όπως απαιτείται.

### Χρειάζομαι άδεια χρήσης για να χρησιμοποιήσω το Aspose.PDF;
Μπορείτε να ξεκινήσετε με μια δωρεάν δοκιμαστική περίοδο, αλλά απαιτείται άδεια χρήσης για εκτεταμένη χρήση. [Αποκτήστε άδεια εδώ](https://purchase.aspose.com/buy).

### Πώς μπορώ να δοκιμάσω τις αλλαγές πριν αποθηκεύσω το PDF;
Μπορείτε να κάνετε προεπισκόπηση του PDF στο περιβάλλον ανάπτυξής σας ή να χρησιμοποιήσετε ένα πρόγραμμα προβολής PDF για να ελέγξετε τις τροποποιήσεις.

### Είναι το Aspose.PDF συμβατό με όλες τις εκδόσεις του .NET;
Το Aspose.PDF υποστηρίζει διάφορες εκδόσεις του .NET. Βεβαιωθείτε ότι έχετε ελέγξει τη συμβατότητα με την συγκεκριμένη έκδοση .NET που διαθέτετε.

### Μπορώ να χειριστώ άλλα πεδία φόρμας με παρόμοιο τρόπο;
Ναι, παρόμοιες τεχνικές μπορούν να εφαρμοστούν και σε άλλους τύπους πεδίων φόρμας σε έγγραφα PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}