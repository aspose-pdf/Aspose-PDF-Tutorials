---
date: '2026-05-28'
description: Aprenda como definir o single page view PDF, alterar as viewer preferences,
  editar bookmarks e configurar as PDF settings usando Aspose.PDF for Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Single page view PDF no Java – Alterar Layout e Editar Bookmarks
url: /pt/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Visualização de Página Única PDF em Java – Alterar Layout e Editar Marcadores

## Introdução
Quando os leitores abrem um PDF grande, o layout padrão do visualizador pode rolar continuamente, dificultando a concentração em uma única página. Ao configurar a configuração **single page view pdf**, você força o visualizador a exibir uma página por vez, o que é ideal para relatórios, e‑books e catálogos. Neste tutorial você também aprenderá a editar marcadores PDF existentes, definir destinos de marcadores ao criar um documento e ajustar outras preferências do visualizador usando Aspose.PDF para Java. Ao final, você terá controle total sobre a navegação, a precisão dos marcadores e o layout na tela.

**O que você aprenderá**
- Como editar marcadores PDF existentes para que apontem para o início de uma página.  
- Como definir destinos de marcadores ao criar um PDF.  
- Como alterar as preferências do visualizador, como layout de página única.  
- Dicas práticas para carregar um documento PDF em Java e otimizar o desempenho.

### Respostas Rápidas
- **Qual é a maneira principal de habilitar a visualização de página única PDF?** Call `PdfContentEditor.changeViewerPreference()` with `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Os destinos de marcadores podem ser editados após a geração de um PDF?** Yes – load the document, retrieve the outline, and assign a new `ExplicitDestination`.  
- **Preciso de uma licença para esses recursos?** A free trial works for evaluation; a full license removes all limitations.  
- **Qual dependência Maven é necessária?** `com.aspose:aspose-pdf:25.3` (or later).  
- **Isso é compatível com Java 11 ou superior?** Absolutely – Aspose.PDF supports Java 8+.

## O que é “alterar layout de página PDF”?
Alterar o layout de página PDF controla como as páginas são exibidas em um visualizador — página única, contínua, visualização de duas páginas etc. Habilitar **single page view pdf** melhora a legibilidade de documentos longos e garante que cada página seja apresentada isoladamente, o que é especialmente útil em dispositivos móveis e tablets.

## Por que editar marcadores PDF e definir destinos de marcadores?
Os marcadores funcionam como um índice dinâmico. Destinos precisos permitem que os leitores pulem diretamente para a seção desejada, eliminando rolagens extras e reduzindo a frustração do usuário. Isso resulta em uma experiência de navegação mais suave e maior satisfação para manuais técnicos, catálogos de produtos e livros digitais.

## Pré-requisitos
- **Bibliotecas e Dependências**: Aspose.PDF for Java v25.3 ou posterior.  
- **Ambiente**: JDK 8 ou mais recente, ferramenta de build Maven ou Gradle.  
- **Conhecimento**: Programação Java básica e familiaridade com conceitos de PDF.

## Configurando Aspose.PDF para Java
### Instalação Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Instalação Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Aquisição de Licença**: Start with a free trial or request a temporary license for full‑feature access. Consider purchasing a permanent license for production use.

### Inicialização Básica
A classe `Document` é o objeto central do Aspose.PDF que representa um arquivo PDF na memória. Após criar uma instância, todas as operações de leitura/escrita fluem através desse objeto.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Guia de Implementação
### Como Alterar o Layout de Página PDF em Java
**Visão geral**: Ajuste as preferências do visualizador para exibir as páginas da maneira desejada.

#### Inicializando PdfContentEditor
`PdfContentEditor` is a utility class that lets you modify viewer settings without rewriting the whole document.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Alterando Preferências do Visualizador
To enable **single page view pdf**, invoke `changeViewerPreference()` with the appropriate enum value. This call updates the PDF’s internal viewer preference dictionary.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Salvando o Documento Atualizado
After modifying preferences, call `save()` to write the changes back to disk.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Como Editar Marcadores PDF
Answer: To modify existing bookmarks, load the PDF with `Document`, retrieve its outline collection, locate the desired `OutlineItem`, and assign a new `ExplicitDestination` that points to the correct page and coordinates. After updating each bookmark, save the document to persist changes. This ensures users are directed precisely to the intended sections without extra scrolling.

#### Acessando Marcadores
The `OutlineItemCollection` represents the hierarchical bookmark tree. Retrieve it from the `Document` object to work with individual entries.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Definindo um Novo Destino
An `ExplicitDestination` defines the exact page and location a bookmark should jump to. Assign it to the `Destination` property of the outline item.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Salvando Alterações
Persist the updated bookmark tree by calling `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Como Definir Destino de Marcador ao Criar um PDF
Answer: When generating a PDF, you can create bookmarks on the fly by instantiating `OutlineItem` objects, setting their titles, and defining an `ExplicitDestination` that targets a specific page and view mode. Add each bookmark to the document’s outline collection before saving, so the resulting file contains a ready‑to‑use navigation tree.

#### Criando e Configurando Marcador
`OutlineItem` represents a single bookmark entry in the PDF outline. When building a PDF from scratch, instantiate a new `OutlineItem` and add it to the document’s outline collection.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definindo Destino do Marcador
Use `ExplicitDestination.createFitH(page, top)` to position the view at the top of the target page.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Adicionando e Salvando o PDF
Finally, add the bookmark to the outline and save the document.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Aplicações Práticas
1. **Livros Digitais** – Garantir que o marcador de cada capítulo chegue ao topo da página para uma experiência de leitura fluida.  
2. **Manuais Técnicos** – Navegação precisa ajuda engenheiros a encontrar seções rapidamente, especialmente em PDFs grandes.  
3. **Catálogos de Produtos** – Layout de página única torna a navegação em catálogos em tablets mais intuitiva.

## Considerações de Desempenho
- **Otimização de Recursos**: Aspose.PDF pode processar PDFs de até 2 GB sem carregar o arquivo inteiro na memória, graças à sua arquitetura de streaming. Use `Document.optimizeResources()` para reduzir ainda mais a pegada de memória.  
- **Gerenciamento de Memória Java**: Feche explicitamente os streams e deixe o coletor de lixo liberar os objetos após o processamento para evitar vazamentos de memória.

## Problemas Comuns e Soluções
- **Marcadores Não Atualizando**: Verify you’re modifying the correct outline index (`get_Item(1)` refers to the first top‑level bookmark).  
- **Preferência de Visualizador Não Aplicada**: Ensure you call `editor.save()` after changing preferences; otherwise changes remain only in memory.  
- **Exceções de Licença**: A trial license may add watermarks; obtain a full license for production.

## Perguntas Frequentes
**Q: Qual é a maneira mais fácil de carregar um documento PDF em Java?**  
A: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects the file format.

**Q: Posso mudar o layout da página sem usar PdfContentEditor?**  
A: Yes, you can set viewer preferences directly on the `Document` object via `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: Alterar o layout do visualizador afeta a impressão?**  
A: Viewer layout only influences on‑screen display; it does not alter the printed output.

**Q: Existem limites para o número de marcadores que posso criar?**  
A: No explicit limit, but extremely large outline trees may impact performance; keep them organized.

**Q: Como garantir que os destinos dos marcadores estejam precisos após adicionar ou remover páginas?**  
A: Re‑calculate destinations using the current page indices after any structural changes.

## Recursos
- **Documentação**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Compra**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Teste Gratuito**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Licença Temporária**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Last Updated:** 2026-05-28  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose

## Tutoriais Relacionados

- [Como Alterar Preferências do Visualizador PDF Usando Aspose.PDF para Java: Um Guia Abrangente](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Como Criar Marcadores PDF e Gerenciar Navegação Usando Aspose.PDF para Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Tutoriais de Marcadores PDF e Navegação para Aspose.PDF Java](/pdf/java/bookmarks-navigation/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}