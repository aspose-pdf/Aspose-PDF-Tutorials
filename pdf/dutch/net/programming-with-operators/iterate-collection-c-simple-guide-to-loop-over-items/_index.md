---
category: general
date: 2026-04-25
description: Itereer collectie C# snel met een duidelijk foreach‑loop voorbeeld. Leer
  hoe je objectnamen kunt ophalen en een stringlijst kunt weergeven in slechts een
  paar stappen.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: nl
og_description: Itereer door een collectie in C# met een foreach-loop voorbeeld. Ontdek
  hoe je objectnamen kunt ophalen en een stringlijst efficiënt kunt weergeven.
og_title: Itereren over collectie C# – Stap‑voor‑stap door items loopen
tags:
- C#
- collections
- loops
title: Itereren over collectie C# – Eenvoudige gids voor het doorlopen van items
url: /nl/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – Hoe je Items Doorloopt met een Foreach‑Loop Voorbeeld

Heb je ooit **iterate collection C#** moeten doen, maar wist je niet welke constructie de netste code oplevert? Je bent niet de enige. In veel projecten schrijven we omslachtige `for`‑loops alleen maar om een paar strings af te drukken—tijdverspilling en minder leesbaarheid. Het goede nieuws? Eén enkele `foreach`‑loop kan elke naam uit een object halen en **display string list** in enkele seconden.

In deze tutorial lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat laat zien hoe je **object names** kunt ophalen, over items kunt itereren en ze naar de console kunt outputten. Aan het einde heb je een zelfstandige snippet die je in elke .NET 6+ console‑app kunt plakken, plus een aantal tips voor randgevallen en performance.

> **Pro tip:** Werk je met grote collecties, overweeg dan `Parallel.ForEach`—maar dat is een onderwerp voor een andere keer.

---

## Wat je gaat leren

- Hoe je een collectie namen uit een object haalt (`GetSignatureNames` in ons voorbeeld)
- De syntaxis en nuances van een **foreach loop example** in C#
- Manieren om **display string list** in de console te tonen, inclusief opmaaktrucs
- Veelvoorkomende valkuilen bij het itereren over items (null‑collecties, lege resultaten)
- Een volledig, kant‑klaar programma dat je direct kunt uitvoeren

Er zijn geen externe libraries nodig; alleen de basis‑class library die met .NET wordt meegeleverd. Als je de .NET SDK geïnstalleerd hebt, ben je klaar om te gaan.

---

![Diagram van collectie iteratie C# dat een lijst toont die in een foreach‑lus stroomt en vervolgens naar de console gaat](/images/iterate-collection-csharp.png "diagram van collectie iteratie c#")

---

## Stap 1: Het Voorbeeldobject Opzetten

Allereerst hebben we een object nodig dat een collectie namen kan teruggeven. Stel je voor dat je een `Signature`‑klasse hebt die meerdere handtekeningen bevat; elke handtekening heeft een `Name`‑eigenschap. De methode `GetSignatureNames` haalt die namen simpelweg uit en zet ze in een `IEnumerable<string>`.

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

**Waarom dit belangrijk is:** Door `IEnumerable<string>` terug te geven, houden we de methode flexibel—aanroepers kunnen enumereren, query‑en of het resultaat omzetten zonder de onderliggende lijst te kopiëren. Het maakt het later ook eenvoudig om **loop over items** uit te voeren.

---

## Stap 2: Schrijf de Foreach‑Loop om de String‑Lijst te Tonen

Nu we een bron van namen hebben, gaan we daadwerkelijk **iterate collection C#**. Het `foreach`‑construct haalt automatisch elk element uit de enumerable, zodat we geen indexvariabele hoeven te beheren.

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

**Uitleg van de code:**

1. **Instantiate** `Signature` – je hebt nu een object dat zijn eigen namen kent.
2. **Retrieve** de collectie via `GetSignatureNames()` – dit is de **get object names** stap.
3. **Foreach loop example** – `foreach (var name in signatureNames)` iterereert automatisch over elke string.
4. **Display** elke `name` met `Console.WriteLine` – de klassieke manier om **display string list** in een console‑app te doen.

Omdat `signatureNames` `IEnumerable<string>` implementeert, werkt de `foreach`‑loop direct, waarbij de enumerator achter de schermen wordt afgehandeld. Geen zorgen over off‑by‑one fouten of handmatige bounds‑checking.

---

## Stap 3: Voer het Programma uit en Controleer de Output

Compileer en voer het programma uit (bijv. `dotnet run` vanuit de projectmap). Je zou moeten zien:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Als er niets wordt afgedrukt, controleer dan of `GetSignatureNames` niet `null` retourneert. Een korte defensieve guard kan je veel hoofdpijn besparen:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Nu zal de loop netjes een ontbrekende collectie afhandelen en simpelweg niets outputten in plaats van een `NullReferenceException` te gooien.

---

## Stap 4: Veelvoorkomende Variaties & Randgevallen

### 4.1 Een Lijst van Complexe Objecten Itereren

Vaak werk je niet met eenvoudige strings maar met objecten die meerdere eigenschappen bevatten. In dat geval kun je nog steeds **loop over items** en bepalen wat je wilt tonen:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Hier gebruiken we string‑interpolatie om velden te combineren—nog steeds een `foreach`‑loop, alleen een rijkere output.

### 4.2 Vroegtijdig Stoppen met `break`

Als je alleen de eerste overeenkomende naam nodig hebt, kun je de loop verlaten:

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

### 4.3 Parallel Enumeratie (Geavanceerd)

Wanneer de collectie enorm is en elke iteratie CPU‑intensief, kan `Parallel.ForEach` de uitvoering versnellen:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Onthoud dat `Console.WriteLine` zelf thread‑safe is, maar de volgorde van de output nondeterministisch zal zijn.

---

## Stap 5: Tips voor Schone en Onderhoudbare Loops

- **Prefer `foreach` over `for`** wanneer je geen index nodig hebt; het vermindert off‑by‑one bugs.
- **Use `IEnumerable<T>`** in methodesignatures om APIs flexibel te houden.
- **Guard against null** collecties met de null‑coalescing operator (`??`).
- **Keep the loop body small**—als je veel regels moet schrijven, haal dan een methode uit.
- **Avoid modifying the collection** tijdens het itereren; dit veroorzaakt een `InvalidOperationException`.

---

## Conclusie

We hebben zojuist laten zien hoe je **iterate collection C#** kunt doen met een nette **foreach loop example**, **object names** kunt ophalen en **display string list** in de console. Het volledige programma—objectdefinitie, ophalen en iteratie—werkt direct, en biedt een solide basis voor elke situatie waarin je items moet doorlopen.

Van hieruit kun je verder gaan met:

- Filteren met LINQ vóór het itereren (`signatureNames.Where(n => n.Contains("a"))`)
- De output naar een bestand schrijven in plaats van naar de console
- `IAsyncEnumerable<T>` gebruiken voor asynchrone streams

Probeer die opties eens uit, en je zult zien hoe veelzijdig het `foreach`‑construct echt is. Vragen over randgevallen of performance? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}