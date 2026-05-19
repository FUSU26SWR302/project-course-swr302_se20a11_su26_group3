# Online Auction Web System (Hệ thống Web Đấu giá Trực tuyến)

🔗 **Jira Task Board:** [Chèn_Link_Jira_Của_Nhóm_Vào_Đây]

## 1. Project Overview
This project is an online auction platform that allows users to list items, place bids in real-time, and securely process payments. 
(Dự án này là nền tảng đấu giá trực tuyến cho phép người dùng đăng sản phẩm, đặt giá thầu theo thời gian thực và thanh toán an toàn.)

## 2. Research By Learning (RBL) Focus
Trong dự án này, nhóm tập trung nghiên cứu và áp dụng các kiến thức chuyên sâu vào các khía cạnh sau (In this project, our RBL focuses on):

* **Thuật toán (Algorithms):** * **Xử lý đồng thời (Concurrency Control):** Thuật toán xử lý tình trạng Race Condition khi nhiều người dùng cùng đặt giá (bid) trong cùng một mili-giây.
  * **Anti-Sniping (Chống bắn tỉa):** Thuật toán tự động gia hạn thời gian đấu giá (ví dụ: thêm 5 phút) nếu có người đặt giá ở những giây cuối cùng.
* **Hệ thống & Kiến trúc (System Architecture):** * **Event-Driven Architecture:** Sử dụng kiến trúc hướng sự kiện để cập nhật trạng thái đấu giá ngay lập tức đến tất cả các client đang theo dõi phiên đấu giá.
  * **Cơ sở dữ liệu (Database Optimization):** Thiết kế SQL database tối ưu cho việc ghi log lịch sử đặt giá thầu với tốc độ cao.
* **Công nghệ (Technologies):** * Nghiên cứu và tích hợp **WebSockets / Socket.io** (để truyền dữ liệu thời gian thực thay vì HTTP request thông thường).
  * Sử dụng **Spring Boot / Java** kết hợp với **Redis** để cache dữ liệu giá thầu, giảm tải cho Database chính.

## 3. Hướng dẫn cài đặt và chạy dự án (Installation & Setup Guide)

### Prerequisites (Yêu cầu môi trường)
- Java 17+ / Node.js
- MySQL / PostgreSQL
- Redis (Optional but recommended for real-time bids)

### Setup Steps (Các bước cài đặt)
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-repo/auction-web.git](https://github.com/your-repo/auction-web.git)
   ```

2. **Thiết lập Cơ sở dữ liệu (Database Setup):**
   * Tạo một database trong MySQL với tên `auction_db`.
   * Chạy các script SQL khởi tạo bảng (nếu có) trong thư mục `/database` hoặc để cấu hình ORM tự động tạo bảng (auto-ddl).

3. **Cấu hình môi trường (Environment Configuration):**
   * Mở file `src/main/resources/application.properties` (hoặc `.yml`).
   * Cấu hình thông tin kết nối Database và Redis:
     ```properties
     spring.datasource.url=jdbc:mysql://localhost:3306/auction_db
     spring.datasource.username=root
     spring.datasource.password=your_password
     
     spring.data.redis.host=localhost
     spring.data.redis.port=6379
     ```

4. **Khởi chạy ứng dụng (Run the Application):**
   * Mở terminal tại thư mục gốc của project và chạy lệnh:
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```
   * Server backend sẽ khởi chạy tại: `http://localhost:8080`

## 4. Tài liệu API (API Documentation)
Sau khi ứng dụng khởi chạy thành công, có thể truy cập tài liệu API (Swagger UI) tại:
👉 `http://localhost:8080/swagger-ui.html`

## 5. Cấu trúc thư mục chính (Main Folder Structure)
```text
src/main/java/com/auction/
├── config/           # Cấu hình WebSocket, Security, Redis
├── controller/       # Các API Endpoints
├── model/            # Thực thể Database (User, Product, Bid...)
├── repository/       # Giao tiếp với Database (Spring Data JPA)
└── service/          # Chứa logic nghiệp vụ (Xử lý đấu giá, tính toán)
```

## 6. Thành viên nhóm (Contributors)
* **[Tuan]** - [DE190463] - Nhiệm vụ: Xử lý CSDL, API Đăng nhập / Backend
* **[Sang]** - [DE190062] - Nhiệm vụ: Thuật toán Real-time Bidding (WebSocket) / Backend
* **[Long]** - [DE190344] - Nhiệm vụ: Thiết kế giao diện / Frontend
* **[Thắng]** - [DE190404] - Nhiệm vụ: Tích hợp thanh toán / API Sản phẩm
* **[Đức]** - [DE191098] - Nhiệm vụ: Viết tài liệu SRS, Tester & Quản lý dự án