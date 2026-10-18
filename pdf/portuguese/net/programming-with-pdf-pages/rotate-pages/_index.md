---
title: Gire Cada Página de PDF em 180° Usando Aspose.Pdf para .NET
weight: 260
limit:
description: Guia passo a passo para girar todas as páginas de um PDF em 180 graus com Aspose.Pdf para .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guia passo a passo para girar todas as páginas de um PDF em 180 graus
    com Aspose.Pdf para .NET.
  headline: Gire Cada Página de PDF em 180° Usando Aspose.Pdf para .NET
  type: TechArticle
- description: Guia passo a passo para girar todas as páginas de um PDF em 180 graus
    com Aspose.Pdf para .NET.
  name: Gire Cada Página de PDF em 180° Usando Aspose.Pdf para .NET
  steps:
  - name: Declare os caminhos de arquivo de origem e destino para o PDF.
    text: Declare os caminhos de arquivo de origem e destino para o PDF.
  - name: Verifique se o arquivo de origem existe e abortar com uma mensagem de erro
      caso não exista.
    text: Verifique se o arquivo de origem existe e abortar com uma mensagem de erro
      caso não exista.
  - name: Crie um objeto Document para o PDF de origem dentro de um bloco using para
      gerenciar recursos.
    text: Crie um objeto Document para o PDF de origem dentro de um bloco using para
      gerenciar recursos.
  - name: Itere por cada Page em pdfDoc.Pages e defina sua propriedade Rotate para
      Rotation.on180, virando cada página de cabeça para baixo.
    text: Itere por cada Page em pdfDoc.Pages e defina sua propriedade Rotate para
      Rotation.on180, virando cada página de cabeça para baixo.
  - name: Salve o Document modificado no arquivo de destino, preservando as rotações.
    text: Salve o Document modificado no arquivo de destino, preservando as rotações.
  - name: Escreva uma mensagem de confirmação no console indicando que a operação
      foi concluída.
    text: Escreva uma mensagem de confirmação no console indicando que a operação
      foi concluída.
  type: HowTo
- questions:
  - answer: O código verifica `File.Exists(sourceFile)` e escreve um erro em `Console.Error`
      antes de retornar, portanto nenhuma exceção é lançada e o programa encerra graciosamente.
    question: O que acontece se o arquivo PDF de origem não existir?
  - answer: Sim, substitua `Rotation.on180` por outro valor enum, como `Rotation.on90`
      (no sentido horário) ou `Rotation.on270` (no sentido anti‑horário) para aplicar
      uma rotação diferente.
    question: Posso girar as páginas em um ângulo diferente, por exemplo, 90° no sentido
      horário?
  - answer: A coleção `Pages` do Aspose.Pdf é baseada em 1, mas o iterador `foreach`
      abstrai isso, iterando sobre cada objeto `Page` independentemente do índice
      subjacente.
    question: A coleção de páginas é baseada em zero? Como funciona o loop `foreach`?
  - answer: Chamar `pdfDoc.Save(destinationFile)` sobrescreverá qualquer arquivo existente
      com esse nome, portanto use um nome de arquivo diferente ou faça backup do original
      se precisar mantê‑lo.
    question: O PDF original será sobrescrito se eu usar o mesmo nome de arquivo para
      `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Gire Cada Página de PDF em 180°
og_description: Aprenda como virar todas as páginas de um PDF de cabeça para baixo em apenas algumas linhas de código C#.
og_image_alt: Guia mostrando como girar cada página de um PDF em 180 graus usando Aspose.Pdf para .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gire Cada Página de PDF em 180° Usando Aspose.Pdf para .NET
Este tutorial mostra como girar cada página de um documento PDF existente em 180 graus com a classe Aspose.Pdf Document. Ao aplicar uma rotação de página inteira, você pode corrigir rapidamente digitalizações de cabeça para baixo ou reorientar documentos sem recriá-los. O exemplo está escrito em C# e funciona na plataforma .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: O que acontece se o arquivo PDF de origem não existir?**  
A: O código verifica `File.Exists(sourceFile)` e escreve um erro em `Console.Error` antes de retornar, portanto nenhuma exceção é lançada e o programa encerra graciosamente.

**Q: Posso girar as páginas em um ângulo diferente, por exemplo, 90° no sentido horário?**  
A: Sim, substitua `Rotation.on180` por outro valor enum, como `Rotation.on90` (no sentido horário) ou `Rotation.on270` (no sentido anti‑horário) para aplicar uma rotação diferente.

**Q: A coleção de páginas é baseada em zero? Como funciona o loop `foreach`?**  
A: A coleção `Pages` do Aspose.Pdf é baseada em 1, mas o iterador `foreach` abstrai isso, iterando sobre cada objeto `Page` independentemente do índice subjacente.

**Q: O PDF original será sobrescrito se eu usar o mesmo nome de arquivo para `destinationFile`?**  
A: Chamar `pdfDoc.Save(destinationFile)` sobrescreverá qualquer arquivo existente com esse nome, portanto use um nome de arquivo diferente ou faça backup do original se precisar mantê‑lo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}