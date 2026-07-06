# Báo Cáo Tổng Hợp Kiểm Thử - 23127482 (Bổ sung từ bài Domain Testing)

Tài liệu này cập nhật phần báo cáo cá nhân dựa trên bài Domain Testing đính kèm `23127482_HW02_AI_DomainTesting_100`.

Nguồn tổng hợp:

- `MainReport.md` / `README.md` (số liệu chính thức)
- Ảnh issue tracker (13 issue đang mở, phục vụ đối soát bug candidate)

## 1. Tổng Quan

| Chỉ số | Giá trị |
| --- | ---: |
| Tổng cộng số testcase thiết kế | 57 |
| Số testcase đã thực thi | 38 |
| Số testcase Pass | 28 |
| Số testcase Failed | 10 |
| Số testcase Not executed | 19 |
| Số feature / requirement được bao phủ | 4 |
| Tổng số bug chính thức | 10 |

## 2. Coverage Của Testcase

### 2.1 Coverage theo Feature / Requirement

| Feature | Requirement | Số testcase | Tỷ lệ trên tổng 57 TC |
| --- | --- | ---: | ---: |
| Pool A - Account Registration | FR-01 | 20 | 35.1% |
| Pool B - Shopping Cart | FR-07 | 15 | 26.3% |
| Pool C - Access Control | FR-12 | 10 | 17.5% |
| Pool D - Mobile Registration | FR-MOB | 12 | 21.1% |

### 2.2 Coverage theo Kỹ Thuật Thiết Kế

| Kỹ thuật | Feature áp dụng | Quy mô |
| --- | --- | --- |
| Domain Testing (EP) | FR-01, FR-07, FR-12, FR-MOB | Kỹ thuật chủ lực cho toàn bộ suite |
| Boundary Value Analysis | FR-01, FR-07, FR-12, FR-MOB | 3-point boundary cho password/quantity/token-expiry |

## 3. Status Của Testcase

### 3.1 Tổng hợp trạng thái (theo Summary chính thức)

| Trạng thái | Số lượng |
| --- | ---: |
| Pass | 28 |
| Failed | 10 |
| Not executed | 19 |
| Tổng cộng | 57 |

### 3.2 Phân bổ trạng thái theo feature

| Feature | Designed | Executed | Pass | Failed | Not executed |
| --- | ---: | ---: | ---: | ---: | ---: |
| FR-01 | 20 | 20 | 12 | 8 | 0 |
| FR-07 | 15 | 8 | 6 | 2 | 7 |
| FR-12 | 10 | 10 | 10 | 0 | 0 |
| FR-MOB | 12 | 0 | 0 | 0 | 12 |
| **Tổng** | **57** | **38** | **28** | **10** | **19** |

Ghi chú: ảnh issue tracker đang có thêm các issue mobile và một số case ngoài số liệu chính thức. Các issue này được ghi nhận ở trạng thái `candidate/pending triage` cho đến khi đồng bộ lại execution sheet.

## 4. Tổng Hợp Bug

### 4.1 Số lượng bug theo feature (chính thức)

| Feature | Số bug chính thức | Ghi chú |
| --- | ---: | --- |
| FR-01 | 8 | Lỗi tập trung ở validation email/password, UI và HTML5 attributes |
| FR-07 | 2 | Lỗi hành vi thêm sản phẩm trùng và hiển thị định dạng tiền/tổng cộng |
| FR-12 | 0 | Chưa ghi nhận bug chính thức trong summary |
| FR-MOB | 0 | Chưa ghi nhận bug chính thức trong summary |
| **Tổng** | **10** |  |

### 4.2 Bug candidate từ issue tracker (pending triage)

Ảnh issue tracker ghi nhận 13 issue mở, gồm các nhóm:

- FR-01: 8 issue
- FR-07: 2 issue
- FR-12: 1 issue
- FR-MOB: 2 issue

Các issue này cần được đối chiếu ngược vào execution table trước khi chuẩn hóa lại số bug chính thức của báo cáo.

## 5. Kết Luận

- Bộ bài Domain Testing hiện bao phủ 4 feature với 57 test case được thiết kế.
- Theo số liệu chính thức, đã thực thi 38/57 case, ghi nhận 10 bug xác nhận.
- Issue tracker cho thấy thêm các bug candidate (13 issue mở), phản ánh nhu cầu làm bước triage và đồng bộ dữ liệu test execution trước khi chốt số liệu cuối cùng.
