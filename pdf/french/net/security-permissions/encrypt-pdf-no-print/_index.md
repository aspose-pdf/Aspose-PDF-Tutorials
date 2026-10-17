---
title: Chiffrer un PDF sans autorisation d’impression avec Aspose.PDF for .NET
weight: 101
limit:
description: Apprenez à chiffrer un PDF avec AES‑256 et à désactiver l’impression en utilisant Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à chiffrer un PDF avec AES‑256 et à désactiver l’impression
    en utilisant Aspose.PDF for .NET.
  headline: Chiffrer un PDF sans autorisation d’impression avec Aspose.PDF for .NET
  type: TechArticle
- description: Apprenez à chiffrer un PDF avec AES‑256 et à désactiver l’impression
    en utilisant Aspose.PDF for .NET.
  name: Chiffrer un PDF sans autorisation d’impression avec Aspose.PDF for .NET
  steps:
  - name: Définissez le chemin du PDF source, le nom du fichier protégé en sortie,
      ainsi que les mots de passe de visualisation et de propriétaire.
    text: Définissez le chemin du PDF source, le nom du fichier protégé en sortie,
      ainsi que les mots de passe de visualisation et de propriétaire.
  - name: Vérifiez que le fichier source existe et interrompez l’exécution avec un
      message d’erreur s’il est absent.
    text: Vérifiez que le fichier source existe et interrompez l’exécution avec un
      message d’erreur s’il est absent.
  - name: Ouvrez le PDF original, définissez aucune permission, chiffrez‑le avec AES‑256
      en utilisant les mots de passe spécifiés, puis enregistrez le fichier protégé.
    text: Ouvrez le PDF original, définissez aucune permission, chiffrez‑le avec AES‑256
      en utilisant les mots de passe spécifiés, puis enregistrez le fichier protégé.
  - name: Rouvrez le PDF chiffré avec le mot de passe de visualisation et écrivez
      son indicateur IsEncrypted dans la console pour confirmer la protection.
    text: Rouvrez le PDF chiffré avec le mot de passe de visualisation et écrivez
      son indicateur IsEncrypted dans la console pour confirmer la protection.
  - name: Affichez un message final indiquant que le chiffrement est terminé et le
      nom du fichier de sortie.
    text: Affichez un message final indiquant que le chiffrement est terminé et le
      nom du fichier de sortie.
  type: HowTo
- questions:
  - answer: '`Permissions` est une énumération à drapeaux ; affecter `0` signifie
      qu’aucun bit de permission n’est activé, ainsi Aspose.Pdf ne concède pas le
      droit PrintDocument et le visualiseur ne peut pas imprimer le PDF.'
    question: Pourquoi le fait de définir `Permissions rights = 0;` désactive-t-il
      l’impression ?
  - answer: Oui, remplacez `CryptoAlgorithm.AESx256` par `CryptoAlgorithm.AESx128`
      (ou une autre valeur d’énumération prise en charge) dans l’appel `pdfDoc.Encrypt ;`
      le reste du code reste inchangé.
    question: Puis‑je utiliser un autre algorithme de chiffrement, comme AES‑128,
      avec le même code ?
  - answer: Aspose.Pdf acceptera des mots de passe identiques, mais le mot de passe
      propriétaire ne conférera plus de privilèges supplémentaires ; le PDF restera
      chiffré et les permissions que vous avez spécifiées (aucune) s’appliqueront.
    question: Que se passe‑t‑il si le mot de passe de visualisation et le mot de passe
      maître (propriétaire) sont identiques ?
  - answer: Ouvrez le fichier protégé avec le mot de passe de visualisation (`new
      Document(securedFile, viewerPwd)`) et essayez d’imprimer depuis un visualiseur
      PDF ; comme aucune permission `PrintDocument` n’a été définie, le visualiseur
      refusera la commande d’impression.
    question: Comment puis‑je confirmer que l’impression est réellement bloquée après
      le chiffrement ?
  - answer: Le code vérifie `File.Exists(sourceFile)` et écrit une erreur dans `Console.Error`
      avant de retourner, ce qui empêche une `FileNotFoundException` d’être levée
      par le constructeur `Document`.
    question: Quelle erreur est levée si `original.pdf` n’existe pas, et comment dois‑je
      la gérer ?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Chiffrer le PDF et bloquer l’impression
og_description: Sécurisez votre PDF avec le chiffrement AES‑256 et assurez‑vous qu’il ne puisse pas être imprimé—guide étape par étape.
og_image_alt: Capture d’écran montrant le code Aspose.PDF for .NET qui chiffre un PDF et désactive l’impression.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chiffrer un PDF sans autorisation d’impression avec Aspose.PDF
Ce tutoriel montre comment ouvrir un PDF existant avec Aspose.PDF for .NET, appliquer le chiffrement AES‑256 tout en n’accordant aucune permission—désactivant ainsi l’impression—enregistrer le document sécurisé et confirmer la protection en l’ouvrant avec le mot de passe de visualisation. Suivez le code pas à pas pour vous assurer que votre PDF ne pourra pas être imprimé après le chiffrement.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Pourquoi le fait de définir `Permissions rights = 0;` désactive-t-il l’impression ?**  
A: `Permissions` est une énumération à drapeaux ; affecter `0` signifie qu’aucun bit de permission n’est activé, ainsi Aspose.Pdf ne concède pas le droit PrintDocument et le visualiseur ne peut pas imprimer le PDF.

**Q: Puis‑je utiliser un autre algorithme de chiffrement, comme AES‑128, avec le même code ?**  
A: Oui, remplacez `CryptoAlgorithm.AESx256` par `CryptoAlgorithm.AESx128` (ou une autre valeur d’énumération prise en charge) dans l’appel `pdfDoc.Encrypt ;` le reste du code reste inchangé.

**Q: Que se passe‑t‑il si le mot de passe de visualisation et le mot de passe maître (propriétaire) sont identiques ?**  
A: Aspose.Pdf acceptera des mots de passe identiques, mais le mot de passe propriétaire ne conférera plus de privilèges supplémentaires ; le PDF restera chiffré et les permissions que vous avez spécifiées (aucune) s’appliqueront.

**Q: Comment puis‑je confirmer que l’impression est réellement bloquée après le chiffrement ?**  
A: Ouvrez le fichier protégé avec le mot de passe de visualisation (`new Document(securedFile, viewerPwd)`) et essayez d’imprimer depuis un visualiseur PDF ; comme aucune permission `PrintDocument` n’a été définie, le visualiseur refusera la commande d’impression.

**Q: Quelle erreur est levée si `original.pdf` n’existe pas, et comment dois‑je la gérer ?**  
A: Le code vérifie `File.Exists(sourceFile)` et écrit une erreur dans `Console.Error` avant de retourner, ce qui empêche une `FileNotFoundException` d’être levée par le constructeur `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}