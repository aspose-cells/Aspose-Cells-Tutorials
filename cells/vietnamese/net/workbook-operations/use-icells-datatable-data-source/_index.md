---
title: Sử dụng ICellsDataTableDataSource cho Workbook Designer
linktitle: Sử dụng ICellsDataTableDataSource cho Workbook Designer
second_title: API xử lý Excel Aspose.Cells .NET
description: Học cách sử dụng ICellsDataTableDataSource với Aspose.Cells cho .NET để điền dữ liệu động vào bảng tính Excel. Hoàn hảo để tự động hóa dữ liệu khách hàng trong sổ làm việc.
weight: 21
url: /vi/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sử dụng ICellsDataTableDataSource cho Workbook Designer

## Giới thiệu
 Việc tạo bảng tính nâng cao với tích hợp dữ liệu tự động có thể là một bước ngoặt, đặc biệt là trong các ứng dụng kinh doanh. Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách sử dụng`ICellsDataTableDataSource`cho một nhà thiết kế sổ làm việc trong Aspose.Cells cho .NET. Chúng tôi sẽ hướng dẫn bạn xây dựng một giải pháp đơn giản, dễ đọc để tải dữ liệu tùy chỉnh vào tệp Excel một cách động. Vì vậy, nếu bạn đang làm việc với danh sách khách hàng, dữ liệu bán hàng hoặc bất kỳ thứ gì tương tự, hướng dẫn này dành cho bạn!
## Điều kiện tiên quyết
Để bắt đầu, hãy đảm bảo bạn có những điều sau:
-  Aspose.Cells cho Thư viện .NET – Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/) hoặc dùng thử phiên bản miễn phí.
- Môi trường phát triển .NET – Visual Studio là một lựa chọn tuyệt vời.
- Hiểu biết cơ bản về C# – Sự quen thuộc với các lớp và xử lý dữ liệu sẽ giúp bạn theo dõi.
Trước khi tiến hành, hãy đảm bảo rằng môi trường phát triển của bạn đã được thiết lập các gói cần thiết.
## Nhập gói
Để sử dụng Aspose.Cells hiệu quả, bạn cần nhập các gói cần thiết. Dưới đây là tài liệu tham khảo nhanh về các không gian tên cần thiết:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Bước 1: Xác định Lớp dữ liệu khách hàng
 Để bắt đầu, hãy tạo một`Customer` lớp. Lớp này sẽ lưu giữ các thông tin cơ bản của khách hàng như`FullName` Và`Address`Hãy nghĩ về nó như một cách để xác định "hình dạng" dữ liệu của bạn.
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
## Bước 2: Thiết lập lớp danh sách khách hàng
 Tiếp theo, xác định một`CustomerList` lớp mở rộng`ArrayList` . Danh sách tùy chỉnh này sẽ lưu giữ các trường hợp`Customer` và cho phép truy cập được lập chỉ mục vào từng mục nhập.
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
Ở bước này, chúng ta sẽ gói dữ liệu vào định dạng mà Aspose.Cells có thể nhận dạng và xử lý.
## Bước 3: Tạo lớp nguồn dữ liệu khách hàng
 Đây là nơi mọi thứ trở nên thú vị. Chúng tôi sẽ tạo ra một`CustomerDataSource` lớp thực hiện`ICellsDataTable` để làm cho dữ liệu của chúng tôi tương thích với trình thiết kế sổ làm việc của Aspose.Cells.
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
 Phong tục này`CustomerDataSource` lớp cho phép Aspose.Cells diễn giải từng`Customer` đối tượng dưới dạng một hàng trong tệp Excel.
## Bước 4: Khởi tạo dữ liệu khách hàng
Bây giờ, hãy thêm một số khách hàng vào danh sách của chúng ta. Đây là nơi chúng ta tải dữ liệu để ghi vào sổ làm việc. Hãy thoải mái thêm nhiều mục nhập hơn nếu cần.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Trong ví dụ này, chúng ta đang làm việc với một tập dữ liệu nhỏ. Tuy nhiên, bạn có thể dễ dàng mở rộng danh sách này bằng cách tải dữ liệu từ cơ sở dữ liệu hoặc các nguồn khác.
## Bước 5: Tải Workbook
Bây giờ, hãy mở một sổ làm việc Excel hiện có chứa các Smart Marker cần thiết. Sổ làm việc này sẽ đóng vai trò là mẫu của chúng ta và Aspose.Cells sẽ thay thế Smart Marker một cách động bằng dữ liệu khách hàng.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Đảm bảo rằng`"SmartMarker1.xlsx"` chứa các chỗ giữ chỗ như`&=Customer.FullName` Và`&=Customer.Address` nơi dữ liệu cần được điền vào.
## Bước 6: Thiết lập Workbook Designer
Bây giờ, hãy cấu hình trình thiết kế sổ làm việc để liên kết nguồn dữ liệu khách hàng với Smart Marker của sổ làm việc.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 Các`SetDataSource` phương pháp ràng buộc của chúng tôi`CustomerDataSource` vào các Đánh dấu thông minh trong sổ làm việc. Mỗi đánh dấu được dán nhãn`&=Customer` trong Excel bây giờ sẽ được thay thế bằng dữ liệu khách hàng tương ứng.
## Bước 7: Xử lý và Lưu Sổ làm việc
Cuối cùng, hãy xử lý bảng tính để điền dữ liệu và lưu kết quả.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Mã này kích hoạt quá trình xử lý Smart Marker, thay thế tất cả các chỗ giữ chỗ bằng dữ liệu và lưu kết quả dưới dạng`dest.xlsx`.
## Phần kết luận
 Xin chúc mừng! Bạn đã triển khai thành công`ICellsDataTableDataSource` cho một nhà thiết kế sổ làm việc sử dụng Aspose.Cells cho .NET. Phương pháp này lý tưởng để tự động hóa việc điền dữ liệu trong bảng tính, đặc biệt là khi xử lý dữ liệu động như danh sách khách hàng hoặc hàng tồn kho sản phẩm. Với những kỹ năng này, bạn đang trên đường xây dựng các ứng dụng dựa trên dữ liệu giúp việc báo cáo dựa trên Excel trở nên dễ dàng!
## Câu hỏi thường gặp
###  Là gì`ICellsDataTable` in Aspose.Cells?  
Đây là giao diện cho phép liên kết các nguồn dữ liệu tùy chỉnh với Aspose.Cells Smart Markers để điền dữ liệu động.
### Làm thế nào để tùy chỉnh dữ liệu trong mẫu bảng tính?  
 Các chỗ giữ chỗ được gọi là Smart Marker, chẳng hạn như`&=Customer.FullName`, được sử dụng. Các dấu hiệu này được thay thế bằng dữ liệu thực trong quá trình xử lý.
### Aspose.Cells cho .NET có miễn phí không?  
 Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng quyền truy cập đầy đủ yêu cầu giấy phép trả phí. Kiểm tra[dùng thử miễn phí](https://releases.aspose.com/) hoặc[mua](https://purchase.aspose.com/buy) tùy chọn.
### Tôi có thể thêm dữ liệu khách hàng một cách linh hoạt không?  
 Chắc chắn rồi! Chỉ cần điền vào`CustomerList`với các mục nhập bổ sung trước khi chạy chương trình.
### Tôi có thể nhận trợ giúp ở đâu nếu gặp khó khăn?  
 Aspose có một[diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9) nơi người dùng có thể đặt câu hỏi và nhận sự hỗ trợ từ cộng đồng và nhóm Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
