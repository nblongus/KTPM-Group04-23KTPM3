# Báo Cáo Tổng Hợp Kiểm Thử

Tài liệu này tổng hợp kết quả thiết kế, testcase và bug report từ 3 bộ tài liệu:

- [FR-09: Mã Giảm Giá](testdesign.md) / [testcase.md](testcase.md)
- [FR-10: Trạng Thái Đơn Hàng](fr10-order-state-machine/design-analysis.md)
- [FR-03: Quên mật khẩu & Đặt lại mật khẩu](fr03-usecase-testing/design-analysis.md)

## 1. Tổng Quan

| Chỉ số | Giá trị |
| --- | ---: |
| Tổng cộng số testcase | 25 |
| Số feature / requirement được bao phủ | 3 |
| Số kỹ thuật thiết kế được sử dụng | 3 |
| Tổng số bug phát hiện | 4 |

## 2. Coverage Của Testcase

### 2.1 Coverage theo Feature / Requirement / Technique

| Feature | Requirement | Kỹ thuật thiết kế | Số testcase | Tỷ lệ trên tổng tc |
| --- | --- | --- | ---: | ---: |
| FR-09 - Mã Giảm Giá | FR-09 | Bảng Quyết Định + Pairwise | 11 | 44% |
| FR-10 - Trạng Thái Đơn Hàng | FR-10 | State Transition Testing | 8 | 32% |
| FR-03 - Quên mật khẩu & Đặt lại mật khẩu | FR-03 | Use Case Testing | 6 | 24% |

### 2.2 Coverage theo Requirement

| Requirement | Nội dung | Số testcase | Ghi chú |
| --- | --- | ---: | --- |
| FR-09 | Mã Giảm Giá | 11 | Có testcase cho luồng thành công và các nhánh lỗi chính |
| FR-10 | Trạng Thái Đơn Hàng | 8 | Bao phủ đủ chuyển đổi hợp lệ và chuyển đổi không hợp lệ |
| FR-03 | Quên mật khẩu & Đặt lại mật khẩu | 6 | Bao phủ luồng chính và các luồng thay thế quan trọng |

### 2.3 Coverage theo Kỹ Thuật Thiết Kế

| Kỹ thuật | Feature áp dụng | Số testcase | Ghi chú |
| --- | --- | ---: | --- |
| Decision Table + Pairwise | FR-09 | 11 | Có rút gọn logic và tổ hợp cặp |
| State Transition Testing | FR-10 | 8 | Dựa trên state machine của đơn hàng |
| Use Case Testing | FR-03 | 6 | Dựa trên luồng 2 bước và các luồng thay thế |

## 3. Status Của Testcase

### 3.1 Tổng hợp trạng thái

| Trạng thái | Số lượng |
| --- | ---: |
| Pass | 9 |
| Failed | 4 |
| Not executed | 12 |
| Tổng cộng | 25 |

### 3.2 Ghi chú về trạng thái

- FR-09 có trạng thái được ghi trực tiếp trong [testcase.md](testcase.md): 9 Pass, 2 Failed.
- FR-03 và FR-10 có testcase markdown riêng trong các folder chuyên biệt; các bug report đã xác nhận 4 testcase thất bại tương ứng.
- 12 testcase còn lại trong FR-03 và FR-10 chưa được cập nhật trạng thái Pass/Failed trong file testcase, nên được giữ là Not executed.

## 4. Tổng Hợp Bug

### 4.1 Số lượng bug theo feature / requirement

| Feature | Requirement | Số bug | Bug IDs |
| --- | --- | ---: | --- |
| FR-09 - Mã Giảm Giá | FR-09 | 0 | - |
| FR-10 - Trạng Thái Đơn Hàng | FR-10 | 2 | BUG-01 (TC-06), BUG-02 (TC-08) |
| FR-03 - Quên mật khẩu & Đặt lại mật khẩu | FR-03 | 2 | BUG-01 (TC-01), BUG-02 (TC-06) |

### 4.2 Coverage của bug theo severity

| Severity | Số bug | Ghi chú |
| --- | ---: | --- |
| High | 3 | Gồm 2 bug FR-10 và 1 bug FR-03 về mật khẩu yếu |
| Medium | 1 | Bug FR-03 về OTP không đủ 6 chữ số |
| Low | 0 | Không ghi nhận |
| Critical | 0 | Không ghi nhận |

### 4.3 Bug coverage theo yêu cầu vi phạm

| Bug ID | Feature | Requirement vi phạm | Severity | Test case liên quan |
| --- | --- | --- | --- | --- |
| BUG-01 | FR-03 - Quên mật khẩu & Đặt lại mật khẩu | FR-03: OTP phải là 6 chữ số | Medium | TC-01 |
| BUG-02 | FR-03 - Quên mật khẩu & Đặt lại mật khẩu | FR-03, FR-01: mật khẩu mới phải mạnh | High | TC-06 |
| BUG-01 | FR-10 - Trạng thái Đơn hàng | FR-10: shipping không được user hủy | High | TC-06 |
| BUG-02 | FR-10 - Trạng thái Đơn hàng | FR-10: canceled là trạng thái kết thúc | High | TC-08 |

## 5. Kết Luận

- Bộ testcase hiện có bao phủ 3 feature / requirement và 3 kỹ thuật thiết kế khác nhau.
- Tổng cộng 25 testcase, trong đó 9 testcase Pass, 4 testcase Failed và 12 testcase Not executed.
- Đã xác nhận 4 bug, tập trung vào FR-03 và FR-10.
- Các bug report có số hiệu cục bộ theo từng folder, nên cần đọc kèm testcase liên quan để tránh nhầm BUG-01 / BUG-02 giữa FR-03 và FR-10.
- FR-09 hiện chưa ghi nhận bug trong bộ tài liệu tổng hợp này.
