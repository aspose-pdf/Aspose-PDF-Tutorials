---
"description": "Aprenda a añadir y eliminar JavaScript en documentos PDF con Aspose.PDF para .NET. Guía paso a paso con tutoriales de código para scripting a nivel de documento."
"linktitle": "Agregar o quitar Javascript al documento"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Agregar o quitar Javascript a un documento PDF"
"url": "/es/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar o quitar Javascript a un documento PDF

## Introducción

En esta guía, explicaremos cómo usar Aspose.PDF para .NET para insertar JavaScript en un archivo PDF y cómo eliminarlo cuando sea necesario. Al finalizar este tutorial, comprenderá claramente cómo manipular JavaScript en archivos PDF sin esfuerzo.

## Prerrequisitos

Antes de sumergirnos en el código, hay algunas cosas que deberás tener configuradas:

1. Aspose.PDF para .NET: Necesitará tener la biblioteca Aspose.PDF para .NET instalada en su proyecto. Si aún no la tiene, descargue la biblioteca desde [Página de descarga de Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/).
2. IDE o editor de texto: puede utilizar cualquier IDE compatible con .NET como Visual Studio.
3. Conocimientos básicos de C#: este tutorial supone que está cómodo con C# y familiarizado con la manipulación de PDF.
4. Licencia: Asegúrese de solicitar una licencia válida para evitar limitaciones. Puede obtener una licencia temporal en [aquí](https://purchase.aspose.com/temporary-license/).

## Importar paquetes

Para empezar a usar Aspose.PDF para .NET, deberá importar los espacios de nombres necesarios a su proyecto. A continuación, le explicamos cómo:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

Estos dos espacios de nombres son esenciales. `Aspose.Pdf` le permite trabajar con documentos PDF, mientras `System.Collections` Se utilizará para manejar claves JavaScript.

Analicemos todo el proceso de agregar y eliminar JavaScript de un PDF en pasos fáciles de seguir.

## Paso 1: Inicializar un nuevo documento PDF

Lo primero que debes hacer es crear un nuevo documento PDF. Este documento servirá como lienzo en blanco para agregar JavaScript.

```csharp
Document doc = new Document();
doc.Pages.Add();
```

Aquí estamos inicializando un nuevo `Document` objeto y añadirle una página en blanco. Piensa en esto como la base de tu PDF.

## Paso 2: Agregar JavaScript al PDF

Ahora que tenemos un documento, es hora de agregarle JavaScript. JavaScript en PDF permite agregar comportamientos personalizados, como alertas o validación de formularios.

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

En este fragmento de código, agregamos dos funciones de JavaScript (`func1` y `func2`) al PDF. Estas funciones pueden realizar diversas tareas, según sus necesidades. Aquí, simplemente llamamos a una función de marcador de posición llamada `hello()`.

## Paso 3: Guarde el PDF con JavaScript

Una vez que haya agregado el JavaScript deseado, es momento de guardar el PDF.

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

Esto guardará el documento con JavaScript bajo el nombre `AddJavascript.pdf` en el directorio especificado (`dataDir`).

## Paso 4: Cargar y visualizar JavaScript en el PDF existente

Supongamos que necesita comprobar o modificar las funciones de JavaScript en un PDF existente. El primer paso es cargar el archivo PDF y acceder a las claves de JavaScript.

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

Estamos cargando lo existente `AddJavascript.pdf` y almacenar las claves JavaScript en una lista. `Keys` La propiedad devuelve los nombres de todas las funciones de JavaScript adjuntas al documento.

## Paso 5: Mostrar funciones de JavaScript

A continuación, podemos iterar a través de las funciones de JavaScript para ver qué hay disponible en el documento.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

Esto imprimirá el nombre de cada función JavaScript y su código correspondiente en la consola. Resulta útil para verificar qué funciones están actualmente en el documento.

## Paso 6: Eliminar JavaScript del PDF

Ahora, digamos que desea eliminar una función específica de JavaScript, como `func1`Aquí te explicamos cómo hacerlo:

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

El `Remove` El método toma el nombre de la función JavaScript como argumento y lo elimina del documento.

## Paso 7: Verificar la eliminación de JavaScript

Después de eliminar el JavaScript, puede volver a imprimir las funciones restantes para confirmarlo. `func1` Se ha eliminado correctamente.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

Esta última parte del código garantiza que todo esté en su lugar y que las funciones de JavaScript se actualicen correctamente.

## Conclusión

¡Felicitaciones! Acaba de aprender a agregar y eliminar JavaScript de un documento PDF con Aspose.PDF para .NET. Esta potente función puede utilizarse para diversas tareas, desde agregar mensajes dinámicos hasta realizar cálculos o validaciones personalizadas. Al manipular JavaScript en un PDF, puede mejorar significativamente la experiencia del usuario.

## Preguntas frecuentes

### ¿Puedo agregar múltiples funciones de JavaScript a un solo PDF?
¡Por supuesto! Puedes agregar tantas funciones de JavaScript como necesites usando `doc.JavaScript` recopilación.

### ¿Qué sucede si intento eliminar una función de JavaScript inexistente?
Si la función no existe, la `Remove` El método no generará un error, pero tampoco eliminará nada.

### ¿Es posible ejecutar JavaScript tan pronto como se abre el PDF?
¡Sí! Puedes configurar JavaScript para que se ejecute al activarse ciertos disparadores, como abrir el documento o hacer clic en un botón.

### ¿Puedo editar el JavaScript después de haberlo agregado al PDF?
Sí, puedes cargar un PDF existente, acceder a su JavaScript, modificar el código y guardar el documento nuevamente.

### ¿Eliminar JavaScript afecta al resto del contenido del PDF?
No, eliminar JavaScript solo afecta al script. El contenido del PDF permanece intacto.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}