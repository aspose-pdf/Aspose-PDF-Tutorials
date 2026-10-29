---
title: Dividir PDF após a décima página usando Aspose.Pdf for .NET
weight: 360
limit:
description: Código passo a passo para dividir um documento PDF logo após a décima página com Aspose.Pdf for .NET.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Código passo a passo para dividir um documento PDF logo após a décima
    página com Aspose.Pdf for .NET.
  headline: Dividir PDF após a décima página usando Aspose.Pdf for .NET
  type: TechArticle
- description: Código passo a passo para dividir um documento PDF logo após a décima
    página com Aspose.Pdf for .NET.
  name: Dividir PDF após a décima página usando Aspose.Pdf for .NET
  steps:
  - name: Os comentários de cabeçalho explicam o objetivo do exemplo, observam que
      o código completo foi movido e fornecem um link para a fonte atualizada.
    text: Os comentários de cabeçalho explicam o objetivo do exemplo, observam que
      o código completo foi movido e fornecem um link para a fonte atualizada.
  - name: A linha de stub não realiza nenhuma ação e existe apenas para manter a URL
      original funcional.
    text: A linha de stub não realiza nenhuma ação e existe apenas para manter a URL
      original funcional.
  type: HowTo
- questions:
  - answer: Aspose.Pdf não lançará um erro; o método `Split` simplesmente retornará
      o documento original inalterado porque não há página após a décima para iniciar
      uma nova parte.
    question: O que acontece se o PDF de origem tiver menos de dez páginas?
  - answer: Você chama `PdfDocument.Split(pageNumber)` em uma instância de `PdfDocument`,
      passando `10` como `pageNumber` para criar dois documentos separados.
    question: Qual classe e método são usados para dividir o PDF na página dez?
  - answer: Sim, Aspose.Pdf preserva todos os objetos de nível de página (marcadores,
      anotações, campos de formulário, etc.) nos documentos resultantes da divisão,
      mantendo-os vinculados às páginas de origem.
    question: Os marcadores, anotações e campos de formulário permanecem nas suas
      páginas originais após a divisão?
  - answer: Após chamar `Split`, você recebe dois objetos `PdfDocument`; você deve
      chamar `Save(\"FirstPart.pdf\")` no primeiro e `Save(\"SecondPart.pdf\")` no
      segundo, fornecendo nomes de arquivo distintos você mesmo.
    question: Como devo nomear os arquivos de saída para as duas partes criadas pela
      divisão?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: Dividir PDF após a página 10
og_description: Tutorial rápido para dividir um PDF na página 10 usando Aspose.Pdf for .NET.
og_image_alt: Guia que mostra como dividir um PDF após a décima página usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dividir PDF após a décima página usando Aspose.Pdf
Dividir um PDF em documentos separados pode simplificar a distribuição e o processamento. Este tutorial orienta você a usar Aspose.Pdf for .NET para dividir um PDF logo após a décima página, criando dois arquivos distintos. Siga o código passo a passo para extrair as primeiras dez páginas e as páginas restantes com apenas algumas linhas de C#.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: O que acontece se o PDF de origem tiver menos de dez páginas?**  
A: Aspose.Pdf não lançará um erro; o método `Split` simplesmente retornará o documento original inalterado porque não há página após a décima para iniciar uma nova parte.

**Q: Qual classe e método são usados para dividir o PDF na página dez?**  
A: Você chama `PdfDocument.Split(pageNumber)` em uma instância de `PdfDocument`, passando `10` como `pageNumber` para criar dois documentos separados.

**Q: Os marcadores, anotações e campos de formulário permanecem nas suas páginas originais após a divisão?**  
A: Sim, Aspose.Pdf preserva todos os objetos de nível de página (marcadores, anotações, campos de formulário, etc.) nos documentos resultantes da divisão, mantendo-os vinculados às páginas de origem.

**Q: Como devo nomear os arquivos de saída para as duas partes criadas pela divisão?**  
A: Após chamar `Split`, você recebe dois objetos `PdfDocument`; você deve chamar `Save(\"FirstPart.pdf\")` no primeiro e `Save(\"SecondPart.pdf\")` no segundo, fornecendo nomes de arquivo distintos você mesmo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}