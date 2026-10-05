---
category: general
date: 2026-02-25
description: tutoriel de numérotation Bates – apprenez comment ajouter des numéros
  de page PDF et appliquer une numérotation Bates personnalisée avec Aspose.Pdf en
  C#. Guide étape par étape avec le code complet.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: fr
og_description: Le tutoriel sur la numérotation Bates vous montre comment ajouter
  des numéros de page PDF et une numérotation Bates personnalisée en C#. Code complet,
  explications et astuces.
og_title: Tutoriel de numérotation Bates – Ajouter des numéros Bates aux PDF avec
  C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Tutoriel de numérotation Bates : ajouter des numéros Bates aux PDF avec C#'
url: /fr/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel de numérotation Bates – Ajouter des numéros Bates aux PDF en C#

Vous êtes-vous déjà demandé comment ajouter des numéros de page à un PDF tout en intégrant un numéro Bates de style juridique ? Vous n'êtes pas seul. Dans ce **tutoriel de numérotation Bates** nous allons passer en revue tout ce que vous devez savoir pour tamponner chaque page d’un PDF avec un préfixe personnalisé, des zéros de tête et un positionnement précis—en utilisant Aspose.Pdf pour .NET.

Bonne nouvelle ? C’est assez simple une fois les concepts de base compris. À la fin de ce guide, vous disposerez d’un programme exécutable qui prend *input.pdf* et génère *bates_out.pdf* avec une étiquette « ABC‑01000 » sur chaque page. Allons-y.

## Ce dont vous avez besoin

- **Aspose.Pdf pour .NET** (version 23.10 ou ultérieure). La bibliothèque est commerciale, mais une version d’essai gratuite suffit pour l’apprentissage.
- SDK .NET 6+ (toute version récente convient).
- Un environnement de développement C# de base — Visual Studio, VS Code ou Rider.
- Un PDF d’entrée pour expérimenter (tout document multipage illustrera l’effet).

Aucun package NuGet supplémentaire au‑delà d’Aspose.Pdf n’est requis, et le code fonctionne sous Windows, Linux ou macOS sans modification.

## Étape 1 : Charger le document PDF source (tutoriel de numérotation Bates – initialisation)

Nous créons d’abord un objet `Document` qui représente le PDF que nous voulons modifier. Considérez‑le comme le chargement d’une toile vierge sur laquelle vous pouvez dessiner.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Pourquoi c’est important :** Sans charger le fichier, il n’y a rien à annoter. La vérification de validité empêche un échec silencieux plus tard lorsque vous essayez d’ajouter des artefacts à une collection de pages inexistante.

## Étape 2 : Définir l’artefact de numérotation Bates (comment ajouter des Bates)

Un *BatesNumberingArtifact* indique à Aspose où et comment dessiner l’identifiant. Vous pouvez contrôler le préfixe, le numéro de départ, le remplissage de zéros, la taille de police et les coordonnées X/Y exactes.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Pourquoi c’est important :** La propriété `LeadingZeros` garantit que chaque étiquette a la même longueur, ce qui est crucial pour les documents juridiques où l’alignement compte. Ajustez `X` et `Y` pour déplacer le tampon vers le coin supérieur‑droit, inférieur‑gauche, ou où votre flux de travail le nécessite.

## Étape 3 : Attacher l’artefact à chaque page (ajouter des numéros de page pdf)

Nous parcourons chaque page et y attachons le même artefact. C’est ici que l’exigence *add page numbers pdf* est satisfaite — chaque page reçoit automatiquement son propre libellé séquentiel.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Pourquoi c’est important :** En ajoutant l’artefact à la collection `Artifacts` plutôt qu’en dessinant du texte manuellement, nous laissons Aspose gérer la logique de numérotation, les zéros de tête et le rendu. Cela réduit les bugs et garde le code concis.

## Étape 4 : Enregistrer le PDF modifié (ajouter la numérotation Bates)

Enfin, nous persistons les modifications dans un nouveau fichier. C’est une bonne pratique d’écrire sous un nom de fichier différent afin de conserver l’original intact.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Pourquoi c’est important :** La méthode `Save` écrit l’ensemble du PDF, intégrant les artefacts dans le flux de contenu de la page. Le fichier résultant peut être ouvert avec n’importe quel lecteur PDF et affichera les numéros Bates exactement comme spécifié.

## Exemple complet fonctionnel (Toutes les étapes combinées)

Voici le programme complet, prêt à être exécuté. Copiez‑collez‑le dans un projet d’application console, remplacez les chemins d’accès factices, et appuyez sur **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Résultat attendu

Ouvrez *bates_out.pdf* avec Adobe Reader, Foxit ou tout autre lecteur. Vous devriez voir une étiquette comme **ABC‑01000** sur la première page, **ABC‑01001** sur la deuxième, etc., positionnée à 50 pts du bord gauche et 30 pts du bord inférieur. Les nombres sont alignés à droite grâce aux zéros de tête, donnant au document un aspect propre et professionnel.

## Variantes courantes & cas limites

| Scénario | Comment ajuster |
|----------|-----------------|
| **Préfixe différent** | Changez `Prefix = "XYZ"` dans la définition de l’artefact. |
| **Départ à un numéro personnalisé** | Définissez `Start = 5000` (ou tout entier). |
| **Placer le numéro dans le coin supérieur‑droit** | Utilisez `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Modifier la taille de police pour les documents plus grands** | Modifiez `FontSize = 12` (ou toute taille). |
| **Ajouter un rectangle d’arrière‑plan** | Créez un `RectangleArtifact` et ajoutez‑le avant le `BatesNumberingArtifact`. |
| **Ignorer certaines pages** | Dans la boucle `foreach`, ajoutez `if (page.Number % 2 == 0) continue;` pour sauter les pages paires. |

**Astuce pro :** Testez toujours d’abord avec un PDF court. Il est plus rapide de vérifier le positionnement avant d’exécuter le script sur un fichier de 200 pages.

## Questions fréquentes

- **Cela fonctionne‑t‑il avec des PDF chiffrés ?**  
  Aspose.Pdf peut ouvrir des fichiers protégés par mot de passe si vous fournissez le mot de passe via `Document(string, string)`. L’artefact Bates sera quand même appliqué après le déchiffrement.

- **Puis‑je ajouter à la fois des numéros Bates et des numéros de page classiques ?**  
  Oui. Ajoutez un `PageNumberArtifact` en parallèle du `BatesNumberingArtifact`. Chaque artefact maintient son propre compteur.

- **Que faire si mon PDF a des tailles de page différentes ?**  
  Les valeurs `Position` sont en points absolus. Pour les documents à tailles mixtes, calculez la position par page à l’intérieur de la boucle en utilisant `page.PageInfo.Width` et `page.PageInfo.Height`.

## Prochaines étapes & sujets associés

Maintenant que vous avez maîtrisé le **tutoriel de numérotation Bates**, vous pourriez explorer :

- **Ajout de filigranes** – approche d’artefact similaire avec `TextArtifact`.
- **Fusion de plusieurs PDF** – utilisez `Document.AppendDocument`.
- **Extraction de texte pour l’indexation de recherche** – classe `TextAbsorber`.
- **Automatisation du traitement par lots** – parcourez un dossier de PDF et appliquez le même artefact.

Tous ces sujets s’appuient sur les mêmes concepts que vous venez d’apprendre, vous plaçant ainsi en excellente position pour élargir votre boîte à outils d’automatisation PDF.

---

*Bon codage ! Si vous rencontrez des difficultés ou avez des idées de personnalisation supplémentaires, n’hésitez pas à laisser un commentaire ci‑dessous. Le monde de la manipulation PDF est vaste, mais avec un solide **tutoriel de numérotation Bates** sous la ceinture, vous avez déjà une longueur d’avance.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}