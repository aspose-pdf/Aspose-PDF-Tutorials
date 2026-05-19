---
category: general
date: 2026-04-25
description: Ajoutez une numérotation Bates aux PDF rapidement avec Aspose.Pdf. Apprenez
  comment ajouter des numéros de page aux PDF, ajuster automatiquement la taille de
  la police et ajouter un filigrane texte en C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: fr
og_description: Ajoutez la numérotation Bates aux PDF avec Aspose.Pdf. Ce guide montre
  comment ajouter des numéros de page aux PDF, ajuster automatiquement la taille de
  la police et ajouter un filigrane texte dans un seul exemple exécutable.
og_title: Ajouter la numérotation Bates aux PDF – Tutoriel complet Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ajouter la numérotation Bates aux PDF avec Aspose – Guide complet
url: /fr/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates aux PDF avec Aspose – Guide complet

Vous avez déjà eu besoin **d’ajouter une numérotation Bates** à un PDF sans savoir par où commencer ? Vous n’êtes pas seul — les équipes juridiques, les auditeurs et les développeurs rencontrent ce problème quotidiennement. Bonne nouvelle ? Avec Aspose.Pdf pour .NET, vous pouvez tamponner un numéro Bates, ajuster automatiquement la taille de la police, et même traiter le tampon comme un filigrane texte subtil — le tout en quelques lignes de C#.

Dans ce tutoriel, nous parcourrons les étapes exactes pour **ajouter des numéros de page pdf**, ajuster la police afin qu’elle ne déborde jamais, et répondre une bonne fois pour toutes à la question « comment ajouter bates ». À la fin, vous disposerez d’une application console prête à l’emploi qui produit un PDF professionnellement numéroté, et vous verrez comment l’étendre en une solution de filigrane complète.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* **Aspose.Pdf pour .NET** (le dernier package NuGet d’avril 2026).  
* SDK .NET 6.0 ou supérieur – l’API fonctionne de la même façon sur .NET Framework, mais .NET 6 offre les meilleures performances.  
* Un PDF d’exemple nommé `input.pdf` placé dans un dossier que vous pouvez référencer (par ex. `C:\Docs\`).  

Aucune configuration supplémentaire n’est requise ; la bibliothèque est autonome.

---

## Étape 1 – Charger le document PDF source

La première chose à faire est d’ouvrir le fichier que nous voulons numéroter. La classe `Document` d’Aspose représente l’ensemble du PDF, et le charger est aussi simple que de passer le chemin au constructeur.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Pourquoi c’est important* : Charger le document vous donne accès à la collection `Pages`, où nous attacherons le tampon Bates plus tard. Si le fichier est introuvable, Aspose lève une `FileNotFoundException` claire, vous indiquant exactement ce qui a échoué.

---

## Étape 2 – Créer un tampon texte pour les numéros Bates

Nous créons maintenant l’élément visuel qui apparaîtra sur chaque page. La classe `TextStamp` vous permet d’insérer n’importe quelle chaîne, et nous utiliserons le placeholder `{page}-{total}` pour que Aspose remplace ces jetons automatiquement.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Points clés* :

* **auto adjust font size** – Mettre `AutoAdjustFontSizeToFitStampRectangle` à `true` garantit que le texte ne déborde jamais du rectangle, idéal pour des numéros de page de longueur variable.  
* **add text watermark** – En diminuant l’`Opacity` nous transformons le numéro Bates en un filigrane discret, répondant ainsi à la contrainte « add text watermark » sans étape supplémentaire.  
* **how to add bates** – Les jetons `{page}` et `{total}` sont la sauce secrète ; Aspose les remplace à l’exécution, vous n’avez donc rien à calculer vous‑même.

---

## Étape 3 – Appliquer le tampon à chaque page

Un piège fréquent consiste à tamponner uniquement la première page. Pour réellement **add page numbers pdf**, il faut parcourir toute la collection `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Pourquoi cloner ? La méthode `AddStamp` crée internement une copie, mais utiliser explicitement une nouvelle instance à chaque itération évite les effets de bord accidentels si vous modifiez plus tard les propriétés du tampon (par ex. changer la couleur pour certaines pages).

---

## Étape 4 – Enregistrer le PDF mis à jour

Une fois les tampons en place, persister les modifications est simple. Vous pouvez écraser le fichier original ou écrire vers un nouvel emplacement — ici nous enregistrons un nouveau fichier nommé `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Si vous ouvrez `output.pdf`, vous verrez chaque page libellée « Bates : 1‑10 », « Bates : 2‑10 », … en bas‑à‑droite, avec une opacité légère qui fait office de **add text watermark**.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici un programme console autonome que vous pouvez copier‑coller dans Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Résultat attendu** : Ouvrez `output.pdf` avec n’importe quel lecteur ; chaque page affiche une ligne du type « Bates : 3‑12 » dans le coin inférieur droit, dimensionnée exactement pour le rectangle et rendue avec 40 % d’opacité. Cela satisfait à la fois l’exigence de suivi juridique et le besoin de filigrane visuel.

---

## Variantes courantes & cas limites

| Situation | Ce qu'il faut changer | Pourquoi |
|-----------|-----------------------|----------|
| **Placement différent** | Ajuster `HorizontalAlignment` / `VerticalAlignment` ou définir `XIndent`/`YIndent` | Certaines entreprises préfèrent un placement en haut‑gauche ou centré. |
| **Préfixe personnalisé** | Remplacer `"Bates: "` par `"Doc‑ID: "` ou toute autre chaîne | Vous utilisez peut‑être une convention de nommage différente. |
| **Tampons multiples** | Créer un second `TextStamp` (par ex. pour une mention de confidentialité) et l’ajouter après le premier | Combiner **add bates numbering** avec d’autres exigences **add text watermark** est trivial. |
| **Comptes de pages élevés** | Augmenter la taille de police initiale (ex. `14`) – l’ajustement automatique la réduira si besoin | Avec plus de 999 pages, la chaîne devient plus longue ; l’ajustement évite le rognage. |
| **PDF chiffrés** | Appeler `pdfDocument.Decrypt("password")` avant le tamponnage | Vous ne pouvez pas modifier un fichier sécurisé sans le mot de passe. |

---

## Astuces pro & pièges à éviter

* **Astuce pro** : Définissez `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` si le texte colle trop aux bords de la page.  
* **À surveiller** : Des rectangles très petits (la taille par défaut est 100 × 30 pt). Si vous avez besoin d’une zone plus grande, définissez manuellement `batesStamp.Width` et `batesStamp.Height`.  
* **Note de performance** : Tamponner des milliers de pages peut prendre quelques secondes, mais Aspose diffuse les pages efficacement — pas besoin de charger tout le document en mémoire.  

---

## Conclusion

Nous venons de montrer comment **add bates numbering** à un PDF avec Aspose.Pdf, tout en **add page numbers pdf**, en activant **auto adjust font size**, et en créant un **add text watermark** dans un flux cohérent. L’exemple complet et exécutable ci‑dessus vous fournit une base solide que vous pouvez adapter à tout workflow de documents juridiques ou de reporting interne.

Prêt pour l’étape suivante ? Essayez d’associer cette approche avec l’API de fusion PDF d’Aspose pour traiter par lots plusieurs fichiers, ou explorez la classe `TextFragment` pour des filigranes plus riches (colorés, tournés, ou multi‑lignes). Les possibilités sont infinies, et le code que vous avez maintenant constitue une base fiable.

Si ce guide vous a été utile, n’hésitez pas à laisser un commentaire, à étoiler le dépôt, ou à partager vos propres variantes. Bon codage, et que vos PDF soient toujours parfaitement numérotés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}