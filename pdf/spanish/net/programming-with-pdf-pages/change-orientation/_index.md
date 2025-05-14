---
"description": "Guía paso a paso para cambiar la orientación de un PDF con Aspose.PDF para .NET. Fácil de seguir e implementar en tus proyectos."
"linktitle": "Cambiar la orientación"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Cambiar la orientación"
"url": "/es/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar la orientación

## Introducción

¿Alguna vez has tenido problemas con un archivo PDF cuya orientación de página está... desfasada? Quizás se trata de un documento escaneado o creado incorrectamente, y es necesario rotar las páginas para que tengan sentido. Por suerte, Aspose.PDF para .NET ofrece una forma sencilla y eficaz de manipular archivos PDF de prácticamente cualquier forma imaginable, incluyendo cambiar la orientación de las páginas. Tanto si quieres cambiar de vertical a horizontal como viceversa, esta guía te guiará paso a paso por el proceso.

Entonces, si estás listo para sumergirte y rotar esas páginas PDF con facilidad, ¡comencemos!

## Prerrequisitos

Antes de entrar en detalles sobre cómo cambiar la orientación de la página en tu PDF, veamos rápidamente lo que necesitarás tener en cuenta:

- Aspose.PDF para .NET: Asegúrate de tener instalada la biblioteca Aspose.PDF para .NET. Si no la tienes, puedes... [Descárgalo aquí](https://releases.aspose.com/pdf/net/).
- Un entorno de desarrollo .NET: puede utilizar Visual Studio, JetBrains Rider o cualquier IDE preferido para trabajar con .NET.
- Conocimientos básicos de C#: si bien esta guía es sencilla, algunos conocimientos básicos de C# harán que sea aún más fácil seguirla.
- Un archivo PDF: El ejemplo a continuación asume que tiene un archivo PDF con varias páginas. Si no tiene uno a mano, cree o descargue un PDF de muestra para trabajar con él.

Además, si recién estás comenzando, puedes probar Aspose.PDF con un [licencia temporal gratuita](https://purchase.aspose.com/temporary-license/) Antes de decidir [comprar la versión completa](https://purchase.aspose.com/buy).

## Importar espacios de nombres

Antes de poder manipular la orientación de las páginas de su PDF, deberá importar los espacios de nombres necesarios en su proyecto de C#. Asegúrese de tener lo siguiente:

```csharp
using System.IO;
using Aspose.Pdf;
```

Con esto importado, pasemos a la parte principal del tutorial.

## Paso 1: Cargue el documento PDF

Lo primero que debemos hacer es cargar el archivo PDF que desea modificar. Puede usar el `Document` clase del espacio de nombres Aspose.PDF para abrir su PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Esta línea carga el PDF desde el directorio especificado. Asegúrese de reemplazar `"YOUR DOCUMENT DIRECTORY"` con la ruta real a su archivo. El `"input.pdf"` es el PDF cuya orientación desea cambiar.

## Paso 2: Recorre cada página

Ahora que tenemos el documento cargado, vamos a recorrer cada página del PDF. Usaremos un `foreach` bucle para recorrer cada página, permitiéndonos aplicar el cambio de orientación a todas ellas.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipular cada página
}
```

Este bucle iterará a través de todas las páginas del documento.

## Paso 3: Obtener el MediaBox de la página

Cada página de un PDF tiene una `MediaBox` Que define los límites de la página. Necesitamos acceder a él para determinar la orientación actual y modificarla.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

El `MediaBox` nos da las dimensiones de la página, como su ancho, alto y posicionamiento.

## Paso 4: Intercambia el ancho y la altura

Para cambiar la orientación de la página de vertical a horizontal o de horizontal a vertical, simplemente intercambiamos los valores de ancho y alto. Este paso ajustará las dimensiones de la página.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Este código intercambia la altura y el ancho y reposiciona la esquina inferior izquierda (`LLY`) para que el contenido encaje perfectamente después de la rotación.

## Paso 5: Actualizar MediaBox y CropBox

Ahora que tenemos la nueva altura y ancho, apliquemos los cambios a la página. `MediaBox` y `CropBox`. El `CropBox` es esencial si el documento original tenía un conjunto, asegurando que toda la página se muestre correctamente.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Este paso redimensiona la página según las nuevas dimensiones que acabamos de calcular.

## Paso 6: Girar la página

Finalmente, configuramos el ángulo de rotación de la página. Aspose.PDF lo simplifica muchísimo. Podemos rotar la página 90 grados para cambiar de vertical a horizontal o viceversa.

```csharp
page.Rotate = Rotation.on90;
```

Este código gira la página 90 grados, girándola a la orientación deseada.

## Paso 7: Guardar el PDF de salida

Después de aplicar los cambios de orientación a todas las páginas, guardamos el documento modificado en un nuevo archivo. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Asegúrese de proporcionar un nuevo nombre de archivo (en este caso, `ChangeOrientation_out.pdf`) para guardar el resultado. De esta forma, no sobrescribes el archivo original.

### Conclusión

¡Y listo! Cambiar la orientación de un archivo PDF con Aspose.PDF para .NET es tan sencillo como cargar el documento, recorrer las páginas, ajustar el MediaBox y guardar el archivo actualizado. Tanto si se trata de un documento mal escaneado como si necesita rotar páginas para adaptarlas a sus necesidades de formato, esta guía paso a paso le ayudará.

## Preguntas frecuentes

### ¿Puedo rotar páginas específicas en lugar de todas las páginas del PDF?  
Sí, puedes modificar el bucle para apuntar a páginas específicas usando su índice en lugar de recorrer todas las páginas.

### ¿Qué es el? `MediaBox`?  
El `MediaBox` Define el tamaño y la forma de la página en un archivo PDF. Es donde se coloca el contenido de la página.

### ¿Aspose.PDF para .NET funciona con otros formatos de archivos?  
Sí, Aspose.PDF puede manejar una variedad de formatos de archivos como HTML, XML, XPS y más.

### ¿Existe una versión gratuita de Aspose.PDF para .NET?  
Sí, puedes empezar con un [prueba gratuita](https://releases.aspose.com/) o solicitar una [licencia temporal](https://purchase.aspose.com/temporary-license/).

### ¿Puedo deshacer los cambios una vez guardados?  
Una vez que guarde el documento, los cambios serán permanentes. Asegúrese de trabajar en una copia o guardar una copia de seguridad del archivo original.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}