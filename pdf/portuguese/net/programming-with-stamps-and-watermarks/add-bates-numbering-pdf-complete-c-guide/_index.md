---
category: general
date: 2026-02-14
description: Adicione numeração Bates em PDF aos seus documentos sem esforço. Aprenda
  como adicionar números de página no rodapé e números sequenciais em PDF com Aspose.Pdf
  em minutos.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: pt
og_description: Adicione numeração Bates ao PDF rapidamente. Este guia mostra como
  adicionar números de página no rodapé e numeração sequencial ao PDF usando Aspose.Pdf,
  com código completo e dicas.
og_title: Adicionar Numeração Bates a PDF – Tutorial C# Passo a Passo
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

# Adicionar Numeração Bates PDF – Guia Completo em C#

Já precisou **adicionar numeração Bates PDF** a arquivos, mas não sabia por onde começar? Você não está sozinho. Equipes jurídicas, auditores e qualquer pessoa que lide com grandes conjuntos de documentos perguntam constantemente: “Como adiciono números Bates sem quebrar o layout?” A boa notícia é que, com Aspose.Pdf para .NET, você pode inserir esses números como um simples rodapé — sem necessidade de edição manual.

Neste tutorial vamos percorrer uma solução prática, de ponta a ponta, que não só **adiciona números de página no rodapé**, mas também permite **adicionar números sequenciais PDF** com um prefixo personalizado, tamanho de fonte e alinhamento. Ao final, você terá um programa C# pronto‑para‑executar, uma compreensão clara de por que cada configuração importa e algumas dicas avançadas para evitar os erros mais comuns.

## O que você aprenderá

- Como carregar um PDF existente e prepará‑lo para a numeração Bates.  
- Quais propriedades de **BatesNumberingOptions** controlam a aparência e a posição.  
- Como aplicar a numeração a todas as páginas em uma única chamada.  
- Formas de personalizar o prefixo, número inicial e margens para diferentes formatos jurídicos.  
- Tratamento de casos extremos — o que fazer com PDFs criptografados ou documentos que já contêm rodapés.

**Pré‑requisitos**: .NET 6+ (ou .NET Framework 4.7+), uma versão recente do Aspose.Pdf (o exemplo usa 23.10) e um PDF de entrada que você tenha direitos de modificar. Nenhuma outra biblioteca de terceiros é necessária.

---

## Etapa 1 – Carregar o PDF que você deseja numerar

A primeira coisa que fazemos é criar uma instância `Document` que aponta para o arquivo fonte. Usar o padrão `using var` garante que o manipulador de arquivo seja liberado automaticamente.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Por que isso importa:** Aspose.Pdf lê toda a estrutura do PDF para a memória, permitindo manipular páginas, anotações e metadados sem tocar no arquivo original no disco. Se o PDF estiver protegido por senha, você pode passar a senha ao construtor — veja a nota “PDFs Criptografados” ao final.

---

## Etapa 2 – Definir suas Opções de Numeração Bates

Números Bates são essencialmente rodapés de página com um prefixo configurável e um contador sequencial. A classe `BatesNumberingOptions` permite ajustar cada aspecto visual.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Dica rápida

- **Prefix**: Use um identificador curto e único (por exemplo, número do caso) para manter o rodapé legível.  
- **StartNumber**: Escritórios jurídicos costumam iniciar em `1` ou em um deslocamento personalizado; escolha o que combinar com seu sistema de arquivamento.  
- **Margins**: A margem inferior de `20` pontos mantém o texto afastado de notas de rodapé ou assinaturas que já possam estar próximas à borda da página.

---

## Etapa 3 – Aplicar a Numeração a Todas as Páginas

Com as opções configuradas, a injeção real é feita em uma única linha. Aspose.Pdf cuida da paginação, atualiza fluxos de conteúdo existentes e respeita a rotação da página automaticamente.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **O que está acontecendo nos bastidores?** A biblioteca itera sobre cada objeto `Page`, cria um `TextFragment` que incorpora o prefixo e o contador atual, e então o desenha usando o sistema de coordenadas da página. Como definimos `HorizontalAlignment.Right` e `VerticalAlignment.Bottom`, o texto fixa no canto inferior‑direito independentemente do tamanho da página.

---

## Etapa 4 – Salvar o PDF Modificado

Por fim, escreva o resultado em um novo arquivo. Substituir o original é possível, mas manter uma cópia ajuda no controle de versões.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Se precisar preservar os metadados originais (autor, data de criação), Aspose.Pdf os copia por padrão. Você também pode especificar um objeto `SaveOptions` para conformidade PDF/A ou compressão.

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar. Cole-o em um projeto de aplicação console, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Resultado esperado:** Cada página de `output.pdf` agora exibe um rodapé como `ABC-1000`, `ABC-1001`, … ancorado no canto inferior‑direito. Abra o arquivo em qualquer leitor de PDF para verificar.

---

## Lidando com Variações Comuns

### Adicionando Apenas Números de Página no Rodapé

Se você precisar apenas de números de página simples, sem prefixo, defina `Prefix = ""` e talvez ajuste a margem para evitar colisões com rodapés existentes.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Usando um Alinhamento Diferente

Documentos jurídicos às vezes exigem que o número fique centralizado na parte inferior. Altere o alinhamento:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Lidando com PDFs Criptografados

Quando o PDF fonte está protegido por senha, forneça a senha assim:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

O restante do fluxo permanece idêntico.

### Ignorando Rodapés Existentes

Se um documento já contém um rodapé que você não quer sobrescrever, pode prefixar uma string personalizada que torne o novo número distinto, ou iterar manualmente as páginas e adicionar um `TextFragment` apenas onde o rodapé estiver ausente. A classe `Page` da biblioteca expõe as coleções `Annotations` e `Contents` para controle granular.

---

## Dicas Profissionais & Armadilhas

- **Evite corte**: Margens inferiores muito pequenas podem fazer o texto ser cortado nas impressoras. Teste com impressão física se for distribuir cópias impressas.  
- **Desempenho**: Adicionar números Bates a um PDF de 500 páginas leva menos de um segundo em um laptop moderno, mas lotes grandes se beneficiam de processamento paralelo — apenas lembre‑se de que `Document` não é thread‑safe, então cada thread precisa da sua própria instância.  
- **Compatibilidade de versão**: O código funciona com Aspose.Pdf 23.10 e versões posteriores. Se estiver usando uma versão mais antiga, os nomes das propriedades são os mesmos, mas o construtor `MarginInfo` pode exigir argumentos `float`.  
- **Conformidade legal**: Algumas jurisdições exigem que o número Bates seja colocado em um local específico (por exemplo, canto inferior‑esquerdo). Ajuste o `HorizontalAlignment` conforme necessário.  

---

## Conclusão

Acabamos de demonstrar como **adicionar numeração Bates PDF** usando Aspose.Pdf para .NET, cobrindo tudo, desde o carregamento do documento até a gravação da versão final com um rodapé limpo. Ajustando alguns poucos parâmetros, você também pode **adicionar números de página no rodapé**, **adicionar números sequenciais PDF**, ou personalizar a aparência para atender a qualquer padrão jurídico.

Pronto para o próximo passo? Experimente combinar esta técnica com extração de texto OCR para inserir palavras‑chave pesquisáveis ao lado dos números Bates, ou automatize o processo para pastas inteiras usando `Directory.GetFiles`. As possibilidades são infinitas, e a base que você agora tem tornará essas extensões simples.

Feliz codificação, e que seus PDFs estejam sempre perfeitamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}