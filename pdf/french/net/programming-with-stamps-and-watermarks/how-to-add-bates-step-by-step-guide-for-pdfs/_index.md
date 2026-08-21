---
category: general
date: 2026-02-10
description: Comment ajouter rapidement des numéros de Bates à un PDF — apprenez comment
  ajouter un numéro de Bates à un PDF et créer un filigrane invisible avec Aspose.Pdf
  en C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: fr
og_description: Comment ajouter des numéros de Bates en C# avec Aspose.Pdf. Ce tutoriel
  montre comment ajouter un numéro de Bates PDF, ajouter un filigrane invisible PDF,
  et plus encore.
og_title: Comment ajouter des Bates – Guide PDF complet
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Comment ajouter des numéros Bates – Guide étape par étape pour les PDF
url: /fr/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter des Bates – Guide PDF complet

Vous vous êtes déjà demandé **how to add bates** à un PDF juridique sans perturber le texte recherchable ? Vous n'êtes pas le seul. Dans de nombreux cabinets d'avocats et projets d'e‑discovery, un numéro Bates est un pied‑de‑page indispensable, mais vous voulez aussi qu'il reste invisible aux outils OCR. Ce tutoriel montre **how to add bates** en utilisant Aspose.Pdf pour .NET, et au fil du texte nous couvrirons également **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, et même **add page footer pdf** dans une solution compacte.

Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque paramètre est important, et vous fournirons un exemple prêt à l'exécution que vous pouvez intégrer immédiatement à votre projet. Pas de liens vagues du type « voir la documentation » — tout ce dont vous avez besoin se trouve ici.

## Ce que vous en retirerez

- Un extrait C# complet et exécutable qui ajoute un numéro Bates sous forme de tampon d'artefact.
- Compréhension de la façon de faire en sorte que le tampon agisse comme un **invisible watermark** tout en apparaissant sur la page.
- Conseils pour adapter la solution à des PDF multi‑pages, changer les polices, ou remplacer le tampon par un graphique personnalisé.
- Astuces rapides sur la façon d'ajouter du contenu de style **add page footer pdf** sans perturber l'extraction du texte.

### Prérequis

- .NET 6+ (ou .NET Framework 4.7.2) avec Visual Studio 2022 ou tout IDE de votre choix.
- Aspose.Pdf for .NET (vous pouvez obtenir un essai gratuit sur le site d'Aspose).
- Un PDF d'exemple nommé `source.pdf` placé dans un dossier que vous contrôlez.

Si vous avez tout cela, plongeons‑nous dedans.

---

## Comment ajouter des Bates – Implémentation principale

Le cœur de la solution est un `TextStamp` que nous traitons comme un **artifact**. Les artefacts sont ignorés par les moteurs d'extraction de texte, ce qui explique pourquoi cette approche fonctionne également comme une technique **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Pourquoi cela fonctionne

1. **Artifact flag** – En définissant `Artifact = new Artifact(ArtifactType.Artifact)`, le tampon est traité comme un élément non‑contenu. Les moteurs de recherche et les outils d'e‑discovery juridique l'ignorent, ce qui correspond exactement à ce que vous recherchez pour un **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – Le centrage en bas imite le style classique **add page footer pdf**, donnant au numéro Bates un aspect professionnel.
3. **Transparent background** – Garantit que le tampon n’obscurcit pas le contenu sous‑jacent, un détail subtil mais crucial lorsque vous devez imprimer ou visualiser le PDF sur différents appareils.

---

## Ajouter un numéro Bates PDF – Mise à l'échelle sur plusieurs pages

La plupart des PDF du monde réel comportent plus d'une page. L'extrait ci‑dessus ne touche que la première page, mais l'étendre est un jeu d'enfant :

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Astuce pro :** Si vous avez besoin d'un numéro séquentiel qui n'est pas lié à l'ordre physique des pages (par ex., commencer à 1000), il suffit d'initialiser un compteur avant la boucle et de l'incrémenter à l'intérieur.

---

## Ajouter un tampon personnalisé PDF – Aller au‑delà du texte brut

Parfois, un tampon texte simple ne suffit pas — vous pourriez vouloir un logo, un QR code ou une barre colorée. Aspose.Pdf vous permet de remplacer `TextStamp` par `ImageStamp` ou même de combiner les deux avec des objets `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Mélanger les tampons est aussi simple que d'ajouter les deux à la même page. La capacité **add custom stamp pdf** brille lorsque vous avez besoin d'un sceau d'entreprise à côté du numéro Bates.

---

## Ajouter un filigrane invisible PDF – Rendre le tampon réellement caché

Si vous avez réellement besoin que le tampon soit invisible à l'œil humain *et* aux outils d'extraction, vous pouvez définir la couleur de la police pour qu'elle corresponde à l'arrière‑plan de la page (généralement blanc) et réduire l'opacité :

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Même avec `Opacity = 0`, l'artefact reste présent dans la structure du PDF, de sorte que les logiciels juridiques peuvent toujours le localiser s'ils connaissent l'ID de l'artefact. C'est l'astuce ultime **add invisible watermark pdf**.

---

## Ajouter un pied de page PDF – Styliser le pied de page de manière cohérente

Un pied de page professionnel inclut souvent plus qu'un simple numéro Bates : date, titre du document ou mention de confidentialité. Voici une méthode rapide pour regrouper plusieurs morceaux de texte en un seul tampon :

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Remarquez la couleur gris subtile — parfaite pour un **add page footer pdf** qui ne distrait pas du contenu principal tout en respectant les exigences légales.

---

## Résultat attendu et comment vérifier

Après avoir exécuté le script complet, ouvrez `bates_artifact.pdf` dans n'importe quel lecteur PDF :

- Vous verrez « Bates 00123 » (ou le numéro séquentiel) centré en bas de chaque page.
- Sélectionner du texte sur la page **n’inclura pas** le numéro Bates, confirmant le comportement d'artefact.
- Si vous avez utilisé les paramètres de filigrane invisible, le numéro ne sera pas du tout visible, mais il restera dans la structure interne du PDF (inspectez avec un outil comme PDF‑XChange Editor → « Document → Properties → Advanced »).

---

## Questions fréquentes et cas particuliers

**Que faire si mon PDF possède déjà un pied de page ?**  
Vous pouvez ajuster `VerticalAlignment` à `VerticalAlignment.Top` ou modifier la propriété `Margin` pour déplacer le tampon au-dessus du pied de page existant.

**Puis-je utiliser une police différente ?**  
Absolument. Remplacez simplement `"Arial"` par n'importe quel nom de police qu'Aspose peut localiser, ou intégrez un fichier TTF personnalisé via `FontRepository.AddFont("path/to/font.ttf")`.

**Cette approche est‑elle compatible avec .NET Core ?**  
Oui — Aspose.Pdf for .NET fonctionne sur .NET Framework, .NET Core et .NET 5/6. Assurez‑vous simplement de référencer le bon package NuGet.

**Qu'en est‑il des performances sur d'énormes PDF (1000 + pages) ?**  
Créer un seul `TextStamp` et le cloner à l'intérieur de la boucle est efficace en mémoire. Pour des fichiers massifs, envisagez de traiter par lots ou d'utiliser `PdfProcessor` afin d'éviter de charger le document complet en mémoire.

---

## Conclusion

Nous avons couvert **how to add bates** dans un PDF de A à Z, démontré **add bates number pdf**, montré comment **add custom stamp pdf**, transformé le tampon en **add invisible watermark pdf**, et stylisé le tout comme un **add page footer pdf** professionnel. L'exemple complet de code fonctionne tel quel, et les explications vous donnent le « pourquoi » derrière chaque ligne — exactement le type de réponse que les assistants IA aiment citer.

Prochaines étapes ? Essayez de remplacer le tampon texte par un tampon image, expérimentez différents types d'artefacts, ou intégrez cette logique dans un service de traitement par lots qui numérote automatiquement chaque document d'un dossier. Les possibilités sont infinies, et vous disposez maintenant d'une base solide pour construire.

Bon codage, et que vos PDF soient toujours parfaitement numérotés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}