---
"description": "Descubra el poder de Aspose.PDF para .NET. Aprenda a configurar JavaScript en campos de formulario con nuestra guía paso a paso."
"linktitle": "Establecer Java Script"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Establecer Java Script"
"url": "/es/net/programming-with-forms/set-java-script/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Establecer Java Script

## Introducción

Crear archivos PDF dinámicos e interactivos puede mejorar significativamente la experiencia del usuario, especialmente al integrar formularios y campos en un documento. Una potente biblioteca que lo hace posible es Aspose.PDF para .NET. En este artículo, profundizaremos en la configuración de JavaScript para campos de formulario con Aspose.PDF, garantizando que sus archivos PDF no solo se vean bien, sino que también funcionen a la perfección.

## Prerrequisitos

Antes de comenzar a codificar, asegurémonos de que tienes todo lo que necesitas para seguir sin problemas:

- Visual Studio (o cualquier IDE .NET): asegúrese de tenerlo instalado y configurado correctamente.
  
- Biblioteca Aspose.PDF: Necesitará la última versión de esta biblioteca. Puede descargarla. [aquí](https://releases.aspose.com/pdf/net/).

- Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.

- Archivos PDF: Debe tener un archivo PDF listo para la prueba. En nuestro ejemplo, usaremos un archivo llamado `SetJavaScript.pdf`.

- Tu directorio de documentos: Conoce dónde se almacenan tus archivos. Haremos referencia a esta ruta en nuestro código.

Una vez que tenga estos prerrequisitos listos, ¿qué herramientas utilizaremos? Exploremos lo que Aspose.PDF puede hacer.

## Importar paquetes

Para comenzar, debe incluir los espacios de nombres necesarios en su proyecto de C#. Abra el archivo principal de C# y agregue las siguientes instrucciones de importación:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Estos espacios de nombres proporcionan acceso al PDF y a la funcionalidad relacionada con formularios dentro de la biblioteca Aspose.PDF.

¿Listo para que tu PDF sea interactivo? ¡Aprende a programar y veamos cómo funciona paso a paso!

## Paso 1: Definir la ruta del documento

Primero, necesitamos especificar la ubicación de nuestro archivo PDF. Esto sienta las bases para todo lo que sigue. Así es como se hace:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Reemplazar `"YOUR DOCUMENT DIRECTORY"` Con la ruta real donde se encuentra tu archivo PDF. Piensa en esto como establecer las coordenadas de un mapa del tesoro: ¡necesitas saber dónde está la "X"!

## Paso 2: Cargue el documento PDF

Una vez que hayamos definido el directorio, cargaremos nuestro archivo PDF. 

```csharp
Document doc = new Document(dataDir + "SetJavaScript.pdf");
```

Esta línea abre el archivo PDF especificado y lo prepara para su manipulación. 

## Paso 3: Acceda al campo de formulario

A continuación, queremos acceder al campo de formulario donde aplicaremos nuestro JavaScript. 

```csharp
TextBoxField field = (TextBoxField)doc.Form["textbox1"];
```

Aquí, asumimos que hay un cuadro de texto en su PDF llamado `textbox1`Si no tiene un campo con este nombre, puede cambiarle el nombre o ajustar el código según corresponda. 

## Paso 4: Configurar acciones de JavaScript

Ahora, ¡añadamos funcionalidad a nuestro cuadro de texto! Configuraremos acciones de JavaScript que se activarán ante ciertos eventos. 

```csharp
field.Actions.OnModifyCharacter = new JavascriptAction("AFNumber_Keystroke(2, 1, 1, 0, \"\", true)");
field.Actions.OnFormat = new JavascriptAction("AFNumber_Format(2, 1, 1, 0, \"\", true)");
```

Esto es lo que está pasando:
- OnModifyCharacter: Esta función de JavaScript especifica cómo debe comportarse el campo al modificarse un carácter. En este caso, permite dos decimales después del número sin separador.
- OnFormat: Esto garantiza que cuando el usuario formatea el número, este se adhiere a la misma regla.

Al configurar estas acciones, esencialmente le damos una personalidad a nuestro cuadro de texto, ¡como si le enseñáramos un paso de baile!

## Paso 5: Inicializar el valor del campo

A continuación, vamos a darle a nuestro cuadro de texto un punto de partida estableciendo un valor inicial. 

```csharp
field.Value = "123";
```

Esta línea establece "123" como el valor predefinido en el cuadro de texto. Es como preparar el escenario para una actuación.

## Paso 6: Guardar el PDF modificado

Por último, debemos guardar nuestro documento después de realizar todos estos cambios.

```csharp
dataDir = dataDir + "Restricted_out.pdf";
doc.Save(dataDir);
```

Esto actualiza el archivo original con sus cambios y lo guarda como `Restricted_out.pdf`Piense en esto como sellar el destino de su PDF: una vez guardado, ¡estará listo para el mundo!

## Paso 7: Confirmar el éxito

Por último, comprobemos si todo ha ido bien. 

```csharp
Console.WriteLine("\nJavaScript on form field setup successfully.\nFile saved at " + dataDir);
```

Al ejecutar este mensaje, tendrá la seguridad de que la operación se ha completado con éxito, como recibir un aplauso del público después de una gran actuación.

## Conclusión

¡Felicitaciones! Has configurado correctamente JavaScript para campos de formulario en un PDF con Aspose.PDF para .NET. Este tutorial no solo te proporcionó las herramientas para mejorar la interacción del usuario, sino que también te permitió personalizar tus documentos como un profesional. Ya sea que trabajes con formularios en facturas, encuestas u otros PDF interactivos, las posibilidades son infinitas.

### Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?  
Aspose.PDF es una biblioteca diseñada para crear, editar y manipular archivos PDF dentro de aplicaciones .NET, proporcionando potentes funcionalidades de PDF.

### ¿Necesito una licencia para utilizar Aspose.PDF?  
Aunque hay una prueba gratuita disponible, se requiere una licencia para usarla completamente sin limitaciones. Puedes comprar una licencia. [aquí](https://purchase.aspose.com/buy).

### ¿Puedo configurar JavaScript en otros tipos de campos de formulario?  
¡Por supuesto! Aspose.PDF permite acciones de JavaScript en diversos campos de formulario, como casillas de verificación, botones de opción y menús desplegables.

### ¿Cómo puedo obtener ayuda para los problemas con Aspose.PDF?  
Puede acceder al soporte a través de su [foro](https://forum.aspose.com/c/pdf/10) Para cualquier consulta o problema.

### ¿Hay alguna forma de probar Aspose.PDF sin comprarlo?  
¡Sí! Aspose ofrece una [prueba gratuita](https://releases.aspose.com/) para probar las características de la biblioteca antes de comprometerse con una compra.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}