---
category: general
date: 2026-06-21
description: Adicione numeração Bates ao PDF e aprenda como adicionar números Bates,
  converter PDF para PDF/X‑4, converter PDF para PDF/A‑4 e assinar digitalmente PDF
  em C# em um único tutorial.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: pt
og_description: Adicionar numeração Bates ao PDF, ver como adicionar números Bates,
  converter PDF para PDF/X-4, converter PDF para PDF/A-4 e assinar digitalmente PDF
  em C# com Aspose.Pdf.
og_title: Adicionar numeração Bates ao PDF – Tutorial passo a passo em C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Adicionar Numeração Bates ao PDF – Guia Completo em C# com Assinatura e Conversão
url: /pt/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Numeração Bates a PDF – Guia Completo em C# com Assinatura & Conversão

Já se perguntou como **add bates numbering pdf** sem perder a cabeça? Você não está sozinho. Equipes jurídicas, auditores e qualquer pessoa que precise de documentos rastreáveis perguntam constantemente *como adicionar números bates* a um PDF, e ainda precisam que o arquivo atenda aos padrões PDF/X‑4 ou PDF/A‑4 e seja assinado digitalmente.  

Neste tutorial vamos percorrer exatamente isso—usando Aspose.Pdf para .NET vamos **add bates numbering pdf**, mostrar **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, e finalmente **digitally sign pdf c#**. Ao final você terá um programa pronto‑para‑executar que produz três PDFs polidos: uma versão PDF/X‑4, uma versão com numeração Bates e uma versão assinada digitalmente.

![exemplo de add bates numbering pdf](image-placeholder.png "Captura de tela mostrando add bates numbering pdf em ação")

## O que Você Precisa

- **.NET 6+** (ou .NET Framework 4.6+). Aspose.Pdf suporta ambos.
- Uma **licença válida do Aspose.Pdf for .NET** (ou você pode usar a avaliação, mas marcas d'água aparecerão).
- Um **arquivo de certificado PKCS#7** (`.pfx`) e sua senha para assinatura.
- O **PDF de exemplo** que você deseja transformar (coloque‑o em uma pasta que você controla).
- Visual Studio, Rider ou qualquer IDE C# de sua preferência.

É só isso—nenhum pacote NuGet extra além do `Aspose.Pdf`. Se ainda não adicionou a biblioteca, execute:

```bash
dotnet add package Aspose.Pdf
```

Agora vamos mergulhar no código.

## Etapa 1: Carregar o Documento PDF de Origem

Primeiro, precisamos trazer o arquivo original para a memória. Esta é a base para todas as operações subsequentes.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Por que isso importa:** Carregar o PDF cria um objeto `Document` que representa todo o arquivo, dando acesso às APIs de conversão, campos de formulário e segurança.

## Etapa 2: Converter PDF para PDF/X‑4 (Conformidade PDF/A‑4)

Se o seu fluxo de trabalho exige qualidade de arquivamento, PDF/X‑4 (um subconjunto do PDF/A‑4) é a escolha certa. Veja como **convert pdf to pdf/x-4** com Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Dica:** O sinalizador `ConvertErrorAction.Delete` remove qualquer conteúdo que possa quebrar a conformidade, garantindo uma saída limpa de PDF/X‑4.

## Etapa 3: Salvar a Versão PDF/X‑4

Agora que o documento está em conformidade com PDF/X‑4, persistimos ele no disco.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Você agora tem um arquivo compatível com **convert pdf to pdfa-4** (PDF/X‑4 faz parte da família PDF/A‑4). Sinta‑se à vontade para abri‑lo no Acrobat e verificar o selo de conformidade.

## Etapa 4: Adicionar Numeração Bates – O Núcleo do “Add Bates Numbering PDF”

A numeração Bates é um identificador sequencial colocado em cada página. Esta é a resposta exata para *como adicionar números bates* programaticamente.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Por que isso funciona:** `AddBatesNumbering` percorre cada página e grava o número na localização padrão (canto inferior direito). Você pode ajustar a posição posteriormente via `BatesNumberingOptions`, se necessário.

## Etapa 5: Salvar o PDF com Numeração Bates

Depois de **add bates numbering pdf**, precisamos de um arquivo separado que preserve os números.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Abra o arquivo; você deverá ver “CASE‑5000”, “CASE‑5001” e assim por diante na parte inferior de cada página.

## Etapa 6: Assinar Digitalmente o PDF – “Digitally Sign PDF C#” em Ação

Uma assinatura digital garante autenticidade e integridade. A seguir, vamos **digitally sign pdf c#** usando um hash SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro dica:** O `Rectangle` define onde a assinatura visível aparece. Se não precisar de um indicativo visual, defina `signatureAppearance` como `false`.

## Etapa 7: Salvar o PDF Assinado Digitalmente

Por fim, grave o documento assinado no disco.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Você agora tem um arquivo **digitally sign pdf c#** que pode ser validado em qualquer leitor de PDF que suporte assinaturas digitais.

## Código Fonte Completo – Solução Tudo‑em‑Um

Abaixo está o programa completo, pronto‑para‑executar, que une tudo. Copie‑e‑cole, ajuste os caminhos e pressione **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Saída Esperada

| Arquivo | Finalidade | Recurso Principal |
|------|---------|-------------|
| `sample_pdfx4.pdf` | Versão PDF/X‑4 | Atende à conformidade PDF/A‑4 |
| `sample_bates.pdf` | PDF com numeração Bates | **add bates numbering pdf** aplicado |
| `sample_signed.pdf` | PDF assinado digitalmente | **digitally sign pdf c#** com SHA‑384 |

Abra qualquer um dos três arquivos no Adobe Acrobat Reader; você verá os números Bates no segundo arquivo e um campo de assinatura no terceiro.

## Perguntas Frequentes (FAQ)

**P: Posso mudar a posição dos números Bates?**  
R: Sim. Use as propriedades de `BatesNumberingOptions` como `Location` e `FontSize` para ajustar a colocação.

**P: E se eu precisar de PDF/A‑4 em vez de PDF/X‑4?**  
R: Troque `PdfFormat.PDF_X_4` por `PdfFormat.PDFA_4` nas opções de conversão. Isso satisfaz o requisito **convert pdf to pdfa-4**.

**P: Meu certificado usa outro algoritmo de hash—posso usar SHA‑256?**  
R: Claro. Substitua `DigestHashAlgorithm.Sha384` por `DigestHashAlgorithm.Sha256` (ou qualquer algoritmo suportado).

**P: Preciso chamar `document.Save` após cada etapa?**  
R: Não necessariamente. Neste fluxo salvamos após a conversão e após a numeração Bates para fornecer arquivos intermediários. Você pode adiar a gravação até o final, se preferir uma única operação de escrita.

## Conclusão

Acabamos de demonstrar uma solução prática, de ponta a ponta que **add bates numbering pdf**, explica **how to add bates numbers**, mostra **convert pdf to pdf/x-4**, cobre


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}