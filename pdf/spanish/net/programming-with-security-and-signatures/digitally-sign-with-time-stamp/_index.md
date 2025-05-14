---
"description": "Aprenda a firmar digitalmente un PDF con una marca de tiempo usando Aspose.PDF para .NET. Esta guía paso a paso cubre los prerrequisitos, la configuración del certificado, la marca de tiempo y más."
"linktitle": "Firma digital con sello de tiempo en archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Firma digital con sello de tiempo en archivo PDF"
"url": "/es/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Firma digital con sello de tiempo en archivo PDF

## Introducción

¿Alguna vez has necesitado firmar digitalmente un PDF e incluir una marca de tiempo para mayor seguridad? Ya sea que trabajes con documentos legales, contratos o cualquier documento que requiera autenticación segura, una firma digital con marca de tiempo añade una capa extra de credibilidad. En este tutorial, te explicaremos cómo usar Aspose.PDF para .NET para agregar una firma digital y una marca de tiempo a tus documentos PDF. ¡No te preocupes, te lo explicaremos paso a paso!

## Prerrequisitos

Antes de profundizar en el código, deberá configurar algunos aspectos para poder seguir el proceso. Aquí tiene una breve lista de requisitos previos para empezar:

- Biblioteca Aspose.PDF para .NET: Necesitará tener la biblioteca Aspose.PDF para .NET instalada en su proyecto. Puede... [Descargue la última versión aquí](https://releases.aspose.com/pdf/net/) o agréguelo a su proyecto a través de NuGet.
- Un documento PDF: Necesitará un archivo PDF de muestra para trabajar con él. Asegúrese de tener un archivo en el directorio de su proyecto que desee firmar.
- Certificado digital (archivo PFX): asegúrese de tener un certificado digital (un `.pfx` archivo) para firmar digitalmente el documento.
- URL de sellado de tiempo: este es un servicio de sellado de tiempo en línea que se utilizará para adjuntar una marca de tiempo a la firma digital. 
- Conocimientos básicos de C#: no necesitas ser un experto, pero conocer los conceptos básicos de C# te ayudará a comprender y personalizar el código.

Una vez que hayas marcado todas estas casillas, ¡estarás listo para comenzar a codificar!

## Importar paquetes

Para comenzar, deberá importar los siguientes espacios de nombres a su proyecto de C#. Esto le garantizará acceso a las clases y funciones relevantes de Aspose.PDF.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Paso 1: Cargue el documento PDF

Lo primero que debemos hacer es cargar el documento PDF que queremos firmar. Así es como se hace:

```csharp
// Define la ruta a tu directorio de documentos
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Cargar el documento PDF
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Este paso es bastante sencillo. Simplemente definimos la ruta al documento que queremos firmar. `Document` La clase de Aspose.PDF maneja la carga del archivo.

## Paso 2: Configurar la firma digital

A continuación, crearemos la firma digital usando la clase PKCS7 y cargaremos el archivo PFX. Este archivo PFX contiene su certificado y clave privada, necesarios para firmar el documento.

```csharp
// Ruta a su archivo .pfx
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Inicializar el objeto de firma
PdfFileSignature signature = new PdfFileSignature(document);

// Cargue el archivo PFX con una contraseña
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

En este punto, le estás indicando a Aspose que use tu certificado digital para firmar el documento. `PKCS7` object maneja todo el trabajo criptográfico para usted, por lo que no tiene que preocuparse por los detalles esenciales.

## Paso 3: Agregar la configuración de la marca de tiempo

Uno de los componentes clave de una firma digital robusta es el sello de tiempo. Este garantiza que la firma del documento pueda verificarse incluso después de la expiración del certificado. Configuremos el sello de tiempo utilizando una autoridad de sellado de tiempo en línea.

```csharp
// Definir la configuración de la marca de tiempo
TimestampSettings timestampSettings = new TimestampSettings("https://su_url_de_marca_de_tiempo", "usuario:contraseña");

// Agregar configuraciones de marca de tiempo al objeto PKCS7
pkcs.TimestampSettings = timestampSettings;
```

Aquí, especifica la URL del servicio de sellado de tiempo, que asignará automáticamente la fecha y la hora a su firma. Esto puede hacerse con o sin autenticación.

## Paso 4: Definir la ubicación y la apariencia de la firma

Ahora, definiremos dónde aparecerá la firma en el PDF y sus dimensiones. Puedes personalizar la posición y el tamaño del recuadro de la firma en la página.

```csharp
// Define la apariencia y ubicación de la firma (página 1, con rectángulo especificado)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Aquí, definimos un rectángulo que posiciona la firma en las coordenadas (100, 100) en la primera página del PDF, con un ancho de 200 y una altura de 100. Puedes cambiar estos valores para que se ajusten a tu diseño.

## Paso 5: Firme el documento PDF

Con todo configurado, es hora de aplicar la firma digital al PDF. Este paso combina el certificado, la marca de tiempo y la posición en un solo comando.

```csharp
// Firme el documento en la primera página
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Esto es lo que está pasando:
- 1: Esto indica que la firma debe aplicarse en la primera página.
- "Motivo de la firma": aquí puedes especificar por qué estás firmando el documento.
- “Contacto”: Ingrese la información de contacto del firmante.
- "Ubicación": especifique la ubicación del firmante.
- verdadero: este valor booleano indica si la firma es visible en el documento.
- rect: El rectángulo que definimos anteriormente especifica el tamaño y la posición de la firma.
- pkcs: El objeto PKCS7 contiene la configuración del certificado digital y de la marca de tiempo.

## Paso 6: Guarde el PDF firmado

Una vez firmado el documento, solo queda guardarlo. Puedes elegir un nuevo nombre de archivo para conservar tanto la versión original como la firmada.

```csharp
// Guardar el documento PDF firmado
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

¡Su PDF recién firmado y con marca de tiempo ahora está guardado en el directorio especificado!

## Conclusión

¡Y listo! Has firmado digitalmente un PDF con marca de tiempo usando Aspose.PDF para .NET. Este proceso garantiza la autenticidad e integridad de tus documentos, brindándote tranquilidad tanto a ti como al destinatario. Las firmas digitales son cada vez más esenciales en el mundo digital actual, por lo que dominar este proceso es sin duda una habilidad que vale la pena adquirir.

## Preguntas frecuentes

### ¿Puedo utilizar un formato de archivo diferente para el certificado?  
Sí, pero el tutorial se centra en el uso de un archivo PFX, que es el formato más común para certificados digitales.

### ¿Necesito una conexión a Internet para aplicar la marca de tiempo?  
Sí, dado que la marca de tiempo se obtiene de una autoridad de sellado de tiempo en línea, necesitará acceso a Internet.

### ¿Puedo firmar varias páginas en un PDF?  
¡Por supuesto! Puedes modificarlo. `signature.Sign()` Método para apuntar a múltiples páginas o recorrer todas las páginas.

### ¿Qué sucede si la contraseña del archivo PFX es incorrecta?  
Recibirás una excepción si la contraseña es incorrecta, así que asegúrate de ingresarla correctamente.

### ¿Puedo hacer la firma invisible?  
Sí, puedes pasar `false` hacia `Sign` parámetro de visibilidad del método para hacer la firma invisible.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}