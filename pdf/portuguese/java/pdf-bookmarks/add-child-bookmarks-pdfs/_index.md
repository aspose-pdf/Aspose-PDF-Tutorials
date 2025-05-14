---
"description": "Aprenda a aprimorar documentos PDF com marcadores secundários usando o Aspose.PDF para Java. Guia passo a passo com exemplos de código para melhor navegação e organização."
"linktitle": "Adicionar marcadores secundários aos PDFs"
"second_title": "API de processamento de PDF Java Aspose.PDF"
"title": "Adicionar marcadores secundários aos PDFs"
"url": "/pt/java/pdf-bookmarks/add-child-bookmarks-pdfs/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar marcadores secundários aos PDFs


## Introdução à adição de marcadores secundários em PDFs

Neste artigo, exploraremos como adicionar marcadores secundários a documentos PDF usando o Aspose.PDF para Java. Os marcadores secundários são uma maneira conveniente de organizar e navegar pelo conteúdo de um documento PDF, facilitando a localização de seções ou tópicos específicos dentro do documento.

## Pré-requisitos

Antes de começarmos a implementação, certifique-se de ter os seguintes pré-requisitos em vigor:

- Ambiente de desenvolvimento Java instalado no seu sistema.
- Biblioteca Aspose.PDF para Java. Você pode baixá-la em [aqui](https://releases.aspose.com/pdf/java/).

## Configurando o ambiente

1. Baixe a biblioteca Aspose.PDF para Java no link fornecido.
2. Adicione a biblioteca ao seu projeto Java.

Agora, vamos começar criando um novo documento PDF e adicionando marcadores filhos a ele passo a passo.

## Criando um novo documento PDF

Para começar, precisamos inicializar um documento PDF e adicionar páginas a ele. Aqui está o trecho de código para começar:

```java
// Inicializar um documento PDF
Document pdfDocument = new Document();

// Adicionar páginas ao PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();
```

Neste exemplo, criamos um novo documento PDF e adicionamos duas páginas a ele.

## Adicionando marcadores dos pais

Os marcadores principais funcionam como as principais seções ou categorias do seu documento PDF. Vamos criar alguns marcadores principais:

```java
// Criar marcadores para os pais
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);
```

Adicionamos dois marcadores principais, "Marcador Principal 1" e "Marcador Principal 2".

## Adicionando marcadores infantis

Agora, é hora de adicionar marcadores filhos aos marcadores pais que criamos anteriormente. Os marcadores filhos representam tópicos ou subseções específicas dentro de cada marcador pai. Veja como fazer isso:

```java
// Adicionar marcadores filhos ao marcador pai 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Adicionar marcadores filhos ao marcador pai 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);
```

Adicionamos marcadores infantis ao "Marcador pai 1" e ao "Marcador pai 2".

## Personalizando a aparência do marcador

Você pode personalizar a aparência dos favoritos alterando seu texto e estilo. Além disso, você pode adicionar ícones aos favoritos para uma melhor representação visual. Veja um exemplo de como fazer isso:

```java
// Personalizar a aparência do marcador
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());
```

Neste exemplo, deixamos o marcador pai em itálico, alteramos a cor do texto do marcador filho para verde e adicionamos um ícone em itálico ao marcador filho.

## Manipulando Eventos

Os favoritos também podem ter ações associadas. Por exemplo, você pode adicionar ações que são acionadas quando um usuário clica em um favorito. Veja como você pode lidar com eventos de clique em favoritos:

```java
// Adicionar uma ação a um marcador
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);
```

Neste código, adicionamos uma ação "Ir para" a um marcador filho que levará o usuário para a segunda página do PDF quando clicado.

## Salvando o PDF

Depois de adicionar todos os marcadores necessários e personalizar sua aparência e ações, você pode salvar o documento PDF modificado:

```java
// Salvar o documento PDF
pdfDocument.save("output.pdf");
```

Seu documento PDF com marcadores infantis agora está pronto.

## Código-fonte completo

Aqui está o código-fonte completo para adicionar marcadores filhos a um documento PDF usando o Aspose.PDF para Java:

```java
// Inicializar um documento PDF
Document pdfDocument = new Document();

// Adicionar páginas ao PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();

// Criar marcadores para os pais
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);

// Adicionar marcadores filhos ao marcador pai 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Adicionar marcadores filhos ao marcador pai 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);

// Personalizar a aparência do marcador
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());

// Adicionar uma ação a um marcador
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);

// Salvar o documento PDF
pdfDocument.save("output.pdf");
```

## Conclusão

Adicionar marcadores secundários a PDFs usando o Aspose.PDF para Java é um recurso poderoso que aprimora a navegação e a organização dos seus documentos. Seguindo os passos descritos neste artigo, você pode criar PDFs bem estruturados com marcadores primários e secundários, personalizar sua aparência e até mesmo adicionar ações para aprimorar a experiência do usuário.

## Perguntas frequentes

### Como posso baixar o Aspose.PDF para Java?

Você pode baixar Aspose.PDF para Java no site [aqui](https://releases.aspose.com/pdf/java/).

### Os marcadores infantis são suportados em todos os visualizadores de PDF?

Sim, os marcadores infantis são suportados pela maioria dos visualizadores de PDF modernos e proporcionam uma experiência de usuário aprimorada para navegar pelos documentos PDF.

### Posso personalizar ainda mais a aparência dos favoritos?

Sim, você pode personalizar a aparência dos favoritos ajustando estilos de texto, cores e ícones para se adequarem ao design do seu documento.

### Que outras ações posso adicionar aos favoritos?

Além das ações "GoTo", você pode adicionar ações como ações "URI" para abrir links da web ou ações "JavaScript" para executar scripts personalizados quando um favorito for clicado.

### O Aspose.PDF para Java é adequado para projetos comerciais?

Sim, o Aspose.PDF para Java é adequado para projetos pessoais e comerciais e oferece uma ampla gama de recursos para manipulação e geração de PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}