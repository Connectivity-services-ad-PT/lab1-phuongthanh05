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

## 8. Sơ đồ Service Boundary Diagram

```mermaid
graph TD
    subgraph Actors["Actors (Đối tượng tương tác)"]
        J["👤 User<br/>(Xem dữ liệu)"]
        K["👨‍💼 Admin<br/>(Quản lý thiết bị)"]
        L["📱 IoT Device<br/>(Gửi dữ liệu)"]
        M["🔗 Service khác<br/>(Frontend/AI/Dashboard)"]
    end
    
    subgraph Boundary["🔷 IoT Service Boundary (Nhóm kiểm soát)"]
        A["1️⃣ Nhận dữ liệu từ IoT Device"]
        B["2️⃣ Xử lý dữ liệu<br/>(kiểm tra, chuẩn hóa)"]
        C["3️⃣ Lưu trữ dữ liệu<br/>vào Database"]
        D["4️⃣ Cung cấp API<br/>truy vấn dữ liệu"]
        E["5️⃣ Theo dõi<br/>trạng thái thiết bị"]
    end
    
    subgraph Integration["🟨 Dịch vụ tích hợp (Nhóm chỉ tích hợp)"]
        F["🖥️ Frontend<br/>(Web/App)"]
        G["🔐 Auth Service<br/>(Đăng nhập)"]
        H["🤖 AI Service<br/>(Phân tích dữ liệu)"]
        I["🔔 Notification Service<br/>(Gửi cảnh báo)"]
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
    
    style Boundary fill:#87CEEB,stroke:#0066cc,stroke-width:3px,color:#000
    style Integration fill:#FFD700,stroke:#ff9900,stroke-width:2px,color:#000
    style Actors fill:#D3D3D3,stroke:#666,stroke-width:2px,color:#000
```

**Giải thích biểu đồ:**
- **Actors (xám)**: Các đối tượng tương tác với hệ thống từ bên ngoài.
- **IoT Service Boundary (xanh)**: Phần mà nhóm kiểm soát và xây dựng, bao gồm 5 bước xử lý dữ liệu.
- **Dịch vụ tích hợp (vàng)**: Các service bên ngoài mà nhóm tích hợp nhưng không tự xây dựng.
- **Luồng dữ liệu**: Mũi tên thể hiện hướng truyền dữ liệu từ IoT Device → xử lý → lưu trữ → cung cấp API → các service khác.

**Link Lucidchart**: https://lucid.app/lucidchart/3ebb9a7f-307a-4b4d-af3f-fe2e5d2b4d0c
