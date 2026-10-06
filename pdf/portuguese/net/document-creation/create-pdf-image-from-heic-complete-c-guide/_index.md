---
category: general
date: 2026-06-08
description: Crie imagem PDF em C# convertendo HEIC para PDF. Aprenda como adicionar
  imagem ao PDF e gerar PDF a partir de imagem com código passo a passo.
draft: false
keywords:
- create pdf image
- convert heic to pdf
- add image to pdf
- generate pdf from image
- how to read heic
language: pt
og_description: Crie imagem PDF em C# convertendo HEIC para PDF. Siga este guia para
  adicionar a imagem ao PDF e gerar PDF a partir da imagem rapidamente.
og_title: Criar imagem PDF a partir de HEIC – Tutorial completo em C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  headline: Create PDF Image from HEIC – Complete C# Guide
  type: TechArticle
- description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  name: Create PDF Image from HEIC – Complete C# Guide
  steps:
  - name: What if the HEIC file is corrupted?
    text: The `HeicImage.Load` method throws a `HeicException`. Wrap the call in a
      try/catch (as shown) and log the error. In production you might fall back to
      a default placeholder image.
  - name: Can I batch‑process multiple HEIC files?
    text: Absolutely. Just move the core logic into a method like `ConvertHeicToPdf(string
      input, string output)` and iterate over a directory with `Directory.GetFiles("*.heic")`.
  - name: Does this approach preserve EXIF metadata?
    text: No, Aspose.Pdf does not automatically copy EXIF data into the PDF. If you
      need metadata, extract it with `HeicImage.Metadata` and add it to the PDF using
      `Document.Info` properties.
  - name: What about memory usage for huge images?
    text: For images larger than 10 MP, consider down‑sampling before creating `BitmapInfo`.
      You can use `HeicImage.Resize` (if supported) or a third‑party bitmap library
      to reduce dimensions.
  type: HowTo
tags:
- C#
- Aspose.Pdf
- HEIC
- ImageConversion
title: Criar imagem PDF a partir de HEIC – Guia completo de C#
url: /pt/net/document-creation/create-pdf-image-from-heic-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Imagem PDF a partir de HEIC – Guia Completo em C#

Já se perguntou como **criar imagem PDF** a partir de um arquivo HEIC sem perder a cabeça? Você não está sozinho. Em muitos aplicativos mobile‑first a câmera gera HEIC, porém sistemas legados ainda precisam de um bom e velho PDF. Este tutorial mostra exatamente como **converter HEIC para PDF**, adicionar a imagem a uma nova página PDF e, finalmente, **gerar PDF a partir de imagem** com Aspose.Pdf.

Vamos percorrer cada linha de código, explicar por que cada parte importa e fornecer um exemplo pronto‑para‑executar. Ao final, você poderá colocar um HEIC em uma pasta e obter um PDF nítido — sem ferramentas externas necessárias.

## O que você aprenderá

* Como **ler arquivos HEIC** em C# usando o decodificador `FileFormat.Heic`.
* Os passos exatos para **converter HEIC para PDF** com Aspose.Pdf.
* Formas de **adicionar imagem ao PDF** e controlar o formato de pixel.
* Dicas para lidar com imagens grandes e armadilhas comuns.
* Um programa completo, pronto para compilar, que você pode copiar e colar.

*Pré‑requisitos*: .NET 6+ (ou .NET Framework 4.6+), Aspose.Pdf for .NET e o pacote NuGet `FileFormat.Heic`. Se você nunca usou essas bibliotecas, não se preocupe — a instalação é abordada no primeiro passo.

---

## Etapa 0: Instalar Pacotes Necessários

Antes de mergulharmos no código, certifique‑se de que as duas bibliotecas estejam referenciadas no seu projeto:

```powershell
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic
```

Ambos os pacotes são gratuitos para desenvolvimento e suportam .NET Standard, portanto funcionam em aplicativos de console, ASP.NET ou até mesmo Unity.

---

## Etapa 1: Como Ler HEIC – Carregar o Arquivo como Stream

Ler um arquivo HEIC é semelhante a abrir qualquer arquivo binário, mas você precisa de um decodificador que entenda o contêiner HEIC. A biblioteca `FileFormat.Heic` nos fornece um conveniente método estático `Load`.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

// ...

// Open the HEIC file safely with a using block
using (FileStream heicStream = new FileStream(
           @"C:\Images\input.heic", FileMode.Open, FileAccess.Read))
{
    // Decode the HEIC image into a HeicImage object
    HeicImage heicImage = HeicImage.Load(heicStream);
```

**Por que um stream?**  
Um stream permite que o decodificador leia o arquivo de forma preguiçosa, o que reduz a pressão de memória para imagens enormes. A instrução `using` também garante que o manipulador de arquivo seja liberado, evitando erros de bloqueio de arquivo posteriormente.

---

## Etapa 2: Converter HEIC para PDF – Extrair Dados de Pixel

Aspose.Pdf espera dados bitmap brutos, não um objeto HEIC. Portanto, extraímos os bytes de pixel em um formato que ele entende — `Rgb24` funciona para a maioria dos casos de uso.

```csharp
    // Grab the raw RGB24 pixel array from the HEIC image
    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

    // Capture image dimensions for later use
    int width  = (int)heicImage.Width;
    int height = (int)heicImage.Height;
```

**Observação de caso extremo:** Se o seu HEIC de origem contém um canal alfa, `Rgb24` o descartará. Para transparência, você deve mudar para `Rgba32` e ajustar o `BitmapInfo` adequadamente.

---

## Etapa 3: Adicionar Imagem ao PDF – Construir o Objeto Aspose Image

Agora encapsulamos os bytes brutos em um `Aspose.Pdf.Image`. O construtor `BitmapInfo` informa ao Aspose o stride, tamanho e formato de pixel.

```csharp
    // Create an Aspose PDF Image using the pixel buffer
    Image pdfImage = new Image
    {
        BitmapInfo = new BitmapInfo(
            pixelData,
            width,
            height,
            BitmapInfo.PixelFormat.Rgb24)
    };
```

**Dica profissional:** Se você pretende incorporar muitas imagens no mesmo documento, reutilize uma única instância `Document` e crie novos objetos `Image` apenas por página. Isso economiza sobrecarga de criação de objetos.

---

## Etapa 4: Gerar PDF a partir da Imagem – Montar o Documento

Com a imagem pronta, criamos um novo documento PDF, adicionamos uma página e inserimos a imagem nela. A coleção `Paragraphs` do Aspose torna isso trivial.

```csharp
    // Initialize a new PDF document
    Document pdfDoc = new Document();

    // Add a blank page to the document
    Page page = pdfDoc.Pages.Add();

    // Insert the image into the page's paragraph collection
    page.Paragraphs.Add(pdfImage);
```

Se precisar posicionar a imagem (centralizar, escalar, etc.), você pode encapsul‑la em um `ImageStamp` ou ajustar `pdfImage.Margin`. Para a maioria das conversões um‑para‑um, o posicionamento padrão funciona bem.

---

## Etapa 5: Salvar o Resultado – Gravar o PDF no Disco

A etapa final é simplesmente persistir o arquivo PDF. Aspose suporta vários formatos; aqui usamos o clássico `.pdf`.

```csharp
    // Define the output path and save the PDF
    string outputPath = @"C:\Images\output.pdf";
    pdfDoc.Save(outputPath);
}
```

**Saída esperada:** Abrir `output.pdf` em qualquer visualizador mostrará a imagem HEIC original renderizada em sua resolução nativa. Nenhuma perda de qualidade além da compressão original do HEIC.

---

## Exemplo Completo em Funcionamento

Abaixo está o programa completo que você pode copiar para um aplicativo de console. Ele inclui todas as diretivas using e tratamento de erros para uma sensação pronta para produção.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

namespace HeicToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath  = @"C:\Images\input.heic";
            string outputPath = @"C:\Images\output.pdf";

            try
            {
                // 1️⃣ Open the HEIC file as a stream
                using (FileStream heicStream = new FileStream(
                           inputPath, FileMode.Open, FileAccess.Read))
                {
                    // 2️⃣ Load the HEIC image from the stream
                    HeicImage heicImage = HeicImage.Load(heicStream);

                    // 3️⃣ Extract pixel data in RGB24 format
                    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
                    int width  = (int)heicImage.Width;
                    int height = (int)heicImage.Height;

                    // 4️⃣ Create an Aspose.Pdf.Image using the pixel data
                    Image pdfImage = new Image
                    {
                        BitmapInfo = new BitmapInfo(
                            pixelData,
                            width,
                            height,
                            BitmapInfo.PixelFormat.Rgb24)
                    };

                    // 5️⃣ Add the image to a new PDF page
                    Document pdfDoc = new Document();
                    Page page = pdfDoc.Pages.Add();
                    page.Paragraphs.Add(pdfImage);

                    // 6️⃣ Save the resulting PDF
                    pdfDoc.Save(outputPath);
                }

                Console.WriteLine($"✅ Success! PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error: {ex.Message}");
            }
        }
    }
}
```

Execute o programa e você verá a mensagem no console confirmando a criação do PDF. Abra o arquivo e a imagem deverá ser idêntica ao HEIC original.

---

## Perguntas Frequentes & Armadilhas

### E se o arquivo HEIC estiver corrompido?
O método `HeicImage.Load` lança uma `HeicException`. Envolva a chamada em um try/catch (como mostrado) e registre o erro. Em produção, você pode recorrer a uma imagem placeholder padrão.

### Posso processar em lote vários arquivos HEIC?
Com certeza. Basta mover a lógica principal para um método como `ConvertHeicToPdf(string input, string output)` e iterar sobre um diretório com `Directory.GetFiles("*.heic")`.

### Esta abordagem preserva os metadados EXIF?
Não, o Aspose.Pdf não copia automaticamente os dados EXIF para o PDF. Se precisar de metadados, extraia-os com `HeicImage.Metadata` e adicione ao PDF usando as propriedades `Document.Info`.

### E quanto ao uso de memória para imagens enormes?
Para imagens maiores que 10 MP, considere reduzir a resolução antes de criar o `BitmapInfo`. Você pode usar `HeicImage.Resize` (se suportado) ou uma biblioteca bitmap de terceiros para reduzir as dimensões.

---

## Conclusão

Agora você sabe como **criar imagem PDF** a partir de uma fonte HEIC, efetivamente **converter HEIC para PDF** e **adicionar imagem ao PDF** usando Aspose.Pdf em C#. As etapas — ler o HEIC, extrair dados de pixel, encapsular em uma imagem PDF e salvar — são simples, mas poderosas o suficiente para pipelines de produção.

Em seguida, tente estender o script: gerar um PDF multipágina onde cada página contém um HEIC diferente, ou incorporar camadas de texto OCR para PDFs pesquisáveis. Você também pode explorar outros formatos de imagem (`jpeg`, `png`) com o mesmo padrão, reforçando a habilidade de **gerar PDF a partir de imagem**.

Sinta‑se à vontade para experimentar, compartilhar suas descobertas ou fazer perguntas nos comentários. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Adicionar um Cabeçalho de Imagem a PDFs Usando Aspose.PDF para .NET: Um Guia Passo a Passo](/pdf/english/net/images-graphics/add-image-header-pdf-aspose-dotnet/)
- [Como Adicionar um Carimbo de Imagem a um PDF Usando Aspose.PDF para .NET: Um Guia Passo a Passo](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Adicionar Carimbo de Imagem ao Rodapé de PDF Usando Aspose.PDF .NET: Um Guia Passo a Passo](/pdf/english/net/document-manipulation/add-image-stamp-pdf-footer-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}