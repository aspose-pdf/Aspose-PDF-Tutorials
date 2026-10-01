---
category: general
date: 2026-04-25
description: Προσθέστε αρίθμηση Bates σε PDF γρήγορα χρησιμοποιώντας το Aspose.Pdf.
  Μάθετε πώς να προσθέτετε αριθμούς σελίδων σε PDF, να προσαρμόζετε αυτόματα το μέγεθος
  γραμματοσειράς και να προσθέτετε υδατογράφημα κειμένου σε C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: el
og_description: Προσθέστε αρίθμηση Bates σε PDF με το Aspose.Pdf. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε αριθμούς σελίδων σε PDF, να προσαρμόσετε αυτόματα το μέγεθος γραμματοσειράς
  και να προσθέσετε υδατογράφημα κειμένου σε ένα ενιαίο, εκτελέσιμο παράδειγμα.
og_title: Προσθήκη αρίθμησης Bates σε PDF – Πλήρης οδηγός Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Προσθήκη αρίθμησης Bates σε PDF με το Aspose – Πλήρης Οδηγός
url: /el/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering σε PDF με Aspose – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **add bates numbering** σε ένα PDF αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—νομικές ομάδες, ελεγκτές και προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα καθημερινά. Τα καλά νέα; Με το Aspose.Pdf for .NET μπορείτε να σφραγίσετε έναν Bates αριθμό, να προσαρμόσετε αυτόματα το μέγεθος της γραμματοσειράς και ακόμη να μετατρέψετε τη σφραγίδα σε διακριτικό υδατογράφημα κειμένου—όλα σε λίγες γραμμές C#.

Σε αυτό το tutorial θα περάσουμε βήμα προς βήμα τις ακριβείς ενέργειες για **add page numbers pdf**, θα ρυθμίσουμε τη γραμματοσειρά ώστε να μην υπερβαίνει ποτέ, και θα απαντήσουμε στην ερώτηση “how to add bates” μια και για πάντα. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση console εφαρμογή που παράγει ένα επαγγελματικά αριθμημένο PDF, και θα δείτε πώς να το επεκτείνετε σε μια πλήρη λύση υδατογραφήματος.

## Προαπαιτούμενα

* **Aspose.Pdf for .NET** (το πιο πρόσφατο πακέτο NuGet μέχρι Απρίλιο 2026).  
* .NET 6.0 SDK ή νεότερο – το API λειτουργεί το ίδιο στο .NET Framework, αλλά το .NET 6 προσφέρει την καλύτερη απόδοση.  
* Ένα δείγμα PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (π.χ., `C:\Docs\`).  

Δεν απαιτείται επιπλέον ρύθμιση· η βιβλιοθήκη είναι αυτόνομη.

---

## Βήμα 1 – Φόρτωση του Πηγής PDF Εγγράφου

Το πρώτο που κάνουμε είναι να ανοίξουμε το αρχείο που θέλουμε να αριθμήσουμε. Η κλάση `Document` της Aspose αντιπροσωπεύει ολόκληρο το PDF, και η φόρτωσή του είναι τόσο απλή όσο η μεταβίβαση της διαδρομής στον κατασκευαστή.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου σας δίνει πρόσβαση στη συλλογή `Pages`, όπου θα προσθέσουμε το σφραγίδα Bates αργότερα. Αν το αρχείο δεν βρεθεί, η Aspose ρίχνει ένα σαφές `FileNotFoundException`, ώστε να γνωρίζετε ακριβώς τι πήγε στραβά.

---

## Βήμα 2 – Δημιουργία Text Stamp για Bates Numbers

Τώρα δημιουργούμε το οπτικό στοιχείο που θα εμφανίζεται σε κάθε σελίδα. Η κλάση `TextStamp` σας επιτρέπει να ενσωματώσετε οποιαδήποτε συμβολοσειρά, και θα χρησιμοποιήσουμε το placeholder `{page}-{total}` ώστε η Aspose να αντικαταστήσει αυτά τα tokens αυτόματα.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Βασικά σημεία*:

* **auto adjust font size** – Ορίζοντας το `AutoAdjustFontSizeToFitStampRectangle` σε `true` εξασφαλίζει ότι το κείμενο δεν θα ξεχειλίσει έξω από το ορθογώνιο, κάτι που είναι τέλειο για αριθμούς σελίδων μεταβλητού μήκους.
* **add text watermark** – Με τη μείωση του `Opacity` μετατρέπουμε τον Bates αριθμό σε αχνό υδατογράφημα, ικανοποιώντας την απαίτηση “add text watermark” χωρίς ξεχωριστό βήμα.
* **how to add bates** – Τα tokens `{page}` και `{total}` είναι το μυστικό συστατικό· η Aspose τα αντικαθιστά κατά την εκτέλεση, ώστε να μην χρειάζεται να υπολογίσετε τίποτα μόνοι σας.

---

## Βήμα 3 – Εφαρμογή της Σφραγίδας σε Κάθε Σελίδα

Ένα κοινό λάθος είναι η σφράγιση μόνο της πρώτης σελίδας. Για να **add page numbers pdf** πραγματικά, πρέπει να επαναλάβουμε τη συλλογή `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Γιατί κλωνοποίηση; Η μέθοδος `AddStamp` δημιουργεί εσωτερικά ένα αντίγραφο, αλλά η ρητή χρήση μιας νέας εμφάνισης ανά επανάληψη αποφεύγει τυχαίες παρενέργειες αν αργότερα τροποποιήσετε τις ιδιότητες της σφραγίδας (π.χ., αλλαγή χρώματος για συγκεκριμένες σελίδες).

---

## Βήμα 4 – Αποθήκευση του Ενημερωμένου PDF

Με τις σφραγίδες στη θέση τους, η αποθήκευση των αλλαγών είναι απλή. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να γράψετε σε νέα τοποθεσία—εδώ θα αποθηκεύσουμε ένα νέο αρχείο με όνομα `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Αν ανοίξετε το `output.pdf` θα δείτε κάθε σελίδα να φέρει την ετικέτα “Bates: 1‑10”, “Bates: 2‑10”, … στο κάτω‑δεξιό μέρος, με αχνή διαφάνεια που λειτουργεί επίσης ως **add text watermark**.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα ενιαίο, αυτόνομο πρόγραμμα console που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα**: Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα· κάθε σελίδα εμφανίζει μια γραμμή όπως “Bates: 3‑12” στην κάτω‑δεξιά γωνία, με μέγεθος ακριβώς κατάλληλο για το ορθογώνιο και αποδοθεί με 40 % διαφάνεια. Αυτό ικανοποιεί τόσο την απαίτηση νομικής παρακολούθησης όσο και την ανάγκη για οπτικό υδατογράφημα.

---

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

| Κατάσταση | Τι να αλλάξετε | Γιατί |
|-----------|----------------|------|
| **Διαφορετική τοποθέτηση** | Ρυθμίστε `HorizontalAlignment` / `VerticalAlignment` ή ορίστε `XIndent`/`YIndent` | Ορισμένες εταιρείες προτιμούν τοποθέτηση πάνω‑αριστερά ή στο κέντρο. |
| **Προσαρμοσμένο πρόθεμα** | Αντικαταστήστε το `"Bates: "` με το `"Doc‑ID: "` ή οποιαδήποτε συμβολοσειρά | Μπορεί να χρησιμοποιείτε διαφορετική σύμβαση ονομασίας. |
| **Πολλαπλές σφραγίδες** | Δημιουργήστε ένα δεύτερο `TextStamp` (π.χ., για ειδοποίηση εμπιστευτικότητας) και προσθέστε το μετά το πρώτο | Ο συνδυασμός **add bates numbering** με άλλες απαιτήσεις **add text watermark** είναι απλός. |
| **Μεγάλος αριθμός σελίδων** | Αυξήστε το αρχικό μέγεθος γραμματοσειράς (π.χ., `14`) – η αυτόματη προσαρμογή θα το μειώσει όταν χρειαστεί | Όταν έχετε > 999 σελίδες η συμβολοσειρά γίνεται μεγαλύτερη· η αυτόματη προσαρμογή αποτρέπει την αποκοπή. |
| **Κρυπτογραφημένα PDFs** | Καλέστε `pdfDocument.Decrypt("password")` πριν τη σφράγιση | Δεν μπορείτε να τροποποιήσετε ένα ασφαλισμένο αρχείο χωρίς τον κωδικό. |

---

## Συμβουλές & Πιθανά Προβλήματα

* **Pro tip:** Ορίστε `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` αν παρατηρήσετε ότι το κείμενο αγκαλιάζει την άκρη της σελίδας.  
* **Watch out for:** Πολύ μικρά ορθογώνια (το προεπιλεγμένο μέγεθος είναι 100 × 30 pt). Αν χρειάζεστε μεγαλύτερη περιοχή, ορίστε το `batesStamp.Width` και το `batesStamp.Height` χειροκίνητα.  
* **Performance note:** Η σφράγιση χιλιάδων σελίδων μπορεί να διαρκέσει μερικά δευτερόλεπτα, αλλά η Aspose μεταδίδει τις σελίδες αποδοτικά—δεν χρειάζεται να φορτώσετε ολόκληρο το έγγραφο στη μνήμη.  

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **add bates numbering** σε ένα PDF χρησιμοποιώντας το Aspose.Pdf, ενώ ταυτόχρονα **add page numbers pdf**, ενεργοποιούμε το **auto adjust font size** και δημιουργούμε ένα **add text watermark** σε μια ενιαία ροή. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω σας παρέχει μια σταθερή βάση που μπορείτε να προσαρμόσετε σε οποιαδήποτε ροή εργασίας νομικών εγγράφων ή εσωτερικό σύστημα αναφοράς.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να συνδυάσετε αυτή την προσέγγιση με το API συγχώνευσης PDF της Aspose για μαζική επεξεργασία πολλαπλών αρχείων, ή εξερευνήστε την κλάση `TextFragment` για πιο πλούσια υδατογραφήματα (χρωματιστά, περιστραμμένα ή πολλαπλών γραμμών). Οι δυνατότητες είναι ατελείωτες, και ο κώδικας που έχετε τώρα είναι μια αξιόπιστη βάση.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μη διστάσετε να αφήσετε ένα σχόλιο, να δώσετε αστέρι στο αποθετήριο, ή να μοιραστείτε τις δικές σας παραλλαγές. Καλή προγραμματιστική, και εύχομαι τα PDF σας να είναι πάντα τέλεια αριθμημένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}