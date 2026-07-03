---
date: '2026-07-03'
description: Μάθετε πώς να προσθέσετε την Aspose PDF Maven dependency και να μετατρέψετε
  PDF σε XPS με επιλέξιμο κείμενο χρησιμοποιώντας Aspose.PDF for Java. Οδηγός βήμα‑βήμα
  με προαπαιτούμενα και Συχνές Ερωτήσεις.
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: Aspose PDF Maven Dependency – Μετατροπή PDF σε XPS (Java)
url: /el/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven Dependency – Μετατροπή PDF σε XPS (Java)

## Εισαγωγή

Αν χρειάζεστε να **προσθέσετε την εξάρτηση Aspose PDF Maven** και στη συνέχεια να μετατρέψετε έγγραφα PDF σε XPS διατηρώντας το κείμενο επιλέξιμο, βρίσκεστε στο σωστό μέρος. Αυτό το σεμινάριο σας καθοδηγεί βήμα προς βήμα—από τη διαμόρφωση του Maven ή Gradle, στη φόρτωση ενός PDF, στη ρύθμιση των επιλογών XPS, και τέλος στην αποθήκευση ενός αρχείου XPS με επιλέξιμο κείμενο. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Γρήγορες Απαντήσεις
- **Τι εξάρτηση χρειάζομαι;** `com.aspose:aspose-pdf` (Maven) ή το ισοδύναμο Gradle artifact.  
- **Μπορεί το XPS να διατηρήσει επιλέξιμο κείμενο;** Ναι—Aspose.PDF διατηρεί αυτόματα τα στρώματα κειμένου.  
- **Ποια έκδοση Java απαιτείται;** JDK 8 ή νεότερη.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται έγκυρη άδεια Aspose.PDF για απεριόριστη χρήση.  
- **Πόσο χρόνο διαρκεί η μετατροπή;** Συνήθως κάτω από ένα δευτερόλεπτο για αρχεία κάτω από 100 σελίδες σε τυπικό υλικό.

## Τι είναι η εξάρτηση Aspose PDF Maven;
Το Maven artifact `aspose-pdf` παρέχει το πλήρες API Aspose.PDF for Java, επιτρέποντας τη δημιουργία, τη διαχείριση και τη μετατροπή PDF χωρίς εξωτερικό λογισμικό. Η προσθήκη αυτής της εξάρτησης στο `pom.xml` ή στο `build.gradle` κατεβάζει όλα τα απαιτούμενα δυαδικά αρχεία, ώστε να μπορείτε να αρχίσετε να κωδικοποιείτε αμέσως χωρίς χειροκίνητη διαχείριση JAR.

## Γιατί να μετατρέψετε PDF σε XPS με επιλέξιμο κείμενο;
Το Aspose.PDF υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να δημιουργήσει αρχεία XPS που διατηρούν ένα αναζητήσιμο, επιλέξιμο στρώμα κειμένου. Αυτό είναι κρίσιμο για ροές εργασίας που απαιτούν αρχεία αρχειοθέτησης, ακριβή διατήρηση διάταξης ή επεξεργασία σε εργαλεία που υποστηρίζουν XPS. Οι μετατροπές ολοκληρώνονται σε λιγότερο από ένα δευτερόλεπτο για τυπικά PDF 20 σελίδων σε σύγχρονο CPU.

## Προαπαιτούμενα

- **Java Development Kit (JDK) 8+** εγκατεστημένο και `JAVA_HOME` ρυθμισμένο.  
- **Maven 3.6+** ή **Gradle 6+** για **διαχείριση εξαρτήσεων**.  
- Βασική εξοικείωση με **Java file I/O** και **διαχείριση εξαιρέσεων**.  

### Απαιτούμενες βιβλιοθήκες και εξαρτήσεις

Θα χρειαστείτε τη βιβλιοθήκη Aspose.PDF for Java έκδοση 25.3 ή νεότερη. Συμπεριλάβετε την χρησιμοποιώντας ένα από τα παρακάτω εργαλεία κατασκευής:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### Ρύθμιση Περιβάλλοντος

Βεβαιωθείτε ότι το IDE ή το περιβάλλον κατασκευής σας δείχνει στη σωστή JDK και ότι το δίκτυο μπορεί να φτάσει στο Maven Central ή στο ιδιωτικό σας αποθετήριο.

## Πώς να προσθέσετε την εξάρτηση Aspose PDF Maven;

`aspose-pdf` είναι το artifact που **προσθέτετε** στο αρχείο κατασκευής του έργου σας, στη συνέχεια **ανανεώνετε** τις εξαρτήσεις ώστε τα JAR να κατεβαίνουν αυτόματα. Για **Maven**, εισάγετε το μπλοκ `<dependency>` μέσα στο `<dependencies>`· για **Gradle**, τοποθετήστε τη γραμμή `implementation` μέσα στο μπλοκ `dependencies`. Μετά την ανανέωση, οι κλάσεις Aspose γίνονται διαθέσιμες στο classpath, και μπορείτε να **ξεκινήσετε** την κωδικοποίηση χωρίς χειροκίνητη διαχείριση JAR.

## Ρύθμιση Aspose.PDF για Java

### Βήματα εγκατάστασης

1. **Ρύθμιση Maven/Gradle:** Προσθέστε την εξάρτηση όπως φαίνεται παραπάνω και εκτελέστε `mvn clean install` ή `gradle build` για να κατεβάσετε τη βιβλιοθήκη.  
2. **Απόκτηση άδειας:**  
   - Κατεβάστε μια [δωρεάν δοκιμή](https://releases.aspose.com/pdf/java/) ή αποκτήστε μια [προσωρινή άδεια](https://purchase.aspose.com/temporary-license/).  
   - Τοποθετήστε το αρχείο άδειας (`Aspose.Pdf.lic`) σε φάκελο προσβάσιμο στην εφαρμογή σας και **φορτώστε** το κατά την **εκκίνηση**.

### Βασική αρχικοποίηση

`License` εφαρμόζει ένα αρχείο άδειας Aspose για να ξεκλειδώσει πλήρη λειτουργικότητα.  
Φορτώστε την άδεια (αν **έχετε** μία) και δημιουργήστε ένα αντικείμενο `Document` για εργασία με PDF.  
`Document` αντιπροσωπεύει ένα αρχείο PDF και παρέχει μεθόδους για τη διαχείριση του περιεχομένου του.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Πώς να μετατρέψετε PDF σε XPS με επιλέξιμο κείμενο;

`XpsSaveOptions` διαμορφώνει τις ρυθμίσεις για την αποθήκευση ενός PDF ως έγγραφο XPS, συμπεριλαμβανομένης της διατήρησης του κειμένου.  
Φορτώστε το πηγαίο PDF, ρυθμίστε το `XpsSaveOptions` ώστε να διατηρεί το κείμενο, και καλέστε `save` με την επέκταση `.xps`. Το API ενσωματώνει αυτόματα ένα στρώμα κειμένου, έτσι ώστε το παραγόμενο XPS να μπορεί να αναζητηθεί και να αντιγραφεί όπως το αρχικό PDF. Ολόκληρη αυτή η διαδικασία συνήθως απαιτεί μόνο τρεις γραμμές κώδικα μετά τη ρύθμιση της βιβλιοθήκης.

## Οδηγός υλοποίησης

### Μετατροπή PDF σε XPS

Αυτή η δυνατότητα σας επιτρέπει να μετατρέψετε ένα έγγραφο PDF σε αρχείο XPS χρησιμοποιώντας το Aspose.PDF for Java.

#### Βήμα 1: Φόρτωση του PDF εγγράφου

Αρχικά, φορτώστε το PDF έγγραφό σας από τον φάκελό του:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Βήμα 2: Διαμόρφωση επιλογών αποθήκευσης

Δημιουργήστε μια παρουσία του `XpsSaveOptions` για να ρυθμίσετε τις επιλογές μετατροπής XPS:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Βήμα 3: Αποθήκευση ως αρχείο XPS

Τέλος, αποθηκεύστε το έγγραφο σε μορφή XPS στον επιθυμητό φάκελο εξόδου:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Κοινά προβλήματα και λύσεις

- **Κενές σελίδες στο αρχείο XPS:** Βεβαιωθείτε ότι το PDF δεν χρησιμοποιεί κρυπτογραφημένα ρεύματα· αν το κάνει, παρέχετε τον κωδικό πρόσβασης κατά τη φόρτωση του `Document`.  
- **Σφάλματα μνήμης σε μεγάλα PDF:** Χρησιμοποιήστε `Document.optimizeResources()` πριν την αποθήκευση για να μειώσετε το αποτύπωμα μνήμης.  
- **Απουσία γραμματοσειρών:** Εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον διακομιστή ή ενσωματώστε τις στο PDF πριν τη μετατροπή.

## Συχνές ερωτήσεις

**Ε: Μπορώ να μετατρέψω PDF με κωδικό πρόσβασης;**  
Α: Ναι—περάστε τον κωδικό πρόσβασης στον κατασκευαστή `Document` ή χρησιμοποιήστε `Document.open(String path, String password)` πριν τη μετατροπή.

**Ε: Διατηρεί το XPS τα διανυσματικά γραφικά;**  
Α: Απόλυτα. Όλα τα διανυσματικά σχήματα, οι εικόνες και το κείμενο διατηρούνται, και το κείμενο παραμένει επιλέξιμο.

**Ε: Είναι η άδεια υποχρεωτική για την δοκιμαστική έκδοση;**  
Α: Η δοκιμαστική έκδοση λειτουργεί χωρίς άδεια αλλά προσθέτει υδατογράφημα στο αποτέλεσμα· μια μόνιμη άδεια αφαιρεί όλους τους περιορισμούς.

**Ε: Πώς το Aspose.PDF διαχειρίζεται μεγάλα αρχεία;**  
Α: Επεξεργάζεται τα αρχεία με ροή, επιτρέποντας τη μετατροπή PDF με εκατοντάδες σελίδες χωρίς να φορτώνει ολόκληρο το έγγραφο στη μνήμη.

**Ε: Ποιες πλατφόρμες υποστηρίζονται;**  
Α: Η βιβλιοθήκη εκτελείται σε οποιοδήποτε λειτουργικό σύστημα με συμβατό JDK, συμπεριλαμβανομένων των Windows, Linux και macOS.

---

**Τελευταία ενημέρωση:** 2026-07-03  
**Δοκιμάστηκε με:** Aspose.PDF for Java 25.3  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά σεμινάρια

- [Μετατροπή PDF σε JPEG χρησιμοποιώντας Aspose.PDF for Java: Οδηγός βήμα‑βήμα](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Πώς να μετατρέψετε PDF σε Excel χρησιμοποιώντας Aspose.PDF for Java | Οδηγός βήμα‑βήμα](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Πώς να μετατρέψετε αρχεία XPS σε PDF χρησιμοποιώντας Aspose.PDF σε Java: Πλήρης οδηγός](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}