---
category: general
date: 2026-03-06
description: Crie documentos PDF em C# e adicione números de Bates facilmente. Aprenda
  como adicionar uma página em branco ao PDF, colocar um selo na página e implementar
  a numeração de Bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: pt
og_description: Criar documento PDF em C# e adicionar numeração Bates. Este guia mostra
  como adicionar página em branco ao PDF, colocar selo na página e aplicar numeração
  Bates.
og_title: Criar documento PDF com numeração Bates – Tutorial C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Criar documento PDF com numeração Bates em C# – Guia completo
url: /pt/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF com Numeração Bates em C#

Já precisou **criar um documento PDF** em C# e se perguntou como adicionar uma numeração Bates sem perder a cabeça? Você não está sozinho — escritórios de advocacia, tribunais e até algumas equipes de compliance corporativo enfrentam esse mesmo desafio todos os dias. A boa notícia? Com algumas linhas de código Aspose.Pdf você pode gerar um PDF novinho, acrescentar uma página em branco e inserir a numeração Bates de forma fluida.

Neste tutorial vamos percorrer todo o processo: desde a configuração do projeto, passando pela adição de uma página em branco ao PDF, até descobrir **como adicionar numeração Bates**, e finalmente **colocar o selo na página** e salvar o resultado. Ao final, você terá um trecho pronto para uso que pode ser inserido em qualquer aplicação .NET. Sem referências vagas, apenas um exemplo completo e executável.

## O que você vai precisar

- **.NET 6+** (ou .NET Framework 4.6+ – Aspose.Pdf funciona com ambos)
- **Aspose.Pdf for .NET** pacote NuGet (`Install-Package Aspose.Pdf`)
- Uma IDE decente (Visual Studio, Rider ou VS Code com extensão C#)

É só isso. Sem DLLs extras, sem serviços externos. Vamos lá.

## Etapa 1: Criar Documento PDF – Configuração Inicial

Primeiro de tudo, precisamos de um objeto `Document` novo. Pense nele como a tela vazia onde tudo mais será inserido.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Por que isso importa:** A classe `Document` é o ponto de entrada para toda operação do Aspose. Instanciá‑la dá acesso à coleção `Pages`, metadados e configurações de segurança — todos os blocos de construção para um PDF profissional.

## Etapa 2: Adicionar Página em Branco ao PDF

Um PDF sem páginas é como um livro sem folhas — praticamente inútil. Inserir uma página em branco é simples e nos fornece uma superfície para carimbar a numeração Bates.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Dica de especialista:** Se precisar de várias páginas, basta chamar `pdfDocument.Pages.Add()` dentro de um loop. Cada chamada retorna um objeto `Page` novo que pode ser customizado de forma independente.

## Etapa 3: Como Adicionar Numeração Bates – Criar o TextStamp

Agora vem a parte central: a **numeração Bates**. No Aspose.Pdf ela é apenas um `TextStamp` com uma flag de artefato especial.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Por que definimos `Artifact`**: Alguns leitores de PDF expõem números Bates como metadados pesquisáveis. Marcar o selo como um artefato `BatesNumbering` garante que ferramentas subsequentes o reconheçam automaticamente.

## Etapa 4: Colocar o Selo na Página

Com o selo pronto, agora **colocamos o selo na página**. É nesta etapa que o número visual aparece no PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Caso extremo:** Se precisar que o número incremente em cada página, faça um loop sobre `pdfDocument.Pages` e atualize `batesStamp.Value` antes de chamar `AddStamp`. O exemplo aqui mantém a simplicidade com um “Bates‑001” estático.

## Etapa 5: Salvar e Verificar o Resultado

Por fim, persistimos o PDF no disco. Escolha uma pasta onde você tenha permissão de escrita; caso contrário, ocorrerá um `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Ao abrir `BatesStamped.pdf` em qualquer visualizador, você deverá ver um pequeno “Bates‑001” discretamente posicionado no canto inferior direito da página em branco.

> **Saída esperada:**  
> ![PDF com selo de número Bates](image-placeholder.png "PDF com selo de número Bates")  
> *Texto alternativo: PDF com selo de número Bates no canto inferior direito.*

Se o número não aparecer, verifique os valores de margem e assegure‑se de que o tamanho da página não está muito pequeno (o padrão A4 funciona bem). Também confirme que a flag `Artifact` não está sendo removida por ferramentas de pós‑processamento.

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para copiar e colar. Ele inclui todas as diretivas `using` e comentários para mantê‑lo orientado.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Execute o programa, abra o PDF e você verá a numeração Bates exatamente onde indicamos. 🎉

## Variações Comuns & Armadilhas

| Cenário | O que mudar | Por quê |
|----------|----------------|-----|
| **Múltiplas páginas, números incrementais** | Percorrer `pdfDocument.Pages`, definir `batesStamp.Value = $"Bates-{i:D3}"` antes de `AddStamp` | Fornece a cada página um identificador único, típico para pacotes jurídicos |
| **Posicionamento diferente (canto superior esquerdo)** | Alterar `HorizontalAlignment = HorizontalAlignment.Left` e `VerticalAlignment = VerticalAlignment.Top` | Algumas organizações preferem o número no cabeçalho em vez do rodapé |
| **Fonte ou cor personalizada** | Definir `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Melhora a legibilidade ou atende a diretrizes de marca |
| **Adicionar um PDF existente como fundo** | Carregar o PDF fonte com `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Útil quando é necessário carimbar sobre um formulário pré‑gerado |

## Conclusão

Acabamos de mostrar como **criar documento PDF**, **adicionar página em branco ao PDF**, e **inserir número Bates** usando Aspose.Pdf para .NET, depois **colocar o selo na página** e salvar o arquivo. O código foi mantido deliberadamente compacto para que você possa adaptá‑lo a fluxos de trabalho maiores — seja processando dezenas de arquivos ou integrando a um serviço web.

Se estiver pronto para avançar, considere:

- Automatizar a lógica de incremento para grandes volumes de processos.
- Incorporar a geração de PDF em uma API ASP.NET Core.
- Adicionar segurança (proteção por senha) com `pdfDocument.Encrypt(...)`.

Sinta‑se à vontade para experimentar, quebrar coisas e fazer perguntas nos comentários. Boa codificação, e que seus PDFs estejam sempre perfeitamente carimbados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}