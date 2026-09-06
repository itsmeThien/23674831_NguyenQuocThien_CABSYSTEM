# Software Requirements Specification (SRS) - CAB System

## 1. Stakeholder List & Roles (Danh sách & Vai trò Bên liên quan)

| Stakeholder | Vai trò chính |
| :--- | :--- |
| **Ban Giám đốc** | Ra quyết định chiến lược, duyệt ngân sách và phê duyệt các quy tắc nghiệp vụ. |
| **Khách hàng** | Đặt xe, theo dõi chuyến đi, thanh toán và đánh giá chất lượng dịch vụ. |
| **Tài xế** | Bật trạng thái sẵn sàng, nhận/từ chối chuyến và cập nhật tiến trình chuyến đi. |
| **Nhân viên vận hành** | Theo dõi hệ thống, hỗ trợ xử lý sự cố chuyến đi và quản trị dữ liệu. |
| **Business Analyst (BA)** | Làm rõ yêu cầu chưa chốt và chi tiết hóa quy trình nghiệp vụ cho team. |
| **Nhóm Phát triển (Dev/QA)** | Thiết kế kiến trúc, lập trình và hoàn thiện hệ thống trong 7 tuần. |
| **Đối tác Thanh toán & Thông báo** | Tích hợp xử lý giao dịch điện tử và gửi thông báo tức thì đến người dùng. |

---

## 2. Stakeholder Matrix (Ma trận Bên liên quan)

```mermaid
quadrantChart
    title Ma trận Stakeholder (Power vs Interest)
    x-axis "Mức độ quan tâm Thấp" --> "Mức độ quan tâm Cao"
    y-axis "Quyền lực / Ảnh hưởng Thấp" --> "Quyền lực / Ảnh hưởng Cao"
    quadrant-1 "Quản lý chặt chẽ (Manage Closely)"
    quadrant-2 "Thỏa mãn nhu cầu (Keep Satisfied)"
    quadrant-3 "Theo dõi tối thiểu (Monitor)"
    quadrant-4 "Cung cấp thông tin (Keep Informed)"
    
    "Ban Giam doc": [0.85, 0.90]
    "Business Analyst": [0.75, 0.70]
    "Nhom Phat trien": [0.80, 0.60]
    "Doi tac Thanh toan": [0.35, 0.75]
    "Doi tac Thong bao": [0.30, 0.65]
    "Khach hang": [0.85, 0.35]
    "Tai xe": [0.80, 0.30]
    "Nhan vien Van hanh": [0.70, 0.40]
```

---

## 3. Business Goals (Mục tiêu Kinh doanh)

* **BG01:** Tự động hóa quy trình phân công tài xế và tối ưu hóa vận hành nhằm giảm thiểu sự can thiệp thủ công, sẵn sàng mở rộng quy mô hệ thống phục vụ lượng lớn khách hàng và tài xế trong tương lai.
* **BG0c:** Nâng cao doanh thu, tỷ lệ hoàn thành chuyến đi và giảm tỷ lệ hủy chuyến thông qua việc tối ưu cơ chế đề xuất, ghép nối tài xế gần nhất theo thời gian thực.
* **BG03:** Tăng cường trải nghiệm và độ hài lòng của khách hàng bằng việc minh bạch hóa thông tin trạng thái chuyến đi, vị trí tài xế, thời gian dự kiến đến và đa dạng hóa phương thức thanh toán an toàn.
* **BG04:** Tăng hiệu quả hoạt động và thu nhập cho tài xế nhờ cơ chế thông báo nhận chuyến chủ động, minh bạch tiến trình chuyến đi và quy trình hỗ trợ vận hành rõ ràng.
* **BG05:** Nâng cao năng lực quản trị, hỗ trợ và xử lý sự cố kịp thời thông qua hệ thống theo dõi trực quan, phân quyền chặt chẽ và công cụ báo cáo hoạt động chuyên sâu.
* **BG06:** Xây dựng kiến trúc nền tảng ổn định, bảo mật cao, có khả năng mở rộng độc lập và linh hoạt tích hợp/bổ sung các loại hình dịch vụ, đối tác thanh toán hay thông báo mới trong tương lai mà không ảnh hưởng tới hệ thống đang chạy.

---

## 4. Minimum Viable Product (MVP) Modules

1. **Module Quản lý Tài khoản & Định danh (Account & Auth Module):** Đăng ký, đăng nhập, quản lý hồ sơ (Khách hàng, Tài xế) và phân quyền quản trị (Nhân viên vận hành).
2. **Module Đặt xe & Phân công (Booking & Matching Module):** Tạo chuyến, định vị thời gian thực, thuật toán tự động ghép nối/tìm tài xế gần nhất và xử lý chuyển tiếp khi từ chối.
3. **Module Quản lý Tiến trình Chuyến đi (Trip Management Module):** Cập nhật/theo dõi trạng thái chuyến đi theo thời gian thực (ETA, vị trí), lịch sử chuyến và đánh giá tài xế.
4. **Module Tính cước & Thanh toán (Pricing & Payment Module):** Tính tiền tự động, hỗ trợ tiền mặt và tích hợp Payment Gateway bên ngoài xử lý thanh toán điện tử.
5. **Module Thông báo (Notification Module):** Gửi thông báo tức thì cho Khách hàng/Tài xế theo từng sự kiện của chuyến đi.
6. **Module Vận hành & Báo cáo (Admin & Analytics Module):** Giao diện quản trị theo dõi chuyến đi, hỗ trợ xử lý sự cố và xuất báo cáo doanh thu, hiệu suất cho Ban giám đốc.

## 5. Business Requirements

| ID | Business Requirement | Description |
| **BR01** | **Quản lý tài khoản và người dùng** | Hệ thống phải hỗ trợ đăng ký, đăng nhập và quản lý thông tin tài khoản của Khách hàng, Tài xế và Nhân viên vận hành. |
| **BR02** | **Quản lý đặt xe** | Hệ thống phải cho phép Khách hàng tạo yêu cầu đặt xe bằng cách cung cấp điểm đón, điểm đến và phương thức thanh toán. |
| **BR03** | **Tự động phân công tài xế** | Hệ thống phải tự động tìm kiếm và phân công Tài xế phù hợp dựa trên vị trí hiện tại và trạng thái sẵn sàng, ưu tiên Tài xế gần Khách hàng. |
| **BR04** | **Xử lý từ chối chuyến** | Khi Tài xế từ chối hoặc không phản hồi yêu cầu chuyến đi, hệ thống phải tự động chuyển yêu cầu cho Tài xế phù hợp tiếp theo. |
| **BR05** | **Quản lý tiến trình chuyến đi** | Hệ thống phải quản lý và cập nhật trạng thái chuyến đi từ khi tạo yêu cầu, tìm Tài xế, đón khách, thực hiện chuyến cho đến khi hoàn thành hoặc hủy. |
| **BR06** | **Theo dõi vị trí và ETA** | Hệ thống phải cung cấp vị trí của Tài xế và thời gian dự kiến đến (ETA) để Khách hàng có thể theo dõi chuyến đi theo thời gian thực. |
| **BR07** | **Tính cước chuyến đi** | Hệ thống phải tự động tính giá chuyến đi dựa trên các quy tắc tính cước do doanh nghiệp thiết lập. |
| **BR08** | **Quản lý thanh toán** | Hệ thống phải hỗ trợ thanh toán bằng tiền mặt và thanh toán điện tử thông qua Payment Gateway. |
| **BR09** | **Quản lý thông báo** | Hệ thống phải gửi thông báo đến Khách hàng và Tài xế khi xảy ra các sự kiện quan trọng như nhận chuyến, tài xế đến, bắt đầu chuyến, hoàn thành hoặc hủy chuyến. |
| **BR10** | **Đánh giá dịch vụ** | Hệ thống phải cho phép Khách hàng đánh giá chất lượng chuyến đi và Tài xế sau khi chuyến đi hoàn thành. |
| **BR11** | **Quản lý lịch sử chuyến đi** | Hệ thống phải lưu trữ và cho phép Khách hàng tra cứu lịch sử đặt xe, chuyến đi và thanh toán. |
| **BR12** | **Giám sát và hỗ trợ vận hành** | Hệ thống phải cung cấp công cụ để Nhân viên vận hành theo dõi các chuyến đi đang hoạt động và hỗ trợ xử lý các sự cố phát sinh. |
| **BR13** | **Quản lý dữ liệu và phân quyền** | Hệ thống phải đảm bảo dữ liệu được quản lý tập trung và người dùng chỉ được truy cập các chức năng, dữ liệu phù hợp với vai trò được cấp. |
| **BR14** | **Báo cáo kinh doanh** | Hệ thống phải cung cấp báo cáo về doanh thu, số lượng chuyến, tỷ lệ hoàn thành, tỷ lệ hủy chuyến và hiệu suất hoạt động của Tài xế. |
| **BR15** | **Khả năng mở rộng hệ thống** | Hệ thống phải có khả năng mở rộng để đáp ứng số lượng Khách hàng, Tài xế và chuyến đi ngày càng tăng trong tương lai. |
| **BR16** | **Tích hợp đối tác bên ngoài** | Hệ thống phải hỗ trợ tích hợp với các đối tác thanh toán và thông báo bên ngoài để phục vụ hoạt động kinh doanh. |
