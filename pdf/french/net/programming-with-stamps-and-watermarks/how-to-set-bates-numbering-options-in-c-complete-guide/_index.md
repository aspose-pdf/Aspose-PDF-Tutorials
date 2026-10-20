---
category: general
date: 2026-08-14
description: Comment définir les options de numérotation Bates en C# avec GroupDocs.
  Suivez ce tutoriel étape par étape pour ajouter des préfixes personnalisés et des
  numéros de départ lors de la conversion de Word en PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: fr
lastmod: 2026-08-14
og_description: Comment configurer rapidement les options de numérotation Bates en
  C#. Ce guide vous montre comment ajouter des préfixes personnalisés et des numéros
  de départ lors de la conversion de Word en PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Comment configurer les options de numérotation Bates en C# – tutoriel étape
  par étape
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Comment configurer les options de numérotation Bates en C# – guide complet
url: /fr/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir les options de numérotation Bates en C# – guide complet

Si vous avez besoin de **how to set bates numbering options** en C#, ce guide vous accompagne pas à pas. Vous apprendrez à configurer le numéro de départ, ajouter un préfixe et appliquer la numérotation lors de la conversion d’un document Word en PDF à l’aide de l’API GroupDocs.

Le traitement de documents nécessite souvent des identifiants uniques sur chaque page à des fins juridiques ou d’archivage. À la fin de ce tutoriel, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet .NET, que vous développiez un outil d’assistance juridique ou un générateur de rapports automatisé. Aucun outil externe n’est requis — seulement la bibliothèque GroupDocs.Conversion et quelques lignes de C#.

## Ce dont vous avez besoin

* .NET 6.0 SDK ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE supportant .NET)  
* Une licence valide GroupDocs.Conversion (l’essai gratuit fonctionne pour les tests)  
* Un document Word d’exemple (`input.docx`) que vous souhaitez numéroter  

Ces prérequis garantissent que le code s’exécute sans configuration supplémentaire.

## Comment définir les options de numérotation Bates – aperçu

Le cœur de **how to set bates numbering options** repose sur trois objets :

1. `Document` – charge le fichier source.  
2. `BatesNumberingOptions` – contient le numéro de départ, le préfixe et d’autres détails de formatage.  
3. `AddBatesNumbering` – la méthode qui injecte la numérotation dans chaque page.  

Comprendre pourquoi chaque élément existe vous aide à adapter la solution à des scénarios plus complexes, comme des polices personnalisées ou une numérotation multilingue.

## Étape 1 : Installer le package NuGet GroupDocs.Conversion

Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet add package GroupDocs.Conversion
```

L’**API GroupDocs** fournit la classe `Document` et la méthode d’extension `AddBatesNumbering` utilisée plus tard dans le tutoriel.

## Étape 2 : Charger le document source

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Pourquoi cette étape ?*  
Le chargement du fichier crée une représentation en mémoire que le moteur de conversion peut manipuler. Sans instance de `Document`, vous ne pouvez pas appliquer la numérotation Bates ni aucune autre transformation.

## Étape 3 : Créer les options de numérotation Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Pourquoi cette étape ?*  
`BatesNumberingOptions` encapsule tous les paramètres dont vous pourriez avoir besoin lors de **setting bates numbering options**. Ajuster `StartNumber` et `Prefix` vous permet d’aligner la sortie avec votre système de gestion de dossiers. La propriété `Position` contrôle le placement visuel, ce qui est souvent une exigence de conformité.

## Étape 4 : Appliquer la numérotation Bates au document

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

La méthode `AddBatesNumbering` parcourt chaque page du `Document` chargé et insère la chaîne configurée. Comme la méthode agit sur la représentation en mémoire, vous pouvez chaîner des étapes de traitement supplémentaires (par ex., filigrane) avant l’enregistrement.

## Étape 5 : Convertir et enregistrer le résultat au format PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Pourquoi cette étape ?*  
Enregistrer en PDF est un format final courant pour les documents juridiques. L’objet `PdfConvertOptions` vous permet d’ajuster finement la sortie, mais il n’est pas requis pour une numérotation de base. L’appel `Save` écrit le PDF entièrement numéroté sur le disque.

## Exemple complet et exécutable

En rassemblant tous les éléments, voici une application console autonome que vous pouvez compiler et exécuter :

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Sortie attendue**

L’exécution du programme crée `output.pdf` où chaque page affiche une étiquette telle que `CASE-1000`, `CASE-1001`, etc., positionnée dans le pied de page droit. Ouvrez le PDF dans n’importe quel lecteur pour vérifier que les numéros apparaissent comme prévu.

## Pièges courants et bonnes pratiques

| Problème | Pourquoi cela se produit | Comment l’éviter |
|----------|--------------------------|------------------|
| **Les chemins relatifs provoquent `FileNotFoundException`** | Le répertoire de travail d’une application console peut différer de celui de Visual Studio. | Utilisez des chemins absolus ou `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **La numérotation chevauche les pieds de page existants** | Si le document source contient déjà du contenu dans la zone de pied de page choisie, le nouveau numéro peut être masqué. | Choisissez une autre `Position` (par ex., `HeaderLeft`) ou ajustez le modèle source. |
| **Les gros documents sont lents** | La numérotation Bates parcourt chaque page ; l’utilisation de la mémoire augmente avec la taille du fichier. | Traitez le document par morceaux en utilisant `Document.Split` si vous dépassez 500 pages. |
| **Expiration de la licence** | L’essai gratuit de GroupDocs expire après 30 jours, provoquant une exception sur `AddBatesNumbering`. | Appliquez une clé de licence valide avant de charger le document : `License license = new License(); license.SetLicense("license.lic");`. |

**Astuce :** Si vous avez besoin d’un format de numéro différent par dossier (par ex., `2023-CASE-001`), construisez le préfixe dynamiquement avant de créer `BatesNumberingOptions`.

## Étendre la solution

La même approche **Bates numbering C#** fonctionne avec d’autres formats source tels que `.txt`, `.html` ou même des images. Il suffit de changer l’extension du fichier lors de la construction de l’objet `Document`, et le moteur de conversion se chargera du reste.

Vous pouvez également combiner **document conversion C#** avec l’OCR pour les PDF numérisés :

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Conclusion

Vous savez maintenant **how to set bates numbering options** en C# du début à la fin. En créant un objet `BatesNumberingOptions`, en l’appliquant avec `AddBatesNumbering` et en enregistrant le résultat au format PDF, vous pouvez automatiser la production de documents légalement conformes et identifiés de façon unique.

À partir de là, vous pouvez explorer des sujets connexes tels que **C# PDF generation**, **document conversion C#**, ou les fonctionnalités avancées de l’**API GroupDocs** comme le filigrane et les signatures numériques. Expérimentez différents préfixes, positions et formats de numéros pour adapter à votre flux de travail.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Ajouter la numérotation Bates PDF en C# – Guide complet](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Comment ajouter et personnaliser les numéros de page dans les PDF avec Aspose.PDF pour .NET | Guide de manipulation de documents](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Comment ajouter un pied de page de tampon texte dans les PDF avec Aspose.PDF pour .NET&#58; Guide étape par étape](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}