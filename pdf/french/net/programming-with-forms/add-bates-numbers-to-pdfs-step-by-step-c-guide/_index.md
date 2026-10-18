---
category: general
date: 2026-02-12
description: Ajoutez rapidement des numéros Bates aux fichiers PDF. Apprenez comment
  ajouter un champ de texte PDF, ajouter un champ de formulaire PDF et ajouter des
  numéros de page PDF en utilisant Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: fr
og_description: Ajoutez des numéros Bates aux documents PDF en C#. Ce guide montre
  comment ajouter un champ de texte PDF, ajouter un champ de formulaire PDF et ajouter
  des numéros de page PDF avec Aspose.PDF.
og_title: Ajouter des numéros Bates aux PDF – Tutoriel complet C#
tags:
- PDF
- C#
- Aspose.PDF
title: Ajouter des numéros Bates aux PDF – Guide C# étape par étape
url: /fr/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---



{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des numéros Bates aux PDF – Guide complet en C#

Vous avez déjà eu besoin **d’ajouter des numéros Bates** à une pile de PDF juridiques sans savoir par où commencer ? Vous n’êtes pas seul. Dans de nombreux cabinets d’avocats et projets d’e‑discovery, tamponner chaque page avec un identifiant unique est une tâche quotidienne, et le faire manuellement est un cauchemar.  

La bonne nouvelle ? Avec quelques lignes de C# et Aspose.PDF, vous pouvez automatiser le tout. Dans ce tutoriel, nous verrons **comment ajouter des numéros Bates**, placer un champ texte sur chaque page, et enregistrer un PDF propre et interrogeable — le tout sans effort.

> **Ce que vous obtiendrez :** un exemple de code entièrement exécutable, des explications sur l’importance de chaque ligne, des astuces pour les cas limites, et une petite checklist pour vérifier votre résultat.  

Nous aborderons également des tâches connexes comme **add text field pdf**, **add form field pdf**, et **add page numbers pdf**, afin que vous disposiez d’une boîte à outils prête pour tout défi d’automatisation de documents.

---

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+)  
- Visual Studio 2022 (ou tout IDE de votre choix)  
- Une licence valide d’Aspose.PDF pour .NET (l’essai gratuit suffit pour les tests)  
- Un PDF source nommé `source.pdf` placé dans un dossier que vous pouvez référencer  

Si l’un de ces éléments vous est inconnu, faites une pause et installez ce qui manque avant de continuer. Les étapes ci‑dessous supposent que vous avez déjà ajouté le package NuGet Aspose.PDF :

```bash
dotnet add package Aspose.Pdf
```

---

## Comment ajouter des numéros Bates à un PDF avec Aspose.PDF

Voici le programme complet, prêt à copier‑coller. Il charge un PDF, crée un **champ de zone de texte** sur chaque page, écrit un numéro Bates formaté, puis enregistre le fichier modifié.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Pourquoi cela fonctionne

- **`Document`** est le point d’entrée ; il représente le fichier PDF entier.  
- **`Rectangle`** définit l’emplacement du champ sur la page. Les dimensions sont en points (1 pt ≈ 1/72 in). Ajustez les coordonnées si vous avez besoin du numéro dans un coin différent.  
- **`TextBoxField`** est un *form field* qui peut contenir n’importe quelle chaîne. En assignant `Value`, nous **add page numbers pdf** avec un préfixe personnalisé.  
- **`pdfDocument.Form.Add`** enregistre le champ dans l’AcroForm du PDF, le rendant visible dans les visionneuses comme Adobe Acrobat.  

Si vous devez modifier l’apparence (police, couleur, taille), vous pouvez ajuster les propriétés du `TextBoxField` — voir la documentation Aspose pour `DefaultAppearance` et `Border`.

---

## Ajouter un champ texte à chaque page PDF (l’étape « add text field pdf »)

Parfois, vous ne voulez qu’une étiquette visible, pas un champ de formulaire interactif. Dans ce cas, remplacez le `TextBoxField` par un `TextFragment` et ajoutez‑le directement à la collection `Paragraphs` de la page. Voici une alternative rapide :

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

L’approche **add text field pdf** est utile lorsque le document final sera en lecture‑seule, tandis que la méthode **add form field pdf** garde les numéros modifiables ultérieurement.

---

## Enregistrer le PDF avec les numéros Bates (le moment « add page numbers pdf »)

Une fois la boucle terminée, l’appel à `pdfDocument.Save` écrit tout sur le disque. Si vous devez préserver le fichier original, changez simplement le chemin de sortie ou utilisez les surcharges de `pdfDocument.Save` pour diffuser le résultat directement dans une réponse d’API web.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

C’est la partie pratique — pas de fichiers temporaires, pas de bibliothèques supplémentaires, juste Aspose qui fait le gros du travail.

---

## Résultat attendu & Vérification rapide

Ouvrez `bates.pdf` dans n’importe quel lecteur PDF. Vous devez voir une petite boîte dans le coin inférieur gauche de chaque page affichant :

```
BATES-00001
BATES-00002
…
```

Si vous inspectez les propriétés du document, vous remarquerez un AcroForm contenant des champs nommés `Bates_1`, `Bates_2`, etc. Cela confirme que l’étape **add form field pdf** a réussi.

---

## Pièges courants & Astuces pro

| Problème | Pourquoi cela arrive | Solution |
|----------|----------------------|----------|
| Les numéros sont décalés | Les coordonnées du rectangle sont relatives au coin inférieur gauche de la page. | Inversez la valeur Y (`pageHeight - marginTop`) ou utilisez `page.PageInfo.Height` pour calculer une marge supérieure. |
| Les champs sont invisibles dans Adobe Reader | La bordure par défaut est définie sur « No ». | Définissez `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Les gros PDF provoquent une pression mémoire | `using` libère le document seulement après la fin de la boucle. | Traitez les pages par lots ou utilisez `pdfDocument.Save` avec des `SaveOptions` qui activent le streaming. |
| Licence non appliquée | Aspose ajoute un filigrane sur la première page. | Enregistrez votre licence dès le départ : `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Étendre la solution

- **Préfixes personnalisés :** Remplacez `"BATES-"` par n’importe quelle chaîne (`"DOC-"`, `"CASE-"`, …).  
- **Longueur du remplissage de zéros :** Changez `{pageNumber:D5}` en `{pageNumber:D3}` pour trois chiffres.  
- **Placement dynamique :** Utilisez `pdfDocument.Pages[pageNumber].PageInfo.Width` pour positionner le champ du côté droit.  
- **Numérotation conditionnelle :** Ignorez les pages blanches en vérifiant `pdfDocument.Pages[pageNumber].IsBlank`.

Toutes ces variantes conservent le schéma de base **add bates numbers**, **add text field pdf**, et **add form field pdf**.

---

## Exemple complet (tout‑en‑un)

Voici le programme final, prêt à être exécuté. Copiez‑le dans une nouvelle application console et appuyez sur F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Exécutez‑le, ouvrez le résultat, et vous verrez un identifiant au look professionnel sur chaque page — exactement ce qu’attend un spécialiste du support juridique.

---

## Conclusion

Nous venons de démontrer **comment ajouter des numéros Bates** à n’importe quel PDF avec C# et Aspose.PDF. En créant un **text box field** sur chaque page, nous **add text field pdf**, **add form field pdf**, et **add page numbers pdf** en une seule passe. L’approche est rapide, évolutive et facile à ajuster pour des préfixes personnalisés, des mises en page différentes ou une logique conditionnelle.

Prêt pour le prochain défi ? Essayez d’intégrer un QR code qui pointe vers le dossier du dossier original, ou générez une page d’index séparée listant tous les numéros Bates avec leurs titres de page correspondants. La même API vous permet de fusionner des PDF, d’extraire des pages, et même de masquer des données sensibles — le ciel est la limite.

Si vous rencontrez un problème, laissez un commentaire ci‑dessous ou consultez la documentation officielle d’Aspose pour approfondir. Bon codage, et que vos PDF restent toujours parfaitement numérotés !  

---  

![capture d'écran d'ajout de numéros Bates](https://example.com/images/add-bates-numbers.png "exemple d'ajout de numéros Bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}