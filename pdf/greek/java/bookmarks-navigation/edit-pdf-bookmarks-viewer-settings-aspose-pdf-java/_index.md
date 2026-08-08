---
date: '2026-05-28'
description: Μάθετε πώς να ορίσετε την προβολή μίας σελίδας PDF, να αλλάξετε viewer
  preferences, να επεξεργαστείτε σελιδοδείκτες και να διαμορφώσετε τις ρυθμίσεις PDF
  χρησιμοποιώντας Aspose.PDF for Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Προβολή Μίας Σελίδας PDF σε Java – Αλλαγή Layout & Επεξεργασία Bookmarks
url: /el/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Προβολή μίας σελίδας PDF σε Java – Αλλαγή διάταξης & επεξεργασία σελιδοδεικτών

## Εισαγωγή
Όταν οι αναγνώστες ανοίγουν ένα μεγάλο PDF, η προεπιλεγμένη διάταξη του προβολέα μπορεί να κυλά συνεχώς, καθιστώντας δύσκολο το να εστιάσουν σε μία σελίδα. Με τη ρύθμιση **single page view pdf**, αναγκάζετε τον προβολέα να εμφανίζει μία σελίδα τη φορά, κάτι που είναι ιδανικό για εκθέσεις, e‑books και καταλόγους. Σε αυτό το σεμινάριο θα μάθετε επίσης πώς να επεξεργαστείτε υπάρχοντες σελιδοδείκτες PDF, να ορίσετε προορισμούς σελιδοδεικτών κατά τη δημιουργία ενός εγγράφου και να προσαρμόσετε άλλες προτιμήσεις προβολέα χρησιμοποιώντας το Aspose.PDF for Java. Στο τέλος θα έχετε πλήρη έλεγχο της πλοήγησης, της ακρίβειας των σελιδοδεικτών και της διάταξης στην οθόνη.

**Τι θα μάθετε**
- Πώς να επεξεργαστείτε υπάρχοντες σελιδοδείκτες PDF ώστε να δείχνουν στην αρχή μιας σελίδας.  
- Πώς να ορίσετε προορισμούς σελιδοδεικτών κατά τη δημιουργία ενός PDF.  
- Πώς να αλλάξετε τις προτιμήσεις του προβολέα, όπως η διάταξη μίας σελίδας.  
- Πρακτικές συμβουλές για τη φόρτωση ενός εγγράφου PDF σε Java και τη βελτιστοποίηση της απόδοσης.

### Γρήγορες Απαντήσεις
- **Ποιος είναι ο κύριος τρόπος ενεργοποίησης της προβολής μίας σελίδας PDF;** Call `PdfContentEditor.changeViewerPreference()` with `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Μπορούν οι προορισμοί σελιδοδεικτών να επεξεργαστούν μετά τη δημιουργία ενός PDF;** Yes – load the document, retrieve the outline, and assign a new `ExplicitDestination`.  
- **Χρειάζομαι άδεια για αυτές τις λειτουργίες;** A free trial works for evaluation; a full license removes all limitations.  
- **Ποια εξάρτηση Maven απαιτείται;** `com.aspose:aspose-pdf:25.3` (or later).  
- **Είναι συμβατό με Java 11 και νεότερες;** Absolutely – Aspose.PDF supports Java 8+.

## Τι είναι η «αλλαγή διάταξης σελίδας PDF»;
Η αλλαγή της διάταξης σελίδας PDF ελέγχει πώς εμφανίζονται οι σελίδες σε έναν προβολέα — μία σελίδα, συνεχόμενη, προβολή δύο σελίδων κ.λπ. Η ενεργοποίηση του **single page view pdf** βελτιώνει την αναγνωσιμότητα για μεγάλα έγγραφα και εξασφαλίζει ότι κάθε σελίδα παρουσιάζεται ξεχωριστά, κάτι που είναι ιδιαίτερα χρήσιμο σε κινητές συσκευές και tablet.

## Γιατί να επεξεργαστείτε σελιδοδείκτες PDF και να ορίσετε προορισμούς σελιδοδεικτών;
Οι σελιδοδείκτες λειτουργούν όπως ένας δυναμικός πίνακας περιεχομένων. Ακριβείς προορισμοί επιτρέπουν στους αναγνώστες να μεταβούν άμεσα στην επιθυμητή ενότητα, εξαλείφοντας την επιπλέον κύλιση και μειώνοντας την απογοήτευση του χρήστη. Αυτό οδηγεί σε πιο ομαλή εμπειρία πλοήγησης και μεγαλύτερη ικανοποίηση για τεχνικά εγχειρίδια, καταλόγους προϊόντων και ψηφιακά βιβλία.

## Προαπαιτούμενα
- **Βιβλιοθήκες & Εξαρτήσεις**: Aspose.PDF for Java v25.3 ή νεότερη.  
- **Περιβάλλον**: JDK 8 ή νεότερο, εργαλείο κατασκευής Maven ή Gradle.  
- **Γνώση**: Βασικός προγραμματισμός Java και εξοικείωση με έννοιες PDF.

## Ρύθμιση Aspose.PDF για Java
### Εγκατάσταση Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Εγκατάσταση Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Απόκτηση Άδειας**: Ξεκινήστε με μια δωρεάν δοκιμή ή ζητήστε προσωρινή άδεια για πλήρη πρόσβαση σε όλες τις λειτουργίες. Σκεφτείτε την αγορά μόνιμης άδειας για χρήση σε παραγωγή.

### Βασική Αρχικοποίηση
Η κλάση `Document` είναι το βασικό αντικείμενο του Aspose.PDF που αντιπροσωπεύει ένα αρχείο PDF στη μνήμη. Μετά τη δημιουργία ενός στιγμιότυπου, όλες οι λειτουργίες ανάγνωσης/εγγραφής περνούν μέσω αυτού του αντικειμένου.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Οδηγός Υλοποίησης
### Πώς να Αλλάξετε τη Διάταξη Σελίδας PDF σε Java
**Επισκόπηση**: Ρυθμίστε τις προτιμήσεις προβολέα ώστε να εμφανίζει τις σελίδες όπως επιθυμείτε.

#### Αρχικοποίηση PdfContentEditor
`PdfContentEditor` είναι μια βοηθητική κλάση που σας επιτρέπει να τροποποιήσετε τις ρυθμίσεις προβολέα χωρίς να ξαναγράψετε ολόκληρο το έγγραφο.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Αλλαγή Προτιμήσεων Προβολέα
Για να ενεργοποιήσετε το **single page view pdf**, καλέστε `changeViewerPreference()` με την κατάλληλη τιμή enum. Αυτή η κλήση ενημερώνει το εσωτερικό λεξικό προτιμήσεων προβολέα του PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Αποθήκευση Ενημερωμένου Εγγράφου
Μετά την τροποποίηση των προτιμήσεων, καλέστε `save()` για να γράψετε τις αλλαγές πίσω στο δίσκο.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Πώς να Επεξεργαστείτε Σελιδοδείκτες PDF
**Απάντηση**: Για να τροποποιήσετε υπάρχοντες σελιδοδείκτες, φορτώστε το PDF με `Document`, ανακτήστε τη συλλογή περιγράμματος (outline), εντοπίστε το επιθυμητό `OutlineItem` και εκχωρήστε ένα νέο `ExplicitDestination` που δείχνει στη σωστή σελίδα και συντεταγμένες. Μετά την ενημέρωση κάθε σελιδοδείκτη, αποθηκεύστε το έγγραφο για να διατηρηθούν οι αλλαγές. Αυτό εξασφαλίζει ότι οι χρήστες κατευθύνονται ακριβώς στις προορισμένες ενότητες χωρίς επιπλέον κύλιση.

#### Πρόσβαση σε Σελιδοδείκτες
Η `OutlineItemCollection` αντιπροσωπεύει το ιεραρχικό δέντρο σελιδοδεικτών. Ανακτήστε την από το αντικείμενο `Document` για να εργαστείτε με μεμονωμένες καταχωρίσεις.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Ορισμός Νέου Προορισμού
Ένα `ExplicitDestination` ορίζει την ακριβή σελίδα και θέση στην οποία πρέπει να μεταβεί ένας σελιδοδείκτης. Εκχωρήστε το στην ιδιότητα `Destination` του στοιχείου περιγράμματος.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Αποθήκευση Αλλαγών
Διατηρήστε το ενημερωμένο δέντρο σελιδοδεικτών καλώντας `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Πώς να Ορίσετε Προορισμό Σελιδοδείκτη Κατά τη Δημιουργία PDF
**Απάντηση**: Κατά τη δημιουργία ενός PDF, μπορείτε να δημιουργήσετε σελιδοδείκτες άμεσα δημιουργώντας αντικείμενα `OutlineItem`, ορίζοντας τους τίτλους τους και ορίζοντας ένα `ExplicitDestination` που στοχεύει σε συγκεκριμένη σελίδα και τρόπο προβολής. Προσθέστε κάθε σελιδοδείκτη στη συλλογή περιγράμματος του εγγράφου πριν την αποθήκευση, ώστε το τελικό αρχείο να περιέχει ένα έτοιμο προς χρήση δέντρο πλοήγησης.

#### Δημιουργία και Διαμόρφωση Σελιδοδείκτη
`OutlineItem` αντιπροσωπεύει μία μοναδική καταχώριση σελιδοδείκτη στο περίγραμμα PDF. Όταν δημιουργείτε ένα PDF από το μηδέν, δημιουργήστε ένα νέο `OutlineItem` και προσθέστε το στη συλλογή περιγράμματος του εγγράφου.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Ορισμός Προορισμού Σελιδοδείκτη
Χρησιμοποιήστε `ExplicitDestination.createFitH(page, top)` για να τοποθετήσετε την προβολή στην κορυφή της επιλεγμένης σελίδας.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Προσθήκη και Αποθήκευση του PDF
Τέλος, προσθέστε το σελιδοδείκτη στο περίγραμμα και αποθηκεύστε το έγγραφο.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Πρακτικές Εφαρμογές
1. **Ψηφιακά Βιβλία** – Διασφαλίστε ότι κάθε σελιδοδείκτης κεφαλαίου καταλήγει στην κορυφή της σελίδας για μια απρόσκοπτη εμπειρία ανάγνωσης.  
2. **Τεχνικά Εγχειρίδια** – Η ακριβής πλοήγηση βοηθά τους μηχανικούς να βρίσκουν ενότητες γρήγορα, ιδιαίτερα σε μεγάλα PDF.  
3. **Κατάλογοι Προϊόντων** – Η διάταξη μίας σελίδας κάνει την περιήγηση σε καταλόγους σε tablet πιο διαισθητική.

## Σκέψεις για την Απόδοση
- **Βελτιστοποίηση Πόρων**: Το Aspose.PDF μπορεί να επεξεργαστεί PDF έως 2 GB χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, χάρη στην αρχιτεκτονική ροής του. Χρησιμοποιήστε `Document.optimizeResources()` για περαιτέρω μείωση του αποτυπώματος μνήμης.  
- **Διαχείριση Μνήμης Java**: Κλείστε ρητά τα streams και αφήστε τον garbage collector να ανακτήσει τα αντικείμενα μετά την επεξεργασία για να αποφύγετε διαρροές μνήμης.

## Συχνά Προβλήματα & Λύσεις
- **Οι σελιδοδείκτες δεν ενημερώνονται**: Επαληθεύστε ότι τροποποιείτε το σωστό δείκτη περιγράμματος (`get_Item(1)` αναφέρεται στον πρώτο σελιδοδείκτη κορυφαίου επιπέδου).  
- **Η προτίμηση προβολέα δεν εφαρμόζεται**: Βεβαιωθείτε ότι καλείτε `editor.save()` μετά την αλλαγή των προτιμήσεων· διαφορετικά οι αλλαγές παραμένουν μόνο στη μνήμη.  
- **Εξαιρέσεις άδειας**: Μια δοκιμαστική άδεια μπορεί να προσθέσει υδατογραφήματα· αποκτήστε πλήρη άδεια για παραγωγή.

## Συχνές Ερωτήσεις
**Ε: Ποιος είναι ο πιο εύκολος τρόπος φόρτωσης ενός εγγράφου PDF σε Java;**  
Α: Χρησιμοποιήστε `new Document("path/to/file.pdf")`; το Aspose.PDF ανιχνεύει αυτόματα τη μορφή του αρχείου.

**Ε: Μπορώ να αλλάξω τη διάταξη σελίδας χωρίς να χρησιμοποιήσω το PdfContentEditor;**  
Α: Ναι, μπορείτε να ορίσετε τις προτιμήσεις προβολέα απευθείας στο αντικείμενο `Document` μέσω `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Ε: Η αλλαγή της διάταξης προβολέα επηρεάζει την εκτύπωση;**  
Α: Η διάταξη προβολέα επηρεάζει μόνο την εμφάνιση στην οθόνη· δεν αλλάζει το εκτυπωμένο αποτέλεσμα.

**Ε: Υπάρχουν όρια στον αριθμό των σελιδοδεικτών που μπορώ να δημιουργήσω;**  
Α: Δεν υπάρχει σαφές όριο, αλλά πολύ μεγάλα δέντρα περιγράμματος μπορεί να επηρεάσουν την απόδοση· διατηρήστε τα οργανωμένα.

**Ε: Πώς μπορώ να διασφαλίσω ότι οι προορισμοί σελιδοδεικτών είναι ακριβείς μετά την προσθήκη ή αφαίρεση σελίδων;**  
Α: Επαναϋπολογίστε τους προορισμούς χρησιμοποιώντας τους τρέχοντες δείκτες σελίδων μετά από οποιεσδήποτε δομικές αλλαγές.

## Πόροι
- **Documentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Purchase**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporary License**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

**Τελευταία ενημέρωση:** 2026-05-28  
**Δοκιμάστηκε με:** Aspose.PDF for Java v25.3  
**Συγγραφέας:** Aspose

## Σχετικά Μαθήματα

- [Πώς να Αλλάξετε τις Προτιμήσεις Προβολέα PDF Χρησιμοποιώντας το Aspose.PDF για Java: Ένας Πλήρης Οδηγός](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Πώς να Δημιουργήσετε Σελιδοδείκτες PDF και να Διαχειριστείτε την Πλοήγηση Χρησιμοποιώντας το Aspose.PDF για Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Σελιδοδείκτες PDF και Μαθήματα Πλοήγησης για Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}