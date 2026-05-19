---
category: general
date: 2026-03-24
description: Créer un document PDF et apprendre à définir la position absolue du texte
  balisé. Ce tutoriel montre comment ajouter un élément span, comment ajouter du contenu
  balisé et positionner le texte sur la page.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: fr
og_description: Créez un document PDF et voyez instantanément comment définir une
  position absolue, ajouter un élément <span> et positionner du texte sur la page
  avec du contenu PDF balisé.
og_title: Créer un document PDF – Positionnement absolu du texte balisé
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Créer un document PDF – Définir la position absolue du texte balisé
url: /fr/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document PDF – Définir une position absolue pour du texte balisé

Vous avez déjà eu besoin de **créer un document pdf** contenant du texte accessible, balisé et positionné exactement où vous le souhaitez ? Peut‑être que vous construisez un PDF de type formulaire où le libellé doit se placer à une coordonnée précise, ou que vous générez un certificat et que le nom doit s’aligner parfaitement avec une image de fond.  

Dans ce guide, nous parcourrons un exemple complet et exécutable qui montre **comment ajouter du contenu balisé**, **définir une position absolue**, et **ajouter un élément span** afin que vous puissiez **positionner du texte sur la page** sans deviner. Aucun lien externe — juste le code à copier‑coller, plus des explications du « pourquoi » derrière chaque ligne.

## Prérequis

- .NET 6+ (ou .NET Framework 4.6+) avec un compilateur C#  
- Aspose.Pdf for .NET (dernière version au moment de la rédaction, 23.12) installé via NuGet  
- Familiarité de base avec la syntaxe C#  

Si vous avez tout cela, commençons.

---

## Créer un document PDF – Définir la position absolue

La première chose que nous faisons est d’instancier un `Document` vide. Cet objet représente l’ensemble du fichier PDF et nous donne accès à l’arbre de contenu balisé.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Pourquoi c’est important :**  
`Document` est la racine de la structure PDF. En le créant d’abord, nous nous assurons qu’il existe une toile à la fois pour les éléments visuels (pages, graphiques) et pour la structure logique (balises). L’instruction `using` garantit que le fichier est correctement libéré, ce qui évite les fuites de descripteurs de fichiers sous Windows.

---

## Activer le contenu balisé (Comment ajouter du balisage)

Avant de pouvoir insérer des éléments balisés, le document doit être marqué comme *balisé*. Aspose.Pdf crée automatiquement un objet `TaggedContent`, mais il faut tout de même activer le drapeau.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Que se passe-t-il en coulisses ?**  
Définir `TaggedContent` à `true` indique aux lecteurs PDF que le fichier contient un arbre de structure logique. C’est crucial pour les lecteurs d’écran et pour que la méthode `SetPosition` fonctionne correctement sur un élément span.

---

## Obtenir l’élément racine de l’arbre de contenu balisé

L’élément racine est le point d’entrée pour toutes les balises structurelles (comme `<Document>`, `<Section>`, `<Span>`). Pensez‑y comme le « body » invisible du PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Pourquoi nous avons besoin de la racine :**  
Toutes les balises suivantes doivent être attachées quelque part dans l’arbre ; sinon elles n’apparaîtront pas dans la hiérarchie d’accessibilité.

---

## Ajouter un élément Span – Le bloc de construction pour le texte en ligne

Un *span* est l’équivalent PDF d’un `<span>` HTML — parfait pour de courts morceaux de texte que vous voulez positionner précisément.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Note de conception :**  
Si vous avez besoin d’un formatage plus riche (gras, italique, hyperliens), vous pouvez envelopper le span dans un `<Paragraph>` ou utiliser des objets `TextFragment` plus tard. Pour le positionnement absolu, un span simple est le plus léger.

---

## Définir la position absolue – X=100, Y=200

Voici la partie amusante : placer le span à un emplacement exact sur la page. Le système de coordonnées commence au coin inférieur‑gauche (0,0) et utilise des points (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Pourquoi le positionnement absolu ?**  
Lorsque vous avez besoin d’une mise en page pixel‑perfect — pensez certificats, factures ou formulaires — le flux relatif (texte de gauche à droite) ne suffit pas. `SetPosition` contourne le flux de texte normal et épingle l’élément à l’endroit que vous spécifiez.

---

## Ajouter du texte au Span

Une fois le span positionné, nous injectons la chaîne réelle.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Astuce :**  
Si vous avez besoin de caractères Unicode ou de scripts de droite à gauche, passez simplement la chaîne ; Aspose.Pdf gère l’encodage automatiquement.

---

## Ajouter le Span à l’élément racine

Enfin, nous attachons le span à l’arbre logique du document afin qu’il devienne partie intégrante du PDF final.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Que se passe‑t‑il si vous oubliez cette étape ?**  
Le span existerait en mémoire mais ne serait jamais sérialisé dans le fichier, vous ne verriez donc aucun texte et l’arbre d’accessibilité serait incomplet.

---

## Exemple complet, exécutable

Voici le programme complet que vous pouvez coller dans une application console. Il crée un PDF d’une page, ajoute un span balisé à (100, 200), et enregistre le fichier sous le nom `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Résultat attendu :**  
Ouvrez `TaggedPositioned.pdf` dans n’importe quel visualiseur (Adobe Acrobat, Foxit, etc.). Vous verrez la phrase **« Positioned tagged text »** exactement à 100 pt du bord gauche et 200 pt du bord inférieur de la page. Si vous inspectez le panneau *Tags*, un élément `<Span>` sera listé sous la racine du document, confirmant que le contenu est correctement balisé.

---

## Questions fréquentes & cas particuliers

### Et si je dois positionner du texte sur une page spécifique autre que la première ?

Ajoutez la page souhaitée (`var page = pdfDocument.Pages[3];`) avant d’appeler `SetPosition`. Le span s’attachera automatiquement au contexte de page actif.

### Puis‑je définir la position en pouces ou en centimètres ?

`SetPosition` accepte des points. Convertissez avec les formules :  
- **Pouces → points** : `points = inches * 72`  
- **Centimètres → points** : `points = cm * 28.3465`

### Comment changer la police ou la couleur du span ?

Après avoir créé le span, vous pouvez récupérer son `TextState` et le modifier :

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Et si le document possède déjà des balises existantes ?

Vous pouvez toujours créer un nouveau span et l’ajouter à n’importe quel élément existant (`rootElement`, une `<Section>` spécifique, etc.). Veillez simplement à conserver une hiérarchie logique — les lecteurs d’écran attendent un arbre bien structuré.

### Cela fonctionne‑t‑il avec la conformité PDF/A ou PDF/UA ?

Oui. Les PDF balisés sont une exigence de base pour PDF/UA. Si vous avez besoin de PDF/A, appelez `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` après avoir construit le contenu.

---

## Astuces pro & pièges à éviter

- **Astuce pro** : ajoutez toujours une page avant de positionner du contenu. Sans page, `SetPosition` échoue silencieusement parce qu’il n’y a nulle part où rendre le texte.
- **Surveillez les unités** : mélanger des pixels d’un design UI avec des points PDF déplacera votre texte. Vérifiez vos conversions.
- **Indice de performance** : si vous générez des milliers de PDFs, réutilisez une même instance `Document` et appelez `pdfDocument.Pages.Clear()` entre les exécutions pour éviter une allocation mémoire excessive.
- **Rappel accessibilité** : le balisage n’est pas qu’une option ; de nombreuses réglementations (Section 508, EN 301 549) l’exigent. Utiliser `CreateSpanElement` garantit que le texte est détectable par les technologies d’assistance.

---

## Conclusion

Nous venons de **créer un document pdf** à partir de zéro, **définir une position absolue**, **ajouter un élément span**, et démontrer **comment ajouter du contenu balisé** afin que vous puissiez **positionner du texte sur la page** avec une précision pixel‑perfect. L’exemple complet est prêt à être exécuté, et l’explication a couvert à la fois le *comment* et le *pourquoi*—exactement ce que recherchent les développeurs (et les assistants IA) lorsqu’ils ont besoin d’une solution fiable.

Ensuite, vous pourriez explorer :

- Ajouter des images derrière le texte positionné pour des certificats filigranés.  
- Utiliser `CreateParagraphElement` pour des blocs multi‑lignes qui nécessitent tout de même un placement absolu.  
- Exporter vers PDF/UA pour satisfaire des audits d’accessibilité stricts.  

N’hésitez pas à ajuster les coordonnées, les polices ou les couleurs—l’expérimentation est le moyen le plus rapide de maîtriser la génération de PDF balisés. Si vous rencontrez un problème, laissez un commentaire ci‑dessous ; bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}