---
category: general
date: 2026-04-25
description: Itere coleções em C# rapidamente com um exemplo claro de loop foreach.
  Aprenda como obter nomes de objetos e exibir uma lista de strings em apenas alguns
  passos.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: pt
og_description: Itere uma coleção C# usando um exemplo de loop foreach. Descubra como
  obter nomes de objetos e exibir uma lista de strings de forma eficiente.
og_title: Iterar Coleção C# – Loop passo a passo sobre itens
tags:
- C#
- collections
- loops
title: Iterar Coleção C# – Guia Simples para Percorrer Itens
url: /pt/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterar Coleção C# – Como Percorrer Itens com um Exemplo de Loop Foreach

Já precisou **iterate collection C#** mas não tinha certeza de qual construção oferece o código mais limpo? Você não está sozinho. Em muitos projetos acabamos escrevendo loops `for` verbosos apenas para imprimir algumas strings—perdendo tempo e legibilidade. A boa notícia? Um único loop `foreach` pode extrair cada nome de um objeto e **display string list** em segundos.

Neste tutorial, percorreremos um exemplo completo e executável que mostra como **get object names**, percorrer itens e enviá‑los para o console. Ao final, você terá um trecho autocontido que pode inserir em qualquer aplicativo console .NET 6+, além de algumas dicas para casos extremos e desempenho.

> **Dica profissional:** Se você estiver trabalhando com coleções grandes, considere usar `Parallel.ForEach`—mas esse é um tópico para outro dia.

---

## O que você aprenderá

- Como recuperar uma coleção de nomes de um objeto (`GetSignatureNames` em nosso exemplo)
- A sintaxe e nuances de um **foreach loop example** em C#
- Maneiras de **display string list** no console, incluindo truques de formatação
- Armadilhas comuns ao percorrer itens (coleções nulas, resultados vazios)
- Um programa completo, pronto para copiar e colar, que você pode executar instantaneamente

Nenhuma biblioteca externa é necessária; apenas a biblioteca de classes base que vem com o .NET. Se você tem o .NET SDK instalado, está pronto para começar.

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Etapa 1: Configurar o Objeto de Exemplo

Primeiro de tudo — precisamos de um objeto que possa retornar uma coleção de nomes. Imagine que você tem uma classe `Signature` que contém várias assinaturas; cada assinatura tem uma propriedade `Name`. O método `GetSignatureNames` simplesmente extrai esses nomes para um `IEnumerable<string>`.

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

**Por que isso importa:** Ao retornar `IEnumerable<string>` mantemos o método flexível — os chamadores podem enumerar, consultar ou converter o resultado sem copiar a lista subjacente. Isso também facilita **loop over items** posteriormente.

---

## Etapa 2: Escrever o Loop Foreach para Exibir a Lista de Strings

Agora que temos uma fonte de nomes, vamos realmente **iterate collection C#**. O construtor `foreach` extrai automaticamente cada elemento do enumerável, então não precisamos gerenciar uma variável de índice.

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

**Explicação do código:**

1. **Instanciar** `Signature` – agora você tem um objeto que conhece seus próprios nomes.
2. **Recuperar** a coleção via `GetSignatureNames()` – este é o passo de **get object names**.
3. **Exemplo de loop foreach** – `foreach (var name in signatureNames)` itera automaticamente sobre cada string.
4. **Exibir** cada `name` com `Console.WriteLine` – a forma clássica de **display string list** em um aplicativo console.

Como `signatureNames` implementa `IEnumerable<string>`, o loop `foreach` funciona imediatamente, lidando com o enumerador nos bastidores. Não há necessidade de se preocupar com erros de deslocamento ou verificações de limites manuais.

---

## Etapa 3: Executar o Programa e Verificar a Saída

Compile e execute o programa (por exemplo, `dotnet run` na pasta do projeto). Você deverá ver:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Se nada for impresso, verifique se `GetSignatureNames` não está retornando `null`. Uma verificação defensiva rápida pode evitar dores de cabeça:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Agora o loop lidará graciosamente com uma coleção ausente e simplesmente não exibirá nada ao invés de lançar uma `NullReferenceException`.

---

## Etapa 4: Variações Comuns e Casos Limítrofes

### 4.1 Percorrendo uma Lista de Objetos Complexos

Frequentemente você não lidará com strings simples, mas com objetos que contêm várias propriedades. Nesse caso, ainda pode **loop over items** e decidir o que exibir:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Aqui usamos interpolação de strings para combinar campos — ainda um loop `foreach`, apenas com uma saída mais rica.

### 4.2 Saída Antecipada com `break`

Se você precisar apenas do primeiro nome correspondente, saia do loop com `break`:

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

### 4.3 Enumeração Paralela (Avançado)

Quando a coleção é enorme e cada iteração consome muita CPU, `Parallel.ForEach` pode acelerar as coisas:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Lembre‑se, `Console.WriteLine` por si só é thread‑safe, mas a ordem da saída será não determinística.

---

## Etapa 5: Dicas para Loops Limpos e Manuteníveis

- **Prefira `foreach` ao invés de `for`** quando você não precisar de um índice; isso reduz bugs de deslocamento.
- **Use `IEnumerable<T>`** nas assinaturas de método para manter as APIs flexíveis.
- **Proteja contra coleções nulas** usando o operador de coalescência nula (`??`).
- **Mantenha o corpo do loop pequeno** — se você se pegar escrevendo muitas linhas, extraia um método.
- **Evite modificar a coleção** enquanto itera; isso lança uma `InvalidOperationException`.

---

## Conclusão

Acabamos de demonstrar como **iterate collection C#** usando um **foreach loop example** limpo, recuperar **object names** e **display string list** no console. O programa completo — definição do objeto, recuperação e iteração — funciona como está, fornecendo uma base sólida para qualquer cenário onde você precise percorrer itens.

A partir daqui você pode explorar:

- Filtragem com LINQ antes de percorrer (`signatureNames.Where(n => n.Contains("a"))`)
- Escrever a saída em um arquivo ao invés do console
- Usar `IAsyncEnumerable<T>` para fluxos assíncronos

Experimente isso, e você verá quão versátil o construtor `foreach` realmente é. Tem perguntas sobre casos limites ou desempenho? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}