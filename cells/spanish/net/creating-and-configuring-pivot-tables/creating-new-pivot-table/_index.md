---
title: Crear una nueva tabla dinámica mediante programación en .NET
linktitle: Crear una nueva tabla dinámica mediante programación en .NET
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a crear una tabla dinámica mediante programación en .NET usando Aspose.Cells con nuestra guía paso a paso. Analice sus datos de manera eficiente.
weight: 13
url: /es/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear una nueva tabla dinámica mediante programación en .NET

## Introducción
Crear una tabla dinámica puede parecer una tarea intimidante, especialmente cuando se hace de forma programática. ¡Pero no temas! Con Aspose.Cells para .NET, crear una tabla dinámica no solo es sencillo, sino que también es muy eficaz para el análisis de datos. En este tutorial, te guiaremos paso a paso sobre cómo crear una nueva tabla dinámica en una aplicación .NET. Ya sea que estés agregando datos de ventas, deportes o cualquier otra métrica empresarial, esta guía te ayudará a poner en funcionamiento tus tablas dinámicas en poco tiempo.

## Prerrequisitos
Antes de empezar, asegurémonos de que tienes todo listo. Esto es lo que tienes que hacer:

1. Instalar .NET Framework: Asegúrate de tener instalado .NET Framework en tu equipo. Aspose.Cells admite varias versiones, pero es mejor usar la más reciente.
2.  Biblioteca Aspose.Cells: Necesita tener la biblioteca Aspose.Cells. Puede[Descárgalo aquí](https://releases.aspose.com/cells/net/) conseguir uno[licencia temporal](https://purchase.aspose.com/temporary-license/) para evaluación.
3. Configuración de IDE: tenga listo un IDE compatible con C#, como Visual Studio, donde pueda comenzar un nuevo proyecto.
4. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a seguir el curso sin atascarse demasiado.

¿Está todo listo? ¡Genial! Pasemos a importar los paquetes necesarios.

## Importar paquetes
Lo primero es lo primero: debes importar los espacios de nombres necesarios en tu proyecto de C#. Abre tu archivo de C# y agrega las siguientes directivas using:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Estos espacios de nombres le brindan acceso a las funcionalidades de libro de trabajo, hoja de trabajo y tabla dinámica que usaremos en este tutorial.

## Paso 1: Crear un objeto de libro de trabajo
Crear un libro de trabajo es el comienzo de su recorrido. Comencemos por crear una instancia de un nuevo libro de trabajo y acceder a la primera hoja de trabajo.

```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Creación de una instancia de un objeto Workbook
Workbook workbook = new Workbook();

// Obtención de la referencia de la hoja de trabajo recién agregada
Worksheet sheet = workbook.Worksheets[0];
```

 En este paso, creamos un`Workbook`instancia que representa nuestro archivo Excel y toma la primera hoja de trabajo, que será nuestro campo de juego para la tabla dinámica.

## Paso 2: Insertar datos en las celdas
A continuación, vamos a completar nuestra hoja de cálculo con algunos datos de muestra. Vamos a ingresar filas para diferentes deportes, trimestres y cifras de ventas para darle a nuestra tabla dinámica algo para resumir.

```csharp
Cells cells = sheet.Cells;

// Establecer el valor de las celdas
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Rellenar celda de datos = celdas["A2"];
cell.PutValue("Golf");
// ... Más entradas de datos
```

Aquí, definimos los encabezados de las columnas e insertamos valores debajo de cada encabezado. Estos datos actuarán como fuente para nuestra tabla dinámica, así que asegúrese de que estén organizados. Siga este bloque y creará un conjunto de datos completo.

## Paso 3: Agregar una tabla dinámica
Con los datos listos, es momento de crear la tabla dinámica. Usaremos la colección de tablas dinámicas de la hoja de cálculo para agregar nuestra nueva tabla dinámica.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Cómo agregar una tabla dinámica a la hoja de cálculo
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

En este fragmento, agregamos una tabla dinámica a la hoja de cálculo que hace referencia a nuestro rango de datos (en este caso, las celdas A1 a C8). Colocamos la tabla dinámica a partir de la celda E3 y la llamamos "PivotTable2". Bastante simple, ¿verdad?

## Paso 4: Personalizar la tabla dinámica
Ahora que tenemos nuestra tabla dinámica, personalicémosla para mostrar resúmenes significativos. Podemos controlar lo que aparece en las filas, columnas y áreas de datos de la tabla dinámica.

```csharp
// Acceder a la instancia de la tabla dinámica recién agregada
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// No se muestran los totales generales de las filas.
pivotTable.RowGrand = false;

// Arrastrando el primer campo al área de fila.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Arrastrando el segundo campo al área de la columna.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Arrastrando el tercer campo al área de datos.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

En este paso, le indicamos a la tabla dinámica que oculte los totales generales de las filas y, luego, especificamos qué campos se incluyen en las áreas de filas, columnas y datos. Los nombres de los deportes llenarán las filas, los trimestres llenarán las columnas y las cifras de ventas proporcionarán los resúmenes.

## Paso 5: Guardar el libro de trabajo
Por último, queremos guardar nuestro libro de trabajo recién creado para ver los frutos de nuestro trabajo.

```csharp
// Guardando el archivo Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Simplemente proporcione una ruta adecuada y tendrá la salida de su tabla dinámica guardada en un archivo Excel que puede abrir y revisar.

## Conclusión
La creación de tablas dinámicas mediante programación con Aspose.Cells para .NET puede ahorrarle mucho tiempo, especialmente cuando trabaja con grandes conjuntos de datos. Aprendió a configurar su proyecto, importar los paquetes necesarios, completar datos y crear una tabla dinámica personalizable desde cero. Por lo tanto, la próxima vez que se sienta abrumado por los números, recuerde este tutorial y deje que Aspose.Cells haga el trabajo pesado por usted.

## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca .NET para crear y administrar hojas de cálculo de Excel mediante programación.

### ¿Existe una prueba gratuita de Aspose.Cells?
 Sí, puedes obtener una prueba gratuita[aquí](https://releases.aspose.com/).

### ¿Puedo personalizar la apariencia de la tabla dinámica?
¡Por supuesto! Puedes personalizar el formato, el diseño e incluso los estilos de la tabla dinámica según tus necesidades.

### ¿Dónde puedo encontrar más ejemplos y documentación sobre Aspose.Cells?
 Puedes comprobarlo[documentación](https://reference.aspose.com/cells/net/) para guías completas y ejemplos.

### ¿Cómo puedo obtener soporte para Aspose.Cells?
 Puede obtener ayuda a través de[Foro de Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
