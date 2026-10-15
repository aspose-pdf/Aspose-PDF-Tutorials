---
category: general
date: 2026-03-03
description: Πώς να επαληθεύσετε την εγκατάσταση ενός πακέτου NuGet στο PowerShell.
  Μάθετε πώς να εκτελείτε το PowerShell ως διαχειριστής, να εγκαθιστάτε συγκεκριμένη
  έκδοση και να διαχειρίζεστε τα πακέτα αποδοτικά.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: el
og_description: Πώς να επαληθεύσετε την εγκατάσταση ενός πακέτου NuGet στο PowerShell.
  Αυτός ο οδηγός βήμα‑προς‑βήμα σας δείχνει πώς να εκτελέσετε το PowerShell ως διαχειριστής,
  να εγκαταστήσετε μια συγκεκριμένη έκδοση και να επιβεβαιώσετε ότι το πακέτο είναι
  παρόν.
og_title: Πώς να ελέγξετε την εγκατάσταση ενός πακέτου NuGet με το PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Πώς να επαληθεύσετε την εγκατάσταση ενός πακέτου NuGet με το PowerShell
url: /el/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Επαληθεύσετε την Εγκατάσταση ενός Πακέτου NuGet με το PowerShell

Η επαλήθευση της εγκατάστασης ενός πακέτου NuGet στο PowerShell είναι μια συνηθισμένη εργασία για διαχειριστές Windows. Αν ποτέ αναρωτηθήκατε αν το πακέτο πραγματικά εγκαταστάθηκε στο σύστημά σας, αυτός ο οδηγός σας δείχνει ακριβώς πώς να επαληθεύσετε την εγκατάσταση — χωρίς εικασίες.  

Στα επόμενα λίγα λεπτά θα περάσουμε από το άνοιγμα του PowerShell ως διαχειριστής, τη λήψη μιας συγκεκριμένης έκδοσης ενός πακέτου και, τέλος, την επιβεβαίωση ότι το πακέτο υπάρχει στον υπολογιστή σας. Θα μάθετε επίσης μερικές συμβουλές για την καθημερινή **PowerShell package management** που διατηρούν το περιβάλλον σας καθαρό.  

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε έναν υπολογιστή Windows με PowerShell 7 (ή Windows PowerShell 5.1) και σύνδεση στο διαδίκτυο. Δεν χρειάζονται επιπλέον εργαλεία· όλα εκτελούνται απευθείας από τον ενσωματωμένο πάροχο PackageManagement.

---

![Στιγμιότυπο οθόνης ενός ανυψωμένου παραθύρου PowerShell με την εντολή Get-Package](/images/verify-installation.png "Στιγμιότυπο που δείχνει πώς να επαληθεύσετε την εγκατάσταση σε ένα ανυψωμένο παράθυρο PowerShell")

## Βήμα 1: Εκτελέστε το PowerShell ως Διαχειριστής  

Η εκτέλεση του PowerShell με δικαιώματα διαχειριστή είναι η πρώτη γραμμή άμυνας ενάντια σε προβλήματα που σχετίζονται με τα δικαιώματα. Όταν **εκτελείτε το PowerShell ως διαχειριστής**, η εντολή `Install-Package` μπορεί να γράψει στο φάκελο Program Files και να καταχωρήσει το πακέτο στον ευρέως διαδεδομένο κατάλογο του συστήματος.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** Καρφιτσωστε τη συντόμευση “Windows PowerShell (Admin)” στη γραμμή εργασιών. Ένα κλικ και είστε έτοιμοι.

### Γιατί η ανύψωση είναι σημαντική  

Χωρίς ανύψωση, η `Install-Package` μπορεί σιωπηρά να επιστρέψει σε θέση περιορισμένης σε χρήστη, κάτι που μπορεί αργότερα να μπερδέψει την `Get-Package` επειδή ψάχνει στην περιοχή του συστήματος από προεπιλογή. Η ανύψωση εγγυάται ότι το πακέτο εμφανίζεται εκεί που τα περισσότερα σενάρια το περιμένουν.

---

## Βήμα 2: Εγκατάσταση μιας Συγκεκριμένης Έκδοσης του Πακέτου NuGet  

Συχνά δεν θέλετε την πιο πρόσφατη έκδοση αλλά μια γνωστή‑σταθερή έκδοση που το έργο σας έχει δοκιμάσει. Το μοτίβο **install specific version** είναι απλό με τη σημαία `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Ανάλυση της εντολής  

| Parameter | Τι κάνει | Γιατί το χρειάζεστε |
|-----------|----------|---------------------|
| `-Version 25.3` | Καθορίζει τον ακριβή αριθμό build | Εγγυάται επαναλήψιμες κατασκευές |
| `-ProviderName NuGet` | Ενημερώνει το PowerShell ποιον πάροχο να χρησιμοποιήσει | Αποφεύγει ασάφεια αν υπάρχουν πολλοί πάροχοι εγγεγραμμένοι |
| `-Scope AllUsers` | Εγκαθιστά για κάθε λογαριασμό στον υπολογιστή | Λειτουργεί με ερωτήματα `Get-Package` σε επίπεδο συστήματος |
| `-Force` | Καταστέλλει τα προτροπές (χρήσιμο σε σενάρια) | Κρατά την αυτοματοποίηση ομαλή |

> **Watch out:** Αν παραλείψετε το `-Version`, το PowerShell θα φέρει το πιο νέο πακέτο, το οποίο μπορεί να εισάγει αλλαγές που σπάζουν τη λειτουργικότητα.

---

## Βήμα 3: Επαλήθευση της Εγκατάστασης  

Τώρα έρχεται η στιγμή της αλήθειας: **πώς να επαληθεύσετε την εγκατάσταση**. Ο πιο άμεσος τρόπος είναι να ρωτήσετε το PowerShell για το πακέτο που μόλις εγκαταστήσατε.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Θα πρέπει να δείτε έξοδο παρόμοια με:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Αν η εντολή δεν επιστρέψει τίποτα, δοκιμάστε το ερώτημα περιορισμένο σε χρήστη:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Εναλλακτικές μέθοδοι επαλήθευσης  

1. **Ελέγξτε το φάκελο του module** – Τα πακέτα αποθηκεύονται στο `C:\Program Files\PackageManagement\Packages\`. Αναζητήστε έναν φάκελο με το όνομα `Aspose.PDF.25.3`.  
2. **Χρησιμοποιήστε το `Find-Package`** – Αυτό ψάχνει στο αποθετήριο και μπορεί να επιβεβαιώσει ότι η έκδοση είναι διαθέσιμη:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Επικύρωση με .NET** – Φορτώστε το assembly στο PowerShell για να βεβαιωθείτε ότι το DLL μπορεί να φορτωθεί:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Αν οποιοσδήποτε από αυτούς τους ελέγχους πετύχει, έχετε επαληθεύσει με επιτυχία την **εγκατάσταση**.

---

## Συνηθισμένα Παράπλοκα και Πώς να τα Αποφύγετε  

- **Απουσία παρόχου NuGet** – Εκτελέστε πρώτα `Install-PackageProvider -Name NuGet -Force`.  
- **Αποκλεισμοί ExecutionPolicy** – Ορίστε προσωρινά `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` για τη συνεδρία.  
- **Προβλήματα δικτυακού proxy** – Χρησιμοποιήστε τις παραμέτρους `-Proxy` και `-ProxyCredential` εάν το περιβάλλον σας βρίσκεται πίσω από εταιρικό proxy.  
- **Σύγκρουση εκδόσεων** – Όταν υπάρχουν πολλαπλές εκδόσεις, καθορίστε `-RequiredVersion` στην `Get-Package` για να ξεκαθαρίσετε.

---

## Συνδυάζοντας Όλα – Ένα Πλήρες Script  

Παρακάτω υπάρχει ένα έτοιμο προς εκτέλεση script που ενσωματώνει τα τρία βήματα, περιλαμβάνει διαχείριση σφαλμάτων και εκτυπώνει ένα φιλικό μήνυμα επιτυχίας.

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

Η εκτέλεση του script παράγει μια σαφή γραμμή “✅ Successfully verified installation…” που επιβεβαιώνει ότι η **πώς να επαληθεύσετε την εγκατάσταση** λειτουργεί από άκρη σε άκρη.

---

## Συμπέρασμα  

Τώρα γνωρίζετε **πώς να επαληθεύσετε την εγκατάσταση** οποιουδήποτε πακέτου NuGet χρησιμοποιώντας το PowerShell, από την εκκίνηση μιας ανυψωμένης συνεδρίας μέχρι την εγκατάσταση μιας στοχευμένης έκδοσης και, τέλος, την επιβεβαίωση της παρουσίας του πακέτου. Η κατανόηση αυτών των βημάτων σας δίνει εμπιστοσύνη στη ροή εργασίας **PowerShell package management** και αποτρέπει τα προβλήματα «φαίνεται εγκατεστημένο αλλά δεν είναι» που συχνά ενοχλούν τους προγραμματιστές Windows.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το `Aspose.PDF` με άλλη βιβλιοθήκη, πειραματιστείτε με το `-Scope CurrentUser`, ή γράψτε ένα script για μαζική εγκατάσταση πολλαπλών πακέτων για έναν νέο υπολογιστή. Και αν αντιμετωπίσετε ιδιόμορφα προβλήματα, θυμηθείτε τις παραπάνω συμβουλές αντιμετώπισης – ειδικά τους ελέγχους παρόχου και πολιτικής εκτέλεσης.

Καλή προγραμματιστική, και εύχομαι οι εγκαταστάσεις σας να είναι πάντα επαληθεύσιμες!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}