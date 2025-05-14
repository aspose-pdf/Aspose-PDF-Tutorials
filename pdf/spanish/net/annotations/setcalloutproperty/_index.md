---
"description": "Aprenda a configurar la propiedad de llamada en un archivo PDF usando Aspose.PDF para .NET en este tutorial detallado paso a paso."
"linktitle": "Establecer la propiedad de llamada en un archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Establecer la propiedad de llamada en un archivo PDF"
"url": "/es/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Establecer la propiedad de llamada en un archivo PDF

## Introducción

Crear documentos PDF profesionales y visualmente atractivos suele requerir la adición de anotaciones que dirijan la atención a contenido específico. Una de estas anotaciones es el callout, que es similar a esos bocadillos de diálogo que se ven en los cómics. Ayudan a aclarar o enfatizar el texto dentro del PDF. Aspose.PDF para .NET facilita enormemente la adición de este tipo de anotaciones a los documentos, y en este tutorial, explicaremos cómo configurar la propiedad callout en un archivo PDF con esta potente biblioteca. Tanto si eres un desarrollador experimentado como si estás empezando, al final de esta guía comprenderás claramente cómo trabajar con callouts en archivos PDF.

## Prerrequisitos

Antes de sumergirnos en el código, cubramos los aspectos esenciales que necesitas para comenzar.

1. Aspose.PDF para .NET: Asegúrate de tener instalada la biblioteca Aspose.PDF para .NET. Puedes descargarla desde [aquí](https://releases.aspose.com/pdf/net/).
2. IDE: Un entorno de desarrollo como Visual Studio.
3. .NET Framework: asegúrese de tener .NET instalado en su máquina.
4. Licencia temporal: si desea probar todas las funciones de Aspose.PDF sin limitaciones, obtenga una [licencia temporal](https://purchase.aspose.com/temporary-license/).

## Importar paquetes

Antes de comenzar a escribir el código, debe importar los paquetes necesarios que le permitirán trabajar con archivos PDF y anotaciones.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Estas importaciones le proporcionarán todas las clases y métodos necesarios para manipular documentos PDF y crear anotaciones como el llamado.

## Paso 1: Inicializar el documento PDF

El primer paso es crear un nuevo documento PDF donde añadiremos nuestra anotación de llamada. Piense en esto como si estuviera creando un lienzo en blanco donde puede empezar a añadir elementos.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Inicializar un nuevo documento PDF
Document doc = new Document();
```
Aquí estamos creando uno nuevo `Document` objeto que servirá como nuestro archivo PDF. El `dataDir` La variable se establece en el directorio donde desea guardar el archivo PDF una vez que hayamos terminado.

## Paso 2: Agregar una nueva página al documento

Un documento PDF puede tener varias páginas, y en este paso, agregaremos una nueva. En esta página se colocará la anotación de llamada.

```csharp
// Agregar una nueva página al documento
Page page = doc.Pages.Add();
```
El `Pages.Add()` El método se utiliza para agregar una nueva página a la `doc` objeto. La nueva página se almacena en el `page` variable, que usaremos más adelante cuando agreguemos la anotación.

## Paso 3: Definir la apariencia predeterminada

Las anotaciones, al igual que el texto destacado, tienen una apariencia visual personalizable. En este paso, definiremos el aspecto del texto dentro del texto destacado.

```csharp
// Definir la apariencia predeterminada para la anotación
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Nosotros creamos una `DefaultAppearance` Objeto que define el color del texto y el tamaño de fuente. Aquí, el texto será rojo y el tamaño de fuente será 10. Esta apariencia se aplicará a la anotación de llamada.

## Paso 4: Crear la anotación de texto libre

Ahora es el momento de crear la anotación. La anotación de texto libre nos permite añadir un texto destacado con un estilo específico.

```csharp
// Crear una anotación de texto libre con una llamada
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Nosotros creamos una `FreeTextAnnotation` objeto con coordenadas específicas, que definen su posición en la página. El `Intent` está configurado para `FreeTextCallout`, lo que indica que se trata de una anotación de llamada. El `EndingStyle` está configurado para `OpenArrow`, lo que significa que la línea de llamada terminará con una flecha abierta.

## Paso 5: Defina los puntos de la línea de llamada

Una anotación de llamada tiene una línea que señala el área de interés. Aquí, definiremos los puntos que componen esta línea.

```csharp
// Define los puntos para la línea de llamada
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
El `Callout` La propiedad es un conjunto de `Point` Objetos, cada uno representando una coordenada en la página. Estos puntos definen la trayectoria de la línea de llamada, dándole la apariencia clásica de bocadillo de diálogo.

## Paso 6: Agregar la anotación a la página

Después de crear y configurar nuestra anotación, el siguiente paso es agregarla a la página.

```csharp
// Añadir la anotación a la página
page.Annotations.Add(fta);
```
El `Annotations.Add()` Se utiliza el método para colocar la anotación en la página que creamos anteriormente. Este paso dibuja la llamada en la página PDF.

## Paso 7: Establecer el contenido de texto enriquecido

Las anotaciones de llamada pueden incluir texto enriquecido, lo que permite incluir contenido formateado dentro de la burbuja. Añadamos un texto de muestra.

```csharp
// Establecer el texto enriquecido para la anotación
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Este es un ejemplo</span></p></body>";
```
El `RichText` La propiedad se configura con el contenido HTML. Esto permite un formato detallado dentro del texto destacado, como especificar el tamaño, el color y el estilo de la fuente.

## Paso 8: Guarde el documento PDF

Finalmente, tras configurar todo, debemos guardar el documento. Este paso finaliza la creación del PDF con la anotación de llamada.

```csharp
// Guardar el documento
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
El `Save()` El método guarda el documento en el directorio especificado con el nombre de archivo "SetCalloutProperty.pdf". Con este paso, finalizamos el proceso de creación del PDF.

## Conclusión

¡Y listo! Acabas de crear un documento PDF con una anotación de llamada usando Aspose.PDF para .NET. Esta anotación puede ser increíblemente útil para resaltar o explicar partes específicas de tu documento. Aspose.PDF ofrece una potente API que simplifica y flexibiliza la manipulación de PDF. Ya sea que estés añadiendo anotaciones, convirtiendo documentos o gestionando tareas complejas con PDF, Aspose.PDF te cubre las espaldas.

## Preguntas frecuentes

### ¿Puedo personalizar aún más la apariencia del llamado?

¡Por supuesto! Puedes personalizar varios aspectos, como el color y el grosor de la línea, así como la familia y el estilo de fuente del texto.

### ¿Es posible agregar múltiples llamadas en una sola página?

Sí, puedes agregar tantas llamadas como necesites repitiendo los pasos para cada anotación.

### ¿Cómo cambio la posición del llamado?

Simplemente modifique las coordenadas en el `Rectangle` y `Callout` Propiedades para reposicionar la anotación.

### ¿Puedo agregar otros tipos de anotaciones usando Aspose.PDF?

Sí, Aspose.PDF admite varios tipos de anotaciones, incluidos resaltados, sellos y archivos adjuntos.

### ¿El contenido de texto enriquecido está limitado a HTML?

El `RichText` La propiedad admite un subconjunto de HTML, lo que le permite incluir texto con estilo y formato básico.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}