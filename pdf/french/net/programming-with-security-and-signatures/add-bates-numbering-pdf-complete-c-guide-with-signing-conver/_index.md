---
category: general
date: 2026-06-21
description: Ajoutez la numérotation Bates aux PDF et apprenez comment ajouter des
  numéros Bates, convertir un PDF en PDF/X‑4, convertir un PDF en PDF/A‑4, et signer
  numériquement un PDF en C# dans un seul guide.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: fr
og_description: Ajouter une numérotation Bates au PDF, voir comment ajouter des numéros
  Bates, convertir le PDF en PDF/X‑4, convertir le PDF en PDF/A‑4, et signer numériquement
  un PDF en C# avec Aspose.Pdf.
og_title: Ajouter la numérotation Bates à un PDF – Tutoriel C# étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Ajouter une numérotation Bates à un PDF – Guide complet C# avec signature et
  conversion
url: /fr/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates à un PDF – Guide complet C# avec signature et conversion

Vous vous êtes déjà demandé **add bates numbering pdf** sans perdre patience ? Vous n'êtes pas seul. Les équipes juridiques, les auditeurs et toute personne ayant besoin de documents traçables demandent constamment *comment ajouter des numéros Bates* à un PDF, puis ils ont aussi besoin que le fichier respecte les normes PDF/X‑4 ou PDF/A‑4 et soit signé numériquement.  

Dans ce tutoriel, nous allons passer en revue exactement cela — en utilisant Aspose.Pdf pour .NET, nous **add bates numbering pdf**, montrons **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, et enfin **digitally sign pdf c#**. À la fin, vous disposerez d’un programme prêt à l’emploi qui produit trois PDF soignés : une version PDF/X‑4, une version numérotée Bates, et une version signée numériquement.

![add bates numbering pdf example](image-placeholder.png "Capture d’écran montrant add bates numbering pdf en action")

## Ce dont vous avez besoin

- **.NET 6+** (ou .NET Framework 4.6+). Aspose.Pdf prend en charge les deux.
- Une **licence valide Aspose.Pdf for .NET** (ou vous pouvez travailler avec l’évaluation, mais des filigranes apparaîtront).
- Un **fichier de certificat PKCS#7** (`.pfx`) et son mot de passe pour la signature.
- Le **PDF d’exemple** que vous souhaitez transformer (placez‑le dans un dossier que vous contrôlez).
- Visual Studio, Rider ou tout IDE C# de votre choix.

C’est tout — pas de packages NuGet supplémentaires au‑delà de `Aspose.Pdf`. Si vous n’avez pas encore ajouté la bibliothèque, exécutez :

```bash
dotnet add package Aspose.Pdf
```

Passons maintenant au code.

## Étape 1 : Charger le document PDF source

Tout d’abord, nous devons charger le fichier original en mémoire. C’est la base de toutes les opérations suivantes.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Pourquoi c’est important :** Charger le PDF crée un objet `Document` qui représente le fichier complet, nous donnant accès aux API de conversion, de champs de formulaire et de sécurité.

## Étape 2 : Convertir le PDF en PDF/X‑4 (conformité PDF/A‑4)

Si votre flux de travail exige une qualité d’archivage, PDF/X‑4 (un sous‑ensemble de PDF/A‑4) est la solution. Voici comment **convert pdf to pdf/x-4** avec Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Astuce :** Le drapeau `ConvertErrorAction.Delete` supprime tout contenu qui pourrait rompre la conformité, garantissant une sortie PDF/X‑4 propre.

## Étape 3 : Enregistrer la version PDF/X‑4

Maintenant que le document est conforme à PDF/X‑4, nous l’enregistrons sur le disque.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Vous avez maintenant un fichier compatible **convert pdf to pdfa-4** (PDF/X‑4 fait partie de la famille PDF/A‑4). N’hésitez pas à l’ouvrir dans Acrobat pour vérifier le badge de conformité.

## Étape 4 : Ajouter la numérotation Bates – Le cœur du « Add Bates Numbering PDF »

La numérotation Bates est un identifiant séquentiel placé sur chaque page. C’est la réponse exacte à *how to add bates numbers* de façon programmatique.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Pourquoi cela fonctionne :** `AddBatesNumbering` parcourt chaque page et appose le numéro à l’emplacement par défaut (en bas à droite). Vous pourrez ajuster la position via `BatesNumberingOptions` si besoin.

## Étape 5 : Enregistrer le PDF numéroté Bates

Après avoir **add bates numbering pdf**, nous devons créer un fichier séparé qui conserve les numéros.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Ouvrez le fichier ; vous devriez voir « CASE‑5000 », « CASE‑5001 », etc. en bas de chaque page.

## Étape 6 : Signer numériquement le PDF – « Digitally Sign PDF C# » en action

Une signature numérique garantit l’authenticité et l’intégrité. Ci‑dessous, nous allons **digitally sign pdf c#** en utilisant un hachage SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip :** Le `Rectangle` définit où apparaît la signature visible. Si vous n’avez pas besoin d’un indice visuel, définissez `signatureAppearance` à `false`.

## Étape 7 : Enregistrer le PDF signé numériquement

Enfin, écrivez le document signé sur le disque.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Vous avez maintenant un fichier **digitally sign pdf c#** qui peut être validé dans n’importe quel lecteur PDF supportant les signatures numériques.

## Code source complet – Solution tout‑en‑un

Voici le programme complet, prêt à être exécuté. Copiez‑collez, ajustez les chemins, puis appuyez sur **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Résultat attendu

| Fichier | Objectif | Fonctionnalité clé |
|------|---------|-------------|
| `sample_pdfx4.pdf` | Version PDF/X‑4 | Conforme à la conformité PDF/A‑4 |
| `sample_bates.pdf` | PDF numéroté Bates | **add bates numbering pdf** appliqué |
| `sample_signed.pdf` | PDF signé numériquement | **digitally sign pdf c#** avec SHA‑384 |

Ouvrez l’un des trois fichiers dans Adobe Acrobat Reader ; vous verrez les numéros Bates sur le deuxième fichier et un champ de signature sur le troisième.

## Questions fréquentes (FAQ)

**Q : Puis‑je modifier la position des numéros Bates ?**  
R : Oui. Utilisez les propriétés de `BatesNumberingOptions` telles que `Location` et `FontSize` pour affiner le placement.

**Q : Et si j’ai besoin de PDF/A‑4 au lieu de PDF/X‑4 ?**  
R : Remplacez `PdfFormat.PDF_X_4` par `PdfFormat.PDFA_4` dans les options de conversion. Cela satisfait l’exigence **convert pdf to pdfa-4**.

**Q : Mon certificat utilise un algorithme de hachage différent—puis‑je utiliser SHA‑256 ?**  
R : Absolument. Remplacez `DigestHashAlgorithm.Sha384` par `DigestHashAlgorithm.Sha256` (ou tout autre algorithme supporté).

**Q : Dois‑je appeler `document.Save` après chaque étape ?**  
R : Ce n’est pas obligatoire. Dans ce flux, nous enregistrons après la conversion et après la numérotation Bates pour vous fournir des fichiers intermédiaires. Vous pourriez différer l’enregistrement jusqu’à la fin si vous préférez une seule opération d’écriture.

## Conclusion

Nous venons de démontrer une solution pratique, de bout en bout qui **add bates numbering pdf**, explique **how to add bates numbers**, montre **convert pdf to pdf/x-4**, couvre


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}