# Hệ thống Web Đấu giá Trực tuyến (Online Auction Web System)

Dự án phần mềm nền tảng đấu giá trực tuyến cho phép người dùng đăng sản phẩm, đặt giá thầu theo thời gian thực và thanh toán an toàn, tích hợp trí tuệ nhân tạo và hệ thống lập lịch tự động nhằm số hóa toàn bộ quy trình mua bán minh bạch.

## 1. Thành viên nhóm

| STT | Họ và Tên | Mã Sinh Viên | Phân công công việc |
|---|---|---|---|
| 1 | **Tuan** | DE190463 | Xử lý CSDL, API Đăng nhập / Backend. |
| 2 | **Sang** | DE190062 | Xây dựng thuật toán Real-time Bidding (WebSocket) / Backend. |
| 3 | **Long** | DE190344 | Thiết kế giao diện / Frontend. |
| 4 | **Thắng** | DE190404 | Tích hợp cổng thanh toán / API Sản phẩm. |
| 5 | **Đức** | DE191098 | Viết tài liệu đặc tả (SRS), kiểm thử phần mềm (Tester) & Quản lý dự án. |

---

## 2. Tổng quan Dự án

### 2.1. Phân hệ Nghiệp vụ cốt lõi (Business Scope)
* **Quy trình vận hành khép kín:** Số hóa toàn bộ vòng đời của một phiên đấu giá từ lúc người bán yêu cầu tạo phiên, duyệt sản phẩm, người mua đóng tiền cọc, tham gia phòng đấu giá, cho đến khi chốt đơn và thanh toán.
* **Quản lý Định danh & KYC:** Yêu cầu người dùng xác minh danh tính (KYC) nhiều bước thông qua giấy tờ tùy thân trước khi được cấp quyền tham gia mua hoặc bán, đảm bảo tính minh bạch và an toàn của sàn giao dịch.
* **Quản trị Tài chính & Ví điện tử (E-Wallet):** Tích hợp ví điện tử cá nhân cho phép nạp/rút tiền, tự động đóng băng (hold) khoản cọc khi vào phòng đấu và hoàn cọc (refund) hoặc tất toán (settle) hoàn toàn tự động.

### 2.2. Hàm lượng Nghiên cứu Khoa học & Công nghệ (Research Depth)
* **Xử lý Đồng thời (Concurrency Control):** Thuật toán xử lý tình trạng Race Condition khi nhiều người dùng cùng đặt giá (bid) trong cùng một mili-giây, kết hợp Redis để cache dữ liệu tốc độ cao.
* **Thuật toán Chống bắn tỉa (Anti-Sniping):** Tự động phát hiện và gia hạn thêm thời gian cho phiên đấu giá nếu có người dùng đặt giá ở những giây cuối cùng, đảm bảo công bằng cho mọi người tham gia.
* **Tích hợp Trí tuệ Nhân tạo (AI Evaluation):** Ứng dụng AI phân tích hình ảnh và mô tả để tự động đưa ra các đề xuất về giá trị sản phẩm, hỗ trợ người bán định giá khởi điểm.
* **Cơ chế Hướng sự kiện (Event-Driven Architecture):** Tích hợp WebSockets/Socket.io để truyền tải dữ liệu giá thầu và trạng thái phòng đấu giá theo thời gian thực tới toàn bộ client thay vì dùng HTTP request truyền thống.

---

## 3. Các Tính năng Chính theo Nhóm Người dùng (Key Features)

### 3.1. Guest (Khách vãng lai)
* **Khám phá hệ thống:** Duyệt danh sách các phiên đấu giá công khai, xem thông tin chung và chi tiết sản phẩm.
* **Đăng ký / Đăng nhập:** Tạo tài khoản mới thông qua hệ thống định danh cơ bản hoặc Google/Facebook để trở thành Member.

### 3.2. Member (Thành viên hệ thống)
* **Quản lý hồ sơ:** Cập nhật thông tin cá nhân, địa chỉ, ảnh đại diện và thông tin liên lạc.
* **Xác minh danh tính (KYC):** Tải lên các tài liệu tùy thân để hệ thống xét duyệt trước khi tham gia các hoạt động tài chính.
* **Quản lý Ví điện tử:** Truy cập bảng điều khiển ví (Wallet Dashboard), kiểm tra số dư, nạp tiền (Deposit) và yêu cầu rút tiền (Withdrawal).

### 3.3. Buyer (Người mua - Đã KYC)
* **Đăng ký tham gia & Đặt cọc:** Ghi danh vào các phiên đấu giá sắp tới và thanh toán khoản tiền cọc bắt buộc để giữ chỗ.
* **Phòng đấu giá trực tiếp:** Tham gia phòng đấu giá thời gian thực, liên tục cập nhật giá thầu (Place Bid) cạnh tranh với các người mua khác.
* **Thanh toán & Nhận hàng:** Thực hiện tất toán số tiền còn lại của đơn hàng qua cổng thanh toán sau khi thắng thầu.

### 3.4. Seller (Người bán - Đã KYC)
* **Khởi tạo phiên đấu giá:** Gửi yêu cầu đăng bán sản phẩm, cung cấp chi tiết hình ảnh, giá khởi điểm, bước giá và thực hiện ký cam kết số.
* **Sử dụng AI Định giá:** Nhận đánh giá và gợi ý mức giá khởi điểm tự động từ hệ thống AI dựa trên dữ liệu sản phẩm.
* **Giám sát phiên đấu giá:** Theo dõi trực tiếp diễn biến đặt giá thầu, người trả giá cao nhất và kiểm tra trạng thái thanh toán giải ngân sau sự kiện.

### 3.5. Staff (Nhân viên Kiểm duyệt)
* **Xét duyệt sản phẩm:** Rà soát, phê duyệt hoặc từ chối các yêu cầu tạo phiên đấu giá từ Seller.
* **Kiểm duyệt hồ sơ & Tài chính:** Đánh giá hồ sơ KYC, rà soát và phê duyệt các yêu cầu rút tiền về ngân hàng để phòng chống gian lận.
* **Hỗ trợ khách hàng:** Xử lý các vé hỗ trợ (Support tickets), giải đáp thắc mắc và khắc phục sự cố cho người dùng.

### 3.6. Admin (Quản trị viên hệ thống)
* **Cấu hình Luật đấu giá:** Thiết lập các thông số hệ thống cốt lõi như thời gian Anti-Sniping, bước giá tối thiểu, tỷ lệ phần trăm đặt cọc và hoa hồng nền tảng.
* **Quản lý Tài khoản & Phân quyền:** Khóa, mở khóa tài khoản, thiết lập vai trò (Roles) và cấp quyền truy cập cho nhân viên Staff.
* **Giải quyết Tranh chấp:** Đóng vai trò trọng tài xử lý các vấn đề leo thang giữa Người mua và Người bán (hàng giả, từ chối nhận hàng).
* **Báo cáo & Thống kê:** Theo dõi nhật ký kiểm toán (Audit logs), xuất báo cáo doanh thu và phân tích hiệu suất hệ thống.

### 3.7. Phân hệ Scheduler & Payment Gateway (Tự động hóa)
* **Automated Scheduler:** Tiến trình chạy ngầm tự động kích hoạt phiên đấu giá khi đến giờ, đóng phiên khi hết hạn, chốt kết quả và gọi lệnh hoàn cọc tự động cho những người không thắng thầu.
* **Payment Gateway:** Xử lý giao dịch bảo mật qua VNPay/Stripe cho các thao tác nạp tiền và thanh toán đơn hàng cuối.

---

## 4. Quản lý Tiến độ Công việc (Jira)

Toàn bộ các đầu việc và tiến độ của dự án được quản lý nghiêm ngặt theo mô hình Agile/Scrum.
* **Đường dẫn Jira Board:** [Hệ thống Quản lý Dự án - Jira](https://lsang9494.atlassian.net/jira/software/projects/SCRUM/boards/1)
* **Workflow chuẩn hóa:** `To Do` -> `In Progress` -> `Review` -> `Done`. Các tác vụ được phân công rõ ràng cho từng thành viên (Backend, Frontend, BA) kèm theo thời hạn hoàn thành (Sprint).

---

## 5. Thiết kế Kiến trúc & Cấu trúc Mã nguồn
**Đường dẫn UI figma** [UI design - Figma](https://www.figma.com/design/ESrHd6EHbKn58RLffheDzb/Auction-Online?node-id=0-1&t=gm0KEJMdO2vs1IIL-1)
Hệ thống được phát triển theo kiến trúc Layered Architecture kết hợp Event-Driven. Cấu trúc thư mục nguồn Backend (Java/Spring Boot) được tổ chức tối ưu cho việc bảo trì:
---

## 6. Kho lưu trữ Mã nguồn (Repositories)

Hệ thống được phát triển theo cấu trúc phân tách rõ ràng giữa giao diện và máy chủ, quản lý mã nguồn độc lập qua 2 repository để tối ưu hóa quá trình phát triển và triển khai (CI/CD):

* **Frontend Repository:** [auction-web-frontend](https://github.com/tuan190605/auction-web-frontend.git)
* **Backend Repository:** [auction-web-backend](https://github.com/tuan190605/auction-web-backend.git)

---

## 7. Overleaf 
* **Over leaf link** [overleaf](https://www.overleaf.com/4388332974mwtpqwkrgdnd#4bbf5b)
https://www.overleaf.com/4388332974mwtpqwkrgdnd#4bbf5b

---

```text
src/main/java/com/auction/
├── config/           # Cấu hình WebSocket, Spring Security, Redis Cache, Payment Gateway
├── controller/       # Các API Endpoints (Auth, Auction, Wallet, Product, Bidding)
├── model/            # Thực thể Database (Users, Products, Auctions, Bids, Wallets...)
├── repository/       # Tầng giao tiếp với Cơ sở dữ liệu (Spring Data JPA)
├── service/          # Tầng Business Logic (Xử lý luật đấu giá, xử lý giao dịch, thuật toán)
└── utils/            # Các hàm hỗ trợ (Mã hóa MD5, định dạng thời gian, xử lý file)

