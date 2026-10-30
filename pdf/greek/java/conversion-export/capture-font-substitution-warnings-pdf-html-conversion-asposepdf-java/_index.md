---
date: '2026-09-22'
description: Μάθετε πώς να καταγράψετε προειδοποιήσεις αντικατάστασης γραμματοσειράς
  κατά τη μετατροπή PDF σε HTML με Aspose.PDF for Java, εξασφαλίζοντας accurate rendering
  και ανίχνευση missing fonts.
keywords:
- pdf to html java
- pdf to html aspose
- detect missing fonts pdf
- Aspose.PDF
- Java
lastmod: '2026-09-22'
og_description: Καταγράψτε προειδοποιήσεις αντικατάστασης γραμματοσειράς κατά τη μετατροπή
  PDF σε HTML με Aspose.PDF for Java. Detect missing fonts and ensure accurate rendering.
og_image_alt: Tutorial showing how to log font substitutions during PDF to HTML conversion
  using Aspose.PDF for Java
og_title: Καταγραφή προειδοποιήσεων αντικατάστασης γραμματοσειράς κατά τη μετατροπή
  pdf σε html σε Java
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to capture font substitution warnings while converting PDF
    to HTML with Aspose.PDF for Java, ensuring accurate rendering and detecting missing
    fonts.
  headline: How to capture font substitution warnings during pdf to html conversion
    in Java
  type: TechArticle
- description: Learn how to capture font substitution warnings while converting PDF
    to HTML with Aspose.PDF for Java, ensuring accurate rendering and detecting missing
    fonts.
  name: How to capture font substitution warnings during pdf to html conversion in
    Java
  steps:
  - name: load your PDF document
    text: (Already shown above) Loading the document gives you access to its content
      and font information.
  - name: set up a font substitution handler
    text: The `FontSubstitutionHandler` interface lets you receive a callback each
      time Aspose.PDF replaces a font. Register a handler that logs each substitution
      into a map for later inspection. **Why this matters:** If the conversion swaps
      a proprietary font with a generic one, the HTML may render with unex
  - name: configure HTML save options
    text: The `HtmlSaveOptions` class controls how the PDF is saved as HTML. You can
      fine‑tune page splitting, font embedding, image compression, and more. You can
      further customize properties such as `SplitIntoPages`, `EmbedFonts`, or `ImageCompression`
      depending on your project needs.
  - name: save the converted document
    text: Finally, write the HTML output to disk. After execution, inspect the `names`
      map to see which fonts were substituted. If you notice unexpected entries, consider
      embedding the missing fonts or adjusting the conversion settings.
  type: HowTo
- questions:
  - answer: Yes. Aspose.PDF provides similar font‑substitution events for most conversion
      targets.
    question: Can I use this approach with other output formats (e.g., DOCX)?
  - answer: Inspect the `pdfDoc.getFontInfo()` collection or rely on the substitution
      handler during conversion.
    question: How do I detect missing fonts pdf before conversion?
  - answer: Set `htmlSaveOps.setEmbedFonts(true)`; Aspose.PDF will embed any available
      fonts, but truly missing fonts must be supplied manually.
    question: Is there a way to automatically embed missing fonts?
  - answer: 'Yes, as long as you provide the password when loading the document: `new
      Document(path, new LoadOptions(password))`.'
    question: Does this work with encrypted PDFs?
  - answer: The overhead of logging substitutions is minimal, typically adding only
      a few milliseconds.
    question: Will this increase conversion time?
  type: FAQPage
tags:
- pdf to html
- Aspose.PDF
- Java conversion
- font substitution
title: Πώς να καταγράψετε προειδοποιήσεις αντικατάστασης γραμματοσειράς κατά τη μετατροπή
  pdf σε html σε Java
url: /el/java/conversion-export/capture-font-substitution-warnings-pdf-html-conversion-asposepdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή PDF σε HTML: καταγραφή προειδοποιήσεων αντικατάστασης γραμματοσειράς με το Aspose.PDF for Java

## Εισαγωγή

Όταν εκτελείτε μια **pdf to html conversion**, η αντικατάσταση γραμματοσειράς μπορεί σιωπηρά να αλλάξει την εμφάνιση των σελίδων σας, προκαλώντας μετατοπίσεις διάταξης ή ελλιπή χαρακτήρες. Η καταγραφή αυτών των προειδοποιήσεων σας επιτρέπει να επαληθεύσετε ότι η μετατροπή διατηρεί το αρχικό σχέδιο και βοηθά στην ανίχνευση ελλιπών γραμματοσειρών pdf πριν γίνουν πρόβλημα. Σε αυτό το σεμινάριο, θα μάθετε πώς να συνδέσετε τη διαδικασία μετατροπής του Aspose.PDF for Java, να καταγράψετε τυχόν αλλαγές γραμματοσειράς και να αποθηκεύσετε το παραγόμενο αρχείο HTML με σιγουριά.

**Τι θα επιτύχετε**
- Κατανοήστε γιατί η παρακολούθηση της αντικατάστασης γραμματοσειράς είναι σημαντική για τη pdf to html conversion.  
- Ρυθμίστε έναν διαχειριστή αντικατάστασης γραμματοσειράς που καταγράφει κάθε αλλαγή γραμματοσειράς.  
- Διαμορφώστε το `HtmlSaveOptions` για να βελτιστοποιήσετε την έξοδο της μετατροπής.

Ας βεβαιωθούμε ότι έχετε όλα όσα χρειάζεστε πριν προχωρήσουμε.

## Γρήγορες Απαντήσεις
- **Τι κάνει ο διαχειριστής αντικατάστασης γραμματοσειράς;** Καταγράφει το αρχικό όνομα γραμματοσειράς και τη γραμματοσειρά που αντικαθιστά το Aspose.PDF κατά τη μετατροπή.  
- **Μπορώ να το χρησιμοποιήσω με έργα pdf to html java;** Ναι, ο κώδικας λειτουργεί με οποιαδήποτε εφαρμογή Java που αναφέρεται στο Aspose.PDF.  
- **Χρειάζομαι άδεια για παραγωγική χρήση;** Απαιτείται έγκυρη άδεια Aspose.PDF για εμπορικές αναπτύξεις.  
- **Θα εντοπιστούν αυτόματα οι ελλιπείς γραμματοσειρές;** Ο διαχειριστής καταγράφει κάθε αντικατάσταση, επιτρέποντάς σας έτσι να εντοπίσετε ελλιπείς γραμματοσειρές pdf.  
- **Απαιτείται κάποια πρόσθετη διαμόρφωση;** Μόνο η τυπική ρύθμιση του Aspose.PDF και η καταχώρηση του διαχειριστή όπως φαίνεται παρακάτω.

## Τι είναι η μετατροπή pdf σε html;

Η μετατροπή pdf σε html δημιουργεί μια αναπαράσταση HTML ενός PDF, διατηρώντας τη διάταξη, τις γραμματοσειρές, τις εικόνες και το κείμενο ώστε το έγγραφο να μπορεί να προβληθεί σε οποιονδήποτε web browser χωρίς πρόσθετο PDF. Η διαδικασία εξάγει τις σελίδες, μετατρέπει τα διανυσματικά γραφικά σε στοιχεία HTML και ενσωματώνει ή αντικαθιστά τις γραμματοσειρές, παράγοντας ένα αρχείο φιλικό στο web που αντικατοπτρίζει όσο το δυνατόν πιο πιστά την εμφάνιση του αρχικού PDF.

## Γιατί να καταγράψετε προειδοποιήσεις αντικατάστασης γραμματοσειράς;

Η καταγραφή των προειδοποιήσεων αντικατάστασης γραμματοσειράς σας επιτρέπει να δείτε ακριβώς ποιες γραμματοσειρές αντικαταστάθηκαν κατά τη pdf to html conversion, ώστε να αντιμετωπίσετε ελλιπείς γραμματοσειρές, να ενσωματώσετε τις απαιτούμενες γραμματοσειρές και να διατηρήσετε την οπτική πιστότητα σε διαφορετικά browsers. Καταγράφοντας κάθε αντικατάσταση μπορείτε:
- Να εντοπίσετε νωρίς τις ελλιπείς γραμματοσειρές.  
- Να επιλέξετε την ενσωμάτωση των απαιτούμενων γραμματοσειρών.  
- Να παρέχετε μια εναλλακτική στρατηγική για τους τελικούς χρήστες.

## Προαπαιτούμενα

- **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη.  
- **IDE** – IntelliJ IDEA, Eclipse ή οποιοσδήποτε επεξεργαστής προτιμάτε.  
- **Εργαλείο κατασκευής** – Maven ή Gradle (παρέχονται παραδείγματα και για τα δύο).  
- **Βασικές γνώσεις Java** – αρκετές για να δημιουργήσετε μια απλή μέθοδο `main` και να εκτελέσετε τον κώδικα.

## Ρύθμιση Aspose.PDF for Java

### 1. Προσθέστε την εξάρτηση Aspose.PDF
Χρησιμοποιήστε το απόσπασμα που ταιριάζει στο σύστημα κατασκευής σας.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### 2. Αποκτήστε και εφαρμόστε άδεια
- Αποκτήστε μια δωρεάν δοκιμαστική άδεια για να εξερευνήσετε όλες τις δυνατότητες χωρίς περιορισμούς (κατεβάστε τη δοκιμαστική άδεια [εδώ](https://purchase.aspose.com/temporary-license/)).  
- Για παραγωγική χρήση, αγοράστε μόνιμη άδεια ή μια προσωρινή από την Aspose (αγορά άδειας [εδώ](https://purchase.aspose.com/temporary-license/)).

### 3. Φορτώστε το PDF έγγραφό σας
Η κλάση `Document` είναι το κορυφαίο αντικείμενο του Aspose.PDF που αντιπροσωπεύει ένα μόνο αρχείο PDF στη μνήμη. Δημιουργήστε μια παρουσία `Document` που δείχνει στο πηγαίο PDF.

```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDoc = new Document(dataDir + "input1.pdf");
```

## Οδηγός υλοποίησης

### Λειτουργία: προειδοποίηση αντικατάστασης γραμματοσειράς στη μετατροπή pdf σε html

#### Βήμα 1: φορτώστε το PDF έγγραφό σας
(Ήδη εμφανίζεται παραπάνω) Η φόρτωση του εγγράφου σας δίνει πρόσβαση στο περιεχόμενο και τις πληροφορίες γραμματοσειράς.

#### Βήμα 2: ρυθμίστε έναν διαχειριστή αντικατάστασης γραμματοσειράς
Η διεπαφή `FontSubstitutionHandler` σας επιτρέπει να λαμβάνετε κλήση κάθε φορά που το Aspose.PDF αντικαθιστά μια γραμματοσειρά. Καταχωρήστε έναν διαχειριστή που καταγράφει κάθε αντικατάσταση σε έναν χάρτη για μετέπειτα έλεγχο.

```java
final Map<String, String> names = new HashMap<>();
pdfDoc.FontSubstitution.add(new Document.FontSubstitutionHandler() {
    public void invoke(Font font, Font newFont) {
        // Log substituted FontNames into a map.
        names.put(font.getFontName(), newFont.getFontName());
    }
});
```

**Γιατί είναι σημαντικό:**  
Εάν η μετατροπή αντικαταστήσει μια ιδιόκτητη γραμματοσειρά με μια γενική, το HTML μπορεί να εμφανιστεί με απρόσμενα κενά ή ελλιπή σύμβολα. Ο χάρτης `names` παρέχει ένα σαφές ίχνος ελέγχου.

#### Βήμα 3: διαμορφώστε τις επιλογές αποθήκευσης HTML
Η κλάση `HtmlSaveOptions` ελέγχει πώς αποθηκεύεται το PDF ως HTML. Μπορείτε να ρυθμίσετε λεπτομερώς το διαχωρισμό σελίδων, την ενσωμάτωση γραμματοσειρών, τη συμπίεση εικόνων και άλλα.

```java
HtmlSaveOptions htmlSaveOps = new HtmlSaveOptions();
```

Μπορείτε να προσαρμόσετε περαιτέρω ιδιότητες όπως `SplitIntoPages`, `EmbedFonts` ή `ImageCompression` ανάλογα με τις ανάγκες του έργου σας.

#### Βήμα 4: αποθηκεύστε το μετατρεπόμενο έγγραφο
Τέλος, γράψτε το αποτέλεσμα HTML στο δίσκο.

```java
pdfDoc.save("YOUR_OUTPUT_DIRECTORY/getWarningForFontSubstitution.html\
```

Μετά την εκτέλεση, ελέγξτε τον χάρτη `names` για να δείτε ποιες γραμματοσειρές αντικαταστάθηκαν. Εάν παρατηρήσετε ανεπιθύμητες καταχωρήσεις, σκεφτείτε την ενσωμάτωση των ελλιπών γραμματοσειρών ή την προσαρμογή των ρυθμίσεων μετατροπής.

## Γιατί να χρησιμοποιήσετε το Aspose.PDF for Java;

Το Aspose.PDF υποστηρίζει πάνω από 50 μορφές εισόδου και εξόδου — συμπεριλαμβανομένων PDF, DOCX, XLSX, PPTX, HTML και κοινών τύπων εικόνων — και μπορεί να επεξεργαστεί έγγραφα εκατοντάδων σελίδων χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη. Η βιβλιοθήκη προσφέρει ένα ειδικό γεγονός αντικατάστασης γραμματοσειράς, που την καθιστά ιδανική για αξιόπιστες ροές εργασίας pdf to html java.

## Κοινά προβλήματα & αντιμετώπιση

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Δεν υπάρχουν καταχωρήσεις στον χάρτη `names` | Η αντικατάσταση γραμματοσειράς είναι απενεργοποιημένη ή όλες οι γραμματοσειρές είναι ενσωματωμένες | Βεβαιωθείτε ότι το `EmbedFonts` είναι ορισμένο σε `false` στο `HtmlSaveOptions` αν θέλετε να δείτε τις αντικαταστάσεις. |
| Η διάταξη HTML είναι χαλασμένη | Η αντικατεστημένη γραμματοσειρά δεν διαθέτει τα απαιτούμενα σύμβολα | Ενσωματώστε τη λείπουσα γραμματοσειρά ή παρέχετε εναλλακτικό CSS που ταιριάζει στο αρχικό σχέδιο. |
| Η μέθοδος `pdfDoc.save` ρίχνει εξαίρεση | Λάθος διαδρομή εξόδου ή έλλειψη δικαιωμάτων εγγραφής | Επαληθεύστε ότι ο φάκελος `YOUR_OUTPUT_DIRECTORY` υπάρχει και είναι εγγράψιμος. |

## Συχνές ερωτήσεις

**Μ: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση με άλλες μορφές εξόδου (π.χ., DOCX);**  
Α: Ναι. Το Aspose.PDF παρέχει παρόμοια γεγονότα αντικατάστασης γραμματοσειράς για τους περισσότερους στόχους μετατροπής.

**Μ: Πώς μπορώ να εντοπίσω ελλιπείς γραμματοσειρές pdf πριν από τη μετατροπή;**  
Α: Εξετάστε τη συλλογή `pdfDoc.getFontInfo()` ή βασιστείτε στον διαχειριστή αντικατάστασης κατά τη μετατροπή.

**Μ: Υπάρχει τρόπος να ενσωματωθούν αυτόματα οι ελλιπείς γραμματοσειρές;**  
Α: Ορίστε `htmlSaveOps.setEmbedFonts(true)`· το Aspose.PDF θα ενσωματώσει όλες τις διαθέσιμες γραμματοσειρές, αλλά οι πραγματικά λείπουσες γραμματοσειρές πρέπει να παρασχεθούν χειροκίνητα.

**Μ: Λειτουργεί αυτό με κρυπτογραφημένα PDF;**  
Α: Ναι, εφόσον παρέχετε τον κωδικό πρόσβασης κατά τη φόρτωση του εγγράφου: `new Document(path, new LoadOptions(password))`.

**Μ: Θα αυξήσει αυτό τον χρόνο μετατροπής;**  
Α: Η επιβάρυνση της καταγραφής των αντικαταστάσεων είναι ελάχιστη, συνήθως προσθέτει μόνο μερικά χιλιοστά του δευτερολέπτου.

---

**Last Updated:** 2026-09-22  
**Tested With:** Aspose.PDF 25.3 for Java  
**Author:** Aspose

## Σχετικά Μαθήματα

- [Μετατροπή PDF σε HTML με Αντικατάσταση Γραμματοσειράς Χρησιμοποιώντας το Aspose.PDF for Java](/pdf/java/conversion-export/pdf-to-html-conversion-font-substitution-aspose-pdf-java/)
- [pdf to html java – Μετατροπή PDF σε HTML με Ενσωματωμένους Πόρους Χρησιμοποιώντας το Aspose.PDF for Java](/pdf/java/conversion-export/convert-pdf-to-html-aspose-java-embedded-resources/)
- [Μετατροπή PDF σε Πολυσελίδα HTML Χρησιμοποιώντας το Aspose.PDF for Java: Ολοκληρωμένος Οδηγός](/pdf/java/conversion-export/convert-pdf-to-multipage-html-aspose-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}