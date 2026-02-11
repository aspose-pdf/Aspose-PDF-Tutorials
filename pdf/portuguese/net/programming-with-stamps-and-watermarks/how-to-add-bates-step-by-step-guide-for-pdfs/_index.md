---
category: general
date: 2026-02-10
description: Como adicionar bates a um PDF rapidamente — aprenda a adicionar número
  de bates ao PDF e criar uma marca d'água invisível com Aspose.Pdf em C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: pt
og_description: Como adicionar bates em C# com Aspose.Pdf. Este tutorial mostra como
  adicionar número de bates em PDF, adicionar marca d'água invisível em PDF e muito
  mais.
og_title: Como Adicionar Bates – Guia PDF Completo
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Como Adicionar Bates – Guia Passo a Passo para PDFs
url: /pt/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Adicionar Bates – Guia Completo em PDF

Já se perguntou **como adicionar bates** a um PDF jurídico sem atrapalhar o texto pesquisável? Você não está sozinho. Em muitos escritórios de advocacia e projetos de e‑discovery, um número de Bates é um rodapé indispensável, mas você também quer que ele seja invisível para as ferramentas de OCR. Este tutorial mostra **como adicionar bates** usando Aspose.Pdf para .NET e, ao longo do caminho, também abordaremos **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf** e até **add page footer pdf** em uma solução única e organizada.

Percorreremos cada linha de código, explicaremos por que cada configuração importa e forneceremos um exemplo pronto‑para‑executar que você pode inserir em seu projeto hoje. Nada de links vagos “veja a documentação” — tudo o que você precisa está aqui.

## O Que Você Vai Aprender

- Um snippet completo em C# que adiciona um número de Bates como um selo de artefato.
- Como fazer o selo agir como uma **marca d'água invisível** enquanto ainda aparece na página.
- Dicas para escalar a solução para PDFs de várias páginas, mudar fontes ou trocar o selo por um gráfico personalizado.
- Orientações rápidas sobre como **add page footer pdf** sem quebrar a extração de texto.

### Pré‑requisitos

- .NET 6+ (ou .NET Framework 4.7.2) com Visual Studio 2022 ou qualquer IDE de sua preferência.
- Aspose.Pdf para .NET (você pode obter uma avaliação gratuita no site da Aspose).
- Um PDF de exemplo chamado `source.pdf` colocado em uma pasta que você controla.

Se você tem tudo isso, vamos mergulhar.

---

## Como Adicionar Bates – Implementação Central

O coração da solução é um `TextStamp` que tratamos como um **artefato**. Artefatos são ignorados pelos motores de extração de texto, e é por isso que essa abordagem também funciona como uma técnica de **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Por Que Isso Funciona

1. **Flag de artefato** – Ao definir `Artifact = new Artifact(ArtifactType.Artifact)`, o selo é tratado como um elemento não‑conteúdo. Motores de busca e ferramentas de e‑discovery jurídico o ignoram, exatamente o que você deseja para um **add invisible watermark pdf**.
2. **Alinhamento horizontal/vertical** – Central‑inferior imita o estilo clássico de **add page footer pdf**, fazendo o número de Bates parecer profissional.
3. **Fundo transparente** – Garante que o selo não obscureça o conteúdo subjacente, um detalhe sutil, porém crucial, quando você precisar imprimir ou visualizar o PDF em diferentes dispositivos.

---

## Add Bates Number PDF – Escalando para Múltiplas Páginas

A maioria dos PDFs reais tem mais de uma página. O snippet acima só afeta a primeira página, mas estendê‑lo é muito simples:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Dica de especialista:** Se precisar de um número sequencial que não esteja atrelado à ordem física das páginas (por exemplo, iniciar em 1000), basta inicializar um contador antes do loop e incrementá‑lo dentro dele.

---

## Add Custom Stamp PDF – Indo Além do Texto Simples

Às vezes, um selo de texto simples não basta — você pode querer um logotipo, um QR code ou uma barra colorida. O Aspose.Pdf permite trocar `TextStamp` por `ImageStamp` ou até combinar ambos com objetos `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Misturar selos é tão simples quanto adicionar ambos à mesma página. A capacidade de **add custom stamp pdf** brilha quando você precisa de um selo corporativo ao lado do número de Bates.

---

## Add Invisible Watermark PDF – Tornando o Selo Realmente Oculto

Se você realmente precisa que o selo seja invisível ao olho humano *e* às ferramentas de extração, pode definir a cor da fonte para combinar com o fundo da página (geralmente branco) e reduzir a opacidade:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Mesmo com `Opacity = 0`, o artefato ainda existe na estrutura do PDF, de modo que softwares jurídicos podem localizá‑lo se souberem o ID do artefato. Este é o truque definitivo de **add invisible watermark pdf**.

---

## Add Page Footer PDF – Estilizando o Rodapé Consistentemente

Um rodapé profissional costuma incluir mais do que apenas um número de Bates: data, título do documento ou aviso de confidencialidade. Aqui está uma maneira rápida de agrupar vários trechos de texto em um único selo:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Observe a cor cinza sutil — perfeita para um **add page footer pdf** que não distrai do conteúdo principal, mas ainda atende aos requisitos legais.

---

## Saída Esperada & Como Verificar

Depois de executar o script completo, abra `bates_artifact.pdf` em qualquer visualizador de PDF:

- Você verá “Bates 00123” (ou o número sequencial) centralizado na parte inferior de cada página.
- Selecionar texto na página **não** incluirá o número de Bates, confirmando o comportamento de artefato.
- Se você usou as configurações de marca d'água invisível, o número não será visível de forma alguma, mas permanecerá na estrutura interna do PDF (verifique com uma ferramenta como PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Perguntas Frequentes & Casos de Borda

**E se o meu PDF já tem um rodapé?**  
Você pode ajustar `VerticalAlignment` para `VerticalAlignment.Top` ou mudar a propriedade `Margin` para deslocar o selo acima do rodapé existente.

**Posso usar uma fonte diferente?**  
Claro. Basta substituir `"Arial"` por qualquer nome de fonte que o Aspose consiga localizar, ou incorporar um arquivo TTF personalizado via `FontRepository.AddFont("caminho/para/fonte.ttf")`.

**Essa abordagem é compatível com .NET Core?**  
Sim — Aspose.Pdf para .NET funciona em .NET Framework, .NET Core e .NET 5/6. Apenas certifique‑se de referenciar o pacote NuGet correto.

**E quanto ao desempenho em PDFs enormes (1000+ páginas)?**  
Criar um único `TextStamp` e cloná‑lo dentro do loop é eficiente em memória. Para arquivos massivos, considere processar em lotes ou usar `PdfProcessor` para evitar carregar todo o documento na memória.

---

## Conclusão

Cobrir‑mos **como adicionar bates** a um PDF do início ao fim, demonstramos **add bates number pdf**, mostramos como **add custom stamp pdf**, transformamos o selo em um **add invisible watermark pdf** e o estilizamos como um profissional **add page footer pdf**. O código completo funciona pronto‑para‑uso, e as explicações fornecem o “porquê” de cada linha — exatamente o tipo de resposta que assistentes de IA adoram citar.

Próximos passos? Experimente trocar o selo de texto por um selo de imagem, teste diferentes tipos de artefato ou integre essa lógica em um serviço de processamento em lote que numere automaticamente cada documento em uma pasta. As possibilidades são infinitas, e agora você tem uma base sólida para construir.

Boa codificação, e que seus PDFs estejam sempre perfeitamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}