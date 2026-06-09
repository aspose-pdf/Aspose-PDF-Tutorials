---
category: general
date: 2026-06-08
description: Recadrer une image dans un PDF avec Aspose.PDF en C#. Apprenez à créer
  un PDF avec une image, à enregistrer un PDF avec une image et à ajouter une image
  à un PDF en quelques lignes seulement.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: fr
og_description: Recadrer une image dans un PDF avec Aspose.PDF en C#. Ce tutoriel
  montre comment créer un PDF avec une image, enregistrer un PDF avec une image et
  ajouter rapidement une image à un PDF.
og_title: Recadrer une image dans un PDF avec Aspose.PDF – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Recadrer une image dans un PDF avec Aspose.PDF – Guide complet
url: /fr/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recadrer une image dans un PDF avec Aspose.PDF – Guide complet

Vous vous êtes déjà demandé comment **crop image in PDF** sans sortir un éditeur graphique ? Vous n'êtes pas le seul. Dans de nombreux rapports, factures ou e‑books, vous avez besoin d'une simple tranche d'une image—peut‑être le coin du logo ou un fragment de graphique—et vous voulez l'insérer directement dans le PDF.  

Ce guide vous montre exactement cela : nous allons **create PDF with image**, **add image to PDF**, puis **crop image in PDF** en utilisant la bibliothèque Aspose.PDF pour C#. À la fin, vous saurez également comment **save PDF with image** afin de pouvoir envoyer le fichier à quiconque.

---

## Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.6+)  
- Une copie sous licence ou d'essai de **Aspose.PDF for .NET** (installez via NuGet `Install-Package Aspose.PDF`)  
- Un fichier image (JPEG/PNG) sur le disque – nous l’appellerons `image.jpg`  
- Tout IDE de votre choix (Visual Studio, Rider, VS Code)

C’est tout. Aucun service supplémentaire, aucun outil externe.

---

## Étape 1 : Configurer le projet et les imports

Tout d'abord, créez une application console et importez les espaces de noms dont nous aurons besoin. Les instructions `using` maintiennent le code propre et facilitent la lecture des étapes suivantes.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Astuce :** Si vous utilisez Visual Studio, faites un clic droit sur le projet → *Manage NuGet Packages* → recherchez “Aspose.PDF” et installez-le. La bibliothèque gère à la fois le placement et le recadrage d'image en interne, vous n’aurez donc besoin d’aucune bibliothèque d’image tierce.

---

## Étape 2 : Créer un PDF avec une image

Nous allons maintenant réellement **create pdf with image**. L’extrait ci‑dessous crée un nouveau `Document`, ajoute une page vierge et prépare un flux d’image.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

L’exécution de ce code vous donnera un PDF contenant l’image entière étirée aux dimensions que vous avez spécifiées. C’est un bon test de validité avant de commencer le recadrage.

---

## Étape 3 : Comment ajouter une image à un PDF (et préparer le recadrage)

Si vous connaissez déjà la région exacte que vous souhaitez, vous pouvez ignorer l’étape de taille complète et passer directement à la partie **how to add image to pdf**. La méthode `AddImage` accepte trois paramètres :

1. **Image stream** – les octets bruts de votre image.  
2. **Placement rectangle** – l’endroit sur la page où l’image se trouve.  
3. **Crop rectangle** – la partie de l’image que vous souhaitez réellement rendre.

Voici la version compacte qui effectue à la fois le placement **et** le recadrage en un seul appel.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Pourquoi cela fonctionne :** Aspose.PDF mappe en interne le rectangle de recadrage aux dimensions en pixels de l’image, puis ne rend que cette tranche à l’intérieur de la zone `placement`. Aucun traitement bitmap supplémentaire n’est nécessaire, ce qui permet de garder la taille du PDF réduite.

---

## Étape 4 : Comment recadrer une image PDF – Options avancées

Parfois, le recadrage d’un quart n’est pas suffisant. Vous avez peut‑être besoin d’un rectangle personnalisé ou de préserver le ratio d’aspect de l’image. Voici une approche plus flexible :

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Gestion des cas limites :**  
- **Null streams** – enveloppez toujours le `FileStream` dans un bloc `using`, comme indiqué, pour éviter les fuites.  
- **Large images** – si l’image source est très grande, envisagez de réduire le rectangle `placement` ; Aspose effectuera automatiquement un sous‑échantillonnage.  
- **Transparent PNGs** – la bibliothèque respecte les canaux alpha, ainsi votre zone recadrée conservera la transparence.

---

## Étape 5 : Enregistrer le PDF avec l’image (et vérifier)

Enfin, nous **save pdf with image**. La méthode `Save` écrit le document sur le disque. Vous pouvez également le renvoyer sous forme de flux à un client web si vous créez une API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Lorsque vous ouvrez `output.pdf`, vous ne devriez voir que la partie recadrée de `image.jpg` positionnée exactement où vous l’avez définie. Si l’image semble étirée, ajustez la largeur/hauteur du rectangle `placement` pour correspondre au ratio d’aspect du rectangle de recadrage.

---

## Questions fréquentes & pièges

| Question | Answer |
|----------|--------|
| **Can I crop multiple images on the same page?** | Absolument. Appelez `page.AddImage` pour chaque image avec ses propres rectangles de placement et de recadrage. |
| **What if my image is in a different format (e.g., BMP)?** | Aspose.PDF prend en charge JPEG, PNG, BMP, GIF et TIFF nativement. Changez simplement l’extension du fichier. |
| **Do I need a license for production use?** | Une version d’essai fonctionne jusqu’à 5 pages. Pour les déploiements réels, achetez une licence pour supprimer le filigrane. |
| **How do I rotate the cropped image?** | Après avoir ajouté l’image, récupérez l’objet `Image` et définissez sa propriété `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **Is there a way to crop using percentages instead of absolute points?** | Oui—calculez les dimensions du rectangle en fonction de `image.Width * 0.25`, etc., puis convertissez en points comme montré à l’étape 4. |

---

## Exemple complet (prêt à copier‑coller)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Exécutez le programme, ouvrez `output.pdf`, et vous verrez uniquement le quart supérieur‑gauche de `image.jpg` rendu dans le coin supérieur‑gauche de la page. Modifiez les valeurs du rectangle `crop` pour expérimenter différentes découpes.

---

## Conclusion

Nous avons parcouru l’ensemble du processus de **crop image in pdf** avec Aspose.PDF pour C#. En partant d’un document vierge, nous **create pdf with image**, montrons le **how to add image to pdf**, appliquons un rectangle personnalisé **how to crop image pdf**, et enfin **save pdf with image**.  

Vous pouvez maintenant intégrer des images précisément recadrées dans n’importe quel PDF que vous générez—parfait pour les factures, les brochures marketing ou les rapports automatisés. Ensuite, pensez à ajouter des légendes texte (`TextFragment`) ou à dessiner des formes autour de l’image recadrée pour la mettre davantage en valeur.  

Vous avez d’autres scénarios en tête ? Laissez un commentaire, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment définir la taille d’une image dans un PDF avec Aspose.PDF pour .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Comment ajouter un tampon d’image à un PDF avec Aspose.PDF pour .NET : guide complet](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Comment extraire les informations d’image des PDF avec Aspose.PDF pour .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}