---
category: general
date: 2026-02-20
description: Aprende a instalar paquetes NuGet usando PowerShell, ejecuta PowerShell
  como administrador, lista los paquetes instalados y verifica el paquete instalado
  en minutos.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: es
og_description: cómo instalar paquetes NuGet usando PowerShell, ejecutar PowerShell
  como administrador, listar paquetes instalados y verificar el paquete instalado—guía
  completa.
og_title: Cómo instalar paquetes NuGet mediante PowerShell – guía rápida
tags:
- PowerShell
- NuGet
- Package Management
title: cómo instalar paquetes NuGet mediante PowerShell – paso a paso
url: /es/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo instalar paquetes nuget vía PowerShell – paso a paso

¿Alguna vez te has preguntado **cómo instalar nuget** paquetes sin abrir Visual Studio? No estás solo. En muchos pipelines de CI o en máquinas recién instaladas, la ruta más rápida es entrar en PowerShell—preferiblemente *run powershell as admin*—y dejar que el gestor de paquetes haga su trabajo.

En este tutorial recorreremos todo el proceso: abrir la consola adecuada, descargar una versión específica de una biblioteca y, finalmente, confirmar que el paquete realmente se instaló en tu sistema. Al final podrás **list installed packages**, saber **how to verify package** integridad, y sentirte seguro de que el paso **verify installed package** se completó con éxito cada vez.

## Lo que aprenderás

- Cómo iniciar PowerShell con los privilegios correctos.  
- La sintaxis exacta del comando `Install-Package` para NuGet.  
- Formas de **list installed packages** y confirmar los números de versión.  
- Problemas comunes (faltan derechos de administrador, incompatibilidades de versión) y cómo evitarlos.  

No se requiere experiencia previa con NuGet, solo una máquina Windows funcional y un poco de curiosidad.

---

## Cómo instalar paquetes NuGet usando PowerShell

> **Consejo profesional:** Si frecuentemente añades los mismos paquetes, considera agregarlos a un archivo de script y ejecutarlo con `-File`. Te ahorra escribir la misma línea una y otra vez.

### Paso 1: Abrir PowerShell con los permisos necesarios

Lo primero que debes hacer es **run powershell as admin**. Sin derechos elevados, el cmdlet `Install-Package` puede fallar silenciosamente o solicitar una confirmación con la que no deseas lidiar.

1. Haz clic en el botón Inicio.  
2. Escribe **PowerShell**.  
3. Haz clic derecho en *Windows PowerShell* y elige **Run as administrator**.  

Verás un mensaje UAC; haz clic en **Yes**. Ahora tienes una sesión privilegiada lista para la instalación de paquetes.

> *¿Por qué administrador?*  
> NuGet escribe archivos en la carpeta global de paquetes (`C:\Program Files\PackageManagement\NuGet\Packages` por defecto). Esa ubicación está protegida, por lo que solo un proceso elevado puede escribir allí.

### Paso 2: Instalar el paquete NuGet deseado y su versión

Con la consola abierta, el comando principal es sencillo:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` es el contenedor de PowerShell alrededor del cliente de NuGet.  
- `-Version` fija la compilación exacta que necesitas, evitando actualizaciones accidentales.  

Si omites `-Version`, PowerShell obtendrá la última versión estable—a veces está bien, a veces deseas la versión exacta contra la que probaste.

#### ¿Qué ocurre bajo el capó?

PowerShell contacta la fuente de paquetes configurada (por defecto `https://www.nuget.org/api/v2`) y descarga el archivo `.nupkg`. Luego extrae los DLLs en la carpeta global de paquetes y registra el paquete con el proveedor de paquetes local. Todo el proceso suele terminar en unos segundos, a menos que estés en una red lenta.

### Paso 3: Verificar que el paquete se instaló correctamente

Ahora que el paquete está en disco, probablemente te preguntes, **“How do I verify the package?”** La respuesta está en una consulta simple:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Ejecutar esto devuelve algo como:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Ese resultado confirma dos cosas:

1. El paquete **Aspose.PDF** está presente.  
2. Su versión coincide con la que solicitaste, cumpliendo el requisito **verify installed package**.  

Si deseas ver *todos* los paquetes en la máquina, elimina el filtro `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Esta vista de **list installed packages** es útil para auditorías o cuando necesitas limpiar bibliotecas antiguas.

### Paso 4: Opcional – manejo de casos límite

#### a) Paquete no encontrado o incompatibilidad de versión

Si PowerShell responde con *“Package not found”* o *“Version not available”*, verifica la ortografía y el número de versión. NuGet no distingue mayúsculas, pero un espacio extra romperá el comando.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Ejecutar sin derechos de administrador

Si olvidas **run powershell as admin**, el cmdlet lanzará un error de permisos. La solución es simplemente cerrar la ventana y volver a abrirla con derechos elevados—no es necesario reinstalar nada.

#### c) Usar una fuente personalizada

En entornos corporativos podrías tener un feed interno de NuGet:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

El paso de verificación sigue siendo el mismo; solo recuerda incluir `-Source` al instalar.

---

## Tabla de referencia rápida

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| Abrir consola elevada               | *Run PowerShell as Administrator*                           | Needed for global install |
| Instalar una versión específica    | `Install-Package <pkg> -Version <x.y.z>`                    | Guarantees reproducible builds |
| Listar un paquete único             | `Get-Package -Name <pkg>`                                    | Confirms **how to verify package** |
| Listar todos los paquetes NuGet     | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Useful for **list installed packages** |
| Buscar versiones disponibles         | `Find-Package <pkg> -AllVersions`                           | Helps when version is unknown |

---

## Conclusión

Hemos cubierto **how to install nuget** paquetes usando PowerShell de principio a fin—abriendo la consola **run powershell as admin**, descargando una versión específica y finalmente **list installed packages** para **verify installed package**. Con estos comandos en tu caja de herramientas puedes automatizar la gestión de bibliotecas en cualquier máquina Windows, ya sea que estés scriptando un pipeline CI o simplemente arreglando un DLL faltante en tu equipo de desarrollo.

¿Próximos pasos? Intenta agregar varios paquetes a un solo script, explora el parámetro `-Scope` para instalar localmente en un proyecto, o combina estos comandos con `Invoke-Expression` para crear un instalador ligero para tu equipo. Y si encuentras un obstáculo, recuerda el paso **how to verify package**—ver la versión en `Get-Package` suele ser la forma más rápida de detectar un problema.

¡Feliz PowerShell! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}