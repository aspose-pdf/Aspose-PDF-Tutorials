---
category: general
date: 2026-04-25
description: Επανάληψη συλλογής C# γρήγορα με ένα σαφές παράδειγμα βρόχου foreach.
  Μάθετε πώς να λαμβάνετε τα ονόματα αντικειμένων και να εμφανίζετε λίστα συμβολοσειρών
  σε λίγα μόνο βήματα.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: el
og_description: Επανάληψη συλλογής C# χρησιμοποιώντας παράδειγμα βρόχου foreach. Ανακαλύψτε
  πώς να λαμβάνετε τα ονόματα αντικειμένων και να εμφανίζετε μια λίστα συμβολοσειρών
  αποδοτικά.
og_title: Επανάληψη Συλλογής C# – Βήμα‑βήμα βρόχος στα στοιχεία
tags:
- C#
- collections
- loops
title: Επανάληψη Συλλογής C# – Απλός Οδηγός για την Επανάληψη των Στοιχείων
url: /el/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επανάληψη Συλλογής C# – Πώς να Επαναλάβετε Στοιχεία με Παράδειγμα Βρόχου foreach

Έχετε ποτέ χρειαστεί να **iterate collection C#** αλλά δεν ήσασταν σίγουροι ποια κατασκευή σας δίνει τον πιο καθαρό κώδικα; Δεν είστε μόνοι. Σε πολλά έργα καταλήγουμε να γράφουμε εκτενείς βρόχους `for` μόνο για να εκτυπώσουμε μερικές συμβολοσειρές—σπαταλώντας χρόνο και αναγνωσιμότητα. Τα καλά νέα; Ένας μόνο βρόχος `foreach` μπορεί να εξάγει κάθε όνομα από ένα αντικείμενο και να **display string list** σε δευτερόλεπτα.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **get object names**, να επαναλάβετε στοιχεία, και να τα εμφανίσετε στην κονσόλα. Στο τέλος θα έχετε ένα αυτόνομο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιαδήποτε εφαρμογή κονσόλας .NET 6+, μαζί με μια σειρά συμβουλών για ειδικές περιπτώσεις και απόδοση.

> **Συμβουλή επαγγελματία:** Αν εργάζεστε με μεγάλες συλλογές, σκεφτείτε τη χρήση του `Parallel.ForEach`—αλλά αυτό είναι θέμα για άλλη μέρα.

---

## Τι Θα Μάθετε

- Πώς να ανακτήσετε μια συλλογή ονομάτων από ένα αντικείμενο (`GetSignatureNames` στο παράδειγμά μας)
- Η σύνταξη και οι λεπτομέρειες ενός **foreach loop example** σε C#
- Τρόποι για **display string list** στην κονσόλα, συμπεριλαμβανομένων τεχνικών μορφοποίησης
- Κοινά προβλήματα κατά την επανάληψη στοιχείων (συλλογές null, κενά αποτελέσματα)
- Ένα πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑επικόλληση, που μπορείτε να εκτελέσετε αμέσως

Δεν απαιτούνται εξωτερικές βιβλιοθήκες· μόνο η βασική βιβλιοθήκη κλάσεων που έρχεται με το .NET. Αν έχετε εγκατεστημένο το .NET SDK, είστε έτοιμοι.

![Διάγραμμα επανάληψης συλλογής C# που δείχνει μια λίστα να ρέει σε βρόχο foreach και μετά στην κονσόλα](/images/iterate-collection-csharp.png "διάγραμμα επανάληψης συλλογής c#")

---

## Βήμα 1: Ρύθμιση του Δείγματος Αντικειμένου

Πρώτα απ' όλα—χρειαζόμαστε ένα αντικείμενο που μπορεί να επιστρέψει μια συλλογή ονομάτων. Φανταστείτε ότι έχετε μια κλάση `Signature` που περιέχει πολλές υπογραφές· κάθε υπογραφή έχει μια ιδιότητα `Name`. Η μέθοδος `GetSignatureNames` απλώς εξάγει αυτά τα ονόματα σε ένα `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Γιατί είναι σημαντικό:** Επιστρέφοντας `IEnumerable<string>` διατηρούμε τη μέθοδο ευέλικτη—οι κλήστες μπορούν να κάνει enumeration, ερωτήματα ή μετατροπές του αποτελέσματος χωρίς να αντιγράφουν τη βασική λίστα. Επίσης, καθιστά εύκολο το **loop over items** αργότερα.

---

## Βήμα 2: Γράψτε τον Βρόχο Foreach για την Εμφάνιση της Λίστας Συμβολοσειρών

Τώρα που έχουμε μια πηγή ονομάτων, ας **iterate collection C#** πραγματικά. Η κατασκευή `foreach` εξάγει αυτόματα κάθε στοιχείο από το enumerable, έτσι δεν χρειάζεται να διαχειριζόμαστε μεταβλητή δείκτη.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Επεξήγηση του κώδικα:**

1. **Instantiate** `Signature` – έχετε τώρα ένα αντικείμενο που γνωρίζει τα δικά του ονόματα.
2. **Retrieve** τη συλλογή μέσω `GetSignatureNames()` – αυτό είναι το βήμα **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` επαναλαμβάνει αυτόματα κάθε συμβολοσειρά.
4. **Display** κάθε `name` με `Console.WriteLine` – ο κλασικός τρόπος για **display string list** σε εφαρμογή κονσόλας.

Επειδή το `signatureNames` υλοποιεί `IEnumerable<string>`, ο βρόχος `foreach` λειτουργεί αμέσως, διαχειριζόμενος τον enumerator στο παρασκήνιο. Δεν χρειάζεται να ανησυχείτε για σφάλματα off‑by‑one ή χειροκίνητο έλεγχο ορίων.

---

## Βήμα 3: Εκτελέστε το Πρόγραμμα και Επαληθεύστε το Αποτέλεσμα

Συγκεντρώστε και εκτελέστε το πρόγραμμα (π.χ., `dotnet run` από το φάκελο του έργου). Θα πρέπει να δείτε:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Αν δεν εμφανιστεί τίποτα, ελέγξτε ξανά ότι το `GetSignatureNames` δεν επιστρέφει `null`. Μια γρήγορη προφυλακτική προστασία μπορεί να σας εξοικονομήσει προβλήματα:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Τώρα ο βρόχος θα χειριστεί κομψά μια ελλιπή συλλογή και απλώς δεν θα εμφανίσει τίποτα αντί να ρίξει `NullReferenceException`.

---

## Βήμα 4: Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### 4.1 Επανάληψη Λίστας Πολύπλοκων Αντικειμένων

Συχνά δεν θα δουλεύετε με απλές συμβολοσειρές αλλά με αντικείμενα που περιέχουν πολλαπλές ιδιότητες. Σε αυτήν την περίπτωση μπορείτε ακόμα να **loop over items** και να αποφασίσετε τι να εμφανίσετε:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Εδώ χρησιμοποιούμε διασύνδεση συμβολοσειρών για να συνδυάσουμε πεδία—παραμένει βρόχος `foreach`, απλώς με πιο πλούσια έξοδο.

### 4.2 Πρόωρη Έξοδος με `break`

Αν χρειάζεστε μόνο το πρώτο όνομα που ταιριάζει, βγείτε από το βρόχο:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Παράλληλη Enumeration (Προχωρημένο)

Όταν η συλλογή είναι τεράστια και κάθε επανάληψη είναι απαιτητική για την CPU, το `Parallel.ForEach` μπορεί να επιταχύνει τα πράγματα:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Θυμηθείτε, το `Console.WriteLine` είναι thread‑safe αλλά η σειρά εξόδου θα είναι μη‑προβλέψιμη.

---

## Βήμα 5: Συμβουλές για Καθαρούς και Συντηρήσιμους Βρόχους

- **Prefer `foreach` over `for`** όταν δεν χρειάζεστε δείκτη· μειώνει σφάλματα off‑by‑one.
- **Use `IEnumerable<T>`** στις υπογραφές μεθόδων για να διατηρείτε τα API ευέλικτα.
- **Guard against null** συλλογές με τον τελεστή συνένωσης null (`??`).
- **Keep the loop body small**—αν διαπιστώσετε ότι γράφετε πολλές γραμμές, εξάγετε μια μέθοδο.
- **Avoid modifying the collection** ενώ επαναλαμβάνετε· προκαλεί `InvalidOperationException`.

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **iterate collection C#** χρησιμοποιώντας ένα καθαρό **foreach loop example**, να ανακτήσετε **object names**, και να **display string list** στην κονσόλα. Το πλήρες πρόγραμμα—ορισμός αντικειμένου, ανάκτηση και επανάληψη—εκτελείται όπως είναι, παρέχοντάς σας μια ισχυρή βάση για οποιοδήποτε σενάριο όπου χρειάζεται να επαναλάβετε στοιχεία.

Από εδώ μπορείτε να εξερευνήσετε:

- Φιλτράρισμα με LINQ πριν την επανάληψη (`signatureNames.Where(n => n.Contains("a"))`)
- Γραφή της εξόδου σε αρχείο αντί για την κονσόλα
- Χρήση του `IAsyncEnumerable<T>` για ασύγχρονα ρεύματα

Δοκιμάστε τα και θα δείτε πόσο ευέλικτη είναι πραγματικά η κατασκευή `foreach`. Έχετε ερωτήσεις για ακραίες περιπτώσεις ή απόδοση; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}