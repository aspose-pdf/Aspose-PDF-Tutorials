---
title: Gire uma única página PDF em 180 graus com Aspose.PDF for .NET
weight: 260
limit:
description: Aprenda a girar a terceira página de um PDF em 180° usando Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda a girar a terceira página de um PDF em 180° usando Aspose.PDF
    for .NET.
  headline: Gire uma única página PDF em 180 graus com Aspose.PDF for .NET
  type: TechArticle
- description: Aprenda a girar a terceira página de um PDF em 180° usando Aspose.PDF
    for .NET.
  name: Gire uma única página PDF em 180 graus com Aspose.PDF for .NET
  steps:
  - name: O arquivo contém apenas comentários explicativos e nenhum código executável,
      servindo como um espaço reservado para o exemplo original.
    text: O arquivo contém apenas comentários explicativos e nenhum código executável,
      servindo como um espaço reservado para o exemplo original.
  type: HowTo
- questions:
  - answer: Use a coleção de páginas do SDK com indexação baseada em zero, por exemplo,
      `pdfDocument.Pages[2]`, pois o índice 2 corresponde à terceira página.
    question: Como eu seleciono a terceira página do PDF para rotação?
  - answer: A propriedade de rotação aceita apenas os quatro valores padrão 0, 90,
      180 e 270 graus; qualquer outro valor é arredondado para o ângulo permitido
      mais próximo.
    question: Posso girar uma página em um ângulo diferente de 180 graus?
  - answer: A rotação é aplicada apenas ao `PdfDocument` em memória; você deve chamar
      `pdfDocument.Save(\"output.pdf\")` (ou um método de salvamento semelhante) para
      gravar as alterações em um novo arquivo, deixando a origem inalterada.
    question: A rotação da página modifica o arquivo original automaticamente?
  - answer: O SDK recalcula automaticamente as posições das anotações e dos campos
      de formulário para que permaneçam corretamente alinhados com a nova orientação.
    question: O que acontece com anotações ou campos de formulário após a página ser
      girada?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Gire uma página PDF em 180° com Aspose.PDF
og_description: Vire rapidamente a terceira página do seu PDF de cabeça para baixo com algumas linhas de código Aspose.PDF for .NET.
og_image_alt: Guia que mostra o código que gira a terceira página de um PDF em 180 graus usando Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gire uma única página PDF em 180 graus com Aspose.PDF
Neste tutorial você aprenderá como girar a terceira página de um documento PDF em 180 graus usando Aspose.PDF for .NET. O exemplo demonstra como carregar um PDF, selecionar a página 3, aplicar a rotação e salvar o arquivo atualizado. Essa abordagem permite virar uma página específica sem alterar a orientação das demais páginas.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Como eu seleciono a terceira página do PDF para rotação?**  
A: Use a coleção de páginas do SDK com indexação baseada em zero, por exemplo, `pdfDocument.Pages[2]`, pois o índice 2 corresponde à terceira página.

**Q: Posso girar uma página em um ângulo diferente de 180 graus?**  
A: A propriedade de rotação aceita apenas os quatro valores padrão 0, 90, 180 e 270 graus; qualquer outro valor é arredondado para o ângulo permitido mais próximo.

**Q: A rotação da página modifica o arquivo original automaticamente?**  
A: A rotação é aplicada apenas ao `PdfDocument` em memória; você deve chamar `pdfDocument.Save(\"output.pdf\")` (ou um método de salvamento semelhante) para gravar as alterações em um novo arquivo, deixando a origem inalterada.

**Q: O que acontece com anotações ou campos de formulário após a página ser girada?**  
A: O SDK recalcula automaticamente as posições das anotações e dos campos de formulário para que permaneçam corretamente alinhados com a nova orientação.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}