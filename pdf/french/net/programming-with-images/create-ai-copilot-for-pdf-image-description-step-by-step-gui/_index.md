---
category: general
date: 2026-08-04
description: Créer un copilote IA pour générer des descriptions d'images pour les
  fichiers PDF. Apprenez à configurer les options d'image d'OpenAI et à extraire les
  descriptions d'images efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: fr
lastmod: 2026-08-04
og_description: Créer un copilote IA pour générer des descriptions d'images pour les
  fichiers PDF. Ce tutoriel vous montre comment configurer les options d'image d'OpenAI,
  exécuter le copilote et extraire la description d'image en C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Créer un copilote IA pour la description d'images PDF – guide complet
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Créer un copilote IA pour la description d’images PDF – guide étape par étape
url: /fr/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créez un copilote IA pour la description d’images PDF – guide complet

Si vous devez **créer un copilote IA** qui rédige automatiquement des descriptions pour les images intégrées dans un PDF, ce guide vous montre exactement comment le faire. Vous apprendrez à configurer les options d’image OpenAI, à exécuter le copilote et à **extraire la description d’image** sans quitter votre projet C#.

Générer du contenu textuel pour les images PDF est une exigence courante pour l’accessibilité, l’indexation de contenu et les rapports automatisés. À la fin de ce tutoriel, vous disposerez d’un composant réutilisable qui **génère des descriptions d’image** pour tout document PDF que vous lui indiquerez.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou version ultérieure installé  
* Une licence Aspose.Pdf.AI (ou un essai gratuit)  
* Une clé API OpenAI que le client Aspose peut utiliser  
* Visual Studio 2022 (ou tout IDE supportant C#)  

Aucun package NuGet supplémentaire n’est requis au‑delà de `Aspose.Pdf.AI`.

## Étape 1 : Configurer le client Aspose.Pdf.AI

La première étape consiste à instancier le client IA avec vos informations d’authentification. Le client gère la communication avec le service OpenAI en coulisses.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Pourquoi c’est important :** Le `AiClient` encapsule tous les paramètres au niveau de la requête (clé API, délai d’attente, politique de nouvelle tentative). Le créer une fois et le réutiliser dans plusieurs instances de copilote réduit la surcharge et garantit une authentification cohérente.

## Étape 2 : Créer un copilote de description d’image

Vous créez maintenant le **copilote IA** qui lira le PDF et produira une description pour chaque image. La méthode de fabrique `CreateImageDescriptionCopilot` accepte le client et un ensemble d’options qui définissent comment la description est générée.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Pourquoi c’est important :**  
* `OpenAIImageDescriptionOptions` (les **options d’image OpenAI**) vous permettent d’ajuster le modèle de langage. Modifier la température ou le modèle peut améliorer la pertinence pour les diagrammes techniques versus les photos naturelles.  
* Spécifier le chemin du document indique au copilote quel PDF analyser. Le copilote extrait chaque image raster, l’envoie au modèle et renvoie une description lisible par l’homme.

## Étape 3 : Récupérer la description générée de façon asynchrone

Le copilote fonctionne de manière asynchrone car il peut être nécessaire de télécharger plusieurs mégaoctets de données d’image et d’attendre la réponse du modèle. Utilisez `await` pour vous assurer que l’appel se termine avant d’accéder au résultat.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Pourquoi c’est important :** La méthode renvoie un `Dictionary<int, string>` qui associe chaque page (ou indice d’image) à sa description. Gérer `AiException` vous permet de signaler les erreurs réseau ou de quota au lieu de faire planter l’application.

## Étape 4 : Afficher ou stocker la description

Vous pouvez écrire les descriptions dans la console, un fichier de log, ou les intégrer de nouveau dans le PDF en tant que texte alternatif pour l’accessibilité. Voici un exemple rapide qui écrit la sortie dans un fichier JSON pour une utilisation ultérieure.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Pourquoi c’est important :** Stocker la sortie au format JSON préserve l’association entre chaque page et sa description, ce qui facilite la consommation des données par les processus en aval (indexation de recherche, rendu UI, etc.).

## Gestion de plusieurs images par page

Si une page contient plusieurs images, le copilote renvoie une description concaténée séparée par des sauts de ligne. Pour les séparer, inspectez le résultat brut et divisez sur `\n\n` (double saut de ligne). Voici une méthode d’aide :

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Vous pouvez ensuite parcourir chaque description d’image individuelle et les stocker séparément si besoin.

## Cas particulier : gros PDF et gestion du délai d’attente

Traiter un PDF de plus de 100 Mo peut dépasser les délais d’attente HTTP par défaut. Ajustez le paramètre de délai d’attente du client lors de la création du `AiClient` :

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Augmenter le délai d’attente empêche une terminaison prématurée pendant que le service traite de nombreuses images haute résolution.

## Astuce pro : mettre en cache les résultats pour réduire les coûts

OpenAI facture à la token, et la description d’image peut être répétitive entre différentes versions du même rapport. Mettez en cache la sortie JSON et réutilisez‑la lorsque le hachage du PDF correspond à un fichier déjà traité. Cette pratique économise de l’argent et accélère les exécutions suivantes.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Stockez le hachage avec le fichier JSON ; si le hachage correspond lors d’une exécution ultérieure, sautez l’appel IA.

## Exemple complet exécutable

En réunissant tous les éléments, voici une application console autonome que vous pouvez coller dans un nouveau projet .NET.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Sortie attendue (troncature)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Le programme lit `AnnualReport.pdf`, crée un **copilote IA**, et écrit un fichier JSON qui associe chaque page à sa description générée.

## Questions fréquentes

* **Cela fonctionne‑t‑il avec des PDF chiffrés ?**  
  Oui, mais vous devez fournir le mot de passe lors de la création du copilote :  
  `imageOptions.WithPassword("mySecret")`.

* **Puis‑je limiter le traitement à des pages spécifiques ?**  
  Utilisez `imageOptions.WithPageRange(1, 10)` pour restreindre le copilote aux pages 1‑10.

* **Que se passe‑t‑il si une image contient du texte ?**  
  Le modèle tente de décrire le contenu visuel ; pour une extraction de texte de type OCR, utilisez plutôt `CreateTextExtractionCopilot`.

## Conclusion

Vous savez maintenant comment **créer un copilote IA** qui **génère des descriptions d’image** pour des fichiers PDF, configurer les **options d’image OpenAI**, et **extraire la description d’image** de façon programmatique en C#. L’exemple complet illustre les meilleures pratiques telles que la gestion asynchrone, la gestion des erreurs et la mise en cache des résultats.

Ensuite, vous pourriez explorer :

* Ajouter les descriptions générées dans le PDF en tant que texte alternatif pour améliorer l’accessibilité (`PdfDocument` → `PdfImage.AlternativeText`).  
* Utiliser le même modèle de copilote pour **générer des rapports PDF de description d’image** en traitement par lots.  
* Expérimenter avec différents modèles OpenAI ou paramètres de température pour affiner le style de description.

N’hésitez pas à adapter le code, à tester avec des documents plus volumineux, et à intégrer la sortie dans votre pipeline d’indexation. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un PDF avec image balisée en Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Créer un PDF avec image balisée](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Créer une image PDF balisée Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}