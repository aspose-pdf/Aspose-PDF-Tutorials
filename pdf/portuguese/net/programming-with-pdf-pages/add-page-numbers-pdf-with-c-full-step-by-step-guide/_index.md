---
category: general
date: 2026-01-02
description: Adicione números de página a PDFs rapidamente usando Aspose.Pdf em C#.
  Aprenda a adicionar numeração Bates, texto de rodapé, marca d'água personalizada
  e percorrer as páginas do PDF em um único script.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: pt
og_description: Adicione números de página ao PDF instantaneamente com Aspose.Pdf.
  Este guia também aborda a adição de numeração Bates, texto de rodapé, marca d'água
  personalizada e iteração pelas páginas do PDF.
og_title: Adicionar numeração de páginas ao PDF com C# – Tutorial completo de programação
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Adicionar números de página ao PDF com C# – Guia completo passo a passo
url: /pt/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar numeração de páginas PDF com C# – Tutorial de Programação Completo

Já precisou **adicionar numeração de páginas PDF** mas não sabia por onde começar? Você não está sozinho—desenvolvedores perguntam constantemente como inserir números, rodapés ou até um identificador no estilo Bates em cada página de um PDF.  

Neste tutorial você verá um exemplo pronto‑para‑executar em C# que **percorre páginas PDF**, adiciona um rodapé com número da página e (se desejar) inclui uma marca d’água personalizada. Também mostraremos como trocar o selo por um número Bates, que é apenas uma forma elegante de dizer “adicionar numeração Bates” para documentos legais ou forenses. Ao final, você terá um único método reutilizável que lida com todas essas tarefas sem esforço.

## Adicionar numeração de páginas PDF – Visão geral

Antes de mergulharmos no código, vamos esclarecer o que realmente significa “adicionar numeração de páginas PDF” no mundo do Aspose.Pdf. A biblioteca trata qualquer trecho de texto que você coloca em uma página como um **TextStamp**. Ao criar um selo com um placeholder de página (`{page}`) e aplicá‑lo a cada página, você obtém automaticamente a numeração sequencial. O mesmo selo pode conter texto adicional, permitindo **adicionar texto de rodapé** como “Confidencial” ou um identificador específico do caso.

> **Por que usar um selo em vez de editar o fluxo de conteúdo do PDF?**  
> Selos são objetos de alto nível que respeitam margens, rotação e gráficos existentes da página. Eles também são muito mais fáceis de manter—basta alterar algumas propriedades e reexecutar o script.

## Percorrer páginas PDF para aplicar selos

O primeiro passo prático é abrir o PDF de origem e iterar sobre suas páginas. Este é o padrão clássico de **loop through pdf pages** que a maioria dos exemplos do Aspose utiliza.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Dica profissional:** Se o seu PDF for muito grande (centenas de páginas), considere processá‑lo em lotes para manter o uso de memória baixo. O Aspose.Pdf transmite páginas de forma preguiçosa, portanto o loop já é bastante eficiente.

## Adicionar numeração Bates e texto de rodapé

Agora que podemos percorrer cada página, vamos criar um **TextStamp reutilizável** que contenha tanto o número da página quanto o texto de rodapé opcional. O placeholder `{page}` é substituído automaticamente pelo índice da página atual.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Por que isso funciona

* **`Bates-{page}`** – O Aspose substitui `{page}` pelo número real da página, gerando automaticamente um número Bates clássico.  
* **`Confidential`** – Esta é a parte de **add footer text**. Você pode substituir por qualquer string, inclusive puxando dados de um banco de dados.  
* **Estilização** – Usar `TextState` permite ajustar cor, opacidade e até rotação sem tocar nos fluxos internos do PDF.

Se precisar apenas de números simples, remova o prefixo “Bates‑” e o texto extra:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Adicionar marca d’água personalizada (opcional)

Às vezes você quer mais que um rodapé—precisa de um logotipo semitransparente ou de uma sobreposição “RASCUNHO” em toda a página. É aí que entra **add custom watermark**. A mesma classe `TextStamp` pode ser reutilizada, basta mudar seu alinhamento e opacidade.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Observação:** A ordem importa. Adicionar a marca d’água primeiro garante que os números de página permaneçam legíveis sobre o texto semitransparente.

## Salvar o PDF e verificar os resultados

Após aplicar os selos, o passo final é gravar as alterações no disco. A chamada `Save` que inserimos anteriormente faz o trabalho pesado, mas vamos acrescentar um pequeno trecho de verificação que abre o novo arquivo e exibe quantas páginas foram processadas.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Ao executar o programa completo, você deverá ver um PDF onde cada página termina com algo como **“Bates‑3 – Confidential”** (ou apenas “3” se usou o selo simples) e, se habilitou a marca d’água, um discreto “RASCUNHO” no centro.

### Saída esperada

| Página | Rodapé (exemplo) |
|--------|------------------|
| 1      | Bates‑1 – Confidential |
| 2      | Bates‑2 – Confidential |
| …      | … |
| N      | Bates‑N – Confidential |

Se abrir o arquivo em um visualizador, os números ficarão a 20 pts das margens esquerda e inferior, seguindo as convenções típicas de documentos legais.

## Exemplo completo funcional (pronto para copiar‑colar)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Salve este código como `AddPageNumbers.cs`, restaure o pacote NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`) e execute-o. Você obterá um arquivo **add page numbers pdf** que também demonstra **add bates numbering**, **add footer text**, **add custom watermark** e o clássico padrão **loop through pdf pages**—tudo em um script compacto.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusão

Cobremos tudo o que você precisa para **add page numbers pdf** usando Aspose.Pdf em C#. Desde percorrer cada página, aplicar números Bates, acrescentar texto de rodapé personalizado e até sobrepor uma marca d’água semitransparente, o código é compacto o suficiente para ser inserido em qualquer projeto existente.  

Em seguida, você pode explorar cenários mais avançados—como obter o texto do rodapé de um banco de dados, aplicar fontes diferentes por seção ou gerar um PDF de índice separado que liste todos os números Bates. Todas essas extensões se baseiam nas mesmas ideias centrais que mostramos aqui, então você está bem posicionado para expandir a solução conforme suas necessidades evoluam.  

Experimente, ajuste a estilização e conte nos comentários como funcionou para você. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}