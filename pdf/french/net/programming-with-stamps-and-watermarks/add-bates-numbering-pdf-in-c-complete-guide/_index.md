---
category: general
date: 2026-05-27
description: Ajouter une numérotation Bates à un PDF avec Aspose.Pdf en C#. Apprenez
  à ajouter rapidement la numérotation Bates, à personnaliser le format et à automatiser
  le marquage des documents juridiques.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: fr
og_description: Ajouter une numérotation Bates à un PDF avec Aspose.Pdf en C#. Ce
  guide montre comment ajouter la numérotation Bates, configurer les préfixes et enregistrer
  le résultat.
og_title: Ajouter la numérotation Bates à un PDF en C# – Tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Ajouter la numérotation Bates à un PDF en C# – Guide complet
url: /fr/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates PDF en C# – Guide complet

Vous êtes‑vous déjà demandé **comment ajouter une numérotation Bates** à un PDF sans passer des heures à bricoler avec des outils manuels ? Vous n'êtes pas seul—les équipes juridiques, les auditeurs et les spécialistes de l'e‑discovery ont tous besoin d'une méthode fiable pour **ajouter une numérotation Bates aux fichiers PDF** de manière programmatique.  

Dans ce tutoriel, nous parcourrons une solution concise, de bout en bout, en utilisant Aspose.Pdf pour .NET, afin que vous puissiez appliquer des numéros Bates à n'importe quel document avec seulement quelques lignes de code C#.

## Ce que vous apprendrez

- Comment ouvrir un PDF existant avec Aspose.Pdf  
- Comment créer un artefact de numérotation Bates et affiner son format  
- Comment attacher l'artefact à chaque page (ou seulement à la première)  
- Comment enregistrer le fichier mis à jour et vérifier le résultat  

Aucune expérience préalable avec Aspose n'est requise—juste une compréhension de base de C# et .NET. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez copier‑coller dans n'importe quel projet.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+)  
- Package NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- Un fichier PDF source que vous souhaitez marquer (placez‑le dans un dossier que vous pouvez référencer)

> **Astuce :** Si vous n'avez pas encore de licence, Aspose propose une clé temporaire gratuite qui supprime les filigranes d'évaluation.

## Étape 1 – Ouvrir le document PDF source  

Tout d'abord, nous avons besoin d'un objet `Document` qui représente le fichier sur le disque. Considérez cela comme le chargement d'une toile vierge sur laquelle nous appliquerons plus tard les numéros Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Pourquoi c'est important :** Ouvrir le document à l'intérieur d'un bloc `using` garantit que toutes les ressources non gérées sont libérées rapidement, ce qui est particulièrement crucial pour les gros PDF.

## Étape 2 – Créer un artefact de numérotation Bates  

Un *BatesNumberingArtifact* est la façon dont Aspose décrit l'apparence des numéros. Vous pouvez définir un préfixe, un numéro de départ, un incrément, et même une chaîne de format personnalisée.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Pourquoi vous pourriez modifier ces valeurs :**  
- **Prefix** est utile pour les identifiants de dossiers (« CASE‑», « DOC‑»).  
- **StartNumber** vous permet de poursuivre une série précédente.  
- **Increment** peut être réglé à 2 si vous avez besoin d'une numérotation paire/impair.  
- **Format** accepte n'importe quel format composite .NET ; `{0:D5}` garantit cinq chiffres avec des zéros en tête.

## Étape 3 – Attacher l'artefact aux pages souhaitées  

Vous pouvez ajouter l'artefact à une seule page, à une plage, ou à l'ensemble du document. Pour la plupart des flux de travail juridiques, nous l'attachons à *toutes* les pages, mais l'exemple ci‑dessous montre le cas minimal—l'ajout à la première page.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

If you need to cover all pages, loop through them:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Pourquoi cette étape est cruciale :** Les artefacts sont rendus *après* le contenu de la page, de sorte que les numéros apparaissent au-dessus du texte existant sans modifier la mise en page originale.

## Étape 4 – Enregistrer le PDF modifié  

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser l'original ou créer un nouveau fichier—ici nous générerons une copie fraîche nommée `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Lorsque vous ouvrirez `bates.pdf`, vous verrez « ABC01000 » (ou le format que vous avez choisi) estampillé à l'emplacement par défaut—généralement en bas à droite.

## Exemple complet fonctionnel  

En combinant le tout, voici le programme complet que vous pouvez compiler et exécuter :

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme, la console affiche :

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

L'ouverture de `bates.pdf` montre le préfixe « ABC » suivi d'une séquence de cinq chiffres remplis de zéros sur chaque page—exactement ce que vous avez demandé au code.

## Questions fréquentes & cas particuliers

### Puis-je positionner le numéro Bates ailleurs ?

Oui. Utilisez la propriété `Location` du `BatesNumberingArtifact` (par ex., `Location = new Position(10, 10)`) pour placer le numéro à des coordonnées X/Y personnalisées. Vous pouvez également définir `HorizontalAlignment` et `VerticalAlignment` pour plus de contrôle.

### Que faire si mon PDF comporte des milliers de pages ?

Aspose.Pdf diffuse les pages de manière efficace, mais il reste judicieux de traiter par lots si vous atteignez les limites de mémoire. La classe `Document` prend également en charge `PdfConverter` pour une sauvegarde incrémentielle.

### Comment changer la police ou la couleur ?

Wrap the artifact in a `TextState` object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Ai‑je besoin d'une licence pour une utilisation en production ?

Une version sous licence supprime les filigranes d'évaluation et débloque les performances complètes. L'essai gratuit fonctionne bien pour les tests et les preuves de concept.

## Vérification – Contrôle visuel rapide  

If you prefer an automated verification, Aspose can extract the text of a page and confirm the presence of the prefix:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Running this after the save step will print `Bates number verified.` if everything went smoothly.

## Conclusion  

Vous savez maintenant **comment ajouter une numérotation Bates aux fichiers PDF** en utilisant Aspose.Pdf en C#. De l'ouverture du document à la configuration de l'artefact, en passant par son attachement aux pages et l'enregistrement du résultat, le processus est simple et entièrement scriptable.  

Prochaines étapes ? Essayez d'expérimenter avec :

- Différentes valeurs de `Prefix` pour plusieurs lots de dossiers  
- `Location` et `TextState` personnalisés pour le branding  
- Ajout de préfixes spécifiques à chaque page (par ex., « VOL‑1‑», « VOL‑2‑») en ajustant `StartNumber` à chaque itération de boucle  

Ces ajustements vous permettent d'adapter la solution à presque n'importe quel flux de travail juridique ou d'archivage.  

Vous avez d'autres questions sur **comment ajouter une numérotation Bates** pour des PDF multilingues ou des fichiers chiffrés ? Laissez un commentaire ci‑dessous, et bon codage !

## Tutoriels associés

- [Comment ajouter et personnaliser les numéros de page dans les PDF avec Aspose.PDF pour .NET | Guide de manipulation de documents](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Comment ajouter différents en‑têtes dans un PDF avec Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Comment ajouter un pied de page de tampon texte dans les PDF avec Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}