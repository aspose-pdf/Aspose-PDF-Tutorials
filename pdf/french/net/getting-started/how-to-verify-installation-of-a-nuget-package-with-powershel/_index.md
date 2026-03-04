---
category: general
date: 2026-03-03
description: Comment vérifier l'installation d'un package NuGet dans PowerShell. Apprenez
  à exécuter PowerShell en tant qu'administrateur, installer une version spécifique
  et gérer les packages efficacement.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: fr
og_description: Comment vérifier l'installation d'un package NuGet dans PowerShell.
  Ce guide étape par étape vous montre comment exécuter PowerShell en tant qu'administrateur,
  installer une version spécifique et confirmer que le package est présent.
og_title: Comment vérifier l'installation d'un package NuGet avec PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Comment vérifier l'installation d'un package NuGet avec PowerShell
url: /fr/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment vérifier l'installation d'un package NuGet avec PowerShell

Vérifier l'installation d'un package NuGet dans PowerShell est une tâche courante pour les administrateurs Windows. Si vous vous êtes déjà demandé si le package était réellement installé sur votre système, ce guide vous montre exactement comment vérifier l'installation — sans aucune supposition.  

Dans les quelques minutes qui suivent, nous parcourrons le lancement de PowerShell en tant qu'administrateur, le téléchargement d'une version spécifique d'un package, et enfin la confirmation que le package existe sur votre machine. Vous découvrirez également quelques astuces pour la **gestion de packages PowerShell** au quotidien qui maintiennent votre environnement propre.  

Avant de commencer, assurez‑vous de disposer d’une machine Windows avec PowerShell 7 (ou Windows PowerShell 5.1) et d’une connexion Internet. Aucun outil supplémentaire n’est nécessaire ; tout s’exécute directement à partir du fournisseur intégré PackageManagement.

---

![Capture d'écran d'une fenêtre PowerShell élevée avec la commande Get-Package](/images/verify-installation.png "Capture d'écran montrant comment vérifier l'installation dans une fenêtre PowerShell élevée")

## Étape 1 : Exécuter PowerShell en tant qu'administrateur  

Exécuter PowerShell avec des droits administratifs est la première ligne de défense contre les problèmes liés aux permissions. Lorsque vous **exécutez PowerShell en tant qu'administrateur**, la cmdlet `Install-Package` peut écrire dans le dossier Program Files et enregistrer le package dans le catalogue système.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Astuce :** Épinglez le raccourci « Windows PowerShell (Admin) » à votre barre des tâches. Un clic et vous êtes prêt à partir.

### Pourquoi l'élévation est importante  

Sans élévation, `Install-Package` peut silencieusement revenir à un emplacement limité à l'utilisateur, ce qui peut ensuite perturber `Get-Package` car il recherche par défaut dans la portée système. L'élévation garantit que le package apparaît là où la plupart des scripts s’attendent à le trouver.

---

## Étape 2 : Installer une version spécifique du package NuGet  

Souvent, vous ne voulez pas la dernière version mais une version connue et fiable avec laquelle votre projet a été testé. Le modèle **installer une version spécifique** est simple avec le paramètre `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Décomposition de la commande  

| Paramètre | Ce que ça fait | Pourquoi c’est nécessaire |
|-----------|----------------|---------------------------|
| `-Version 25.3` | Fixe le numéro de build exact | Garantit des builds reproductibles |
| `-ProviderName NuGet` | Indique à PowerShell quel fournisseur utiliser | Évite les ambiguïtés si plusieurs fournisseurs sont enregistrés |
| `-Scope AllUsers` | Installe pour chaque compte sur la machine | Fonctionne avec les requêtes système de `Get-Package` |
| `-Force` | Supprime les invites (utile dans les scripts) | Maintient l’automatisation fluide |

> **Attention :** Si vous omettez `-Version`, PowerShell récupère le package le plus récent, ce qui peut introduire des changements incompatibles.

---

## Étape 3 : Vérifier l'installation  

Voici le moment de vérité : **comment vérifier l'installation**. La façon la plus directe est de demander à PowerShell le package que vous venez d’installer.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Vous devriez voir une sortie similaire à :

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Si la commande ne renvoie rien, essayez la requête limitée à l'utilisateur :

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Méthodes de vérification alternatives  

1. **Vérifier le dossier du module** – Les packages sont stockés sous `C:\Program Files\PackageManagement\Packages\`. Recherchez un dossier nommé `Aspose.PDF.25.3`.  
2. **Utiliser `Find-Package`** – Cette commande recherche dans le dépôt et peut confirmer que la version est disponible :  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Valider avec .NET** – Chargez l'assembly dans PowerShell pour vous assurer que le DLL peut être chargé :  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Si l’une de ces vérifications réussit, vous avez **vérifié l'installation** avec succès.

---

## Pièges courants et comment les éviter  

- **Fournisseur NuGet manquant** – Exécutez d'abord `Install-PackageProvider -Name NuGet -Force`.  
- **Blocages de ExecutionPolicy** – Définissez temporairement `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` pour la session.  
- **Problèmes de proxy réseau** – Utilisez les paramètres `-Proxy` et `-ProxyCredential` si votre environnement se trouve derrière un proxy d’entreprise.  
- **Conflits de version** – Lorsqu’il existe plusieurs versions, spécifiez `-RequiredVersion` dans `Get-Package` pour lever l’ambiguïté.

---

## Assembler le tout – Un script complet  

Ci-dessous se trouve un script prêt à l’exécution qui regroupe les trois étapes, inclut la gestion des erreurs et affiche un message de succès convivial.

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

L’exécution du script produit une ligne claire « ✅ Installation vérifiée avec succès… », confirmant que **comment vérifier l'installation** fonctionne de bout en bout.

---

## Conclusion  

Vous savez maintenant **comment vérifier l'installation** de n'importe quel package NuGet à l'aide de PowerShell, depuis le lancement d’une session élevée jusqu’à l’installation d’une version ciblée et enfin la confirmation de la présence du package. Maîtriser ces étapes vous donne confiance dans votre flux de travail de **gestion de packages PowerShell** et évite les maux de tête du type « il semble installé mais ne l’est pas » qui affectent souvent les développeurs Windows.

Et après ? Essayez de remplacer `Aspose.PDF` par une autre bibliothèque, expérimentez avec `-Scope CurrentUser`, ou scriptz une installation en masse de plusieurs packages pour une nouvelle station de travail. Et si vous rencontrez des particularités, souvenez‑vous des conseils de dépannage ci‑dessus — en particulier les vérifications du fournisseur et de la stratégie d’exécution.

Bon scripting, et que vos installations soient toujours vérifiables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}