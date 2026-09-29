---
title: Ajouter un lien externe balisé avec infobulle au PDF à l'aide d'Aspose.Pdf pour .NET
weight: 440
limit:
description: Apprenez à ajouter un lien hypertexte externe balisé avec texte d'affichage et infobulle à un PDF à l'aide d'Aspose.Pdf pour .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Apprenez à ajouter un lien hypertexte externe balisé avec texte d'affichage
    et infobulle à un PDF à l'aide d'Aspose.Pdf pour .NET.
  headline: Ajouter un lien externe balisé avec infobulle au PDF à l'aide d'Aspose.Pdf
    pour .NET
  type: TechArticle
- description: Apprenez à ajouter un lien hypertexte externe balisé avec texte d'affichage
    et infobulle à un PDF à l'aide d'Aspose.Pdf pour .NET.
  name: Ajouter un lien externe balisé avec infobulle au PDF à l'aide d'Aspose.Pdf
    pour .NET
  steps:
  - name: Définissez les chemins du PDF source et du fichier résultat.
    text: Définissez les chemins du PDF source et du fichier résultat.
  - name: Vérifiez que le PDF source existe et interrompez l'opération s'il est introuvable.
    text: Vérifiez que le PDF source existe et interrompez l'opération s'il est introuvable.
  - name: Ouvrez le document PDF dans un bloc using afin d'assurer une libération
      correcte des ressources.
    text: Ouvrez le document PDF dans un bloc using afin d'assurer une libération
      correcte des ressources.
  - name: Obtenez le gestionnaire de contenu balisé (tagged‑content) pour le document
      ouvert.
    text: Obtenez le gestionnaire de contenu balisé (tagged‑content) pour le document
      ouvert.
  - name: Définissez la langue du document sur English (US) et attribuez au PDF un
      titre dérivé du nom de fichier.
    text: Définissez la langue du document sur English (US) et attribuez au PDF un
      titre dérivé du nom de fichier.
  - name: Récupérez l'élément racine de l'arbre de structure logique auquel les nouveaux
      éléments seront ajoutés.
    text: Récupérez l'élément racine de l'arbre de structure logique auquel les nouveaux
      éléments seront ajoutés.
  - name: Créez un élément de lien, définissez son texte affiché, son URL cible et
      le titre de l'infobulle, puis insérez-le dans la structure du document.
    text: Créez un élément de lien, définissez son texte affiché, son URL cible et
      le titre de l'infobulle, puis insérez-le dans la structure du document.
  - name: Enregistrez le PDF mis à jour dans le fichier résultat spécifié.
    text: Enregistrez le PDF mis à jour dans le fichier résultat spécifié.
  - name: Affichez un message de confirmation indiquant où le PDF modifié a été enregistré.
    text: Affichez un message de confirmation indiquant où le PDF modifié a été enregistré.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` renvoie le contenu balisé existant si le document
      est déjà balisé ; il ne crée pas d''arbre dupliqué.'
    question: Et si le PDF source est déjà balisé – l'appel à `pdfDoc.TaggedContent`
      créera-t-il un nouvel arbre de balises ou réutilisera-t-il celui existant ?
  - answer: Oui – localisez le `StructureElement` souhaité (par ex., un `Div` ou un
      `Paragraph` sur une page) via l'arbre de structure logique et appelez `AppendChild(externalLink)`
      sur cet élément.
    question: Puis-je placer le lien hypertexte sur une page spécifique au lieu de
      l'ajouter à l'élément racine ?
  - answer: L'infobulle s'affiche uniquement si `externalLink.Title` est définie avant
      `pdfDoc.Save` ; la définir après l'enregistrement n'a aucun effet sur le PDF
      déjà écrit.
    question: La propriété `Title` de `LinkElement` est-elle nécessaire pour que l'infobulle
      apparaisse, et peut‑elle être définie après l'appel à `Save` ?
  - answer: Attribuez un `FileSpecification` (par ex., `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      à `externalLink.Hyperlink` au lieu d'utiliser `WebHyperlink`.
    question: Comment créer un lien vers un fichier local au lieu d'une URL web ?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Insérer un lien externe balisé avec infobulle dans un PDF
og_description: Intégrez un lien hypertexte accessible avec texte visible et infobulle dans votre PDF en utilisant Aspose.Pdf pour .NET.
og_image_alt: Guide montrant comment ajouter un lien hypertexte externe balisé avec infobulle à un PDF en utilisant Aspose.Pdf pour .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un lien externe balisé avec infobulle au PDF à l'aide d'Aspose.Pdf pour .NET
Ce tutoriel montre comment ouvrir un PDF existant avec Aspose.Pdf pour .NET, créer un lien hypertexte externe balisé incluant du texte d'affichage visible et un titre d'infobulle, insérer le lien dans la structure logique du document et enregistrer le fichier mis à jour. En suivant les étapes, vous obtiendrez un PDF accessible où le lien fait partie de la hiérarchie des balises et fournit un contexte supplémentaire aux lecteurs.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Et si le PDF source est déjà balisé – l'appel à `pdfDoc.TaggedContent` créera-t-il un nouvel arbre de balises ou réutilisera-t-il celui existant ?**  
A: `pdfDoc.TaggedContent` renvoie le contenu balisé existant si le document est déjà balisé ; il ne crée pas d'arbre dupliqué.

**Q: Puis-je placer le lien hypertexte sur une page spécifique au lieu de l'ajouter à l'élément racine ?**  
A: Oui – localisez le `StructureElement` souhaité (par ex., un `Div` ou un `Paragraph` sur une page) via l'arbre de structure logique et appelez `AppendChild(externalLink)` sur cet élément.

**Q: La propriété `Title` de `LinkElement` est-elle nécessaire pour que l'infobulle apparaisse, et peut‑elle être définie après l'appel à `Save` ?**  
A: L'infobulle s'affiche uniquement si `externalLink.Title` est définie avant `pdfDoc.Save` ; la définir après l'enregistrement n'a aucun effet sur le PDF déjà écrit.

**Q: Comment créer un lien vers un fichier local au lieu d'une URL web ?**  
A: Attribuez un `FileSpecification` (par ex., `new FileSpecification("file:///C:/Docs/manual.pdf")`) à `externalLink.Hyperlink` au lieu d'utiliser `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}