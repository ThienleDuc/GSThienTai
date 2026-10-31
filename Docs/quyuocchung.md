# TEAM DEVELOPMENT CONVENTIONS
# QUY ƯỚC PHÁT TRIỂN VÀ PHỐI HỢP NHÓM

**Dự án:** Global Disaster Monitoring & Analysis System (GDMAS)  
**Phiên bản:** 1.0  
**Trạng thái:** Draft / Pending Approval  
**Phạm vi áp dụng:** Toàn bộ thành viên phát triển dự án  
**Thời gian áp dụng:** Toàn bộ vòng đời phát triển sản phẩm

---

# I. MỤC ĐÍCH VÀ NGUYÊN TẮC CHUNG

## 1. Mục đích

Tài liệu quy định các tiêu chuẩn và quy ước thống nhất trong quá trình phát triển GDMAS nhằm:

- Đảm bảo tất cả thành viên tuân thủ cùng một kiến trúc.
- Thống nhất cách tổ chức mã nguồn và thư mục.
- Hạn chế xung đột khi làm việc đồng thời.
- Đảm bảo khả năng tích hợp giữa các service.
- Thống nhất cấu trúc dữ liệu và giao tiếp API.
- Đảm bảo hệ thống có thể chạy trên môi trường của tất cả thành viên.
- Dễ dàng kiểm thử, bảo trì và bàn giao sản phẩm.

## 2. Nguyên tắc bắt buộc

| Mã | Nguyên tắc | Quy định |
|---|---|---|
| RULE-01 | Kiến trúc | Không tự ý thay đổi kiến trúc đã thống nhất |
| RULE-02 | Công nghệ | Tuân thủ Python, PostgreSQL, React và Docker |
| RULE-03 | Mã nguồn | Sử dụng chung cấu trúc thư mục và quy tắc đặt tên |
| RULE-04 | Git | Mọi thay đổi mã nguồn phải được quản lý bằng Git |
| RULE-05 | Database | Không tự ý thay đổi cấu trúc DB dùng chung |
| RULE-06 | API | Tuân thủ hợp đồng API đã thống nhất |
| RULE-07 | Service | Mỗi service phải có khả năng chạy độc lập |
| RULE-08 | Kiểm thử | Kiểm thử trước khi tích hợp vào nhánh chính |
| RULE-09 | Tài liệu | Cập nhật tài liệu khi có thay đổi liên quan |
| RULE-10 | Bảo mật | Không đưa thông tin bí mật lên GitHub |

**Quy tắc:** Không tự ý thay đổi công nghệ, cấu trúc Database, hợp đồng API hoặc giao tiếp giữa các service nếu chưa được nhóm thống nhất.

---

# II. QUY ƯỚC TỔ CHỨC MÃ NGUỒN

## 3. Cấu trúc thư mục dự án

Toàn bộ thành viên phải tuân thủ cấu trúc repository chung.

```text
GDMAS/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   ├── types/
│   │   ├── utils/
│   │   └── assets/
│   ├── package.json
│   └── Dockerfile
│
├── backend/
│   ├── shared/
│   │   ├── config/
│   │   ├── database/
│   │   ├── models/
│   │   ├── schemas/
│   │   └── utils/
│   │
│   ├── services/
│   │   ├── ingestion/
│   │   ├── analysis/
│   │   ├── clustering/
│   │   ├── prediction/
│   │   └── api/
│   │
│   ├── migrations/
│   ├── tests/
│   ├── requirements.txt
│   └── Dockerfile
│
├── database/
│   └── init/
│
├── docs/
│   ├── SAD.md
│   ├── TEAM_CONVENTIONS.md
│   ├── ERD.md
│   ├── API.md
│   └── TESTING.md
│
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

### 3.1. Quy định tổ chức

- Không tạo thư mục tùy tiện ở thư mục gốc.
- Không đặt mã nguồn của nhiều service trong cùng một module nghiệp vụ nếu không có lý do.
- Các thành phần dùng chung phải đặt trong `shared/`.
- Không sao chép mã nguồn giữa các service khi có thể tái sử dụng module chung.
- Mỗi service phải có điểm khởi chạy riêng.
- Mỗi thành viên chỉ được thay đổi các khu vực mã nguồn thuộc phạm vi công việc hoặc được nhóm phân công.

## 4. Quy ước đặt tên

### 4.1. Python

| Thành phần | Quy ước | Ví dụ |
|---|---|---|
| File | snake_case | `data_ingestion.py` |
| Function | snake_case | `fetch_earthquakes()` |
| Variable | snake_case | `event_time` |
| Class | PascalCase | `EarthquakeProcessor` |
| Constant | UPPER_SNAKE_CASE | `MAX_RETRY` |
| Package | snake_case | `data_analysis` |

### 4.2. Frontend – React/TypeScript

| Thành phần | Quy ước | Ví dụ |
|---|---|---|
| Component | PascalCase | `EarthquakeMap.tsx` |
| Page | PascalCase | `DashboardPage.tsx` |
| Hook | camelCase, tiền tố use | `useEarthquakes.ts` |
| Function | camelCase | `getEarthquakes()` |
| Variable | camelCase | `eventTime` |
| Interface/Type | PascalCase | `EarthquakeEvent` |
| Constant | UPPER_SNAKE_CASE | `API_BASE_URL` |

### 4.3. Database

| Thành phần | Quy ước | Ví dụ |
|---|---|---|
| Table | snake_case, số nhiều | `earthquake_events` |
| Column | snake_case | `event_time` |
| Primary Key | id | `id` |
| Foreign Key | tên trường + `_id` | `event_id` |
| Index | idx_tên_bảng_tên_trường | `idx_earthquake_events_event_time` |
| Unique | uq_tên_bảng_tên_trường | `uq_earthquake_source_id` |

### 4.4. Docker và cấu hình

- Tên service Docker sử dụng chữ thường và dấu gạch ngang hoặc gạch dưới nhất quán.
- Tên biến môi trường sử dụng `UPPER_SNAKE_CASE`.
- Tên file cấu hình sử dụng chữ thường.
- Không đặt tên file có dấu tiếng Việt hoặc khoảng trắng.

---

# III. QUY ƯỚC LẬP TRÌNH

## 5. Quy chuẩn Python Backend

### 5.1. Tiêu chuẩn mã nguồn

- Sử dụng Python 3.x theo phiên bản nhóm thống nhất.
- Sử dụng type hints cho các hàm nghiệp vụ và interface quan trọng.
- Ưu tiên function có một trách nhiệm rõ ràng.
- Hạn chế function quá dài hoặc chứa nhiều logic không liên quan.
- Không sử dụng biến toàn cục để lưu trạng thái nghiệp vụ.
- Không hardcode thông tin cấu hình.
- Xử lý ngoại lệ rõ ràng.
- Sử dụng logging thay vì `print()` trong mã nguồn vận hành.

### 5.2. Công cụ chuẩn hóa

| Công cụ | Mục đích |
|---|---|
| Ruff | Lint và kiểm tra quy tắc mã nguồn |
| Ruff Formatter | Định dạng Python |
| Pytest | Kiểm thử |
| Type Hints | Kiểm soát kiểu dữ liệu |

Tất cả thành viên Backend phải sử dụng chung cấu hình Ruff và chạy kiểm thử trước khi tạo Pull Request.

### 5.3. Cấu trúc module

Mỗi service nên phân tách:

- Entry Point: Điểm khởi chạy.
- Config: Cấu hình.
- Services: Logic nghiệp vụ.
- Repositories: Truy cập dữ liệu.
- Schemas: Kiểu dữ liệu đầu vào và đầu ra.
- Tests: Kiểm thử.

Không bắt buộc tạo đầy đủ các thư mục nếu service nhỏ, nhưng phải đảm bảo phân tách trách nhiệm.

## 6. Quy chuẩn Frontend

- Sử dụng React + TypeScript.
- Sử dụng functional components và React Hooks.
- Tách component giao diện khỏi logic gọi API.
- Không gọi API trực tiếp ở nhiều component nếu có thể tái sử dụng service.
- Không hardcode dữ liệu giả trong giao diện chính thức.
- Có trạng thái Loading, Error và Empty State.
- Có kiểm tra kiểu dữ liệu từ API.
- Sử dụng component dùng chung cho các thành phần giao diện lặp lại.
- Thống nhất cách quản lý CSS và thiết kế giao diện.

### 6.1. Cấu trúc xử lý API

Frontend phải sử dụng lớp API Client hoặc các module dịch vụ riêng.

Ví dụ:

```text
src/
├── services/
│   ├── apiClient.ts
│   ├── earthquakeService.ts
│   ├── analysisService.ts
│   └── predictionService.ts
```

Không đặt URL API rải rác trong các component.

## 7. Quy chuẩn chất lượng mã nguồn

Mã nguồn phải đáp ứng:

- Dễ đọc.
- Dễ hiểu.
- Có cấu trúc.
- Không trùng lặp không cần thiết.
- Có xử lý lỗi.
- Có thể kiểm thử.
- Không chứa mã nguồn thử nghiệm không sử dụng.
- Không để lại đoạn code bị comment kéo dài mà không có lý do.

Comment chỉ sử dụng khi cần giải thích logic, thuật toán hoặc quyết định kỹ thuật khó hiểu.

---

# IV. QUY ƯỚC GIT VÀ GITHUB

## 8. Quản lý repository

GitHub là nền tảng quản lý mã nguồn chính thức của nhóm.

Quy định:

- Mỗi thành viên sử dụng tài khoản GitHub cá nhân.
- Không làm việc trực tiếp trên nhánh `main`.
- Mỗi công việc phải có nhánh riêng.
- Không commit file cấu hình bí mật.
- Không tự ý xóa hoặc ghi đè công việc của thành viên khác.
- Không đưa mã nguồn chưa kiểm thử vào nhánh chính.

## 9. Quy ước đặt tên Branch

Sử dụng cấu trúc:

```text
<type>/<short-description>
```

Các loại branch:

| Type | Mục đích | Ví dụ |
|---|---|---|
| feature | Phát triển chức năng | `feature/earthquake-map` |
| fix | Sửa lỗi | `fix/ingestion-duplicate` |
| refactor | Tái cấu trúc | `refactor/analysis-service` |
| docs | Cập nhật tài liệu | `docs/update-sad` |
| test | Bổ sung kiểm thử | `test/earthquake-api` |
| chore | Công việc cấu hình | `chore/docker-setup` |

## 10. Quy ước Commit

Sử dụng Conventional Commits.

Cấu trúc:

```text
<type>(<scope>): <description>
```

Các loại commit:

| Type | Ý nghĩa |
|---|---|
| feat | Thêm chức năng |
| fix | Sửa lỗi |
| refactor | Tái cấu trúc |
| docs | Tài liệu |
| test | Kiểm thử |
| style | Định dạng mã nguồn |
| chore | Cấu hình và công việc phụ trợ |
| perf | Tối ưu hiệu năng |

Ví dụ:

```text
feat(ingestion): add USGS data collection
fix(database): prevent duplicate earthquake events
feat(api): add earthquake statistics endpoint
refactor(analysis): separate trend calculation
docs(sad): update system architecture
test(prediction): add forecasting unit tests
```

Quy định:

- Mỗi commit tập trung vào một mục đích.
- Không sử dụng nội dung commit chung chung như `update`, `fix`, `done`.
- Không gộp nhiều chức năng không liên quan vào một commit.
- Không commit mã nguồn đang lỗi nếu chưa có lý do được thống nhất.

## 11. Pull Request và Code Review

Mọi thay đổi đưa vào `main` phải thông qua Pull Request.

### 11.1. Nội dung Pull Request

Mỗi PR phải có:

- Tiêu đề rõ ràng.
- Mục đích thay đổi.
- Danh sách nội dung đã thực hiện.
- Kết quả kiểm thử.
- Ảnh minh họa nếu thay đổi giao diện.
- Ảnh hưởng đến API hoặc Database nếu có.

### 11.2. Quy trình

1. Thành viên tạo branch.
2. Phát triển chức năng.
3. Kiểm thử cục bộ.
4. Commit và push lên GitHub.
5. Tạo Pull Request.
6. Thành viên khác hoặc người phụ trách kỹ thuật review.
7. Sửa các vấn đề được phản hồi.
8. Merge vào `main`.

### 11.3. Điều kiện Merge

- Mã nguồn không có lỗi nghiêm trọng đã biết.
- Đã chạy kiểm thử liên quan.
- Không chứa thông tin bí mật.
- Không phá vỡ API hoặc cấu trúc dữ liệu đã thống nhất.
- PR được người có trách nhiệm chấp thuận.

---

# V. QUY ƯỚC DATABASE

## 12. Quản lý PostgreSQL

PostgreSQL là cơ sở dữ liệu tập trung của hệ thống.

Quy định:

- Sử dụng một cấu hình Database thống nhất.
- Không tự tạo Database riêng cho từng service nếu chưa được thống nhất.
- Các service dùng chung quy ước truy cập dữ liệu.
- Không tự ý sửa bảng đang được service khác sử dụng.
- Không thay đổi tên cột hoặc kiểu dữ liệu mà không thông báo nhóm.
- Sử dụng migration để quản lý thay đổi cấu trúc Database.

## 13. Quy định thay đổi Schema

Mọi thay đổi Database phải:

1. Xác định lý do thay đổi.
2. Đánh giá ảnh hưởng đến các service.
3. Cập nhật ERD.
4. Tạo migration.
5. Kiểm thử migration.
6. Thông báo các thành viên liên quan.
7. Cập nhật tài liệu dữ liệu.

Sử dụng Alembic để quản lý migration trong Backend Python.

Không chỉnh sửa trực tiếp Database dùng chung mà không cập nhật migration tương ứng.

## 14. Quy ước dữ liệu

| Nội dung | Quy định |
|---|---|
| Timezone | UTC |
| Thời gian | TIMESTAMPTZ |
| Latitude | WGS84 |
| Longitude | WGS84 |
| Depth | Kilometers |
| Magnitude | Numeric value |
| Source ID | Giữ nguyên mã sự kiện nguồn |
| Raw Data | JSONB khi cần |
| Duplicate | UNIQUE + UPSERT |

Đối với sự kiện động đất:

```text
UNIQUE(source, source_event_id)
```

Tất cả thành viên phải sử dụng thống nhất cách hiểu và đơn vị của dữ liệu.

Không tự ý chuyển đổi đơn vị hoặc thay đổi ý nghĩa trường dữ liệu.

---

# VI. QUY ƯỚC API VÀ GIAO TIẾP SERVICE

## 15. Quy chuẩn REST API

- Sử dụng HTTP REST.
- Trao đổi dữ liệu JSON.
- Sử dụng danh từ cho tài nguyên.
- Sử dụng HTTP Method đúng mục đích.
- Có kiểm tra tham số.
- Có phân trang khi trả về danh sách.
- Có cấu trúc lỗi thống nhất.
- Có tài liệu API cập nhật.

Ví dụ:

```text
GET /api/earthquakes
GET /api/earthquakes/{id}
GET /api/statistics/earthquakes
GET /api/analysis/trend
GET /api/predictions
GET /api/classifications
```

## 16. Quy chuẩn phản hồi API

Phản hồi thành công:

```json
{
  "success": true,
  "data": {},
  "metadata": {}
}
```

Phản hồi thất bại:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description"
  }
}
```

Không tự ý thay đổi cấu trúc phản hồi API mà không thông báo Frontend và các thành viên liên quan.

## 17. Quy chuẩn giao tiếp giữa các service

Các service xử lý dữ liệu sử dụng PostgreSQL làm phương thức trao đổi dữ liệu trong MVP.

Quy định:

- Không tự ý tạo API nội bộ giữa các service.
- Không truy cập trực tiếp vào bảng không thuộc phạm vi trách nhiệm nếu không cần thiết.
- Phải thống nhất schema dữ liệu đầu vào và đầu ra.
- Không ghi đè dữ liệu kết quả của service khác.
- Kết quả xử lý phải có thời gian tạo và thông tin phương pháp.
- Các service phải xử lý được trường hợp dữ liệu chưa có hoặc chưa cập nhật.

---

# VII. QUY ƯỚC SERVICE VÀ DOCKER

## 18. Quy định triển khai service

Các service bắt buộc:

| Service | Trách nhiệm |
|---|---|
| Data Ingestion | Thu thập dữ liệu |
| Data Analysis | Phân tích chuỗi thời gian |
| Clustering | Phân cụm |
| Prediction | Dự báo và phân loại |
| Database API | Cung cấp API |
| Frontend | Giao diện |
| PostgreSQL | Lưu trữ |

Mỗi service phải:

- Có entrypoint riêng.
- Có cấu hình riêng khi cần.
- Có log riêng.
- Có thể khởi động độc lập.
- Có thể dừng độc lập.
- Không phụ thuộc terminal của service khác.
- Không chứa logic nghiệp vụ của service khác.

## 19. Quy định Docker

- Mỗi service có cấu hình chạy riêng.
- Các service được quản lý thống nhất bằng Docker Compose.
- Không đưa `.env` vào Docker image.
- PostgreSQL sử dụng persistent volume.
- Sử dụng Docker network nội bộ.
- Không công khai cổng Database nếu không cần thiết.
- Không sử dụng `localhost` để kết nối giữa các container; sử dụng tên service trong Docker network.
- Phải có hướng dẫn chạy và dừng hệ thống.

## 20. Quy trình kiểm tra trước khi bàn giao

Mỗi thành viên phải đảm bảo:

- Service khởi động thành công.
- Kết nối Database hoạt động.
- Không có lỗi cấu hình.
- Các chức năng chính hoạt động.
- Log được ghi nhận.
- Có hướng dẫn chạy nếu có thay đổi cấu hình.
- Có thể chạy trong môi trường Docker đã thống nhất.

---

# VIII. QUY ƯỚC PHÂN TÍCH VÀ MACHINE LEARNING

## 21. Quy chuẩn xử lý dữ liệu

- Không tự ý thay đổi dữ liệu gốc.
- Phải xác định rõ dữ liệu thiếu.
- Phải thống nhất cách resampling.
- Phải ghi rõ đơn vị và khoảng thời gian.
- Không tùy tiện loại bỏ dữ liệu ngoại lệ.
- Các bước tiền xử lý phải có thể tái hiện.

## 22. Quy chuẩn thuật toán

Mọi thuật toán phải có:

- Mục tiêu xử lý.
- Dữ liệu đầu vào.
- Các bước tiền xử lý.
- Phương pháp sử dụng.
- Kết quả đầu ra.
- Chỉ số đánh giá phù hợp.
- Giới hạn của phương pháp.

## 23. Quy chuẩn dự báo

- Không sử dụng dữ liệu tương lai trong quá trình huấn luyện.
- Chia tập dữ liệu theo thời gian.
- Có baseline so sánh.
- Ghi nhận sai số.
- Phân biệt dữ liệu thực tế và dự báo.
- Không tuyên bố dự báo chính xác thời điểm xảy ra động đất.

## 24. Quy chuẩn kết quả phân tích

Mỗi kết quả phân tích cần xác định:

- Service tạo kết quả.
- Khoảng thời gian dữ liệu.
- Thời điểm xử lý.
- Phương pháp sử dụng.
- Phiên bản thuật toán hoặc mô hình khi phù hợp.
- Trạng thái xử lý.

---

# IX. QUY ƯỚC KIỂM THỬ VÀ TÀI LIỆU

## 25. Kiểm thử

Mỗi thành viên chịu trách nhiệm kiểm thử phần việc của mình.

| Loại kiểm thử | Nội dung |
|---|---|
| Unit Test | Kiểm thử logic riêng lẻ |
| Integration Test | Kiểm thử Database và service |
| API Test | Kiểm thử endpoint |
| End-to-End Test | Kiểm thử luồng toàn hệ thống |

Không đưa chức năng mới vào nhánh chính khi chưa kiểm tra các trường hợp quan trọng.

## 26. Tài liệu

Các thay đổi sau phải cập nhật tài liệu tương ứng:

| Thay đổi | Tài liệu cần cập nhật |
|---|---|
| Thay đổi kiến trúc | SAD |
| Thay đổi Database | ERD |
| Thay đổi API | API Specification |
| Thay đổi thuật toán | Analysis Documentation |
| Thay đổi môi trường | README / Deployment Guide |
| Thay đổi kiểm thử | Testing Documentation |

Không để tài liệu mô tả khác với hệ thống thực tế.

---

# X. QUY ƯỚC PHỐI HỢP NHÓM

## 27. Phân công trách nhiệm

Mỗi công việc phải có một người chịu trách nhiệm chính.

Quy định:

- Một task có một người chịu trách nhiệm chính.
- Có thể có người hỗ trợ.
- Không để hai thành viên cùng sửa một module mà không thống nhất.
- Người phụ trách module chịu trách nhiệm kiểm tra và bàn giao.
- Các thay đổi ảnh hưởng module khác phải thông báo trước.

## 28. Giao tiếp và báo cáo tiến độ

Mỗi thành viên cần cập nhật:

- Công việc đã hoàn thành.
- Công việc đang thực hiện.
- Khó khăn gặp phải.
- Những thay đổi kỹ thuật.
- Công việc cần thành viên khác hỗ trợ.

Khi gặp vấn đề ảnh hưởng kiến trúc, Database hoặc API, phải thông báo nhóm trước khi tự ý thay đổi.

## 29. Xử lý xung đột

Khi phát sinh bất đồng:

1. Xác định vấn đề kỹ thuật.
2. Đánh giá ảnh hưởng đến kiến trúc.
3. Đưa ra phương án.
4. Thảo luận với các thành viên liên quan.
5. Người phụ trách kỹ thuật tổng hợp quyết định.
6. Cập nhật tài liệu nếu quyết định làm thay đổi thiết kế.

Không tự ý áp dụng giải pháp có thể phá vỡ tính tương thích của hệ thống.

---

# XI. DEFINITION OF DONE – TIÊU CHUẨN HOÀN THÀNH CÔNG VIỆC

## 30. Điều kiện hoàn thành một task

Một task chỉ được xem là hoàn thành khi:

- [ ] Đúng yêu cầu được giao.
- [ ] Tuân thủ cấu trúc và quy ước mã nguồn.
- [ ] Không ảnh hưởng chức năng hiện có.
- [ ] Đã kiểm thử.
- [ ] Không còn lỗi nghiêm trọng đã biết.
- [ ] Đã commit và push lên GitHub.
- [ ] Đã tạo Pull Request nếu cần tích hợp vào nhánh chính.
- [ ] Đã cập nhật tài liệu liên quan.
- [ ] Đã được review và chấp thuận.

## 31. Điều kiện hoàn thành một service

- [ ] Có entrypoint riêng.
- [ ] Có thể chạy độc lập.
- [ ] Kết nối đúng PostgreSQL.
- [ ] Có cấu hình môi trường.
- [ ] Có logging.
- [ ] Có xử lý lỗi.
- [ ] Có kiểm thử cơ bản.
- [ ] Có Dockerfile hoặc cấu hình chạy Docker tương ứng.
- [ ] Được tích hợp thành công với hệ thống.

## 32. Điều kiện hoàn thành toàn bộ hệ thống

- [ ] Tất cả service hoạt động.
- [ ] Data Ingestion thu thập được dữ liệu thực.
- [ ] PostgreSQL lưu trữ dữ liệu đúng.
- [ ] Các tác vụ định kỳ hoạt động.
- [ ] Database API cung cấp dữ liệu chính xác.
- [ ] Frontend hiển thị dữ liệu.
- [ ] Sáu nhóm phân tích có kết quả tương ứng.
- [ ] Docker Compose khởi chạy được hệ thống.
- [ ] Repository GitHub đầy đủ mã nguồn và tài liệu.
- [ ] Có hướng dẫn cài đặt, chạy và kiểm thử.

---

# XII. QUẢN LÝ VÀ PHÊ DUYỆT QUY ƯỚC

## 33. Nguyên tắc áp dụng

- Tất cả thành viên phải đọc và thống nhất quy ước trước khi phát triển.
- Không tự ý bỏ qua quy định.
- Các ngoại lệ phải được trao đổi và thống nhất.
- Quy ước có thể cập nhật khi kiến trúc thay đổi.
- Mọi phiên bản cập nhật phải được lưu trên GitHub.

## 34. Phê duyệt

| Vai trò | Người phụ trách | Trạng thái |
|---|---|---|
| Người soạn thảo | [Tên] | Pending |
| Người phụ trách kỹ thuật | [Tên] | Pending |
| Thành viên 1 | [Tên] | Pending |
| Thành viên 2 | [Tên] | Pending |
| Thành viên 3 | [Tên] | Pending |
| Thành viên 4 | [Tên] | Pending |

**Trạng thái tài liệu:** Pending Approval

**Nguyên tắc cuối cùng:**

Tất cả thành viên phải phát triển theo cùng một kiến trúc, cùng một quy ước dữ liệu, cùng một tiêu chuẩn mã nguồn và cùng một quy trình tích hợp.

Mục tiêu không chỉ là hoàn thành chức năng riêng lẻ mà là đảm bảo tất cả thành phần có thể kết hợp thành một hệ thống thống nhất, hoạt động ổn định và có thể bàn giao.