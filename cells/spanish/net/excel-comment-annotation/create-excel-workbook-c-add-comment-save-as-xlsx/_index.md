---
category: general
date: 2026-03-18
description: Crear libro de Excel en C# con un comentario y guardar el libro como
  XLSX. Aprende cómo agregar un comentario, generar un comentario en Excel y automatizar
  archivos de Excel.
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: es
og_description: Crear un libro de Excel en C# con un comentario y guardar el libro
  como XLSX. Sigue esta guía paso a paso para añadir un comentario en Excel y generar
  un comentario de Excel programáticamente.
og_title: Crear libro de Excel en C# – Añadir comentario y guardar como XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Crear libro de Excel en C# – Añadir comentario y guardar como XLSX
url: /es/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel C# – Añadir comentario y guardar como XLSX

¿Alguna vez necesitaste **crear un libro de Excel C#** y colocar una nota dentro de una celda, pero no sabías por dónde empezar? No eres el único: los desarrolladores preguntan constantemente *cómo añadir comentario* sin abrir Excel manualmente.  

En este tutorial obtendrás una solución completa, lista para ejecutar, que muestra **cómo añadir comentario en Excel**, **generar comentario en Excel** con un Smart Marker, y **guardar el libro como xlsx** en un flujo único y fluido. Sin referencias colgantes, solo código puro que puedes pegar en Visual Studio y ver cómo funciona.

## Lo que aprenderás

- Inicializar un libro de Excel desde cero usando C#.
- Insertar un Smart Marker que se convierta en un comentario de Excel.
- Alimentar datos JSON para transformar el marcador en un comentario real.
- Persistir el archivo como un libro `.xlsx`.
- Enfoques opcionales para añadir comentarios sin Smart Markers.

Al final tendrás un ejemplo autocontenido que podrás adaptar a facturas, informes de pruebas o cualquier situación donde un comentario de celda añada contexto.

### Requisitos previos

- .NET 6 (o .NET Framework 4.7+).  
- Paquete NuGet **Aspose.Cells for .NET** – la biblioteca que potencia la función Smart Marker.  
- Un entorno básico de desarrollo en C# (Visual Studio, VS Code, Rider…).

> **Consejo profesional:** Si tienes un presupuesto limitado, Aspose ofrece una prueba gratuita que es totalmente funcional para desarrollo y pruebas.

---

## Paso 1: Crear libro de Excel C# – Configuración del proyecto

Primero, creemos una nueva aplicación de consola y añadamos el paquete Aspose.Cells.

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

Ahora abre `Program.cs`. Lo primero que hacemos es **crear un nuevo libro**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

¿Por qué comenzar con un libro completamente nuevo? Garantiza una hoja limpia, elimina formatos ocultos y te permite controlar todo desde cero, ideal para la generación automática de informes.

---

## Paso 2: Cómo añadir comentario – Usando un Smart Marker

Los Smart Markers son marcadores de posición que Aspose reemplaza con datos en tiempo de ejecución. Al incrustar un marcador que sigue el patrón **`${Comment:UserComment}`**, indicamos al motor que convierta el marcador en un comentario real.

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

¿Notas el prefijo `Comment:`? Esa es la señal para que el procesador trate el valor como un comentario y no como texto plano. Si te preguntas *“¿funciona esto con otros tipos de celda?”*—sí, puedes aplicar el mismo marcador a cualquier celda, incluso a rangos combinados.

---

## Paso 3: Preparar los datos JSON – Lo que dirá el comentario

El siguiente elemento es la fuente de datos. Aquí usamos una cadena JSON sencilla, pero también podrías proporcionar un DataTable, una List o incluso un objeto personalizado.

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

Si lo deseas, reemplaza `"Reviewed by QA"` por cualquier valor dinámico—por ejemplo una marca de tiempo, un nombre de usuario o un enlace a un gestor de incidencias. El nombre de la clave (`UserComment`) debe coincidir con el identificador del marcador.

---

## Paso 4: Generar comentario en Excel – Procesando el Smart Marker

Ahora entregamos el JSON al procesador de Smart Markers. Este es el momento en que **generar comentario en Excel** ocurre realmente.

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

Detrás de escena, Aspose analiza el JSON, encuentra el campo `UserComment` y lo inserta como un comentario adjunto a la celda **B2**. El valor visible de la celda sigue siendo el texto del marcador original, pero Excel mostrará el comentario al pasar el cursor sobre ella.

---

## Paso 5: Guardar el libro como XLSX – Persistiendo el resultado

Finalmente, escribimos el libro en disco. Esto satisface el requisito de **guardar libro como xlsx**.

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Abre `output.xlsx` en Excel, pasa el cursor sobre la celda **B2** y verás aparecer el comentario *“Reviewed by QA”*. Eso es todo—sin pasos manuales, sin interop COM, solo C# puro.

---

## Alternativa: Cómo añadir comentario sin Smart Markers

Si prefieres un enfoque más directo, puedes crear tú mismo un objeto de comentario:

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

Este método es útil cuando el texto del comentario ya se conoce en tiempo de compilación, o cuando necesitas establecer propiedades adicionales como autor, ancho o alto. Sin embargo, **generar comentario en Excel** mediante Smart Markers destaca cuando tienes un escenario impulsado por datos con muchas filas y columnas.

---

## Consejos profesionales y errores comunes

| Situación | Qué observar | Solución recomendada |
|-----------|--------------|----------------------|
| Conjuntos de datos grandes (10 k+ filas) | El procesamiento de Smart Marker puede consumir mucha memoria | Usa la sobrecarga `SmartMarkerProcessor.Process` que transmite datos, o divide el libro en fragmentos |
| Necesitas un nombre de autor personalizado | El autor predeterminado está vacío | `comment.Author = "MyApp";` después de crear el comentario |
| Quieres que el comentario sea visible por defecto | Excel oculta los comentarios hasta pasar el cursor | Establece `comment.Visible = true;` |
| Trabajas con versiones antiguas de Excel | `.xlsx` puede no ser compatible | Guarda como `SaveFormat.Xls` en su lugar, pero ten en cuenta que algunas funciones de comentario difieren |

---

## Resultado esperado

- **Archivo de libro:** `output.xlsx` ubicado en la carpeta *bin* del proyecto.  
- **Celda B2:** Muestra el texto del marcador `${Comment:UserComment}` (puedes ocultarlo cambiando el color de fuente a blanco).  
- **Comentario adjunto a B2:** Muestra “Reviewed by QA” al pasar el cursor.

![Crear libro de Excel C# ejemplo mostrando comentario en la celda B2](https://example.com/placeholder-image.png "Crear libro de Excel C# ejemplo mostrando comentario en la celda B2")

*Texto alternativo de la imagen:* **Crear libro de Excel C# ejemplo mostrando comentario en la celda B2**

---

## Recapitulación – Lo que logramos

**Creamos un libro de Excel C#**, insertamos un **Smart Marker** que se convirtió en un **comentario de Excel**, alimentamos JSON para **generar comentario en Excel**, y finalmente **guardamos el libro como xlsx**. Todo el flujo está encapsulado en unas pocas docenas de líneas de código C# limpio y autocontenido.

---

## ¿Qué sigue? Extender la solución

- **Generación masiva de comentarios:** Recorrer un DataTable y aplicar un Smart Marker a cada fila para añadir notas específicas por fila.  
- **Estilizar comentarios:** Ajustar tamaño de fuente, color o incluso añadir texto enriquecido usando la colección `Comment.RichText`.  
- **Exportar a PDF:** Usa `workbook.Save("output.pdf", SaveFormat.Pdf);` para compartir informes con los comentarios intactos.  

Si tienes curiosidad sobre **añadir comentario en Excel** programáticamente en otros contextos—como usando OpenXML SDK o EPPlus—esas bibliotecas también soportan la creación de comentarios, aunque su API difiere.

---

### Reflexiones finales

Añadir un comentario a un archivo de Excel desde C# no tiene por qué ser una tarea engorrosa. Al aprovechar el motor Smart Marker de Aspose.Cells obtienes una forma concisa y basada en datos para **añadir comentario en Excel**, **generar comentario en Excel** y **guardar el libro como xlsx** con un mínimo de código repetitivo.  

Pruébalo, modifica el JSON y observa lo rápido que puedes transformar datos crudos en una hoja de cálculo pulida y rica en comentarios. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}