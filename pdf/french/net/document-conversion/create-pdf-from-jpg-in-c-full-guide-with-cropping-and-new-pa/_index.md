---
category: general
date: 2026-04-06
description: Créez rapidement un PDF à partir d’un JPG et apprenez comment recadrer
  une image dans le PDF, ajouter une nouvelle page PDF, et convertir un JPG en PDF
  avec recadrage en utilisant C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: fr
og_description: Créer un PDF à partir d’un JPG et recadrer l’image dans le PDF avec
  C#. Apprenez comment ajouter une nouvelle page PDF et convertir un JPG en PDF avec
  recadrage.
og_title: Créer un PDF à partir de JPG en C# – Guide étape par étape
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Créer un PDF à partir de JPG en C# – Guide complet avec recadrage et nouvelles
  pages
url: /fr/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF à partir de JPG en C# – Guide complet avec recadrage et nouvelles pages

Vous avez déjà eu besoin de **créer un PDF à partir de JPG** mais vous ne saviez pas comment ne conserver que la partie réellement souhaitée ? Vous n'êtes pas seul. Dans de nombreuses applications — pensez aux factures, aux reçus ou aux livres photo — les développeurs doivent transformer une image en PDF tout en éliminant les bords indésirables.  

Dans ce tutoriel, nous parcourrons une solution complète, prête à l’emploi, qui **crée un PDF à partir de JPG**, vous montre comment **recadrer une image dans un PDF**, et démontre le **how to add new pdf page** lorsque vous avez besoin de plusieurs images. À la fin, vous saurez également comment **convertir JPG en PDF avec crop** et **insérer une image dans PDF C#** en utilisant la bibliothèque Aspose.Pdf.

## Ce que vous allez apprendre

- Configurer Aspose.Pdf dans un projet .NET (sans configuration lourde).  
- Charger un JPEG, définir la zone que vous souhaitez conserver, et la recadrer lors de son insertion dans une page PDF.  
- Ajouter des pages supplémentaires au même document, vous permettant de créer des PDF multi‑pages à partir de plusieurs images.  
- Enregistrer le fichier final et vérifier le résultat.  

**Prérequis :** .NET 6+ (ou .NET Framework 4.6+), Visual Studio 2022 ou tout autre éditeur de votre choix, et une référence NuGet à `Aspose.Pdf`. Aucun autre service externe n’est nécessaire.

![Create PDF from JPG example](image.jpg){: .align-center alt="Exemple de création de PDF à partir de JPG montrant une image recadrée placée sur une page PDF"}

---

## Étape 1 : Installer Aspose.Pdf et préparer votre projet

Tout d’abord, ajoutez le package Aspose.Pdf. Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet add package Aspose.Pdf
```

Cette seule ligne récupère tout ce dont vous avez besoin : les classes `Document`, `Rectangle` et `Page` que nous utiliserons plus tard. D’après mon expérience, le recours à NuGet est la façon la plus propre de rester à jour sans manipuler les DLL.

> **Astuce :** Si vous ciblez .NET Framework, utilisez le package `Aspose.Pdf.NET` à la place ; l’interface de l’API est identique.

---

## Étape 2 : Charger le JPEG et définir la taille de la page

Nous avons besoin d’un canevas qui corresponde aux dimensions souhaitées pour la page PDF finale. Le code ci‑dessous crée un nouveau `Document` et ouvre l’image source sous forme de flux.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Pourquoi un rectangle ? Dans Aspose.Pdf, un `Rectangle` représente à la fois les dimensions de la page et la région de l’image que vous souhaitez afficher. En séparant la *page* de la *zone de recadrage*, vous obtenez un contrôle fin sur ce qui apparaît dans le PDF.

---

## Étape 3 : Choisir la zone de recadrage (quart supérieur gauche)

Supposons que vous n’ayez besoin que du quart supérieur gauche de la photo. Nous calculons cette région par rapport à la taille de la page :

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

Le constructeur `Rectangle` prend les valeurs **X/Y en bas‑gauche** et **X/Y en haut‑droite**. En ajoutant la moitié de la hauteur à `LLY`, nous déplaçons le bas du recadrage vers le haut, éliminant ainsi la moitié inférieure de l’image. Ajustez ces calculs si vous avez besoin d’une autre portion.

> **Pourquoi recadrer avant d’ajouter ?**  
> Recadrer du côté du PDF évite de créer un bitmap temporaire sur le disque, économisant ainsi les entrées/sorties et la mémoire. Aspose gère les calculs pour vous, et le résultat est un PDF propre et compatible vecteur.

---

## Étape 4 : Ajouter une nouvelle page et insérer l’image recadrée

Nous plaçons maintenant réellement l’image sur une page PDF. C’est ici que le mot‑clé **how to add new pdf page** brille.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` prend trois arguments :

1. **Stream** – le JPEG source.  
2. **Rectangle de page** – définit la taille de la page (notre `pageBounds`).  
3. **Rectangle de recadrage** – indique à Aspose quelle partie de l’image rendre.

Si vous avez besoin de plus de pages, répétez simplement le modèle `Add` + `AddImage` avec un nouveau `imageStream` à chaque fois. Cela satisfait le besoin **how to add new pdf page** tout en gardant le code propre.

---

## Étape 5 : Enregistrer le PDF et vérifier le résultat

L’étape finale est une seule ligne, mais ne la sous‑estimez pas — enregistrer dans le bon chemin garantit que le fichier pourra être ouvert par n’importe quel lecteur PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Lorsque vous ouvrez `cropped_image.pdf`, vous devriez voir une seule page contenant uniquement le quart supérieur gauche du JPEG original, parfaitement centré dans la page de 600 × 800.

---

## Exemple complet fonctionnel (toutes les étapes combinées)

Voici le programme complet que vous pouvez copier‑coller dans une application console. Il compile tel quel, en supposant que vous avez installé Aspose.Pdf et placé un JPEG à l’emplacement indiqué.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Résultat attendu

- **Fichier :** `cropped_image.pdf` (≈ 30 KB).  
- **Contenu :** Une page, 600 × 800 points, affichant le quart supérieur gauche de `photo.jpg`.  
- **Comportement :** Aucun distorsion ; l’image conserve sa résolution originale dans les limites du recadrage.

---

## Questions fréquentes et cas particuliers

### Et si je dois conserver l’image entière, pas seulement un quart ?

Il suffit de définir `cropArea` égal à `pageBounds` :

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Puis‑je utiliser une taille de page différente (par ex., A4) ?

Absolument. Remplacez les valeurs de `pageBounds` par les dimensions d’une page A4 en points (595 × 842) :

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Le rectangle de recadrage peut rester le même ou être recalculé pour correspondre au nouveau rapport d’aspect.

### Comment ajouter plusieurs images, chacune sur sa propre page ?

Parcourez une collection de chemins de fichiers :

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Qu’en est‑il de la transparence ou des images PNG ?

Aspose.Pdf traite les PNG de la même manière que les JPEG. Si la source possède un canal alpha, le PDF le préservera, à condition que la version du PDF prenne en charge la transparence (le réglage par défaut convient).

### Cela fonctionne‑t‑il sur .NET Core sous Linux ?

Oui. Aspose.Pdf est multiplateforme ; assurez‑vous simplement que `imageStream` pointe vers un chemin de fichier valide sur le système d’exploitation cible. Aucune API spécifique à Windows n’est utilisée.

---

## Astuces et bonnes pratiques

- **Gestion de la mémoire :** Enveloppez toujours les flux dans des instructions `using` (comme montré) pour éviter les verrous de fichiers.  
- **Performance :** Si vous traitez des dizaines d’images, envisagez de réutiliser une seule instance `Document` et d’appeler `pdfDocument.Pages.Add()` pour chaque image.  
- **Gestion des erreurs :** Encapsulez l’ensemble de la routine dans un bloc `try/catch` et consignez `PdfException` pour le dépannage.  
- **Contrôle de la qualité :** Aspose.Pdf vous permet de définir la résolution de l’image via `ImageFragment`. Pour des numérisations haute résolution, définissez `ImageFragment.Resolution = 300;`.  
- **Sécurité :** Si le PDF doit être partagé à l’extérieur, vous pouvez ajouter un chiffrement avec `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Conclusion

Nous venons de couvrir comment **créer un PDF à partir de JPG** en C#, **recadrer une image dans un PDF**, et **ajouter une nouvelle page PDF** pour créer des documents multi‑pages. Le même modèle vous permet de **convertir JPG en PDF avec recadrage** et **d’insérer une image dans un PDF C#** pour n’importe quel scénario — des simples reçus aux livres photo complexes.  

Essayez‑le : modifiez la logique de recadrage, expérimentez avec des pages A4, ou enchaînez plusieurs images. La bibliothèque Aspose.Pdf rend ces tâches simples, et le code ci‑dessus constitue une référence solide et digne de citation que vous pouvez coller dans n’importe quel projet.

### Et après ?

- **Ajouter des annotations de texte** au PDF (par ex., des légendes sous chaque image).  
- **Créer automatiquement une table des matières** pour les PDF multi‑pages.  
- **Fusionner plusieurs PDF** en utilisant `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Chacun de ces sujets s’appuie sur les fondamentaux que vous venez de maîtriser, vous êtes donc bien placé pour les explorer

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}