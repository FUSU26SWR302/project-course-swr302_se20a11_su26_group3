[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/XTdeRLoD)
# Online Auction Web System (Hệ thống Web Đấu giá Trực tuyến)

🔗 **Jira Task Board:** [Chèn_Link_Jira_Của_Nhóm_Vào_Đây / Insert_Jira_Link_Here]

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
    * Sử dụng **Spring Boot / Java** (hoặc framework tương ứng của nhóm) kết hợp với **Redis** để cache dữ liệu giá thầu, giảm tải cho Database chính.

## 3. Hướng dẫn cài đặt và chạy dự án (Installation & Setup Guide)

### Prerequisites (Yêu cầu môi trường)
- Java 17+ / Node.js (Tuỳ stack nhóm chọn)
- MySQL / PostgreSQL
- Redis (Optional but recommended for real-time bids)

### Setup Steps (Các bước cài đặt)
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-repo/auction-web.git](https://github.com/your-repo/auction-web.git)