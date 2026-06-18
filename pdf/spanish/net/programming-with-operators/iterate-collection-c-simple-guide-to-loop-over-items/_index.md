---
category: general
date: 2026-04-25
description: Itera una colección en C# rápidamente con un ejemplo claro de bucle foreach.
  Aprende cómo obtener los nombres de los objetos y mostrar una lista de cadenas en
  solo unos pocos pasos.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: es
og_description: Iterar colección C# usando un bucle foreach como ejemplo. Descubre
  cómo obtener nombres de objetos y mostrar una lista de cadenas de manera eficiente.
og_title: Iterar colección C# – Bucle paso a paso sobre los elementos
tags:
- C#
- collections
- loops
title: Iterar colección C# – Guía simple para recorrer elementos
url: /es/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recorrer colección C# – Cómo iterar elementos con un ejemplo de bucle foreach

¿Alguna vez necesitaste **iterar colección C#** pero no estabas seguro de qué constructo te brinda el código más limpio? No estás solo. En muchos proyectos terminamos escribiendo bucles `for` verbosos solo para imprimir unas cuantas cadenas, perdiendo tiempo y legibilidad. ¿La buena noticia? Un solo bucle `foreach` puede extraer cada nombre de un objeto y **mostrar lista de cadenas** en segundos.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra cómo **obtener nombres de objetos**, iterar sobre los elementos y mostrarlos en la consola. Al final tendrás un fragmento autónomo que puedes insertar en cualquier aplicación de consola .NET 6+, además de varios consejos para casos límite y rendimiento.

> **Consejo profesional:** Si trabajas con colecciones grandes, considera usar `Parallel.ForEach`; pero ese es un tema para otro día.

---

## Lo que aprenderás

- Cómo obtener una colección de nombres de un objeto (`GetSignatureNames` en nuestro ejemplo)
- La sintaxis y matices de un **ejemplo de bucle foreach** en C#
- Formas de **mostrar lista de cadenas** en la consola, incluyendo trucos de formato
- Trampas comunes al iterar sobre elementos (colecciones nulas, resultados vacíos)
- Un programa completo listo para copiar y pegar que puedes ejecutar al instante

No se requieren bibliotecas externas; solo la biblioteca de clases base que viene con .NET. Si tienes el SDK de .NET instalado, ya estás listo.

![Diagrama de iterar colección C# que muestra una lista fluyendo a un bucle foreach y luego a la consola](/images/iterate-collection-csharp.png "diagrama de iterar colección c#")

---

## Paso 1: Configurar el objeto de ejemplo

Primero lo primero: necesitamos un objeto que pueda devolver una colección de nombres. Imagina que tienes una clase `Signature` que contiene varias firmas; cada firma tiene una propiedad `Name`. El método `GetSignatureNames` simplemente extrae esos nombres a un `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Por qué es importante:** Al devolver `IEnumerable<string>` mantenemos el método flexible—los llamadores pueden enumerar, consultar o convertir el resultado sin copiar la lista subyacente. También facilita **iterar sobre elementos** más adelante.

---

## Paso 2: Escribir el bucle foreach para mostrar la lista de cadenas

Ahora que tenemos una fuente de nombres, vamos a **iterar colección C#**. El constructo `foreach` extrae automáticamente cada elemento del enumerable, por lo que no necesitamos gestionar una variable de índice.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Explicación del código:**

1. **Instanciar** `Signature` – ahora tienes un objeto que conoce sus propios nombres.
2. **Recuperar** la colección mediante `GetSignatureNames()` – este es el paso de **obtener nombres de objetos**.
3. **Ejemplo de bucle foreach** – `foreach (var name in signatureNames)` itera automáticamente sobre cada cadena.
4. **Mostrar** cada `name` con `Console.WriteLine` – la forma clásica de **mostrar lista de cadenas** en una aplicación de consola.

Como `signatureNames` implementa `IEnumerable<string>`, el bucle `foreach` funciona de inmediato, manejando el enumerador internamente. No es necesario preocuparse por errores de desbordamiento o comprobaciones manuales de límites.

---

## Paso 3: Ejecutar el programa y verificar la salida

Compila y ejecuta el programa (p. ej., `dotnet run` desde la carpeta del proyecto). Deberías ver:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Si no se imprime nada, verifica que `GetSignatureNames` no esté devolviendo `null`. Una rápida protección defensiva puede ahorrarte dolores de cabeza:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Ahora el bucle manejará elegantemente una colección ausente y simplemente no mostrará nada en lugar de lanzar una `NullReferenceException`.

---

## Paso 4: Variaciones comunes y casos límite

### 4.1 Iterar sobre una lista de objetos complejos

A menudo no trabajarás con cadenas simples sino con objetos que contienen múltiples propiedades. En ese caso aún puedes **iterar sobre elementos** y decidir qué mostrar:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Aquí usamos interpolación de cadenas para combinar campos—todavía es un bucle `foreach`, solo que con una salida más rica.

### 4.2 Salida temprana con `break`

Si solo necesitas el primer nombre que coincida, rompe el bucle:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Enumeración paralela (Avanzado)

Cuando la colección es enorme y cada iteración es intensiva en CPU, `Parallel.ForEach` puede acelerar las cosas:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Recuerda, `Console.WriteLine` es seguro para subprocesos, pero el orden de salida será no determinista.

---

## Paso 5: Consejos para bucles limpios y mantenibles

- **Prefiere `foreach` sobre `for`** cuando no necesitas un índice; reduce errores de desbordamiento.
- **Usa `IEnumerable<T>`** en firmas de método para mantener las API flexibles.
- **Protege contra colecciones nulas** con el operador de fusión nula (`??`).
- **Mantén el cuerpo del bucle pequeño**—si te encuentras escribiendo muchas líneas, extrae un método.
- **Evita modificar la colección** mientras iteras; lanza una `InvalidOperationException`.

---

## Conclusión

Acabamos de demostrar cómo **iterar colección C#** usando un **ejemplo de bucle foreach** limpio, obtener **nombres de objetos** y **mostrar lista de cadenas** en la consola. El programa completo—definición del objeto, recuperación e iteración—se ejecuta tal cual, brindándote una base sólida para cualquier escenario donde necesites iterar sobre elementos.

A partir de aquí podrías explorar:

- Filtrado con LINQ antes de iterar (`signatureNames.Where(n => n.Contains("a"))`)
- Escribir la salida a un archivo en lugar de la consola
- Usar `IAsyncEnumerable<T>` para flujos asíncronos

Pruébalos y verás lo versátil que es realmente el constructo `foreach`. ¿Tienes preguntas sobre casos límite o rendimiento? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}