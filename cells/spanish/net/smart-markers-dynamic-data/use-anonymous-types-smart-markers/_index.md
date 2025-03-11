---
title: Utilice tipos anónimos con marcadores inteligentes Aspose.Cells
linktitle: Utilice tipos anónimos con marcadores inteligentes Aspose.Cells
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a utilizar tipos anónimos con marcadores inteligentes en Aspose.Cells para la generación dinámica de informes de Excel en .NET. Siga nuestra sencilla guía.
weight: 17
url: /es/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utilice tipos anónimos con marcadores inteligentes Aspose.Cells

## Introducción
Cuando se trata de generar informes dinámicos de Excel en aplicaciones .NET, Aspose.Cells se destaca como una herramienta poderosa. Una de sus mejores características es la capacidad de trabajar con marcadores inteligentes y tipos anónimos. Si este concepto es nuevo para usted, ¡no se preocupe! Esta guía desglosará todo lo que necesita saber, desde los requisitos previos hasta ejemplos prácticos, todo de manera interesante y fácil de seguir.
## Prerrequisitos
Antes de sumergirnos en el código, asegurémonos de que tienes todo lo que necesitas para ejecutar sin problemas los ejemplos de este tutorial.
### 1. Entorno .NET
Asegúrate de tener un entorno .NET funcional configurado en tu equipo local. Puedes usar Visual Studio o cualquier otro IDE de tu elección.
### 2. Biblioteca Aspose.Cells
 Necesitarás la biblioteca Aspose.Cells. Si aún no la has descargado, puedes encontrarla fácilmente.[aquí](https://releases.aspose.com/cells/net/) También puedes probarlo con una versión de prueba gratuita disponible en[Este enlace](https://releases.aspose.com/).
### 3. Conocimientos básicos de C#
Un conocimiento básico de la programación en C# te ayudará a navegar por el tutorial con mayor facilidad. Si te resultan familiares términos como clases, objetos y propiedades, ¡estás listo para comenzar!
## Importar paquetes
Para utilizar la biblioteca Aspose.Cells en su proyecto, debe importar los espacios de nombres relacionados. Agregue las siguientes directivas using en la parte superior de su archivo C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Estos espacios de nombres le darán acceso a todas las clases y métodos necesarios que se analizarán más adelante.
Ahora, ¡entremos en el meollo del tutorial! Verás cómo crear un archivo de Excel con marcadores inteligentes usando una clase personalizada. No te preocupes; ¡lo dividiremos todo en pasos manejables!
## Paso 1: Crear una clase personalizada
En primer lugar, necesitamos una clase sencilla que represente los datos que queremos agregar a nuestro archivo de Excel. Esta clase contendrá información sobre una persona.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
 Aquí, estamos definiendo una clase llamada`Person` con dos propiedades,`Name` y`Age`El constructor inicializa estas propiedades. 
## Paso 2: Configurar el Diseñador de libros de trabajo
 A continuación, vamos a crear una instancia de`WorkbookDesigner`clase que usaremos para diseñar nuestro archivo Excel con marcadores inteligentes.
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Cree una instancia del objeto de diseño de libros de trabajo.
WorkbookDesigner report = new WorkbookDesigner();
```
 Reemplazar`"Your Document Directory"` con la ruta de archivo actual donde desea guardar el archivo de Excel.`WorkbookDesigner` La clase es el corazón de esta operación, donde define su plantilla.
## Paso 3: Agregar marcadores a las celdas
Ahora, debemos agregar marcadores inteligentes a la hoja de cálculo. Estos marcadores serán marcadores de posición para los datos que ingresaremos más adelante.
```csharp
// Obtenga la primera hoja de trabajo del libro de trabajo.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Introduzca algunos marcadores en las celdas.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Designamos la primera hoja de cálculo y establecemos valores para las celdas de encabezado. Los marcadores inteligentes tienen como prefijo`&=` que le dice a Aspose que estos son marcadores de posición para que se inserten datos más adelante.
## Paso 4: Crea una lista de personas
 Ahora vamos a crear una lista de personas que utilizan nuestro`Person` clase que usaremos para rellenar los marcadores inteligentes.
```csharp
// Cree una instancia de la colección de listas en función de la clase personalizada.
IList<Person> list = new List<Person>();
// Proporcione valores para los marcadores utilizando el objeto de clase personalizado.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Creamos una lista y agregamos instancias de`Person`Esta lista nos sirve como fuente de datos al completar la plantilla de Excel.
## Paso 5: Establecer la fuente de datos y los marcadores de proceso
 Una vez que tengamos nuestra lista lista, debemos configurarla como fuente de datos para nuestra`WorkbookDesigner` instancia y luego procesar los marcadores.
```csharp
// Establecer la fuente de datos.
report.SetDataSource("MyProduct", list);
// Procesar los marcadores.
report.Process(false);
```
 El`SetDataSource` El método vincula nuestra lista previamente definida a los marcadores.`Process` El método reemplaza los marcadores inteligentes en el libro de trabajo con valores reales de nuestros objetos.
## Paso 6: Guarde el archivo Excel
Finalmente, guardaremos el libro de trabajo modificado en nuestro directorio designado.
```csharp
// Guarde el archivo Excel.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Esta línea guarda el libro de trabajo en la ruta de archivo especificada. Puede abrir este archivo con Excel para ver los datos insertados.
## Conclusión
¡Y ya está! Has creado con éxito un archivo de Excel usando marcadores inteligentes en Aspose.Cells con tu propia clase personalizada. Este método no solo hace que la gestión de datos sea más dinámica, sino que también mantiene tu código limpio y organizado.
Entonces, ya sea que esté generando informes para análisis, seguimiento de información o cualquier otra tarea relacionada con datos, los marcadores inteligentes son su aliado para hacer que los informes de Excel sean más manejables y flexibles.
## Preguntas frecuentes
### ¿Qué son los marcadores inteligentes en Aspose.Cells?
Los marcadores inteligentes son marcadores de posición especiales en su documento de Excel que le permiten insertar datos dinámicamente durante el tiempo de ejecución.
### ¿Puedo utilizar tipos anónimos para marcadores inteligentes?
¡Sí! Los marcadores inteligentes se pueden utilizar con cualquier tipo de objeto, incluidos los tipos anónimos, siempre que coincidan con la estructura de datos esperada.
### ¿Aspose.Cells es de uso gratuito?
Aspose.Cells es un producto pago, pero puedes comenzar con una prueba gratuita para explorar sus funciones.
### ¿Qué formatos de archivos admite Aspose.Cells?
Admite una amplia gama de formatos de archivos, incluidos XLS, XLSX, CSV y más.
### ¿Dónde puedo encontrar más información sobre Aspose.Cells?
 Para obtener más detalles, consulte la[documentación](https://reference.aspose.com/cells/net/) o visite el[foro de soporte](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
