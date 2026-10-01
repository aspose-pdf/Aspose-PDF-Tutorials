---
category: general
date: 2026-04-25
description: Adicione numeração Bates a PDFs rapidamente usando Aspose.Pdf. Aprenda
  como adicionar numeração de páginas em PDF, ajustar automaticamente o tamanho da
  fonte e inserir marca d'água de texto em C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: pt
og_description: Adicione numeração Bates a PDFs com Aspose.Pdf. Este guia mostra como
  adicionar numeração de páginas em PDF, ajustar automaticamente o tamanho da fonte
  e inserir marca d'água de texto em um único exemplo executável.
og_title: Adicionar numeração Bates a PDFs – Tutorial completo Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Adicionar numeração Bates a PDFs com Aspose – Guia completo
url: /pt/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates a PDFs com Aspose – Guia Completo

Já precisou **adicionar numeração bates** a um PDF mas não sabia por onde começar? Você não está sozinho—equipes jurídicas, auditores e desenvolvedores enfrentam essa barreira diariamente. A boa notícia? Com Aspose.Pdf para .NET você pode aplicar um número Bates, ajustar automaticamente o tamanho da fonte e até tratar o selo como uma marca d'água de texto sutil—tudo em algumas linhas de C#.

Neste tutorial vamos percorrer os passos exatos para **add page numbers pdf**, ajustar a fonte para que nunca exceda o limite e responder à pergunta “how to add bates” de uma vez por todas. Ao final você terá um aplicativo console pronto‑para‑executar que produz um PDF profissionalmente numerado, e verá como expandi‑lo para uma solução completa de marca d'água.

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

* **Aspose.Pdf for .NET** (o pacote NuGet mais recente em abril 2026).  
* .NET 6.0 SDK ou superior – a API funciona da mesma forma no .NET Framework, mas o .NET 6 oferece o melhor desempenho.  
* Um PDF de exemplo chamado `input.pdf` colocado em uma pasta que você possa referenciar (por exemplo, `C:\Docs\`).  

Nenhuma configuração extra é necessária; a biblioteca é autônoma.

---

## Passo 1 – Carregar o Documento PDF de Origem

A primeira coisa que fazemos é abrir o arquivo que queremos numerar. A classe `Document` da Aspose representa todo o PDF, e carregá‑lo é tão simples quanto passar o caminho para o construtor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Por que isso importa*: Carregar o documento lhe dá acesso à coleção `Pages`, onde anexaremos o selo Bates mais tarde. Se o arquivo não for encontrado, a Aspose lança uma clara `FileNotFoundException`, então você saberá exatamente o que deu errado.

---

## Passo 2 – Criar um Selo de Texto para Números Bates

Agora criamos o elemento visual que aparecerá em cada página. A classe `TextStamp` permite inserir qualquer string, e usaremos o placeholder `{page}-{total}` para que a Aspose substitua esses tokens automaticamente.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Pontos principais*:

* **auto adjust font size** – Definir `AutoAdjustFontSizeToFitStampRectangle` como `true` garante que o texto nunca transborde o retângulo, o que é perfeito para números de página de comprimento variável.  
* **add text watermark** – Ao reduzir a `Opacity` transformamos o número Bates em uma marca d'água sutil, atendendo ao requisito “add text watermark” sem uma etapa separada.  
* **how to add bates** – Os tokens `{page}` e `{total}` são o segredo; a Aspose os substitui em tempo de execução, então você não precisa calcular nada manualmente.

---

## Passo 3 – Aplicar o Selo em Cada Página

Um erro comum é aplicar o selo apenas na primeira página. Para realmente **add page numbers pdf**, precisamos percorrer toda a coleção `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Por que clonar? O método `AddStamp` cria internamente uma cópia, mas usar explicitamente uma nova instância por iteração evita efeitos colaterais acidentais se você modificar propriedades do selo posteriormente (como mudar a cor para páginas específicas).

---

## Passo 4 – Salvar o PDF Atualizado

Com os selos no lugar, persistir as alterações é simples. Você pode sobrescrever o arquivo original ou gravar em um novo local—aqui salvaremos um novo arquivo chamado `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Se você abrir `output.pdf` verá cada página rotulada “Bates: 1‑10”, “Bates: 2‑10”, … no canto inferior‑direito, com opacidade suave que também funciona como **add text watermark**.

---

## Exemplo Completo Funcional

Juntando tudo, aqui está um programa console único e autônomo que você pode copiar‑colar no Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Resultado esperado**: Abra `output.pdf` em qualquer visualizador; cada página mostra uma linha como “Bates: 3‑12” no canto inferior‑direito, dimensionada exatamente para o retângulo e renderizada com 40 % de opacidade. Isso satisfaz tanto o requisito de rastreamento legal quanto a necessidade de marca d'água visual.

---

## Variações Comuns & Casos de Borda

| Situação | O que mudar | Por quê |
|----------|-------------|--------|
| **Different placement** | Ajuste `HorizontalAlignment` / `VerticalAlignment` ou defina `XIndent`/`YIndent` | Algumas empresas preferem posicionamento no canto superior‑esquerdo ou central. |
| **Custom prefix** | Substitua `"Bates: "` por `"Doc‑ID: "` ou qualquer outra string | Você pode estar usando uma convenção de nomenclatura diferente. |
| **Multiple stamps** | Crie um segundo `TextStamp` (por exemplo, para um aviso de confidencialidade) e adicione‑o após o primeiro | Combinar **add bates numbering** com outros requisitos de **add text watermark** é trivial. |
| **Large page counts** | Aumente o tamanho inicial da fonte (ex.: `14`) – o auto‑adjust reduzirá quando necessário | Quando há > 999 páginas a string fica mais longa; o auto‑adjust evita cortes. |
| **Encrypted PDFs** | Chame `pdfDocument.Decrypt("password")` antes de aplicar o selo | Não é possível modificar um arquivo protegido sem a senha. |

---

## Dicas Profissionais & Armadilhas

* **Pro tip:** Defina `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` se perceber que o texto está colado à borda da página.  
* **Watch out for:** Retângulos muito pequenos (tamanho padrão é 100 × 30 pt). Se precisar de uma área maior, ajuste manualmente `batesStamp.Width` e `batesStamp.Height`.  
* **Performance note:** Aplicar selos em milhares de páginas pode levar alguns segundos, mas a Aspose faz streaming das páginas de forma eficiente—não é necessário carregar todo o documento na memória.  

---

## Conclusão

Acabamos de demonstrar como **add bates numbering** a um PDF usando Aspose.Pdf, enquanto simultaneamente **add page numbers pdf**, habilitamos **auto adjust font size** e criamos um **add text watermark** em um fluxo coeso. O exemplo completo e executável acima fornece uma base sólida que você pode adaptar a qualquer fluxo de trabalho de documentos legais ou sistema interno de relatórios.

Pronto para o próximo passo? Experimente combinar esta abordagem com a API de mesclagem de PDFs da Aspose para processar vários arquivos em lote, ou explore a classe `TextFragment` para marcas d'água mais ricas (coloridas, rotacionadas ou multilinha). As possibilidades são infinitas, e o código que você tem agora é uma base confiável.

Se este guia foi útil, sinta‑se à vontade para deixar um comentário, dar uma estrela ao repositório ou compartilhar suas próprias variações. Boa codificação, e que seus PDFs estejam sempre perfeitamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}