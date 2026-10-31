# KẾ HOẠCH THIẾT KẾ VÀ CHUẨN BỊ KỸ THUẬT
## Hệ thống Giám sát và Phân tích Thiên tai Toàn cầu

**Phiên bản:** Tinh gọn cho đồ án học tập  
**Thời gian:** 3 tuần chính, tối đa 4 tuần  
**Mục tiêu:** Hoàn thành thiết kế và xây dựng một nguyên mẫu hoạt động với dữ liệu thực, ưu tiên khả năng trình diễn, tính đúng đắn và dễ phát triển.

---

## 1. Mục tiêu sản phẩm

Xây dựng một ứng dụng web cho phép người dùng theo dõi sự kiện thiên tai trên bản đồ toàn cầu, xem thông tin chi tiết, phân tích dữ liệu cơ bản và thử nghiệm một chức năng phân tích hoặc dự báo có giới hạn.

Sản phẩm tập trung vào ba năng lực:

1. **Giám sát:** Thu thập, lưu trữ và hiển thị dữ liệu sự kiện động đất.
2. **Phân tích:** Lọc sự kiện, thống kê và trực quan hóa dữ liệu.
3. **Thử nghiệm dự báo:** Xây dựng một mô hình hoặc phương pháp phân tích thử nghiệm, đánh giá bằng dữ liệu lịch sử và công bố rõ giới hạn.

Phạm vi toàn cầu thể hiện qua dữ liệu và bản đồ, không đồng nghĩa với yêu cầu hạ tầng phân tán toàn cầu.

### 1.1. Phạm vi MVP

**Bắt buộc**
- Bản đồ thế giới hiển thị các trận động đất gần đây.
- Danh sách sự kiện, bộ lọc theo thời gian và độ lớn.
- Trang hoặc cửa sổ chi tiết sự kiện.
- Backend cung cấp REST API.
- Cơ sở dữ liệu lưu sự kiện đã thu thập.
- Cập nhật dữ liệu USGS định kỳ, có xử lý lỗi cơ bản.
- Dashboard thống kê đơn giản.
- Kiểm thử các luồng chính và hướng dẫn chạy ứng dụng.

**Nếu còn thời gian**
- Tích hợp dữ liệu dự báo thời tiết từ Open-Meteo.
- Biểu đồ chuỗi thời gian hoặc thống kê theo khu vực.
- Một thử nghiệm ML có mục tiêu, dữ liệu và chỉ số đánh giá rõ ràng.
- Docker Compose để chạy toàn bộ hệ thống thuận tiện hơn.

**Không thuộc MVP**
- Dự báo chính xác thời điểm hoặc vị trí động đất.
- Tự xây dựng hệ thống dự báo sóng thần hoặc phát cảnh báo chính thức.
- Kafka, Kubernetes, microservices đầy đủ.
- Hạ tầng đa vùng, tự động mở rộng toàn cầu.
- MLOps hoàn chỉnh, huấn luyện liên tục hoặc nhiều mô hình.
- Đăng nhập người dùng, thanh toán và thông báo đa kênh.

---

## 2. Kiến trúc đề xuất

Ưu tiên kiến trúc đơn giản, có ranh giới module rõ ràng và có thể mở rộng sau đồ án.

### 2.1. Công nghệ

| Thành phần | Công nghệ đề xuất | Mục đích |
|---|---|---|
| Frontend | React + TypeScript | Giao diện người dùng |
| Bản đồ | MapLibre GL JS | Hiển thị dữ liệu địa lý |
| Backend | Node.js + Express + TypeScript | REST API và nghiệp vụ |
| Cơ sở dữ liệu | PostgreSQL + PostGIS | Lưu sự kiện và truy vấn địa lý |
| Nguồn dữ liệu | USGS Earthquake GeoJSON | Dữ liệu động đất thực |
| Dữ liệu bổ sung | Open-Meteo (tùy chọn) | Dữ liệu thời tiết |
| ML/Phân tích | Python + scikit-learn (tùy chọn) | Thử nghiệm phân tích dữ liệu |
| Môi trường | Docker Compose (nếu cần) | Chuẩn hóa chạy ứng dụng |
| Kiểm thử API | Postman hoặc công cụ tương đương | Kiểm tra endpoint |

Không bắt buộc sử dụng TimescaleDB, Redis, Kafka, RabbitMQ hay MinIO trong phiên bản đầu tiên. Chỉ bổ sung khi có yêu cầu cụ thể mà kiến trúc hiện tại không đáp ứng được.

### 2.2. Luồng xử lý

1. Backend lấy dữ liệu từ nguồn USGS.
2. Bộ xử lý kiểm tra dữ liệu, chuẩn hóa trường và loại bỏ bản ghi trùng.
3. Dữ liệu được lưu vào PostgreSQL/PostGIS.
4. Backend cung cấp API cho frontend.
5. Frontend hiển thị bản đồ, danh sách, chi tiết và thống kê.
6. Nếu có ML, mô hình đọc dữ liệu lịch sử và tạo kết quả phân tích thử nghiệm riêng biệt.

### 2.3. Quy tắc kiến trúc

- Tách module lấy dữ liệu, xử lý dữ liệu, truy cập cơ sở dữ liệu và API.
- Dùng một backend chính; chưa cần chia thành nhiều dịch vụ.
- Tách phần ML thành module hoặc dịch vụ riêng chỉ khi thật sự cần.
- Lưu thời gian sự kiện, thời gian nguồn cập nhật và thời gian hệ thống thu thập.
- Khi dữ liệu không cập nhật được, giao diện cần thể hiện thời điểm cập nhật gần nhất thay vì giả định dữ liệu vẫn mới.
- Dữ liệu và kết quả ML không được trình bày như cảnh báo thiên tai chính thức.

---

## 3. Kế hoạch thực hiện trong 3 tuần

### Tuần 1 — Chốt phạm vi và thiết kế nền tảng

**Mục tiêu:** Xác định rõ sản phẩm cần làm và đưa ra quyết định kỹ thuật đủ để bắt đầu phát triển.

**Công việc**
- Chốt yêu cầu chức năng và phi chức năng ở mức đồ án.
- Xác định vai trò người dùng chính: khách truy cập công khai.
- Chọn USGS làm nguồn dữ liệu bắt buộc.
- Khảo sát cấu trúc dữ liệu và điều kiện sử dụng của nguồn.
- Vẽ sơ đồ kiến trúc tổng thể.
- Thiết kế các module chính và luồng dữ liệu.
- Chốt công nghệ, cấu trúc thư mục và môi trường phát triển.
- Tạo repository, cấu hình dự án cơ bản.

**Đầu ra**
- Tài liệu phạm vi MVP.
- Sơ đồ kiến trúc tổng thể.
- Danh sách quyết định kỹ thuật quan trọng.
- Đặc tả nguồn dữ liệu.
- Cấu trúc dự án khởi tạo.

**Điều kiện hoàn thành**
- Có thể giải thích luồng dữ liệu từ USGS đến giao diện.
- Không còn yêu cầu bắt buộc nào vượt quá phạm vi đồ án đã chốt.

### Tuần 2 — Thiết kế dữ liệu, API và giao diện

**Mục tiêu:** Hoàn thành bản thiết kế đủ chi tiết để triển khai mà không phải thiết kế lại lớn.

**Công việc**
- Thiết kế ERD và bảng lưu sự kiện động đất.
- Xác định các trường dữ liệu, khóa và chỉ mục cần thiết.
- Thiết kế REST API cho danh sách, chi tiết, bộ lọc và thống kê.
- Xây dựng wireframe cho bản đồ và dashboard.
- Xác định cách cập nhật dữ liệu và xử lý bản ghi trùng.
- Định nghĩa trạng thái tải dữ liệu, lỗi và dữ liệu cũ.
- Thiết kế các trường hợp kiểm thử chính.
- Nếu có thời gian, thử lấy một mẫu dữ liệu thực và lưu vào cơ sở dữ liệu.

**Đầu ra**
- ERD và mô tả trường dữ liệu.
- Danh sách endpoint API.
- Wireframe giao diện.
- Đặc tả quy trình nhập dữ liệu.
- Danh sách kiểm thử cơ bản.

**Điều kiện hoàn thành**
- Các endpoint và cấu trúc dữ liệu đủ rõ để frontend, backend có thể triển khai nhất quán.
- Có thể lưu và truy vấn thử một sự kiện từ dữ liệu thực.

### Tuần 3 — Hoàn thiện thiết kế kỹ thuật và xác minh khả năng triển khai

**Mục tiêu:** Chốt tài liệu, xác minh rủi ro kỹ thuật và chuẩn bị cho giai đoạn phát triển.

**Công việc**
- Xác định cách lập lịch lấy dữ liệu, timeout, retry và ghi log.
- Xác định cơ chế chống trùng và cập nhật bản ghi đã tồn tại.
- Chốt cách xử lý lỗi nguồn dữ liệu hoặc mất kết nối cơ sở dữ liệu.
- Xác định các kiểm thử API, dữ liệu và giao diện.
- Lập danh sách yêu cầu bảo mật cơ bản.
- Thiết kế cách đo hiệu năng cho một số API quan trọng.
- Nếu có ML, xác định bài toán, dữ liệu, baseline và chỉ số đánh giá; không bắt buộc huấn luyện mô hình mới.
- Viết hướng dẫn cài đặt và chạy ứng dụng.
- Tổng hợp rủi ro và kế hoạch phát triển tiếp theo.

**Đầu ra**
- Tài liệu thiết kế kỹ thuật hoàn chỉnh.
- Đặc tả API và cơ sở dữ liệu đã thống nhất.
- Kế hoạch kiểm thử.
- Hướng dẫn môi trường phát triển.
- Báo cáo rủi ro và giới hạn của hệ thống.
- Bản PoC lấy dữ liệu thực nếu chưa hoàn thành ở tuần 2.

**Điều kiện hoàn thành**
- Nhóm có thể bắt đầu phát triển mà không cần bổ sung những quyết định kiến trúc lớn.
- Ít nhất một luồng dữ liệu thực đã được xác minh từ nguồn đến cơ sở dữ liệu hoặc API.

---

## 4. Tuần 4 — Dự phòng và xác minh nguyên mẫu

Tuần 4 chỉ sử dụng khi cần; không bổ sung tính năng mới nếu MVP chưa ổn định.

**Ưu tiên theo thứ tự**
1. Hoàn thiện luồng USGS → xử lý → PostgreSQL/PostGIS.
2. Hoàn thiện API và kiểm tra dữ liệu trả về.
3. Hiển thị sự kiện trên bản đồ.
4. Hoàn thiện bộ lọc và trang chi tiết.
5. Kiểm thử lỗi mạng, dữ liệu trùng và dữ liệu cũ.
6. Chuẩn hóa Docker Compose và hướng dẫn chạy.
7. Thử nghiệm ML hoặc tích hợp thời tiết nếu các phần bắt buộc đã ổn định.

**Nguyên tắc:** Nếu thời gian không đủ, bỏ tính năng tùy chọn thay vì giảm chất lượng của luồng dữ liệu và chức năng chính.

---

## 5. Thiết kế dữ liệu tối thiểu

### 5.1. Bảng `earthquake_events`

Các trường đề xuất:

- `id`: khóa chính nội bộ.
- `source`: nguồn dữ liệu, ví dụ USGS.
- `source_event_id`: mã sự kiện từ nguồn.
- `event_time`: thời điểm xảy ra sự kiện.
- `source_updated_at`: thời điểm nguồn cập nhật bản ghi.
- `ingested_at`: thời điểm hệ thống thu thập.
- `latitude`, `longitude`: tọa độ.
- `depth_km`: độ sâu, nếu có.
- `magnitude`: độ lớn, nếu có.
- `place`: mô tả địa điểm.
- `source_url`: liên kết bản ghi nguồn.
- `raw_data`: dữ liệu gốc dạng JSON, tùy nhu cầu triển khai.

Đặt ràng buộc duy nhất trên tổ hợp `source` và `source_event_id` để hạn chế bản ghi trùng.

Có thể dùng kiểu dữ liệu địa lý PostGIS cho tọa độ nếu cần truy vấn theo khu vực. Không cần thiết kế quá nhiều bảng khi nghiệp vụ chưa yêu cầu.

### 5.2. Dữ liệu thời tiết (tùy chọn)

Chỉ thiết kế bảng riêng khi đã quyết định tích hợp Open-Meteo. Cần phân biệt vị trí, thời điểm dự báo, thời điểm dữ liệu được phát hành và đơn vị đo.

Không gộp dữ liệu thời tiết dự báo vào bảng sự kiện động đất.

---

## 6. API tối thiểu

Các endpoint dưới đây là đề xuất ban đầu; có thể điều chỉnh theo thiết kế thực tế.

| Endpoint | Chức năng |
|---|---|
| `GET /api/earthquakes` | Danh sách sự kiện, hỗ trợ phân trang và lọc |
| `GET /api/earthquakes/:id` | Chi tiết một sự kiện |
| `GET /api/statistics/earthquakes` | Thống kê tổng hợp |
| `GET /api/health` | Kiểm tra trạng thái ứng dụng |

Bộ lọc ban đầu có thể gồm khoảng thời gian, độ lớn tối thiểu và giới hạn số bản ghi.

Yêu cầu cơ bản:
- Kiểm tra tham số đầu vào.
- Giới hạn kích thước kết quả và hỗ trợ phân trang.
- Trả về lỗi có cấu trúc nhất quán.
- Không trả về thông tin bí mật trong thông báo lỗi.
- Ghi nhận lỗi khi nguồn dữ liệu không truy cập được.

---

## 7. ML và dự báo: giới hạn rõ ràng

ML là phần mở rộng, không phải điều kiện để hoàn thành MVP.

Có thể lựa chọn một trong các hướng sau nếu đủ thời gian:

- Phân cụm các sự kiện lịch sử để trực quan hóa các vùng có nhiều hoạt động địa chấn.
- Phân tích thống kê tần suất sự kiện theo thời gian hoặc khu vực.
- Thử nghiệm mô hình dự báo một biến có dữ liệu phù hợp, kèm baseline và đánh giá trên dữ liệu chưa dùng để huấn luyện.

Không được xem phân cụm là dự báo, hoặc tuyên bố mô hình có thể dự báo chính xác động đất chỉ dựa vào dữ liệu lịch sử.

Nếu sử dụng mô hình:
- Xác định câu hỏi cụ thể cần trả lời.
- So sánh với baseline đơn giản.
- Chọn chỉ số đánh giá phù hợp với bài toán.
- Tránh rò rỉ dữ liệu giữa tập huấn luyện và tập kiểm thử.
- Hiển thị kết quả như phân tích thử nghiệm, không phải cảnh báo chính thức.

---

## 8. Kiểm thử và tiêu chí nghiệm thu

### 8.1. Chức năng

- Có thể lấy dữ liệu động đất từ nguồn USGS.
- Dữ liệu được chuẩn hóa và lưu vào cơ sở dữ liệu.
- Không tạo bản ghi trùng khi nhập lại cùng một sự kiện.
- API trả về danh sách và chi tiết đúng cấu trúc.
- Người dùng có thể lọc sự kiện và xem chúng trên bản đồ.
- Giao diện thể hiện được trạng thái tải dữ liệu và lỗi.
- Thời điểm cập nhật dữ liệu được hiển thị rõ ràng.

### 8.2. Kỹ thuật

- Có hướng dẫn chạy dự án từ môi trường mới.
- Các endpoint chính có kiểm thử.
- Có log lỗi cho quy trình nhập dữ liệu.
- Có cấu hình biến môi trường; không đưa bí mật vào repository.
- Có thể khởi động các thành phần bằng hướng dẫn thống nhất.
- Có báo cáo những giới hạn chưa giải quyết.

### 8.3. Hiệu năng

Không đặt mục tiêu hiệu năng toàn cầu khi chưa có kiểm thử tải. Có thể đo thời gian phản hồi của các API chính trên môi trường phát triển và ghi nhận kết quả thực tế.

### 8.4. An toàn thông tin và cảnh báo

- API công khai chỉ cung cấp dữ liệu cần thiết.
- Giới hạn tham số và kích thước truy vấn.
- Không để lộ thông tin kết nối cơ sở dữ liệu.
- Không tự phát thông báo như thể đó là cảnh báo thiên tai chính thức.
- Ghi rõ nguồn dữ liệu, thời điểm cập nhật và giới hạn của các kết quả phân tích.

---

## 9. Danh sách bàn giao

1. Tài liệu yêu cầu và phạm vi MVP.
2. Sơ đồ kiến trúc tổng thể.
3. Các quyết định công nghệ chính.
4. Đặc tả nguồn dữ liệu USGS.
5. ERD và mô tả dữ liệu.
6. Đặc tả REST API.
7. Wireframe giao diện.
8. Thiết kế quy trình thu thập dữ liệu.
9. Thiết kế xử lý lỗi và độ mới dữ liệu.
10. Kế hoạch kiểm thử.
11. Hướng dẫn môi trường và chạy dự án.
12. PoC sử dụng dữ liệu thực.
13. Danh sách rủi ro và giới hạn.
14. Báo cáo nghiệm thu thiết kế.

---

## 10. Thứ tự ưu tiên khi thiếu thời gian

**P0 — Bắt buộc**
- USGS.
- PostgreSQL/PostGIS.
- Backend API.
- Bản đồ sự kiện.
- Bộ lọc và chi tiết.
- Kiểm thử luồng chính.
- Tài liệu chạy dự án.

**P1 — Nên có**
- Dashboard thống kê.
- Docker Compose.
- Xử lý retry, log và dữ liệu cũ tốt hơn.

**P2 — Chỉ làm khi còn thời gian**
- Open-Meteo.
- ML thử nghiệm.
- Redis, hàng đợi hoặc các thành phần hạ tầng bổ sung.

---

## Kết luận

Kế hoạch này phù hợp với một đồ án học tập có định hướng toàn cầu nhưng giới hạn phạm vi triển khai. Ba tuần dành cho thiết kế và chuẩn bị kỹ thuật; tuần thứ tư làm vùng đệm để xác minh nguyên mẫu và xử lý những phần chưa hoàn thiện.

Tiêu chí thành công không phải là số lượng công nghệ được sử dụng, mà là một luồng dữ liệu thực hoạt động xuyên suốt, một giao diện có thể trình diễn, các API có kiểm thử và tài liệu đủ rõ để tiếp tục phát triển.

Hệ thống là công cụ giám sát và phân tích phục vụ học tập; không thay thế các cơ quan cảnh báo thiên tai có thẩm quyền.