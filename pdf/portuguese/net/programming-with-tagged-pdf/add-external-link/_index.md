---
title: Adicionar Link Externo Marcado com Tooltip ao PDF usando Aspose.Pdf para .NET
weight: 440
limit:
description: Aprenda a adicionar um hyperlink externo marcado com texto de exibição e tooltip a um PDF usando Aspose.Pdf para .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Aprenda a adicionar um hyperlink externo marcado com texto de exibição
    e tooltip a um PDF usando Aspose.Pdf para .NET.
  headline: Adicionar Link Externo Marcado com Tooltip ao PDF usando Aspose.Pdf para
    .NET
  type: TechArticle
- description: Aprenda a adicionar um hyperlink externo marcado com texto de exibição
    e tooltip a um PDF usando Aspose.Pdf para .NET.
  name: Adicionar Link Externo Marcado com Tooltip ao PDF usando Aspose.Pdf para .NET
  steps:
  - name: Defina os caminhos para o PDF de origem e o arquivo de resultado.
    text: Defina os caminhos para o PDF de origem e o arquivo de resultado.
  - name: Verifique se o PDF de origem existe e interrompa a execução se não for encontrado.
    text: Verifique se o PDF de origem existe e interrompa a execução se não for encontrado.
  - name: Abra o documento PDF dentro de um bloco using para garantir a liberação
      adequada.
    text: Abra o documento PDF dentro de um bloco using para garantir a liberação
      adequada.
  - name: Obtenha o gerenciador de conteúdo marcado (tagged‑content) para o documento
      aberto.
    text: Obtenha o gerenciador de conteúdo marcado (tagged‑content) para o documento
      aberto.
  - name: Defina o idioma do documento como English (US) e atribua ao PDF um título
      derivado do nome do arquivo.
    text: Defina o idioma do documento como English (US) e atribua ao PDF um título
      derivado do nome do arquivo.
  - name: Recupere o elemento raiz da árvore de estrutura lógica ao qual novos elementos
      serão adicionados.
    text: Recupere o elemento raiz da árvore de estrutura lógica ao qual novos elementos
      serão adicionados.
  - name: Crie um elemento de link, defina seu texto exibido, URL de destino e título
      da tooltip, e então insira‑o na estrutura do documento.
    text: Crie um elemento de link, defina seu texto exibido, URL de destino e título
      da tooltip, e então insira‑o na estrutura do documento.
  - name: Salve o PDF atualizado no arquivo de resultado especificado.
    text: Salve o PDF atualizado no arquivo de resultado especificado.
  - name: Exiba uma mensagem de confirmação indicando onde o PDF modificado foi salvo.
    text: Exiba uma mensagem de confirmação indicando onde o PDF modificado foi salvo.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` retorna o conteúdo marcado existente se o documento
      já estiver marcado; ele não cria uma árvore duplicada.'
    question: E se o PDF de origem já estiver marcado – a chamada a `pdfDoc.TaggedContent`
      criará uma nova árvore de tags ou reutilizará a existente?
  - answer: Sim – localize o `StructureElement` desejado (por exemplo, um `Div` ou
      `Paragraph` em uma página) através da árvore de estrutura lógica e chame `AppendChild(externalLink)`
      nesse elemento.
    question: Posso colocar o hyperlink em uma página específica em vez de adicioná‑lo
      ao elemento raiz?
  - answer: A tooltip é exibida somente se `externalLink.Title` for definido antes
      de `pdfDoc.Save`; defini‑la após a gravação não tem efeito no PDF já escrito.
    question: A propriedade `Title` de `LinkElement` é necessária para que a tooltip
      apareça, e ela pode ser definida após chamar `Save`?
  - answer: Atribua um `FileSpecification` (por exemplo, `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`)
      a `externalLink.Hyperlink` em vez de usar `WebHyperlink`.
    question: Como criar um link para um arquivo local em vez de uma URL da web?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Inserir um Link Externo Marcado com Tooltip em um PDF
og_description: Incorpore um hyperlink acessível com texto visível e tooltip no seu PDF usando Aspose.Pdf para .NET.
og_image_alt: Guia que mostra como adicionar um hyperlink externo marcado com tooltip a um PDF usando Aspose.Pdf para .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Link Externo Marcado com Tooltip ao PDF usando Aspose.Pdf para .NET
Este tutorial mostra como abrir um PDF existente com Aspose.Pdf para .NET, criar um hyperlink externo marcado que inclui texto de exibição visível e um título de tooltip, inserir o link na estrutura lógica do documento e salvar o arquivo atualizado. Ao seguir os passos, você produzirá um PDF acessível onde o link faz parte da hierarquia de tags e fornece contexto adicional aos leitores.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: E se o PDF de origem já estiver marcado – a chamada a `pdfDoc.TaggedContent` criará uma nova árvore de tags ou reutilizará a existente?**  
A: `pdfDoc.TaggedContent` retorna o conteúdo marcado existente se o documento já estiver marcado; ele não cria uma árvore duplicada.

**Q: Posso colocar o hyperlink em uma página específica em vez de adicioná‑lo ao elemento raiz?**  
A: Sim – localize o `StructureElement` desejado (por exemplo, um `Div` ou `Paragraph` em uma página) através da árvore de estrutura lógica e chame `AppendChild(externalLink)` nesse elemento.

**Q: A propriedade `Title` de `LinkElement` é necessária para que a tooltip apareça, e ela pode ser definida após chamar `Save`?**  
A: A tooltip é exibida somente se `externalLink.Title` for definido antes de `pdfDoc.Save`; defini‑la após a gravação não tem efeito no PDF já escrito.

**Q: Como criar um link para um arquivo local em vez de uma URL da web?**  
A: Atribua um `FileSpecification` (por exemplo, `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`) a `externalLink.Hyperlink` em vez de usar `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}