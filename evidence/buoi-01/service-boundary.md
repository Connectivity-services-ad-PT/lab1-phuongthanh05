# Service Boundary của nhóm

## 1. Thông tin nhóm

- Tên nhóm:Nhóm 3B
- Lớp: CNTT 1710
- Thành viên: 
Hà Thị Phương Thanh
Đỗ Công Ngọc Sơn
Nguyễn Thị Thu Vui
Đinh Mạnh Đà
- Service nhóm phụ trách: IOT
- Sản phẩm tổng thể của lớp:
Hệ thống quản lý thông minh 
## 2. Actor

Các đối tượng tương tác với hệ thống/service:

User (Người dùng): xem dữ liệu từ thiết bị (nhiệt độ, độ ẩm, trạng thái…)
Admin: quản lý thiết bị, cấu hình hệ thống
IoT Device (Thiết bị): gửi dữ liệu sensor về hệ thống
Service khác (Frontend / AI / Dashboard): gọi API để lấy dữ liệu

## 3. System Boundary
Nhóm xây dựng IoT Service – xử lý dữ liệu từ thiết bị
Phần nhóm kiểm soát:
Nhận dữ liệu từ IoT device
Xử lý dữ liệu (kiểm tra, chuẩn hóa)
Lưu trữ dữ liệu vào database
Cung cấp API cho hệ thống
Theo dõi trạng thái thiết bị
- ...

Phần nhóm chỉ tích hợp:
Frontend (Web/App)
Auth Service (đăng nhập)
AI Service (phân tích dữ liệu)
Notification Service (gửi cảnh báo)
- ...

## 4. Service Boundary

Service của nhóm có trách nhiệm gì?
Thu thập dữ liệu từ thiết bị IoT
Lưu trữ dữ liệu sensor
Cung cấp API truy vấn dữ liệu
Quản lý thông tin thiết bị
Theo dõi trạng thái hoạt động

Service KHÔNG làm gì?
Không xây dựng giao diện người dùng
Không xử lý đăng nhập / xác thực
Không phân tích AI nâng cao
Không gửi thông báo trực tiếp cho người dùng
## 5. Input / Output

### Input
Dữ liệu từ IoT Device:
Nhiệt độ
Độ ẩm
Trạng thái thiết bị
Request từ hệ thống:
Lấy dữ liệu sensor
Lấy thông tin thiết bị
- ...

### Output
Dữ liệu sensor (JSON)
Trạng thái thiết bị
API response
- ...

## 6. API dự kiến

| Method | Endpoint | Mục đích |
|---|---|---|
| GET | /health | Kiểm tra service |
| POST | ... | ... |

Method | Endpoint | Mục đích
|---|---|---|
GET	|/health|	Kiểm tra service|
POST|	/iot/data	|Nhận dữ liệu từ thiết bị
GET|	/iot/data	|Lấy dữ liệu sensor
GET|	/iot/device/{id}	|Lấy thông tin thiết bị
POST|	/iot/device	|Thêm thiết bị
PUT|	/iot/device/{id}	|Cập nhật thiết bị
DELETE|	/iot/device/{id}	|Xóa thiết bị

## 7. Phụ thuộc service khác

Service này gọi đến:
Auth Service → kiểm tra quyền
Notification Service → gửi cảnh báo
AI Service → phân tích dữ liệu

Service gọi đến IoT Service:
Frontend → hiển thị dữ liệu
Dashboard Service → thống kê
AI Service → lấy dữ liệu

## 8. Biểu đồ Service Boundary

Dưới đây là biểu đồ minh họa Service Boundary của nhóm cho đề tài IoT:

```mermaid
graph TD
    subgraph "IoT Service Boundary (Nhóm kiểm soát)"
        A[Nhận dữ liệu từ IoT Device]
        B[Xử lý dữ liệu (kiểm tra, chuẩn hóa)]
        C[Lưu trữ dữ liệu vào Database]
        D[Cung cấp API truy vấn dữ liệu]
        E[Theo dõi trạng thái thiết bị]
    end
    subgraph "Dịch vụ tích hợp (Nhóm chỉ tích hợp)"
        F[Frontend (Web/App)]
        G[Auth Service (đăng nhập)]
        H[AI Service (phân tích dữ liệu)]
        I[Notification Service (gửi cảnh báo)]
    end
    subgraph "Actors (Đối tượng tương tác)"
        J[User (Người dùng): xem dữ liệu]
        K[Admin: quản lý thiết bị, cấu hình]
        L[IoT Device: gửi dữ liệu sensor]
        M[Service khác (Frontend/AI/Dashboard): gọi API]
    end
    L --> A
    A --> B
    B --> C
    C --> D
    D --> E
    J --> D
    K --> D
    M --> D
    D --> F
    D --> G
    D --> H
    D --> I
```

**Giải thích biểu đồ:**
- **IoT Service Boundary**: Phần mà nhóm kiểm soát và xây dựng, bao gồm quy trình xử lý dữ liệu từ thiết bị IoT.
- **Dịch vụ tích hợp**: Các dịch vụ bên ngoài mà nhóm chỉ tích hợp (không tự xây dựng).
- **Actors**: Các đối tượng tương tác với hệ thống.
- **Luồng tương tác**: Mũi tên cho thấy luồng dữ liệu và tương tác giữa các phần.
