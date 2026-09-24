---
category: general
date: 2026-01-15
description: Adicione números de Bates ao seu PDF rapidamente com Aspose.Pdf. Aprenda
  como adicionar rodapé ao PDF, adicionar numeração de páginas ao PDF e adicionar
  numeração de página personalizada.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: pt
og_description: Adicione números Bates ao seu PDF rapidamente com Aspose.Pdf. Aprenda
  como adicionar rodapé ao PDF, inserir números de página no PDF e criar numeração
  de página personalizada.
og_title: Adicionar Números Bates ao PDF – numeração bates pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Adicionar Números Bates ao PDF – numeração Bates PDF
url: /pt/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Números Bates a PDF – Guia Completo

Já precisou **adicionar números bates** a um PDF e não sabia por onde começar? Você não está sozinho—equipes jurídicas, auditores e quem trabalha com grandes volumes de documentos enfrentam esse problema diariamente. A boa notícia? Com Aspose.Pdf para .NET você pode espalhar esses números em cada página com apenas algumas linhas de código.

Neste tutorial vamos percorrer todo o processo: desde a importação da biblioteca Aspose.Pdf, carregamento do arquivo fonte, configuração de um *BatesNumberingArtifact*, anexação como rodapé e, por fim, salvamento do resultado. Ao final, você também saberá como **add footer to pdf**, **add page numbers pdf** e até **add custom page numbering** para aqueles casos mais complexos.

## O que você vai precisar

- .NET 6+ (ou .NET Framework 4.8 se ainda estiver na pilha clássica)  
- Uma referência ao pacote NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Um arquivo PDF que você deseja marcar (vamos chamá‑lo de `source.pdf`)  

É só isso—nenhuma ferramenta extra, nenhum editor de PDF pesado. Vamos lá.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Etapa 1: Add Bates Numbers – Carregar o Documento PDF

Primeiro, precisamos de um objeto `Document` que represente o PDF que será modificado. Pense nisso como abrir um documento do Word antes de começar a digitar.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Por que isso importa:** Carregar o arquivo dá acesso à coleção `Pages`, onde anexaremos o artefato de numeração Bates mais adiante. Se o arquivo não for encontrado, o Aspose lançará uma clara `FileNotFoundException`, então verifique o caminho.

## Etapa 2: Configure bates numbering pdf Settings

Agora definimos *como* os números devem aparecer. O `BatesNumberingArtifact` permite definir um prefixo, número inicial, preenchimento de dígitos, sufixo e posicionamento. Este é o núcleo do **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Dica de especialista:** Se precisar que os números apareçam no cabeçalho, troque `BottomCenter` por `TopCenter`. O enum de posicionamento também suporta `BottomLeft`, `BottomRight`, etc., oferecendo flexibilidade para diferentes estilos de **add footer to pdf**.

## Etapa 3: Add page numbers pdf – Anexar o Artifact a Cada Página

Com o artifact pronto, percorremos cada página e o adicionamos à coleção `Artifacts`. Esta é a etapa que realmente **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **O que está acontecendo nos bastidores?** A coleção `Artifacts` é renderizada após o conteúdo principal da página, garantindo que o número Bates fique acima de qualquer texto existente, mas abaixo de anotações. Se precisar que o número fique atrás do conteúdo (caso raro), use `page.Artifacts.Insert(0, batesArtifact)`.

## Etapa 4: Add custom page numbering – Salvar o PDF Atualizado

Por fim, gravamos o documento modificado no disco. O arquivo de saída conterá os números Bates como parte permanente de cada página.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Dica de verificação:** Abra `bates_out.pdf` em qualquer visualizador. Você deverá ver algo como `CASE-01000-A` centralizado na parte inferior de cada página. Se os números não aparecerem, verifique se a propriedade `Placement` corresponde ao local desejado.

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Resultado Esperado

- **Arquivo:** `bates_out.pdf` na mesma pasta que `source.pdf`  
- **Visual:** Texto centralizado na parte inferior `CASE-01000-A`, `CASE-01001-A`, … para cada página subsequente  
- **Comportamento:** Os números são incorporados permanentemente; permanecem após impressão, flattening e edições posteriores.

## Variações Comuns & Casos de Borda

| Situação | Como Ajustar |
|-----------|---------------|
| **Número inicial diferente** | Altere `StartNumber` para qualquer inteiro (ex.: `StartNumber = 500`). |
| **Sufixos de letra por volume** | Use um loop para modificar `Suffix` por página, ou crie múltiplos artifacts com sufixos diferentes. |
| **Numeração alinhada à direita** | Defina `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Documentos grandes (10k+ páginas)** | Considere processar páginas em lotes ou aumentar `NumberDigits` para evitar overflow. |
| **Precisar ocultar números em certas páginas** | Pule essas páginas no loop `foreach` (ex.: `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Cuidado:** Usar um `Prefix` ou `Suffix` que contenha caracteres ilegais em nomes de arquivo (ex.: `*` ou `?`). O Aspose ainda os incorporará, mas podem causar problemas ao extrair o texto posteriormente.

## Dicas Profissionais para Uso em Produção

- **Cache o artifact** se estiver processando muitos PDFs consecutivamente; criá‑lo uma única vez economiza alguns milissegundos por arquivo.  
- **Segurança de threads:** A instância `BatesNumberingArtifact` não é thread‑safe, portanto dê a cada thread sua própria cópia.  
- **Desempenho:** Para lotes massivos, desative a compressão do PDF (`pdfDocument.Compress = false`) antes de salvar, reativando‑a se necessário.  
- **Testes:** Sempre faça uma rápida verificação visual no primeiro PDF gerado para garantir que o posicionamento atende aos padrões da sua equipe jurídica.

## Conclusão

Agora você tem uma receita completa, de ponta a ponta, para **add bates numbers** a qualquer PDF usando Aspose.Pdf, incluindo opções para **add footer to pdf**, **add page numbers pdf** e **add custom page numbering**. O código é totalmente autocontido, funciona com .NET 6 ou superior, e pode ser inserido em qualquer pipeline de automação existente.

Qual o próximo passo? Experimente trocar o posicionamento `BottomCenter` por um estilo de cabeçalho, teste prefixos dinâmicos (ex.: IDs de casos vindos de um banco de dados) ou combine isso com os recursos de extração de texto do Aspose para gerar um índice pesquisável dos documentos recém‑numerados. O céu é o limite, e você acabou de ganhar uma ferramenta poderosa para controle de documentos.

Boa codificação, e que seus PDFs estejam sempre perfeitamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}