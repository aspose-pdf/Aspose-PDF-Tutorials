---
category: general
date: 2026-04-06
description: Crie PDF a partir de JPG rapidamente e aprenda como recortar imagem em
  PDF, adicionar nova página ao PDF e converter JPG para PDF com recorte usando C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: pt
og_description: Crie PDF a partir de JPG e recorte a imagem no PDF com C#. Aprenda
  como adicionar uma nova página PDF e converter JPG para PDF com recorte.
og_title: Criar PDF a partir de JPG em C# – Guia passo a passo
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Criar PDF a partir de JPG em C# – Guia Completo com Recorte e Novas Páginas
url: /pt/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF a partir de JPG em C# – Guia Completo com Corte e Novas Páginas

Já precisou **criar PDF a partir de JPG** mas não sabia como manter apenas a parte que realmente deseja? Você não está sozinho. Em muitos aplicativos—pense em notas fiscais, recibos ou fotolivros—os desenvolvedores precisam transformar uma imagem em PDF descartando as bordas indesejadas.  

Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que **cria PDF a partir de JPG**, mostra como **cortar imagem no PDF** e demonstra o **como adicionar nova página pdf** quando precisar de mais de uma foto. Ao final, você também saberá como **converter JPG para PDF com corte** e **inserir imagem no PDF C#** usando a biblioteca Aspose.Pdf.

## O que você vai aprender

- Configurar Aspose.Pdf em um projeto .NET (sem necessidade de configuração pesada).  
- Carregar um JPEG, definir a área que deseja manter e recortá‑la ao inseri‑la em uma página PDF.  
- Adicionar páginas adicionais ao mesmo documento, permitindo criar PDFs de várias páginas a partir de muitas imagens.  
- Salvar o arquivo final e verificar o resultado.  

**Pré‑requisitos:** .NET 6+ (ou .NET Framework 4.6+), Visual Studio 2022 ou qualquer editor de sua preferência, e uma referência NuGet ao `Aspose.Pdf`. Nenhum outro serviço externo é necessário.

![Create PDF from JPG example](image.jpg){: .align-center alt="Create PDF from JPG example showing a cropped image placed on a PDF page"}

---

## Etapa 1: Instalar Aspose.Pdf e preparar seu projeto

Primeiro de tudo—adicione o pacote Aspose.Pdf. Abra um terminal na pasta da sua solução e execute:

```bash
dotnet add package Aspose.Pdf
```

Essa única linha traz tudo que você precisa: as classes `Document`, `Rectangle` e `Page` que usaremos mais adiante. Na minha experiência, o caminho NuGet é a forma mais limpa de se manter atualizado sem mexer em DLLs.

> **Dica de especialista:** Se você estiver direcionando .NET Framework, use o pacote `Aspose.Pdf.NET` em vez disso; a superfície da API é idêntica.

---

## Etapa 2: Carregar o JPEG e definir o tamanho da página

Precisamos de uma tela que corresponda às dimensões que queremos para a página PDF final. O código abaixo cria um novo `Document` e abre a imagem de origem como um stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Por que um retângulo? No Aspose.Pdf um `Rectangle` representa tanto as dimensões da página quanto a região da imagem que você deseja exibir. Ao separar a *página* da *área de corte* você ganha controle fino sobre o que aparecerá no PDF.

---

## Etapa 3: Escolher a área de corte (quadrante superior‑esquerdo)

Suponha que você precise apenas do quadrante superior‑esquerdo da foto. Calculamos essa região em relação ao tamanho da página:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

O construtor `Rectangle` recebe valores de **X/Y inferior‑esquerdo** e **X/Y superior‑direito**. Ao adicionar metade da altura a `LLY` deslocamos a parte inferior do corte para cima, descartando efetivamente a metade inferior da imagem. Ajuste esses cálculos se precisar de outra porção.

> **Por que cortar antes de adicionar?**  
> Cortar no lado do PDF evita a criação de um bitmap temporário no disco, economizando I/O e memória. Aspose cuida dos cálculos para você, e o resultado é um PDF limpo e amigável a vetores.

---

## Etapa 4: Adicionar uma nova página e inserir a imagem recortada

Agora realmente colocamos a imagem em uma página PDF. É aqui que a palavra‑chave **como adicionar nova página pdf** brilha.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` recebe três argumentos:

1. **Stream** – o JPEG de origem.  
2. **Retângulo da página** – define o tamanho da página (nosso `pageBounds`).  
3. **Retângulo de corte** – indica ao Aspose qual parte da imagem renderizar.

Se precisar de mais páginas, basta repetir o padrão `Add` + `AddImage` com um novo `imageStream` a cada vez. Isso satisfaz o requisito **como adicionar nova página pdf** mantendo o código organizado.

---

## Etapa 5: Salvar o PDF e verificar o resultado

A etapa final é uma única linha, mas não a subestime—salvar no caminho correto garante que o arquivo possa ser aberto por qualquer visualizador de PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Ao abrir `cropped_image.pdf`, você deverá ver uma única página que contém apenas o quadrante superior‑esquerdo do JPEG original, perfeitamente centralizado dentro da página 600 × 800.

---

## Exemplo completo (todas as etapas combinadas)

A seguir está o programa completo que você pode copiar‑colar em um aplicativo de console. Ele compila como está, assumindo que você instalou o Aspose.Pdf e colocou um JPEG no local especificado.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Saída esperada

- **Arquivo:** `cropped_image.pdf` (≈ 30 KB).  
- **Conteúdo:** Uma página, 600 × 800 pontos, mostrando o quadrante superior‑esquerdo de `photo.jpg`.  
- **Comportamento:** Sem distorção; a imagem mantém sua resolução original dentro dos limites recortados.

---

## Perguntas Frequentes & Casos de Borda

### E se eu precisar manter a imagem inteira, não apenas um quadrante?

Basta definir `cropArea` igual a `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Posso usar um tamanho de página diferente (por exemplo, A4)?

Claro. Substitua os valores de `pageBounds` pelas dimensões de uma página A4 em pontos (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

O retângulo de corte pode permanecer o mesmo ou ser recalculado para combinar com a nova proporção.

### Como adiciono várias imagens, cada uma em sua própria página?

Itere sobre uma coleção de caminhos de arquivos:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### E quanto à transparência ou imagens PNG?

Aspose.Pdf trata PNG da mesma forma que JPEG. Se a origem possuir canal alfa, o PDF preservará a transparência, desde que a versão do PDF suporte (o padrão já permite).

### Isso funciona no .NET Core em Linux?

Sim. Aspose.Pdf é multiplataforma; basta garantir que `imageStream` aponte para um caminho de arquivo válido no sistema operacional de destino. Nenhuma API exclusiva do Windows é utilizada.

---

## Dicas & Melhores Práticas

- **Gerenciamento de memória:** Sempre envolva streams em blocos `using` (como mostrado) para evitar bloqueios de arquivos.  
- **Desempenho:** Se estiver processando dezenas de imagens, considere reutilizar uma única instância de `Document` e chamar `pdfDocument.Pages.Add()` para cada imagem.  
- **Tratamento de erros:** Envolva toda a rotina em um bloco `try/catch` e registre `PdfException` para depuração.  
- **Controle de qualidade:** Aspose.Pdf permite definir a resolução da imagem via `ImageFragment`. Para digitalizações de alta DPI, ajuste `ImageFragment.Resolution = 300;`.  
- **Segurança:** Se o PDF for compartilhado externamente, você pode adicionar criptografia com `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Conclusão

Acabamos de cobrir como **criar PDF a partir de JPG** em C#, **cortar imagem no PDF** e **adicionar nova página PDF** para montar documentos de várias páginas. O mesmo padrão permite **converter JPG para PDF com corte** e **inserir imagem no PDF C#** para qualquer cenário—desde recibos simples até fotolivros complexos.  

Experimente: troque a lógica de corte, teste páginas A4 ou encadeie várias imagens. A biblioteca Aspose.Pdf torna essas tarefas indolores, e o código acima é uma referência sólida e citável que você pode colar em qualquer projeto.

---

### Próximos passos

- **Adicionar anotações de texto** ao PDF (por exemplo, legendas abaixo de cada imagem).  
- **Criar um índice** automaticamente para PDFs de várias páginas.  
- **Mesclar múltiplos PDFs** usando `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Cada um desses tópicos se baseia nos fundamentos que você acabou de dominar, então você está bem posicionado para explorá‑los.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}