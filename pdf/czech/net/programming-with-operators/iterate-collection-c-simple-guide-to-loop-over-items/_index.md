---
category: general
date: 2026-04-25
description: Rychle iterujte kolekci v C# pomocí přehledného příkladu smyčky foreach.
  Naučte se, jak získat názvy objektů a zobrazit seznam řetězců během několika kroků.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: cs
og_description: Iterujte kolekci v C# pomocí příkladu smyčky foreach. Objevte, jak
  získat názvy objektů a efektivně zobrazit seznam řetězců.
og_title: Iterace kolekce v C# – Krok za krokem procházet položky
tags:
- C#
- collections
- loops
title: Iterovat kolekci v C# – Jednoduchý průvodce procházením položek
url: /cs/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterovat kolekci C# – Jak procházet položky pomocí smyčky foreach

Už jste někdy potřebovali **iterate collection C#**, ale nebyli jste si jisti, který konstruktor vám poskytne nejčistší kód? Nejste v tom sami. V mnoha projektech končíme psaním podrobných `for` smyček jen kvůli vytištění několika řetězců—ztrácíme čas a čitelnost. Dobrá zpráva? Jedna `foreach` smyčka může vytáhnout každé jméno z objektu a **display string list** během několika sekund.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje, jak **get object names**, procházet položky a vypisovat je do konzole. Na konci budete mít samostatný úryvek, který můžete vložit do libovolné .NET 6+ konzolové aplikace, plus několik tipů pro okrajové případy a výkon.

> **Pro tip:** Pokud pracujete s velkými kolekcemi, zvažte použití `Parallel.ForEach`—ale to je téma na jiný den.

## Co se naučíte

- Jak získat kolekci jmen z objektu (`GetSignatureNames` v našem příkladu)
- Syntax a nuance **foreach loop example** v C#
- Způsoby, jak **display string list** v konzoli, včetně triků na formátování
- Běžné úskalí při procházení položek (null kolekce, prázdné výsledky)
- Úplný program připravený ke kopírování a vložení, který můžete spustit okamžitě

Nejsou vyžadovány žádné externí knihovny; stačí základní knihovna tříd, která je součástí .NET. Pokud máte nainstalovaný .NET SDK, můžete začít.

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

## Krok 1: Nastavte ukázkový objekt

Nejprve potřebujeme objekt, který dokáže vrátit kolekci jmen. Představte si, že máte třídu `Signature`, která obsahuje několik podpisů; každý podpis má vlastnost `Name`. Metoda `GetSignatureNames` jednoduše vytáhne tato jména do `IEnumerable<string>`.

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

**Proč je to důležité:** Vrácením `IEnumerable<string>` udržujeme metodu flexibilní—volající mohou enumerovat, dotazovat se nebo převést výsledek bez kopírování podkladového seznamu. Také to usnadňuje **loop over items** později.

## Krok 2: Napište smyčku foreach pro zobrazení seznamu řetězců

Nyní, když máme zdroj jmen, pojďme skutečně **iterate collection C#**. Konstrukce `foreach` automaticky získává každý prvek z enumerable, takže nemusíme spravovat proměnnou indexu.

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

**Vysvětlení kódu:**

1. **Instantiate** `Signature` – nyní máte objekt, který zná své vlastní názvy.
2. **Retrieve** kolekci pomocí `GetSignatureNames()` – to je krok **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` automaticky prochází každý řetězec.
4. **Display** každé `name` pomocí `Console.WriteLine` – klasický způsob, jak **display string list** v konzolové aplikaci.

Protože `signatureNames` implementuje `IEnumerable<string>`, smyčka `foreach` funguje hned z krabice a zajišťuje enumerátor v pozadí. Není třeba se obávat chyb o jeden index nebo ručního kontrolování hranic.

## Krok 3: Spusťte program a ověřte výstup

Přeložte a spusťte program (např. `dotnet run` ze složky projektu). Měli byste vidět:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Pokud se nic nevytištělo, zkontrolujte, že `GetSignatureNames` nevrací `null`. Rychlá obranná kontrola vám může ušetřit starosti:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Nyní smyčka elegantně zvládne chybějící kolekci a jednoduše nic nevypíše místo vyhození `NullReferenceException`.

## Krok 4: Běžné varianty a okrajové případy

### 4.1 Procházení seznamu složitých objektů

Často nebudete pracovat s prostými řetězci, ale s objekty, které obsahují více vlastností. V takovém případě můžete stále **loop over items** a rozhodnout, co zobrazit:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Zde používáme interpolaci řetězců k sloučení polí—stále `foreach` smyčka, jen s bohatším výstupem.

### 4.2 Předčasný odchod pomocí `break`

Pokud potřebujete jen první odpovídající jméno, přerušte smyčku:

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

### 4.3 Paralelní enumerace (pokročilé)

Když je kolekce obrovská a každá iterace je náročná na CPU, může `Parallel.ForEach` urychlit věci:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Pamatujte, že `Console.WriteLine` je samotné vlákny‑bezpečné, ale pořadí výstupu bude nedeterministické.

## Krok 5: Tipy pro čisté a udržovatelné smyčky

- **Prefer `foreach` over `for`** když nepotřebujete index; snižuje chyby o jeden.
- **Use `IEnumerable<T>`** v signaturách metod, aby API byla flexibilní.
- **Guard against null** kolekce pomocí operátoru null‑coalescing (`??`).
- **Keep the loop body small**—pokud zjistíte, že píšete mnoho řádků, vytáhněte metodu.
- **Avoid modifying the collection** během iterace; vyvolá `InvalidOperationException`.

## Závěr

Právě jsme ukázali, jak **iterate collection C#** pomocí čistého **foreach loop example**, získat **object names** a **display string list** v konzoli. Kompletní program—definice objektu, získání a iterace—běží tak, jak je, a poskytuje vám pevný základ pro jakýkoli scénář, kde potřebujete procházet položky.

Odtud můžete zkoumat:

- Filtrování pomocí LINQ před iterací (`signatureNames.Where(n => n.Contains("a"))`)
- Zapisování výstupu do souboru místo konzole
- Použití `IAsyncEnumerable<T>` pro asynchronní proudy

Vyzkoušejte je a uvidíte, jak všestranný je konstruktor `foreach`. Máte otázky ohledně okrajových případů nebo výkonu? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}