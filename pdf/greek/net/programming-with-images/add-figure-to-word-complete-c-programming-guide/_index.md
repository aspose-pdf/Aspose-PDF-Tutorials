---
category: general
date: 2026-04-12
description: Προσθέστε σχήμα στο Word γρήγορα με C#. Μάθετε πώς να τοποθετήσετε το
  σχήμα στο Word, να εισάγετε σχήμα σε αρχείο docx και να προσθέσετε προσαρμοσμένο
  XML για προχωρημένη διάταξη.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: el
og_description: Προσθέστε σχήμα στο Word γρήγορα με C#. Μάθετε πώς να τοποθετείτε
  σχήμα στο Word, να εισάγετε σχήμα σε docx και να προσθέτετε προσαρμοσμένο XML για
  προχωρημένη διάταξη.
og_title: Προσθήκη Σχήματος στο Word – Πλήρης Οδηγός Προγραμματισμού C#
tags:
- C#
- Word Automation
- Document Generation
title: Προσθήκη Σχήματος στο Word – Πλήρης Οδηγός Προγραμματισμού C#
url: /el/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Σχήματος στο Word – Πλήρης Οδηγός Προγραμματισμού C#

Έχετε χρειαστεί ποτέ να **προσθέσετε σχήμα στο Word** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι. Σε πολλά έργα αυτοματισμού γραφείου το ελλιπές κομμάτι είναι μια ωραία τοποθετημένη εικόνα ή διάγραμμα που ζει μέσα σε ένα προσαρμοσμένο τμήμα XML. Αυτός ο οδηγός σας δείχνει ακριβώς πώς να **τοποθετήσετε σχήμα στο Word**, να εισάγετε το σχήμα σε ένα αρχείο *.docx* και ακόμη να ρυθμίσετε το υποκείμενο προσαρμοσμένο XML ώστε το σχήμα να συμπεριφέρεται όπως οποιοδήποτε ενσωματωμένο αντικείμενο του Word.

Θα περάσουμε από ένα πραγματικό παράδειγμα χρησιμοποιώντας τη βιβλιοθήκη GemBox.Document (δωρεάν για μικρά αρχεία, εμπορική για μεγαλύτερα φορτία εργασίας). Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο πρόγραμμα που τοποθετεί ένα σχήμα στις συντεταγμένες X = 50, Y = 200 μέσα σε ένα δοχείο με ετικέτα‑περιεχομένου. Χωρίς ασαφείς «δείτε την τεκμηρίωση» συντομεύσεις—απλός κώδικας, γιατί λειτουργεί, και συμβουλές που μπορείτε να αντιγράψετε απευθείας στο δικό σας έργο.

## Προαπαιτήσεις

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης με .NET Core 3.1)
- **GemBox.Document** πακέτο NuGet (`Install-Package GemBox.Document`)
- Ένα αρχικό αρχείο Word (`input.docx`) που ήδη περιέχει μια προσαρμοσμένη ετικέτα XML όπου θέλετε να εμφανιστεί το σχήμα
- Βασικές γνώσεις C# (θα δείτε γιατί κάθε γραμμή έχει σημασία)

> **Συμβουλή επαγγελματία:** Αν δεν έχετε ένα προ‑ετικετοποιημένο έγγραφο, μπορείτε να δημιουργήσετε ένα στο Word εισάγοντας έναν *Content Control* → *XML Mapping Pane* → αντιστοιχίστε ένα προσαρμοσμένο τμήμα XML. Η βιβλιοθήκη θα θεωρήσει αυτόν τον έλεγχο ως `TaggedContent`.

## Βήμα 1 – Φόρτωση του Πηγαίου Εγγράφου

Το πρώτο που κάνουμε είναι να ανοίξουμε το υπάρχον αρχείο *.docx*. Το `Document` είναι το σημείο εισόδου για όλες τις λειτουργίες της GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Γιατί;* Η φόρτωση του αρχείου μας δίνει πρόσβαση στα εσωτερικά του μέρη, συμπεριλαμβανομένων τυχόν προσαρμοσμένων XML containers. Χωρίς αυτό, δεν θα μπορούσαμε να εντοπίσουμε τον κόμβο `TaggedContent` που θα κρατήσει το σχήμα μας.

## Βήμα 2 – Πρόσβαση στο Tagged Content (Προσαρμοσμένο XML Container)

Το προσαρμοσμένο XML αποθηκεύεται μέσα σε έναν *content control* στο Word. Η GemBox το εκθέτει ως `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Αν το έγγραφο έχει πολλαπλές ετικετοποιημένες ενότητες, το `TaggedContent` επιστρέφει την **πρώτη**. Μπορείτε επίσης να κάνετε επανάληψη στο `doc.TaggedContents` για να επιλέξετε μια συγκεκριμένη ετικέτα με όνομα.

## Βήμα 3 – Δημιουργία του Στοιχείου Figure

Ένα `FigureElement` αντιπροσωπεύει μια εικόνα, διάγραμμα ή οποιοδήποτε οπτικό αντικείμενο που το Word θεωρεί ως *shape*. Θα το δημιουργήσουμε μέσα στο ετικετοποιημένο container.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Γιατί να δημιουργήσετε σχήμα εδώ;* Συνδέοντάς το με τον κόμβο προσαρμοσμένου XML, το Word γνωρίζει ότι το σχήμα ανήκει σε αυτή τη λογική ενότητα, κάτι που είναι κρίσιμο για μετέπειτα επεξεργασία ή ροές εργασίας βασισμένες σε content‑control.

## Βήμα 4 – Ακριβής Τοποθέτηση του Σχήματος

Το Word χρησιμοποιεί μονάδες point (1 pt ≈ 1/72 in) για την τοποθέτηση. Η δομή `PointF` μας επιτρέπει να ορίσουμε εύκολα τις συντεταγμένες X/Y.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Πώς να τοποθετήσετε shape στο Word:** Η ιδιότητα `Position` δέχεται ένα `PointF` όπου η πρώτη τιμή είναι η οριζόντια μετατόπιση (αριστερά) και η δεύτερη είναι η κάθετη μετατόπιση (πάνω) σε σχέση με το περιθώριο της σελίδας. Προσαρμόστε αυτούς τους αριθμούς για ακριβή τοποθέτηση.

## Βήμα 5 – Εισαγωγή του Σχήματος στο Δέντρο Tagged Content

Τώρα συνδέουμε το σχήμα με το στοιχείο ρίζας του δέντρου προσαρμοσμένου XML. Αυτό προσθέτει φυσικά το shape στο έγγραφο Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Σε αυτό το σημείο το σχήμα υπάρχει μέσα στο έγγραφο, αλλά δεν έχει ακόμη πηγή εικόνας. Ας προσθέσουμε ένα απλό PNG από το δίσκο.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Βήμα 6 – Αποθήκευση του Τροποποιημένου Εγγράφου

Τέλος, γράφουμε τις αλλαγές πίσω σε ένα νέο αρχείο *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Όταν ανοίξετε το `output.docx` στο Word, θα δείτε την εικόνα τοποθετημένη ακριβώς στο (50, 200) μέσα στο προσαρμοσμένο‑XML μπλοκ που στοχεύσατε.

### Πλήρες Παράδειγμα Εργασίας

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Το άνοιγμα του `output.docx` δείχνει το PNG τοποθετημένο ακριβώς όπου καθορίσατε, ενσωματωμένο μέσα στο προσαρμοσμένο τμήμα XML. Αν ελέγξετε το XML του εγγράφου (`.docx` → unzip → `word/document.xml`), θα δείτε ένα στοιχείο `<w:pict>` με τις σωστές συντεταγμένες `<v:shape>`.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το έγγραφο έχει πολλαπλές ετικετοποιημένες ενότητες;

Χρησιμοποιήστε το `doc.TaggedContents` για να κάνετε επανάληψη και να επιλέξετε με βάση το όνομα της ετικέτας:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Πώς να προσθέσετε λεζάντα στο σχήμα;

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Λειτουργεί αυτό με Word 2010 και νεότερα;

Ναι. Η GemBox.Document στοχεύει στο πρότυπο Open XML, το οποίο είναι συμβατό με Word 2007 + (συμπεριλαμβανομένων των 2010, 2013, 2016, 2019, και Microsoft 365).

### Τι γίνεται αν χρειαστεί να περιστρέψετε το shape;

```csharp
figure.Rotation = 45; // degrees
```

### Πώς να προσθέσετε διανυσματικό γραφικό αντί για ραστερ εικόνα;

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Συμβουλές & Πιθανά Προβλήματα

- **Διαδρομές αρχείων:** Χρησιμοποιήστε `Path.Combine` για να αποφύγετε σκληρά κωδικοποιημένους διαχωριστές, ειδικά σε πλατφόρμες που δεν είναι Windows.
- **Όρια άδειας:** Η δωρεάν άδεια GemBox περιορίζει το μέγεθος του εγγράφου στα 20 KB. Για μεγαλύτερα αρχεία, αγοράστε εμπορικό κλειδί.
- **Απόδοση:** Η επαναχρησιμοποίηση μιας μόνο παρουσίας `Document` για επεξεργασία σε batch μειώνει δραστικά το φορτίο μνήμης.
- **Υπερχείλιση σχήματος:** Αν οι διαστάσεις του σχήματος υπερβαίνουν τα περιθώρια της σελίδας, το Word θα το κόψει. Προσαρμόστε τα `figure.Width` και `figure.Height` αναλόγως.

## Συμπέρασμα

Τώρα ξέρετε **πώς να προσθέσετε σχήμα στο Word**, ακριβώς **πώς να τοποθετήσετε σχήμα στο Word**, και πώς να χειριστείτε το υποκείμενο προσαρμοσμένο XML ώστε το shape να συμπεριφέρεται όπως οποιοδήποτε ενσωματωμένο στοιχείο. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει κάθε βήμα—από τη φόρτωση του εγγράφου, τη δημιουργία ενός `FigureElement`, τον καθορισμό των συντεταγμένων, την προσθήκη μιας εικόνας, και τελικά την αποθήκευση του ενημερωμένου *.docx*.

Στη συνέχεια, δοκιμάστε να πειραματιστείτε με **insert figure into docx** προσθέτοντας πολλαπλά σχήματα, χρησιμοποιώντας βρόχους, ή δημιουργώντας διαγράμματα εν κινήσει. Μπορείτε επίσης να εξερευνήσετε **how to add custom xml** για πιο πλούσιους ελέγχους περιεχομένου ή να μάθετε **how to position shape word** σε πίνακες και κεφαλίδες. Οι δυνατότητες είναι απεριόριστες, και με τις βασικές αρχές που καλύφθηκαν εδώ είστε έτοιμοι να αυτοματοποιήσετε έγγραφα Word σαν επαγγελματίας.

Καλό κώδικα, και μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε δυσκολίες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}