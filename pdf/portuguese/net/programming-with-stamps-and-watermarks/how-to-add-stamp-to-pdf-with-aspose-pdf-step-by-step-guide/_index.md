---
category: general
date: 2026-03-24
description: Como adicionar selo a um PDF usando Aspose.Pdf em C#. Aprenda a inserir
  selo PDF e a adicionar selo de texto PDF com redimensionamento automático em poucos
  passos simples.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: pt
og_description: Como adicionar selo a um PDF em C#? Este guia mostra como inserir
  selo em PDF e adicionar selo de texto em PDF com dimensionamento automático de fonte
  usando Aspose.Pdf.
og_title: Como adicionar selo a PDF com Aspose.Pdf – Guia rápido
tags:
- pdf
- csharp
- aspose
- stamping
title: Como adicionar selo ao PDF com Aspose.Pdf – Guia passo a passo
url: /pt/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Adicionar Carimbo a PDF com Aspose.Pdf – Guia Passo a Passo

**Como adicionar carimbo** a um PDF é uma necessidade comum quando você quer marcar, certificar ou simplesmente anotar um documento. Já se perguntou a maneira mais fácil de colocar um carimbo PDF sem lutar com gráficos de baixo nível? Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que não só mostra **como adicionar carimbo**, mas também explica *por que* cada linha é importante.

Você aprenderá como **colocar carimbo PDF** em qualquer página, como **adicionar carimbo de texto PDF** que encolhe automaticamente para caber em seu retângulo, e quais armadilhas evitar quando o texto for muito longo. Ao final, você terá um único arquivo C# que pode inserir em seu projeto e começar a carimbar PDFs imediatamente.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

* .NET 6.0 ou superior (o código funciona também com .NET Core e .NET Framework).
* O pacote NuGet Aspose.Pdf for .NET (`Aspose.Pdf`) instalado.
* Um arquivo PDF chamado `input.pdf` em uma pasta que você possa referenciar (qualquer PDF simples de uma página serve).

Nenhuma configuração extra é necessária—Aspose.Pdf cuida de todo o trabalho pesado.

## Etapa 1: Configurar o Projeto e Carregar o PDF de Origem

A primeira coisa que precisamos é de um objeto `Document` que represente o PDF que queremos anotar. Pense nele como carregar uma tela em branco que mais tarde pintaremos com um carimbo.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Por que isso importa:** `Document` é o ponto de entrada para qualquer manipulação de PDF no Aspose.Pdf. Ao usar o padrão `using` garantimos que o manipulador de arquivo seja liberado, o que impede problemas de bloqueio de arquivo quando você tentar salvar o PDF modificado posteriormente.

## Etapa 2: Criar um Carimbo de Texto com Redimensionamento Automático da Fonte

Agora criamos um `TextStamp`. O truque que faz este exemplo se destacar é a flag `AutoAdjustFontSizeToFitStampRectangle`—ela indica ao Aspose para encolher o texto até que caiba dentro do retângulo que definimos.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Dica profissional:** Se precisar de um logotipo ou imagem em vez de texto, use `ImageStamp`—a mesma lógica de ajuste automático existe para dimensionamento de imagens.

## Etapa 3: Escolher Onde **Colocar Carimbo PDF** – Primeira Página, Última Página ou Índice Personalizado

Aspose.Pdf armazena as páginas em uma coleção baseada em 1 (`pdfDocument.Pages[1]` é a primeira página). Você pode **colocar carimbo PDF** em qualquer página alterando o índice.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Por que isso é flexível:** Como a coleção `Pages` é mutável, você pode percorrer todas as páginas e adicionar o mesmo carimbo a cada uma, ou direcionar uma página específica com base em lógica de negócio (por exemplo, apenas a capa).

## Etapa 4: Salvar o Documento Modificado

Depois de aplicar o carimbo, você precisa gravar as alterações no disco. Pode sobrescrever o arquivo original ou criar um novo—como preferir.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Ao abrir `output-stamped.pdf` você verá um retângulo cinza claro na primeira página contendo o texto “Long text that must fit”. Se o texto fosse mais longo, o Aspose o encolheria automaticamente até que coubesse perfeitamente dentro do retângulo de 300 × 100 pt.

## Exemplo Completo Funcionando

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console (`Program.cs`). Ele inclui todas as partes que discutimos, além de um pequeno helper para verificar se o carimbo aparece.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Resultado Esperado

* O PDF abre com uma caixa cinza semitransparente na primeira página.
* Dentro da caixa o texto fornecido cabe perfeitamente, mesmo que você o substitua por uma frase mais longa.
* Nenhum cálculo manual de tamanho de fonte é necessário—o Aspose faz o trabalho pesado.

## Armadilhas Comuns ao **Colocar Carimbo PDF**

| Sintoma | Causa Provável | Solução |
|---------|----------------|---------|
| O texto é cortado | `AutoAdjustFontSizeToFitStampRectangle` está **false** ou o retângulo é muito pequeno. | Ative a flag e aumente `Width`/`Height` ou reduza o comprimento do texto. |
| O carimbo aparece fora do centro | `HorizontalAlignment`/`VerticalAlignment` padrão são `Left`/`Top`. | Defina `HorizontalAlignment = HorizontalAlignment.Center` e `VerticalAlignment = VerticalAlignment.Center`. |
| O carimbo não é visível em alguns visualizadores | Opacidade de fundo definida como 0 ou a cor do carimbo combina com o fundo da página. | Use um `Background.Color` contrastante ou defina `Opacity` > 0.3. |
| Vários carimbos se sobrepõem | Adição de carimbos em loop sem ajustar coordenadas. | Use `textStamp.XIndent` e `textStamp.YIndent` para deslocar cada carimbo. |

Tratar essas questões cedo economiza muito tempo de depuração depois.

## Expandindo o Exemplo: Adicionando um Carimbo de Imagem

Se precisar **adicionar carimbo de texto PDF** *e* uma imagem (por exemplo, o logotipo da empresa), pode combinar ambos:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Agora a página mostra tanto um carimbo de texto dinâmico quanto um carimbo de imagem estático lado a lado.

## Testando sua Implementação

1. Execute o aplicativo console.  
2. Abra `output-stamped.pdf` no Adobe Reader, Edge ou qualquer visualizador de PDF.  
3. Verifique se o retângulo do carimbo está presente e o texto está totalmente visível.  
4. Altere o texto para uma frase mais longa, execute novamente e confirme que a fonte encolhe automaticamente.

Se algo parecer errado, verifique novamente as dimensões do retângulo e a configuração `AutoAdjustFontSizePrecision`.

## Conclusão

Agora você sabe **como adicionar carimbo** a um PDF usando Aspose.Pdf, como **colocar carimbo PDF** em uma página específica, e como **adicionar carimbo de texto PDF** que ajusta automaticamente o tamanho da fonte. O exemplo completo e executável acima elimina adivinhações e fornece uma base sólida para cenários de carimbagem mais avançados—como processamento em lote de dezenas de arquivos ou adição condicional de marcas d'água.

Pronto para o próximo passo? Experimente carimbar todas as páginas em um loop, experimente diferentes fontes, ou combine carimbos de imagem e texto para criar um selo com aparência profissional. O céu é o limite, e com Aspose.Pdf você tem um motor confiável sob o capô.

Se encontrou algum obstáculo, deixe um comentário ou consulte a documentação do Aspose.Pdf para opções de personalização mais avançadas. Boa carimbagem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}