---
title: Utilice ICellsDataTableDataSource para el Diseñador de libros de trabajo
linktitle: Utilice ICellsDataTableDataSource para el Diseñador de libros de trabajo
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a utilizar ICellsDataTableDataSource con Aspose.Cells para .NET para completar dinámicamente hojas de Excel. Perfecto para automatizar datos de clientes en libros de trabajo.
weight: 21
url: /es/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utilice ICellsDataTableDataSource para el Diseñador de libros de trabajo

## Introducción
 La creación de hojas de cálculo avanzadas con integración de datos automatizada puede ser un punto de inflexión, especialmente en aplicaciones empresariales. En este tutorial, analizaremos en profundidad cómo utilizar`ICellsDataTableDataSource`para un diseñador de libros de trabajo en Aspose.Cells para .NET. Le guiaremos en la creación de una solución sencilla y legible para cargar datos personalizados en un archivo de Excel de forma dinámica. Por lo tanto, si trabaja con listas de clientes, datos de ventas o algo similar, ¡esta guía es para usted!
## Prerrequisitos
Para comenzar, asegúrese de tener lo siguiente:
-  Biblioteca Aspose.Cells para .NET: puede descargarla desde[aquí](https://releases.aspose.com/cells/net/) o obtenga una versión de prueba gratuita.
- Entorno de desarrollo .NET: Visual Studio es una excelente opción.
- Comprensión básica de C#: la familiaridad con las clases y el manejo de datos le ayudará a seguir adelante.
Antes de continuar, asegúrese de que su entorno de desarrollo esté configurado con los paquetes necesarios.
## Importar paquetes
Para utilizar Aspose.Cells de forma eficaz, es necesario importar los paquetes esenciales. A continuación, se incluye una referencia rápida de los espacios de nombres necesarios:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Paso 1: Definir una clase de datos de cliente
 Para comenzar, crea un simple`Customer` Clase. Esta clase contendrá detalles básicos del cliente como`FullName` y`Address`Piense en ello como una forma de definir la "forma" de sus datos.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Paso 2: Configurar la clase de lista de clientes
 A continuación, defina una`CustomerList` clase que se extiende`ArrayList` Esta lista personalizada contendrá instancias de`Customer` y permitir el acceso indexado a cada entrada.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
En este paso, envolvemos nuestros datos en un formato que Aspose.Cells pueda reconocer y procesar.
## Paso 3: Crear la clase de fuente de datos del cliente
 Aquí es donde las cosas se ponen interesantes. Crearemos un`CustomerDataSource` clase que implementa`ICellsDataTable` para hacer que nuestros datos sean compatibles con el diseñador de libros de trabajo de Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 Esta costumbre`CustomerDataSource` La clase permite que Aspose.Cells interprete cada una`Customer` objeto como una fila en el archivo Excel.
## Paso 4: Inicializar los datos del cliente
Ahora, agreguemos algunos clientes a nuestra lista. Aquí es donde cargamos los datos que se escribirán en el libro de trabajo. Siéntase libre de agregar más entradas según sea necesario.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
En este ejemplo, trabajamos con un conjunto de datos pequeño. Sin embargo, puedes ampliar fácilmente esta lista cargando datos de una base de datos u otras fuentes.
## Paso 5: Cargue el libro de trabajo
Ahora, abramos un libro de Excel existente que contenga los marcadores inteligentes necesarios. Este libro de Excel servirá como plantilla y Aspose.Cells reemplazará dinámicamente los marcadores inteligentes con los datos del cliente.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Asegúrese de que`"SmartMarker1.xlsx"` contiene marcadores de posición como`&=Customer.FullName` y`&=Customer.Address` donde se deben rellenar los datos.
## Paso 6: Configurar el Diseñador de libros de trabajo
Ahora, configuremos el diseñador del libro de trabajo para vincular nuestra fuente de datos de clientes con los marcadores inteligentes del libro de trabajo.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 El`SetDataSource` El método une nuestro`CustomerDataSource` a los marcadores inteligentes en el libro de trabajo. Cada marcador etiquetado`&=Customer` en Excel ahora serán reemplazados por los datos del cliente correspondientes.
## Paso 7: Procesar y guardar el libro de trabajo
Por último, procesemos el libro de trabajo para completar los datos y guardar los resultados.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Este código activa el procesamiento del marcador inteligente, reemplaza todos los marcadores de posición con datos y guarda el resultado como`dest.xlsx`.
## Conclusión
 ¡Felicitaciones! Lo has implementado exitosamente`ICellsDataTableDataSource` para un diseñador de libros de trabajo que utilice Aspose.Cells para .NET. Este enfoque es ideal para automatizar la introducción de datos en hojas de cálculo, especialmente cuando se trabaja con datos dinámicos como listas de clientes o inventarios de productos. Con estas habilidades, estará en camino de crear aplicaciones basadas en datos que faciliten la creación de informes basados en Excel.
## Preguntas frecuentes
###  Qué es`ICellsDataTable` in Aspose.Cells?  
Es una interfaz que permite vincular fuentes de datos personalizadas con marcadores inteligentes Aspose.Cells para la población de datos dinámica.
### ¿Cómo puedo personalizar los datos en la plantilla del libro de trabajo?  
 Los marcadores de posición llamados marcadores inteligentes, como`&=Customer.FullName`Se utilizan marcadores que se reemplazan con datos reales durante el procesamiento.
### ¿Aspose.Cells para .NET es gratuito?  
 Aspose.Cells ofrece una prueba gratuita, pero el acceso completo requiere una licencia paga. Consulte su[prueba gratis](https://releases.aspose.com/) o[comprar](https://purchase.aspose.com/buy) Opciones.
### ¿Puedo agregar más datos de clientes de forma dinámica?  
 ¡Por supuesto! Simplemente complete el campo`CustomerList`con entradas adicionales antes de ejecutar el programa.
### ¿Dónde puedo obtener ayuda si estoy estancado?  
 Aspose tiene una[foro de soporte](https://forum.aspose.com/c/cells/9) donde los usuarios pueden hacer preguntas y obtener asistencia de la comunidad y del equipo de Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
