---
"date": "2025-04-14"
"description": "Aprenda a anotar arquivos PDF em Java usando o Aspose.PDF adicionando anotações tachadas. Siga este guia para obter instruções passo a passo sobre como modificar o conteúdo do PDF."
"title": "Como anotar PDFs em Java com anotações tachadas usando Aspose.PDF"
"url": "/pt/java/forms-annotations/annotate-pdfs-java-strikeout-aspose-pdf/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Como anotar PDFs em Java com anotações tachadas usando Aspose.PDF

Libere todo o potencial da manipulação de PDFs com o Aspose.PDF para Java, aprendendo a anotar e salvar arquivos PDF com anotações tachadas. Este guia completo orientará você na inicialização de um documento, na busca por fragmentos de texto, na criação de anotações e no salvamento do documento anotado.

## Introdução

Navegar pela complexidade dos PDFs pode ser desafiador, seja para extrair dados ou modificar conteúdo. Se você deseja adicionar anotações visuais, como tachados, diretamente em seus aplicativos Java usando o Aspose.PDF para Java, este guia é perfeito. Você aprenderá a integrar perfeitamente a funcionalidade PDF aos seus projetos.

### O que você aprenderá
- Como inicializar e carregar um documento PDF com Aspose.PDF
- Técnicas para pesquisar fragmentos de texto específicos em um PDF
- Etapas para criar e configurar anotações de strikeout
- Métodos para salvar o documento PDF modificado

Vamos analisar os pré-requisitos que você precisa antes de começar.

## Pré-requisitos

### Bibliotecas, versões e dependências necessárias
Para seguir este tutorial, certifique-se de ter:
- Java Development Kit (JDK) 8 ou posterior instalado.
- Um IDE como IntelliJ IDEA ou Eclipse para editar seu código Java.

Usaremos o Aspose.PDF para Java versão 25.3. Você pode incorporá-lo ao seu projeto via Maven ou Gradle, conforme mostrado abaixo.

### Requisitos de configuração do ambiente
Certifique-se de que seu ambiente esteja configurado para lidar com as dependências e que você tenha acesso a um diretório onde seus documentos PDF de entrada são armazenados, juntamente com um diretório de saída para salvar arquivos anotados.

### Pré-requisitos de conhecimento
Familiaridade com programação Java e conhecimento básico de manipulação de PDFs programaticamente serão benéficos.

## Configurando Aspose.PDF para Java
Integrar o Aspose.PDF ao seu projeto Java é simples. Veja como você pode adicioná-lo usando Maven ou Gradle:

**Especialista**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Aquisição de Licença
Aspose.PDF é uma biblioteca comercial, mas você pode começar obtendo uma avaliação gratuita ou uma licença temporária para fins de avaliação. Visite o [Página de compra Aspose](https://purchase.aspose.com/buy) para explorar suas opções.

## Guia de Implementação
Dividiremos nossa implementação em seções com base na funcionalidade: inicialização do documento, pesquisa de fragmentos de texto, criação de anotações e salvamento do documento.

### Inicialização e carregamento de documentos
#### Visão geral
Primeiro, precisamos carregar um arquivo PDF usando o Aspose.PDF para Java. Esta etapa envolve a inicialização do `Document` classe com o caminho para seu PDF.

**Passo 1**Importe as classes necessárias.
```java
import com.aspose.pdf.Document;
```

**Passo 2**: Defina seu diretório de documentos e inicialize o objeto Document.
```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document(dataDir + "/input.pdf");
```
Este código carrega um PDF de `dataDir` em um `Document` por exemplo, permitindo operações posteriores.

### Absorção de Fragmentos de Texto
#### Visão geral
Pesquisar texto em seu PDF é essencial antes de criar anotações. Usaremos o `TextFragmentAbsorber`.

**Passo 1**: Importe a classe.
```java
import com.aspose.pdf.TextFragmentAbsorber;
```

**Passo 2**: Crie uma instância de TextFragmentAbsorber com a consulta de pesquisa.
```java
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Sample");
```

**Etapa 3**: Aceite o absorvedor em cada página para encontrar todos os fragmentos de texto correspondentes.
```java
for (int i = 1; i <= document.getPages().size(); i++) {
    document.getPages().get_Item(i).accept(textFragmentAbsorber);
}
```
Este loop pesquisa em cada página, coletando correspondências para "Amostra".

### Recuperar coleção de fragmentos de texto
#### Visão geral
Depois que os fragmentos de texto são absorvidos, nós os recuperamos em uma coleção para processar anotações.

**Passo 1**: Importe a classe necessária.
```java
import com.aspose.pdf.TextFragmentCollection;
```

**Passo 2**:Pegue a coleção do absorvedor.
```java
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.getTextFragments();
```
Isso nos dá acesso a todas as instâncias encontradas de "Sample".

### Criar anotação tachada
#### Visão geral
Adicionaremos uma anotação tachada sobre cada fragmento de texto identificado, destacando-o ou marcando-o visualmente.

**Passo 1**Importe as classes necessárias.
```java
import com.aspose.pdf.StrikeOutAnnotation;
import com.aspose.pdf.Rectangle;
import com.aspose.pdf.Border;
import com.aspose.pdf.Color;
import com.aspose.pdf.Page;
```

**Passo 2**: Percorra os fragmentos de texto e crie anotações.
```java
for (int j = 1; j <= textFragmentCollection.size(); j++) {
    com.aspose.pdf.TextFragment textFragment = textFragmentCollection.get_Item(j);

    // Defina a área retangular para anotação com base na localização do fragmento de texto.
    Rectangle rect = new Rectangle((float) textFragment.getPosition().getXIndent(),
                                   (float) textFragment.getPosition().getYIndent(),
                                   (float) textFragment.getPosition().getXIndent() + (float) textFragment.getRectangle().getWidth(),
                                   (float) textFragment.getPosition().getYIndent() + (float) textFragment.getRectangle().getHeight());

    // Crie e configure a anotação de eliminação.
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.getPage(), rect);
    strikeOut.setOpacity(0.80f);  // Defina a opacidade para 80%
    strikeOut.setBorder(new Border(strikeOut));  // Inicializar uma borda para a anotação
    strikeOut.setColor(Color.getRed());  // Definir cor da anotação para vermelho

    // Adicione a anotação à página.
    textFragment.getPage().getAnnotations().add(strikeOut);
}
```
Cada anotação é configurada com configurações de opacidade, borda e cor antes de ser adicionada.

### Salvar documento com anotações
#### Visão geral
Depois de criar as anotações, salvamos o documento anotado.

**Passo 1**: Importe as classes necessárias caso ainda não tenha feito isso.
```java
import com.aspose.pdf.Document;
```

**Passo 2**: Defina o diretório de saída e salve o documento.
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
document.save(outputDir + "/StrikeOut.pdf");
```
Esta etapa finaliza seu PDF anotado com todas as modificações intactas.

## Aplicações práticas
O Aspose.PDF para Java pode ser usado em vários cenários, como:
1. **Processos de revisão de documentos**Automatize o processo de revisão marcando programaticamente as alterações necessárias.
2. **Manuseio de documentos legais**: Anote rapidamente contratos ou acordos com as redações ou edições necessárias.
3. **Criação de Conteúdo Educacional**: Aprimore os materiais de aprendizagem eliminando informações desatualizadas e anotando correções.

## Considerações de desempenho
Para garantir um desempenho ideal:
- Use estruturas de dados eficientes ao lidar com grandes coleções de fragmentos de texto.
- Gerencie a memória de forma eficaz, especialmente em ambientes com recursos limitados.
- Atualize regularmente para a versão mais recente do Aspose.PDF para obter recursos aprimorados e correções.

## Conclusão
Você aprendeu com sucesso a usar o Aspose.PDF para Java para anotar PDFs com linhas tachadas. Ao seguir este guia, você deu um passo significativo rumo à automatização dos seus processos de processamento de PDF. Explore mais, experimentando outros tipos de anotação ou integrando funcionalidades adicionais da biblioteca Aspose.

Pronto para ir mais longe? Visite o [Documentação Aspose](https://reference.aspose.com/pdf/java/) para recursos e funcionalidades mais avançados.

## Seção de perguntas frequentes
**1. Como instalo o Aspose.PDF no meu projeto Java?**
Você pode adicioná-lo por meio de dependências do Maven ou Gradle, conforme mostrado neste tutorial. Certifique-se de que seu IDE esteja configurado para reconhecer essas configurações.

**2. Posso fazer anotações em PDF sem ser com tachados usando o Aspose.PDF para Java?**
Sim, você pode criar várias anotações, como destaques, sublinhados e muito mais.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}