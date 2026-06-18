---
category: general
date: 2026-04-12
description: Πώς να διαβάσετε ένα έγγραφο Word και να εξάγετε συγκεκριμένη σελίδα
  από το Word χρησιμοποιώντας C#. Ο κώδικας βήμα‑βήμα δείχνει τη φόρτωση ενός .docx,
  την λήψη της σελίδας 2 και την ανάγνωση ενός αντικειμένου Bates.
draft: false
keywords:
- how to read word document
- extract specific page from word
- C# Word processing
- read .docx page
- document artifact extraction
language: el
og_description: Πώς να διαβάσετε ένα έγγραφο Word και να εξάγετε συγκεκριμένη σελίδα
  από το Word με πλήρες παράδειγμα C#. Μάθετε πώς να φορτώνετε ένα .docx, να στοχεύετε
  στη σελίδα 2 και να εξάγετε τους αριθμούς Bates.
og_title: Πώς να διαβάσετε ένα έγγραφο Word – Εξαγωγή συγκεκριμένης σελίδας από το
  Word σε C#
tags:
- C#
- Word
- Document Automation
title: Πώς να διαβάσετε έγγραφο Word και να εξάγετε συγκεκριμένη σελίδα από το Word
  – Οδηγός C#
url: /el/net/programming-with-document/how-to-read-word-document-and-extract-specific-page-from-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Διαβάσετε Έγγραφο Word και να Εξάγετε Συγκεκριμένη Σελίδα από το Word – Πλήρες Tutorial C#  

Έχετε αναρωτηθεί ποτέ **πώς να διαβάσετε ένα έγγραφο word** προγραμματιστικά και να πάρετε μόνο το τμήμα που χρειάζεστε; Ίσως να χτίζετε ένα σύστημα διαχείρισης υποθέσεων που πρέπει να εξάγει έναν αριθμό Bates από τη σελίδα 2 ενός νομικού εγγράφου. Σε αυτήν την περίπτωση θα χρειαστείτε να **εξάγετε συγκεκριμένη σελίδα από word** χωρίς να φορτώνετε ολόκληρο το αρχείο στη μνήμη κάθε φορά.  

Σε αυτόν τον οδηγό θα περάσουμε από μια πραγματική λύση: φόρτωση ενός `.docx`, επιλογή της δεύτερης σελίδας, εντοπισμός του πρώτου αντικειμένου “Bates” και εκτύπωση του κειμένου του. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project. Χωρίς ασαφείς «δείτε την τεκμηρίωση» συντομεύσεις—μόνο συγκεκριμένος κώδικας και εξηγήσεις του *γιατί* κάθε γραμμή είναι σημαντική.

> **Τι θα μάθετε**  
> * Πώς να διαβάσετε ένα έγγραφο Word σε C# με ένα δημοφιλές SDK.  
> * Πώς να **εξάγετε συγκεκριμένη σελίδα από word** χρησιμοποιώντας μηδενική (zero‑based) αρίθμηση.  
> * Πώς να αναζητήσετε ένα αντικείμενο (π.χ., αριθμό Bates) και να διαχειριστείτε τα ελλιπή δεδομένα με χάρη.  
> * Συμβουλές για ακραίες περιπτώσεις, απόδοση και περαιτέρω επεκτάσεις.

## Προαπαιτούμενα  

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| .NET 6.0 ή νεότερο (ή .NET Framework 4.7+) | Το SDK που θα χρησιμοποιήσουμε στοχεύει στο .NET Standard 2.0+. |
| Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε) | Για εύκολο debugging και IntelliSense. |
| **GroupDocs.Annotation for .NET** (ή Aspose.Words αν προτιμάτε) εγκατεστημένο μέσω NuGet | Παρέχει τις κλάσεις `Document`, `Page` και `Artifact` που χρησιμοποιούνται στο παράδειγμα. |
| Ένα δείγμα αρχείου Word (`input.docx`) τοποθετημένο σε φάκελο με όνομα `YOUR_DIRECTORY` | Το tutorial υποθέτει ότι το αρχείο υπάρχει· μπορείτε να αντικαταστήσετε τη διαδρομή με τη δική σας. |

Μπορείτε να προσθέσετε το πακέτο με:

```bash
dotnet add package GroupDocs.Annotation --version 23.10
```

Αν προτιμήσετε το Aspose.Words, το API διαφέρει ελαφρώς—αλλά η βασική ιδέα της φόρτωσης ενός εγγράφου, της πρόσβασης σε συλλογές σελίδων και της επανάληψης πάνω στα αντικείμενα παραμένει η ίδια.

![Diagram illustrating how to read word document and extract a single page](/images/read-word-document.png){: .center alt="Διάγραμμα που δείχνει πώς να διαβάσετε ένα έγγραφο word και να εξάγετε μια μόνο σελίδα"}

## Υλοποίηση Βήμα‑βήμα  

Παρακάτω χωρίζουμε τη λύση σε λογικά τμήματα. Κάθε τμήμα έχει σαφή επικεφαλίδα (καλό για AI indexing) και ένα μικρό απόσπασμα κώδικα που βασίζεται στο προηγούμενο.

### 1. Πώς να Διαβάσετε Έγγραφο Word – Φόρτωση του Αρχείου  

Το πρώτο πράγμα που κάνει οποιοσδήποτε κώδικας επεξεργασίας εγγράφων είναι να ανοίξει το αρχείο. Με το GroupDocs.Annotation δημιουργείτε ένα αντικείμενο `Document`, περνώντας τη πλήρη διαδρομή προς το `.docx`.  

```csharp
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

// Load the source document (replace YOUR_DIRECTORY with your actual path)
string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
Document doc = new Document(docPath);
```

**Γιατί είναι σημαντικό:**  
* Ο κατασκευαστής (constructor) αναλύει το αρχείο Word και δημιουργεί μια αναπαράσταση στη μνήμη των σελίδων, των σχολίων και των αντικειμένων.  
* Αν το αρχείο λείπει ή είναι κατεστραμμένο, το SDK ρίχνει μια περιγραφική `FileNotFoundException` ή `AnnotationException`, την οποία μπορείτε να πιάσετε αργότερα.

### 2. Εξάγετε Συγκεκριμένη Σελίδα από Word – Πρόσβαση στην Επιθυμητή Σελίδα  

Τα έγγραφα Word δεν εκθέτουν ένα εγγενές αντικείμενο “σελίδα” επειδή η σελιδοποίηση εξαρτάται από τη διάταξη. Το SDK, ωστόσο, αποδίδει το έγγραφο σε μια συλλογή αντικειμένων `Page` μετά τη φόρτωση. Οι σελίδες είναι μηδενικής βάσης, έτσι η σελίδα 2 έχει δείκτη 1.  

```csharp
// Retrieve the second page (zero‑based index)
int pageIndex = 1; // page 2 in human terms
Page secondPage = doc.Pages[pageIndex];
```

**Γιατί το χρειάζεστε:**  
* Η άμεση πρόσβαση στο `doc.Pages[1]` αποφεύγει την επανάληψη σε όλο το έγγραφο όταν σας ενδιαφέρει μόνο ένα τμήμα.  
* Αν το έγγραφο έχει λιγότερες σελίδες, θα ριχθεί `IndexOutOfRangeException`—χειριστείτε το για να κρατήσετε την εφαρμογή σας ανθεκτική (δείτε την ενότητα «Διαχείριση σφαλμάτων» παρακάτω).

### 3. Εντοπίστε ένα Αντικείμενο Bates – Αναζήτηση Μέσα στη Σελίδα  

Τα αντικείμενα (Artifacts) είναι μεταδεδομένα που συνδέονται με μια σελίδα—σκεφτείτε τα ως κρυφές σημειώσεις όπως αριθμούς Bates, σχόλια ή προσαρμοσμένες ετικέτες. Θα ψάξουμε για το πρώτο αντικείμενο του οποίου το `Subtype` ισούται με `"Bates"`.  

```csharp
// Find the first artifact with subtype "Bates"
Artifact batesArtifact = secondPage.Artifacts
    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));
```

**Γιατί αυτό το βήμα είναι κρίσιμο:**  
* Η χρήση του `FirstOrDefault` σας δίνει ένα ασφαλές null αποτέλεσμα αν δεν υπάρχει αντικείμενο Bates, επιτρέποντάς σας να αποφασίσετε πώς θα αντιδράσετε (καταγραφή, προεπιλεγμένη τιμή κ.λπ.).  
* Η προστασία `StringComparison.OrdinalIgnoreCase` αποτρέπει προβλήματα με διαφορετική κεφαλοποίηση στο πηγαίο έγγραφο.

### 4. Εμφάνιση του Κειμένου του Αντικειμένου – Ασφαλής Εκτύπωση στην Κονσόλα  

Τώρα που έχουμε (ή δεν έχουμε) ένα αντικείμενο Bates, απλώς εμφανίζουμε το κείμενό του. Αυτό αντικατοπτρίζει αυτό που μια πραγματική εφαρμογή μπορεί να αποθηκεύσει σε βάση δεδομένων ή να στείλει σε άλλη υπηρεσία.  

```csharp
if (batesArtifact != null)
{
    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
}
else
{
    Console.WriteLine("No Bates artifact found on page 2.");
}
```

**Τι να περιμένετε:**  
Η εκτέλεση του προγράμματος με ένα έγγραφο που περιέχει αριθμό Bates στη σελίδα 2 εκτυπώνει κάτι όπως:

```
Current Bates: 2023-00123
```

Αν το αντικείμενο λείπει, θα δείτε το μήνυμα εναλλακτικής λύσης, αποτρέποντας ένα `NullReferenceException`.

### 5. Πλήρες Παράδειγμα Εργασίας – Συνδυάστε Όλα Μαζί  

Παρακάτω είναι η πλήρης, έτοιμη για εκτέλεση κονσόλα εφαρμογή. Αντιγράψτε‑επικολλήστε την σε ένα νέο C# project, επαναφέρετε τα πακέτα NuGet και πατήστε **F5**.  

```csharp
using System;
using System.IO;
using System.Linq;
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

namespace WordPageExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the source document
                string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
                Document doc = new Document(docPath);

                // 2️⃣ Extract specific page from word (page 2 = index 1)
                int pageIndex = 1;
                if (pageIndex >= doc.Pages.Count)
                {
                    Console.WriteLine($"Document only has {doc.Pages.Count} page(s). Cannot access page {pageIndex + 1}.");
                    return;
                }
                Page secondPage = doc.Pages[pageIndex];

                // 3️⃣ Locate the first Bates artifact on that page
                Artifact batesArtifact = secondPage.Artifacts
                    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));

                // 4️⃣ Output the result
                if (batesArtifact != null)
                {
                    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
                }
                else
                {
                    Console.WriteLine("No Bates artifact found on page 2.");
                }
            }
            catch (Exception ex)
            {
                // Pro tip: Log the exception details for troubleshooting
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

**Επεξήγηση των επιπλέον τμημάτων:**  

* **Έλεγχος ορίων** – Επαληθεύουμε το `pageIndex` έναντι του `doc.Pages.Count` για να αποφύγουμε καταρρεύσεις σε σύντομα έγγραφα.  
* **Μπλοκ try‑catch** – Πιάνει σφάλματα πρόσβασης αρχείου, προβλήματα δικαιωμάτων ή εξαιρέσεις του SDK, παρέχοντάς σας καθαρό μήνυμα σφάλματος αντί για ακατέργαστο σφάλμα.  
* **Σχόλια** – Τα ενσωματωμένα σχόλια (`// 1️⃣`) λειτουργούν ως οπτικές αγκίστρες· είναι χρήσιμα για νέους που διαβάζουν γρήγορα τον κώδικα.

### 6. Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις  

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|-------------------------------|
| **Πολλαπλοί αριθμοί Bates στην ίδια σελίδα** | Χρησιμοποιήστε `Where(...).Select(a => a.Text)` για να ανακτήσετε όλα τα ταιριάσματα, έπειτα επαναλάβετε ή ενώστε τα. |
| **Χρειάζεστε τη σελίδα 5 αντί για τη σελίδα 2** | Αλλάξτε `int pageIndex = 4;` (θυμηθείτε ότι η αρίθμηση είναι μηδενική). |
| **Το έγγραφο χρησιμοποιεί διαφορετικό υποτύπο αντικειμένου (π.χ., “Comment”)** | Αντικαταστήστε `"Bates"` με `"Comment"` στην πρόταση `FirstOrDefault`. |
| **Απόδοση σε τεράστια έγγραφα** | Φορτώστε μόνο τη ζητούμενη σελίδα χρησιμοποιώντας `Document.LoadPage(pageIndex)` αν το SDK υποστηρίζει lazy loading. |
| **Εκτέλεση σε .NET Core σε Linux** | Βεβαιωθείτε ότι οι εγγενείς εξαρτήσεις του GroupDocs.Annotation είναι εγκατεστημένες (`libgdiplus` για απόδοση εικόνων). |

### 7. Συμβουλές & Προειδοποιήσεις  

* **Pro tip:** Αν επεξεργάζεστε πολλά έγγραφα σε batch, επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο άδειας `Annotation` για να αποφύγετε επαναλαμβανόμενους ελέγχους άδειας.  
* **Watch out for:** Word files that contain hidden sections (e.g., footnotes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}