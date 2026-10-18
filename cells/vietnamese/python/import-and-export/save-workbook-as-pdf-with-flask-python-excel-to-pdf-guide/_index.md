---
category: general
date: 2026-06-21
description: Lưu workbook dưới dạng PDF bằng Flask và Aspose.Cells trong Python –
  học cách chuyển đổi XLSX sang PDF, tự động điều chỉnh độ rộng cột Excel, và trả
  về tệp bằng flask send_file pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: vi
og_description: Lưu workbook dưới dạng PDF trong Python bằng Flask. Hướng dẫn chi
  tiết này chỉ cách chuyển đổi XLSX sang PDF, tự động điều chỉnh độ rộng cột Excel
  và phục vụ kết quả bằng flask send_file pdf.
og_title: Lưu sổ làm việc dưới dạng PDF với Flask – Hướng dẫn Python toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: Lưu Sổ làm việc dưới dạng PDF với Flask – Hướng dẫn Python chuyển Excel sang
  PDF
url: /vi/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu Workbook dưới dạng PDF với Flask – Hướng dẫn Python Excel sang PDF

Cần **lưu workbook dưới dạng PDF** từ một dịch vụ web? Bạn không phải là người duy nhất đang thắc mắc cách chuyển một tệp Excel đã tải lên thành PDF mượt mà ngay lập tức. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách lưu workbook dưới dạng PDF bằng Flask và Aspose.Cells, đồng thời đề cập đến cách **chuyển đổi XLSX sang PDF**, tự động điều chỉnh độ rộng cột Excel, và cuối cùng gửi kết quả bằng `flask send_file pdf`.

Chúng ta sẽ bắt đầu với một dự án Flask mới, thêm một vài mẹo thực tiễn, và kết thúc với một endpoint hoạt động đầy đủ mà bất kỳ client nào cũng có thể gọi. Khi hoàn thành, bạn sẽ có thể biến bất kỳ bảng tính nào thành PDF chỉ trong vài dòng mã Python.

## Những gì bạn cần

- **Python 3.8+** (mã chạy được trên 3.9, 3.10 và các phiên bản mới hơn)
- **Flask** (`pip install flask`) – framework web nhẹ mà chúng ta dùng để xây dựng API
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – thư viện thực sự đọc XLSX và ghi PDF
- Kiến thức cơ bản về các yêu cầu HTTP `POST` (không cần gì phức tạp)

Nếu bạn đã có những thành phần này, tuyệt vời—hãy bắt đầu. Nếu chưa, bước “Cài đặt phụ thuộc” sẽ giúp bạn thiết lập.

## Bước 1 – Thiết lập dự án Flask

Đầu tiên, tạo một thư mục mới cho dự án và khởi tạo môi trường ảo. Điều này giúp chúng ta giữ các phụ thuộc gọn gàng.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Bây giờ tạo một tệp có tên `app.py`. Tệp này sẽ chứa toàn bộ logic **save workbook as pdf**.

## Bước 2 – Khởi tạo Ứng dụng Flask

Chúng ta bắt đầu bằng việc import các thành phần cần thiết và tạo đối tượng Flask app. Lưu ý cách block import ngắn gọn—không có module thừa, giúp thời gian khởi động thấp.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Mẹo chuyên nghiệp:** Giữ `app = Flask(__name__)` ở đầu tệp; điều này giúp việc test sau này với các công cụ như `pytest-flask` trở nên dễ dàng.

## Bước 3 – Xây dựng Endpoint Chuyển đổi (convert xlsx to pdf)

Đây là phần cốt lõi của tutorial: một endpoint nhận bảng tính qua `POST`, tải nó vào workbook Aspose.Cells, và chuẩn bị xuất ra PDF.

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### Tại sao mỗi phần lại quan trọng

- **`request.files.get("file")`** – Lấy tệp đã tải lên một cách an toàn; dùng `.get` tránh `KeyError` nếu trường bị thiếu.
- **`io.BytesIO`** – Giữ mọi thứ trong RAM, vì vậy chúng ta không bao giờ ghi tệp tạm thời ra đĩa. Điều này rất quan trọng cho khả năng mở rộng.
- **`auto_fit_columns()`** – Nếu không có hàm này, độ rộng cột thường bị chật trong PDF. Phương thức mở rộng mỗi cột để vừa với ô dài nhất, tạo cảm giác chuyên nghiệp.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – Lệnh duy nhất này thực hiện việc chuyển đổi XLSX sang PDF. Aspose.Cells xử lý công thức, biểu đồ và ngay cả các ô đã hợp nhất.
- **`flask send_file pdf`** – Gửi PDF về client với các header phù hợp, kích hoạt tải xuống với tên `output.pdf`.

## Bước 4 – Chạy Server Flask

Thêm “run guard” tiêu chuẩn ở cuối `app.py` để script có thể được thực thi trực tiếp.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

Chạy `python app.py` sẽ khởi động server tại `http://localhost:5000`. Cờ `debug=True` hữu ích trong quá trình phát triển; nhớ tắt nó khi đưa vào production.

## Bước 5 – Kiểm tra Endpoint (Thủ công & Tự động)

### Kiểm tra thủ công với cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

Nếu mọi thứ diễn ra tốt, `result.pdf` sẽ chứa phiên bản được định dạng đẹp của `sample.xlsx`, với tất cả các cột đã được tự động điều chỉnh.

### Kiểm tra tự động với `requests` của Python

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

Cả hai cách đều minh họa quy trình **python excel to pdf** đầy đủ—from upload to download—mà không cần chạm tới hệ thống tệp trên server.

## Bước 6 – Các trường hợp góc cạnh & Những lỗi thường gặp

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Các tệp XLSX lớn ( > 50 MB ) | Áp lực bộ nhớ trên server | Dòng dữ liệu tải lên vào một tệp tạm thời và sử dụng `Workbook(file_path)` thay vì `BytesIO`. |
| Workbook được bảo vệ bằng mật khẩu | `Workbook` ném ra ngoại lệ | Truyền mật khẩu vào constructor của `Workbook`: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| Thiếu `auto_fit_columns()` | Các cột PDF bị cắt ngắn | Luôn gọi `auto_fit_columns()` **trước** `save()`. |
| Client mong đợi lỗi dạng JSON | Flask trả về trang lỗi HTML | Trả về một dict JSON với mã trạng thái phù hợp như trong endpoint (dòng `return {"error": "No file provided"}, 400`). |

Bằng cách dự đoán những tình huống này, API của bạn sẽ luôn ổn định và thân thiện với người dùng.

## Bước 7 – Triển khai vào môi trường Production

Khi bạn đã sẵn sàng đưa vào hoạt động, hãy cân nhắc các điều chỉnh cấp production sau:

- **Sử dụng server WSGI** như `gunicorn` (`gunicorn -w 4 app:app`) thay vì server tích hợp của Flask.
- **Kích hoạt HTTPS** qua reverse proxy (NGINX) để bảo vệ các tệp tải lên.
- **Đặt giới hạn kích thước yêu cầu** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) để tránh các cuộc tấn công từ chối dịch vụ.
- **Ghi log lỗi** bằng một logger có cấu trúc (ví dụ `structlog`) để bạn có thể truy vết các lỗi chuyển đổi.

Tất cả các bước này vẫn giữ nguyên logic cốt lõi **save workbook as pdf** trong khi làm cho dịch vụ sẵn sàng cho production.

## Kết quả mong đợi

Khi bạn gọi endpoint `/convert` với một tệp XLSX hợp lệ, phản hồi sẽ:

1. Có header `Content-Type: application/pdf`.
2. Yêu cầu trình duyệt (hoặc client) tải về tệp có tên `output.pdf`.
3. Hiển thị bảng tính với các cột tự động điều chỉnh kích thước theo nội dung, nhờ lời gọi `auto fit excel columns`.

Mở PDF đã tải xuống—bạn sẽ thấy mỗi cột hiển thị đầy đủ, công thức đã được tính toán, và bất kỳ hình ảnh nhúng nào cũng được giữ nguyên.

## Kết luận

Bạn giờ đã có một ví dụ hoàn chỉnh, sẵn sàng cho production, giúp **save workbook as pdf** bằng Flask, Aspose.Cells và Python thuần. Tutorial đã bao phủ mọi thứ từ thiết lập môi trường, **convert xlsx to pdf**, tự động điều chỉnh cột, và cuối cùng gửi kết quả bằng `flask send_file pdf`.

Tiếp theo, bạn có thể khám phá việc thêm **custom styling**, hợp nhất ô, hoặc thậm chí chuyển đổi nhiều worksheet thành một PDF đa trang. Mẫu này cũng áp dụng cho các loại tệp khác—chỉ cần thay đổi enum `SaveFormat`.

Có câu hỏi nào về các trường hợp góc cạnh hoặc triển khai? Hãy để lại bình luận bên dưới, và chúc bạn coding vui!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn đầy đủ cùng giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Lưu Các Trang Cụ thể của Tệp Excel dưới dạng PDF bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Lưu Workbook Excel dưới dạng PDF với Font Tùy chỉnh bằng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Chuyển đổi Excel sang PDF với Điều chỉnh Cột trong Java bằng Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}