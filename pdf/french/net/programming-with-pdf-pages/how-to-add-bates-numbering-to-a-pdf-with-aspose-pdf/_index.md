---
category: general
date: 2026-10-07
description: Apprenez comment ajouter une numérotation Bates à un PDF en C#. Ce guide
  étape par étape couvre également la numérotation des pages PDF et d’autres astuces
  de numérotation.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: fr
lastmod: 2026-10-07
og_description: Ajoutez rapidement une numérotation Bates à un PDF. Suivez ce tutoriel
  pour maîtriser la numérotation des pages PDF, numéroter les pages PDF et automatiser
  le suivi des documents.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Ajouter une numérotation Bates aux PDF en C# – guide complet Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Comment ajouter une numérotation Bates à un PDF avec Aspose.Pdf
url: /fr/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter une numérotation Bates à un PDF avec Aspose.Pdf

Si vous devez **ajouter une numérotation Bates** à un PDF, ce guide vous montre exactement comment le faire en C#. Que vous prépariez des dossiers juridiques, gériez des dossiers de cas, ou que vous souhaitiez simplement une **numérotation de pages PDF** fiable, les étapes ci‑dessous vous offrent une solution complète et exécutable.

Dans ce tutoriel, vous apprendrez comment :

* Charger un fichier PDF existant.
* Configurer les options de numérotation Bates telles que le préfixe, le numéro de départ, le remplissage des chiffres, le séparateur et le suffixe.
* Appliquer la numérotation à chaque page.
* Enregistrer le document mis à jour.

Aucun outil externe n'est requis en dehors de la bibliothèque Aspose.Pdf pour .NET, et le code fonctionne avec .NET 6+ ainsi qu'avec .NET Framework 4.7.2+.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir :

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Fournit les classes `Document` et `BatesNumberingOptions` utilisées dans le code. |
| **.NET SDK** (6.0 or later recommended) | Vous permet de compiler et d'exécuter l'application console C#. |
| **A source PDF** you want to number | Le tutoriel utilise `source.pdf` comme exemple ; remplacez le chemin par votre propre fichier. |
| **Write permission** to the output folder | L'appel `Save` doit écrire le nouveau fichier. |

Vous pouvez installer la bibliothèque avec la commande CLI suivante :

```bash
dotnet add package Aspose.Pdf
```

---

## Étape 1 : Créer un nouveau projet console

Ouvrez un terminal et exécutez :

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Cela crée un projet C# minimal que nous remplirons avec le code nécessaire pour **ajouter une numérotation Bates**.

---

## Étape 2 : Ajouter les directives `using` requises

Ouvrez `Program.cs` et ajoutez les espaces de noms en haut du fichier :

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` vous donne accès à la classe `Document` pour charger et enregistrer des PDF.  
* `Aspose.Pdf.Text` contient `BatesNumberingOptions`, l'objet qui définit l'apparence des numéros.

---

## Étape 3 : Charger le PDF source

La première ligne opérationnelle charge le PDF que vous souhaitez numéroter. Remplacez `"YOUR_DIRECTORY/source.pdf"` par le chemin réel de votre fichier.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Si le fichier est introuvable, Aspose lève une `FileNotFoundException`. Pour éviter cela, vous pouvez valider le chemin au préalable :

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Étape 4 : Définir les options de numérotation Bates

`BatesNumberingOptions` vous permet de contrôler chaque élément visuel de la numérotation. L'exemple ci‑dessous montre une configuration typique pour les dossiers de cas juridiques :

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Pourquoi chaque propriété est importante**

| Property | Purpose |
|----------|---------|
| `Prefix` | Vous aide à regrouper les documents par projet, client ou dossier. |
| `StartNumber` | Définit le compteur initial ; utile lorsque vous avez déjà des fichiers numérotés. |
| `Digits` | Assure une largeur uniforme, facilitant le tri. |
| `Separator` | Améliore la lisibilité, notamment lors de la combinaison du préfixe et du suffixe. |
| `Suffix` | Vous permet d'ajouter une année, une version ou tout autre identifiant final. |

Vous pouvez également contrôler le placement (haut, bas, gauche, droite) et le style de police en accédant à `batesOptions.Position` et `batesOptions.Font`. Dans la plupart des scénarios, les valeurs par défaut (en bas à droite, Times New Roman 12 pt) fonctionnent bien.

---

## Étape 5 : Appliquer la numérotation à chaque page

L'appel à `pdf.BatesNumbering.Add` insère les numéros sur chaque page dans l'ordre d'apparition.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Si vous devez **numéroter les pages PDF** uniquement sur un sous‑ensemble (par ex., ignorer la page de garde), vous pouvez passer une `PageCollection` à la place :

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Étape 6 : Enregistrer le PDF mis à jour

Enfin, écrivez le document modifié sur le disque. Le nom du fichier reflète généralement que le PDF contient désormais des numéros Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Si le dossier de sortie n'existe pas, Aspose le crée automatiquement. Cependant, vous devez vous assurer d'avoir les permissions d'écriture pour éviter une `UnauthorizedAccessException`.

---

## Exemple complet et exécutable

En rassemblant tous les éléments, voici un programme complet que vous pouvez copier, coller et exécuter :

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Sortie attendue** (console) :

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Ouvrez `bates_numbered.pdf` et vous verrez chaque page étiquetée comme `CASE-001000-2025`, `CASE-001001-2025`, etc., positionnée dans le coin inférieur droit par défaut.

---

## Questions fréquemment posées (FAQ)

### 1. Puis-je changer l'emplacement des numéros ?

Oui. Définissez `batesOptions.Position = new Position(10, 10, 10, 10);` où les quatre valeurs représentent les marges depuis le haut, le bas, la gauche et la droite. Aspose fournit également des énumérations prédéfinies comme `BatesNumberingPosition.BottomCenter`.

### 2. Que se passe-t-il si mon PDF contient déjà des numéros de page ?

L'ajout de numéros Bates **s'empilera** sur les numéros existants. Pour éviter l'encombrement visuel, soit masquez les numéros originaux (s'ils font partie d'un calque texte), soit ajustez la taille de police et la position dans `batesOptions`.

### 3. Cela fonctionne-t-il avec des PDF chiffrés ?

Aspose peut ouvrir les PDF protégés par mot de passe si vous fournissez le mot de passe :

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

La numérotation Bates est alors appliquée de la même manière.

### 4. Comment **numéroter les pages PDF** avec un simple compteur séquentiel (sans préfixe/suffixe) ?

Il suffit de définir `Prefix = string.Empty` et `Suffix = string.Empty` :

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Puis-je utiliser cette approche dans ASP.NET Core pour servir des PDF à la volée ?

Absolument. Chargez le document, appliquez la numérotation, puis écrivez le flux dans la réponse HTTP :

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Cas limites et conseils de bonnes pratiques

| Situation | Recommended approach |
|-----------|----------------------|
| **Large PDFs (hundreds of pages)** | Appelez `pdf.BatesNumbering.Add` **après** avoir effectué toutes les transformations au niveau des pages afin d'éviter de retraiter les mêmes pages plusieurs fois. |
| **Custom fonts** | Définissez `batesOptions.Font = FontRepository.FindFont("Arial")` et ajustez `batesOptions.FontSize` pour une meilleure lisibilité sur les documents numérisés. |
| **Performance‑critical batch jobs** | Réutilisez une seule instance `Document` lors du traitement de nombreux fichiers dans une boucle ; libérez‑la après chaque itération pour libérer la mémoire. |
| **International characters** | Utilisez des polices compatibles Unicode (par ex., `Times New Roman Unicode`) pour garantir que le préfixe ou le suffixe s'affiche correctement. |
| **Version compatibility** | Le code fonctionne avec Aspose.Pdf 23.10 et plus. Si vous ciblez une version antérieure, vérifiez la référence API pour d'éventuels changements de noms de propriétés. |

---

## Conclusion

Vous savez maintenant comment **ajouter une numérotation Bates** à un PDF en utilisant Aspose.Pdf pour .NET. Le tutoriel a couvert le chargement d'un PDF, la configuration de `BatesNumberingOptions`, l'application des numéros à chaque page et l'enregistrement du résultat. Avec ces blocs de construction, vous pouvez également implémenter une **numérotation de pages PDF** générique, **numéroter les pages PDF** avec des formats personnalisés, et intégrer le processus dans des pipelines d'automatisation plus vastes.

**Prochaines étapes**

* Explorez davantage l'API **bates numbering pdf** pour personnaliser la police, la couleur et le placement.  
* Combinez cette technique avec les **signatures numériques** pour créer des dossiers juridiques à l'épreuve de la falsification.  
* Examinez les capacités de **fusion de PDF** d'Aspose si vous devez concaténer plusieurs dossiers avant la numérotation.

N'hésitez pas à expérimenter différents préfixes, suffixes et longueurs de chiffres pour correspondre aux normes de classement de votre organisation. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un document PDF C# – Guide d'ajout de numérotation Bates](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [Comment ajouter une numérotation Bates dans un PDF avec C# – Guide complet](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Tutoriel Aspose PDF – Insérer une page blanche et mettre à jour la numérotation Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}