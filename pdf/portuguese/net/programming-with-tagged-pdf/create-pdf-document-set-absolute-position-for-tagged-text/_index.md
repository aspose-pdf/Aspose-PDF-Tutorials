---
category: general
date: 2026-03-24
description: Crie um documento PDF e aprenda como definir posição absoluta para texto
  marcado. Este tutorial mostra como adicionar o elemento span, como inserir conteúdo
  marcado e posicionar texto na página.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: pt
og_description: Crie um documento PDF e veja instantaneamente como definir posição
  absoluta, adicionar um elemento span e posicionar texto na página com conteúdo PDF
  marcado.
og_title: Criar documento PDF – Posicionamento absoluto de texto marcado
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Criar documento PDF – Definir posição absoluta para texto marcado
url: /pt/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento PDF – Definir Posição Absoluta para Texto Marcado

Já precisou **criar documento pdf** que contenha texto marcado e acessível posicionado exatamente onde deseja? Talvez esteja construindo um PDF no estilo de formulário onde o rótulo deve ficar em uma coordenada precisa, ou gerando um certificado e o nome precisa alinhar perfeitamente com uma imagem de fundo.  

Neste guia vamos percorrer um exemplo completo e executável que mostra **como adicionar conteúdo marcado**, **definir posição absoluta** e **adicionar elemento span** para que você possa **posicionar texto na página** sem adivinhações. Sem referências externas — apenas o código que você pode copiar‑colar, mais explicações do “porquê” de cada linha.

## Pré‑requisitos

- .NET 6+ (ou .NET Framework 4.6+) com compilador C#  
- Aspose.Pdf for .NET (versão mais recente no momento da escrita, 23.12) instalado via NuGet  
- Familiaridade básica com a sintaxe C#  

Se você tem isso, vamos começar.

---

## Criar Documento PDF – Definindo a Posição Absoluta

A primeira coisa que fazemos é instanciar um `Document` vazio. Esse objeto representa todo o arquivo PDF e nos dá acesso à árvore de conteúdo marcado.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Por que isso importa:**  
`Document` é a raiz da estrutura PDF. Ao criá‑lo primeiro garantimos que exista uma “tela” tanto para elementos visuais (páginas, gráficos) quanto para a estrutura lógica (tags). A instrução `using` garante que o arquivo seja descartado corretamente, evitando vazamentos de manipuladores de arquivo no Windows.

---

## Habilitar Conteúdo Marcado (Como Adicionar Marcado)

Antes de inserir quaisquer elementos marcados, o documento deve ser marcado como *tagged*. O Aspose.Pdf cria automaticamente um objeto `TaggedContent`, mas ainda é necessário ativar a flag.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**O que acontece nos bastidores?**  
Definir `TaggedContent` como `true` informa aos leitores PDF que o arquivo contém uma árvore de estrutura lógica. Isso é crucial para leitores de tela e para que o método `SetPosition` funcione corretamente em um elemento span.

---

## Obter o Elemento Raiz da Árvore de Conteúdo Marcado

O elemento raiz é o ponto de entrada para todas as tags estruturais (como `<Document>`, `<Section>`, `<Span>`). Pense nele como o “corpo” invisível do PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Por que precisamos da raiz:**  
Todas as tags subsequentes devem ser anexadas em algum lugar da árvore; caso contrário, não aparecerão na hierarquia de acessibilidade.

---

## Adicionar um Elemento Span – O Bloco de Construção para Texto Inline

Um *span* é o equivalente PDF de um `<span>` HTML — perfeito para pequenos trechos de texto que você deseja posicionar com precisão.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Nota de design:**  
Se precisar de formatação mais rica (negrito, itálico, hyperlinks), pode envolver o span em um `<Paragraph>` ou usar objetos `TextFragment` posteriormente. Para posicionamento absoluto, um span simples é o mais leve.

---

## Definir Posição Absoluta – X=100, Y=200

Agora vem a parte divertida: colocar o span em uma localização exata na página. O sistema de coordenadas começa no canto inferior‑esquerdo (0,0) e usa pontos (1 pt ≈ 1/72 pol).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Por que posicionamento absoluto?**  
Quando você precisa de layout pixel‑perfect — pense em certificados, faturas ou formulários — o fluxo relativo (como texto da esquerda para a direita) não é suficiente. `SetPosition` ignora o fluxo normal de texto e fixa o elemento onde você especificar.

---

## Adicionar Texto ao Span

Com o span posicionado, agora inserimos a string real.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Dica:**  
Se precisar de caracteres Unicode ou scripts da direita para a esquerda, basta passar a string; o Aspose.Pdf trata a codificação automaticamente.

---

## Anexar o Span ao Elemento Raiz

Por fim, conectamos o span à árvore lógica do documento para que ele faça parte do PDF final.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**E se esquecer este passo?**  
O span existirá na memória, mas nunca será serializado no arquivo, então você não verá texto e a árvore de acessibilidade ficará incompleta.

---

## Exemplo Completo e Executável

Abaixo está o programa completo que pode ser colocado em um aplicativo console. Ele cria um PDF de uma página, adiciona um span marcado em (100, 200) e salva o arquivo como `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Saída esperada:**  
Abra `TaggedPositioned.pdf` em qualquer visualizador (Adobe Acrobat, Foxit, etc.). Você verá a frase **“Positioned tagged text”** exatamente 100 pt da borda esquerda e 200 pt da borda inferior da página. Se inspecionar o painel *Tags*, um elemento `<Span>` aparecerá sob a raiz do documento, confirmando que o conteúdo está corretamente marcado.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar posicionar texto em uma página específica que não seja a primeira?

Adicione a página desejada (`var page = pdfDocument.Pages[3];`) antes de chamar `SetPosition`. O span será anexado automaticamente ao contexto da página ativa.

### Posso definir a posição em polegadas ou centímetros?

`SetPosition` aceita pontos. Converta usando as fórmulas:  
- **Polegadas → pontos:** `points = inches * 72`  
- **Centímetros → pontos:** `points = cm * 28.3465`

### Como altero a fonte ou a cor do span?

Após criar o span, você pode obter seu `TextState` e modificá‑lo:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### E se o documento já possuir tags existentes?

Ainda é possível criar um novo span e anexá‑lo a qualquer elemento existente (`rootElement`, um `<Section>` específico, etc.). Apenas garanta que mantenha uma hierarquia lógica — leitores de tela esperam uma árvore bem estruturada.

### Isso funciona com conformidade PDF/A ou PDF/UA?

Sim. PDFs marcados são requisito central para PDF/UA. Se precisar de PDF/A, chame `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` após montar o conteúdo.

---

## Dicas Profissionais & Armadilhas

- **Dica pro:** Sempre adicione uma página antes de posicionar conteúdo. Sem página, `SetPosition` falha silenciosamente porque não há onde renderizar.
- **Cuidado com unidades:** Misturar pixels de um design UI com pontos PDF deslocará seu texto. Verifique a conversão.
- **Sugestão de desempenho:** Se estiver gerando milhares de PDFs, reutilize uma única instância de `Document` e chame `pdfDocument.Pages.Clear()` entre as execuções para evitar alocação excessiva de memória.
- **Lembrete de acessibilidade:** Marcar não é apenas um “nice‑to‑have”; muitas regulamentações (Seção 508, EN 301 549) exigem isso. Usar `CreateSpanElement` garante que o texto seja descoberto por tecnologias assistivas.

---

## Conclusão

Acabamos de **criar documento pdf** do zero, **definir posição absoluta**, **adicionar elemento span** e demonstrar **como adicionar conteúdo marcado** para que você possa **posicionar texto na página** com precisão pixel‑perfect. O exemplo completo está pronto para ser executado, e a explicação cobriu tanto o *como* quanto o *porquê* — exatamente o que desenvolvedores (e assistentes de IA) buscam quando precisam de uma solução confiável.

Em seguida, você pode explorar:

- Adicionar imagens atrás do texto posicionado para certificados com marca d’água.  
- Usar `CreateParagraphElement` para blocos de múltiplas linhas que ainda precisem de posicionamento absoluto.  
- Exportar para PDF/UA para atender a auditorias de acessibilidade rigorosas.  

Sinta‑se à vontade para ajustar coordenadas, fontes ou cores — a experimentação é o caminho mais rápido para dominar a geração de PDFs marcados. Se encontrar algum problema, deixe um comentário abaixo; boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}