---
"description": "Aprenda a establecer una fecha de caducidad en archivos PDF con Aspose.PDF para .NET. Mejore la seguridad de sus documentos con esta guía paso a paso."
"linktitle": "Establecer fecha de caducidad en archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Establecer fecha de caducidad en archivo PDF"
"url": "/es/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Establecer fecha de caducidad en archivo PDF

## Introducción

En la era digital actual, gestionar y proteger documentos es más crucial que nunca. Imagina enviar un PDF que se vuelve inaccesible automáticamente después de cierta fecha. ¿Suena mágico, verdad? Pues bien, con Aspose.PDF para .NET, puedes establecer fácilmente una fecha de caducidad para tus archivos PDF. Esta función es especialmente útil para documentos confidenciales que necesitan restringirse después de cierto tiempo. En este tutorial, te guiaremos paso a paso en el proceso de establecer una fecha de caducidad en un archivo PDF. ¡Así que, ponte a programar y manos a la obra!

## Prerrequisitos

Antes de comenzar, hay algunas cosas que debes tener en cuenta:

1. Entorno de desarrollo: Asegúrese de tener configurado un entorno de desarrollo .NET. Este podría ser Visual Studio o cualquier otro IDE compatible con .NET.
2. Aspose.PDF para .NET: Necesita tener instalada la biblioteca Aspose.PDF. Si aún no lo ha hecho, puede descargarla desde [aquí](https://releases.aspose.com/pdf/net/).
3. Conocimientos básicos de C#: Este tutorial asume que tienes conocimientos básicos de programación en C#. Si eres nuevo en C#, ¡no te preocupes! Lo explicaremos de forma sencilla y directa.

## Importar paquetes

Para empezar a usar Aspose.PDF, necesitas importar los espacios de nombres necesarios en tu proyecto de C#. Así es como puedes hacerlo:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Estos espacios de nombres le brindan acceso a las funcionalidades principales necesarias para trabajar con documentos PDF en Aspose.PDF.

## Paso 1: Configure su directorio de documentos

Primero, debe especificar la ruta del directorio de sus documentos. Aquí se guardará el PDF resultante. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Reemplazar `"YOUR DOCUMENT DIRECTORY"` Con la ruta donde quieres guardar tu archivo PDF. Es como decirle a tu programa: "¡Aquí guardo mis archivos!".

## Paso 2: Crear una instancia del objeto de documento

A continuación, debe crear una nueva instancia del `Document` Clase. Este es tu lienzo donde crearás tu PDF.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Piensa en el `Document` El objeto es una hoja en blanco. ¡Puedes añadirle el contenido que quieras!

## Paso 3: Agregar una página al PDF

Ahora que tienes tu documento configurado, es hora de añadirle una página. Aquí es donde irá tu contenido.

```csharp
doc.Pages.Add();
```

Acabas de crear una nueva página en tu PDF. Es como añadir una nueva página a tu cuaderno donde puedes anotar tus ideas.

## Paso 4: Agregar texto a la página

Hagamos esta página un poco más interesante añadiendo texto. Añadiremos un simple mensaje de "Hola mundo".

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Esta línea de código añade un fragmento de texto a la primera página de tu PDF. ¡Es como escribir un título en la parte superior de la página!

## Paso 5: Crear JavaScript para la fecha de caducidad

¡Ahora viene la parte divertida! Crearás una acción de JavaScript que comprobará la fecha de caducidad del PDF. Si la fecha actual supera la fecha de caducidad, un mensaje alertará al usuario.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Esto es lo que está pasando:
- Usted define el año y mes de vencimiento.
- Obtendrás la fecha de hoy.
- Compara la fecha de hoy con la fecha de vencimiento.
- ¡Si la fecha de hoy ha pasado la fecha de vencimiento, aparecerá un mensaje!

## Paso 6: Configurar JavaScript como acción para abrir PDF

Ahora, debe configurar la acción de JavaScript como la acción de apertura para su documento PDF. Esto significa que JavaScript se ejecutará en cuanto se abra el PDF.

```csharp
doc.OpenAction = javaScript;
```

Esta línea le indica al PDF que ejecute el JavaScript al abrirlo. ¡Es como configurar un recordatorio que suena al abrir el calendario!

## Paso 7: Guarde el documento PDF

Finalmente, es el momento de guardar su documento PDF con la función de fecha de caducidad. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Esta línea guarda tu PDF en el directorio especificado con el nombre "SetExpiryDate_out.pdf". ¡Es como enmarcar tu obra terminada!

## Conclusión

¡Y listo! Has creado correctamente un archivo PDF con fecha de caducidad usando Aspose.PDF para .NET. Esta función no solo mejora la seguridad, sino que también garantiza que la información confidencial se mantenga bajo control. Ya sea que envíes contratos, informes o cualquier otro documento importante, establecer una fecha de caducidad puede ser un cambio radical.

## Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?
Aspose.PDF para .NET es una potente biblioteca que permite a los desarrolladores crear, manipular y convertir documentos PDF en aplicaciones .NET.

### ¿Puedo utilizar Aspose.PDF gratis?
Sí, puedes usar una versión de prueba gratuita de Aspose.PDF. Puedes descargarla. [aquí](https://releases.aspose.com/).

### ¿Cómo compro Aspose.PDF?
Puedes comprar Aspose.PDF visitando el sitio web [página de compra](https://purchase.aspose.com/buy).

### ¿Qué pasa si necesito ayuda?
Si tiene alguna pregunta o necesita ayuda, puede visitar el [Foro de soporte de Aspose](https://forum.aspose.com/c/pdf/10).

### ¿Puedo obtener una licencia temporal para Aspose.PDF?
Sí, puedes solicitar una licencia temporal [aquí](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}