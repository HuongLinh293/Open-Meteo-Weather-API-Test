# 🚀 API Automation & Manual Testing Collection

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![API Testing](https://img.shields.io/badge/Testing-QA%2FQC-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

Dự án này lưu trữ các bộ kịch bản kiểm thử API (Postman Collections) tự động và thủ công cho các dịch vụ RESTful API công khai, bao gồm báo cáo kiểm thử và mã kiểm tra phản hồi (Test Scripts).

---

## 📋 Danh Sách API Đã Kiểm Thử

1. **NASA NeoWS API** (`Near Earth Object Web Service`)
   - **Endpoint:** `https://api.nasa.gov/neo/rest/v1/neo/browse`
   - **Mục tiêu:** Kiểm thử danh sách tiểu hành tinh, xử lý phân trang và xử lý lỗi đường dẫn 404.

2. **Open-Meteo Weather API**
   - **Endpoint:** `https://api.open-meteo.com/v1/forecast`
   - **Mục tiêu:** Kiểm thử truy vấn thông số thời tiết thời gian thực, validate tham số tọa độ (Latitude/Longitude) và đơn vị đo.

---

## 🛠️ Yêu Cầu Môi Trường & Công Cụ

- **Postman:** Phiên bản Desktop App hoặc Web App.
- **Node.js / Newman** *(Tùy chọn nếu muốn chạy CLI)*: Phiên bản `>=14.x`.

---

## 📦 Hướng Dẫn Import & Chạy Kiểm Thử Trong Postman

### Bước 1: Clone hoặc Cài đặt Collection
1. Sao chép nội dung mã JSON Postman Collection tương ứng (NASA hoặc Open-Meteo).
2. Lưu thành tập tin `.json` (Ví dụ: `Open-Meteo_Test_Collection.json`).

### Bước 2: Import vào Postman
1. Mở phần mềm **Postman**.
2. Nhấn nút **Import** ở góc trên bên trái.
3. Kéo thả tập tin `.json` vừa lưu vào vùng làm việc.

### Bước 3: Thực thi Test Suite
1. Nhấp chuột phải vào tên **Collection** vừa import.
2. Chọn **Run collection**.
3. Bấm **Run [Tên Collection]** để tiến hành chạy tự động tất cả các Test Scripts.

---

## 📊 Báo Cáo Kết Quả Kiểm Thử (Test Summary)

| Tên Dịch Vụ API | Tổng Số Test Case | PASS | FAIL (Expected Error) | Tỷ Lệ Thành Công |
| :--- | :---: | :---: | :---: | :---: |
| **NASA NeoWS API** | 3 | 2 | 1 (404 Not Found) | **66.67%** |
| **Open-Meteo API** | 3 | 2 | 1 (400 Bad Request) | **66.67%** |

---

## 🧪 Các Kịch Bản Kiểm Thử Chi Tiết

<details>
<summary><b>1. Open-Meteo Weather API</b></summary>

- **Kịch bản 1 (PASS):** Lấy thông tin thời tiết hiện tại (Nhiệt độ, Độ ẩm, Lượng mưa, Mã thời tiết) tại Bern (`latitude=46.9481`, `longitude=7.4474`).
- **Kịch bản 2 (FAIL - Expected):** Truyền vĩ độ `latitude=999.0` vượt quá dải cho phép (`-90` đến `90`). Trả về mã lỗi `400 Bad Request`.
- **Kịch bản 3 (PASS):** Tùy chỉnh đơn vị đo sang Fahrenheit (`temperature_unit=fahrenheit`).
</details>

<details>
<summary><b>2. NASA NeoWS API</b></summary>

- **Kịch bản 1 (PASS):** Lấy thông tin danh sách tiểu hành tinh mặc định từ Endpoint gốc.
- **Kịch bản 2 (FAIL - Expected):** Gửi yêu cầu thiếu tài nguyên `/neo/browse`. Server trả về `404 Not Found`.
- **Kịch bản 3 (PASS):** Phân trang dữ liệu với tham số `page=1&size=2`.
</details>

---

## 👤 Thông Tin Người Thực Hiện

- **Người kiểm thử:** Giang Thành An
- **Vai trò:** QA / QC Tester
- **Ngày thực hiện:** 07/10/2026# Open-Meteo-Weather-API-Test
