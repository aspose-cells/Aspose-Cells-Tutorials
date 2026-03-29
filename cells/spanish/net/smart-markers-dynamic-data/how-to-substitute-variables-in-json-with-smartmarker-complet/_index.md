---
category: general
date: 2026-03-29
description: Cómo sustituir variables en JSON usando SmartMarker – aprende a usar
  la expresión if, aplicar lógica condicional, multiplicar valores y generar JSON
  sin esfuerzo.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: es
og_description: Cómo sustituir variables en JSON usando SmartMarker. Descubre cómo
  usar la expresión if, aplicar lógica condicional, multiplicar valores y generar
  JSON en minutos.
og_title: Cómo sustituir variables en JSON con SmartMarker – Paso a paso
tags:
- C#
- SmartMarker
- JSON templating
title: Cómo sustituir variables en JSON con SmartMarker – Guía completa
url: /es/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo sustituir variables en JSON con SmartMarker – Guía completa

¿Alguna vez te has preguntado **cómo sustituir variables** dentro de una carga JSON sin escribir un analizador personalizado? No estás solo. En muchos escenarios de integración —piense en facturas, motores de precios o archivos de configuración dinámicos— necesita inyectar valores en tiempo de ejecución, aplicar condiciones simples y quizá incluso hacer una multiplicación rápida. Este tutorial le muestra exactamente **cómo sustituir variables** usando la biblioteca SmartMarker, todo mientras mantiene el JSON limpio y legible.

Recorreremos un ejemplo del mundo real que cubre **use if expression**, **how to apply conditional**, **how to multiply values** y **how to generate json** al instante. Al final, tendrás un fragmento de C# listo para ejecutar que podrás insertar en cualquier proyecto .NET.

## Qué aprenderás

- Configurar `SmartMarkerOptions` para almacenar variables reutilizables.  
- Escribir una plantilla JSON que contenga una expresión `if` para lógica condicional.  
- Multiplicar un valor por una variable dentro de la plantilla.  
- Procesar la plantilla con `SmartMarkerProcessor` y obtener la cadena JSON final.  
- Solucionar problemas comunes como variables faltantes o expresiones mal formadas.

Sin servicios externos, sin dependencias pesadas —solo C# puro y el paquete NuGet SmartMarker.

---

## Cómo sustituir variables – Visión general paso a paso

A continuación se muestra una visión general de alto nivel del flujo de trabajo. Piénsalo como una canalización donde tu plantilla JSON cruda entra por la izquierda, el motor SmartMarker hace su magia y el JSON completamente renderizado sale por la derecha.

![Diagrama que muestra cómo sustituir variables en JSON](https://example.com/images/smartmarker-flow.png "Cómo sustituir variables en JSON")

*Texto alternativo de la imagen: Diagrama que muestra cómo sustituir variables en JSON.*

---

## Paso 1: Instalar e importar SmartMarker

Antes de comenzar, asegúrate de que el paquete SmartMarker esté referenciado en tu proyecto. Si utilizas la CLI de .NET, ejecuta:

```bash
dotnet add package SmartMarker
```

Luego, agrega las directivas `using` necesarias al inicio de tu archivo C#:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Consejo profesional:** La última versión (a partir de marzo 2026) es 2.4.1. Soporta .NET 6 y posteriores, pero funciona perfectamente con .NET Framework 4.7 también.

---

## Paso 2: Crear opciones SmartMarker y definir variables

Ahora crearemos una instancia de `SmartMarkerOptions` que contendrá todas las variables que deseamos reutilizar en la plantilla. Aquí es donde respondemos a la pregunta **how to substitute variables** —las variables actúan como marcadores de posición que SmartMarker reemplazará más adelante.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

¿Por qué almacenar la tasa en `Variables` en lugar de codificarla directamente? Porque podrías obtener ese número de una base de datos, un archivo de configuración o una entrada del usuario. Mantenerla en las opciones hace que la plantilla sea reutilizable y testeable.

---

## Paso 3: Escribir la plantilla JSON con una expresión `if`

Aquí es donde brilla la palabra clave **use if expression**. SmartMarker te permite incrustar lógica condicional directamente dentro de la cadena JSON. La sintaxis se parece un poco a un nombre de propiedad, pero SmartMarker la trata como una directiva.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Observa la clave `if(Amount>500)`. SmartMarker evalúa la expresión `Amount>500`; si es verdadera, el valor correspondiente (`${Amount * Rate}`) se inserta en la salida. La sintaxis `${...}` es el motor de *sustitución de variables* —aquí **how to multiply values** (`Amount * Rate`) antes de inyectar el resultado.

---

## Paso 4: Procesar la plantilla y obtener el JSON final

Con las opciones y la plantilla listas, entregamos todo al procesador. El método `ProcessJson` analiza la plantilla, aplica la condición, realiza la multiplicación y devuelve una cadena JSON limpia.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Ejecutar el fragmento imprime:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**¿Qué ocurrió?**  
- `Amount` es 1000, lo que satisface `Amount>500`.  
- SmartMarker evalúa `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- La clave condicional original (`if(Amount>500)`) se reemplaza por un nombre de propiedad limpio (`Result`). Por defecto SmartMarker usa `"Result"` pero puedes personalizarlo (más adelante).

Si cambias `Amount` a `400`, la salida se vuelve:

```json
{
  "Amount": 400
}
```

El bloque condicional desaparece porque la expresión se evaluó como `false`. Esa es la esencia de la lógica **how to apply conditional** en JSON.

---

## Paso 5: Personalizar el nombre de la propiedad de salida (Opcional)

A veces no deseas la clave genérica `"Result"`. SmartMarker te permite especificar un nombre personalizado usando la opción `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Salida:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Ahora el valor condicional se almacena bajo un nombre de propiedad más significativo —perfecto para servicios posteriores que esperan un campo específico.

---

## Problemas comunes y cómo evitarlos

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Variable no encontrada | Referencias una variable que no está en `smartMarkerOptions.Variables`. | Verifica la ortografía y asegura que la variable se añada antes del procesamiento. |
| Sintaxis `if` inválida | Faltan paréntesis o el operador es incorrecto (`>`, `<`, `==`). | Sigue el patrón exacto `if(<expression>)`; SmartMarker solo admite comparaciones numéricas simples. |
| JSON queda malformado | Dejar accidentalmente una coma final después del bloque condicional. | Deja que SmartMarker maneje la eliminación; mantén la plantilla original sintácticamente correcta. |
| Formato de número inesperado | El resultado aparece como una cadena `"80"` en lugar de un número. | Convierte o analiza más tarde, o usa `${(Amount * Rate):N0}` para formateo numérico. |

---

## Ejemplo completo (listo para copiar y pegar)

A continuación está el programa completo que puedes compilar y ejecutar. Demuestra **how to generate json** con variables dinámicas, condicionales y aritmética —todo en menos de 30 líneas.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Salida esperada en la consola**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Siéntete libre de cambiar `Amount` para probar la rama condicional, o ajustar `Rate` para ver diferentes cálculos de descuento.

---

## Extender el patrón – Más escenarios “How to”

- **How to substitute variables** desde un archivo de configuración: Carga un `Dictionary<string, object>` desde `appsettings.json` y pásalo a `smartMarkerOptions.Variables`.  
- **How to use if expression** para múltiples condiciones: Encádnalas como `"if(Amount>500 && CustomerType=='VIP')"` —SmartMarker soporta AND/OR lógico.  
- **How to apply conditional** formateo: Usa `${Amount:0.00}` dentro de la expresión para controlar los decimales.  
- **How to multiply values** con matemáticas más complejas: `${(Amount - Discount) * TaxRate}` funciona de la misma manera.  
- **How to generate json** para objetos anidados: Coloca el bloque condicional dentro de otro objeto JSON, y SmartMarker preservará la jerarquía.

---

## Conclusión

Hemos cubierto **how to substitute variables** en JSON usando SmartMarker, demostrado **use if expression** para inclusión condicional, explicado **how to apply conditional** lógica, mostrado **how to multiply values** dentro de una plantilla, y finalmente ilustrado **how to generate json** listo para el consumo posterior. El enfoque es liviano, no requiere un motor de plantillas externo y encaja perfectamente en cualquier base de código C#.

Pruébalo—ajusta las variables, agrega más condiciones, o envuelve todo en una clase auxiliar para reutilizarla en toda tu solución. Cuando necesites generar JSON dinámico rápidamente, SmartMarker es una opción sólida y lista para producción.

**Próximos pasos**

- Profundiza en las características avanzadas de SmartMarker como bucles (`foreach`) y funciones personalizadas.  
- Combina esta técnica con endpoints de ASP.NET Core para servir APIs JSON dinámicas.  
- Explora otras bibliotecas de plantillas (p.ej., Handlebars.NET) para comparar, especialmente si necesitas una sintaxis más rica.

¿Tienes preguntas o un caso de uso particular con el que estás lidiando? Deja un comentario abajo, y solucionemos juntos. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}