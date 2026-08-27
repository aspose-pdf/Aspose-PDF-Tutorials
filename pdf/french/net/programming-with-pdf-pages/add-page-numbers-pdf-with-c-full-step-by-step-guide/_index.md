---
category: general
date: 2026-01-02
description: Ajoutez rapidement des numéros de page à un PDF en utilisant Aspose.Pdf
  en C#. Apprenez à ajouter une numérotation Bates, du texte de pied de page, un filigrane
  personnalisé et à parcourir les pages du PDF dans un seul script.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: fr
og_description: Ajoutez des numéros de page PDF instantanément avec Aspose.Pdf. Ce
  guide couvre également l'ajout de numérotation Bates, de texte de pied de page,
  de filigrane personnalisé et le parcours des pages PDF.
og_title: Ajouter des numéros de page à un PDF avec C# – Tutoriel complet de programmation
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Ajouter des numéros de page à un PDF avec C# – Guide complet étape par étape
url: /fr/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des numéros de page PDF avec C# – Tutoriel complet de programmation

Vous avez déjà eu besoin d'**ajouter des numéros de page PDF** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul — les développeurs demandent constamment comment apposer des numéros, des pieds de page, ou même un identifiant de type Bates sur chaque page d’un PDF.  

Dans ce tutoriel, vous verrez un exemple C# prêt à l’emploi qui **parcourt les pages PDF**, appose un pied de page avec le numéro de page, et (si vous le souhaitez) ajoute un filigrane personnalisé. Nous vous montrerons également comment passer du tampon à un numéro Bates, ce qui n’est rien d’autre qu’une façon élégante de dire « ajouter une numérotation Bates » pour les documents juridiques ou médico-légaux. À la fin, vous disposerez d’une méthode unique et réutilisable qui gère toutes ces tâches sans effort.

## Ajouter des numéros de page PDF – Vue d’ensemble

Avant de plonger dans le code, clarifions ce que signifie réellement « add page numbers pdf » dans le monde d’Aspose.Pdf. La bibliothèque considère tout morceau de texte que vous placez sur une page comme un **TextStamp**. En créant un tampon avec un espace réservé de page (`{page}`) et en l’appliquant à chaque page, vous obtenez automatiquement une numérotation séquentielle. Le même tampon peut contenir du texte supplémentaire, vous permettant ainsi d'**ajouter du texte de pied de page** comme « Confidential » ou un identifiant propre à un dossier.

> **Pourquoi utiliser un tampon plutôt que de modifier le flux de contenu du PDF ?**  
> Les tampons sont des objets de haut niveau qui respectent les marges, la rotation et les graphiques existants. Ils sont également beaucoup plus faciles à maintenir — il suffit de changer quelques propriétés et de relancer le script.

## Parcourir les pages PDF pour appliquer les tampons

La première étape pratique consiste à ouvrir le PDF source et à itérer sur ses pages. C’est le modèle classique **loop through pdf pages** que la plupart des exemples Aspose utilisent.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Astuce :** Si votre PDF est volumineux (des centaines de pages), envisagez de le traiter par lots afin de limiter la consommation de mémoire. Aspose.Pdf charge les pages de façon paresseuse, donc la boucle est déjà assez efficace.

## Ajouter une numérotation Bates et du texte de pied de page

Maintenant que nous pouvons parcourir chaque page, créons un **TextStamp réutilisable** qui porte à la fois le numéro de page et le texte de pied de page optionnel. L’espace réservé `{page}` est remplacé automatiquement par l’indice de la page courante.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Pourquoi cela fonctionne

* **`Bates-{page}`** – Aspose remplace `{page}` par le numéro réel de la page, vous donnant ainsi automatiquement un numéro Bates classique.
* **`Confidential`** – C’est la partie **add footer text**. Vous pouvez la remplacer par n’importe quelle chaîne, voire récupérer des données depuis une base de données.
* **Style** – L’utilisation de `TextState` vous permet d’ajuster la couleur, l’opacité et même la rotation sans toucher aux flux de contenu internes du PDF.

Si vous avez seulement besoin de numéros simples, supprimez le préfixe « Bates‑ » et le texte supplémentaire :

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Ajouter un filigrane personnalisé (optionnel)

Parfois, vous voulez plus qu’un simple pied de page — vous avez besoin d’un logo semi‑transparent ou d’une superposition « DRAFT » sur toute la page. C’est là qu’intervient **add custom watermark**. La même classe `TextStamp` peut être réutilisée, il suffit de changer son alignement et son opacité.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Remarque :** L’ordre compte. Ajouter le filigrane en premier garantit que les numéros de page restent lisibles au-dessus du texte semi‑transparent.

## Enregistrer le PDF et vérifier le résultat

Après le tamponnage, l’étape finale consiste à écrire les modifications sur le disque. L’appel `Save` que nous avons placé plus tôt effectue le travail lourd, mais ajoutons un petit extrait de vérification qui ouvre le nouveau fichier et indique le nombre de pages traitées.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Lorsque vous exécuterez le programme complet, vous devriez obtenir un PDF où chaque page se termine par quelque chose comme **« Bates‑3 – Confidential »** (ou simplement « 3 » si vous avez utilisé le tampon simple) et, si vous avez activé le filigrane, un léger « DRAFT » au centre.

### Résultat attendu

| Page | Pied de page (exemple) |
|------|------------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

Si vous ouvrez le fichier dans un visualiseur, les numéros seront placés à 20 pts du bord gauche et du bas, conformément aux conventions habituelles des documents juridiques.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Enregistrez ceci sous le nom `AddPageNumbers.cs`, restaurez le package NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`), puis exécutez-le. Vous obtiendrez un fichier **add page numbers pdf** qui montre également **add bates numbering**, **add footer text**, **add custom watermark**, et le modèle classique **loop through pdf pages**—le tout dans un script propre.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **add page numbers pdf** avec Aspose.Pdf en C#. Du parcours de chaque page, à l’apposition de numéros Bates, en passant par l’ajout de texte de pied de page personnalisé et même le superposition d’un filigrane semi‑transparent, le code est suffisamment compact pour être intégré dans n’importe quel projet existant.  

Ensuite, vous pourriez explorer des scénarios plus avancés — par exemple récupérer le texte du pied de page depuis une base de données, appliquer des polices différentes selon les sections, ou générer un PDF d’index séparé listant tous les numéros Bates. Toutes ces extensions reposent sur les mêmes concepts de base que nous avons présentés, vous plaçant ainsi dans une position idéale pour faire évoluer la solution selon vos besoins croissants.  

Essayez, ajustez le style, et dites‑nous dans les commentaires comment cela a fonctionné pour vous. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}