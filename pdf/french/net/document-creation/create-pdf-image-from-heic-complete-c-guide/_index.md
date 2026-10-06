---
category: general
date: 2026-06-08
description: Créer une image PDF en C# en convertissant HEIC en PDF. Apprenez comment
  ajouter une image à un PDF et générer un PDF à partir d’une image avec un code étape
  par étape.
draft: false
keywords:
- create pdf image
- convert heic to pdf
- add image to pdf
- generate pdf from image
- how to read heic
language: fr
og_description: Créez une image PDF en C# en convertissant le HEIC en PDF. Suivez
  ce guide pour ajouter une image au PDF et générer rapidement un PDF à partir d’une
  image.
og_title: Créer une image PDF à partir de HEIC – Tutoriel complet C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  headline: Create PDF Image from HEIC – Complete C# Guide
  type: TechArticle
- description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  name: Create PDF Image from HEIC – Complete C# Guide
  steps:
  - name: What if the HEIC file is corrupted?
    text: The `HeicImage.Load` method throws a `HeicException`. Wrap the call in a
      try/catch (as shown) and log the error. In production you might fall back to
      a default placeholder image.
  - name: Can I batch‑process multiple HEIC files?
    text: Absolutely. Just move the core logic into a method like `ConvertHeicToPdf(string
      input, string output)` and iterate over a directory with `Directory.GetFiles("*.heic")`.
  - name: Does this approach preserve EXIF metadata?
    text: No, Aspose.Pdf does not automatically copy EXIF data into the PDF. If you
      need metadata, extract it with `HeicImage.Metadata` and add it to the PDF using
      `Document.Info` properties.
  - name: What about memory usage for huge images?
    text: For images larger than 10 MP, consider down‑sampling before creating `BitmapInfo`.
      You can use `HeicImage.Resize` (if supported) or a third‑party bitmap library
      to reduce dimensions.
  type: HowTo
tags:
- C#
- Aspose.Pdf
- HEIC
- ImageConversion
title: Créer une image PDF à partir de HEIC – Guide complet C#
url: /fr/net/document-creation/create-pdf-image-from-heic-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une image PDF à partir de HEIC – Guide complet C#

Vous êtes-vous déjà demandé comment **créer une image PDF** à partir d’un fichier HEIC sans perdre patience ? Vous n’êtes pas seul. Dans de nombreuses applications mobile‑first, l’appareil photo génère du HEIC, alors que les systèmes hérités ont encore besoin d’un bon vieux PDF. Ce tutoriel vous montre exactement comment **convertir HEIC en PDF**, ajouter l’image à une nouvelle page PDF, et enfin **générer un PDF à partir d’une image** avec Aspose.Pdf.

Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque élément est important, et vous fournirons un exemple prêt à l’emploi. À la fin, vous pourrez déposer un fichier HEIC dans un dossier et obtenir un PDF net—sans outils externes.

## Ce que vous allez apprendre

* Comment **lire des fichiers HEIC** en C# avec le décodeur `FileFormat.Heic`.
* Les étapes exactes pour **convertir HEIC en PDF** avec Aspose.Pdf.
* Les différentes manières **d’ajouter une image à un PDF** et de contrôler le format des pixels.
* Des astuces pour gérer les images volumineuses et éviter les pièges courants.
* Un programme complet, prêt à être compilé, que vous pouvez copier‑coller.

*Prérequis* : .NET 6+ (ou .NET Framework 4.6+), Aspose.Pdf pour .NET, et le package NuGet `FileFormat.Heic`. Si vous n’avez jamais utilisé ces bibliothèques, ne vous inquiétez pas — l’installation est couverte à la première étape.

---

## Étape 0 : Installer les packages requis

Avant de plonger dans le code, assurez‑vous que les deux bibliothèques sont référencées dans votre projet :

```powershell
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic
```

Les deux packages sont gratuits pour le développement et supportent .NET Standard, ils fonctionnent donc dans les applications console, ASP.NET ou même Unity.

---

## Étape 1 : Lire le HEIC – Charger le fichier en tant que flux

Lire un fichier HEIC est similaire à ouvrir n’importe quel fichier binaire, mais il faut un décodeur qui comprend le conteneur HEIC. La bibliothèque `FileFormat.Heic` nous fournit une méthode statique `Load`.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

// ...

// Open the HEIC file safely with a using block
using (FileStream heicStream = new FileStream(
           @"C:\Images\input.heic", FileMode.Open, FileAccess.Read))
{
    // Decode the HEIC image into a HeicImage object
    HeicImage heicImage = HeicImage.Load(heicStream);
```

**Pourquoi un flux ?**  
Un flux permet au décodeur de lire le fichier de façon paresseuse, ce qui réduit la pression mémoire pour les images très lourdes. L’instruction `using` garantit également que le handle du fichier est libéré, évitant ainsi les erreurs de verrouillage de fichier ultérieures.

---

## Étape 2 : Convertir HEIC en PDF – Extraire les données de pixels

Aspose.Pdf attend des données bitmap brutes, pas un objet HEIC. Nous extrayons donc les octets de pixels dans un format qu’il comprend — `Rgb24` convient à la plupart des cas d’utilisation.

```csharp
    // Grab the raw RGB24 pixel array from the HEIC image
    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

    // Capture image dimensions for later use
    int width  = (int)heicImage.Width;
    int height = (int)heicImage.Height;
```

**Note sur les cas limites** : Si votre HEIC source contient un canal alpha, `Rgb24` le supprimera. Pour la transparence, il faut passer à `Rgba32` et ajuster le `BitmapInfo` en conséquence.

---

## Étape 3 : Ajouter l’image au PDF – Construire l’objet Aspose Image

Nous encapsulons maintenant les octets bruts dans un `Aspose.Pdf.Image`. Le constructeur `BitmapInfo` indique à Aspose le stride, la taille et le format des pixels.

```csharp
    // Create an Aspose PDF Image using the pixel buffer
    Image pdfImage = new Image
    {
        BitmapInfo = new BitmapInfo(
            pixelData,
            width,
            height,
            BitmapInfo.PixelFormat.Rgb24)
    };
```

**Astuce pro** : Si vous prévoyez d’insérer plusieurs images dans le même document, réutilisez une seule instance `Document` et créez uniquement de nouveaux objets `Image` par page. Cela réduit le sur‑coût de création d’objets.

---

## Étape 4 : Générer le PDF à partir de l’image – Assembler le document

Avec l’image prête, nous créons un nouveau document PDF, ajoutons une page, puis déposons l’image dessus. La collection `Paragraphs` d’Aspose rend cela trivial.

```csharp
    // Initialize a new PDF document
    Document pdfDoc = new Document();

    // Add a blank page to the document
    Page page = pdfDoc.Pages.Add();

    // Insert the image into the page's paragraph collection
    page.Paragraphs.Add(pdfImage);
```

Si vous devez positionner l’image (centrer, mettre à l’échelle, etc.), vous pouvez l’envelopper dans un `ImageStamp` ou ajuster `pdfImage.Margin`. Pour la plupart des conversions un‑à‑un, le placement par défaut suffit.

---

## Étape 5 : Enregistrer le résultat – Écrire le PDF sur le disque

La dernière étape consiste simplement à persister le fichier PDF. Aspose supporte de nombreux formats ; ici nous restons sur le classique `.pdf`.

```csharp
    // Define the output path and save the PDF
    string outputPath = @"C:\Images\output.pdf";
    pdfDoc.Save(outputPath);
}
```

**Résultat attendu** : L’ouverture de `output.pdf` dans n’importe quel visualiseur affichera l’image HEIC originale rendue à sa résolution native. Aucun perte de qualité au‑delà de la compression HEIC d’origine.

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier dans une application console. Il inclut toutes les directives `using` et la gestion des erreurs pour un rendu prêt à la production.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

namespace HeicToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath  = @"C:\Images\input.heic";
            string outputPath = @"C:\Images\output.pdf";

            try
            {
                // 1️⃣ Open the HEIC file as a stream
                using (FileStream heicStream = new FileStream(
                           inputPath, FileMode.Open, FileAccess.Read))
                {
                    // 2️⃣ Load the HEIC image from the stream
                    HeicImage heicImage = HeicImage.Load(heicStream);

                    // 3️⃣ Extract pixel data in RGB24 format
                    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
                    int width  = (int)heicImage.Width;
                    int height = (int)heicImage.Height;

                    // 4️⃣ Create an Aspose.Pdf.Image using the pixel data
                    Image pdfImage = new Image
                    {
                        BitmapInfo = new BitmapInfo(
                            pixelData,
                            width,
                            height,
                            BitmapInfo.PixelFormat.Rgb24)
                    };

                    // 5️⃣ Add the image to a new PDF page
                    Document pdfDoc = new Document();
                    Page page = pdfDoc.Pages.Add();
                    page.Paragraphs.Add(pdfImage);

                    // 6️⃣ Save the resulting PDF
                    pdfDoc.Save(outputPath);
                }

                Console.WriteLine($"✅ Success! PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error: {ex.Message}");
            }
        }
    }
}
```

Exécutez le programme, et vous verrez le message console confirmant la création du PDF. Ouvrez le fichier, et l’image devrait être identique à celle du HEIC d’origine.

---

## Questions fréquentes & Pièges

### Que faire si le fichier HEIC est corrompu ?
La méthode `HeicImage.Load` lève une `HeicException`. Enveloppez l’appel dans un `try/catch` (comme montré) et consignez l’erreur. En production, vous pourriez revenir à une image de remplacement par défaut.

### Puis‑je traiter plusieurs fichiers HEIC en lot ?
Absolument. Déplacez simplement la logique principale dans une méthode comme `ConvertHeicToPdf(string input, string output)` et itérez sur un répertoire avec `Directory.GetFiles("*.heic")`.

### Cette approche conserve‑t‑elle les métadonnées EXIF ?
Non, Aspose.Pdf ne copie pas automatiquement les données EXIF dans le PDF. Si vous avez besoin de métadonnées, extrayez‑les avec `HeicImage.Metadata` et ajoutez‑les au PDF via les propriétés `Document.Info`.

### Qu’en est‑il de l’utilisation mémoire pour les très grandes images ?
Pour les images supérieures à 10 MP, envisagez un sous‑échantillonnage avant de créer le `BitmapInfo`. Vous pouvez utiliser `HeicImage.Resize` (si supporté) ou une bibliothèque bitmap tierce pour réduire les dimensions.

---

## Conclusion

Vous savez maintenant comment **créer une image PDF** à partir d’une source HEIC, **convertir HEIC en PDF**, et **ajouter une image à un PDF** en utilisant Aspose.Pdf en C#. Les étapes — lecture du HEIC, extraction des pixels, encapsulation dans une image PDF, puis sauvegarde—sont simples, tout en étant suffisamment puissantes pour des pipelines de production.

Ensuite, essayez d’étendre le script : générez un PDF multi‑pages où chaque page contient un HEIC différent, ou intégrez des calques OCR pour des PDF recherchables. Vous pouvez également explorer d’autres formats d’image (`jpeg`, `png`) avec le même schéma, consolidant ainsi la compétence **générer un PDF à partir d’une image**.

N’hésitez pas à expérimenter, partager vos découvertes ou poser des questions dans les commentaires. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Add an Image Header to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-header-pdf-aspose-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Add Image Stamp to PDF Footer Using Aspose.PDF .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-image-stamp-pdf-footer-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}