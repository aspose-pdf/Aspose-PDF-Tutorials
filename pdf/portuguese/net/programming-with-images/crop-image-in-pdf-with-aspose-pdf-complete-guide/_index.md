---
category: general
date: 2026-06-08
description: Corte imagem em PDF usando Aspose.PDF em C#. Aprenda como criar PDF com
  imagem, salvar PDF com imagem e adicionar imagem ao PDF em apenas algumas linhas.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: pt
og_description: Corte de imagem em PDF usando Aspose.PDF em C#. Este tutorial mostra
  como criar PDF com imagem, salvar PDF com imagem e adicionar imagem ao PDF rapidamente.
og_title: Cortar Imagem em PDF com Aspose.PDF – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Cortar Imagem em PDF com Aspose.PDF – Guia Completo
url: /pt/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recortar Imagem em PDF com Aspose.PDF – Guia Completo

Já se perguntou como **recortar imagem em PDF** sem precisar abrir um editor gráfico? Você não está sozinho. Em muitos relatórios, faturas ou e‑books você precisa apenas de um pedaço de uma imagem — talvez o canto do logotipo ou um fragmento de gráfico — e quer isso direto no PDF.  

Este guia mostra exatamente isso: vamos **criar PDF com imagem**, **adicionar imagem ao PDF**, e então **recortar imagem em PDF** usando a biblioteca Aspose.PDF para C#. Ao final, você também saberá como **salvar PDF com imagem** para enviar o arquivo a qualquer pessoa.

---

## O que você precisará

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+)  
- Uma cópia licenciada ou de avaliação do **Aspose.PDF for .NET** (instale via NuGet `Install-Package Aspose.PDF`)  
- Um arquivo de imagem (JPEG/PNG) no disco – vamos chamá‑lo de `image.jpg`  
- Qualquer IDE de sua preferência (Visual Studio, Rider, VS Code)

É só isso. Nenhum serviço extra, nenhuma ferramenta externa.

---

## Etapa 1: Configurar o Projeto e os Imports

Primeiro, crie um aplicativo console e importe os namespaces que usaremos. As instruções `using` mantêm o código organizado e facilitam a leitura das etapas posteriores.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Dica profissional:** Se estiver usando o Visual Studio, clique com o botão direito no projeto → *Manage NuGet Packages* → procure por “Aspose.PDF” e instale. A biblioteca cuida tanto da colocação quanto do recorte da imagem internamente, então você não precisará de bibliotecas de imagem de terceiros.

---

## Etapa 2: Criar PDF com Imagem

Agora vamos realmente **criar pdf com imagem**. O trecho abaixo cria um novo `Document`, adiciona uma página em branco e prepara um stream de imagem.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Executar este código gerará um PDF com a imagem inteira esticada nas dimensões que você especificou. É um bom teste de sanidade antes de começar a cortar.

---

## Etapa 3: Como Adicionar Imagem ao PDF (e Preparar para Recorte)

Se você já souber a região exata que deseja, pode pular a etapa de tamanho completo e ir direto para a parte **como adicionar imagem ao pdf**. O método `AddImage` aceita três parâmetros:

1. **Stream da imagem** – os bytes brutos da sua foto.  
2. **Retângulo de posicionamento** – onde na página a imagem será colocada.  
3. **Retângulo de recorte** – a parte da imagem que você realmente quer renderizar.

A seguir está a versão compacta que faz tanto o posicionamento **quanto** o recorte em uma única chamada.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Por que isso funciona:** Aspose.PDF mapeia internamente o retângulo de recorte para as dimensões de pixel da imagem, então renderiza apenas essa fatia dentro da área de `placement`. Nenhum processamento extra de bitmap é necessário, o que mantém o tamanho do PDF pequeno.

---

## Etapa 4: Como Recortar Imagem em PDF – Opções Avançadas

Às vezes o recorte simples não é suficiente. Talvez você precise de um retângulo personalizado ou queira preservar a proporção da imagem. Aqui está uma abordagem mais flexível:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Tratamento de casos extremos:**  
- **Streams nulos** – sempre envolva o `FileStream` em um bloco `using`, como mostrado, para evitar vazamentos.  
- **Imagens grandes** – se a imagem de origem for enorme, considere reduzir o retângulo de `placement`; o Aspose fará downsample automaticamente.  
- **PNGs transparentes** – a biblioteca respeita canais alfa, então a área recortada manterá a transparência.

---

## Etapa 5: Salvar PDF com Imagem (e Verificar)

Por fim, vamos **salvar pdf com imagem**. O método `Save` grava o documento no disco. Você também pode enviá‑lo como stream para um cliente web se estiver construindo uma API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Ao abrir `output.pdf`, você deverá ver apenas a porção recortada de `image.jpg` posicionada exatamente onde definiu. Se a imagem parecer esticada, ajuste a largura/altura do retângulo de `placement` para coincidir com a proporção do retângulo de recorte.

---

## Perguntas Frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **Posso recortar várias imagens na mesma página?** | Absolutamente. Chame `page.AddImage` para cada imagem com seus próprios retângulos de posicionamento e recorte. |
| **E se minha imagem estiver em outro formato (ex.: BMP)?** | Aspose.PDF suporta JPEG, PNG, BMP, GIF e TIFF nativamente. Basta mudar a extensão do arquivo. |
| **Preciso de licença para uso em produção?** | Uma avaliação funciona para até 5 páginas. Para implantações reais, adquira uma licença para remover a marca d'água. |
| **Como rotacionar a imagem recortada?** | Após adicionar a imagem, recupere o objeto `Image` e defina sua propriedade `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **Existe forma de recortar usando porcentagens ao invés de pontos absolutos?** | Sim — calcule as dimensões do retângulo com base em `image.Width * 0.25` etc., depois converta para pontos como mostrado na Etapa 4. |

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Execute o programa, abra `output.pdf` e você verá apenas o quadrante superior‑esquerdo de `image.jpg` renderizado no canto superior‑esquerdo da página. Altere os valores do retângulo `crop` para experimentar diferentes recortes.

---

## Conclusão

Percorremos todo o processo de **recortar imagem em pdf** usando Aspose.PDF para C#. Começando de um documento novo, **criamos pdf com imagem**, demonstramos o **como adicionar imagem ao pdf**, aplicamos um retângulo customizado de **como recortar imagem pdf**, e finalmente **salvamos pdf com imagem**.  

Agora você pode incorporar imagens recortadas com precisão em qualquer PDF que gerar — ideal para faturas, brochuras de marketing ou relatórios automatizados. Como próximo passo, considere adicionar legendas de texto (`TextFragment`) ou desenhar formas ao redor da imagem recortada para destacá‑la ainda mais.  

Tem mais cenários que gostaria de explorar? Deixe um comentário, e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Set Image Size in a PDF Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Extract Image Information from PDFs Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}