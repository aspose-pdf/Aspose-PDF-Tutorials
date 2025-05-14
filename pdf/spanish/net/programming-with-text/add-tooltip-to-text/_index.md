---
"description": "Aprenda a añadir información sobre herramientas al texto de archivos PDF con Aspose.PDF para .NET. Mejore sus PDF con textos informativos al pasar el cursor fácilmente."
"linktitle": "Agregar información sobre herramientas al texto en un archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Agregar información sobre herramientas al texto en un archivo PDF"
"url": "/es/net/programming-with-text/add-tooltip-to-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar información sobre herramientas al texto en un archivo PDF

## Introducción

la hora de crear PDF atractivos e interactivos, la información sobre herramientas puede ser invaluable. ¿Conoces esos pequeños cuadros emergentes que te ofrecen información adicional al pasar el cursor sobre algo? Pueden proporcionar contexto, descripciones o incluso consejos sin sobrecargar el documento. En este tutorial, te explicaremos cómo añadir información sobre herramientas al texto de un archivo PDF con la biblioteca Aspose.PDF para .NET. Tanto si eres un desarrollador experimentado como si estás empezando en el mundo de los PDF, ¡estás en el lugar adecuado! ¡Comencemos!

## Prerrequisitos

Antes de pasar a la parte de codificación, asegurémonos de que tienes todo lo que necesitas para seguir sin problemas.

### Visual Studio instalado
Es esencial tener Visual Studio instalado en su máquina, ya que será su entorno de desarrollo principal para aplicaciones .NET.

### Biblioteca Aspose.PDF para .NET
También necesitarás tener la biblioteca Aspose.PDF a tu disposición. Puedes [Descárgalo aquí](https://releases.aspose.com/pdf/net/)Asegúrese de incluirlo en las referencias de su proyecto.

### Conocimientos básicos de C#
Tener conocimientos de C# será muy útil, ya que programaremos en ese lenguaje. Pero no te preocupes, ¡te guiaré paso a paso!

### Un documento PDF para trabajar
Puedes comenzar con un documento PDF en blanco, como hacemos en este ejemplo, o utilizar uno existente si lo prefieres.

¡Ahora, pasemos a la parte de codificación!

## Importar paquetes 

El primer paso en nuestra aventura de programación consiste en importar los paquetes necesarios. Abra su proyecto de Visual Studio y, en la parte superior de su archivo de C#, deberá agregar lo siguiente: `using` directivas:

```csharp
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
```

Estos paquetes le brindan acceso a todas las clases y funcionalidades que necesita para crear y manipular documentos PDF.

## Paso 1: Configure su directorio de documentos

Primero, necesitamos configurar la ruta donde guardarás tus documentos. Piensa en esto como encontrar un lugar seguro en tu sistema de archivos donde residirán todas tus creaciones.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outputFile = dataDir + "Tooltip_out.pdf";
```

Asegúrese de reemplazar `YOUR DOCUMENT DIRECTORY` con la ruta actual en su máquina.

## Paso 2: Crear un documento PDF de muestra

A continuación, es hora de crear un PDF sencillo con texto. ¡Aquí es donde iniciamos nuestro proceso creativo!

```csharp
// Crear un documento de muestra con texto
Document doc = new Document();
doc.Pages.Add().Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a tooltip"));
doc.Pages[1].Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a very long tooltip"));
doc.Save(outputFile);
```

En este paso, creamos un documento, agregamos dos fragmentos de texto y lo guardamos en la ruta previamente especificada.

## Paso 3: Abra el documento para procesarlo

¡Ahora que hemos creado nuestro documento, abrámoslo para que podamos trabajar en esas descripciones emergentes!

```csharp
// Abrir documento con texto
Document document = new Document(outputFile);
```

Aquí, simplemente cargamos el documento que acabamos de crear.

## Paso 4: Crear un absorbedor de texto para encontrar fragmentos de texto

Necesitamos encontrar los fragmentos de texto donde queremos añadir la información sobre herramientas. ¡Es como usar una lupa para resaltar una parte específica de un mapa grande! 

```csharp
// Cree un objeto TextAbsorber para encontrar todas las frases que coincidan con la expresión regular
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a tooltip");
document.Pages.Accept(absorber);
```

## Paso 5: Extraer fragmentos de texto

continuación, extraemos los fragmentos de texto que encontramos en nuestro paso anterior.

```csharp
// Obtener los fragmentos de texto extraídos
TextFragmentCollection textFragments = absorber.TextFragments;
```

Este fragmento nos permite conservar referencias de los fragmentos de texto que nos interesan.

## Paso 6: Recorrer los fragmentos y agregar información sobre herramientas

¡Ahora viene la parte divertida! Recorreremos cada fragmento de texto y añadiremos una descripción emergente a cada uno. Imagina envolver pequeños regalos (descripciones emergentes) alrededor de elementos específicos (fragmentos de texto).

```csharp
// Recorrer los fragmentos
foreach (TextFragment fragment in textFragments)
{
	// Crear un botón invisible en la posición del fragmento de texto
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// El valor de AlternateName se mostrará como información sobre herramientas en una aplicación de visualización
	field.AlternateName = "Tooltip for text.";
	// Agregar campo de botón al documento
	document.Form.Add(field);
}
```

En cada iteración, creamos un campo de botón que corresponde a la posición del fragmento de texto y le asignamos el texto de la información sobre herramientas.

## Paso 7: Repetir para las descripciones emergentes largas

Al igual que añadimos una descripción emergente sencilla, podemos hacer lo mismo con texto más largo. ¡Desarrollemos nuestra creatividad!

```csharp
// A continuación se mostrará un ejemplo de una descripción emergente muy larga.
absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a very long tooltip");
document.Pages.Accept(absorber);
textFragments = absorber.TextFragments;
foreach (TextFragment fragment in textFragments)
{
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// Establecer texto muy largo
	field.AlternateName = "Lorem ipsum dolor sit amet, consectetur adipiscing elit," +
							" sed do eiusmod tempor incididunt ut labore et dolore magna" +
							" aliqua. Ut enim ad minim veniam, quis nostrud exercitation" +
							" ullamco laboris nisi ut aliquip ex ea commodo consequat." +
							" Duis aute irure dolor in reprehenderit in voluptate velit" +
							" esse cillum dolore eu fugiat nulla pariatur. Excepteur sint" +
							" occaecat cupidatat non proident, sunt in culpa qui officia" +
							" deserunt mollit anim id est laborum.";
	document.Form.Add(field);
}
```

Aquí estamos haciendo el mismo tipo de trabajo que antes, pero con una información sobre herramientas mucho más extendida.

## Paso 8: Guarde su documento

El paso final es guardar el documento con todas esas nuevas y brillantes descripciones emergentes. 

```csharp
// Guardar documento
document.Save(outputFile);
```

¡Listo! Has añadido información sobre herramientas a tu PDF, haciéndolo más intuitivo e interactivo.

## Conclusión

Aquí la tienes: una guía fácil de seguir sobre cómo añadir información sobre herramientas al texto de archivos PDF con Aspose.PDF para .NET. Esta técnica puede mejorar significativamente la experiencia del usuario, haciendo que tus documentos sean más informativos sin abrumar al lector con demasiado texto. 

Con solo pasar el cursor sobre una palabra o frase, el lector obtiene información relevante que aporta valor sin ser redundante. ¡Así que, anímate y pruébalo! En un abrir y cerrar de ojos, podrías estar creando todo tipo de documentos atractivos y que destaquen.

## Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?
Aspose.PDF para .NET es una biblioteca que permite a los desarrolladores crear, manipular y convertir documentos PDF en aplicaciones .NET.

### ¿Puedo utilizar Aspose.PDF gratis?
Sí, Aspose ofrece una prueba gratuita para que explores sus funciones. Puedes encontrarla. [aquí](https://releases.aspose.com/).

### ¿Hay opciones de licencia disponibles para Aspose.PDF?
Sí, puedes comprar una licencia u obtener una licencia temporal. Consulta las opciones. [aquí](https://purchase.aspose.com/).

### ¿Puedo agregar elementos interactivos además de información sobre herramientas usando Aspose.PDF?
¡Por supuesto! Aspose.PDF permite añadir diversos elementos interactivos como hipervínculos, botones y formularios.

### ¿Dónde puedo encontrar más documentación sobre Aspose.PDF?
Puedes consultar la documentación [aquí](https://reference.aspose.com/pdf/net/) para obtener una orientación más detallada.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}