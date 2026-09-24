---
category: general
date: 2026-03-03
description: Crie documento PDF em C# com numeração Bates – aprenda como adicionar
  Bates, inserir numeração sequencial de páginas e gerar Bates em apenas alguns passos.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: pt
og_description: Crie documento PDF em C# com numeração Bates. Este guia mostra como
  adicionar Bates, adicionar numeração sequencial de páginas e gerar Bates rapidamente.
og_title: Criar documento PDF C# – Adicionar numeração Bates
tags:
- C#
- PDF
- Bates numbering
title: Criar documento PDF em C# – Adicionar numeração Bates
url: /pt/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF C# – Adicionar Numeração Bates

Já precisou **criar documento PDF C#** e então marcar cada página com um identificador único para fins legais ou de arquivamento? Você não está sozinho—escritórios de advocacia, tribunais e até grandes corporações perguntam constantemente: “Como adiciono numeração Bates aos meus PDFs automaticamente?” A boa notícia é que, com algumas linhas de código, você pode gerar um PDF, espalhar números Bates em cada página e salvar o resultado sem nunca abrir um editor.

Neste tutorial, percorreremos um exemplo prático, de ponta a ponta, que mostra **como adicionar Bates**, como **adicionar numeração sequencial de páginas**, e até como **gerar Bates** com prefixos personalizados. Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto .NET.

## O que você precisará

- **.NET 6+** (o código funciona também no .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – uma biblioteca comercial que oferece uma API limpa para manipulação de PDFs. Uma avaliação gratuita funciona bem para testes.
- Um entendimento básico de C# (você provavelmente já está confortável com declarações `using` e objetos).

Nenhum pacote NuGet adicional é necessário além do `Aspose.Pdf`. Se ainda não o instalou, execute:

```bash
dotnet add package Aspose.Pdf
```

> **Dica profissional:** Mantenha sua versão do Aspose atualizada; a versão mais recente 23.x adiciona ajustes de desempenho para documentos grandes.

## Etapa 1: Abrir (ou Criar) o Documento PDF Fonte

Primeiro precisamos de um PDF para trabalhar. Em muitos cenários reais, você já tem um arquivo de entrada—por exemplo, um contrato escaneado. Para fins de exemplo, vamos abrir um arquivo existente chamado `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Por que isso importa:** Abrir o documento dentro de um bloco `using` garante que o manipulador de arquivo seja liberado rapidamente, evitando problemas de bloqueio de arquivo quando você tentar sobrescrever o mesmo arquivo mais tarde.

## Etapa 2: Definir suas Opções de Numeração Bates

Os números Bates consistem em um **prefixo** (geralmente um identificador de caso) e um **número inicial**. Você também pode controlar o número de dígitos, a posição na página e o estilo da fonte. Aqui usaremos a palavra‑chave secundária **add bates numbering pdf** configurando um objeto `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Como adicionar Bates:** Ajustando `Prefix` e `Start` você controla a string exata que aparecerá em cada página. A propriedade `NumberOfDigits` garante largura consistente, o que é útil para processos legais.

## Etapa 3: Aplicar Numeração Bates a Cada Página

Agora vem a operação principal—adicionar os números. O método `AddBatesNumbering` percorre cada página, desenha o texto e respeita as opções que definimos.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Nos bastidores, o Aspose renderiza o texto como um elemento *content*, o que significa que os números se tornam parte do PDF e não podem ser desativados em um visualizador. Isso é exatamente o que você precisa quando deseja **adicionar numeração sequencial de páginas** que seja imutável.

### Casos Limite & Variações

- **Múltiplos prefixos:** Se precisar de prefixos diferentes por seção, crie `BatesNumberingOptions` separados e chame `AddBatesNumbering` em um intervalo de páginas (`pdfDocument.Pages[1..5]`).
- **Controle de preenchimento com zeros:** Omitir `NumberOfDigits` para um número de comprimento variável, ou definir um valor maior para zeros à esquerda.
- **Posicionamento personalizado:** Use `Margin` para deslocar o número da borda, ou altere `HorizontalAlignment` para `Center` para um estilo de rodapé.

## Etapa 4: Salvar o PDF Modificado

Finalmente, grave o documento atualizado no disco. Você pode sobrescrever o original ou criar um arquivo totalmente novo.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Depois que esta linha for executada, `output.pdf` contém o conteúdo original mais uma marca Bates visível em cada página—exatamente o que se espera ao **how to generate bates** para um arquivo de caso.

## Exemplo Completo e Executável

Juntando tudo, aqui está o trecho completo que você pode copiar‑colar em um aplicativo de console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Resultado Esperado

Abra `output.pdf` em qualquer visualizador (Adobe Reader, Edge, etc.). Você verá cada página carimbada com algo como **CASE-001000**, **CASE-001001**, … até a última página. Os números ficam bem posicionados no canto inferior‑direito, correspondendo às opções que definimos.

## Perguntas Frequentes & Solução de Problemas

- **“E se meu PDF estiver protegido por senha?”**  
  Carregue‑o com a senha: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“Posso adicionar números Bates a um PDF recém‑criado?”**  
  Claro. Basta criar o documento primeiro (`var doc = new Document();`) e então seguir as Etapas 2‑4 antes de salvar.

- **“A fonte é sempre incorporada?”**  
  O Aspose incorpora automaticamente a fonte se ela ainda não estiver no PDF. Se precisar de uma família de fontes específica, defina `options.Font` adequadamente.

- **“E quanto ao desempenho em arquivos de 10.000 páginas?”**  
  A biblioteca faz streaming das páginas, então o uso de memória permanece modesto. Contudo, pode ser interessante aumentar o `PdfSaveOptions.CompressionMode` para I/O mais rápido.

## Dicas Profissionais para Uso em Produção

1. **Processamento em lote:** Envolva a lógica acima em um loop que itere sobre uma pasta de PDFs. Use `Directory.GetFiles("*.pdf")` e processe cada arquivo individualmente.
2. **Logging:** Registre os primeiros e últimos números Bates em um arquivo de log—ajuda auditores a verificar se a numeração foi contínua.
3. **Tratamento de erros:** Envolva todo o bloco em um `try/catch` e exiba uma mensagem clara se o PDF de origem estiver ausente ou corrompido.
4. **Flexibilidade de preenchimento com zeros:** Se precisar de uma contagem de dígitos dinâmica baseada no total de páginas, calcule `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Conclusão

Acabamos de mostrar como **criar documento PDF C#** e adicionar numeração Bates de forma contínua—cobrindo tudo, desde o carregamento inicial até a gravação final. O exemplo curto demonstra **como adicionar bates**, **adicionar numeração sequencial de páginas**, e **como gerar bates** com prefixos personalizados e preenchimento com zeros. Com alguns ajustes, você pode adaptar esse padrão para trabalhos em lote, diferentes layouts ou até integrá‑lo a uma API web que devolve um PDF recém‑numerado sob demanda.

Pronto para o próximo passo? Experimente combinar isso com o recurso de **marca‑d’água** da Aspose, ou gerar um índice resumido que liste cada número Bates ao lado de uma breve descrição do conteúdo da página. As possibilidades são infinitas, e o código que você tem agora é uma base sólida para qualquer fluxo de trabalho de automação de documentos.

Feliz codificação, e que seus PDFs estejam sempre perfeitamente numerados! 

![Screenshot of a PDF viewer showing create pdf document c# with Bates numbers applied](image-placeholder.png "create pdf document c# with Bates numbers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}