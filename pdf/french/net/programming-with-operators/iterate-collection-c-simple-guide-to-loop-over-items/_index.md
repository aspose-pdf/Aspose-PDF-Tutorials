---
category: general
date: 2026-04-25
description: Itérez une collection C# rapidement avec un exemple clair de boucle foreach.
  Apprenez à obtenir les noms d’objets et à afficher une liste de chaînes en quelques
  étapes seulement.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: fr
og_description: Itérez une collection C# avec un exemple de boucle foreach. Découvrez
  comment obtenir les noms d’objets et afficher une liste de chaînes efficacement.
og_title: Itérer une collection C# – Boucle pas à pas sur les éléments
tags:
- C#
- collections
- loops
title: Itérer une collection C# – Guide simple pour parcourir les éléments
url: /fr/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Itérer une collection C# – Comment parcourir des éléments avec un exemple de boucle foreach

Vous avez déjà eu besoin d'**itérer une collection C#** sans savoir quel construit vous donne le code le plus propre ? Vous n'êtes pas seul. Dans de nombreux projets, nous finissons par écrire des boucles `for` verbeuses juste pour afficher quelques chaînes — perdant du temps et de la lisibilité. La bonne nouvelle ? Une seule boucle `foreach` peut extraire chaque nom d'un objet et **afficher une liste de chaînes** en quelques secondes.

Dans ce tutoriel, nous passerons en revue un exemple complet et exécutable qui montre comment **obtenir les noms d'objets**, parcourir les éléments et les afficher dans la console. À la fin, vous disposerez d'un extrait autonome que vous pourrez coller dans n'importe quelle application console .NET 6+, ainsi que de quelques astuces pour les cas limites et les performances.

> **Pro tip :** Si vous travaillez avec de très grandes collections, envisagez d'utiliser `Parallel.ForEach` — mais c'est un sujet pour une autre fois.

---

## Ce que vous allez apprendre

- Comment récupérer une collection de noms à partir d'un objet (`GetSignatureNames` dans notre exemple)
- La syntaxe et les subtilités d'un **exemple de boucle foreach** en C#
- Les différentes façons **d'afficher une liste de chaînes** dans la console, y compris des astuces de formatage
- Les pièges courants lors du parcours d'éléments (collections nulles, résultats vides)
- Un programme complet, prêt à copier‑coller, que vous pouvez exécuter immédiatement

Aucune bibliothèque externe n'est requise ; seule la bibliothèque de classes de base fournie avec .NET. Si le SDK .NET est installé, vous êtes prêt à partir.

---

![Diagramme d'itération d'une collection C# montrant une liste qui s'écoule vers une boucle foreach puis vers la console](/images/iterate-collection-csharp.png "diagramme d'itération d'une collection c#")

---

## Étape 1 : Configurer l'objet d'exemple

Tout d'abord, nous avons besoin d'un objet capable de renvoyer une collection de noms. Imaginez que vous avez une classe `Signature` qui contient plusieurs signatures ; chaque signature possède une propriété `Name`. La méthode `GetSignatureNames` extrait simplement ces noms dans un `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Pourquoi c'est important :** En renvoyant un `IEnumerable<string>`, nous gardons la méthode flexible — les appelants peuvent énumérer, interroger ou convertir le résultat sans copier la liste sous‑jacente. Cela facilite également **le parcours des éléments** ultérieurement.

---

## Étape 2 : Écrire la boucle foreach pour afficher la liste de chaînes

Maintenant que nous disposons d'une source de noms, **itérons la collection C#**. Le construit `foreach` extrait automatiquement chaque élément de l'énumérable, nous évitant de gérer une variable d'index.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Explication du code :**

1. **Instancier** `Signature` – vous avez maintenant un objet qui connaît ses propres noms.
2. **Récupérer** la collection via `GetSignatureNames()` – c'est l'étape **obtenir les noms d'objets**.
3. **Exemple de boucle foreach** – `foreach (var name in signatureNames)` itère automatiquement sur chaque chaîne.
4. **Afficher** chaque `name` avec `Console.WriteLine` – la façon classique **d'afficher une liste de chaînes** dans une application console.

Comme `signatureNames` implémente `IEnumerable<string>`, la boucle `foreach` fonctionne immédiatement, gérant l'énumérateur en interne. Pas besoin de se soucier des erreurs d'index ou de vérifications de limites manuelles.

---

## Étape 3 : Exécuter le programme et vérifier la sortie

Compilez et exécutez le programme (par ex. `dotnet run` depuis le dossier du projet). Vous devriez voir :

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Si rien n'est affiché, vérifiez que `GetSignatureNames` ne renvoie pas `null`. Une petite protection défensive peut vous éviter des maux de tête :

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Désormais, la boucle gérera gracieusement une collection manquante et n'affichera rien au lieu de lever une `NullReferenceException`.

---

## Étape 4 : Variations courantes & cas limites

### 4.1 Parcourir une liste d'objets complexes

Souvent, vous ne traiterez pas de simples chaînes mais des objets contenant plusieurs propriétés. Dans ce cas, vous pouvez toujours **parcourir les éléments** et choisir ce que vous affichez :

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Ici, nous utilisons l'interpolation de chaînes pour combiner les champs — toujours une boucle `foreach`, mais avec une sortie plus riche.

### 4.2 Sortie anticipée avec `break`

Si vous ne avez besoin que du premier nom correspondant, sortez de la boucle :

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Énumération parallèle (avancé)

Lorsque la collection est énorme et que chaque itération est gourmande en CPU, `Parallel.ForEach` peut accélérer les choses :

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Rappelez‑vous que `Console.WriteLine` est thread‑safe, mais l'ordre de sortie sera non déterministe.

---

## Étape 5 : Conseils pour des boucles propres et maintenables

- **Privilégiez `foreach` à `for`** lorsque vous n'avez pas besoin d'un indice ; cela réduit les bugs d'index.
- **Utilisez `IEnumerable<T>`** dans les signatures de méthodes pour garder les API flexibles.
- **Protégez-vous contre les collections nulles** avec l'opérateur de coalescence nulle (`??`).
- **Gardez le corps de la boucle petit** — si vous vous retrouvez à écrire plusieurs lignes, extrayez une méthode.
- **Évitez de modifier la collection** pendant l'itération ; cela déclenche une `InvalidOperationException`.

---

## Conclusion

Nous venons de montrer comment **itérer une collection C#** en utilisant un **exemple de boucle foreach** propre, récupérer les **noms d'objets** et **afficher une liste de chaînes** dans la console. Le programme complet — définition d'objet, récupération et itération—fonctionne tel quel, vous offrant une base solide pour tout scénario où vous devez parcourir des éléments.

À partir d'ici, vous pouvez explorer :

- Le filtrage avec LINQ avant la boucle (`signatureNames.Where(n => n.Contains("a"))`)
- L'écriture de la sortie dans un fichier au lieu de la console
- L'utilisation de `IAsyncEnumerable<T>` pour les flux asynchrones

Essayez ces pistes, et vous verrez à quel point le construct `foreach` est polyvalent. Des questions sur les cas limites ou les performances ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}