---
"description": "Automatice el formato de números en Excel con Aspose.Cells para .NET. Aprenda a aplicar formatos de fecha, porcentaje y moneda mediante programación."
"linktitle": "Uso de formatos numéricos integrados en Excel mediante programación"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Uso de formatos numéricos integrados en Excel mediante programación"
"url": "/es/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Uso de formatos numéricos integrados en Excel mediante programación

## Introducción
En este tutorial, te explicaremos cómo usar los formatos numéricos integrados en Excel con Aspose.Cells para .NET. Abarcaremos todo, desde la configuración de tu entorno hasta la aplicación de diferentes formatos, como fechas, porcentajes y monedas. Tanto si eres un experto como si apenas estás incursionando en el ecosistema .NET, esta guía te ayudará a formatear celdas de Excel en un abrir y cerrar de ojos.
## Prerrequisitos
Antes de sumergirte, asegúrate de tener lo siguiente:
- Biblioteca Aspose.Cells para .NET instalada. Puedes... [Descárgalo aquí](https://releases.aspose.com/cells/net/).
- Un conocimiento práctico de C# y programación básica .NET.
- Visual Studio o cualquier IDE .NET instalado en su máquina.
- Una licencia válida de Aspose o [licencia temporal](https://purchase.aspose.com/temporary-license/).
- .NET framework instalado (versión 4.0 o superior).
  
Si te falta alguno de los elementos anteriores, sigue los enlaces para configurarlo todo. ¿Listo? ¡Pasemos a la parte divertida!
## Importar paquetes
Antes de comenzar con el tutorial, asegúrese de importar los espacios de nombres necesarios para trabajar con Aspose.Cells para .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Una vez importados, ya puedes manipular archivos de Excel mediante programación. ¡Ahora, profundicemos en la guía paso a paso!
## Paso 1: Cree o acceda a su libro de Excel
En este paso, creará un nuevo libro. Piense en ello como abrir un nuevo archivo de Excel, ¡pero lo hará mediante código!
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Creación de una instancia de un objeto Workbook
Workbook workbook = new Workbook();
```
Aquí, simplemente estamos instanciando una nueva `Workbook` Objeto. Este actúa como su archivo de Excel, listo para la manipulación de datos. También puede cargar un archivo existente proporcionando su ruta.
## Paso 2: Acceda a la hoja de trabajo
Los libros de Excel pueden contener varias hojas de cálculo. En este paso, accederemos a la primera hoja de cálculo del libro:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Ahora estamos accediendo a la primera hoja de cálculo del libro. Si necesita manipular hojas adicionales, puede referenciarlas mediante su índice o nombre.
## Paso 3: Agregar datos a las celdas
Comencemos agregando datos a celdas específicas. Primero, insertaremos la fecha actual del sistema en la celda "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Esta línea inserta la fecha actual en la celda A1. ¡Genial, verdad? Imagina hacer esto manualmente para cientos de celdas; sería una pesadilla. ¡Ahora, pasemos al formato!
## Paso 4: Formatear la fecha en la celda "A1"
A continuación, formateemos esa fecha con un formato más legible, como "15-Oct-24". Aquí es donde Aspose.Cells realmente destaca:
1. Recuperar el estilo de la celda:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Aquí, estamos capturando el estilo de la celda A1. Piensa en esto como capturar el estilo de la celda antes de hacer cualquier ajuste.
2. Establezca el formato de fecha:
```csharp
style.Number = 15;
```
Configuración de la `Number` La propiedad 15 aplica el formato de fecha deseado. Este es un código de formato numérico integrado para mostrar fechas en el formato "d-mmm-aa".
3. Aplicar el estilo a la celda:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Esta línea aplica los cambios de estilo a la celda. Ahora, en lugar del formato de fecha predeterminado, verá algo mucho más intuitivo como "15-Oct-24".
## Paso 5: Agregar y dar formato a un porcentaje en la celda "A2"
Pasemos al formato de porcentajes. Imagina que quieres insertar un valor y mostrarlo como porcentaje. En este paso, agregaremos un valor numérico a la celda "A2" y le daremos formato de porcentaje:
1. Insertar valor numérico:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Esto inserta el número 20 en la celda A2. Quizás estés pensando: "Es solo un número, ¿cómo lo convierto en un porcentaje?". Bueno, ya llegamos a eso.
2. Recupere el estilo y establezca el formato de porcentaje:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Formato como porcentaje
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Aquí, sumamos 2546 en la celda A3. A continuación, formatearemos este número para que aparezca como moneda.
2. Recupere el estilo y establezca el formato de moneda:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Formato como moneda
worksheet.Cells["A3"].SetStyle(style);
```
Configuración de la `Number` La propiedad a 6 aplica el formato de moneda. Ahora, el valor en la celda A3 se mostrará como "2546,00", con comas y dos decimales.
## Paso 7: Guarde el archivo de Excel
Ahora que hemos aplicado toda la magia del formato, es hora de guardar el archivo:
```csharp
// Guardar el archivo de Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Esta línea guarda el archivo de Excel en el formato Excel 97-2003. Puede cambiar el `SaveFormat` Para adaptarlo a tus necesidades. ¡Y así, creaste y formateaste un archivo de Excel programáticamente!
## Conclusión
¡Felicitaciones! Aprendió a usar Aspose.Cells para .NET para aplicar formatos numéricos integrados a las celdas de un archivo de Excel. Desde fechas hasta porcentajes y monedas, hemos cubierto algunas de las necesidades de formato más comunes para el procesamiento de datos en Excel. Ahora, en lugar de formatear las celdas manualmente, puede automatizar todo el proceso, ahorrando tiempo y reduciendo errores.
## Preguntas frecuentes
### ¿Puedo aplicar formatos de números personalizados usando Aspose.Cells para .NET?
¡Sí! Además de los formatos integrados, Aspose.Cells también admite formatos numéricos personalizados. Puedes crear formatos muy específicos usando... `Custom` propiedad en el `Style` clase.
### ¿Cómo puedo formatear una celda como moneda con un símbolo específico?
Para aplicar un símbolo de moneda específico, puede utilizar un formato personalizado configurando el `Style.Custom` propiedad.
### ¿Puedo formatear filas o columnas enteras?
¡Por supuesto! Puedes aplicar estilos a filas o columnas enteras usando `Rows` o `Columns` colecciones en el `Worksheet` objeto.
### ¿Cómo puedo formatear varias celdas a la vez?
Puedes utilizar el `Range` objeto para seleccionar varias celdas y aplicar estilos a todas ellas a la vez.
### ¿Necesito tener instalado Microsoft Excel para utilizar Aspose.Cells?
No, Aspose.Cells funciona independientemente de Microsoft Excel, por lo que no necesita tener Excel instalado en su máquina.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}