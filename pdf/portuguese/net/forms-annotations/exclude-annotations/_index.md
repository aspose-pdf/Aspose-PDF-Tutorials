---
title: Comparação PDF Lado a Lado Excluindo Anotações com Aspose.Pdf for .NET
weight: 101
limit:
description: Guia passo a passo para comparar PDFs e excluir áreas de anotação usando Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guia passo a passo para comparar PDFs e excluir áreas de anotação usando
    Aspose.Pdf for .NET.
  headline: Comparação PDF Lado a Lado Excluindo Anotações com Aspose.Pdf for .NET
  type: TechArticle
- description: Guia passo a passo para comparar PDFs e excluir áreas de anotação usando
    Aspose.Pdf for .NET.
  name: Comparação PDF Lado a Lado Excluindo Anotações com Aspose.Pdf for .NET
  steps:
  - name: Defina os caminhos dos arquivos para o PDF principal, o PDF secundário e
      o PDF de diferenças de saída.
    text: Defina os caminhos dos arquivos para o PDF principal, o PDF secundário e
      o PDF de diferenças de saída.
  - name: Verifique se ambos os arquivos PDF de entrada existem e interrompa com uma
      mensagem de erro se algum estiver ausente.
    text: Verifique se ambos os arquivos PDF de entrada existem e interrompa com uma
      mensagem de erro se algum estiver ausente.
  - name: Abra os dois arquivos PDF como objetos Document (pdfA e pdfB) dentro de
      um bloco using para que sejam descartados automaticamente.
    text: Abra os dois arquivos PDF como objetos Document (pdfA e pdfB) dentro de
      um bloco using para que sejam descartados automaticamente.
  - name: Colete os retângulos delimitadores de todas as anotações em pdfA e armazene-os
      em ignoredRectsA.
    text: Colete os retângulos delimitadores de todas as anotações em pdfA e armazene-os
      em ignoredRectsA.
  - name: Colete os retângulos delimitadores de todas as anotações em pdfB e armazene-os
      em ignoredRectsB.
    text: Colete os retângulos delimitadores de todas as anotações em pdfB e armazene-os
      em ignoredRectsB.
  - name: Crie um objeto SideBySideComparisonOptions e atribua os retângulos de anotação
      coletados anteriormente a ExcludeAreas1 e ExcludeAreas2, de modo que essas regiões
      sejam ignoradas durante a comparação.
    text: Crie um objeto SideBySideComparisonOptions e atribua os retângulos de anotação
      coletados anteriormente a ExcludeAreas1 e ExcludeAreas2, de modo que essas regiões
      sejam ignoradas durante a comparação.
  - name: Execute a comparação PDF lado a lado usando os dois objetos Document e as
      opções configuradas, gravando o resultado em outputPdf.
    text: Execute a comparação PDF lado a lado usando os dois objetos Document e as
      opções configuradas, gravando o resultado em outputPdf.
  - name: Descartar os objetos Document e sair do bloco using.
    text: Descartar os objetos Document e sair do bloco using.
  - name: Imprima uma mensagem de confirmação indicando que a comparação foi concluída
      e onde o PDF de diferenças foi salvo.
    text: Imprima uma mensagem de confirmação indicando que a comparação foi concluída
      e onde o PDF de diferenças foi salvo.
  type: HowTo
- questions:
  - answer: Sim. O código simplesmente não adiciona retângulos à lista `ignoredRects`
      correspondente, de modo que `ExcludeAreas1`/`ExcludeAreas2` recebem um array
      vazio e o comparador processa a página inteira.
    question: O que acontece se uma página PDF não tiver anotações – a comparação
      ainda funcionará?
  - answer: Defina `ExcludeAreas1` (ou `ExcludeAreas2`) com os retângulos coletados
      e deixe a outra propriedade como um array vazio; o comparador ignorará as regiões
      apenas no documento especificado.
    question: Posso excluir apenas as anotações de um documento mantendo as anotações
      do outro no diff?
  - answer: Retângulos sobrepostos são mesclados internamente pelo comparador, de
      modo que limites de anotações sobrepostas são excluídos com segurança, sem contagem
      dupla.
    question: Retângulos de anotação sobrepostos causam algum problema com `ExcludeAreas`?
  - answer: Sim, defina `compareOpts.ExcludeTables = true;` – essa flag funciona juntamente
      com `ExcludeAreas1`/`ExcludeAreas2` para também ignorar regiões de tabelas.
    question: Existe uma maneira de excluir tabelas além das anotações usando o mesmo
      objeto de opções?
  - answer: O código verifica `if (a != null && a.Rect != null)` antes de adicionar
      à lista, portanto retângulos nulos são simplesmente ignorados e nenhuma exceção
      é lançada.
    question: E se a propriedade `Rect` de uma anotação for nula – o código lançará
      uma exceção?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Comparar PDFs sem Anotações
og_description: Execute uma comparação PDF lado a lado que ignora todas as marcas de anotação.
og_image_alt: Guia que mostra uma comparação PDF lado a lado que exclui regiões de anotação usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparação PDF Lado a Lado Excluindo Anotações com Aspose.Pdf
Este tutorial mostra como comparar dois arquivos PDF usando Aspose.Pdf for .NET ignorando qualquer conteúdo de anotação. Ele extrai as caixas delimitadoras de todas as anotações de cada documento, alimenta essas regiões em SideBySideComparisonOptions e, em seguida, executa uma comparação lado a lado. O resultado é um PDF de diferenças que destaca apenas as alterações que não são anotações.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: O que acontece se uma página PDF não tiver anotações – a comparação ainda funcionará?**  
A: Sim. O código simplesmente não adiciona retângulos à lista `ignoredRects` correspondente, de modo que `ExcludeAreas1`/`ExcludeAreas2` recebem um array vazio e o comparador processa a página inteira.

**Q: Posso excluir apenas as anotações de um documento mantendo as anotações do outro no diff?**  
A: Defina `ExcludeAreas1` (ou `ExcludeAreas2`) com os retângulos coletados e deixe a outra propriedade como um array vazio; o comparador ignorará as regiões apenas no documento especificado.

**Q: Retângulos de anotação sobrepostos causam algum problema com `ExcludeAreas`?**  
A: Retângulos sobrepostos são mesclados internamente pelo comparador, de modo que limites de anotações sobrepostas são excluídos com segurança, sem contagem dupla.

**Q: Existe uma maneira de excluir tabelas além das anotações usando o mesmo objeto de opções?**  
A: Sim, defina `compareOpts.ExcludeTables = true;` – essa flag funciona juntamente com `ExcludeAreas1`/`ExcludeAreas2` para também ignorar regiões de tabelas.

**Q: E se a propriedade `Rect` de uma anotação for nula – o código lançará uma exceção?**  
A: O código verifica `if (a != null && a.Rect != null)` antes de adicionar à lista, portanto retângulos nulos são simplesmente ignorados e nenhuma exceção é lançada.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}