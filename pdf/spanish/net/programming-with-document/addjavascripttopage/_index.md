---
"description": "Aprenda a añadir JavaScript a archivos PDF con Aspose.PDF para .NET. Guía paso a paso con tutoriales de código para scripting a nivel de documento y página."
"linktitle": "Agregar archivo PDF de Java Script"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Agregar Java Script a un archivo PDF"
"url": "/es/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar Java Script a un archivo PDF

## Introducción

¿Alguna vez te has preguntado cómo mejorar tus PDF con elementos interactivos como alertas emergentes o funciones de impresión automática? ¡Buenas noticias! ¡Puedes! Con Aspose.PDF para .NET, puedes añadir JavaScript a tus documentos PDF sin problemas. Ya sea que estés automatizando tareas o creando experiencias de usuario dinámicas, incrustar JavaScript en PDF les da a tus archivos un nivel extra de funcionalidad.

## Prerrequisitos

Antes de pasar a la parte de codificación, hay algunas cosas que deberás tener configuradas:

- Aspose.PDF para .NET: Descargue la biblioteca desde [Lanzamientos de Aspose](https://releases.aspose.com/pdf/net/) o conseguir uno [prueba gratuita](https://releases.aspose.com/).
- Entorno de desarrollo: cualquier IDE compatible con .NET como Visual Studio.
- Conocimientos básicos de C#: esta guía asume que está familiarizado con la sintaxis básica de C#.
- Licencia Temporal (Opcional): Puedes obtener una [licencia temporal](https://purchase.aspose.com/temporary-license/) Si quieres evitar limitaciones durante tu desarrollo.

## Importar paquetes

Antes de empezar a escribir código, deberá importar los espacios de nombres necesarios de la biblioteca Aspose.PDF. Estos espacios de nombres le permitirán manipular archivos PDF y añadir acciones de JavaScript fácilmente.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Ahora que ha importado los espacios de nombres correctos, está todo listo para comenzar a codificar.

## Paso 1: Cargar un PDF existente

Primero lo primero: debes cargar el documento PDF al que quieres añadir JavaScript. Este paso prepara el terreno para todas las modificaciones posteriores. Imagina que tienes un PDF que quieres mejorar con funciones dinámicas, como imprimirlo automáticamente al abrirlo.

Aquí te explicamos cómo puedes cargar ese archivo PDF:

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Cargar un archivo PDF existente
Document doc = new Document(dataDir + "input.pdf");
```

En este fragmento de código, usamos el `Document` Clase para cargar un archivo PDF existente desde el directorio especificado. Asegúrese de reemplazar `"YOUR DOCUMENT DIRECTORY"` con la ruta real a su archivo PDF.

## Paso 2: Agregar JavaScript a nivel de documento

Ahora, agreguemos JavaScript que se activará al abrir el documento. En este ejemplo, escribiremos un script que abre el cuadro de diálogo de impresión en cuanto el usuario abre el PDF.

JavaScript a nivel de documento es perfecto para acciones que desee aplicar a todo el PDF. Piense en ello como si estuviera configurando una regla global para su documento.

Aquí está el código:

```csharp
// Agregar JavaScript a nivel de documento
// Crear una instancia de JavascriptAction con la declaración de JavaScript deseada
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// Asignar objeto JavascriptAction a OpenAction del documento
doc.OpenAction = javaScript;
```

En este paso, creamos un `JavascriptAction` objeto que define una función de JavaScript para abrir el cuadro de diálogo de impresión cuando se abre el documento. El `doc.OpenAction` A continuación, a la propiedad se le asigna esta acción de JavaScript.

## Paso 3: Agregar JavaScript a nivel de página

No todas las acciones tienen que afectar a todo el documento. A veces, es necesario que se ejecuten acciones específicas al abrir o cerrar ciertas páginas. Aquí, configuraremos acciones de JavaScript para cuando se abra o cierre una página específica (por ejemplo, la página 2).

El JavaScript a nivel de página es útil para interacciones específicas. Puede ser desde mostrar un mensaje cuando un usuario accede a una página hasta acciones personalizadas como el autocompletado de campos de formulario.

Aquí te explicamos cómo hacerlo:

```csharp
// Agregar JavaScript a nivel de página
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

En este fragmento de código, agregamos dos acciones de JavaScript:
1. Acción OnOpen: muestra una alerta que dice “Página 2 abierta” cuando el usuario abre la página 2.
2. Acción OnClose: muestra una alerta que dice “Página 2 cerrada” cuando el usuario sale de la página 2.

Esto añade interactividad a tu PDF. Imagina guiar al usuario a través de una serie de pasos en diferentes páginas, con alertas que aparecen al entrar o salir de una página.

## Paso 4: Guardar el documento PDF

Ya has añadido JavaScript tanto al documento como a las páginas específicas. El último paso es guardar el PDF modificado en la ubicación deseada. Este paso es sencillo, pero crucial: ¡no olvides guardar tu trabajo!

Aquí está el código:

```csharp
// Especifique la ruta del archivo de salida
dataDir = dataDir + "JavaScript-Added_out.pdf";

// Guardar el documento PDF actualizado
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

En este fragmento, guardamos el documento actualizado con el JavaScript agregado en un nuevo archivo llamado `"JavaScript-Added_out.pdf"`Esto garantiza que no sobrescriba el archivo original y le brinda una copia de seguridad con la que trabajar.

## Conclusión

Añadir JavaScript a archivos PDF con Aspose.PDF para .NET es una forma eficaz de crear PDF interactivos y dinámicos. Ya sea que automatice tareas como la impresión o cree alertas personalizadas, la posibilidad de incrustar JavaScript en sus PDF hace que sus documentos sean más atractivos y funcionales.

## Preguntas frecuentes

### ¿Puedo agregar múltiples acciones de JavaScript a diferentes páginas de un PDF?
Sí, puedes asignar diferentes acciones de JavaScript a páginas individuales o a todo el documento.

### ¿Es posible eliminar JavaScript de un PDF después de agregarlo?
Sí, puedes eliminar o modificar acciones de JavaScript existentes borrando la `Actions` propiedades del documento o página.

### ¿Qué tipos de funciones de JavaScript puedo utilizar en un PDF?
Puede utilizar cualquier JavaScript compatible con el motor JavaScript de Adobe Acrobat, como impresión, alertas y manipulaciones de formularios.

### ¿Funciona JavaScript en todos los visores de PDF?
La mayoría de las acciones de JavaScript funcionan en visores de PDF compatibles con archivos PDF interactivos, como Adobe Acrobat. Sin embargo, es posible que algunos lectores de PDF básicos no sean compatibles con JavaScript.

### ¿Puedo activar acciones de JavaScript en función de la entrada del usuario en el PDF?
Sí, puedes vincular JavaScript a los campos de formulario para activar acciones según la entrada del usuario.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}