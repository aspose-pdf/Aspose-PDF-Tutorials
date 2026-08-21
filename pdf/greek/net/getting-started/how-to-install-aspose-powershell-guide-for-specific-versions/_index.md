---
category: general
date: 2026-02-10
description: πώς να εγκαταστήσετε το aspose χρησιμοποιώντας το PowerShell. Μάθετε
  πώς να εκτελείτε το PowerShell ως διαχειριστής, να εγκαταστήσετε συγκεκριμένη έκδοση
  και πώς να εμφανίσετε τη λίστα των πακέτων.
draft: false
keywords:
- how to install aspose
- install specific version
- install nuget package powershell
- run powershell as administrator
- how to list packages
language: el
og_description: πώς να εγκαταστήσετε το aspose με το PowerShell. Αυτό το σεμινάριο
  δείχνει πώς να εκτελέσετε το PowerShell ως διαχειριστής, να εγκαταστήσετε μια συγκεκριμένη
  έκδοση και να εμφανίσετε τα πακέτα.
og_title: πώς να εγκαταστήσετε το aspose – Οδηγός βήμα‑βήμα PowerShell
tags:
- powershell
- nuget
- aspose
- devops
title: πώς να εγκαταστήσετε το aspose – Οδηγός PowerShell για συγκεκριμένες εκδόσεις
url: /el/net/getting-started/how-to-install-aspose-powershell-guide-for-specific-versions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να εγκαταστήσετε το aspose – Οδηγός βήμα‑βήμα PowerShell

Έχετε αναρωτηθεί ποτέ **πώς να εγκαταστήσετε το aspose** σε έναν καινούργιο υπολογιστή με Windows; Δεν είστε ο μόνος. Σε πολλά .NET projects το πακέτο Aspose.PDF NuGet είναι η προτιμώμενη βιβλιοθήκη για χειρισμό PDF, όμως το βήμα της εγκατάστασης μπορεί να φαίνεται ασαφές—ιδιαίτερα όταν χρειάζεστε μια συγκεκριμένη έκδοση ή εργάζεστε από έναν περιορισμένο διακομιστή.

Το θέμα είναι: μπορείτε να έχετε το Aspose έτοιμο σε δευτερόλεπτα, απευθείας από το PowerShell. Σε αυτό το tutorial θα περάσουμε από το άνοιγμα του PowerShell με τα κατάλληλα δικαιώματα, τη λήψη μιας συγκεκριμένης έκδοσης του πακέτου, και την επιβεβαίωση της εγκατάστασης με **πώς να εμφανίσετε τα πακέτα**. Στο τέλος θα έχετε μια επαναλήψιμη εντολή μίας γραμμής που μπορείτε να ενσωματώσετε σε σενάρια CI, και θα κατανοήσετε το «γιατί» πίσω από κάθε παράμετρο.

## Προαπαιτούμενα

- Windows 10/11 (ή Windows Server) με εγκατεστημένο PowerShell 5.1+.
- Πρόσβαση στο Internet ώστε να μπορεί να προσεγγιστεί το NuGet feed.
- Προαιρετικό αλλά χρήσιμο: ο **NuGet provider** (`Install-PackageProvider -Name NuGet -Force`) αν δεν είναι ήδη παρών.
- Δικαιώματα διαχειριστή εάν το περιβάλλον σας περιορίζει την εγκατάσταση πακέτων στο σύστημα.

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—τα περισσότερα μηχανήματα προγραμματιστών τα καλύπτουν ήδη. Θα καλύψουμε επίσης το βήμα **run powershell as administrator**, για κάθε περίπτωση.

## Βήμα 1: Ανοίξτε το PowerShell με τα κατάλληλα δικαιώματα

> **Pro tip:** Σε εταιρικό σταθμό εργασίας μπορεί να χρειαστεί να αυξήσετε τα δικαιώματα για να παρακάμψετε τους περιορισμούς της πολιτικής εκτέλεσης.

1. Κάντε κλικ στο **Start**, πληκτρολογήστε **PowerShell**, κάντε δεξί κλικ στο αποτέλεσμα και επιλέξτε **Run as administrator**.  
2. Αν προτιμάτε τη συντόμευση, πατήστε `Win + X` → **Windows PowerShell (Admin)**.

```powershell
# Verify you’re running as admin (will output True if elevated)
([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
    [Security.Principal.WindowsBuiltInRole]::Administrator)
```

Η εκτέλεση ως ανυψωμένος χρήστης εξασφαλίζει ότι το πακέτο θα τοποθετηθεί στο παγκόσμιο αποθετήριο πακέτων, κάτι που περιμένουν οι περισσότεροι build agents.

## Βήμα 2: Εγκατάσταση συγκεκριμένης έκδοσης του Aspose

Ο κύριος λόγος που οι προγραμματιστές ρωτούν “**πώς να εγκαταστήσετε το aspose**” είναι ότι χρειάζονται μια γνωστή, σταθερή έκδοση—ίσως επειδή ο κώδικάς τους στοχεύει σε μια έκδοση με διορθώσεις σφαλμάτων. Η εντολή `Install-Package` σας επιτρέπει να κλειδώσετε την έκδοση με τη σημαία `-Version`.

```powershell
# Step 2: Install Aspose.PDF version 25.3
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force
```

### Γιατί έχουν σημασία οι παράμετροι

| Flag | Reason |
|------|--------|
| `-Version 25.3` | Εξασφαλίζει ότι θα λάβετε ακριβώς την 25.3, αποφεύγοντας τυχαίες αναβαθμίσεις. |
| `-ProviderName NuGet` | Ενημερώνει ρητά το PowerShell ποιον provider να χρησιμοποιήσει· αποτρέπει την ασάφεια εάν έχετε άλλες πηγές πακέτων. |
| `-Force` | Καταστέλλει τις προτροπές που θα μπορούσαν να σταματήσουν ένα αυτοματοποιημένο script. |

> **Edge case:** Εάν έχετε ήδη εγκατεστημένη μια νεότερη έκδοση, το PowerShell θα αρνηθεί να κάνει υποβάθμιση εκτός εάν προσθέσετε `-AllowDowngrade`. Χρησιμοποιήστε το με μέτρο:

```powershell
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force -AllowDowngrade
```

## Βήμα 3: Επαλήθευση της εγκατάστασης – πώς να εμφανίσετε τα πακέτα

Μετά το τέλος της εγκατάστασης, θα θέλετε να βεβαιωθείτε ότι η σωστή έκδοση τοποθετήθηκε εκεί που περιμένετε. Εκεί έρχεται το **πώς να εμφανίσετε τα πακέτα**.

```powershell
# Step 3: List all installed packages named Aspose.PDF
Get-Package -Name Aspose.PDF
```

Η τυπική έξοδος φαίνεται ως εξής:

```
Name                     Version          Source
----                     -------          ------
Aspose.PDF               25.3             nuget.org
```

Αν δείτε διαφορετική έκδοση, ελέγξτε ξανά τη σημαία `-Version` που χρησιμοποιήσατε νωρίτερα, ή εκτελέστε `Get-PackageSource` για να επιβεβαιώσετε ότι παίρνετε από το σωστό NuGet feed.

### Εμφάνιση πακέτων σε συγκεκριμένο πεδίο

Μερικές φορές θέλετε να δείτε μόνο τα πακέτα που έχουν εγκατασταθεί για τον τρέχοντα χρήστη:

```powershell
Get-Package -Name Aspose.PDF -Scope CurrentUser
```

Ή, για έλεγχο του αποθετηρίου σε επίπεδο συστήματος:

```powershell
Get-Package -Name Aspose.PDF -Scope AllUsers
```

Αυτές οι παραλλαγές είναι χρήσιμες όταν αντιμετωπίζετε σφάλματα που σχετίζονται με δικαιώματα.

## Βήμα 4: Προαιρετικό – Προσθήκη του πακέτου σε έργο αυτόματα

Εάν εργάζεστε μέσα σε φάκελο λύσης, το PowerShell μπορεί επίσης να ενημερώσει το αρχείο `.csproj` για εσάς:

```powershell
# Add Aspose.PDF 25.3 to the current directory’s .csproj
dotnet add package Aspose.PDF --version 25.3
```

Αυτή η εντολή χρησιμοποιεί το .NET CLI αντί για τον NuGet provider του PowerShell, αλλά το αποτέλεσμα είναι το ίδιο: μια εγγραφή αναφοράς στο αρχείο του έργου σας. Είναι ένας γρήγορος τρόπος να διατηρήσετε το source control συγχρονισμένο με την ακριβή έκδοση που μόλις εγκαταστήσατε.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `Install-Package : No match was found for the specified search criteria` | Λείπει ή είναι παλαιός ο NuGet provider | `Install-PackageProvider -Name NuGet -Force` και μετά `Set-PSRepository -Name 'PSGallery' -InstallationPolicy Trusted` |
| `Access denied` when installing | Δεν εκτελείται ως διαχειριστής | Ξανανοίξτε το PowerShell με **Run as administrator** |
| Wrong version appears in `Get-Package` | Κρυφή (cached) μεταδεδομένα | Εκτελέστε `Update-Module -Name PowerShellGet` και δοκιμάστε ξανά |
| Package appears but VS can’t find it | Το έργο στοχεύει ακόμα σε παλαιότερο .NET framework | Αναβαθμίστε το target framework ή εγκαταστήστε μια συμβατή έκδοση του Aspose |

## Πλήρες script που μπορείτε να αντιγράψετε‑επικολλήσετε

Παρακάτω είναι ένα μονοαρχείο PowerShell script που ενσωματώνει όλα όσα συζητήσαμε. Αποθηκεύστε το ως `Install-Aspose.ps1` και εκτελέστε το με δικαιώματα διαχειριστή.

```powershell
<# 
.SYNOPSIS
Installs a specific version of Aspose.PDF via PowerShell and verifies the installation.

.DESCRIPTION
This script demonstrates how to run PowerShell as administrator, install a
specific version of the Aspose.PDF NuGet package, and list the installed
packages to confirm success. It also shows optional steps for adding the
package to a .NET project.

.AUTHOR
Your Name – 2026
#>

# 1️⃣ Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Error "Please run this script from an elevated PowerShell session."
    exit 1
}

# 2️⃣ Install NuGet provider if missing
if (-not (Get-PackageProvider -Name NuGet -ErrorAction SilentlyContinue)) {
    Write-Host "NuGet provider not found – installing..."
    Install-PackageProvider -Name NuGet -Force | Out-Null
}

# 3️⃣ Install Aspose.PDF version 25.3
$desiredVersion = "25.3"
Write-Host "Installing Aspose.PDF version $desiredVersion ..."
Install-Package Aspose.PDF -Version $desiredVersion -ProviderName NuGet -Force

# 4️⃣ Verify installation
Write-Host "`nVerifying installation..."
$pkg = Get-Package -Name Aspose.PDF -ErrorAction SilentlyContinue
if ($pkg) {
    Write-Host "✅ Aspose.PDF $($pkg.Version) installed successfully."
} else {
    Write-Error "❌ Installation failed – package not found."
}

# 5️⃣ (Optional) Add to .csproj if present
$csproj = Get-ChildItem -Path . -Filter *.csproj -ErrorAction SilentlyContinue | Select-Object -First 1
if ($csproj) {
    Write-Host "`nAdding package reference to $($csproj.Name)..."
    dotnet add $csproj.FullName package Aspose.PDF --version $desiredVersion
}
```

Τρέξτε το ως εξής:

```powershell
.\Install-Aspose.ps1
```

Θα πρέπει να δείτε ένα πράσινο σημάδι ελέγχου που επιβεβαιώνει την έκδοση, ακολουθούμενο από μια προαιρετική ενημέρωση του έργου.

## Συμπέρασμα

Καλύψαμε **πώς να εγκαταστήσετε το aspose** χρησιμοποιώντας PowerShell από την αρχή μέχρι το τέλος: εκκίνηση μιας ανυψωμένης συνεδρίας, λήψη ακριβούς έκδοσης, και επιβεβαίωση του αποτελέσματος με **πώς να εμφανίσετε τα πακέτα**. Το παραπάνω script κάνει όλη τη διαδικασία επαναλήψιμη—ιδανική για CI pipelines ή για ενσωμάτωση νέων μελών στην ομάδα.

Στη συνέχεια, μπορείτε να εξερευνήσετε το **install nuget package powershell** για άλλες βιβλιοθήκες, ή να εμβαθύνετε στο δικό του API του Aspose για να αρχίσετε να δημιουργείτε PDFs. Εάν αντιμετωπίσετε πρόβλημα, επανεξετάστε τον πίνακα «Συνηθισμένα προβλήματα»· τα περισσότερα ζητήματα οφείλονται σε δικαιώματα ή σε παλιό provider.

Καλό κώδικα, και εύχομαι οι εγκαταστάσεις NuGet σας να είναι πάντα χωρίς σφάλματα!

![πώς να εγκαταστήσετε το aspose PowerShell screenshot](https://example.com/images/install-aspose-powershell.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}