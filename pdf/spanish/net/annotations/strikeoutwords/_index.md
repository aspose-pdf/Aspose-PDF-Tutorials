---
"description": "Aprenda a tachar palabras en un PDF con Aspose.PDF para .NET con esta completa guía paso a paso. Mejore sus habilidades de edición de documentos."
"linktitle": "Tachar palabras"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Tachar palabras"
"url": "/es/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tachar palabras

## Introducción

¿Alguna vez has tenido que tachar texto específico en un PDF para enfatizarlo? Ya sea que estés revisando documentos, marcando texto o simplemente necesites resaltar ciertas secciones, tachar palabras puede ser una herramienta valiosa. En este tutorial, exploraremos cómo hacerlo usando Aspose.PDF para .NET. Esta guía completa te guiará paso a paso, asegurándote de que tengas toda la información necesaria para implementar esta función eficazmente en tus aplicaciones .NET. 

## Prerrequisitos

Antes de pasar al código, hay algunos requisitos previos que deberás cumplir para seguir este tutorial:

1. Biblioteca Aspose.PDF para .NET: Asegúrese de tener instalada la biblioteca Aspose.PDF para .NET. Puede... [Descárgalo aquí](https://releases.aspose.com/pdf/net/).

2. .NET Framework: Asegúrese de tener .NET Framework instalado en su equipo. Este tutorial está diseñado para aplicaciones .NET.

3. Entorno de desarrollo: necesitará un IDE como Visual Studio para escribir y ejecutar su código.

4. Documento PDF: Tenga listo un archivo PDF de muestra con el que quiera trabajar. Este será el documento donde tacharemos el texto.

5. Conocimientos básicos de C#: es necesario estar familiarizado con la programación en C# para comprender e implementar los pasos de este tutorial.

## Importar paquetes

Antes de empezar a codificar, necesitamos importar los espacios de nombres necesarios en nuestro proyecto .NET. Esto nos dará acceso a las clases y métodos necesarios para manipular archivos PDF con Aspose.PDF.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Estos espacios de nombres son esenciales para trabajar con documentos PDF, manejar texto y agregar anotaciones como tachados.

En esta sección, desglosaremos el proceso de eliminar palabras en un documento PDF en pasos sencillos y fáciles de seguir. Cada paso irá acompañado de una explicación detallada para que comprenda cómo funciona todo.

## Paso 1: Cargue el documento PDF

El primer paso es cargar el documento PDF que desea editar. En este documento, deberá tachar palabras o frases específicas.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Abrir el documento PDF
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`: Esta variable contiene la ruta al directorio de su documento. Reemplazar `"YOUR DOCUMENT DIRECTORY"` con la ruta real donde se encuentra su archivo PDF.
- `Document`: El `Document` La clase representa un documento PDF. Al pasar la ruta del archivo a su constructor, abrimos el archivo PDF para su procesamiento.

## Paso 2: Crear un absorbedor de fragmentos de texto para encontrar texto específico

A continuación, crearemos una instancia de `TextFragmentAbsorber` Para buscar un fragmento de texto específico en el documento PDF. Esto nos permite localizar el texto que queremos eliminar.

```csharp
// Cree una instancia de TextFragment Absorber para buscar un fragmento de texto específico
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Esta clase se utiliza para buscar y trabajar con fragmentos de texto específicos dentro del documento PDF. En este ejemplo, buscamos la palabra "Estoque". Reemplace "Estoque" con la palabra o frase que desea encontrar en su documento.

## Paso 3: Iterar a través de las páginas del documento PDF

Ahora que tenemos nuestro `TextFragmentAbsorber`Necesitamos iterar a través de cada página del documento PDF para encontrar el texto especificado.

```csharp
// Iterar a través de las páginas del documento PDF
for (int i = 1; i <= document.Pages.Count; i++)
{
    // Obtener la página actual del documento PDF
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`:Este bucle itera a través de cada página del documento PDF.
- `document.Pages[i]`:Recupera la página actual que se está procesando.
- `page.Accept(textFragmentAbsorber)`:Este método aplica el `TextFragmentAbsorber` a la página actual, buscando el texto especificado.

## Paso 4: Recopilar y procesar los fragmentos de texto

Después de iterar a través de las páginas, recopilaremos los fragmentos de texto encontrados y los prepararemos para su posterior procesamiento.

```csharp
// Crear una colección de fragmentos de texto absorbidos
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Esta colección almacena todos los fragmentos de texto encontrados en el documento. La usaremos en el siguiente paso para eliminar el texto.

## Paso 5: Iterar a través de los fragmentos de texto y eliminarlos

En este paso, recorreremos cada fragmento de texto de nuestra colección y le aplicaremos una anotación de tachado.

```csharp
// Iterar sobre la colección de fragmentos de texto
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // Obtener las dimensiones rectangulares del objeto TextFragment
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Crear una instancia de anotación StrikeOut
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Establecer propiedades de la anotación tachada
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Añade la anotación a la colección de anotaciones de la página del fragmento de texto
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`:Esta línea recupera el fragmento de texto actual.
- `Aspose.Pdf.Rectangle`:Calculamos las dimensiones rectangulares del fragmento de texto para determinar dónde aplicar el tachado.
- `StrikeOutAnnotation`Esta clase representa la anotación de tachado. La instanciamos con el rectángulo calculado y la página actual.
- `strikeOut.Opacity`:Esta propiedad establece la opacidad del tachado, haciéndolo visible en un 80%.
- `strikeOut.Color`Hemos establecido el color del tachado en rojo. Puedes cambiarlo al color que prefieras.
- `textFragment.Page.Annotations.Add(strikeOut)`:Esto agrega la anotación tachada a la página.

## Paso 6: Guardar el documento PDF modificado

El paso final es guardar el documento PDF modificado con los tachados aplicados.

```csharp
// Guardar el documento PDF actualizado
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`Esto crea un nuevo nombre de archivo para el documento modificado. El archivo original permanece sin cambios.
- `document.Save(dataDir)`: Guarda el documento PDF con los tachados en la ubicación especificada.

## Conclusión

¡Felicitaciones! Has tachado palabras específicas en un documento PDF con Aspose.PDF para .NET. Siguiendo esta guía paso a paso, ahora puedes personalizar documentos PDF resaltando o tachando texto, haciéndolos más dinámicos y adaptados a tus necesidades. Ya sea que estés anotando documentos legales, preparando informes o simplemente marcando texto para su revisión, este tutorial te ha proporcionado las habilidades necesarias para hacerlo eficientemente.

## Preguntas frecuentes

### ¿Puedo cambiar el color del tachado?

Sí, puedes cambiar el color modificando el `strikeOut.Color` propiedad. Por ejemplo, puedes configurarlo como `Aspose.Pdf.Color.Blue` para un ponche azul.

### ¿Es posible tachar varias palabras a la vez?

¡Por supuesto! El `TextFragmentAbsorber` Se puede usar para buscar cualquier palabra o frase en el documento. Puede aplicar el tachado a varias instancias iterando a través de la `TextFragmentCollection`.

### ¿Qué pasa si quiero tachar texto sólo en páginas específicas?

Puedes modificar el bucle que itera por las páginas para incluir solo las que quieres modificar. Por ejemplo, `for (int i = 1; i <= 3; i++)` Aplicaría el tachado sólo a las primeras tres páginas.

### ¿Cómo puedo ajustar el grosor de la línea de tachado?

Puede ajustar el grosor de la línea tachada modificando el `Border` propiedad de la `StrikeOutAnnotation`Esto permite personalizar la apariencia del tachado.

### ¿Hay alguna forma de deshacer el tachado después de guardar el documento?

Una vez guardado el documento, el tachado es permanente. Si necesita conservar el texto original sin el tachado, considere guardar una copia de seguridad del documento original antes de aplicar cualquier modificación.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}