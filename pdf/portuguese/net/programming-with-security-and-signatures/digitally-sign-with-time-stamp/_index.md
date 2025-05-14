---
"description": "Aprenda a assinar digitalmente um PDF com carimbo de data/hora usando o Aspose.PDF para .NET. Este guia passo a passo aborda pré-requisitos, configuração de certificado, carimbo de data/hora e muito mais."
"linktitle": "Assine digitalmente com carimbo de data/hora em arquivo PDF"
"second_title": "Referência da API Aspose.PDF para .NET"
"title": "Assine digitalmente com carimbo de data/hora em arquivo PDF"
"url": "/pt/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Assine digitalmente com carimbo de data/hora em arquivo PDF

## Introdução

Você já precisou assinar digitalmente um PDF e incluir um carimbo de data/hora para maior segurança? Seja trabalhando em documentos jurídicos, contratos ou qualquer coisa que exija autenticação segura, uma assinatura digital com carimbo de data/hora adiciona uma camada extra de credibilidade. Neste tutorial, explicaremos como você pode usar o Aspose.PDF para .NET para adicionar uma assinatura digital e um carimbo de data/hora aos seus documentos PDF. Não se preocupe, vamos passo a passo!

## Pré-requisitos

Antes de mergulharmos no código, há algumas coisas que você precisa configurar para prosseguir. Aqui está uma lista de verificação rápida dos pré-requisitos para você começar:

- Biblioteca Aspose.PDF para .NET: Você precisará da biblioteca Aspose.PDF para .NET instalada em seu projeto. Você pode [baixe a versão mais recente aqui](https://releases.aspose.com/pdf/net/) ou adicione-o ao seu projeto via NuGet.
- Um documento PDF: você precisará de um arquivo PDF de exemplo para trabalhar. Certifique-se de ter um arquivo no diretório do seu projeto que você deseja assinar.
- Certificado Digital (arquivo PFX): Certifique-se de ter um certificado digital (um `.pfx` arquivo) para assinar digitalmente o documento.
- URL de registro de data e hora: Este é um serviço de registro de data e hora on-line que será usado para anexar um registro de data e hora à assinatura digital. 
- Conhecimento básico de C#: você não precisa ser um especialista, mas conhecer os conceitos básicos de C# ajudará você a entender e personalizar o código.

Depois de marcar todas essas caixas, você estará pronto para começar a programar!

## Pacotes de importação

Para começar, você precisará importar os seguintes namespaces para o seu projeto C#. Isso garante que você tenha acesso às classes e funções Aspose.PDF relevantes.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Etapa 1: Carregue o documento PDF

A primeira coisa que precisamos fazer é carregar o documento PDF que queremos assinar. Veja como fazer isso:

```csharp
// Defina o caminho para o diretório do seu documento
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Carregar o documento PDF
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Esta etapa é bastante simples. Estamos apenas definindo o caminho para o documento que queremos assinar. `Document` classe do Aspose.PDF manipula o carregamento do arquivo.

## Etapa 2: Configurar a assinatura digital

Em seguida, criaremos a assinatura digital usando a classe PKCS7 e carregaremos o arquivo PFX. Este arquivo PFX contém seu certificado e chave privada, necessários para assinar o documento.

```csharp
// Caminho para seu arquivo .pfx
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Inicializar o objeto de assinatura
PdfFileSignature signature = new PdfFileSignature(document);

// Carregue o arquivo PFX com uma senha
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

Neste ponto, você está dizendo ao Aspose para usar seu certificado digital para assinar o documento. `PKCS7` O objeto cuida de todo o trabalho criptográfico para você, para que não precise se preocupar com detalhes essenciais.

## Etapa 3: adicione as configurações de registro de data e hora

Um dos principais componentes de uma assinatura digital robusta é o carimbo de data/hora. Ele garante que a assinatura do documento possa ser verificada mesmo após a expiração do certificado. Vamos configurar o carimbo de data/hora usando uma autoridade de carimbo de data/hora online.

```csharp
// Definir configurações de registro de data e hora
TimestampSettings timestampSettings = new TimestampSettings("https://your_timestamp_url", "usuário:senha");

// Adicionar configurações de registro de data e hora ao objeto PKCS7
pkcs.TimestampSettings = timestampSettings;
```

Aqui, você especifica a URL para o serviço de carimbo de data/hora, que fornecerá automaticamente a hora e a data para sua assinatura. Isso pode ser feito com ou sem autenticação.

## Etapa 4: Defina a localização e a aparência da assinatura

Agora, definiremos onde a assinatura aparecerá no PDF e suas dimensões. Você pode personalizar a posição da caixa de assinatura na página, bem como o tamanho.

```csharp
// Defina a aparência e a localização da assinatura (página 1, com retângulo especificado)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Aqui, estamos definindo um retângulo que posiciona a assinatura nas coordenadas (100, 100) na primeira página do PDF, com largura de 200 e altura de 100. Você pode alterar esses valores para ajustá-los ao seu design.

## Etapa 5: Assine o documento PDF

Com tudo configurado, é hora de aplicar a assinatura digital ao PDF. Esta etapa combina o certificado, o carimbo de data/hora e o posicionamento em um comando simples.

```csharp
// Assine o documento na primeira página
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Veja o que está acontecendo:
- 1: Isso indica que a assinatura deve ser aplicada à primeira página.
- "Motivo da assinatura": aqui você pode especificar o motivo pelo qual está assinando o documento.
- "Contato": insira as informações de contato do signatário.
- "Localização": especifique a localização do signatário.
- true: Este valor booleano indica se a assinatura está visível no documento.
- retângulo: O retângulo que definimos anteriormente especifica o tamanho e a posição da assinatura.
- pkcs: O objeto PKCS7 contém as configurações do certificado digital e do registro de data e hora.

## Etapa 6: Salve o PDF assinado

Depois que o documento for assinado, basta salvá-lo. Você pode escolher um novo nome de arquivo para manter tanto a versão original quanto a assinada.

```csharp
// Salvar o documento PDF assinado
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Seu PDF recém-assinado e com carimbo de data/hora agora está salvo no diretório especificado!

## Conclusão

pronto! Você assinou digitalmente um PDF com carimbo de data/hora usando o Aspose.PDF para .NET. Esse processo garante a autenticidade e a integridade dos seus documentos, proporcionando tranquilidade tanto para você quanto para o destinatário. As assinaturas digitais estão se tornando cada vez mais essenciais no mundo digital de hoje, portanto, dominar esse processo é definitivamente uma habilidade que vale a pena ter.

## Perguntas frequentes

### Posso usar um formato de arquivo diferente para o certificado?  
Sim, mas o tutorial se concentra no uso de um arquivo PFX, que é o formato mais comum para certificados digitais.

### Preciso de uma conexão com a internet para aplicar o registro de data e hora?  
Sim, como o registro de data e hora é obtido de uma autoridade de registro de data e hora on-line, você precisará de acesso à Internet.

### Posso assinar várias páginas de um PDF?  
Com certeza! Você pode modificar o `signature.Sign()` método para atingir várias páginas ou fazer um loop em todas elas.

### O que acontece se a senha do arquivo PFX estiver incorreta?  
Você receberá uma exceção se a senha estiver errada, então certifique-se de que ela foi digitada corretamente.

### Posso tornar a assinatura invisível?  
Sim, você pode passar `false` para o `Sign` parâmetro de visibilidade do método para tornar a assinatura invisível.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}