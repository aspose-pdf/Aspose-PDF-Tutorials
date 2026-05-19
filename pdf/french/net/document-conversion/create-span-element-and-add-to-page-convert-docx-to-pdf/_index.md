---
category: general
date: 2026-03-27
description: Créer un élément span en C# et apprendre comment ajouter un span à une
  page lors de la conversion de DOCX en PDF et de l’enregistrement en PDF. Guide étape
  par étape pour les développeurs.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: fr
og_description: Créer un élément span en C# et apprendre comment ajouter un span à
  une page lors de la conversion de DOCX en PDF, puis enregistrer en PDF. Exemple
  de code complet inclus.
og_title: Créer un élément <span> et l’ajouter à la page – Convertir DOCX en PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Créer un élément span et l’ajouter à la page – Convertir DOCX en PDF
url: /fr/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un élément span et l'ajouter à la page – Convertir DOCX en PDF

Créer un **élément span** dans un fichier DOCX est une tâche courante lorsque vous avez besoin d'un contrôle précis de la mise en page. Dans ce tutoriel, nous vous montrerons **comment ajouter un span** à une page, **convertir DOCX en PDF**, et **enregistrer en PDF** — le tout en quelques étapes simples.  

Si vous avez déjà fixé un document Word en pensant « J'aimerais pouvoir placer une petite zone de texte à une coordonnée précise », vous êtes au bon endroit. Nous parcourrons l’ensemble du flux de travail, du chargement du fichier source à l’obtention d’un PDF soigné.

## Ce que vous accomplirez

* Charger un fichier `.docx` en utilisant la classe `Document` de la bibliothèque de documents.  
* **Créer un élément span** avec l'API `TaggedContent`.  
* Positionner ce span aux coordonnées X/Y exactes sur une page choisie.  
* **Ajouter l'élément à la page** de manière fiable, même lorsque la page n’est pas la première.  
* **Convertir DOCX en PDF** et **enregistrer en PDF** avec un seul appel `Save`.

Pas d'outils externes, pas de paramètres mystérieux — juste du code C# simple que vous pouvez copier‑coller dans votre projet.

## Prérequis

* .NET 6+ (ou tout runtime .NET récent supporté par votre bibliothèque).  
* Le SDK de traitement de documents qui fournit `Document`, `TaggedContent`, `Position`, etc.  
* Une compréhension de base de la syntaxe C# — si vous pouvez écrire un `Console.WriteLine`, vous êtes bon.

> **Astuce :** Gardez votre version du SDK à jour ; la dernière version (v3.2 en mars 2026) inclut des améliorations de performance pour les opérations au niveau des pages.

---

![Diagramme illustrant comment créer un élément span et le placer sur une page PDF](https://example.com/images/create-span-element.png "Diagramme de placement de l'élément span")

## Créer un élément span – Positionner et ajouter à la page

Ci-dessous se trouve le code complet et exécutable qui fait tout, du chargement du DOCX source à l'écriture du PDF final. N'hésitez pas à le coller dans une application console, à ajuster les chemins, et à l'exécuter.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Explication étape par étape

#### Étape 1 – Charger le document DOCX  
Nous instancions un objet `Document` pointant vers `input.docx`. Cet objet représente l'intégralité du fichier Word en mémoire, nous donnant accès aux pages, au contenu et aux métadonnées.  

#### Étape 2 – Créer un élément span  
L'appel `TaggedContent.CreateSpanElement()` renvoie un conteneur en ligne léger. Pensez-y comme une petite boîte invisible pouvant contenir du texte, des images ou d'autres éléments en ligne. Ajouter du texte (`span.Text`) est optionnel mais utile pour le débogage.

#### Étape 3 – Positionner le span  
`new Position(50, 750)` place le coin supérieur gauche du span à 50 pts du bord gauche et 750 pts du haut de la page. Ces valeurs sont absolues, vous pouvez donc placer le span n'importe où — idéal pour des mises en page précises.

#### Étape 4 – Ajouter le span à la page cible  
`doc.Pages[1].Add(span)` injecte le span dans la deuxième page. L'API utilise un indexage à base zéro, donc la page 0 est la première page. Si vous devez l'ajouter à la première page, utilisez simplement `doc.Pages[0]`.

#### Étape 5 – Convertir DOCX en PDF et enregistrer en PDF  
Appeler `doc.Save("output.pdf")` fait deux choses : il écrit le document modifié sur le disque **et** convertit le contenu en PDF grâce à l'extension `.pdf`. Aucun pas de conversion supplémentaire n'est requis — c’est la façon la plus simple de **enregistrer en PDF**.

---

## Comment ajouter un span sur une page différente (avancé)

Parfois, vous ne connaissez pas l'index de la page à l'avance. Vous pouvez localiser une page par son numéro (lisible par l'homme) ou en recherchant un mot‑clé spécifique.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Pourquoi c'est important :** Dans les rapports où le nombre de pages varie, coder en dur `Pages[1]` peut casser la mise en page. Cet extrait montre un modèle robuste pour **comment ajouter un span** dynamiquement.

---

## Pièges courants et comment les éviter

| Problème | Ce qui se passe | Solution |
|----------|----------------|----------|
| **Span non visible** | Les coordonnées sont hors de la page ou le span a une largeur/hauteur nulle. | Vérifiez à nouveau les valeurs de `Position` ; utilisez une règle dans votre visualiseur PDF. |
| **Index de page incorrect** | Vous ajoutez à la page 0 mais vous vous attendez à la page 2. | Rappelez‑vous que l'API utilise un index à base zéro ; ajoutez 1 au numéro de page lisible. |
| **Enregistrement écrase la source** | `doc.Save("input.docx")` remplace le fichier original. | Enregistrez toujours vers un nouveau chemin (`output.pdf`) lors de la conversion. |
| **Référence SDK manquante** | Erreur de compilation sur la classe `Document`. | Installez le paquet NuGet : `dotnet add package DocumentProcessing.SDK`. |

---

## Vérification du résultat

Après avoir exécuté le programme, ouvrez `output.pdf` dans n'importe quel visualiseur PDF. Vous devriez voir le texte « Hello, world! » positionné exactement à (50, 750) sur la deuxième page. Si le texte apparaît ailleurs, ajustez les valeurs de `Position` et relancez.  

Pour les tests automatisés, vous pouvez utiliser un analyseur PDF (par ex., iTextSharp) afin d'affirmer les coordonnées du texte de façon programmatique.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Prochaines étapes

* **Styliser le span** – explorez `span.Font`, `span.Color` et d'autres propriétés de style.  
* **Ajouter des images** – utilisez `CreateImageElement()` à la place d'un span pour les graphiques.  
* **Traitement par lots** – parcourez un dossier de fichiers DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}