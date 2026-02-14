---
category: general
date: 2026-02-14
description: Ajoutez une numérotation Bates à vos PDF en toute simplicité. Apprenez
  à ajouter des numéros de page en pied de page et à insérer des numéros séquentiels
  dans les PDF avec Aspose.Pdf en quelques minutes.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: fr
og_description: Ajoutez rapidement une numérotation Bates aux PDF. Ce guide montre
  comment ajouter des numéros de page en pied de page et des numéros séquentiels aux
  PDF en utilisant Aspose.Pdf, avec le code complet et des astuces.
og_title: Ajouter une numérotation Bates à un PDF – Tutoriel C# étape par étape
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Ajouter la numérotation Bates PDF – Guide complet C#
url: /fr/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter la numérotation Bates aux PDF – Guide complet C#

Vous avez déjà eu besoin d'**ajouter une numérotation Bates aux fichiers PDF** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Les équipes juridiques, les auditeurs et toute personne manipulant de grands ensembles de documents demandent constamment : « Comment ajouter des numéros Bates sans casser la mise en page ? » La bonne nouvelle, c’est qu’avec Aspose.Pdf pour .NET, vous pouvez injecter ces numéros sous forme de simple pied de page — aucune édition manuelle requise.

Dans ce tutoriel, nous allons parcourir une solution pratique, de bout en bout, qui non seulement **ajoute des numéros de page en pied de page**, mais vous permet également d'**ajouter des numéros séquentiels aux PDF** avec un préfixe personnalisé, une taille de police et un alignement. À la fin, vous disposerez d’un programme C# prêt à l’emploi, d’une compréhension claire de l’importance de chaque paramètre, et de quelques astuces professionnelles pour éviter les pièges les plus courants.

## Ce que vous apprendrez

- Comment charger un PDF existant et le préparer pour la numérotation Bates.  
- Quelles propriétés de **BatesNumberingOptions** contrôlent l’apparence et le placement.  
- Comment appliquer la numérotation à chaque page en un seul appel.  
- Comment personnaliser le préfixe, le numéro de départ et les marges pour différents formats juridiques.  
- Gestion des cas limites — que faire avec les PDF chiffrés ou les documents contenant déjà des pieds de page.

**Prérequis** : .NET 6+ (ou .NET Framework 4.7+), une version récente d’Aspose.Pdf (l’exemple utilise la 23.10), et un PDF d’entrée dont vous possédez les droits de modification. Aucune autre bibliothèque tierce n’est nécessaire.

---

## Étape 1 – Charger le PDF que vous souhaitez numéroter

La première chose que nous faisons est de créer une instance `Document` qui pointe vers le fichier source. Le modèle `using var` garantit que le handle du fichier est libéré automatiquement.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Pourquoi c’est important :** Aspose.Pdf lit toute la structure du PDF en mémoire, ce qui nous permet de manipuler les pages, les annotations et les métadonnées sans toucher au fichier original sur le disque. Si le PDF est protégé par mot de passe, vous pouvez transmettre le mot de passe au constructeur — voir la note « PDF chiffrés » à la fin.

---

## Étape 2 – Définir vos options de numérotation Bates

Les numéros Bates sont essentiellement des pieds de page avec un préfixe configurable et un compteur séquentiel. La classe `BatesNumberingOptions` vous permet d’ajuster chaque aspect visuel.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Astuce rapide

- **Prefix** : Utilisez un identifiant court et unique (par ex., le numéro de dossier) pour garder le pied de page lisible.  
- **StartNumber** : Les cabinets juridiques commencent souvent à `1` ou à un décalage personnalisé ; choisissez ce qui correspond à votre système de classement.  
- **Margins** : La marge inférieure de `20` points garde le texte à l’écart des notes de bas de page ou des signatures qui pourraient déjà se trouver près du bord de la page.

---

## Étape 3 – Appliquer la numérotation à toutes les pages

Une fois les options configurées, l’injection réelle se résume à une seule ligne. Aspose.Pdf gère la pagination, met à jour les flux de contenu existants et respecte automatiquement la rotation des pages.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Que se passe-t-il en coulisses ?** La bibliothèque itère sur chaque objet `Page`, crée un `TextFragment` qui intègre le préfixe et le compteur actuel, puis le dessine en utilisant le système de coordonnées de la page. Comme nous avons défini `HorizontalAlignment.Right` et `VerticalAlignment.Bottom`, le texte se place dans le coin inférieur droit quel que soit le format de la page.

---

## Étape 4 – Enregistrer le PDF modifié

Enfin, écrivez le résultat dans un nouveau fichier. Il est possible d’écraser l’original, mais conserver une copie aide à la gestion des versions.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Si vous devez préserver les métadonnées originales (auteur, date de création), Aspose.Pdf les copie par défaut. Vous pouvez également spécifier un objet `SaveOptions` pour la conformité PDF/A ou la compression.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Collez‑le dans un projet d’application console, ajustez les chemins de fichiers, et appuyez sur **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Résultat attendu** : chaque page de `output.pdf` affiche désormais un pied de page tel que `ABC-1000`, `ABC-1001`, … ancré dans le coin inférieur droit. Ouvrez le fichier avec n’importe quel lecteur PDF pour vérifier.

---

## Gestion des variations courantes

### Ajouter uniquement des numéros de page en pied de page

Si vous avez seulement besoin de numéros de page simples sans préfixe, définissez `Prefix = ""` et ajustez éventuellement la marge pour éviter les collisions avec les pieds de page existants.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Utiliser un alignement différent

Les documents juridiques exigent parfois que le numéro soit centré en bas. Changez simplement l’alignement :

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Gérer les PDF chiffrés

Lorsque le PDF source est protégé par mot de passe, fournissez le mot de passe comme suit :

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Le reste du flux de travail reste identique.

### Ignorer les pieds de page existants

Si un document contient déjà un pied de page que vous ne voulez pas écraser, vous pouvez préfixer une chaîne personnalisée qui rend le nouveau numéro distinct, ou parcourir les pages manuellement et ajouter un `TextFragment` uniquement là où le pied de page est absent. La classe `Page` de la bibliothèque expose les collections `Annotations` et `Contents` pour un contrôle granulaire.

---

## Astuces pro & pièges

- **Éviter la coupe** : des marges inférieures très petites peuvent entraîner la coupure du texte à l’impression. Testez avec une impression physique si vous devez distribuer des copies papier.  
- **Performance** : ajouter des numéros Bates à un PDF de 500 pages prend moins d’une seconde sur un ordinateur portable moderne, mais les gros lots bénéficient d’un traitement parallèle — rappelez‑vous simplement que `Document` n’est pas thread‑safe, chaque thread doit donc disposer de sa propre instance.  
- **Compatibilité de version** : le code fonctionne avec Aspose.Pdf 23.10 et versions ultérieures. Si vous utilisez une version antérieure, les noms de propriétés sont les mêmes mais le constructeur `MarginInfo` peut nécessiter des arguments `float`.  
- **Conformité légale** : certaines juridictions exigent que le numéro Bates soit placé à un emplacement précis (par ex., en bas à gauche). Ajustez le `HorizontalAlignment` en conséquence.

---

## Conclusion

Nous venons de démontrer comment **ajouter une numérotation Bates aux fichiers PDF** en utilisant Aspose.Pdf pour .NET, couvrant tout, du chargement du document à l’enregistrement de la version finale avec un pied de page propre. En ajustant quelques propriétés, vous pouvez également **ajouter des numéros de page en pied de page**, **ajouter des numéros séquentiels aux PDF**, ou personnaliser l’apparence pour répondre à n’importe quelle norme juridique.

Prêt pour l’étape suivante ? Essayez de combiner cette technique avec l’extraction OCR de texte pour intégrer des mots‑clés recherchables à côté de vos numéros Bates, ou automatisez le processus pour des dossiers entiers en utilisant `Directory.GetFiles`. Les possibilités sont infinies, et la base que vous avez maintenant rendra ces extensions sans effort.

Bon codage, et que vos PDF soient toujours parfaitement numérotés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}