# SOFTWARE ARCHITECTURE DOCUMENT (SAD)
## TÀI LIỆU KIẾN TRÚC PHẦN MỀM

**Tên hệ thống:** [Tên sản phẩm]  
**Phiên bản:** 1.0  
**Ngày cập nhật:** [DD/MM/YYYY]  
**Trạng thái:** Draft / In Review / Approved  
**Phạm vi:** Đồ án học phần – thời gian phát triển dự kiến 3–4 tuần.

---

# PHẦN I. TỔNG QUAN VÀ BỐI CẢNH HỆ THỐNG

## 1. Giới thiệu
- Mục đích xây dựng tài liệu SAD.
- Mục tiêu và phạm vi của sản phẩm.
- Đối tượng sử dụng tài liệu.

## 2. Bối cảnh và mục tiêu hệ thống
- Bài toán cần giải quyết.
- Mục tiêu chính của sản phẩm.
- Các chức năng và khả năng cốt lõi.

## 3. Tổng quan kiến trúc
- Mô hình kiến trúc tổng thể.
- Sơ đồ C4 – Level 1: System Context.
- Sơ đồ C4 – Level 2: Container.
- Mối quan hệ giữa các thành phần chính.

## 4. Công nghệ sử dụng (Technology Stack)
- Backend: **Python (bắt buộc)**.
- Database: **PostgreSQL (bắt buộc)**.
- Frontend: [Công nghệ đề xuất].
- Thư viện xử lý dữ liệu và phân tích.
- Công cụ phát triển, quản lý mã nguồn và triển khai.

---

# PHẦN II. KIẾN TRÚC VÀ THÀNH PHẦN PHẦN MỀM

## 5. Kiến trúc hạ tầng và triển khai (Infrastructure & Deployment)
- Mô hình triển khai tổng thể.
- Môi trường phát triển và vận hành.
- Phương án kết nối giữa các thành phần.

## 6. Thành phần hệ thống (Container / Component / Client)
Mô tả trách nhiệm và chức năng của từng thành phần:

| Thành phần | Trách nhiệm chính |
|---|---|
| T1 – Data Ingestion | Tiếp nhận và thu thập dữ liệu |
| T2 – Data Analysis | Phân tích dữ liệu chuỗi thời gian |
| T3 – Clustering | Phân nhóm dữ liệu |
| T4 – Prediction | Dự đoán dữ liệu |
| T5 – Database API | Cung cấp API truy xuất dữ liệu |
| T6 – Frontend Client | Giao diện tương tác với người dùng |

## 7. Giao tiếp và tích hợp API
- Các API chính giữa Frontend và Backend.
- Phương thức giao tiếp giữa các thành phần.
- Quy ước dữ liệu đầu vào và đầu ra.
- Nguyên tắc xử lý lỗi giao tiếp.

## 8. Kiến trúc dữ liệu (Data Architecture)
- Nguồn dữ liệu đầu vào.
- Quy trình tiếp nhận và xử lý dữ liệu.
- Cách tổ chức, lưu trữ và truy xuất dữ liệu.
- Quan hệ giữa các nhóm dữ liệu chính.

## 9. Kiến trúc sự kiện và xử lý định kỳ (Events & Scheduling)
- Các tác vụ xử lý tự động.
- Chu kỳ thực thi dự kiến:
  - Data Ingestion: 5 phút.
  - Data Analysis: 5 phút.
  - Clustering: 1 ngày.
  - Prediction: 5 phút.
- Cơ chế kích hoạt, theo dõi và xử lý tác vụ.

---

# PHẦN III. LUỒNG XỬ LÝ VÀ NGHIỆP VỤ

## 10. Luồng nghiệp vụ chính (Business Flows)
- Luồng thu thập dữ liệu.
- Luồng phân tích và xử lý dữ liệu.
- Luồng phân nhóm và dự đoán.
- Luồng truy xuất và hiển thị kết quả.

## 11. Luồng dữ liệu (Data Flows)
- Dữ liệu đi qua các thành phần như thế nào.
- Các bước biến đổi dữ liệu.
- Điểm lưu trữ dữ liệu.
- Kết quả đầu ra của từng giai đoạn.

## 12. Các phương pháp phân tích dữ liệu
Định hướng hỗ trợ 6 nhóm phân tích chính:

| Mã | Phương pháp | Nội dung |
|---|---|---|
| P-01 | Temporal Visualization | Trực quan hóa dữ liệu theo thời gian |
| P-02 | Trend Analysis | Phân tích xu hướng |
| P-03 | Seasonality Analysis | Phân tích tính mùa vụ |
| P-04 | Correlation Analysis | Phân tích tương quan |
| P-05 | Regression & Forecasting | Hồi quy và dự báo |
| P-06 | Classification | Phân loại dữ liệu |

## 13. Tích hợp và phụ thuộc (Integrations & Dependencies)
- Các dịch vụ hoặc nguồn dữ liệu bên ngoài.
- Thư viện và thành phần phụ thuộc.
- Quan hệ phụ thuộc giữa các module.
- Giới hạn và ràng buộc tích hợp.

---

# PHẦN IV. BẢO MẬT VÀ QUẢN LÝ TRUY CẬP

## 14. Xác thực và phân quyền (Authentication & Authorization)
- Cơ chế xác thực người dùng.
- Vai trò và quyền truy cập.
- Phạm vi bảo vệ API.

## 15. Bảo mật dữ liệu và hệ thống
- Bảo vệ thông tin kết nối và cấu hình.
- Kiểm soát truy cập cơ sở dữ liệu.
- Kiểm tra và xác thực dữ liệu đầu vào.
- Các nguyên tắc bảo mật cơ bản.

---

# PHẦN V. YÊU CẦU PHI CHỨC NĂNG

## 16. Hiệu năng và khả năng mở rộng (Performance & Scalability)
- Thời gian phản hồi dự kiến.
- Khả năng xử lý dữ liệu định kỳ.
- Định hướng mở rộng khi khối lượng dữ liệu tăng.

## 17. Độ tin cậy và xử lý lỗi (Resilience & Error Handling)
- Xử lý lỗi trong quá trình thu thập và phân tích.
- Cơ chế ghi nhận trạng thái tác vụ.
- Nguyên tắc hạn chế mất hoặc xử lý trùng dữ liệu.

## 18. Khả năng bảo trì và phát triển
- Nguyên tắc tổ chức mã nguồn.
- Phân tách trách nhiệm giữa các thành phần.
- Khả năng kiểm thử và thay thế module.

## 19. Cấu hình và quản lý môi trường (Configuration)
- Quản lý biến môi trường.
- Cấu hình kết nối cơ sở dữ liệu.
- Phân biệt môi trường phát triển và triển khai.

---

# PHẦN VI. VẬN HÀNH, KIỂM THỬ VÀ GIÁM SÁT

## 20. CI/CD và quy trình phát triển
- Quy ước quản lý mã nguồn.
- Quy trình tích hợp và kiểm tra mã.
- Định hướng tự động hóa triển khai phù hợp quy mô đồ án.

## 21. Chiến lược kiểm thử (Testing)
- Unit Testing.
- Integration Testing.
- API Testing.
- Kiểm thử luồng xử lý dữ liệu chính.

## 22. Giám sát và ghi nhật ký (Observability & Logging)
- Ghi nhận hoạt động hệ thống.
- Theo dõi trạng thái các tác vụ định kỳ.
- Ghi nhận và truy vết lỗi.

## 23. Sao lưu và khôi phục dữ liệu (Backup & Recovery)
- Phương án sao lưu PostgreSQL.
- Định hướng khôi phục dữ liệu khi xảy ra sự cố.

## 24. Chi phí và giới hạn triển khai (Cost & Constraints)
- Chi phí hạ tầng và công cụ.
- Giới hạn tài nguyên.
- Các giới hạn kỹ thuật và phạm vi đồ án.

## 25. Kết luận và định hướng phát triển
- Tổng kết phương án kiến trúc được lựa chọn.
- Các nội dung cần tiếp tục nghiên cứu.
- Những hạng mục có thể mở rộng sau đồ án.

---

# PHỤ LỤC

## A. Architectural Decisions
Ghi nhận các quyết định kiến trúc quan trọng:

| ID | Quyết định | Lý do | Trạng thái |
|---|---|---|---|
| ADR-01 | Sử dụng Python cho Backend | Ràng buộc bắt buộc | Accepted |
| ADR-02 | Sử dụng PostgreSQL cho Database | Ràng buộc bắt buộc | Accepted |
| ADR-03 | [Quyết định khác] | [Lý do] | Proposed |

## B. Các vấn đề cần xác nhận
Liệt kê những thông tin chưa đủ cơ sở để quyết định, tránh tự giả định trong quá trình thiết kế.

## C. Tài liệu tham khảo
- Tài liệu yêu cầu hệ thống.
- Tài liệu công nghệ và thư viện.
- Tài liệu thiết kế liên quan.

---

# PHÊ DUYỆT TÀI LIỆU

| Vai trò | Người phụ trách | Trạng thái |
|---|---|---|
| Người xây dựng tài liệu | [Tên] | Pending |
| Người đánh giá kỹ thuật | [Tên] | Pending |
| Giảng viên hướng dẫn | [Tên] | Pending |

**Trạng thái phê duyệt:** Pending Approval

**Điều kiện phê duyệt:**
- Phạm vi và mục tiêu hệ thống được xác định rõ.
- Kiến trúc tổng thể và trách nhiệm các thành phần được thống nhất.
- Python và PostgreSQL được xác định là công nghệ bắt buộc.
- Luồng dữ liệu và các phương pháp xử lý chính được mô tả.
- Không còn quyết định kiến trúc quan trọng chưa được làm rõ hoặc có người chịu trách nhiệm xác nhận.

**Lưu ý:** Tài liệu SAD này định hướng kiến trúc và phát triển sản phẩm. Không yêu cầu mô tả chi tiết từng API, câu lệnh SQL, thuật toán, mã nguồn hoặc quy trình triển khai ở mức hướng dẫn thực thi.