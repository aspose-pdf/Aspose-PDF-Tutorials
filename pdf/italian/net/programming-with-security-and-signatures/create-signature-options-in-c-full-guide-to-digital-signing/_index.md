---
category: general
date: 2026-08-14
description: Crea opzioni di firma in C# per applicare la firma digitale. Scopri come
  configurare la firma, implementare una funzione hash personalizzata e firmare i
  documenti programmaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: it
lastmod: 2026-08-14
og_description: Crea opzioni di firma in C# e applica una firma digitale. Questo tutorial
  ti guida nella configurazione della firma, nell'aggiunta di una funzione hash personalizzata
  e nella firma di un documento.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Crea opzioni di firma in C# – guida passo‑passo alla firma digitale
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
title: Crea opzioni di firma in C# – guida completa alla firma digitale
url: /it/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea opzioni di firma in C# – guida completa alla firma digitale

Crea opzioni di firma in C# per configurare un flusso di lavoro di firma digitale. Questo tutorial mostra come applicare una firma digitale, implementare una funzione hash personalizzata e firmare un documento utilizzando la classe `SignatureOptions`. Se hai mai dovuto firmare un PDF, XML o qualsiasi payload binario da un'applicazione .NET, i passaggi seguenti ti forniscono una soluzione pronta all'uso.

Imparerai a:

* configurare `SignatureOptions` con un algoritmo hash personalizzato,
* chiamare correttamente il metodo di firma,
* verificare che la firma sia stata applicata,
* evitare le insidie comuni nella configurazione della firma.

Le uniche prerequisiti sono un SDK .NET recente (≥ .NET 6) e una libreria di firma che espone `SignatureOptions` (ad esempio, **GroupDocs.Signature**, **Aspose.Signature**, o un'API simile). Non sono necessari strumenti esterni.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6 SDK or later | Fornisce le moderne funzionalità del linguaggio utilizzate negli esempi. |
| A signing‑library NuGet package (e.g., `GroupDocs.Signature`) | Fornisce il tipo `SignatureOptions` e il metodo di estensione `Sign`. |
| Access to a private key or certificate | Necessario per generare una firma digitale verificabile. |

Installa la libreria con la CLI standard:

```bash
dotnet add package GroupDocs.Signature
```

---

## Passo 1: Crea opzioni di firma

Il primo passo è istanziare `SignatureOptions` e impostare le proprietà che controllano il processo di firma. Questo oggetto indica alla libreria *cosa* firmare e *come* farlo.

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

**Perché è importante:** `SignatureOptions` funge da contratto tra il tuo codice e il motore di firma. Configurandolo in anticipo eviti boilerplate ripetuto quando firmi più documenti.

---

## Passo 2: Implementa una funzione hash personalizzata

Una *funzione hash personalizzata* ti dà il pieno controllo sul digest che l'algoritmo di firma firma. Questo è utile quando l'hash predefinito (SHA‑256) non soddisfa i requisiti di conformità o quando è necessario hashare una parte del documento.

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

**Perché è importante:** Assegnando `CustomSignHash`, sostituisci il passaggio di hashing interno della libreria con `MyHash`. Il motore di firma ora firmerà i byte restituiti dalla tua funzione, garantendo la conformità a qualsiasi politica personalizzata.

---

## Passo 3: Carica il documento e applica la firma digitale

Con le opzioni pronte, ora puoi aprire il file di destinazione e chiamare il metodo di firma. Il metodo `Sign` è fornito dalla libreria e utilizza le `SignatureOptions` configurate.

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

**Perché è importante:** La chiamata a `Sign` esegue tre azioni internamente:

1. **Calcolo hash** – ora delegato alla tua funzione hash personalizzata.
2. **Generazione firma** – usando la chiave privata fornita nella configurazione della libreria.
3. **Incorporamento** – la firma generata viene allegata al file di output.

Se qualche passaggio fallisce, il metodo restituisce `false`, consentendoti di gestire l'errore in modo elegante.

---

## Passo 4: Verifica che il documento sia firmato

Una rapida verifica conferma che la firma sia stata applicata correttamente. La maggior parte delle librerie espone un metodo `Verify` che controlla l'integrità del file firmato.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Perché è importante:** La verifica assicura che il documento firmato non sia stato manomesso dopo la firma e che l'hash personalizzato abbia prodotto un digest compatibile.

---

## Come configurare la firma per diversi tipi di file

Lo stesso oggetto `SignatureOptions` può essere riutilizzato per PDF, documenti Word, immagini o binari grezzi. L'unica modifica necessaria è la classe di opzioni specifica (ad es., `PdfSignatureOptions`, `WordSignatureOptions`). Ecco un rapido esempio per un'immagine JPEG:

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

**Perché è importante:** Comprendere come *configurare la firma* per ogni formato ti consente di estendere lo stesso codice a più tipi di documento senza riscrivere la logica di hashing.

---

## Problemi comuni e migliori pratiche

| Problema | Correzione consigliata |
|---------|-----------------|
| Dimenticare di impostare `CustomSignHash` dopo aver creato `SignatureOptions` | Assegnare il delegato subito dopo aver costruito l'oggetto delle opzioni. |
| Usare un algoritmo hash non supportato dal certificato di firma | Verificare che l'uso della chiave del certificato corrisponda alla lunghezza dell'hash (ad es., RSA‑2048 con SHA‑512). |
| Trascurare la necessità di rilasciare gli oggetti `Signature` | Avvolgere l'istanza `Signature` in un blocco `using` per rilasciare i handle dei file. |
| Salvare il file firmato sovrascrivendo l'originale | Scrivere sempre su un nuovo percorso file (`outputPath`) per preservare il documento originale. |

---

## Esempio completo funzionante

Di seguito è riportato un programma autonomo che mette insieme tutti i componenti. Copialo in un nuovo progetto console e eseguilo; la console segnalerà successo o fallimento.

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

**Output previsto**

```
Signature verified successfully.
```

Se la console stampa “Signing failed.” o “Signature verification failed.”, ricontrolla la configurazione del certificato e assicurati che l'hash personalizzato restituisca un array di byte della dimensione prevista.

---

## Conclusione

Ora sai come **creare opzioni di firma** in C#, allegare una **funzione hash personalizzata** e **applicare la firma digitale** a qualsiasi documento supportato. Il tutorial ha coperto l'intero ciclo di vita: configurare le opzioni, firmare il file e verificare il risultato. Riutilizzando la stessa istanza di `SignatureOptions` puoi anche **configurare la firma** per immagini, file Word o binari grezzi.

---

## Cosa fare dopo?

* Esplora proprietà aggiuntive di `SignatureOptions` come timbri visivi, server di timestamp e catene di certificati – questi sono allineati con la parola chiave **apply digital signature**.
* Sperimenta con altri algoritmi hash (ad es., Blake2b) sostituendo l'implementazione all'interno di `MyHash`.
* Integra il flusso di firma in un'API web per abilitare la firma di documenti al volo – un'estensione naturale di **how to sign document** in un'architettura orientata ai servizi.

Sentiti libero di adattare il codice alle tue politiche di sicurezza e condividi la tua esperienza nei commenti. Buona firma!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come cambiare la lingua della firma PDF con Aspose.PDF per .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Tutorial di firma digitale Aspose Pdf Net](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Tutorial di firma digitale Aspose Pdf Net](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}