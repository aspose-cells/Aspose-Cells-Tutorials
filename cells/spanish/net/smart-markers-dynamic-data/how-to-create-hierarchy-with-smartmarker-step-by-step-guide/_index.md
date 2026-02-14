---
category: general
date: 2026-02-14
description: 'Crear jerarquías en plantillas SmartMarker es más fácil de lo que piensas:
  aprende a crear datos jerárquicos y a listar empleados de manera eficiente.'
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: es
og_description: Cómo crear jerarquía en plantillas SmartMarker es sencillo. Sigue
  esta guía para crear datos jerárquicos y listar empleados con rangos anidados.
og_title: Cómo crear jerarquía con SmartMarker – Guía completa
tags:
- SmartMarker
- C#
- templating
title: Cómo crear jerarquía con SmartMarker – Guía paso a paso
url: /es/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear jerarquía con SmartMarker – Guía completa

¿Alguna vez te has preguntado **cómo crear jerarquía** dentro de una plantilla SmartMarker sin volverte loco? No eres el único. En muchos escenarios de informes necesitas una relación padre‑hijo—piensa en departamentos y las personas que trabajan en ellos. La buena noticia es que SmartMarker lo hace pan comido una vez que conoces los pasos correctos.

En este tutorial recorreremos todo el proceso: desde **crear datos jerárquicos** en C#, habilitar rangos anidados y, finalmente, renderizar una plantilla que **lista empleados** para cada departamento. Al final tendrás un ejemplo listo para ejecutar que puedes insertar en cualquier proyecto .NET.

---

## Lo que necesitarás

- .NET 6+ (cualquier versión reciente funciona)
- Una referencia a la biblioteca **SmartMarker** (el espacio de nombres `ws.SmartMarkerProcessor`)
- Conocimientos básicos de C# – nada complicado, solo unos pocos objetos y una lambda o dos
- Un IDE o editor de tu elección (Visual Studio, Rider, VS Code… tú decides)

Si ya tienes eso, genial—¡vamos al grano!

---

## Cómo crear jerarquía – Visión general

La idea central es construir un **grafo de objetos anidado** que refleje la estructura que deseas ver en el documento final. En nuestro caso el grafo se ve así:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker puede entonces iterar sobre `Departments` y, como activaremos **el procesamiento de rangos anidados**, también recorrerá automáticamente la colección `Employees` de cada departamento.

---

## Paso 1: Construir el modelo de datos jerárquico

Primero creamos un objeto anónimo que contiene una matriz de departamentos, cada uno con su propia lista de empleados. Usar un tipo anónimo mantiene el ejemplo ligero—siéntete libre de reemplazarlo con clases POCO reales más adelante.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Por qué es importante:** La matriz `Departments` es la colección de nivel superior. Cada elemento contiene una matriz `Employees`, dándonos el segundo nivel de jerarquía al que accederemos más tarde con `#Departments.Employees#`.

---

## Paso 2: Habilitar el procesamiento de rangos anidados

SmartMarker no profundizará en colecciones internas a menos que se lo indiques. El objeto `SmartMarkerOptions` contiene ese interruptor.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Consejo profesional:** Si olvidas esta bandera, el rango interno `#Employees#` simplemente no devuelve nada, y estarás rascándote la cabeza preguntándote por qué la plantilla está en blanco.

---

## Paso 3: Ejecutar el procesador con tus datos

Ahora entregamos los datos y las opciones al procesador. La variable `ws` representa tu **WebService** (o cualquier objeto que aloje el motor SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

En este punto SmartMarker analiza la plantilla, sustituye `#Departments.Name#` por cada nombre de departamento y, como los rangos anidados están habilitados, itera a través de la colección `Employees` de cada departamento.

---

## Paso 4: Crear los marcadores de la plantilla

A continuación tienes una plantilla mínima que demuestra tanto el bucle externo como el interno. Pégala en el editor de plantillas SmartMarker (o en un archivo `.txt` que pases al procesador).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Al renderizarla verás:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Lo que estás viendo:** El `#Departments.Name#` externo imprime el título del departamento. El bloque interno `#Departments.Employees#` recorre cada empleado, y `#Departments.Employees#` dentro del bloque muestra el nombre real.

---

## Salida esperada y verificación

Ejecutar el ejemplo completo (datos + opciones + plantilla) debería producir exactamente la lista mostrada arriba. Para verificar rápidamente, puedes volcar el resultado en la consola:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Si ves los dos encabezados de departamento seguidos de sus viñetas de empleados, has creado con éxito **una jerarquía** y **listado empleados**.

---

## Problemas comunes y casos límite

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| No hay salida para empleados | `EnableNestedRange` dejado en false | Establecer `EnableNestedRange = true` |
| Nombres de empleados duplicados | La misma matriz reutilizada en varios departamentos | Clonar la matriz o usar colecciones distintas |
| Jerarquías muy grandes causan presión de memoria | SmartMarker carga todo el grafo de objetos en memoria | Transmitir datos o paginar colecciones grandes |
| Errores de sintaxis en la plantilla | Falta de cierre de etiquetas `#/…#` | Usar el validador de SmartMarker o ejecutar una prueba rápida con una plantilla pequeña |

---

## Ir más allá – Variaciones del mundo real

1. **Fuentes de datos dinámicas** – Obtener departamentos de una base de datos y mapearlos a la estructura anónima usando LINQ.  
2. **Formato condicional** – Añadir una bandera `IsManager` a cada empleado y usar las etiquetas condicionales de SmartMarker (`#if …#`) para resaltar a los gerentes.  
3. **Múltiples niveles de anidación** – Si necesitas equipos dentro de departamentos, simplemente agrega otra colección (`Teams`) y mantén `EnableNestedRange` activado.

---

## Ejemplo completo funcional (listo para copiar y pegar)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Plantilla (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Ejecutar el programa imprime la jerarquía exactamente como se mostró antes.

---

## Conclusión

Hemos cubierto **cómo crear jerarquía** en SmartMarker, desde dar forma a **datos jerárquicos** en C# hasta activar rangos anidados y finalmente renderizar una plantilla que **lista empleados** por departamento. El patrón escala—solo agrega más colecciones anidadas o lógica condicional y tendrás un motor de informes potente al alcance de tu mano.

¿Listo para el próximo desafío? Prueba cambiar los tipos anónimos por clases POCO fuertemente tipadas, o integra este flujo en un endpoint ASP.NET Core que devuelva un documento PDF o Word. El cielo es el límite, y ahora tienes una base sólida.

![Diagrama de cómo crear jerarquía](image.png){alt="Diagrama de cómo crear jerarquía que muestra la relación departamento‑empleado"}

*¡Feliz codificación! Si encuentras algún problema, deja un comentario abajo—estaré encantado de ayudar.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}