---
category: general
date: 2026-04-25
description: Itera rapidamente una collezione C# con un chiaro esempio di ciclo foreach.
  Scopri come ottenere i nomi degli oggetti e visualizzare una lista di stringhe in
  pochi passaggi.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: it
og_description: Itera una collezione C# usando un esempio di ciclo foreach. Scopri
  come ottenere i nomi degli oggetti e visualizzare una lista di stringhe in modo
  efficiente.
og_title: Iterare una collezione C# – Ciclo passo passo sugli elementi
tags:
- C#
- collections
- loops
title: Iterare una collezione C# – Guida semplice per scorrere gli elementi
url: /it/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterare una Collezione C# – Come Scorrere gli Elementi con un Esempio di Loop Foreach

Ti è mai capitato di dover **iterare una collezione C#** ma non eri sicuro quale costrutto ti fornisse il codice più pulito? Non sei il solo. In molti progetti finiamo per scrivere loop `for` prolissi solo per stampare qualche stringa—perdendo tempo e leggibilità. La buona notizia? Un singolo loop `foreach` può estrarre ogni nome da un oggetto e **visualizzare una lista di stringhe** in pochi secondi.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra come **ottenere i nomi degli oggetti**, scorrere gli elementi e stamparli sulla console. Alla fine avrai uno snippet autonomo che potrai inserire in qualsiasi applicazione console .NET 6+, oltre a una serie di consigli per casi limite e prestazioni.

> **Consiglio professionale:** Se lavori con collezioni di grandi dimensioni, considera l'uso di `Parallel.ForEach`—ma questo è un argomento per un altro giorno.

---

## Cosa Imparerai

- Come recuperare una collezione di nomi da un oggetto (`GetSignatureNames` nel nostro esempio)
- La sintassi e le sfumature di un **esempio di loop foreach** in C#
- Modi per **visualizzare una lista di stringhe** nella console, includendo trucchi di formattazione
- Errori comuni quando si scorre gli elementi (collezioni null, risultati vuoti)
- Un programma completo, pronto per il copia‑incolla, che puoi eseguire immediatamente

Nessuna libreria esterna è richiesta; basta la base class library fornita con .NET. Se hai installato il .NET SDK, sei pronto per partire.

![Diagramma di iterazione della collezione C# che mostra una lista che fluisce in un loop foreach e poi nella console](/images/iterate-collection-csharp.png "diagramma di iterazione della collezione c#")

---

## Passo 1: Configurare l'Oggetto di Esempio

Prima di tutto—abbiamo bisogno di un oggetto che possa restituire una collezione di nomi. Immagina di avere una classe `Signature` che contiene diverse firme; ogni firma ha una proprietà `Name`. Il metodo `GetSignatureNames` estrae semplicemente quei nomi in un `IEnumerable<string>`.

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

**Perché è importante:** Restituendo `IEnumerable<string>` manteniamo il metodo flessibile—i chiamanti possono enumerare, interrogare o convertire il risultato senza copiare la lista sottostante. Inoltre rende facile **scorrere gli elementi** in seguito.

---

## Passo 2: Scrivere il Loop Foreach per Visualizzare la Lista di Stringhe

Ora che abbiamo una fonte di nomi, procediamo a **iterare una collezione C#**. Il costrutto `foreach` estrae automaticamente ogni elemento dall'enumerabile, così non dobbiamo gestire una variabile indice.

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

**Spiegazione del codice:**

1. **Instanziare** `Signature` – ora hai un oggetto che conosce i propri nomi.
2. **Recuperare** la collezione tramite `GetSignatureNames()` – questo è il passo di **ottenere i nomi degli oggetti**.
3. **Esempio di loop foreach** – `foreach (var name in signatureNames)` itera automaticamente su ogni stringa.
4. **Visualizzare** ogni `name` con `Console.WriteLine` – il modo classico per **visualizzare una lista di stringhe** in un'app console.

Poiché `signatureNames` implementa `IEnumerable<string>`, il loop `foreach` funziona subito, gestendo l'enumeratore dietro le quinte. Non c'è bisogno di preoccuparsi di errori di off‑by‑one o di controlli manuali dei limiti.

---

## Passo 3: Eseguire il Programma e Verificare l'Uscita

Compila ed esegui il programma (ad es., `dotnet run` dalla cartella del progetto). Dovresti vedere:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Se non viene stampato nulla, verifica che `GetSignatureNames` non restituisca `null`. Una difesa rapida può salvarti da problemi:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Ora il loop gestirà elegantemente una collezione mancante e semplicemente non stamperà nulla invece di lanciare una `NullReferenceException`.

---

## Passo 4: Variazioni Comuni e Casi Limite

### 4.1 Scorrere una Lista di Oggetti Complessi

Spesso non si lavora con semplici stringhe ma con oggetti che contengono più proprietà. In tal caso puoi comunque **scorrere gli elementi** e decidere cosa visualizzare:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Qui usiamo l'interpolazione di stringhe per combinare i campi—ancora un loop `foreach`, ma con un output più ricco.

### 4.2 Uscita Anticipata con `break`

Se ti serve solo il primo nome corrispondente, esci dal loop con `break`:

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

### 4.3 Enumerazione Parallela (Avanzato)

Quando la collezione è enorme e ogni iterazione è intensiva per la CPU, `Parallel.ForEach` può accelerare le cose:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Ricorda, `Console.WriteLine` è thread‑safe ma l'ordine di output sarà non deterministico.

---

## Passo 5: Consigli per Loop Puliti e Manutenibili

- **Preferisci `foreach` rispetto a `for`** quando non ti serve un indice; riduce gli errori off‑by‑one.
- **Usa `IEnumerable<T>`** nelle firme dei metodi per mantenere le API flessibili.
- **Proteggi dalle collezioni null** usando l'operatore di coalescenza null (`??`).
- **Mantieni il corpo del loop piccolo**—se ti trovi a scrivere molte righe, estrai un metodo.
- **Evita di modificare la collezione** durante l'iterazione; genera un `InvalidOperationException`.

---

## Conclusione

Abbiamo appena dimostrato come **iterare una collezione C#** usando un pulito **esempio di loop foreach**, recuperare **i nomi degli oggetti** e **visualizzare una lista di stringhe** nella console. Il programma completo—definizione dell'oggetto, recupero e iterazione—funziona così com'è, fornendoti una solida base per qualsiasi scenario in cui devi scorrere gli elementi.

Da qui potresti esplorare:

- Filtrare con LINQ prima del loop (`signatureNames.Where(n => n.Contains("a"))`)
- Scrivere l'output su un file invece che sulla console
- Usare `IAsyncEnumerable<T>` per stream asincroni

Provali e vedrai quanto sia versatile il costrutto `foreach`. Hai domande su casi limite o prestazioni? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}