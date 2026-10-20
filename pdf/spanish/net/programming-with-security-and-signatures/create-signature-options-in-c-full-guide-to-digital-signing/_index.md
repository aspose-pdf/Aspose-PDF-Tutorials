---
category: general
date: 2026-08-14
description: Crea opciones de firma en C# para aplicar una firma digital. Aprende
  cómo configurar la firma, implementar una función hash personalizada y firmar documentos
  programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: es
lastmod: 2026-08-14
og_description: Crea opciones de firma en C# y aplica una firma digital. Este tutorial
  te guía paso a paso en la configuración de la firma, la incorporación de una función
  hash personalizada y la firma de un documento.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Crear opciones de firma en C# – guía paso a paso para la firma digital
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
title: Crear opciones de firma en C# – guía completa de firma digital
url: /es/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear opciones de firma en C# – guía completa para la firma digital

Crear opciones de firma en C# para configurar un flujo de trabajo de firma digital. Este tutorial muestra cómo aplicar una firma digital, implementar una función hash personalizada y firmar un documento usando la clase `SignatureOptions`. Si alguna vez necesitaste firmar un PDF, XML o cualquier carga binaria desde una aplicación .NET, los pasos a continuación te proporcionan una solución lista para ejecutar.

Aprenderás a:

* configurar `SignatureOptions` con un algoritmo hash personalizado,
* invocar el método de firma correctamente,
* verificar que la firma se haya aplicado,
* evitar errores comunes al configurar la firma.

Los únicos requisitos previos son un SDK reciente de .NET (≥ .NET 6) y una biblioteca de firma que exponga `SignatureOptions` (por ejemplo, **GroupDocs.Signature**, **Aspose.Signature**, o una API similar). No se requieren herramientas externas.

---

## Prerrequisitos

| Requisito | Por qué es importante |
|-------------|----------------|
| .NET 6 SDK o posterior | Proporciona las características modernas del lenguaje usadas en los ejemplos. |
| Un paquete NuGet de biblioteca de firma (p. ej., `GroupDocs.Signature`) | Suministra el tipo `SignatureOptions` y el método de extensión `Sign`. |
| Acceso a una clave privada o certificado | Necesario para generar una firma digital verificable. |

Instala la biblioteca con la CLI estándar:

```bash
dotnet add package GroupDocs.Signature
```

---

## Paso 1: Crear opciones de firma

El primer paso es instanciar `SignatureOptions` y establecer las propiedades que controlan el proceso de firma. Este objeto indica a la biblioteca *qué* firmar y *cómo* hacerlo.

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

**Por qué es importante:** `SignatureOptions` actúa como un contrato entre tu código y el motor de firma. Al configurarlo de antemano evitas código repetitivo cuando firmas varios documentos.

---

## Paso 2: Implementar una función hash personalizada

Una *función hash personalizada* te brinda control total sobre el digest que el algoritmo de firma firma. Esto es útil cuando el hash predeterminado (SHA‑256) no cumple con los requisitos de cumplimiento o cuando necesitas hash de una parte del documento.

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

**Por qué es importante:** Al asignar `CustomSignHash`, sustituyes el paso interno de hash de la biblioteca por `MyHash`. El motor de firma ahora firmará los bytes devueltos por tu función, garantizando el cumplimiento de cualquier política personalizada.

---

## Paso 3: Cargar el documento y aplicar la firma digital

Con las opciones preparadas, ahora puedes abrir el archivo objetivo y llamar al método de firma. El método `Sign` lo proporciona la biblioteca y utiliza el `SignatureOptions` configurado.

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

**Por qué es importante:** La llamada a `Sign` realiza tres acciones internamente:

1. **Cálculo del hash** – ahora delegada a tu función hash personalizada.
2. **Generación de la firma** – usando la clave privada suministrada a la configuración de la biblioteca.
3. **Incorporación** – la firma generada se adjunta al archivo de salida.

Si alguna etapa falla, el método devuelve `false`, permitiéndote manejar el error de forma elegante.

---

## Paso 4: Verificar que el documento esté firmado

Una verificación rápida confirma que la firma se aplicó correctamente. La mayoría de las bibliotecas exponen un método `Verify` que comprueba la integridad del archivo firmado.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Por qué es importante:** La verificación asegura que el documento firmado no haya sido manipulado después de la firma y que el hash personalizado haya producido un digest compatible.

---

## Cómo configurar la firma para diferentes tipos de archivo

El mismo objeto `SignatureOptions` puede reutilizarse para PDFs, documentos Word, imágenes o binarios simples. El único cambio necesario es la clase de opciones específica (p. ej., `PdfSignatureOptions`, `WordSignatureOptions`). Aquí tienes un ejemplo rápido para una imagen JPEG:

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

**Por qué es importante:** Entender cómo *configurar la firma* para cada formato te permite extender la misma base de código a múltiples tipos de documento sin reescribir la lógica de hash.

---

## Errores comunes y buenas prácticas

| Error | Solución recomendada |
|---------|-----------------|
| Olvidar establecer `CustomSignHash` después de crear `SignatureOptions` | Asigna el delegado inmediatamente después de construir el objeto de opciones. |
| Usar un algoritmo hash que el certificado de firma no soporta | Verifica que el uso de clave del certificado coincida con la longitud del hash (p. ej., RSA‑2048 con SHA‑512). |
| Pasar por alto la necesidad de disponer los objetos `Signature` | Envuelve la instancia `Signature` en un bloque `using` para liberar los manejadores de archivo. |
| Guardar el archivo firmado sobre la fuente original | Siempre escribe en una ruta de archivo nueva (`outputPath`) para preservar el documento original. |

---

## Ejemplo completo funcional

A continuación se muestra un programa autocontenido que reúne todas las piezas. Cópialo en un nuevo proyecto de consola y ejecútalo; la consola informará éxito o fracaso.

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

**Salida esperada**

```
Signature verified successfully.
```

Si la consola muestra “Signing failed.” o “Signature verification failed.”, revisa la configuración del certificado y asegura que la función hash personalizada devuelva una matriz de bytes del tamaño esperado.

---

## Conclusión

Ahora sabes cómo **crear opciones de firma** en C#, adjuntar una **función hash personalizada** y **aplicar una firma digital** a cualquier documento compatible. El tutorial cubrió todo el ciclo de vida: configurar las opciones, firmar el archivo y verificar el resultado. Reutilizando la misma instancia de `SignatureOptions` también puedes **cómo configurar la firma** para imágenes, archivos Word o binarios crudos.

---

## ¿Qué sigue?

* Explora propiedades adicionales de `SignatureOptions` como sellos visuales, servidores de timestamp y cadenas de certificados – se alinean con la palabra clave **apply digital signature**.
* Experimenta con otros algoritmos hash (p. ej., Blake2b) cambiando la implementación dentro de `MyHash`.
* Integra el flujo de firma en una API web para habilitar la firma de documentos sobre la marcha – una extensión natural de **how to sign document** en una arquitectura orientada a servicios.

¡Siéntete libre de adaptar el código a tus propias políticas de seguridad y comparte tu experiencia en los comentarios! ¡Feliz firma!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Change PDF Signature Language with Aspose.PDF for .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}