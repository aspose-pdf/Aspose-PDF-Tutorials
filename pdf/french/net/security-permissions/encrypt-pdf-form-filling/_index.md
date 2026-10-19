---
title: Chiffrer un PDF pour n'autoriser que le remplissage de formulaire avec Aspose.Pdf pour .NET
weight: 101
limit:
description: Apprenez à chiffrer un PDF avec AES‑256, à définir des mots de passe et à limiter les autorisations au seul remplissage de formulaire en utilisant Aspose.Pdf pour .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à chiffrer un PDF avec AES‑256, à définir des mots de passe
    et à limiter les autorisations au seul remplissage de formulaire en utilisant
    Aspose.Pdf pour .NET.
  headline: Chiffrer un PDF pour n'autoriser que le remplissage de formulaire avec
    Aspose.Pdf pour .NET
  type: TechArticle
- description: Apprenez à chiffrer un PDF avec AES‑256, à définir des mots de passe
    et à limiter les autorisations au seul remplissage de formulaire en utilisant
    Aspose.Pdf pour .NET.
  name: Chiffrer un PDF pour n'autoriser que le remplissage de formulaire avec Aspose.Pdf
    pour .NET
  steps:
  - name: Définissez les chemins d'accès du fichier source et du fichier de destination
      ainsi que les mots de passe visualiseur et propriétaire.
    text: Définissez les chemins d'accès du fichier source et du fichier de destination
      ainsi que les mots de passe visualiseur et propriétaire.
  - name: Vérifiez que le PDF source existe et arrêtez le processus avec un message
      d'erreur s'il n'existe pas.
    text: Vérifiez que le PDF source existe et arrêtez le processus avec un message
      d'erreur s'il n'existe pas.
  - name: Commencez un bloc try pour gérer les éventuelles erreurs pouvant survenir
      pendant le traitement.
    text: Commencez un bloc try pour gérer les éventuelles erreurs pouvant survenir
      pendant le traitement.
  - name: Ouvrez le fichier PDF existant en créant un objet Document nommé pdfDoc.
    text: Ouvrez le fichier PDF existant en créant un objet Document nommé pdfDoc.
  - name: Définissez les autorisations pour n'autoriser que le remplissage de formulaire,
      chiffrez le document avec les mots de passe visualiseur et propriétaire en utilisant
      AES‑256, puis enregistrez le PDF protégé.
    text: Définissez les autorisations pour n'autoriser que le remplissage de formulaire,
      chiffrez le document avec les mots de passe visualiseur et propriétaire en utilisant
      AES‑256, puis enregistrez le PDF protégé.
  - name: Écrivez un message de confirmation dans la console et fermez le bloc try.
    text: Écrivez un message de confirmation dans la console et fermez le bloc try.
  - name: Capturez les éventuelles exceptions et affichez le message d'erreur dans
      la console.
    text: Capturez les éventuelles exceptions et affichez le message d'erreur dans
      la console.
  type: HowTo
- questions:
  - answer: Lorsqu'il est ouvert avec le mot de passe visualiseur (utilisateur), le
      document peut être consulté et les champs de formulaire remplis, mais toutes
      les autres actions telles que la modification du texte, l'ajout d'annotations
      ou l'extraction de contenu sont bloquées.
    question: Que peut faire un utilisateur avec le PDF après qu'il a été chiffré
      avec `Permissions.FillForm` ?
  - answer: Combinez les autorisations en utilisant l'opérateur OU binaire, par exemple
      `Permissions allowed = Permissions.FillForm | Permissions.Printing;` et transmettez
      la valeur combinée à `pdfDoc.Encrypt`.
    question: Comment puis‑je autoriser des droits supplémentaires, comme l'impression,
      tout en continuant à restreindre tout le reste ?
  - answer: Oui. Le premier argument est le mot de passe utilisateur (visualiseur)
      qui accorde les droits limités, et le deuxième argument est le mot de passe
      propriétaire (admin) qui offre le contrôle total du document.
    question: L'ordre des mots de passe dans `pdfDoc.Encrypt(viewerPass, adminPass,
      …)` a‑t‑il de l'importance ?
  - answer: Aspose.Pdf lèvera une exception en essayant d'ouvrir un fichier déjà chiffré ;
      vous devez d'abord l'ouvrir avec son mot de passe existant, supprimer ou modifier
      la protection, puis appliquer les nouveaux paramètres de chiffrement.
    question: Que se passe-t-il si le PDF source est déjà protégé par un mot de passe ?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: Chiffrer le PDF et n'autoriser que le remplissage de formulaire
og_description: Sécurisez votre PDF avec AES‑256 et laissez les utilisateurs remplir les formulaires, mais rien d'autre.
og_image_alt: Capture d'écran montrant le code Aspose.Pdf pour .NET qui chiffre un PDF et le restreint au seul remplissage de formulaire
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chiffrer un PDF pour n'autoriser que le remplissage de formulaire avec Aspose.Pdf pour .NET
Dans ce tutoriel, vous apprendrez comment ouvrir un PDF existant avec Aspose.Pdf pour .NET, appliquer le chiffrement AES‑256, définir les mots de passe visualiseur et propriétaire, et restreindre les autorisations du document afin que les destinataires ne puissent remplir que les champs de formulaire. Cette approche est utile lorsque vous devez protéger le contenu tout en permettant aux utilisateurs de compléter des formulaires interactifs. Le code parcourt chaque étape et enregistre le PDF sécurisé, prêt à être distribué.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-form-filling" >}}


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

**Q: Que peut faire un utilisateur avec le PDF après qu'il a été chiffré avec `Permissions.FillForm` ?**  
A: Lorsqu'il est ouvert avec le mot de passe visualiseur (utilisateur), le document peut être consulté et les champs de formulaire remplis, mais toutes les autres actions telles que la modification du texte, l'ajout d'annotations ou l'extraction de contenu sont bloquées.

**Q: Comment puis‑je autoriser des droits supplémentaires, comme l'impression, tout en continuant à restreindre tout le reste ?**  
A: Combinez les autorisations en utilisant l'opérateur OU binaire, par exemple `Permissions allowed = Permissions.FillForm | Permissions.Printing;` et transmettez la valeur combinée à `pdfDoc.Encrypt`.

**Q: L'ordre des mots de passe dans `pdfDoc.Encrypt(viewerPass, adminPass, …)` a‑t‑il de l'importance ?**  
A: Oui. Le premier argument est le mot de passe utilisateur (visualiseur) qui accorde les droits limités, et le deuxième argument est le mot de passe propriétaire (admin) qui offre le contrôle total du document.

**Q: Que se passe-t-il si le PDF source est déjà protégé par un mot de passe ?**  
A: Aspose.Pdf lèvera une exception en essayant d'ouvrir un fichier déjà chiffré ; vous devez d'abord l'ouvrir avec son mot de passe existant, supprimer ou modifier la protection, puis appliquer les nouveaux paramètres de chiffrement.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}