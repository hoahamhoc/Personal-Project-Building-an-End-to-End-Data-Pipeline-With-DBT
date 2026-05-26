# 📁 Building an End-to-End Data Pipeline

> Mô tả chi tiết quy trình xử lý dữ liệu từ raw data đến visualization bằng BI tools.

![Pipeline Overview](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

---

## 📌 Tổng quan dự án

Dự án này xây dựng một pipeline dữ liệu hoàn chỉnh (end-to-end), bao gồm các bước từ thu thập dữ liệu thô, xử lý, xây dựng data mart đến trực quan hóa bằng dashboard.

**Dataset sử dụng:** [Wide World Importers – Microsoft SQL Server](https://dataedo.com/samples/html/WideWorldImporters/doc/WideWorldImporters_5/tables.html)

---

## 🔄 Kiến trúc Pipeline

```
CSV Files (Wide World Importers)
        │
        ▼
  [PySpark] – Đọc & nạp dữ liệu thô
        │
        ▼
   SQL Server – Lưu trữ raw data
        │
        ▼
  [dbt] – Xây dựng Data Mart (Kimball Architecture)
        │
        ▼
  Power BI – Dashboard & Visualization
```

---

## 🚀 Các bước thực hiện

### Bước 1 – Chuẩn bị dữ liệu

- Nguồn dữ liệu: **Wide World Importers dataset** ở định dạng CSV (wide format)
- Chứa đầy đủ thông tin cần thiết cho phân tích sales
- 📥 [Tải dataset tại đây](https://dataedo.com/samples/html/WideWorldImporters/doc/WideWorldImporters_5/tables.html)

---

### Bước 2 – Đẩy dữ liệu thô lên SQL Server bằng PySpark

Sử dụng **PySpark** để đọc nhiều file CSV từ dataset Wide World Importers và nạp vào **SQL Server**.

📄 **Code:** [Transform data.py](https://github.com/hoanguyen290120/Personal-Project/blob/main/Transform%20data.py)

**Quy trình:**
- Đọc các file CSV bằng PySpark
- Thực hiện các bước làm sạch dữ liệu cơ bản
- Nạp dữ liệu vào SQL Server

---

### Bước 3 – Xây dựng Data Mart bằng dbt

Sử dụng **dbt** (Data Build Tool) để xây dựng data mart phục vụ đội sales, dựa trên kiến trúc **Kimball**.

📄 **Code:** [dim_customer.sql](https://github.com/hoanguyen290120/dbt_sqlserver_project/blob/main/models/analytics/dim_customer.sql)

**Công cụ sử dụng:**

| Công cụ | Mục đích |
|---|---|
| `dbt-core` | Xây dựng data pipeline |
| `SQL Server` | Lưu trữ dữ liệu |
| `GitHub` | Quản lý & version control code |

**Kỹ thuật xử lý dữ liệu (Kimball Architecture):**
- **Flatten** – Làm phẳng dữ liệu lồng nhau
- **Junk Dimension** – Gom nhóm các flag/indicator
- **Composite Key** – Khóa tổng hợp
- **Incremental Load** – Tải dữ liệu tăng dần

🗂️ **Data Model:** [Sales Data Mart Model (Kimball)](https://drawdb.vercel.app/editor?shareId=d2671a8933b80673e7ed6abdda8e6d7c)

---

### Bước 4 – Trực quan hóa bằng Power BI

Tạo reports và dashboards từ data mart đã xây dựng ở bước 3.

📊 **Dashboard:** [Xem online](https://report.onhandbi.com/public/report?token=eyJhbGciOiJIUzI1NiJ9.eyJwdWJsaWNfbGlua19pZCI6NjU1LCJoYXNfcGFzc2NvZGUiOmZhbHNlLCJ0aW1lIjoxNzc5NzY0MDI0fQ.uHOJdnJyz7rURt4ARBhjHGRFaBjeeR7EO4kS0J2-bXA) | [PDF](https://drive.google.com/file/d/1bChlDU9gGcN4xuE-p-szMNg91fJn8avO/view?usp=sharing)

> 💡 Nếu không truy cập được Power BI online, hãy tải file PDF để xem nội dung phân tích.

---

## 🛠️ Tech Stack

| Lớp | Công cụ |
|---|---|
| **Ingestion** | PySpark |
| **Storage** | Microsoft SQL Server |
| **Transformation** | dbt-core |
| **Visualization** | Power BI |
| **Version Control** | GitHub |

---

## 📂 Cấu trúc Repository

```
├── Transform data.py         # PySpark script – nạp dữ liệu vào SQL Server
├── dbt_sqlserver_project/
│   └── models/
│       └── analytics/
│           └── dim_customer.sql   # dbt model mẫu
└── README.md
```

---

## 📬 Liên hệ

Nếu bạn có câu hỏi hoặc góp ý về dự án, hãy tạo một **Issue** hoặc liên hệ trực tiếp qua GitHub.

---

*Cảm ơn bạn đã theo dõi dự án!* 🙌
