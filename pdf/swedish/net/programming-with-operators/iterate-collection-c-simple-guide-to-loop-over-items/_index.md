---
category: general
date: 2026-04-25
description: Iterera en samling i C# snabbt med ett tydligt foreach‑loop‑exempel.
  Lär dig hur du får objektens namn och visar en stränglista på bara några steg.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: sv
og_description: Iterera en samling i C# med ett foreach-loop‑exempel. Upptäck hur
  du hämtar objektnamn och visar en stränglista effektivt.
og_title: Iterera samling C# – Steg‑för‑steg loopa över objekt
tags:
- C#
- collections
- loops
title: Iterera samling C# – En enkel guide för att loopa över objekt
url: /sv/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterera samling C# – Hur man loopar över objekt med ett foreach‑loopexempel

Har du någonsin behövt **iterera samling C#** men varit osäker på vilket konstruktion som ger den renaste koden? Du är inte ensam. I många projekt slutar vi med att skriva omständliga `for`‑loopar bara för att skriva ut några strängar—det slösar både tid och läsbarhet. Den goda nyheten? En enda `foreach`‑loop kan plocka ut varje namn från ett objekt och **visa stränglista** på några sekunder.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur man **hämtar objektnamn**, loopar över objekt och skriver ut dem till konsolen. När du är klar har du ett självständigt kodsnutt som du kan klistra in i vilken .NET 6+‑konsolapp som helst, plus ett antal tips för kantfall och prestanda.

> **Proffstips:** Om du arbetar med stora samlingar, överväg att använda `Parallel.ForEach`—men det är ett ämne för en annan dag.

---

## Vad du kommer att lära dig

- Hur man hämtar en samling namn från ett objekt (`GetSignatureNames` i vårt exempel)
- Syntaxen och nyanserna i ett **foreach‑loopexempel** i C#
- Sätt att **visa stränglista** i konsolen, inklusive formateringsknep
- Vanliga fallgropar när man loopar över objekt (null‑samlingar, tomma resultat)
- Ett komplett, kopiera‑och‑klistra‑klart program som du kan köra direkt

Inga externa bibliotek behövs; bara basbiblioteket som följer med .NET. Om du har .NET‑SDK:n installerad är du redo att köra.

---

![Iterera samling C# diagram som visar en lista som flödar in i en foreach‑loop och sedan till konsolen](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Steg 1: Skapa exempelobjektet

Först och främst—vi behöver ett objekt som kan returnera en samling namn. Föreställ dig att du har en `Signature`‑klass som innehåller flera signaturer; varje signatur har en `Name`‑egenskap. Metoden `GetSignatureNames` extraherar helt enkelt dessa namn till en `IEnumerable<string>`.

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

**Varför detta är viktigt:** Genom att returnera `IEnumerable<string>` håller vi metoden flexibel—anroparna kan enumerera, fråga eller konvertera resultatet utan att kopiera den underliggande listan. Det gör det också enkelt att **loopa över objekt** senare.

---

## Steg 2: Skriv foreach‑loopen för att visa stränglistan

Nu när vi har en källa av namn, låt oss faktiskt **iterera samling C#**. `foreach`‑konstruktionen drar automatiskt varje element från den enumererbara samlingen, så vi behöver inte hantera en indexvariabel.

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

**Förklaring av koden:**

1. **Instansiera** `Signature` – du har nu ett objekt som känner till sina egna namn.
2. **Hämta** samlingen via `GetSignatureNames()` – detta är steget **hämta objektnamn**.
3. **Foreach‑loopexempel** – `foreach (var name in signatureNames)` itererar automatiskt över varje sträng.
4. **Visa** varje `name` med `Console.WriteLine` – det klassiska sättet att **visa stränglista** i en konsolapp.

Eftersom `signatureNames` implementerar `IEnumerable<string>` fungerar `foreach`‑loopen direkt, och hanterar enumeratorn bakom kulisserna. Inga bekymmer kring off‑by‑one‑fel eller manuella gränskontroller.

---

## Steg 3: Kör programmet och verifiera utskriften

Kompilera och kör programmet (t.ex. `dotnet run` från projektmappen). Du bör se:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Om inget skrivs ut, dubbelkolla att `GetSignatureNames` inte returnerar `null`. Ett snabbt defensivt skydd kan rädda dig från huvudvärk:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Nu hanterar loopen elegant en eventuell saknad samling och skriver helt enkelt inget istället för att kasta ett `NullReferenceException`.

---

## Steg 4: Vanliga variationer & kantfall

### 4.1 Loopning över en lista med komplexa objekt

Ofta arbetar du inte med rena strängar utan med objekt som innehåller flera egenskaper. I så fall kan du fortfarande **loopa över objekt** och bestämma vad som ska visas:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Här använder vi stränginterpolering för att kombinera fält—fortfarande en `foreach`‑loop, bara med rikare output.

### 4.2 Tidig avbrytning med `break`

Om du bara behöver det första matchande namnet, bryt loopen:

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

### 4.3 Parallell enumeration (avancerat)

När samlingen är enorm och varje iteration är CPU‑intensiv kan `Parallel.ForEach` snabba upp processen:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Kom ihåg att `Console.WriteLine` i sig är trådsäker men utskriftsordningen blir icke‑deterministisk.

---

## Steg 5: Tips för rena och underhållbara loopar

- **Föredra `foreach` framför `for`** när du inte behöver ett index; det minskar risken för off‑by‑one‑buggar.
- **Använd `IEnumerable<T>`** i metodsignaturer för att hålla API:er flexibla.
- **Skydda mot null**‑samlingar med null‑koalesceringsoperatorn (`??`).
- **Håll loopkroppen liten**—om du skriver många rader, extrahera en metod.
- **Undvik att modifiera samlingen** medan du itererar; det kastar ett `InvalidOperationException`.

---

## Slutsats

Vi har just demonstrerat hur man **itererar samling C#** med ett rent **foreach‑loopexempel**, hämtar **objektnamn** och **visar stränglista** i konsolen. Det kompletta programmet—objektdefinition, hämtning och iteration—kör som det är, och ger dig en solid grund för alla scenarier där du behöver loopa över objekt.

Härnäst kan du utforska:

- Filtrering med LINQ innan loopning (`signatureNames.Where(n => n.Contains("a"))`)
- Skriva utdata till en fil istället för konsolen
- Använda `IAsyncEnumerable<T>` för asynkrona strömmar

Prova dessa, så ser du hur mångsidig `foreach`‑konstruktionen verkligen är. Har du frågor om kantfall eller prestanda? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}