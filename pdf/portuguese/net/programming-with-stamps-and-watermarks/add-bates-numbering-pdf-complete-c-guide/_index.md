---
category: general
date: 2026-03-22
description: Adicione numeração Bates ao PDF rapidamente com Aspose.Pdf. Aprenda como
  adicionar Bates, números de página sequenciais, rodapé personalizado ao PDF e artefato
  ao PDF em minutos.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: pt
og_description: Adicionar numeração Bates em PDF usando Aspose.Pdf. Este guia mostra
  como adicionar Bates, adicionar numeração de página sequencial, adicionar rodapé
  personalizado ao PDF e adicionar artefato ao PDF.
og_title: Adicionar numeração Bates ao PDF – Tutorial passo a passo em C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Adicionar numeração Bates ao PDF – Guia completo de C#
url: /pt/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates em PDF – Guia Completo em C#

Já precisou **adicionar numeração bates pdf** a um lote de documentos jurídicos, mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores enfrentam esse obstáculo ao criar ferramentas de gerenciamento de casos. A boa notícia? Com Aspose.Pdf você pode **adicionar bates**, **adicionar números de página sequenciais** e até **adicionar rodapé pdf personalizado** em apenas algumas linhas de código.  

Neste tutorial vamos percorrer todo o processo, desde a instalação da biblioteca até a gravação do arquivo final, e incluiremos dicas de como **adicionar artefato ao pdf** sem quebrar o conteúdo existente. Ao final, você terá um trecho pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

## O que você vai precisar

- .NET 6+ (o código funciona tanto em .NET Core quanto em .NET Framework)  
- Uma licença válida do Aspose.Pdf for .NET (você pode começar com uma avaliação gratuita)  
- Um PDF de entrada (`input.pdf`) colocado em uma pasta que você possa referenciar  
- Visual Studio, Rider ou qualquer editor C# de sua preferência  

É só isso—nenhum pacote NuGet extra além do Aspose.Pdf.

## Etapa 1: Instalar Aspose.Pdf via NuGet

Primeiro de tudo—vamos colocar a biblioteca na sua máquina. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Pdf
```

Ou, se estiver usando o Console do Gerenciador de Pacotes do Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Dica profissional:* Após a instalação, verifique se a pasta `Aspose.Pdf` aparece em `Dependencies → Packages` no explorador de soluções.

## Etapa 2: Carregar o Documento PDF de Origem

Agora criamos um objeto `Document` que representa o PDF que queremos carimbar. Usar a instrução `using` garante que o manipulador de arquivo seja liberado automaticamente.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Por que usar `using var`? Ele garante a liberação mesmo que ocorra uma exceção, evitando problemas de bloqueio de arquivo ao tentar sobrescrever o mesmo arquivo depois.

## Etapa 3: Criar e Configurar um Artefato de Numeração Bates

Um número Bates é essencialmente um artefato de texto que vive na estrutura lógica do PDF. Você pode tratá‑lo como um **rodapé pdf personalizado**, pois ele aparece em todas as páginas sem fazer parte do fluxo de conteúdo da página.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Por que essas configurações são importantes

- **Prefix**: Útil para distinguir tipos de documento (ex.: “INV‑” para faturas).  
- **Start**: Define o primeiro número; você pode obtê‑lo de um banco de dados se precisar de continuidade entre arquivos.  
- **Format**: `"0000"` força a exibição com quatro dígitos, garantindo alinhamento à medida que os números aumentam.  
- **X/Y**: As coordenadas são medidas a partir do canto inferior esquerdo, então `Y = 20` posiciona o texto logo acima da margem da página. Ajuste `X` se quiser o número alinhado à esquerda ou centralizado.

Se precisar **adicionar números de página sequenciais** em vez de números Bates, basta omitir `Prefix` e ajustar `Format` para `"###"` ou qualquer padrão que preferir.

## Etapa 4: Aplicar o Artefato a Todas as Páginas

Aspose.Pdf permite anexar um artefato a todo o documento em uma única chamada. Essa é a forma mais eficiente de **adicionar artefato ao pdf** sem percorrer manualmente cada página.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Nos bastidores, o Aspose adiciona o artefato ao dicionário de página de cada página, o que significa que a numeração passa a fazer parte da estrutura lógica do PDF—perfeito para extração ou busca posteriores.

## Etapa 5: Salvar o PDF Atualizado

Por fim, grave as alterações no disco. Você pode sobrescrever o original ou salvar em um novo arquivo; a segunda opção é mais segura durante o desenvolvimento.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Ao abrir `output.pdf` em um visualizador, você verá “INV‑1000”, “INV‑1001”, … no canto inferior‑direito de cada página.

### Verificando o Resultado

Abra o PDF no Adobe Acrobat ou em qualquer visualizador e procure pelos números. Se precisar confirmar programaticamente, você pode ler de volta o artefato:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Esse trecho imprime o rótulo Bates de cada página—útil para testes automatizados.

## Casos de Borda & Perguntas Frequentes

### E se meu PDF já tiver um rodapé?

Adicionar um artefato não sobrescreve rodapés existentes porque os artefatos ficam em uma camada separada. Contudo, se a sobreposição visual for um problema, ajuste a coordenada `Y` ou aumente o deslocamento `X` para mover o número Bates para fora do caminho.

### Posso usar uma fonte ou cor diferente?

Com certeza. O `BatesNumberingArtifact` herda de `Artifact`, então você pode definir `Font`, `FontColor` e até `Opacity`. Exemplo:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Como redefinir o contador para um novo documento?

Basta mudar `Start` antes de chamar `AddArtifact`. Se você gerar muitos PDFs em um loop, mantenha um contador em sua lógica de aplicação.

### Essa abordagem funciona com PDFs criptografados?

Aspose.Pdf pode abrir PDFs criptografados se você fornecer a senha:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Após a descriptografia, as mesmas etapas de adição de artefato funcionam perfeitamente.

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar. Cole-o em um aplicativo console, ajuste os caminhos e pressione **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Saída esperada:** O console imprime “Bates numbering added successfully!” e `output.pdf` contém rótulos sequenciais como `INV‑1000`, `INV‑1001`, etc., posicionados no canto inferior‑direito de cada página.

## Resumo Rápido

- **Objetivo principal:** **add bates numbering pdf** usando Aspose.Pdf.  
- Abordamos **como add bates**, **add sequential page numbers** e **add custom footer pdf** através de um único artefato.  
- O tutorial mostrou como **add artifact to pdf**, lidar com casos de borda e verificar o resultado.  

## O que vem a seguir?

- **Prefixos dinâmicos:** Buscar valores em um banco de dados para gerar “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Posicionamento condicional:** Usar detecção de tamanho de página (`page.MediaBox`) para centralizar números em páginas paisagem.  
- **Combinar com marcas d'água:** Adicionar um logotipo semitransparente ao lado do número Bates para branding.  

Sinta‑se à vontade para experimentar—talvez você descubra uma maneira mais inteligente de processar milhares de arquivos em lote. Se encontrar algum problema, deixe um comentário ou consulte a documentação oficial da Aspose (é surpreendentemente clara). Boa codificação!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}