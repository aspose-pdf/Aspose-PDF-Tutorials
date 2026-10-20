---
category: general
date: 2026-07-20
description: Como adicionar numeração Bates a um PDF usando Aspose.Pdf. Aprenda a
  inserir números Bates em PDFs e a adicionar selo em cada página de forma rápida
  e confiável.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: pt
lastmod: 2026-07-20
og_description: Como adicionar numeração Bates a um PDF com Aspose.Pdf. Este guia
  mostra como adicionar números Bates ao PDF e carimbar cada página em apenas algumas
  linhas de C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Como adicionar numeração Bates em PDF – Tutorial completo do Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Como adicionar numeração Bates em PDF com Aspose – Guia passo a passo
url: /pt/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Adicionar Numeração Bates em PDF com Aspose – Guia Passo a Passo

Já se perguntou **como adicionar numeração bates** a um documento jurídico sem perder horas em uma interface gráfica? Você não está sozinho. Em muitos escritórios de advocacia, agências governamentais e até grandes empresas, carimbar cada página com um identificador único é uma tarefa diária — porém uma única linha de C# pode tornar isso muito simples.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente **como adicionar numeração bates** usando a biblioteca Aspose.Pdf. Ao final, você também saberá como **add bates numbers pdf** arquivos e **add stamp to each page** com apenas algumas linhas de código. Sem mágica, apenas raciocínio claro e dicas práticas.

## O que Você Vai Aprender

- Carregar um PDF existente com Aspose.Pdf.  
- Criar um `BatesNumberingStamp` e personalizar sua aparência.  
- Percorrer todas as páginas e **add stamp to each page** automaticamente.  
- Salvar o resultado como um novo PDF que contém um número Bates profissional em cada folha.

### Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
- Uma licença válida do Aspose.Pdf for .NET (ou uma chave de avaliação temporária).  
- Um arquivo PDF original que você deseja numerar (chamaremos de `Original.pdf`).

Se você atende a esses três itens, está pronto para começar.

---

## Etapa 1: Configurar Seu Projeto e Instalar Aspose.Pdf

Primeiro, crie um novo projeto de console (ou adicione o código a um já existente). Em seguida, instale o pacote NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **Dica profissional:** Se você estiver em uma rede corporativa, verifique se sua fonte NuGet está configurada para acessar `https://www.nuget.org`.

## Etapa 2: Carregar o Documento PDF de Origem

Carregar um PDF é tão simples quanto apontar o Aspose para o caminho do arquivo. A classe `Document` representa o arquivo inteiro.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Por que registramos a contagem de páginas? Porque a numeração Bates deve ser sequencial em *todas* as páginas, e é útil confirmar que você não carregou acidentalmente um arquivo diferente.

## Etapa 3: Criar um Selo de Numeração Bates

O coração da operação é o `BatesNumberingStamp`. Ele permite definir prefixo, separador, preenchimento de dígitos e até se o selo deve ser tratado como um *artifact* (ou seja, invisível para ferramentas de extração de texto).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Por que essas configurações?**  
- `StartingNumber = 1000` imita um dossiê jurídico típico que já possui um histórico.  
- `NumberOfDigits = 5` garante que números como `01000`, `01001`, etc., fiquem alinhados corretamente.  
- `Artifact = true` é essencial quando o PDF será processado por OCR ou pipelines de e‑discovery; os números permanecem visíveis para humanos, mas são ignorados pelos mecanismos de busca de texto.

## Etapa 4: Adicionar o Selo a Cada Página

Agora percorrermos `document.Pages` e aplicamos o mesmo selo a cada página. O Aspose incrementa o número automaticamente para você.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Pergunta comum:** *Posso controlar onde o selo aparece?*  
> Absolutamente. O `BatesNumberingStamp` herda de `Stamp`, então você pode definir propriedades como `HorizontalAlignment`, `VerticalAlignment`, `XIndent` e `YIndent` antes do loop. Para simplificar, usaremos o canto inferior‑direito padrão.

## Etapa 5: Salvar o PDF Modificado

Por fim, persista as alterações. Você pode sobrescrever o arquivo original ou gravar em um novo local — aqui manteremos ambas as cópias.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Ao abrir `BatesNumbered.pdf`, cada página exibirá um selo semelhante a:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

onde `00123` representa a contagem total de páginas, e o prefixo `ABC-` permanece constante.

---

## Exemplo Completo Funcional

Copie todo o bloco abaixo para um novo arquivo `Program.cs` e execute. Ajuste os caminhos dos arquivos conforme seu ambiente.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Saída esperada no console:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Abra o arquivo salvo e você verá os números sequenciais em cada página — exatamente o que se espera ao **add bates numbers pdf**.

---

## Ajustes Avançados (Opcional)

| Objetivo | Como alcançar |
|------|-------------------|
| **Alterar a cor do selo** | Defina `batesStamp.Color = Color.FromRgb(255, 0, 0);` antes do loop. |
| **Colocar o selo no cabeçalho** | Ajuste as propriedades `HorizontalAlignment` e `VerticalAlignment` conforme mostrado no código comentado. |
| **Ignorar determinadas páginas** | Adicione uma condição `if (page.Number % 2 == 0) continue;` dentro do `foreach`. |
| **Usar uma fonte personalizada** | Atribua `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Tornar o selo visível ao OCR** | Defina `Artifact = false`. |

Essas variações permitem que você **add stamp to each page** mantendo a lógica central limpa.

---

## Perguntas Frequentes

**P: Isso funciona com PDFs protegidos por senha?**  
R: Sim. Carregue o documento com um objeto `PdfLoadOptions` que fornece a senha, e siga exatamente o mesmo procedimento.

**P: E se eu precisar de prefixos diferentes por caso?**  
R: Crie várias instâncias de `BatesNumberingStamp`, configure cada uma com seu próprio `Prefix` e aplique-as apenas nos intervalos de páginas correspondentes.

**P: A biblioteca é gratuita?**  
R: O Aspose.Pdf oferece um teste de 30 dias. Para uso em produção, será necessária uma licença, mas a API permanece exatamente a mesma.

---

## Conclusão

Acabamos de cobrir **como adicionar numeração bates** a qualquer PDF usando Aspose.Pdf, demonstrado como **add bates numbers pdf** de forma limpa e repetível, e mostramos a maneira mais simples de **add stamp to each page** com um único loop. O código é totalmente autônomo, executa em segundos e pode ser inserido em pipelines maiores de processamento de documentos sem modificações.

Pronto para o próximo desafio? Experimente gerar uma página de capa que liste o intervalo de Bates, ou incorpore um QR code ao lado de cada selo. As possibilidades são infinitas, e o padrão que você aprendeu hoje será útil sempre que precisar automatizar metadados de PDF.

Se este guia foi útil, compartilhe, deixe um comentário ou explore nossos outros tutoriais sobre mesclagem de PDFs, marca d'água e assinaturas digitais. Boa codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}