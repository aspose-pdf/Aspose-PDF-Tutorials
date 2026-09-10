---
category: general
date: 2026-02-25
description: tutorial de numeração Bates – aprenda como adicionar números de página
  em PDF e aplicar numeração Bates personalizada usando Aspose.Pdf em C#. Guia passo
  a passo com código completo.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: pt
og_description: O tutorial de numeração Bates mostra como adicionar números de página
  em PDF e numeração Bates personalizada em C#. Código completo, explicações e dicas.
og_title: Tutorial de numeração Bates – Adicione números Bates a PDFs com C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Tutorial de numeração Bates: adicionar números Bates a PDFs com C#'
url: /pt/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial de numeração Bates – Adicionando Números Bates a PDFs em C#

Já se perguntou como adicionar números de página a um PDF enquanto incorpora um número Bates no estilo jurídico? Você não está sozinho. Neste **tutorial de numeração Bates** vamos percorrer tudo o que você precisa saber para carimbar cada página de um PDF com um prefixo personalizado, zeros à esquerda e posicionamento preciso — usando Aspose.Pdf para .NET.

A boa notícia? É bem direto assim que você entende os conceitos principais. Ao final deste guia você terá um programa executável que recebe *input.pdf* e gera *bates_out.pdf* com um rótulo estilo “ABC‑01000” em cada página. Vamos lá.

## O que você vai precisar

- **Aspose.Pdf for .NET** (versão 23.10 ou posterior). A biblioteca é comercial, mas um trial gratuito funciona perfeitamente para aprendizado.
- SDK .NET 6+ (qualquer versão recente serve).
- Um ambiente básico de desenvolvimento C# — Visual Studio, VS Code ou Rider.
- Um PDF de entrada para experimentar (qualquer documento com várias páginas ilustrará o efeito).

Nenhum pacote NuGet extra além do Aspose.Pdf é necessário, e o código roda no Windows, Linux ou macOS sem modificações.

## Etapa 1: Carregar o Documento PDF de Origem (tutorial de numeração Bates – inicialização)

Primeiro criamos um objeto `Document` que representa o PDF que queremos modificar. Pense nele como carregar uma tela em branco na qual você pode desenhar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Por que isso importa:** Sem carregar o arquivo, não há nada para anotar. A verificação de sanidade impede uma falha silenciosa mais tarde quando você tenta adicionar artefatos a uma coleção de páginas inexistente.

## Etapa 2: Definir o Artefato de Numeração Bates (como adicionar bates)

Um *BatesNumberingArtifact* indica ao Aspose onde e como desenhar o identificador. Você pode controlar o prefixo, número inicial, preenchimento com zeros, tamanho da fonte e coordenadas X/Y exatas.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Por que isso importa:** A propriedade `LeadingZeros` garante que cada rótulo tenha o mesmo comprimento, o que é crucial em documentos legais onde o alinhamento importa. Ajuste `X` e `Y` para mover o carimbo para o canto superior‑direito, inferior‑esquerdo ou onde seu fluxo de trabalho exigir.

## Etapa 3: Anexar o Artefato a Cada Página (adicionar números de página pdf)

Agora percorremos cada página e anexamos o mesmo artefato. É aqui que o requisito de *adicionar números de página pdf* é atendido — cada página recebe seu próprio rótulo sequencial automaticamente.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Por que isso importa:** Ao adicionar o artefato à coleção `Artifacts` em vez de desenhar texto manualmente, deixamos o Aspose gerenciar a lógica de numeração, os zeros à esquerda e a renderização. Isso reduz bugs e mantém o código conciso.

## Etapa 4: Salvar o PDF Modificado (adicionar numeração bates)

Por fim, persistimos as alterações em um novo arquivo. É uma boa prática gravar com um nome diferente para manter o original intacto.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Por que isso importa:** O método `Save` grava todo o PDF, incorporando os artefatos como parte do fluxo de conteúdo da página. O arquivo resultante pode ser aberto em qualquer visualizador de PDF e exibirá os números Bates exatamente como especificado.

## Exemplo Completo Funcional (Todas as Etapas Combinadas)

Abaixo está o programa completo, pronto para ser executado. Copie‑e‑cole em um projeto de console, substitua os caminhos de placeholder e pressione **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Resultado Esperado

Abra *bates_out.pdf* no Adobe Reader, Foxit ou qualquer visualizador. Você deverá ver um rótulo como **ABC‑01000** na primeira página, **ABC‑01001** na segunda, e assim por diante, posicionado 50 pts da borda esquerda e 30 pts da borda inferior. Os números são alinhados à direita por causa dos zeros à esquerda, dando ao documento um aspecto limpo e profissional.

## Variações Comuns & Casos de Borda

| Cenário | Como Ajustar |
|----------|---------------|
| **Prefixo diferente** | Altere `Prefix = "XYZ"` na definição do artefato. |
| **Iniciar em número customizado** | Defina `Start = 5000` (ou qualquer inteiro). |
| **Posicionar o número no canto superior‑direito** | Use `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Alterar tamanho da fonte para documentos maiores** | Modifique `FontSize = 12` (ou qualquer tamanho). |
| **Adicionar um retângulo de fundo** | Crie um `RectangleArtifact` e adicione‑o antes do `BatesNumberingArtifact`. |
| **Pular determinadas páginas** | Dentro do laço `foreach`, adicione `if (page.Number % 2 == 0) continue;` para pular páginas pares. |

**Dica profissional:** Sempre teste primeiro com um PDF curto. É mais rápido verificar o posicionamento antes de executar o script em um arquivo de 200 páginas.

## Perguntas Frequentes

- **Isso funciona com PDFs criptografados?**  
  Aspose.Pdf pode abrir arquivos protegidos por senha se você fornecer a senha via `Document(string, string)`. O artefato Bates ainda será aplicado após a descriptografia.

- **Posso adicionar números Bates e números de página regulares?**  
  Sim. Adicione um `PageNumberArtifact` ao lado do `BatesNumberingArtifact`. Cada artefato mantém seu próprio contador.

- **E se meu PDF tiver tamanhos de página diferentes?**  
  Os valores de `Position` são pontos absolutos. Para documentos com tamanhos mistos, calcule a posição por página dentro do laço usando `page.PageInfo.Width` e `page.PageInfo.Height`.

## Próximos Passos & Tópicos Relacionados

Agora que você dominou o **tutorial de numeração Bates**, pode explorar:

- **Adicionar marcas d'água** – abordagem de artefato similar com `TextArtifact`.
- **Mesclar vários PDFs** – use `Document.AppendDocument`.
- **Extrair texto para indexação de busca** – classe `TextAbsorber`.
- **Automatizar processamento em lote** – percorrer uma pasta de PDFs e aplicar o mesmo artefato.

Todos esses tópicos se baseiam nos mesmos conceitos que você acabou de aprender, então você está bem posicionado para expandir seu kit de ferramentas de automação de PDFs.

---

*Feliz codificação! Se encontrar algum obstáculo ou tiver ideias para personalizações adicionais, sinta‑se à vontade para deixar um comentário abaixo. O mundo da manipulação de PDFs é vasto, mas com um sólido **tutorial de numeração Bates** na bagagem, você já está à frente da curva.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}