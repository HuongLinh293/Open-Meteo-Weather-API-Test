# 🌦️ BÁO CÁO KIỂM THỬ API - OPEN-METEO WEATHER API

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![API Testing](https://img.shields.io/badge/Testing-QA%2FQC-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

Báo cáo kiểm thử chi tiết dịch vụ thời tiết **Open-Meteo Weather API** (`https://api.open-meteo.com/v1/forecast`) bằng công cụ Postman.

---

## 📌 1. Thông Tin Tổng Quan

- **Tên Dự Án:** Open-Meteo Weather API Test Collection
- **Ngày Kiểm Thử:** 07/10/2026
- **Người Kiểm Thử:** Tạ Thu Hương Linh
- **Mục Tiêu Kiểm Thử:** Kiểm tra tính chính xác, khả năng xử lý tham số và phản hồi lỗi của Open-Meteo API.
- **Môi Trường Kiểm Thử:** Postman Desktop.
- **Phương Pháp Kiểm Thử:** Kiểm thử thủ công kết hợp Test Scripts tự động trên Postman.

---

## 🧪 2. Kịch Bản Kiểm Thử (Test Cases)

### 🔹 Kịch Bản Kiểm Thử 1: Lấy thời tiết hiện tại (PASS)

- **Tên Kịch Bản:** Kịch bản 1: Lấy thời tiết hiện tại (PASS)
- **Mục Đích:** Kiểm tra API trả về dữ liệu thời tiết thực tế thành công với các tham số hợp lệ.
- **Phương Thức HTTP:** `GET`
- **URL:** `https://api.open-meteo.com/v1/forecast?latitude=46.9481&longitude=7.4474&current=temperature_2m,relative_humidity_2m,rain,weather_code`
- **Tham Số (Query Params):**
  - `latitude`: `46.9481` (Vĩ độ)
  - `longitude`: `7.4474` (Kinh độ)
  - `current`: `temperature_2m,relative_humidity_2m,rain,weather_code` (Các chỉ số đo lường)
- **Kết Quả Mong Đợi:** Trả về mã HTTP `200 OK`, thời gian phản hồi hợp lý, dữ liệu thời tiết đầy đủ.
- **Kết Quả Thực Tế:** HTTP `200 OK` (886 ms, 457 B), Test Results đạt 2/2.
- **Trạng Thái:** **Thành công (PASS)**

#### Ảnh chụp kiểm thử:
<img width="1223" height="917" alt="Ảnh màn hình Kịch bản 1" src="https://github.com/user-attachments/assets/751fba80-d089-40e4-8f76-5590fc10a2a3" />

#### Dữ liệu phản hồi (Response Body):
```json
{
    "latitude": 46.951378,
    "longitude": 7.4586725,
    "generationtime_ms": 0.13744831085205078,
    "utc_offset_seconds": 0,
    "timezone": "GMT",
    "timezone_abbreviation": "GMT",
    "elevation": 554.0,
    "current_units": {
        "time": "iso8601",
        "interval": "seconds",
        "temperature_2m": "°C",
        "relative_humidity_2m": "%",
        "rain": "mm",
        "weather_code": "wmo code"
    },
    "current": {
        "time": "2026-10-07T09:30",
        "interval": 900,
        "temperature_2m": 16.2,
        "relative_humidity_2m": 71,
        "rain": 0.00,
        "weather_code": 3
    }
}
```

---

### 🔹 Kịch Bản Kiểm Thử 2: Vĩ độ sai dải cho phép (Negative Test - FAIL/400)

- **Tên Kịch Bản:** Kịch bản 2: Vĩ độ sai dải cho phép (FAIL/400)
- **Mục Đích:** Kiểm thử tính đúng đắn khi người dùng nhập dữ liệu không hợp lệ (Negative Testing).
- **Phương Thức HTTP:** `GET`
- **URL:** `https://api.open-meteo.com/v1/forecast?latitude=999.0&longitude=7.4474&current=temperature_2m`
- **Tham Số (Query Params):**
  - `latitude`: `999.0` *(Vượt quá phạm vi hợp lệ [-90, 90])*
  - `longitude`: `7.4474`
  - `current`: `temperature_2m`
- **Kết Quả Mong Đợi:** API chặn lỗi đầu vào, trả về mã HTTP `400 Bad Request` kèm thông báo lý do rõ ràng.
- **Kết Quả Thực Tế:** HTTP `400 Bad Request` (1.02 s, 271 B), Test Results 2/2.
- **Trạng Thái:** **Đạt yêu cầu (Handled Properly)**

#### Ảnh chụp kiểm thử:
<img width="1232" height="880" alt="Ảnh màn hình Kịch bản 2" src="https://github.com/user-attachments/assets/274b7ac9-7aa2-4346-8642-99f360efeaa9" />

#### Dữ liệu phản hồi (Response Body):
```json
{
    "error": true,
    "reason": "Latitude must be in range of -90 to 90°. Given: 999.0."
}
```

---

### 🔹 Kịch Bản Kiểm Thử 3: Tùy chỉnh đơn vị nhiệt độ Fahrenheit (PASS)

- **Tên Kịch Bản:** Kịch bản 3: Tùy chỉnh Đơn vị Fahrenheit (PASS)
- **Mục Đích:** Kiểm tra khả năng xử lý tham số tùy biến đơn vị nhiệt độ (`temperature_unit=fahrenheit`).
- **Phương Thức HTTP:** `GET`
- **URL:** `https://api.open-meteo.com/v1/forecast?latitude=46.9481&longitude=7.4474&current=temperature_2m&temperature_unit=fahrenheit`
- **Tham Số (Query Params):**
  - `latitude`: `46.9481`
  - `longitude`: `7.4474`
  - `current`: `temperature_2m`
  - `temperature_unit`: `fahrenheit`
- **Kết Quả Mong Đợi:** Trả về mã HTTP `200 OK`, đơn vị trả về trong `current_units` là `°F`.
- **Kết Quả Thực Tế:** HTTP `200 OK` (215 ms, 403 B), Test Results 2/2. Nhiệt độ trả về theo độ F (`61.2 °F`).
- **Trạng Thái:** **Thành công (PASS)**

#### Ảnh chụp kiểm thử:
<img width="1242" height="891" alt="Ảnh màn hình Kịch bản 3" src="https://github.com/user-attachments/assets/b7764ab0-27b3-44b3-963e-653f37abce9f" />

#### Dữ liệu phản hồi (Response Body):
```json
{
    "latitude": 46.951378,
    "longitude": 7.4586725,
    "generationtime_ms": 0.03337860107421875,
    "utc_offset_seconds": 0,
    "timezone": "GMT",
    "timezone_abbreviation": "GMT",
    "elevation": 554.0,
    "current_units": {
        "time": "iso8601",
        "interval": "seconds",
        "temperature_2m": "°F"
    },
    "current": {
        "time": "2026-10-07T09:30",
        "interval": 900,
        "temperature_2m": 61.2
    }
}
```

---

## 📊 3. Tổng Kết Kết Quả Kiểm Thử

| STT | Kịch Bản Kiểm Thử | Phương Thức | HTTP Status Code | Kết Quả Thực Tế | Đánh Giá |
|:---:|:---|:---:|:---:|:---|:---:|
| 1 | Lấy thời tiết hiện tại | GET | `200 OK` | Lấy dữ liệu thành công | ✅ PASS |
| 2 | Vĩ độ ngoài dải cho phép (`999.0`) | GET | `400 Bad Request` | Bắt lỗi validation chính xác | ✅ PASS |
| 3 | Tùy chỉnh đơn vị Fahrenheit | GET | `200 OK` | Trả về đơn vị `°F` chính xác | ✅ PASS |

- **Tổng số kịch bản:** 3
- **Số kịch bản đạt yêu cầu (Pass):** 3/3
- **Tỉ lệ đạt yêu cầu:** **100%**

---

## 🐞 4. Nhận Xét & Đánh Giá API

1. **Khả năng phản hồi:** Thời gian phản hồi nhanh (từ 215 ms đến 886 ms).
2. **Xử lý tham số đầu vào:** API xử lý tốt các tham số tùy chọn (như `temperature_unit`).
3. **Bắt lỗi & Validation:** Khi truyền tham số không hợp lệ (như `latitude=999.0`), API không gặp lỗi máy chủ (500) mà trả về `400 Bad Request` với message rõ ràng, giúp client dễ dàng sửa lỗi.
