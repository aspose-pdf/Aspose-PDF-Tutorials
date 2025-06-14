---
"description": "Μάθετε πώς να δημιουργείτε και να διαμορφώνετε ένα στοιχείο πίνακα στο Aspose.PDF για .NET με οδηγίες βήμα προς βήμα, προσαρμοσμένο στυλ και συμμόρφωση με PDF/UA."
"linktitle": "Στοιχείο πίνακα στυλ"
"second_title": "Aspose.PDF για αναφορά API .NET"
"title": "Στοιχείο πίνακα στυλ"
"url": "/el/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Στοιχείο πίνακα στυλ

## Εισαγωγή

Σε αυτό το άρθρο, θα εμβαθύνουμε στον τρόπο δημιουργίας και διαμόρφωσης ενός στοιχείου πίνακα χρησιμοποιώντας το Aspose.PDF για .NET. Θα μάθετε πώς να δομήσετε έναν πίνακα, να εφαρμόσετε προσαρμοσμένα στυλ και να επικυρώσετε τη συμβατότητα PDF/UA του εγγράφου σας. Μέχρι το τέλος αυτού του σεμιναρίου, θα μπορείτε να δημιουργείτε πίνακες επαγγελματικής εμφάνισης στα PDF σας με ευκολία!

## Προαπαιτούμενα

Πριν ξεκινήσετε το σεμινάριο, θα πρέπει να βεβαιωθείτε ότι έχετε τα εξής:

1. Το Visual Studio ή ένα παρόμοιο IDE είναι εγκατεστημένο στον υπολογιστή σας.
2. .NET Framework ή .NET Core SDK για την εκτέλεση της εφαρμογής.
3. Το Aspose.PDF για τη βιβλιοθήκη .NET λήφθηκε και αναφέρθηκε στο έργο σας. Μπορείτε να κατεβάσετε την πιο πρόσφατη έκδοση από [εδώ](https://releases.aspose.com/pdf/net/).
4. Μια έγκυρη άδεια Aspose ή μια [προσωρινή άδεια](https://purchase.aspose.com/temporary-license/) για να ξεκλειδώσετε όλες τις λειτουργίες της βιβλιοθήκης.

## Εισαγωγή πακέτων

Για να ξεκινήσετε, εισαγάγετε τους απαραίτητους χώρους ονομάτων στο έργο σας:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Αυτοί οι χώροι ονομάτων καλύπτουν βασικές λειτουργίες PDF, περιεχόμενο με ετικέτες, πίνακες και μορφοποίηση κειμένου.

Ας αναλύσουμε τώρα τη διαδικασία δημιουργίας και διαμόρφωσης ενός πίνακα στο Aspose.PDF. Θα εξετάσουμε κάθε ενότητα λεπτομερώς, ώστε να μπορείτε να την παρακολουθήσετε.

## Βήμα 1: Δημιουργήστε ένα νέο έγγραφο PDF και ρυθμίστε το περιεχόμενο με ετικέτες

Σε αυτό το πρώτο βήμα, θα δημιουργήσουμε ένα κενό έγγραφο PDF και θα ρυθμίσουμε το περιεχόμενο με ετικέτες.

```csharp
// Η διαδρομή προς τον κατάλογο εγγράφων.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Δημιουργήστε ένα νέο έγγραφο PDF
Document document = new Document();

// Ρύθμιση περιεχομένου με ετικέτα
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Ξεκινάμε δημιουργώντας ένα νέο `Document` αντικείμενο, που αντιπροσωπεύει το PDF μας. Το `TaggedContent` Το αντικείμενο χρησιμοποιείται για τη διαχείριση της δομής του εγγράφου, διασφαλίζοντας τη συμμόρφωση με τα πρότυπα προσβασιμότητας. Ορίζουμε τον τίτλο και τη γλώσσα του εγγράφου για σωστή προσθήκη ετικετών.

## Βήμα 2: Ορίστε το στοιχείο ρίζας

Στη συνέχεια, θα δημιουργήσουμε το στοιχείο ρίζας δομής, το οποίο λειτουργεί ως δοχείο για όλο το περιεχόμενο στο PDF μας.

```csharp
// Λήψη του στοιχείου δομής ρίζας
StructureElement rootElement = taggedContent.RootElement;
```

Ο `RootElement` χρησιμεύει ως το βασικό κοντέινερ για όλα τα δομημένα στοιχεία, συμπεριλαμβανομένου του πίνακά μας. Βοηθά στη διατήρηση της δομικής ιεραρχίας του εγγράφου, η οποία είναι σημαντική τόσο για την οργάνωση όσο και για την προσβασιμότητα.

## Βήμα 3: Δημιουργία και διαμόρφωση του στοιχείου πίνακα

Τώρα που το στοιχείο root έχει ρυθμιστεί, θα δημιουργήσουμε ένα `TableElement` και εφαρμόστε στυλ όπως χρώμα φόντου, περιγράμματα και στοίχιση.

```csharp
// Δημιουργία στοιχείου δομής πίνακα
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Στυλίστε το τραπέζι
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Δημιουργούμε ένα `TableElement`, το οποίο ορίζει τη δομή του πίνακά μας. Το `BackgroundColor`, `Border`, και `Alignment` Οι ιδιότητες μας επιτρέπουν να προσαρμόσουμε την εμφάνιση του πίνακα. `Broken` Η ιδιότητα διασφαλίζει ότι εάν ο πίνακας σπάσει σε σελίδες, σπάει και κάθετα.

## Βήμα 4: Ορισμός διαστάσεων πίνακα και στυλ κελιών

Σε αυτό το βήμα, θα ορίσουμε τον αριθμό των στηλών, την αναπλήρωση κελιών και άλλες σημαντικές ιδιότητες πίνακα.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Καθορίζουμε τα πλάτη των στηλών για να διασφαλίσουμε ότι κάθε στήλη στον πίνακα έχει ομοιόμορφη απόσταση μεταξύ της. `DefaultCellBorder`, `DefaultCellPadding`, και `DefaultCellTextState` ορίστε τα προεπιλεγμένα στυλ για τα κελιά, συμπεριλαμβανομένων των περιγραμμάτων, της αναπλήρωσης, του χρώματος κειμένου και του μεγέθους γραμματοσειράς.

## Βήμα 5: Προσθήκη επαναλαμβανόμενων γραμμών και προσαρμοσμένων στυλ

Μπορούμε επίσης να ορίσουμε στυλ για επαναλαμβανόμενες γραμμές και άλλα συγκεκριμένα στοιχεία πίνακα, όπως κεφαλίδες και υποσέλιδα.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

Ο `RepeatingRowsCount` διασφαλίζει ότι οι τρεις πρώτες γραμμές επαναλαμβάνονται εάν ο πίνακας εκτείνεται σε πολλές σελίδες. Ορίζουμε το `RepeatingRowsStyle` για να εφαρμόσετε ένα προσαρμοσμένο χρώμα φόντου σε αυτές τις γραμμές.

## Βήμα 6: Προσθήκη στοιχείων κεφαλής, σώματος και ποδιού τραπεζιού

Τώρα, ας δημιουργήσουμε τις ενότητες κεφαλίδας, σώματος και υποσέλιδου πίνακα και ας τις συμπληρώσουμε με περιεχόμενο.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Δημιουργία γραμμής κεφαλίδας
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Συμπληρώστε το σώμα του πίνακα
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

Ο πίνακας χωρίζεται σε τρία μέρη: την κεφαλή, το σώμα και το πόδι. Αρχικά δημιουργούμε τη γραμμή κεφαλίδας χρησιμοποιώντας `TableTHElement` και προσθέτουμε επικεφαλίδες στηλών. Στη συνέχεια, συμπληρώνουμε το σώμα του πίνακα με `TableTDElement`, γεμίζοντας κάθε κελί με μια ετικέτα που περιλαμβάνει τη θέση του.

## Βήμα 7: Αποθήκευση του εγγράφου

Τέλος, αποθηκεύουμε το έγγραφο PDF στον καθορισμένο κατάλογο.

```csharp
// Αποθήκευση του εγγράφου PDF με ετικέτα
document.Save(dataDir + "StyleTableElement.pdf");
```

Αυτό το βήμα ολοκληρώνει τη διαδικασία δημιουργίας εγγράφου αποθηκεύοντας το αρχείο PDF με τον στυλιζαρισμένο πίνακα.

## Βήμα 8: Επικύρωση συμμόρφωσης με PDF/UA

Αφού αποθηκεύσετε το έγγραφο, είναι σημαντικό να βεβαιωθείτε ότι συμμορφώνεται με τα πρότυπα PDF/UA (Καθολική Προσβασιμότητα).

```csharp
// Ελέγξτε τη συμμόρφωση με PDF/UA
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Εδώ, επαναφορτώνουμε το έγγραφο και το επικυρώνουμε σύμφωνα με τα πρότυπα PDF/UA. Η συμμόρφωση διασφαλίζει ότι το PDF σας πληροί τις απαιτήσεις προσβασιμότητας, καθιστώντας το κατάλληλο για ένα ευρύ φάσμα χρηστών.

## Σύναψη

Με το Aspose.PDF για .NET, η δημιουργία και η διαμόρφωση πινάκων στα έγγραφα PDF σας είναι απλή και διαισθητική. Ακολουθώντας τα βήματα που περιγράφονται σε αυτό το σεμινάριο, μπορείτε να δημιουργήσετε πίνακες με προσαρμοσμένα στυλ και να διασφαλίσετε ότι τα PDF σας πληρούν τα πρότυπα προσβασιμότητας. Είτε δημιουργείτε αναφορές είτε δημιουργείτε δομημένα έγγραφα, οι πίνακες αποτελούν ένα ισχυρό εργαλείο για την σαφή παρουσίαση δεδομένων.

## Συχνές ερωτήσεις

### Μπορώ να προσθέσω εικόνες μέσα σε κελιά πίνακα;
Ναι, μπορείτε να εισαγάγετε εικόνες σε κελιά πίνακα χρησιμοποιώντας το `Image` στοιχείο.

### Πώς μπορώ να προσαρμόσω δυναμικά τα πλάτη των στηλών;
Μπορείτε να ορίσετε το `ColumnAdjustment` ιδιοκτησία σε `AutoFitToWindow` για αυτόματη προσαρμογή του πλάτους των στηλών με βάση το περιεχόμενο.

### Είναι υποχρεωτική η συμμόρφωση με PDF/UA για όλα τα έγγραφα;
Αν και δεν είναι υποχρεωτικό, συνιστάται για έγγραφα που απαιτούν υψηλά πρότυπα προσβασιμότητας.

### Μπορώ να εφαρμόσω διαφορετικά στυλ σε συγκεκριμένες σειρές;
Ναι, μπορείτε να προσαρμόσετε μεμονωμένες γραμμές ή κελιά προσαρμόζοντάς τα `TextState` ή `BackgroundColor`.

### Ποιο είναι το όφελος από τη χρήση περιεχομένου με ετικέτες;
Το περιεχόμενο με ετικέτες βελτιώνει την προσβασιμότητα των εγγράφων και βοηθά στη διασφάλιση της συμμόρφωσης με πρότυπα όπως το PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}