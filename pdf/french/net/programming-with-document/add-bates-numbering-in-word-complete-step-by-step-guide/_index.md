---
category: general
date: 2026-06-21
description: Ajoutez rapidement la numérotation Bates dans Word. Apprenez comment
  ajouter Bates, appliquer la numérotation Bates aux documents juridiques et automatiser
  la numérotation avec C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: fr
og_description: Ajoutez la numérotation Bates dans Word avec C#. Ce guide montre comment
  ajouter Bates, appliquer la numérotation Bates aux documents juridiques et automatiser
  le processus.
og_title: Ajouter la numérotation Bates dans Word – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Ajouter la numérotation Bates dans Word – Guide complet étape par étape
url: /fr/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter la numérotation Bates dans Word – Guide complet étape par étape

Vous êtes-vous déjà demandé comment ajouter la numérotation Bates à un fichier Word sans taper chaque numéro manuellement ? Vous n'êtes pas seul. De nombreux avocats, assistants juridiques et spécialistes de l’e‑discovery ont besoin d’une méthode fiable pour **ajouter la numérotation Bates** à des centaines de pages, et le faire à la main est un cauchemar.

Dans ce tutoriel, nous passerons en revue une solution C# claire qui **applique la numérotation Bates** à un fichier `.docx`, explique pourquoi chaque ligne est importante, et vous montre comment ajuster le code pour des besoins juridiques spécifiques. À la fin, vous pourrez générer un document parfaitement numéroté en quelques secondes—sans plugins supplémentaires.

## Ce que vous allez apprendre

- Le code exact nécessaire pour **ajouter la numérotation Bates** à un document Word.  
- Le fonctionnement de la classe `BatesNumberingOptions` et pourquoi vous pourriez ajuster le préfixe ou la valeur de départ.  
- Des astuces pour utiliser cette approche sur de gros dossiers, y compris les considérations de mémoire.  
- Un aperçu rapide des prérequis afin que vous puissiez copier‑coller la solution et l’exécuter dès aujourd’hui.

**Prérequis**  
- .NET 6+ (ou .NET Framework 4.7.2+ si vous préférez l’ancien runtime).  
- Une référence à la bibliothèque Aspose.Words for .NET (ou toute API similaire exposant `AddBatesNumbering`).  
- Une connaissance de base du C# et de Visual Studio (ou de votre IDE préféré).

Si vous êtes à l’aise avec ces éléments, plongeons‑y.

## Étape 1 : Configurer le projet et importer la bibliothèque

Tout d’abord, créez une nouvelle application console (ou intégrez‑la à un service existant). Puis ajoutez le package NuGet Aspose.Words :

```bash
dotnet add package Aspose.Words
```

> **Astuce :** Utilisez la licence d’évaluation gratuite pour les tests ; elle ajoute un petit filigrane mais fonctionne exactement comme la version complète.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Ces instructions `using` importent les classes `Document` et `BatesNumberingOptions` dans le scope, ce qui est essentiel pour l’étape **appliquer la numérotation Bates** plus tard.

## Étape 2 : Charger le document source

Vous aurez besoin d’un fichier Word sur lequel travailler. Le code ci‑dessous charge `input.docx` depuis le dossier que vous spécifiez. Remplacez `"YOUR_DIRECTORY"` par le chemin réel sur votre machine.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Pourquoi charger le fichier d’abord ? L’objet `Document` analyse l’ensemble du package Word en mémoire, nous permettant de manipuler les en‑têtes, pieds de page et mises en page avant d’enregistrer. Si le fichier est massif (pensez à 10 000 pages), envisagez d’utiliser `LoadOptions` avec `LoadFormat.Docx` pour diffuser les sections au lieu de tout charger d’un coup.

## Étape 3 : Configurer les options de numérotation Bates

C’est ici que la magie opère. Vous indiquez à la bibliothèque quel préfixe utiliser (`"ABC-"` dans l’exemple) et où commencer le comptage (`1000`). Les deux valeurs sont entièrement personnalisables.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Pourquoi un préfixe ?** Dans la pratique juridique, les préfixes identifient souvent le dossier ou la partie productrice (`"ABC-"` pourrait signifier *Acme Bank Corp.*). Commencer à `1000` est courant car de nombreux cabinets réservent les 999 premiers numéros aux brouillons internes.

Si vous traitez de **numérotation Bates pour les documents juridiques**, vous pouvez également définir `batesOptions.Position` sur `Header` ou `Footer` et ajuster l’alignement pour correspondre aux règles du tribunal. La bibliothèque prend en charge ces ajustements dès le départ.

## Étape 4 : Appliquer la numérotation Bates à l’ensemble du document

Nous injectons maintenant les numéros. La méthode `AddBatesNumbering` parcourt chaque page, insère la chaîne formatée et met à jour le compteur interne du document.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

En coulisses, Aspose.Words crée un champ caché sur chaque page qui s’affiche sous la forme `ABC-1000`, `ABC-1001`, etc. Parce qu’il s’agit d’un champ, vous pouvez plus tard modifier le préfixe ou le numéro de départ sans régénérer le fichier complet—pratique pour **comment ajouter bates** après un changement de demande de découverte.

## Étape 5 : Enregistrer le document modifié

Enfin, écrivez le résultat dans un nouveau fichier. Conserver l’original intact est une bonne pratique, surtout lorsqu’il s’agit de preuves qui doivent rester impeccables.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Vous avez maintenant `output.docx` avec des numéros Bates séquentiels ajoutés à chaque page. Ouvrez‑le dans Word, et vous verrez les numéros exactement où vous les avez spécifiés (pied de page par défaut). La taille du fichier peut légèrement augmenter à cause des champs supplémentaires, mais c’est négligeable comparé aux avantages.

### Résultat attendu

| Page | Numéro Bates |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Si vous ouvrez la vue « Codes de champ » (`Alt+F9` dans Word), vous verrez quelque chose comme `{ BATES \* MERGEFORMAT ABC-1000 }` sur chaque page.

## Cas limites et questions fréquentes

### Et si le document contient déjà des numéros de page ?

La méthode `AddBatesNumbering` **n’écrasera pas** les champs de numérotation de page existants ; elle ajoute simplement un nouveau champ. Si vous souhaitez remplacer les numéros existants, supprimez‑les d’abord ou définissez `batesOptions.Position` à la même position que les numéros actuels.

### Puis‑je sauter des pages (par ex., exclure la page de garde) ?

Oui. Utilisez la surcharge qui accepte un `PageRange` :

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

C’est utile lorsque vous avez besoin de **numérotation Bates pour les mémoires juridiques** qui commencent après une page de titre.

### Comment changer le format de numérotation (chiffres romains, lettres) ?

La classe `BatesNumberingOptions` propose une propriété `NumberFormat` :

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Définissez‑la avant d’appeler `AddBatesNumbering`. Cette flexibilité aide lorsqu’un tribunal impose un style spécifique.

### Qu’en est‑il des performances sur des fichiers très volumineux ?

Charger un fichier Word de 2 Go peut consommer beaucoup de RAM. Pour atténuer le problème, traitez le document par morceaux à l’aide de l’utilitaire `DocumentSplitter`, appliquez la numérotation Bates à chaque segment, puis fusionnez les parties. Cette approche maintient la consommation mémoire sous contrôle tout en vous permettant d’**appliquer la numérotation Bates** efficacement.

## Exemple complet fonctionnel

En rassemblant le tout, voici un programme console prêt à être exécuté :

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Exécutez le programme, ouvrez `output.docx`, et vous verrez une série propre de numéros prête pour le dépôt, la découverte ou la soumission au tribunal.

## Conclusion

Vous savez maintenant exactement **comment ajouter Bates** à un document Word avec C#. Les étapes—chargement, configuration, application et sauvegarde—sont simples, tout en étant suffisamment flexibles pour répondre aux **flux de travail de numérotation Bates pour le juridique**, aux préfixes personnalisés et même au traitement par lots à grande échelle.

Si vous êtes prêt à aller plus loin, envisagez :

- D’intégrer le code dans une API web afin que vos collègues puissent télécharger des fichiers et recevoir instantanément des PDF numérotés.  
- D’ajouter une gestion des erreurs pour les fichiers manquants ou les problèmes de permissions (un simple `try/catch` autour de `Document.Load`).  
- D’explorer d’autres fonctionnalités d’Aspose.Words comme les filigranes ou la rédaction pour un ensemble complet d’outils e‑discovery.

N’hésitez pas à expérimenter avec différents préfixes, numéros de départ, ou même à combiner plusieurs schémas de numérotation dans le même document. Le monde de **l’application de la numérotation Bates** est étonnamment polyvalent une fois que vous avez la logique de base en main.

Des questions ou un scénario difficile ? Laissez un commentaire ci‑dessous, et nous résoudrons le problème ensemble. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches alternatives dans vos propres projets.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}