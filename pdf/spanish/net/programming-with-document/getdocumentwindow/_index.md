---
"description": "Aprenda a utilizar la función GetDocumentWindow de Aspose.PDF para .NET para recuperar información sobre las propiedades de la ventana de un documento PDF."
"linktitle": "Ventana Obtener documento"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Ventana Obtener documento"
"url": "/es/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ventana Obtener documento

# Introducción

¿Trabaja con archivos PDF y desea tener más control sobre su apariencia al abrirlos? Ya sea para ocultar la barra de menú o para ajustar el tamaño de la ventana a la primera página, Aspose.PDF para .NET le ofrece todas las herramientas necesarias para personalizar el comportamiento de un PDF al abrirlo en un visor. En este tutorial, explicaremos cómo recuperar y manipular la configuración de la ventana del documento en Aspose.PDF para .NET.


# Prerrequisitos

Antes de sumergirse en el tutorial, asegúrese de tener los siguientes requisitos previos:

- Aspose.PDF para .NET instalado en su entorno de desarrollo.
  - [Descargar Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/)
- Una licencia válida para Aspose.PDF, o puede obtener una [prueba gratuita](https://releases.aspose.com/) o [licencia temporal](https://purchase.aspose.com/temporary-license/).
- Comprensión básica de .NET y C#.
- Visual Studio u otro IDE adecuado.

# Importar paquetes

Antes de empezar a escribir código, deberá importar los paquetes necesarios. Abra su proyecto y, en la parte superior de su archivo de C#, agregue el siguiente espacio de nombres:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Esto le dará acceso a todas las clases y métodos necesarios para manipular documentos PDF utilizando Aspose.PDF para .NET.

Ahora, analicemos el proceso de recuperación de diferentes configuraciones de la ventana del documento. Para este ejemplo, usaremos un archivo PDF de muestra llamado `GetDocumentWindow.pdf`.

## Paso 1: Establecer la ruta del directorio del documento

Primero, debemos definir la ruta de nuestro archivo PDF. Es fundamental que la ruta sea correcta para evitar errores durante la ejecución.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Aquí, reemplace `"YOUR DOCUMENT DIRECTORY"` Con el directorio donde se encuentra tu archivo PDF. Este es tu directorio de trabajo desde donde cargarás el documento PDF.

## Paso 2: Abra el documento PDF

Una vez establecida la ruta del archivo, el siguiente paso es abrir el documento PDF con Aspose.PDF. Esto cargará el documento en la memoria, lo que le permitirá recuperar sus propiedades.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

Con esta sencilla línea de código, has cargado con éxito tu archivo PDF en el `pdfDocument` objeto, que ahora le permitirá acceder a todas sus propiedades.

## Paso 3: Recuperar el estado de centrado de la ventana

A continuación, verifiquemos si la ventana del documento debe estar centrada al abrirse. El valor predeterminado es `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Si la salida es `true`La ventana del documento se abrirá en el centro de la pantalla. De lo contrario, se abrirá en su posición predeterminada.

## Paso 4: Verificar la dirección del texto

Otro aspecto crucial de la apariencia de un PDF es la dirección del texto, que determina si se lee de izquierda a derecha (L2R) o de derecha a izquierda (R2L). Puede obtener esta información con el siguiente código:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

La salida será `L2R` para texto de izquierda a derecha y `R2L` Para texto de derecha a izquierda. Esta configuración es especialmente útil para documentos en idiomas como el árabe o el hebreo.

## Paso 5: Mostrar el título del documento en la ventana

La siguiente propiedad permite controlar si el título del documento o el nombre del archivo deben mostrarse en la barra de título de la ventana. De forma predeterminada, está configurado en `false`, lo que significa que se mostrará el nombre del archivo.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Si desea que se muestre el título del documento en lugar del nombre del archivo, esta configuración debe estar habilitada.

## Paso 6: Cambiar el tamaño de la ventana para que se ajuste a la primera página

A veces, puede que quieras que la ventana del documento se ajuste automáticamente al tamaño de la primera página del PDF al abrirlo. Aquí te explicamos cómo comprobar si esta función está habilitada:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

De forma predeterminada, esto está configurado en `false`, lo que significa que el tamaño de la ventana permanecerá como está independientemente del tamaño de la primera página.

## Paso 7: Ocultar la barra de menú

Para una experiencia de lectura más enfocada, puede que desee ocultar la barra de menú de la aplicación de visualización. Puede recuperar esta configuración con la siguiente línea:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

Esto volverá `true` Si la barra de menú está oculta, y `false` de lo contrario.

## Paso 8: Ocultar la barra de herramientas

De igual forma, también podría querer ocultar la barra de herramientas en el visor de PDF para una interfaz más limpia. Esta configuración se puede recuperar de la siguiente manera:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Si esta configuración está habilitada, la barra de herramientas se ocultará cuando se abra el PDF.

## Paso 9: Ocultar las barras de desplazamiento y los elementos de la interfaz de usuario

Si desea mostrar solo el contenido de la página sin ningún elemento de interfaz de usuario adicional, como barras de desplazamiento, esta configuración controla ese comportamiento:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

Cuando se establece en `true`El visor de PDF ocultará las barras de desplazamiento y otros elementos de la interfaz de usuario, dejando solo el contenido del documento.

## Paso 10: Establecer el modo de página no de pantalla completa

Puede controlar cómo aparece el documento al salir del modo de pantalla completa utilizando el `NonFullScreenPageMode` Propiedad. Esta configuración es útil para definir cómo debe interactuar el usuario con el documento en modo de pantalla no completa.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

La salida se puede configurar en diferentes modos, como miniaturas, contornos o panel de archivos adjuntos.

## Paso 11: Definir el diseño de la página

Esta configuración le permite controlar la disposición de las páginas del documento. Por ejemplo, puede optar por una vista de página única o una vista de columnas continuas:

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

Esto brinda a los usuarios flexibilidad en cómo leen o ven el contenido del documento.

## Paso 12: Especificar el modo de página

Por último, el `PageMode` La propiedad define cómo se mostrará el documento al abrirlo. Las opciones incluyen mostrar miniaturas, pasar al modo de pantalla completa o mostrar el panel de archivos adjuntos.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

Dependiendo de sus necesidades, puede configurarlo en cualquier modo que se adapte al propósito de su PDF.

## Conclusión

Como puede ver, Aspose.PDF para .NET ofrece herramientas completas para manipular la visualización de sus documentos PDF en diversos visores. Ya sea que desee ocultar la barra de herramientas, centrar la ventana o controlar la dirección del texto, Aspose.PDF ofrece la flexibilidad para mejorar la experiencia de visualización del usuario.

# Preguntas frecuentes

### ¿Puedo personalizar el nivel de zoom inicial del PDF?
Sí, Aspose.PDF le permite establecer el nivel de zoom cuando se abre el documento.

### ¿Cómo puedo bloquear el tamaño de la ventana de un PDF?
Puedes configurar el `FitWindow` Propiedad para evitar que la ventana cambie de tamaño.

### ¿Aspose.PDF admite diferentes modos de lectura?
Sí, admite diferentes modos, como pantalla completa, miniaturas y archivos adjuntos.

### ¿Es posible ocultar las barras de desplazamiento en el visor de PDF?
Por supuesto, puedes ocultar las barras de desplazamiento configurando `HideWindowUI` propiedad a `true`.

### ¿Puedo centrar la ventana del documento cuando está abierta?
Sí, puedes controlar esto configurando el `CenterWindow` propiedad.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}