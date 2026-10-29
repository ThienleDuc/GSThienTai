# KẾ HOẠCH THIẾT KẾ VÀ CHUẨN BỊ KỸ THUẬT HỆ THỐNG (3 TUẦN)

## 1. Mục tiêu

Xây dựng tài liệu thiết kế kỹ thuật, chuẩn hóa các luồng nghiệp vụ cốt lõi và chuẩn bị môi trường phát triển trước khi bước vào giai đoạn Coding toàn diện.

Kế hoạch hướng đến một sản phẩm phục vụ nhu cầu học tập, có định hướng phát triển theo tiêu chuẩn chuyên nghiệp nhưng giới hạn phạm vi ở mức hợp lý, ưu tiên tính đơn giản, khả năng bảo trì và tốc độ phát triển.

### Nguyên tắc thực hiện

- Ưu tiên thiết kế đủ dùng (Just Enough Design), tránh thiết kế quá mức cần thiết.
- Giữ nguyên 21 tiêu chí kỹ thuật, điều chỉnh độ sâu theo quy mô dự án.
- Ưu tiên kiến trúc đơn giản, dễ triển khai và bảo trì.
- Chỉ sử dụng công nghệ nâng cao khi có nhu cầu thực tế.
- Mỗi hạng mục cần có sản phẩm đầu ra cụ thể.
- Các quyết định quan trọng phải được ghi nhận và có thể xem xét lại.
- Cho phép hoàn thiện những chi tiết ít rủi ro trong quá trình phát triển.

### Phạm vi kỹ thuật mặc định

- Kiến trúc: Modular Monolith.
- Giao tiếp: REST API.
- Database: Một cơ sở dữ liệu chính phù hợp với nghiệp vụ.
- Frontend: SPA hoặc kiến trúc phù hợp với sản phẩm.
- Authentication và Authorization: Cơ chế xác thực phù hợp, kết hợp phân quyền theo vai trò và quyền sở hữu tài nguyên khi cần.
- Container: Docker Compose cho môi trường phát triển nếu sử dụng Docker.
- CI/CD: Tự động kiểm tra, chạy test và build; triển khai tự động khi cần.
- Testing: Unit Test, Integration Test và một số E2E Test cho luồng cốt lõi.
- Observability: Logging và Health Check cơ bản.
- Caching, Message Queue và các thành phần hạ tầng nâng cao chỉ được bổ sung khi có nhu cầu rõ ràng.

---

# TUẦN 1: SCOPE, CONTEXT & HIGH-LEVEL ARCHITECTURE

**Mục tiêu:** Xác định phạm vi bài toán, yêu cầu nghiệp vụ và kiến trúc tổng thể trước khi thiết kế chi tiết.

## 0. Template & Metadata

- [ ] Tạo `_template.md` để chuẩn hóa tài liệu kỹ thuật.
- [ ] Thống nhất metadata: Tác giả, Ngày tạo, Phiên bản và Trạng thái.
- [ ] Sử dụng các trạng thái `Draft`, `In Review`, `Approved`.

**Đầu ra:** Template tài liệu dùng chung.

## 1. Tổng quan dự án, Scope & Yêu cầu phi chức năng (NFRs)

- [ ] Mô tả mục tiêu, đối tượng sử dụng và vấn đề cần giải quyết.
- [ ] Xác định phạm vi `In-scope` và `Out-of-scope`.
- [ ] Liệt kê các chức năng cốt lõi.
- [ ] Xác định các NFR quan trọng: hiệu năng cơ bản, bảo mật, khả năng bảo trì và tính ổn định.
- [ ] Ghi nhận giả định, ràng buộc và các vấn đề chưa được xác nhận.

**Đầu ra:** `project-overview.md`, `requirements.md`, `nfr.md`.

**Giới hạn:** Không đặt các chỉ số RPS, p99 latency hoặc SLA phức tạp nếu không có yêu cầu và cơ sở đo lường phù hợp.

## 2. Phân tích nghiệp vụ cốt lõi (Business Analysis)

- [ ] Xác định Actor và ma trận phân quyền chức năng.
- [ ] Xây dựng Use Case cho các chức năng chính.
- [ ] Mô tả Business Flow và các trường hợp ngoại lệ quan trọng.
- [ ] Xác định các quy tắc nghiệp vụ (Business Rules).
- [ ] Xây dựng Acceptance Criteria cho chức năng cốt lõi.
- [ ] Lập bảng truy vết đơn giản từ yêu cầu đến Use Case và Test Case.

**Đầu ra:** `use-cases.md`, `business-flows/`, `acceptance-criteria.md`.

**Giới hạn:** Chỉ sử dụng BPMN hoặc Activity Diagram cho các luồng thực sự cần thiết.

## 3. Ngữ cảnh hệ thống (System Context)

- [ ] Xây dựng C4 Level 1 — System Context Diagram.
- [ ] Xây dựng C4 Level 2 — Container Diagram.
- [ ] Xác định người dùng, ứng dụng, database và hệ thống bên ngoài nếu có.
- [ ] Xác định ranh giới và trách nhiệm của từng thành phần.

**Đầu ra:** Sơ đồ kiến trúc tổng thể và tài liệu mô tả.

**Giới hạn:** Chưa cần C4 Level 3 hoặc Deployment Diagram chi tiết nếu hệ thống đơn giản.

## 4. Công nghệ sử dụng, Container Architecture & Development Standards

- [ ] Chốt Tech Stack cho Frontend, Backend và Database.
- [ ] Xác định kiến trúc triển khai ứng dụng.
- [ ] Tạo `Dockerfile` và `docker-compose.yml` nếu sử dụng Docker.
- [ ] Thống nhất quy ước đặt tên, Linter, Formatter và cấu trúc mã nguồn.
- [ ] Chọn Git Flow hoặc Trunk-based Development.
- [ ] Thống nhất quy ước Commit Message, ưu tiên Conventional Commits nếu phù hợp.

**Đầu ra:** Tài liệu Tech Stack, cấu hình môi trường phát triển và quy chuẩn code.

**Giới hạn:** Không triển khai Kubernetes, Service Mesh hoặc hạ tầng phân tán nâng cao khi chưa có nhu cầu.

## 5. Cấu hình & Quản lý Môi trường

- [ ] Phân biệt môi trường Local và Dev; bổ sung Staging hoặc Production khi cần.
- [ ] Tạo `.env.example`.
- [ ] Xác định các biến môi trường bắt buộc.
- [ ] Quy định cách quản lý thông tin nhạy cảm và Secret.
- [ ] Thống nhất cách cấu hình và khởi chạy dự án.

**Đầu ra:** Tài liệu cấu hình môi trường và hướng dẫn khởi chạy.

**Giới hạn:** Chưa cần Vault hoặc dịch vụ quản lý Secret chuyên dụng cho đồ án nhỏ.

## 6. ADR — Architecture Decision Records

- [ ] Tạo thư mục `docs/adr/`.
- [ ] Ghi nhận các quyết định kiến trúc quan trọng.
- [ ] Mô tả bối cảnh, phương án lựa chọn, lý do và đánh đổi.
- [ ] Ghi nhận các giả định hoặc điều kiện có thể khiến quyết định phải thay đổi.

**Đầu ra:** Các ADR cho kiến trúc tổng thể, database, framework và cách tổ chức module.

**Giới hạn:** Chỉ ghi ADR cho các quyết định có ảnh hưởng đáng kể.

### Cổng kiểm tra cuối tuần 1

- [ ] Phạm vi và chức năng cốt lõi đã được xác định.
- [ ] Các Actor và quy tắc nghiệp vụ chính đã rõ ràng.
- [ ] NFR quan trọng đã được xác định hoặc có kế hoạch làm rõ.
- [ ] Kiến trúc tổng thể và Tech Stack đã được thống nhất.
- [ ] Các rủi ro và giả định quan trọng đã được ghi nhận.

---

# TUẦN 2: DETAILED APPLICATION DESIGN

**Mục tiêu:** Thiết kế dữ liệu, module, API và các luồng tương tác đủ chi tiết để bắt đầu triển khai các chức năng cốt lõi.

## 7. Model & Schema (ERD & State Machine)

- [ ] Thiết kế ERD cho các thực thể chính.
- [ ] Xác định Primary Key, Foreign Key và các ràng buộc dữ liệu.
- [ ] Xây dựng Data Dictionary cho các bảng quan trọng.
- [ ] Xác định trạng thái và quy tắc chuyển trạng thái cho các thực thể có vòng đời phức tạp.
- [ ] Xác định các thao tác cần bảo đảm tính nhất quán dữ liệu.
- [ ] Xác định các chỉ mục cơ bản dựa trên truy vấn quan trọng.

**Đầu ra:** ERD, Data Dictionary và State Machine Diagram khi cần.

**Giới hạn:** Chưa cần tối ưu hóa database chuyên sâu khi chưa có dữ liệu đo lường.

## 8. Kiến trúc Module & Cấu trúc thư mục

- [ ] Ưu tiên Modular Monolith nếu phù hợp với quy mô.
- [ ] Xác định module và trách nhiệm của từng module.
- [ ] Quy định cách các module tương tác.
- [ ] Xác định quy tắc phụ thuộc để hạn chế liên kết chéo.
- [ ] Xây dựng cấu trúc thư mục Frontend và Backend.

**Đầu ra:** `architecture/modules.md` và cấu trúc thư mục dự kiến.

**Giới hạn:** Không bắt buộc triển khai đầy đủ Clean Architecture hoặc Hexagonal Architecture ở mọi lớp.

## 9. Xác thực & Phân quyền chi tiết (Auth & Authorization)

- [ ] Xác định luồng đăng ký, đăng nhập và đăng xuất nếu có.
- [ ] Chọn cơ chế Authentication phù hợp.
- [ ] Nếu sử dụng JWT, xác định thời hạn Access Token và cách quản lý Refresh Token.
- [ ] Xác định quyền theo vai trò và quyền sở hữu tài nguyên.
- [ ] Xác định cách xử lý truy cập trái phép.
- [ ] Xây dựng các trường hợp kiểm thử phân quyền quan trọng.

**Đầu ra:** Tài liệu Authentication, Authorization và ma trận phân quyền.

**Giới hạn:** Ưu tiên RBAC kết hợp kiểm tra quyền sở hữu tài nguyên; chưa cần ABAC hoặc hệ thống IAM riêng.

## 10. Kiến trúc API & Data Contracts

- [ ] Thống nhất quy ước thiết kế REST API.
- [ ] Xác định Endpoint, HTTP Method và Request/Response Payload.
- [ ] Chuẩn hóa định dạng phản hồi thành công và lỗi.
- [ ] Xác định Validation và Authorization cho các API quan trọng.
- [ ] Xây dựng OpenAPI/Swagger Specification.
- [ ] Xác định cách xử lý các trường hợp dữ liệu không hợp lệ hoặc tài nguyên không tồn tại.

**Đầu ra:** `openapi.yaml` hoặc tài liệu Swagger tương đương.

**Giới hạn:** Chưa cần GraphQL, gRPC hoặc hệ thống quản lý phiên bản API phức tạp nếu không có nhu cầu.

## 11. Sơ đồ tuần tự (Sequence Diagrams)

- [ ] Xây dựng Sequence Diagram cho 3–5 luồng nghiệp vụ quan trọng.
- [ ] Thể hiện tương tác giữa Frontend, Backend, Database và dịch vụ ngoài nếu có.
- [ ] Bổ sung các trường hợp lỗi hoặc ngoại lệ có ảnh hưởng đáng kể.

**Đầu ra:** Bộ Sequence Diagram cho các luồng cốt lõi.

**Giới hạn:** Không cần sơ đồ riêng cho mọi API CRUD thông thường.

## 12. Giao diện & Kiến trúc Frontend

- [ ] Xây dựng Wireframe cho các màn hình chính.
- [ ] Xác định luồng điều hướng.
- [ ] Phân chia các Component quan trọng.
- [ ] Thống nhất cách gọi API và quản lý trạng thái.
- [ ] Xác định cách xử lý Loading, Empty State, Error State và Validation.

**Đầu ra:** Wireframe và tài liệu thiết kế Frontend.

**Giới hạn:** Ưu tiên các màn hình và luồng nghiệp vụ cốt lõi; chưa cần hoàn thiện thiết kế UI/UX cho mọi trường hợp.

## 13. Dịch vụ bên ngoài, Async Jobs & Caching Strategy

- [ ] Liệt kê các dịch vụ bên ngoài thực sự cần tích hợp.
- [ ] Xác định cách xử lý Timeout và lỗi tích hợp.
- [ ] Xác định các tác vụ cần chạy bất đồng bộ nếu có.
- [ ] Xác định cơ chế Retry phù hợp cho các tác vụ có thể thử lại.
- [ ] Xác định chiến lược Caching nếu có nhu cầu thực tế.

**Đầu ra:** Tài liệu tích hợp và quy tắc xử lý tác vụ bất đồng bộ khi cần.

**Giới hạn:** Không bắt buộc sử dụng RabbitMQ, Kafka, Redis, Dead Letter Queue hoặc hệ thống Cache chuyên dụng nếu nghiệp vụ không yêu cầu.

### Cổng kiểm tra cuối tuần 2

- [ ] Các chức năng cốt lõi đã được ánh xạ sang module và mô hình dữ liệu.
- [ ] Database Schema và các ràng buộc quan trọng đã được xác định.
- [ ] API Contract đủ rõ để Frontend và Backend triển khai thống nhất.
- [ ] Quy tắc Authentication và Authorization đã được xác định.
- [ ] Các luồng nghiệp vụ quan trọng có Sequence Diagram khi cần.
- [ ] Những rủi ro kỹ thuật lớn đã được kiểm chứng hoặc có phương án xử lý.

---

# TUẦN 3: QUALITY, PLATFORM & DEVELOPMENT READINESS

**Mục tiêu:** Chuẩn hóa xử lý lỗi, kiểm tra chất lượng, bảo mật và chuẩn bị môi trường phát triển có thể tái tạo.

## 14. Error Handling Model & Standard Response Codes

- [ ] Chuẩn hóa cấu trúc phản hồi lỗi.
- [ ] Phân loại lỗi Validation, Business, Authentication, Authorization và Internal Server Error.
- [ ] Thống nhất HTTP Status Code.
- [ ] Bổ sung mã định danh yêu cầu khi cần truy vết lỗi.
- [ ] Xác định thông tin được phép hiển thị cho người dùng và thông tin chỉ ghi trong log.

**Đầu ra:** Tài liệu Error Handling và các mẫu phản hồi.

## 15. Bảo mật & Mô hình mối đe dọa (Security & Threat Modeling)

- [ ] Rà soát các rủi ro bảo mật phù hợp với ứng dụng.
- [ ] Kiểm tra Authentication, Authorization và quyền truy cập tài nguyên.
- [ ] Xác định cách bảo vệ dữ liệu nhạy cảm.
- [ ] Rà soát Injection, XSS, CSRF và các rủi ro liên quan đến ứng dụng.
- [ ] Cấu hình HTTPS, CORS và Security Headers phù hợp với môi trường triển khai.
- [ ] Kiểm tra việc quản lý Secret và dữ liệu nhạy cảm trong log.

**Đầu ra:** Security Checklist và danh sách rủi ro cần xử lý.

**Giới hạn:** Tập trung vào các luồng có dữ liệu người dùng, xác thực và phân quyền; không cần xây dựng chương trình Threat Modeling quy mô doanh nghiệp.

## 16. Database Optimization & Migration Strategy

- [ ] Chọn công cụ hoặc cơ chế quản lý Database Migration.
- [ ] Xác định cách khởi tạo database từ trạng thái ban đầu.
- [ ] Chuẩn bị Seed Data cho phát triển và kiểm thử.
- [ ] Kiểm tra các ràng buộc dữ liệu và giao dịch quan trọng.
- [ ] Xác định các chỉ mục cơ bản dựa trên truy vấn chính.
- [ ] Kiểm tra khả năng chạy Migration trên môi trường Dev.

**Đầu ra:** Migration ban đầu, Seed Data và hướng dẫn khởi tạo database.

**Giới hạn:** Chưa cần Read Replica, Sharding hoặc tối ưu hóa chuyên sâu.

## 17. CI/CD & Automated Pipeline

- [ ] Thiết lập CI chạy Linter, Build và Test.
- [ ] Xác định các điều kiện cơ bản để chấp nhận thay đổi mã nguồn.
- [ ] Tự động Build ứng dụng hoặc Container Image.
- [ ] Thiết lập CD cơ bản nếu có môi trường triển khai phù hợp.
- [ ] Xác định cách quản lý cấu hình theo môi trường.

**Đầu ra:** Pipeline hoạt động và tài liệu sử dụng.

**Giới hạn:** Không bắt buộc Blue/Green Deployment, Kubernetes hoặc quy trình phát hành nhiều tầng.

## 18. Chiến lược Kiểm thử (Testing Strategy & Test Cases)

- [ ] Xác định phạm vi Unit Test, Integration Test và E2E Test.
- [ ] Xây dựng Test Case cho các chức năng cốt lõi.
- [ ] Kiểm thử các trường hợp phân quyền, dữ liệu không hợp lệ và lỗi nghiệp vụ.
- [ ] Xác định tiêu chí Pass/Fail cho các kiểm thử quan trọng.
- [ ] Xác định cách kiểm tra hiệu năng cơ bản nếu NFR yêu cầu.

**Đầu ra:** `testing-strategy.md` và bộ Test Case ban đầu.

**Giới hạn:** Ưu tiên độ tin cậy của các luồng quan trọng; không đặt tỷ lệ Test Coverage cố định cho mọi module.

## 19. Observability & Monitoring

- [ ] Thiết lập Logging có cấu trúc ở mức phù hợp.
- [ ] Xác định các thông tin cần ghi nhận để điều tra lỗi.
- [ ] Thiết lập Health Check cho ứng dụng và các thành phần phụ thuộc quan trọng.
- [ ] Xác định các lỗi hoặc tình trạng bất thường cần theo dõi.

**Đầu ra:** Quy chuẩn Logging và Health Check.

**Giới hạn:** Chưa cần hệ thống ELK, Grafana, Prometheus hoặc Distributed Tracing nếu ứng dụng chưa có nhu cầu.

## 20. Operations Runbook

- [ ] Viết hướng dẫn cài đặt và khởi chạy môi trường.
- [ ] Hướng dẫn cấu hình biến môi trường.
- [ ] Hướng dẫn chạy Migration và Seed Data.
- [ ] Ghi nhận cách xử lý các lỗi phát triển thường gặp.
- [ ] Xác định phương án Backup và Restore phù hợp với dữ liệu.
- [ ] Ghi nhận cách khôi phục phiên bản ứng dụng khi triển khai gặp lỗi.

**Đầu ra:** `development-setup.md` và `operations-runbook.md`.

**Giới hạn:** Chưa cần quy trình Disaster Recovery nhiều vùng hoặc diễn tập sự cố quy mô lớn.

### Cổng kiểm tra cuối tuần 3

- [ ] Tài liệu kiến trúc và thiết kế cốt lõi đã được duyệt.
- [ ] Môi trường Dev có thể khởi chạy theo tài liệu.
- [ ] Database có thể được khởi tạo bằng Migration.
- [ ] API Contract và quy tắc phân quyền đã được xác định.
- [ ] CI chạy thành công với một thay đổi mã nguồn mẫu.
- [ ] Có Test Case cho các chức năng quan trọng.
- [ ] Không còn quyết định kiến trúc chưa giải quyết có khả năng ảnh hưởng lớn đến việc Coding.

---

# 4. KẾ HOẠCH DỰ PHÒNG TUẦN 4

Tuần 4 không phải giai đoạn bắt buộc. Chỉ sử dụng khi cần thêm thời gian hoàn thiện hoặc kiểm chứng.

- [ ] Xử lý các vấn đề phát sinh trong quá trình thiết kế.
- [ ] Hoàn thiện các tài liệu còn thiếu.
- [ ] Kiểm chứng các quyết định kỹ thuật có rủi ro cao.
- [ ] Hoàn thiện PoC cho luồng kỹ thuật quan trọng nếu cần.
- [ ] Kiểm tra khả năng khởi chạy môi trường từ trạng thái sạch.
- [ ] Review toàn bộ tài liệu và xác nhận điều kiện Development Readiness.

**Đầu ra:** Bộ tài liệu được rà soát, môi trường phát triển có thể tái tạo và danh sách vấn đề còn tồn tại.

---

# 5. TIÊU CHÍ PHÊ DUYỆT CUỐI CÙNG

Giai đoạn chuẩn bị kỹ thuật được xem là hoàn thành khi đáp ứng các điều kiện sau:

- [ ] Phạm vi nghiệp vụ và chức năng cốt lõi đã được xác định.
- [ ] Kiến trúc tổng thể và các quyết định công nghệ quan trọng đã được thống nhất.
- [ ] Mô hình dữ liệu và các quy tắc toàn vẹn quan trọng đã được thiết kế.
- [ ] API Contract đủ rõ để Frontend và Backend triển khai.
- [ ] Authentication và Authorization đáp ứng yêu cầu của các luồng cốt lõi.
- [ ] Môi trường phát triển có thể khởi chạy theo tài liệu.
- [ ] Database Migration có thể thực thi.
- [ ] CI chạy được các bước kiểm tra cơ bản.
- [ ] Có chiến lược kiểm thử và Test Case cho các chức năng quan trọng.
- [ ] Các rủi ro còn tồn tại đã được ghi nhận và phân loại.

### Trạng thái phê duyệt

- **Approved:** Đáp ứng các tiêu chí bắt buộc.
- **Approved with Conditions:** Có thể tiếp tục khi các điều kiện còn lại đã được ghi nhận, có người phụ trách và thời hạn xử lý.
- **Blocked:** Còn vấn đề quan trọng có khả năng ảnh hưởng lớn đến tính đúng đắn của thiết kế hoặc tiến độ phát triển.

---

# 6. PHÂN BỔ THỜI GIAN

| Giai đoạn | Thời gian | Kết quả chính |
|---|---|---|
| Tuần 1 | 5 ngày | Scope, Requirements, Business Analysis và kiến trúc tổng thể |
| Tuần 2 | 5 ngày | Database, Module Design, API Contract và Frontend Design |
| Tuần 3 | 5 ngày | Testing Strategy, Security, CI và môi trường phát triển |
| Tuần 4 (dự phòng) | 3–5 ngày | Hoàn thiện, kiểm chứng, review và phê duyệt |

Thời gian trên là ước lượng lập kế hoạch, không phải cam kết tuyệt đối. Tính khả thi phụ thuộc vào độ phức tạp của nghiệp vụ, số người thực hiện và mức độ sẵn sàng của các yêu cầu đầu vào.

**Nguyên tắc cuối cùng:** Không cần hoàn thiện mọi chi tiết trước khi viết dòng code đầu tiên. Cần hoàn thiện đủ những nội dung ảnh hưởng trực tiếp đến kiến trúc, dữ liệu, API, phân quyền và khả năng tích hợp; các tối ưu hóa ít rủi ro có thể được thực hiện trong quá trình phát triển.