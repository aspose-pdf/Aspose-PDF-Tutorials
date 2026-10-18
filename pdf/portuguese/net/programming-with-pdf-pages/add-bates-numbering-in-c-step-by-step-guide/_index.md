---
category: general
date: 2026-03-27
description: Adicione numeração Bates em C# rapidamente. Aprenda como adicionar números
  de página personalizados, números de página sequenciais e números personalizados
  a documentos Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: pt
og_description: Adicione numeração Bates em C# com um exemplo claro. Este guia mostra
  como adicionar números de página personalizados, adicionar números de página sequenciais
  e muito mais.
og_title: Adicionar numeração Bates em C# – Tutorial completo
tags:
- C#
- Document Processing
- Bates Numbering
title: Adicionar numeração Bates em C# – Guia passo a passo
url: /pt/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates em C# – Guia Passo a Passo

Já se perguntou como **add bates numbering** a um documento Word sem perder a cabeça? Você não está sozinho. Em muitos projetos jurídicos ou de conformidade, cada página precisa de um identificador único, e fazer isso manualmente é um pesadelo.  

Neste tutorial vamos percorrer um exemplo completo e executável que **adds bates numbering**, mostra como **how to add bates** em poucas linhas, e ainda cobre como **add custom page numbers** e **add sequential page numbers** quando precisar. Ao final, você terá um arquivo .docx marcado com os números que escolher — sem necessidade de ferramentas de terceiros.

## O que você aprenderá

- Carregar um arquivo DOCX com a API Aspose.Words for .NET (ou qualquer biblioteca compatível).  
- Configurar **add custom numbers** como um prefixo, um valor inicial e um tamanho de fonte.  
- Aplicar a numeração a cada página em uma única chamada.  
- Salvar o resultado e verificar se os números aparecem como esperado.  

Nenhuma experiência prévia com Bates numbering é necessária; apenas uma configuração básica de C# e uma cópia do documento fonte. Vamos mergulhar.

## Pré-requisitos

- .NET 6+ (o código funciona tanto no .NET Core quanto no .NET Framework).  
- Aspose.Words for .NET instalado via NuGet (`Install-Package Aspose.Words`).  
- Um documento Word chamado `input.docx` colocado em uma pasta que você pode referenciar (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code ou qualquer IDE C# de sua preferência.

> **Dica profissional:** Se você estiver usando uma biblioteca diferente (por exemplo, Open XML SDK), os conceitos permanecem os mesmos — basta trocar as chamadas da API.

## Etapa 1: Carregar o Documento Fonte

Primeiro, precisamos trazer o arquivo Word para a memória.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Por que isso importa:* Carregar o arquivo cria um objeto `Document` que dá acesso a páginas, seções e à árvore de nós de baixo nível. Sem ele, você não pode anexar nenhuma numeração.

## Etapa 2: Configurar as Opções de Numeração Bates

Agora definimos exatamente como os números devem aparecer. É aqui que você **add custom page numbers** ou **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Por que isso importa:* O `Prefix` permite que você **add custom numbers** como um ID de caso, enquanto `Start` determina o contador inicial. Alterar `FontSize` garante que os números não invadam as margens da página.

## Etapa 3: Aplicar a Numeração Bates a Cada Página

Com as opções prontas, instruímos a biblioteca a marcar cada página.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Por que isso importa:* O método `AddBatesNumbering` percorre a coleção interna de páginas e injeta uma caixa de texto no canto inferior‑direito (local padrão). É o núcleo de **how to add bates** sem precisar escrever um loop manualmente.

## Etapa 4: Salvar o Documento Atualizado

Finalmente, gravamos o arquivo modificado de volta ao disco.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Por que isso importa:* Salvar cria um novo `output.docx` que você pode abrir no Word, LibreOffice ou qualquer visualizador para confirmar que os números aparecem.

## Resultado Esperado

Abra `output.docx`. Cada página deve exibir algo como:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Se você abrir a visualização de impressão do documento, verá os números no canto inferior‑direito, correspondendo ao tamanho de fonte que definiu.

## Casos Limite e Variações

| Situação | O que mudar | Por quê |
|-----------|----------------|-----|
| **Nenhum prefixo necessário** | `Prefix = string.Empty` | Remove a parte “ABC‑”, deixando apenas a sequência numérica. |
| **Iniciar em 1** | `Start = 1` | Útil para **add sequential page numbers** simples sem um prefixo customizado. |
| **Documentos grandes (>10.000 páginas)** | Aumente `FontSize` ou ajuste `Location` (use sobrecargas de `AddBatesNumbering`) | Evita sobreposição com rodapés ou cabeçalhos. |
| **Arquivo fonte somente leitura** | Abra com `LoadOptions` que permitam acesso de escrita, ou copie o arquivo primeiro | Caso contrário, `document.Save` lançará uma exceção. |
| **Posicionamento diferente** | Use `batesOptions.Position = BatesNumberingPosition.TopLeft` (ou outro enum) | Algumas empresas exigem números no topo da página. |

> **Nota:** Nem todas as bibliotecas expõem uma classe `BatesNumberingOptions`. Com o Open XML SDK você inseriria um `TextBox` manualmente — mesmo princípio, mais código.

## Exemplo Completo Funcional

Aqui está o programa completo em um só lugar. Copie‑e‑cole em um aplicativo console e execute.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Execute o programa, abra `output.docx` e você verá a numeração exatamente onde esperava. 🎉

## Perguntas Frequentes

**Q: Posso mudar a cor dos números?**  
A: Sim. Após chamar `AddBatesNumbering`, você pode recuperar os objetos `Shape` gerados e definir a propriedade `FillColor`.

**Q: E se eu precisar dos números no lado esquerdo em vez do direito?**  
A: Use `batesOptions.Position = BatesNumberingPosition.BottomLeft` (ou `TopLeft`, `TopRight`). A API suporta os quatro cantos.

**Q: Isso funciona com saída PDF?**  
A: Absolutamente. Após adicionar a numeração, chame `document.Save("output.pdf")`. Os números são renderizados no PDF assim como no Word.

## Conclusão

Agora você sabe **how to add bates numbering** a um arquivo Word usando C#. O tutorial abordou carregar um documento, configurar **add custom numbers**, aplicar **add sequential page numbers** e salvar o resultado final. Com o exemplo completo de código, você pode inserir isso em qualquer projeto e começar a marcar documentos instantaneamente.

Pronto para o próximo desafio? Tente combinar isso com um processador em lote que percorra uma pasta de arquivos, ou explore **add custom page numbers** no cabeçalho/rodapé para um visual mais refinado. De qualquer forma, você tem uma base sólida para qualquer tarefa de legal‑tech ou automação de conformidade.

Tem perguntas ou um caso de uso interessante? Deixe um comentário abaixo e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}