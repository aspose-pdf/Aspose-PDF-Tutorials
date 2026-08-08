---
category: general
date: 2026-07-03
description: Tutorial de numeração Bates mostrando como adicionar numeração Bates
  a arquivos PDF usando Aspose.PDF. Inclui configuração de prefixo de número Bates
  e um exemplo completo de numeração Bates.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: pt
og_description: Tutorial de numeração Bates que orienta você a adicionar numeração
  Bates em arquivos PDF, definir um prefixo de número Bates e fornecer um exemplo
  completo em funcionamento.
og_title: 'Tutorial de Numeração Bates: Adicionar Números ao PDF com Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Tutorial de Numeração Bates: Adicionar Números ao PDF com Aspose'
url: /pt/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de Numeração Bates – Adicionando Números Bates a PDFs com Aspose

Já precisou de um **tutorial de numeração bates** porque tinha que marcar milhares de páginas para litígio? Você não está sozinho. Em muitos fluxos de trabalho jurídicos e de conformidade, uma forma confiável de *adicionar numeração bates pdf* é um requisito inegociável. Felizmente, o Aspose.PDF torna todo o processo muito simples, e neste guia vamos percorrer um **exemplo completo de numeração bates** que você pode inserir diretamente no seu projeto.

> **O que você receberá:** um trecho de código executável que define o número inicial, aplica um **prefixo de número bates** e salva o resultado — tudo em menos de 30 linhas de C#.

## Pré‑requisitos

Antes de começarmos, verifique se você tem:

- .NET 6.0 ou superior (a API funciona da mesma forma no .NET Framework 4.6+)
- Uma licença válida do Aspose.PDF for .NET (ou você pode usar o modo de avaliação gratuito)
- Um PDF de entrada chamado `input.pdf` colocado em uma pasta que você controla
- Visual Studio 2022 ou qualquer editor que entenda projetos C#

Nenhum pacote NuGet extra além do `Aspose.Pdf` é necessário.

## Etapa 1: Instalar Aspose.PDF for .NET

Abra seu terminal (ou o Console do Gerenciador de Pacotes) e execute:

```bash
dotnet add package Aspose.Pdf
```

Ou, se preferir a interface gráfica, clique com o botão direito em **Dependencies → Manage NuGet Packages**, procure por *Aspose.Pdf* e clique em **Install**. Isso traz a versão estável mais recente (em julho 2026, versão 23.12).

## Etapa 2: Abrir o Documento PDF Fonte

A primeira linha de qualquer fluxo de trabalho de **adicionar numeração bates pdf** é carregar o arquivo que você deseja marcar. Envolvemos a operação em um bloco `using` para que o documento seja descartado automaticamente.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Dica profissional:** Se o seu PDF estiver em um bucket na nuvem, você pode fornecer um `Stream` em vez de um caminho de arquivo — o Aspose.PDF lida com ambos perfeitamente.

## Etapa 3: Definir o Número Inicial e o Prefixo

Agora vem o coração do **exemplo de numeração bates**: dizer ao Aspose onde começar e qual texto deve preceder cada número. A propriedade `BatesNumbering` expõe tanto `Start` quanto `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

Por que usar um prefixo? Em muitos casos jurídicos o prefixo identifica o processo, o departamento ou o lote de produção. Usando `"ABC-"` como placeholder, você pode alterá‑lo para `"CASE42-"` ou qualquer string que se encaixe na sua convenção de nomenclatura.

## Etapa 4: Escolher Onde os Números Aparecem (Opcional)

Por padrão, o Aspose coloca o número no canto inferior direito, mas você pode movê‑lo para qualquer posição ajustando a propriedade `Location`. Esta etapa não é obrigatória para uma operação básica de **adicionar numeração bates pdf**, porém é útil saber.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

A `Location` recebe coordenadas X e Y medidas em pontos (1 pt ≈ 1/72 pol). Ajuste conforme necessário para o layout da sua página.

## Etapa 5: Salvar o PDF Atualizado

Por fim, persista as alterações. O método `Save` em `BatesNumbering` grava um novo arquivo mantendo o original intacto.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

Ao abrir `output.pdf`, cada página exibirá algo como `ABC-1000`, `ABC-1001`, … até a última página.

## Exemplo Completo Funcional

Juntando tudo, aqui está o **exemplo de numeração bates** que você pode copiar e colar no método `Main` de um aplicativo console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Saída esperada** (no console):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Abra o PDF gerado e você verá números sequenciais prefixados com `ABC-` começando em `1000`.

## Perguntas Frequentes & Casos Especiais

### E se eu precisar reiniciar o contador para cada seção?

Você pode chamar `pdfDocument.BatesNumbering.Reset()` antes de processar um novo intervalo de páginas. Combine isso com um loop sobre `pdfDocument.Pages` e defina `Start` novamente para cada seção.

### Como aplicar prefixos diferentes a intervalos de páginas distintos?

Crie múltiplos objetos `BatesNumbering` — um por intervalo — clonando o documento ou usando o método `Add` (disponível nas versões mais recentes do Aspose). Veja um esboço rápido:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### A biblioteca suporta prefixos Unicode?

Absolutamente. Passe qualquer string Unicode (por exemplo, `"案件‑"`). O Aspose.PDF lida com scripts da direita para a esquerda e símbolos especiais sem configuração extra.

### E quanto à segurança do PDF — a numeração Bates quebra a criptografia?

Se o PDF fonte estiver criptografado, você deve fornecer a senha antes de acessar `BatesNumbering`. O processo de numeração respeita as configurações de criptografia originais — seu output permanecerá criptografado a menos que você o altere explicitamente.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Dicas & Melhores Práticas

- **Processamento em lote:** Envolva toda a rotina em um loop `foreach` para tratar dezenas de arquivos automaticamente.
- **Log:** Registre o número inicial, o prefixo e o caminho de saída em um arquivo de log; isso facilita trilhas de auditoria para equipes jurídicas.
- **Desempenho:** Para PDFs muito grandes (500 + páginas), considere habilitar **otimização de memória** via `pdfDocument.OptimizeMemory = true;`.
- **Testes:** Sempre mantenha uma cópia do PDF original; a numeração Bates é irreversível após a gravação.

## Conclusão

Neste **tutorial de numeração bates** cobrimos tudo o que você precisa para **adicionar numeração bates pdf** com Aspose.PDF:

1. Instale a biblioteca.  
2. Carregue seu documento fonte.  
3. Defina o número inicial e um **prefixo de número bates**.  
4. (Opcional) ajuste a posição.  
5. Salve o resultado.

Agora você tem um **exemplo de numeração bates** sólido que pode ser adaptado a qualquer fluxo de trabalho jurídico, de arquivamento ou de conformidade. Quer ir além? Experimente combinar números Bates com marcas d'água, ou gerar um manifesto CSV que mapeie cada página ao seu identificador. O céu é o limite, e o Aspose fornece as ferramentas para chegar lá.

---

*Pronto para colocar isso em produção? Deixe um comentário se encontrar algum obstáculo, e feliz codificação!*

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}