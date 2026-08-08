---
date: '2026-05-28'
description: Aprenda cómo configurar la vista de página única PDF, cambiar las preferencias
  del visor, editar marcadores y configurar la configuración PDF usando Aspose.PDF
  para Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Vista de página única PDF en Java – Cambiar diseño y editar marcadores
url: /es/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Vista de página única PDF en Java – Cambiar diseño y editar marcadores

## Introducción
Cuando los lectores abren un PDF grande, el diseño predeterminado del visor puede desplazarse de forma continua, lo que dificulta enfocarse en una sola página. Al configurar la opción **single page view pdf**, obligas al visor a mostrar una página a la vez, lo cual es ideal para informes, libros electrónicos y catálogos. En este tutorial también aprenderás a editar marcadores PDF existentes, establecer destinos de marcadores al crear un documento y ajustar otras preferencias del visor usando Aspose.PDF para Java. Al final tendrás control total sobre la navegación, la precisión de los marcadores y el diseño en pantalla.

**Qué aprenderás**
- Cómo editar marcadores PDF existentes para que apunten al inicio de una página.  
- Cómo establecer destinos de marcadores al crear un PDF.  
- Cómo cambiar las preferencias del visor, como el diseño de una sola página.  
- Consejos prácticos para cargar un documento PDF en Java y optimizar el rendimiento.

### Respuestas rápidas
- **¿Cuál es la forma principal de habilitar la vista de página única PDF?** Llama a `PdfContentEditor.changeViewerPreference()` con `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **¿Se pueden editar los destinos de los marcadores después de generar un PDF?** Sí – carga el documento, recupera el esquema y asigna un nuevo `ExplicitDestination`.  
- **¿Necesito una licencia para estas funciones?** Una prueba gratuita sirve para evaluación; una licencia completa elimina todas las limitaciones.  
- **¿Qué dependencia Maven se requiere?** `com.aspose:aspose-pdf:25.3` (o posterior).  
- **¿Es compatible con Java 11 y superiores?** Absolutamente – Aspose.PDF soporta Java 8+.

## Qué es “cambiar el diseño de página PDF”
Cambiar el diseño de página PDF controla cómo se muestran las páginas en un visor: una sola página, continuo, vista de dos páginas, etc. Habilitar **single page view pdf** mejora la legibilidad de documentos extensos y asegura que cada página se presente de forma aislada, lo cual es especialmente útil en dispositivos móviles y tabletas.

## Por qué editar marcadores PDF y establecer destinos de marcadores
Los marcadores actúan como una tabla de contenido dinámica. Los destinos precisos permiten a los lectores saltar directamente a la sección deseada, eliminando desplazamientos innecesarios y reduciendo la frustración del usuario. Esto conduce a una experiencia de navegación más fluida y a una mayor satisfacción en manuales técnicos, catálogos de productos y libros digitales.

## Requisitos previos
- **Bibliotecas y dependencias**: Aspose.PDF para Java v25.3 o posterior.  
- **Entorno**: JDK 8 o superior, herramienta de compilación Maven o Gradle.  
- **Conocimientos**: Programación básica en Java y familiaridad con conceptos de PDF.

## Configuración de Aspose.PDF para Java
### Instalación con Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Instalación con Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Adquisición de licencia**: Comienza con una prueba gratuita o solicita una licencia temporal para acceso a todas las funciones. Considera comprar una licencia permanente para uso en producción.

### Inicialización básica
La clase `Document` es el objeto central de Aspose.PDF que representa un archivo PDF en memoria. Después de crear una instancia, todas las operaciones de lectura/escritura fluyen a través de este objeto.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Guía de implementación
### Cómo cambiar el diseño de página PDF en Java
**Descripción general**: Ajusta las preferencias del visor para mostrar las páginas como desees.

#### Inicializando PdfContentEditor
`PdfContentEditor` es una clase de utilidad que permite modificar la configuración del visor sin reescribir todo el documento.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Cambiando preferencias del visor
Para habilitar **single page view pdf**, invoca `changeViewerPreference()` con el valor enum apropiado. Esta llamada actualiza el diccionario interno de preferencias del visor del PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Guardando el documento actualizado
Después de modificar las preferencias, llama a `save()` para escribir los cambios en el disco.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Cómo editar marcadores PDF
**Respuesta**: Para modificar marcadores existentes, carga el PDF con `Document`, recupera su colección de esquema, localiza el `OutlineItem` deseado y asigna un nuevo `ExplicitDestination` que apunte a la página y coordenadas correctas. Después de actualizar cada marcador, guarda el documento para persistir los cambios. Esto garantiza que los usuarios sean dirigidos precisamente a las secciones deseadas sin desplazamiento adicional.

#### Accediendo a los marcadores
La `OutlineItemCollection` representa el árbol jerárquico de marcadores. Recupera esta colección del objeto `Document` para trabajar con entradas individuales.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Estableciendo un nuevo destino
Un `ExplicitDestination` define la página y ubicación exactas a las que debe saltar un marcador. Asignalo a la propiedad `Destination` del elemento del esquema.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Guardando los cambios
Persistir el árbol de marcadores actualizado llamando a `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Cómo establecer el destino del marcador al crear un PDF
**Respuesta**: Al generar un PDF, puedes crear marcadores al vuelo instanciando objetos `OutlineItem`, estableciendo sus títulos y definiendo un `ExplicitDestination` que apunte a una página y modo de vista específicos. Añade cada marcador a la colección de esquema del documento antes de guardarlo, de modo que el archivo resultante contenga un árbol de navegación listo para usar.

#### Creando y configurando el marcador
`OutlineItem` representa una única entrada de marcador en el esquema del PDF. Al crear un PDF desde cero, instancia un nuevo `OutlineItem` y añádelo a la colección de esquema del documento.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definiendo el destino del marcador
Usa `ExplicitDestination.createFitH(page, top)` para posicionar la vista en la parte superior de la página objetivo.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Añadiendo y guardando el PDF
Finalmente, añade el marcador al esquema y guarda el documento.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Aplicaciones prácticas
1. **Libros digitales** – Asegura que cada marcador de capítulo llegue a la parte superior de la página para una experiencia de lectura fluida.  
2. **Manuales técnicos** – La navegación precisa ayuda a los ingenieros a encontrar secciones rápidamente, especialmente en PDFs extensos.  
3. **Catálogos de productos** – El diseño de una sola página hace que la navegación por catálogos en tabletas sea más intuitiva.

## Consideraciones de rendimiento
- **Optimización de recursos**: Aspose.PDF puede procesar PDFs de hasta 2 GB sin cargar todo el archivo en memoria, gracias a su arquitectura de transmisión. Usa `Document.optimizeResources()` para reducir aún más la huella de memoria.  
- **Gestión de memoria en Java**: Cierra explícitamente los streams y permite que el recolector de basura recupere los objetos después del procesamiento para evitar fugas de memoria.

## Problemas comunes y soluciones
- **Los marcadores no se actualizan**: Verifica que estés modificando el índice de esquema correcto (`get_Item(1)` se refiere al primer marcador de nivel superior).  
- **Preferencia del visor no aplicada**: Asegúrate de llamar a `editor.save()` después de cambiar las preferencias; de lo contrario, los cambios permanecen solo en memoria.  
- **Excepciones de licencia**: Una licencia de prueba puede añadir marcas de agua; obtén una licencia completa para producción.

## Preguntas frecuentes
**P: ¿Cuál es la forma más fácil de cargar un documento PDF en Java?**  
R: Usa `new Document("path/to/file.pdf")`; Aspose.PDF detecta automáticamente el formato del archivo.

**P: ¿Puedo cambiar el diseño de página sin usar PdfContentEditor?**  
R: Sí, puedes establecer las preferencias del visor directamente en el objeto `Document` mediante `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**P: ¿Cambiar el diseño del visor afecta la impresión?**  
R: El diseño del visor solo influye en la visualización en pantalla; no altera la salida impresa.

**P: ¿Hay límites en la cantidad de marcadores que puedo crear?**  
R: No hay un límite explícito, pero árboles de esquema extremadamente grandes pueden afectar el rendimiento; mantenlos organizados.

**P: ¿Cómo asegurar que los destinos de los marcadores sean precisos después de añadir o eliminar páginas?**  
R: Recalcula los destinos usando los índices de página actuales después de cualquier cambio estructural.

## Recursos
- **Documentación**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Descarga**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Compra**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Prueba gratuita**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Licencia temporal**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Última actualización:** 2026-05-28  
**Probado con:** Aspose.PDF para Java v25.3  
**Autor:** Aspose

## Tutoriales relacionados

- [Cómo cambiar las preferencias del visor PDF usando Aspose.PDF para Java: Guía completa](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Cómo crear marcadores PDF y gestionar la navegación usando Aspose.PDF para Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [Tutoriales de marcadores PDF y navegación para Aspose.PDF Java](/pdf/java/bookmarks-navigation/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}