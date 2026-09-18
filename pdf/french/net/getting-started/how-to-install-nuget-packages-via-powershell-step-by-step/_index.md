---
category: general
date: 2026-02-20
description: Apprenez à installer des packages NuGet avec PowerShell, à exécuter PowerShell
  en tant qu'administrateur, à lister les packages installés et à vérifier le package
  installé en quelques minutes.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: fr
og_description: Comment installer des packages NuGet avec PowerShell, exécuter PowerShell
  en tant qu’administrateur, lister les packages installés et vérifier le package
  installé — guide complet.
og_title: comment installer des packages NuGet via PowerShell – guide rapide
tags:
- PowerShell
- NuGet
- Package Management
title: Comment installer des packages NuGet via PowerShell – étape par étape
url: /fr/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment installer des packages nuget via PowerShell – étape par étape

Vous vous êtes déjà demandé **comment installer nuget** sans ouvrir Visual Studio ? Vous n'êtes pas seul. Dans de nombreux pipelines CI ou sur des machines neuves, la solution la plus rapide consiste à passer à PowerShell—de préférence *run powershell as admin*—et laisser le gestionnaire de packages faire son travail.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : ouvrir la console appropriée, télécharger une version précise d’une bibliothèque, puis confirmer que le package a bien été installé sur votre système. À la fin, vous pourrez **list installed packages**, connaître **how to verify package** et être sûr que l’étape **verify installed package** a réussi à chaque fois.

## Ce que vous apprendrez

- Comment lancer PowerShell avec les privilèges appropriés.  
- La syntaxe exacte de la commande `Install-Package` pour NuGet.  
- Les façons de **list installed packages** et de confirmer les numéros de version.  
- Les pièges courants (droits admin manquants, incompatibilités de version) et comment les éviter.  

Aucune expérience préalable avec NuGet n’est requise, juste une machine Windows fonctionnelle et un peu de curiosité.

---

## Comment installer des packages NuGet à l’aide de PowerShell

> **Pro tip :** Si vous ajoutez fréquemment les mêmes packages, pensez à les placer dans un fichier script et à l’exécuter avec `-File`. Cela vous évite de retaper la même ligne encore et encore.

### Étape 1 : Ouvrir PowerShell avec les permissions nécessaires

La toute première chose à faire est **run powershell as admin**. Sans élévation, la cmdlet `Install-Package` peut échouer silencieusement ou demander une confirmation que vous ne voulez pas gérer.

1. Cliquez sur le bouton Démarrer.  
2. Tapez **PowerShell**.  
3. Faites un clic droit sur *Windows PowerShell* et choisissez **Run as administrator**.  

Vous verrez une invite UAC ; cliquez sur **Yes**. Vous avez maintenant une session privilégiée prête pour l’installation de packages.

> *Pourquoi admin ?*  
> NuGet écrit des fichiers dans le dossier global des packages (`C:\Program Files\PackageManagement\NuGet\Packages` par défaut). Cet emplacement est protégé, donc seul un processus élevé peut y écrire.

### Étape 2 : Installer le package NuGet souhaité et la version

Avec la console ouverte, la commande principale est simple :

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` est l’enveloppe PowerShell du client NuGet.  
- `-Version` fixe la version exacte dont vous avez besoin, évitant les mises à jour accidentelles.  

Si vous omettez `-Version`, PowerShell récupérera la dernière version stable—parfois c’est suffisant, parfois vous avez besoin de la version exacte que vous avez testée.

#### Que se passe-t-il en coulisses ?

PowerShell contacte la source de packages configurée (par défaut `https://www.nuget.org/api/v2`) et télécharge le fichier `.nupkg`. Il extrait ensuite les DLLs dans le dossier global des packages et enregistre le package auprès du fournisseur local. Le processus se termine généralement en quelques secondes, sauf si votre réseau est lent.

### Étape 3 : Vérifier que le package a été installé avec succès

Maintenant que le package est sur le disque, vous vous demanderez probablement, **« Comment vérifier le package ? »** La réponse se trouve dans une requête simple :

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

L’exécution de celle‑ci renvoie quelque chose comme :

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Cette sortie confirme deux choses :

1. Le package **Aspose.PDF** est présent.  
2. Sa version correspond à celle que vous avez demandée, satisfaisant ainsi l’exigence **verify installed package**.

Si vous voulez voir *tous* les packages sur la machine, retirez le filtre `-Name` :

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Cette vue **list installed packages** est pratique pour les audits ou lorsque vous devez nettoyer d’anciennes bibliothèques.

### Étape 4 : Optionnel – gestion des cas particuliers

#### a) Package introuvable ou version incompatible

Si PowerShell répond *« Package not found »* ou *« Version not available »*, revérifiez l’orthographe et le numéro de version. NuGet n’est pas sensible à la casse, mais un espace superflu cassera la commande.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Exécution sans droits admin

Si vous avez oublié de **run powershell as admin**, la cmdlet lèvera une erreur de permission. La solution consiste simplement à fermer la fenêtre et à la rouvrir avec les droits élevés—pas besoin de réinstaller quoi que ce soit.

#### c) Utilisation d’une source personnalisée

Dans les environnements d’entreprise, vous pouvez disposer d’un flux NuGet interne :

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

L’étape de vérification reste la même ; il suffit de se rappeler d’ajouter `-Source` lors de l’installation.

---

## Tableau de référence rapide

| Action                              | PowerShell command                                          | Pourquoi c'est important |
|-------------------------------------|-------------------------------------------------------------|---------------------------|
| Ouvrir une console élevée           | *Exécuter PowerShell en tant qu'administrateur*            | Nécessaire pour une installation globale |
| Installer une version spécifique    | `Install-Package <pkg> -Version <x.y.z>`                    | Garantit des builds reproductibles |
| Lister un seul package              | `Get-Package -Name <pkg>`                                   | Confirme **how to verify package** |
| Lister tous les packages NuGet      | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Utile pour **list installed packages** |
| Rechercher les versions disponibles | `Find-Package <pkg> -AllVersions`                           | Aide lorsque la version est inconnue |

---

## Conclusion

Nous avons couvert **how to install nuget** packages en utilisant PowerShell du début à la fin—ouvrir la console **run powershell as admin**, télécharger une version précise, puis **list installed packages** pour **verify installed package**. Avec ces commandes dans votre boîte à outils, vous pouvez automatiser la gestion des bibliothèques sur n’importe quelle machine Windows, que vous scriptiez un pipeline CI ou que vous répariez simplement une DLL manquante sur votre poste de développement.

Prochaines étapes ? Essayez d’ajouter plusieurs packages dans un même script, explorez le paramètre `-Scope` pour installer localement dans un projet, ou combinez ces commandes avec `Invoke-Expression` pour créer un installateur léger pour votre équipe. Et si vous rencontrez un problème, souvenez‑vous de l’étape **how to verify package**—voir la version dans `Get-Package` est souvent le moyen le plus rapide de repérer un souci.

Bonne utilisation de PowerShell ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}