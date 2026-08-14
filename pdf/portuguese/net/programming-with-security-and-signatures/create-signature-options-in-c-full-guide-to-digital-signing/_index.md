---
category: general
date: 2026-08-14
description: Crie opções de assinatura em C# para aplicar assinatura digital. Aprenda
  como configurar a assinatura, implementar uma função de hash personalizada e assinar
  documentos programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: pt
lastmod: 2026-08-14
og_description: Crie opções de assinatura em C# e aplique uma assinatura digital.
  Este tutorial orienta você na configuração da assinatura, na adição de uma função
  de hash personalizada e na assinatura de um documento.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Crie opções de assinatura em C# – guia passo a passo de assinatura digital
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: Crie opções de assinatura em C# – guia completo de assinatura digital
url: /pt/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar opções de assinatura em C# – guia completo para assinatura digital

Crie opções de assinatura em C# para configurar um fluxo de trabalho de assinatura digital. Este tutorial mostra como aplicar assinatura digital, implementar uma função de hash personalizada e assinar um documento usando a classe `SignatureOptions`. Se você já precisou assinar um PDF, XML ou qualquer carga binária a partir de uma aplicação .NET, os passos abaixo fornecem uma solução pronta‑para‑uso.

Você aprenderá a:

* configurar `SignatureOptions` com um algoritmo de hash personalizado,
* chamar o método de assinatura corretamente,
* verificar se a assinatura foi aplicada,
* evitar armadilhas comuns ao configurar a assinatura.

Os únicos pré‑requisitos são um SDK .NET recente (≥ .NET 6) e uma biblioteca de assinatura que exponha `SignatureOptions` (por exemplo, **GroupDocs.Signature**, **Aspose.Signature** ou uma API similar). Nenhuma ferramenta externa é necessária.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| .NET 6 SDK ou posterior | Fornece os recursos de linguagem modernos usados nos exemplos. |
| Um pacote NuGet de biblioteca de assinatura (ex.: `GroupDocs.Signature`) | Disponibiliza o tipo `SignatureOptions` e o método de extensão `Sign`. |
| Acesso a uma chave privada ou certificado | Necessário para gerar uma assinatura digital verificável. |

Instale a biblioteca com a CLI padrão:

```bash
dotnet add package GroupDocs.Signature
```

---

## Etapa 1: Criar opções de assinatura

O primeiro passo é instanciar `SignatureOptions` e definir as propriedades que controlam o processo de assinatura. Este objeto informa à biblioteca *o que* assinar e *como* assinar.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**Por que isso importa:** `SignatureOptions` funciona como um contrato entre seu código e o mecanismo de assinatura. Ao configurá‑lo antecipadamente, você evita boilerplate repetido ao assinar múltiplos documentos.

---

## Etapa 2: Implementar uma função de hash personalizada

Uma *função de hash personalizada* dá controle total sobre o digest que o algoritmo de assinatura assina. Isso é útil quando o hash padrão (SHA‑256) não atende a requisitos de conformidade ou quando você precisa hash de um subconjunto do documento.

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**Por que isso importa:** Ao atribuir `CustomSignHash`, você substitui a etapa interna de hash da biblioteca por `MyHash`. O mecanismo de assinatura agora assinará os bytes retornados pela sua função, garantindo conformidade com qualquer política personalizada.

---

## Etapa 3: Carregar o documento e aplicar assinatura digital

Com as opções preparadas, você pode abrir o arquivo de destino e chamar o método de assinatura. O método `Sign` é fornecido pela biblioteca e usa o `SignatureOptions` configurado.

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**Por que isso importa:** A chamada a `Sign` realiza três ações internamente:

1. **Cálculo do hash** – agora delegada à sua função de hash personalizada.  
2. **Geração da assinatura** – usando a chave privada fornecida na configuração da biblioteca.  
3. **Incorporação** – a assinatura gerada é anexada ao arquivo de saída.

Se qualquer etapa falhar, o método retorna `false`, permitindo que você trate o erro de forma elegante.

---

## Etapa 4: Verificar se o documento está assinado

Uma verificação rápida confirma que a assinatura foi aplicada corretamente. A maioria das bibliotecas expõe um método `Verify` que checa a integridade do arquivo assinado.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Por que isso importa:** A verificação garante que o documento assinado não foi alterado após a assinatura e que o hash personalizado produziu um digest compatível.

---

## Como configurar assinatura para diferentes tipos de arquivo

O mesmo objeto `SignatureOptions` pode ser reutilizado para PDFs, documentos Word, imagens ou binários simples. A única mudança necessária é a classe de opções específica (ex.: `PdfSignatureOptions`, `WordSignatureOptions`). Aqui está um exemplo rápido para uma imagem JPEG:

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**Por que isso importa:** Entender como *configurar assinatura* para cada formato permite que você estenda a mesma base de código a múltiplos tipos de documento sem reescrever a lógica de hash.

---

## Armadilhas comuns e boas práticas

| Armadilha | Correção recomendada |
|-----------|----------------------|
| Esquecer de definir `CustomSignHash` após criar `SignatureOptions` | Atribua o delegate imediatamente após construir o objeto de opções. |
| Usar um algoritmo de hash que o certificado de assinatura não suporta | Verifique se o uso da chave do certificado corresponde ao tamanho do hash (ex.: RSA‑2048 com SHA‑512). |
| Ignorar a necessidade de descartar objetos `Signature` | Envolva a instância `Signature` em um bloco `using` para liberar os manipuladores de arquivo. |
| Salvar o arquivo assinado sobre o arquivo original | Sempre escreva em um novo caminho de arquivo (`outputPath`) para preservar o documento original. |

---

## Exemplo completo funcional

Abaixo está um programa autocontido que reúne todas as peças. Copie-o para um novo projeto de console e execute; o console reportará sucesso ou falha.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**Saída esperada**

```
Signature verified successfully.
```

Se o console imprimir “Signing failed.” ou “Signature verification failed.”, verifique novamente a configuração do certificado e assegure que o hash personalizado retorne um array de bytes do tamanho esperado.

---

## Conclusão

Agora você sabe como **criar opções de assinatura** em C#, anexar uma **função de hash personalizada** e **aplicar assinatura digital** a qualquer documento suportado. O tutorial cobriu todo o ciclo de vida: configurar as opções, assinar o arquivo e verificar o resultado. Reutilizando a mesma instância de `SignatureOptions`, você também pode **como configurar assinatura** para imagens, arquivos Word ou binários crus.

---

## O que vem a seguir?

* Explore propriedades adicionais de `SignatureOptions` como carimbos visuais, servidores de timestamp e cadeias de certificados – elas se alinham com a palavra‑chave **apply digital signature**.  
* Experimente outros algoritmos de hash (ex.: Blake2b) trocando a implementação dentro de `MyHash`.  
* Integre o fluxo de assinatura em uma API web para habilitar assinatura de documentos em tempo real – uma extensão natural de **how to sign document** em uma arquitetura orientada a serviços.

Sinta‑se à vontade para adaptar o código às suas políticas de segurança e compartilhar sua experiência nos comentários. Boa assinatura!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Change PDF Signature Language with Aspose.PDF for .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}