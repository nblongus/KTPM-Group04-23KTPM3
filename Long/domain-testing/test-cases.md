# Test Cases - FR-03: Forgot password and password reset

- **Feature ID:** FR-03
- **Feature Name:** Forgot password and password reset
- **Technique:** Domain Testing / EP; BVA 3-point
- **Test case cuối cùng — Domain Testing / EP:** FR03-EP-OTP-002, FR03-EP-OTP-003, FR03-EP-OTP-004, FR03-EP-OTP-005, FR03-EP-OTP-006, FR03-EP-PWD-001, FR03-EP-PWD-002, FR03-EP-PWD-003, FR03-EP-PWD-004, FR03-EP-PWD-005, FR03-EP-PWD-006, FR03-EP-PWD-007, FR03-EP-ACT-002
- **Test case cuối cùng — BVA 3-point:** FR03-BVA-TC-001, FR03-BVA-TC-002, FR03-BVA-TC-003, FR03-BVA-TC-004, FR03-BVA-TC-006
- **Test case bị loại — Domain Testing / EP:** Cần sinh viên bổ sung.
- **Test case bị loại — BVA 3-point:** FR03-BVA-TC-005
- **Execution status hiện tại:** Executed — 13 Pass, 5 Fail
- **Ghi chú:** Đã thực thi toàn bộ 18 test case FR-03. Nguồn `test-cases.xlsx` không cung cấp danh sách Test Case ID bị loại ở B5.

## Test Case Table

| Test Case ID | Feature ID | Feature Name | Technique | Domain/Boundary ID | Test Objective | Preconditions | Input Data | Steps | Expected Result | Actual Result | Status | Evidence | Bug ID | GitHub Issue Link | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FR03-EP-OTP-002 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-OTP-02 | Kiểm tra OTP 4 số nhưng sai | Form đang mở và hiển thị OTP. Reset context hợp lệ: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | OTP: `<OTP 4 số khác OTP đang hiển thị>`<br>Mật khẩu mới: `ValidPass1!` | 1. Ghi nhận OTP đang hiển thị.<br>2. Nhập một OTP 4 số khác OTP đó.<br>3. Nhập `ValidPass1!`.<br>4. Bấm `Đặt lại mật khẩu`. | OTP không được chấp nhận như OTP đúng. Nội dung thông báo và trạng thái dữ liệu: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. Nếu hệ thống chỉ báo mật khẩu yếu, ghi nhận `Bug candidate cần xác minh khi thực thi`. | Hệ thống không validate được OTP sai. Khi nhập OTP 4 số khác OTP đang hiển thị, hệ thống vẫn không phát hiện đúng lỗi OTP. | Fail | Cần sinh viên bổ sung. |  |  | Bug candidate — OTP sai không được validate đúng. |
| FR03-EP-OTP-003 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-OTP-03 | Kiểm tra OTP ngắn hơn 4 số | Form đang mở và hiển thị OTP. | OTP: `705`<br>Mật khẩu mới: `ValidPass1!` | 1. Thử nhập `705` vào field OTP.<br>2. Ghi nhận field có cho phép nhập hay không.<br>3. Nhập `ValidPass1!`.<br>4. Bấm `Đặt lại mật khẩu` nếu UI cho phép. | Giá trị không đáp ứng label `Mã OTP (4 số)`. Cách UI xử lý, thông báo lỗi và trạng thái dữ liệu: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hệ thống không phát hiện OTP ngắn hơn 4 số. | Fail | Cần sinh viên bổ sung. |  |  | Bug candidate — OTP ngắn hơn 4 số vẫn không bị validate đúng. |
| FR03-EP-OTP-004 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-OTP-03 | Kiểm tra OTP dài hơn 4 số | Form đang mở và hiển thị OTP. | OTP: `70531`<br>Mật khẩu mới: `ValidPass1!` | 1. Thử nhập `70531` vào field OTP.<br>2. Ghi nhận field có giới hạn độ dài hay không.<br>3. Nhập `ValidPass1!`.<br>4. Bấm `Đặt lại mật khẩu` nếu UI cho phép. | Giá trị không đáp ứng label `Mã OTP (4 số)`. Cách UI xử lý, thông báo lỗi và trạng thái dữ liệu: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hệ thống không giới hạn độ dài OTP. OTP dài hơn 4 số vẫn có thể được nhập/xử lý không đúng. | Fail | Cần sinh viên bổ sung. |  |  | Bug candidate — OTP không giới hạn độ dài đúng theo label `Mã OTP (4 số)`. |
| FR03-EP-OTP-005 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-OTP-03 | Kiểm tra OTP chứa ký tự không phải số | Form đang mở và hiển thị OTP. | OTP: `70A3`<br>Mật khẩu mới: `ValidPass1!` | 1. Thử nhập `70A3` vào field OTP.<br>2. Ghi nhận field có chặn chữ cái hay không.<br>3. Nhập `ValidPass1!`.<br>4. Bấm `Đặt lại mật khẩu` nếu UI cho phép. | Giá trị không đáp ứng label `Mã OTP (4 số)`. Cách UI xử lý, thông báo lỗi và trạng thái dữ liệu: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hệ thống không phát hiện OTP có ký tự không phải số. | Fail | Cần sinh viên bổ sung. |  |  | Bug candidate — OTP chứa ký tự chữ vẫn không bị validate đúng. |
| FR03-EP-OTP-006 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-OTP-04 | Kiểm tra OTP rỗng | Form đang mở và hiển thị OTP. | OTP: `""`<br>Mật khẩu mới: `ValidPass1!` | 1. Để trống field OTP.<br>2. Nhập `ValidPass1!`.<br>3. Bấm `Đặt lại mật khẩu`. | Hành vi validation, error message và trạng thái dữ liệu khi OTP rỗng: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Chỉ OTP rỗng; mật khẩu là `ValidPass1!`. |
| FR03-EP-PWD-001 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-01 | Kiểm tra mật khẩu hợp lệ tiềm năng | Form đang mở và hiển thị OTP. Reset context hợp lệ: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `ValidPass1!` | 1. Ghi nhận và nhập đúng OTP đang hiển thị.<br>2. Nhập `ValidPass1!`.<br>3. Bấm `Đặt lại mật khẩu`. | Mật khẩu không bị từ chối bởi quy tắc mật khẩu yếu đã công bố. Output thành công và thay đổi dữ liệu: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. Nếu vẫn xuất hiện alert mật khẩu yếu, ghi nhận `Bug candidate cần xác minh khi thực thi`. | Mật khẩu hợp lệ `ValidPass1!` vẫn bị hệ thống từ chối. | Fail | Cần sinh viên bổ sung. | GH-4 | [Issue #4](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/4) | Bug candidate — mật khẩu đáp ứng rule đã hiển thị nhưng vẫn bị từ chối. |
| FR03-EP-PWD-002 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-02 | Kiểm tra mật khẩu dưới 8 ký tự | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `Abc1!xy` | 1. Nhập đúng OTP đang hiển thị.<br>2. Nhập `Abc1!xy`.<br>3. Bấm `Đặt lại mật khẩu`. | Submission bị từ chối và dự kiến hiển thị alert mật khẩu yếu đã quan sát. Việc từng điều kiện riêng sử dụng đúng alert này: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Mật khẩu chỉ vi phạm độ dài; OTP dùng giá trị đúng động. |
| FR03-EP-PWD-003 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-03 | Kiểm tra mật khẩu thiếu chữ hoa | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `validpass1!` | 1. Nhập đúng OTP đang hiển thị.<br>2. Nhập `validpass1!`.<br>3. Bấm `Đặt lại mật khẩu`. | Submission bị từ chối và dự kiến hiển thị alert mật khẩu yếu đã quan sát. Hành vi riêng của miền thiếu chữ hoa: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Mật khẩu chỉ thiếu chữ hoa; OTP dùng giá trị đúng động. |
| FR03-EP-PWD-004 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-04 | Kiểm tra mật khẩu thiếu chữ thường | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `VALIDPASS1!` | 1. Nhập đúng OTP đang hiển thị.<br>2. Nhập `VALIDPASS1!`.<br>3. Bấm `Đặt lại mật khẩu`. | Submission bị từ chối và dự kiến hiển thị alert mật khẩu yếu đã quan sát. Hành vi riêng của miền thiếu chữ thường: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Mật khẩu chỉ thiếu chữ thường; OTP dùng giá trị đúng động. |
| FR03-EP-PWD-005 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-05 | Kiểm tra mật khẩu thiếu số | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `ValidPass!` | 1. Nhập đúng OTP đang hiển thị.<br>2. Nhập `ValidPass!`.<br>3. Bấm `Đặt lại mật khẩu`. | Submission bị từ chối và dự kiến hiển thị alert mật khẩu yếu đã quan sát. Hành vi riêng của miền thiếu số: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Mật khẩu chỉ thiếu số; OTP dùng giá trị đúng động. |
| FR03-EP-PWD-006 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-06 | Kiểm tra mật khẩu thiếu ký tự đặc biệt | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `ValidPass1` | 1. Nhập đúng OTP đang hiển thị.<br>2. Nhập `ValidPass1`.<br>3. Bấm `Đặt lại mật khẩu`. | Submission bị từ chối và dự kiến hiển thị alert mật khẩu yếu đã quan sát. Hành vi riêng của miền thiếu ký tự đặc biệt: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Mật khẩu chỉ thiếu ký tự đặc biệt; OTP dùng giá trị đúng động. |
| FR03-EP-PWD-007 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-PWD-07 | Kiểm tra mật khẩu rỗng | Form đang mở và hiển thị OTP. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `""` | 1. Nhập đúng OTP đang hiển thị.<br>2. Để trống field mật khẩu mới.<br>3. Bấm `Đặt lại mật khẩu`. | Hành vi validation, error message và trạng thái dữ liệu khi mật khẩu rỗng: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt có điều kiện. Chỉ mật khẩu rỗng; OTP dùng giá trị đúng động. |
| FR03-EP-ACT-002 | FR-03 | Forgot password and password reset | Domain Testing / EP | FR03-D-ACT-02 | Kiểm tra action Quay lại | Form Quên Mật Khẩu đang mở. | OTP: Không thay đổi<br>Mật khẩu mới: Không thay đổi<br>Action: Bấm `← Quay lại` một lần | 1. Quan sát form hiện tại.<br>2. Bấm `← Quay lại`.<br>3. Ghi nhận trang đích và trạng thái form. | Hệ thống thực hiện hành vi quay lại. Trang đích và ảnh hưởng tới reset context: Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Đạt. Không đưa OTP hoặc mật khẩu vào miền không hợp lệ; action quay lại là mục tiêu duy nhất. |
| FR03-BVA-TC-001 | FR-03 | Forgot password and password reset | BVA 3-point | FR03-BVA-OTP-LEN-MIN / FR03-BVA-OTP-LEN-MAX | OTP dài 3 ký tự (`B − 1`) | Form Quên Mật Khẩu đang mở và OTP động đang hiển thị. | OTP: `<3 chữ số tạo bằng cách bỏ 1 chữ số khỏi OTP đang hiển thị>`<br>Mật khẩu mới: `Aa1!bcde` | 1. Nhập OTP dài đúng 3 chữ số.<br>2. Nhập mật khẩu mới `Aa1!bcde`.<br>3. Nhấn `Đặt lại mật khẩu`. | SUT từ chối yêu cầu do OTP không dài đúng 4 số và không đặt lại mật khẩu. Validation order và error message cụ thể cần xác minh khi thực thi. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Chỉ kiểm tra boundary độ dài OTP; mật khẩu đáp ứng các rule đã biết. |
| FR03-BVA-TC-002 | FR-03 | Forgot password and password reset | BVA 3-point | FR03-BVA-OTP-LEN-MIN / FR03-BVA-OTP-LEN-MAX; FR03-BVA-PWD-LEN-MIN | OTP dài 4 ký tự (`B`); đồng thời bao phủ mật khẩu dài 8 ký tự | Form Quên Mật Khẩu đang mở và OTP động đang hiển thị. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `Aa1!bcde` | 1. Nhập chính xác OTP đang hiển thị trên UI.<br>2. Nhập mật khẩu mới `Aa1!bcde`.<br>3. Nhấn `Đặt lại mật khẩu`. | OTP vượt qua validation độ dài 4 số. Yêu cầu đặt lại mật khẩu được chấp nhận nếu không có validation khác; kết quả và thông báo cụ thể cần xác minh khi thực thi. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Dùng OTP động chính xác để không gây nhiễu bởi rule OTP đúng/sai; đồng thời ghi nhận coverage cho `FR03-BV-PWD-LEN-002`. |
| FR03-BVA-TC-003 | FR-03 | Forgot password and password reset | BVA 3-point | FR03-BVA-OTP-LEN-MIN / FR03-BVA-OTP-LEN-MAX | OTP dài 5 ký tự (`B + 1`) | Form Quên Mật Khẩu đang mở và OTP động đang hiển thị. | OTP: `<5 chữ số tạo bằng cách thêm 1 chữ số vào OTP đang hiển thị>`<br>Mật khẩu mới: `Aa1!bcde` | 1. Nhập OTP dài đúng 5 chữ số.<br>2. Nhập mật khẩu mới `Aa1!bcde`.<br>3. Nhấn `Đặt lại mật khẩu`. | SUT từ chối yêu cầu do OTP không dài đúng 4 số và không đặt lại mật khẩu. Validation order và error message cụ thể cần xác minh khi thực thi. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Chỉ kiểm tra boundary độ dài OTP; mật khẩu đáp ứng các rule đã biết. |
| FR03-BVA-TC-004 | FR-03 | Forgot password and password reset | BVA 3-point | FR03-BVA-PWD-LEN-MIN | Mật khẩu dài 7 ký tự (`B − 1`) | Form Quên Mật Khẩu đang mở và OTP động đang hiển thị. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `Aa1!bcd` | 1. Nhập chính xác OTP đang hiển thị trên UI.<br>2. Nhập mật khẩu mới `Aa1!bcd`.<br>3. Nhấn `Đặt lại mật khẩu`. | SUT từ chối mật khẩu vì ngắn hơn 8 ký tự và không đặt lại mật khẩu. Thông báo dự kiến phản ánh yêu cầu tối thiểu 8 ký tự; cần xác minh khi thực thi. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Mật khẩu vẫn có chữ hoa, chữ thường, số và ký tự đặc biệt để cô lập lỗi độ dài. |
| FR03-BVA-TC-006 | FR-03 | Forgot password and password reset | BVA 3-point | FR03-BVA-PWD-LEN-MIN | Mật khẩu dài 9 ký tự (`B + 1`) | Form Quên Mật Khẩu đang mở và OTP động đang hiển thị. | OTP: `<OTP đang hiển thị trên UI>`<br>Mật khẩu mới: `Aa1!bcdef` | 1. Nhập chính xác OTP đang hiển thị trên UI.<br>2. Nhập mật khẩu mới `Aa1!bcdef`.<br>3. Nhấn `Đặt lại mật khẩu`. | Mật khẩu vượt qua validation độ dài tối thiểu và các nhóm ký tự đã biết. Yêu cầu đặt lại mật khẩu được chấp nhận nếu không có validation khác; kết quả cụ thể cần xác minh khi thực thi. | Hành vi thực tế khớp Expected Result. | Pass |  |  |  | Không tạo test case cho `FR03-BVA-PWD-LEN-MAX` vì boundary này chưa có bằng chứng. |


---

# FR-09 — Decision Table và Test Cases cho Mã Giảm Giá

## 1. Phạm vi và nguồn

- Requirement oracle: `eshop-sut/README.md`, mục **FR-09: Mã Giảm Giá**.
- Điểm vào API: `POST /api/apply-coupon`, mô tả tại `eshop-sut/api_specification.md`, mục 5.1.
- Dữ liệu mẫu: `eshop-sut/backend/database.js`, các mã `SAVE10`, `BIGBUY`, `VIP100`, `EXPIRED`.
- Mã nguồn `eshop-sut/backend/server.js` chỉ được dùng để xác định cách gọi SUT và nhận diện điểm cần test; không dùng hành vi implementation làm expected result.
- Trạng thái thực thi: **Not executed**.

Ký hiệu: `T` = điều kiện đúng, `F` = điều kiện sai, `-` = không ảnh hưởng (don't care), `X` = action xảy ra.

## 2. B1 — Lọc requirement phù hợp

Thang điểm mỗi tiêu chí: 0 = thấp/không có, 1 = trung bình, 2 = rõ/cao.

| Requirement | Điều kiện kết hợp | Kết quả rõ | Kiểm soát dữ liệu | Rủi ro | Tổng / 8 | Kết luận |
|---|---:|---:|---:|---:|---:|---|
| FR-01 — Đăng ký | 2 | 2 | 2 | 1 | 7 | Phù hợp; số điều kiện mật khẩu lớn, thiên về validation |
| FR-03 — Reset password | 2 | 2 | 1 | 2 | 7 | Phù hợp; cần kiểm soát OTP và email |
| **FR-09 — Mã giảm giá** | **2** | **2** | **2** | **2** | **8** | **Chọn** |
| FR-10 — State machine | 2 | 2 | 2 | 2 | 8 | Phù hợp nhưng State Transition trực quan hơn |
| FR-12 — Access control | 1 | 2 | 2 | 2 | 7 | Phù hợp nhưng chỉ có hai điều kiện chính |
| FR-16 — Import CSV | 2 | 2 | 1 | 2 | 7 | Phù hợp; cần fixture file và transaction |

Lý do chọn FR-09: requirement nêu tường minh năm điều kiện cùng phải thỏa, có kết quả tài chính quan sát được, có hai công thức tính và có các biên `>=` cùng `<` dễ phát sinh lỗi.

### 2.1 Điều kiện/nguyên nhân

| ID | Điều kiện/nguyên nhân | T | F | Nguồn |
|---|---|---|---|---|
| C1 | Mã tồn tại và đang active | Có trong CSDL, `is_active = 1` | Không tồn tại hoặc inactive | FR-09/C1 |
| C2 | Mã còn hạn | Thời điểm hiện tại trước `expired_at` | Đã đến/sau hạn | FR-09/C2 |
| C3 | Đủ ngưỡng đơn hàng | `total >= min_order_amount` | `total < min_order_amount` | FR-09/C3 |
| C4 | Người dùng đã đăng nhập | Có JWT hợp lệ | Không có/JWT không hợp lệ | FR-09/C4 |
| C5 | Chưa dùng hết lượt | `usage_count < max_uses_per_user` | `usage_count >= max_uses_per_user` | FR-09/C5 |

### 2.2 Kết quả

| ID | Action/Result | Nguồn |
|---|---|---|
| A1 | Chấp nhận mã và tính giảm giá | FR-09: cả năm điều kiện phải thỏa |
| A2 | Từ chối áp dụng mã; không tạo kết quả giảm giá | Suy ra trực tiếp từ điều kiện “tất cả phải thỏa” |
| A3 | Nếu `type = percent`: `discount_amount = total × discount_value / 100` | Công thức FR-09 |
| A4 | Nếu `type = fixed`: `discount_amount = discount_value` | Công thức FR-09 |
| A5 | `final_amount = total - discount_amount` | Công thức FR-09 |

Requirement không quy định HTTP status hay nội dung chính xác/độ ưu tiên của message khi nhiều điều kiện cùng sai. Test chỉ kỳ vọng 4xx và thông báo phù hợp, không tự đặt câu chữ.

## 3. B2 — Bảng chân trị đầy đủ

Năm điều kiện Boolean tạo `2^5 = 32` luật. `A1` chỉ xảy ra khi cả năm điều kiện đều đúng.

| Full Rule | C1 | C2 | C3 | C4 | C5 | A1: Áp dụng | A2: Từ chối |
|---|---|---|---|---|---|---|---|
| F01 | F | F | F | F | F |  | X |
| F02 | F | F | F | F | T |  | X |
| F03 | F | F | F | T | F |  | X |
| F04 | F | F | F | T | T |  | X |
| F05 | F | F | T | F | F |  | X |
| F06 | F | F | T | F | T |  | X |
| F07 | F | F | T | T | F |  | X |
| F08 | F | F | T | T | T |  | X |
| F09 | F | T | F | F | F |  | X |
| F10 | F | T | F | F | T |  | X |
| F11 | F | T | F | T | F |  | X |
| F12 | F | T | F | T | T |  | X |
| F13 | F | T | T | F | F |  | X |
| F14 | F | T | T | F | T |  | X |
| F15 | F | T | T | T | F |  | X |
| F16 | F | T | T | T | T |  | X |
| F17 | T | F | F | F | F |  | X |
| F18 | T | F | F | F | T |  | X |
| F19 | T | F | F | T | F |  | X |
| F20 | T | F | F | T | T |  | X |
| F21 | T | F | T | F | F |  | X |
| F22 | T | F | T | F | T |  | X |
| F23 | T | F | T | T | F |  | X |
| F24 | T | F | T | T | T |  | X |
| F25 | T | T | F | F | F |  | X |
| F26 | T | T | F | F | T |  | X |
| F27 | T | T | F | T | F |  | X |
| F28 | T | T | F | T | T |  | X |
| F29 | T | T | T | F | F |  | X |
| F30 | T | T | T | F | T |  | X |
| F31 | T | T | T | T | F |  | X |
| F32 | T | T | T | T | T | X |  |

### 3.1 Bảng quyết định phụ cho cách tính

Bảng này chỉ được xét sau khi eligibility rule A1 thành công.

| Calculation Rule | Loại mã | A3: Công thức percent | A4: Công thức fixed | A5: Tính final |
|---|---|---|---|---|
| CR1 | percent | X |  | X |
| CR2 | fixed |  | X | X |

## 4. B3 — Rút gọn Decision Table

31 luật từ chối được biểu diễn bởi năm luật “ít nhất một điều kiện sai”; luật thành công giữ nguyên. Các luật R1–R5 có thể chồng lấp nhưng đều dẫn tới cùng A2 nên không xung đột.

| Condition/Action | R1 | R2 | R3 | R4 | R5 | R6 |
|---|---:|---:|---:|---:|---:|---:|
| C1 — Mã tồn tại và active | F | - | - | - | - | T |
| C2 — Còn hạn | - | F | - | - | - | T |
| C3 — Đủ ngưỡng | - | - | F | - | - | T |
| C4 — Đã đăng nhập | - | - | - | F | - | T |
| C5 — Chưa hết lượt | - | - | - | - | F | T |
| A1 — Áp dụng mã |  |  |  |  |  | X |
| A2 — Từ chối | X | X | X | X | X |  |

- Trước rút gọn: 32 luật.
- Sau rút gọn: 6 luật.
- Chứng minh bao phủ: mọi F01–F31 chứa ít nhất một `F`, nên khớp ít nhất một R1–R5; F32 khớp duy nhất R6.
- Chứng minh không đổi hành vi: R1–R5 không thể khớp F32; R6 không thể khớp bất kỳ luật từ chối nào.
- Không gán message riêng theo R1–R5 khi nhiều condition cùng sai vì FR-09 không định nghĩa priority.

## 5. Chọn luật rủi ro cao và pairwise

| Rule | Tác động (1–3) | Khả năng (1–3) | Risk | Lý do |
|---|---:|---:|---:|---|
| R1–R3, R5 | 2 | 2 | 4 | Từ chối sai mã hoặc sai ngưỡng/quota |
| R4 | 3 | 2 | 6 | Nguy cơ bypass xác thực |
| **R6** | **3** | **3** | **9** | Chấp nhận mã làm thay đổi số tiền; có type, boundary, expiry và quota tương tác |

Chọn R6. Tất cả giá trị pairwise bên dưới vẫn giữ C1–C5 = `T`.

### 5.1 Factor và mức giá trị

| Factor | Mức 0 | Mức 1 |
|---|---|---|
| P1 — Coupon type | percent, giảm 10% | fixed, giảm 50.000 ₫ |
| P2 — Total so với min | đúng bằng min | cao hơn min |
| P3 — Expiry | gần: T+1 ngày | xa: T+365 ngày |
| P4 — Usage | 0/2 lượt | 1/2 lượt, còn đúng một lượt |

### 5.2 Covering array

| Pair Row | P1 | P2 | P3 | P4 | Test Case |
|---|---:|---:|---:|---:|---|
| P01 | 0 | 0 | 0 | 0 | FR09-PW-001 |
| P02 | 0 | 0 | 1 | 1 | FR09-PW-002 |
| P03 | 1 | 1 | 0 | 0 | FR09-PW-003 |
| P04 | 1 | 1 | 1 | 1 | FR09-PW-004 |
| P05 | 0 | 1 | 0 | 1 | FR09-PW-005 |
| P06 | 1 | 0 | 1 | 0 | FR09-PW-006 |

### 5.3 Kiểm tra pair coverage

| Cặp factor | Các cặp giá trị được bao phủ |
|---|---|
| P1–P2 | 00, 01, 10, 11 |
| P1–P3 | 00, 01, 10, 11 |
| P1–P4 | 00, 01, 10, 11 |
| P2–P3 | 00, 01, 10, 11 |
| P2–P4 | 00, 01, 10, 11 |
| P3–P4 | 00, 01, 10, 11 |

## 6. Dữ liệu chuẩn bị chung

1. Khởi chạy backend mà không reset hoặc ghi đè dữ liệu người dùng ngoài phạm vi test.
2. Tạo user test có JWT hợp lệ; lấy `user_id` từ token/session, không coi body `user_id` là bằng chứng đăng nhập.
3. Trước mỗi case, đặt chính xác số bản ghi `coupon_usage` được nêu; dọn fixture sau test.
4. Với pairwise, tạo sáu mã riêng `PW01`–`PW06`, đều `is_active = 1`, `max_uses_per_user = 2`:

| Code | Type/value | Min | Expiry | Usage trước test |
|---|---|---:|---|---:|
| PW01 | percent / 10 | 300.000 | T+1 ngày | 0 |
| PW02 | percent / 10 | 300.000 | T+365 ngày | 1 |
| PW03 | fixed / 50.000 | 500.000 | T+1 ngày | 0 |
| PW04 | fixed / 50.000 | 500.000 | T+365 ngày | 1 |
| PW05 | percent / 10 | 300.000 | T+1 ngày | 1 |
| PW06 | fixed / 50.000 | 500.000 | T+365 ngày | 0 |

## 7. Bộ test case cuối cùng

Mọi request dùng `Content-Type: application/json`. Với case đã đăng nhập, gửi `Authorization: Bearer <valid JWT>` và `user_id` đúng user test trong body theo API specification.

| Test Case ID | Rule | Technique | Mục tiêu và precondition | Input/Steps chính | Expected result | Actual | Status |
|---|---|---|---|---|---|---|---|
| FR09-DT-001 | R1 | Decision Table | Mã không tồn tại; user đăng nhập, total hợp lệ | `POST /api/apply-coupon` với `{code: "NOT_FOUND", total_amount: 600000, user_id}` | 4xx; từ chối mã; không trả kết quả giảm giá/final amount đã giảm | Not executed | Not executed |
| FR09-DT-002 | R2 | Decision Table | `EXPIRED` active nhưng hết hạn; user chưa dùng | Gửi `EXPIRED`, `total_amount: 100000`, JWT hợp lệ | 4xx; thông báo phù hợp về hết hạn; không áp dụng giảm giá | Not executed | Not executed |
| FR09-DT-003 | R3 | Decision Table + BVA | `SAVE10` còn hạn, user chưa dùng; total dưới min đúng 1 ₫ | Gửi `SAVE10`, `total_amount: 299999`, JWT hợp lệ | 4xx; từ chối vì chưa đạt 300.000 ₫; không áp dụng giảm giá | Not executed | Not executed |
| FR09-DT-004 | R4 | Decision Table | Các điều kiện khác hợp lệ nhưng không có JWT | Gửi `SAVE10`, `total_amount: 300000`, không có Authorization | 401/403 hoặc 4xx xác thực phù hợp; không áp dụng giảm giá | Not executed | Not executed |
| FR09-DT-005 | R5 | Decision Table | User đã dùng `SAVE10` 1/1 lần | Gửi `SAVE10`, `total_amount: 300000`, JWT hợp lệ | 4xx; từ chối do đạt giới hạn; không áp dụng giảm giá | Not executed | Not executed |
| FR09-PW-001 | R6/CR1 | Decision Table + Pairwise | Fixture PW01, C1–C5 đều T | Gửi `PW01`, `total_amount: 300000`, JWT hợp lệ | Thành công; discount = 30.000; final = 270.000 | Not executed | Not executed |
| FR09-PW-002 | R6/CR1 | Decision Table + Pairwise | Fixture PW02, C1–C5 đều T | Gửi `PW02`, `total_amount: 300000`, JWT hợp lệ | Thành công dù usage = 1 < 2; discount = 30.000; final = 270.000 | Not executed | Not executed |
| FR09-PW-003 | R6/CR2 | Decision Table + Pairwise | Fixture PW03, C1–C5 đều T | Gửi `PW03`, `total_amount: 600000`, JWT hợp lệ | Thành công; discount = 50.000; final = 550.000 | Not executed | Not executed |
| FR09-PW-004 | R6/CR2 | Decision Table + Pairwise | Fixture PW04, C1–C5 đều T | Gửi `PW04`, `total_amount: 600000`, JWT hợp lệ | Thành công dù usage = 1 < 2; discount = 50.000; final = 550.000 | Not executed | Not executed |
| FR09-PW-005 | R6/CR1 | Decision Table + Pairwise | Fixture PW05, C1–C5 đều T | Gửi `PW05`, `total_amount: 600000`, JWT hợp lệ | Thành công; discount = 60.000; final = 540.000 | Not executed | Not executed |
| FR09-PW-006 | R6/CR2 | Decision Table + Pairwise + BVA | Fixture PW06, C1–C5 đều T | Gửi `PW06`, `total_amount: 500000`, JWT hợp lệ | Thành công tại biên `total = min`; discount = 50.000; final = 450.000 | Not executed | Not executed |

### Các bước quan sát áp dụng cho mỗi test

1. Gửi request với fixture tương ứng.
2. Ghi HTTP status và response JSON.
3. Kiểm tra có/không có `discount_amount`, `final_amount` theo expected result.
4. Với response thành công, tự tính lại theo FR-09 và so sánh chính xác.
5. Xác nhận thao tác **apply** đơn thuần không tự tăng `coupon_usage`; lượt chỉ được ghi khi luồng checkout thành công sử dụng mã.

## 8. Traceability

| Requirement/Condition | Reduced Rule | Test Case |
|---|---|---|
| FR-09/C1 | R1 | FR09-DT-001 |
| FR-09/C2 | R2 | FR09-DT-002 |
| FR-09/C3 | R3 | FR09-DT-003 |
| FR-09/C4 | R4 | FR09-DT-004 |
| FR-09/C5 | R5 | FR09-DT-005 |
| FR-09/C1–C5 all true | R6 | FR09-PW-001…006 |
| Formula percent | CR1 | FR09-PW-001, 002, 005 |
| Formula fixed | CR2 | FR09-PW-003, 004, 006 |
| Boundary `total >= min` | R3/R6 | FR09-DT-003, FR09-PW-001, 002, 006 |
| Boundary `usage < max` | R5/R6 | FR09-DT-005, FR09-PW-002, 004, 005 |

## 9. Điểm cần lưu ý khi thực thi

Đối chiếu tĩnh cho thấy các vị trí có khả năng làm test fail, nhưng **chưa được ghi là bug trước khi chạy test**:

- Route apply coupon hiện không dùng middleware xác thực và nhận `user_id` từ body, có nguy cơ vi phạm C4.
- So sánh ngưỡng trong implementation dùng `total_amount > min_order_amount`, trong khi FR-09 yêu cầu `>=`.
- Công thức percent trong implementation dùng biểu thức khác `total × discount_value / 100`.
- C1 gộp hai nguyên nhân “không tồn tại” và “inactive”. Bộ hiện tại dùng đại diện “không tồn tại”; nếu cần coverage theo miền dữ liệu, bổ sung một case inactive nhưng vẫn ánh xạ R1.


---

# Test Cases - FR-10: Order state machine

- **Feature ID:** FR-10
- **Feature Name:** Order state machine
- **Technique:** Domain Testing / EP
- **Test case cuối cùng:** `FR10-EP-001`, `FR10-EP-005`, `FR10-EP-006`, `FR10-EP-009`, `FR10-EP-010`, `FR10-EP-011`
- **Test case bị loại:** Không có trong tập Domain Testing / EP.
- **Execution status hiện tại:** 4 Pass, 2 Fail
- **Ghi chú:** Các case API đã được chạy trên SUT localhost, đối chiếu HTTP response và trạng thái dữ liệu trước/sau; dữ liệu được khôi phục sau khi chạy.

### BVA applicability note for FR-10

FR-10 — Order state machine is mainly a state-transition feature. Based on the available evidence, the observed values are discrete order states such as `Chờ xác nhận`, `Đang giao`, and `Đã hủy`. The available evidence does not define a numeric or ordered boundary, Valid Min, Valid Max, or adjacent boundary values required for Boundary Value Analysis.

Therefore, BVA test cases were not generated for FR-10. This feature is covered by Domain Testing / EP and is more suitable for state-transition testing. BVA is applied to other selected features that contain clearer boundary conditions.

## Test Case Table

| Test Case ID | Feature ID | Feature Name | Technique | Domain/Boundary ID | Test Objective | Preconditions | Input Data | Steps | Expected Result | Actual Result | Status | Evidence | Bug ID | GitHub Issue Link | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FR10-EP-001 | FR-10 | Order state machine | Domain Testing / EP | D-I03-01 | Hủy đơn ở trạng thái `pending` (`Chờ xác nhận`) | Có một đơn thuộc quyền `Test User` đang ở trạng thái `pending`; phiên đăng nhập và quyền sở hữu hợp lệ. | Trạng thái ban đầu = `pending`; action = `Hủy đơn`. | 1. Mở lịch sử đơn hàng.<br>2. Xác nhận đơn ở trạng thái `Chờ xác nhận` và có nút `Hủy đơn`.<br>3. Chọn `Hủy đơn`.<br>4. Quan sát thông báo và trạng thái sau khi dữ liệu được tải lại. | Yêu cầu hủy được chấp nhận; UI hiển thị thông báo hủy thành công; trạng thái đơn chuyển thành `canceled` (`Đã hủy`) và không còn nút `Hủy đơn`. | Actual result quan sát từ SUT: API trả HTTP 200 với `Order canceled successfully`; trạng thái dữ liệu chuyển từ `pending` sang `canceled`. | Pass | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau |  |  | Dữ liệu đã được khôi phục sau test. |
| FR10-EP-005 | FR-10 | Order state machine | Domain Testing / EP | D-I03-02 | Chặn hủy đơn ở trạng thái `shipping` (`Đang giao`) | Có một đơn thuộc quyền `Test User` đang ở trạng thái `shipping`; phiên đăng nhập và quyền sở hữu hợp lệ. | Trạng thái ban đầu = `shipping`; action = `Hủy đơn`. | 1. Mở lịch sử đơn hàng.<br>2. Xác nhận đơn ở trạng thái `Đang giao`.<br>3. Kiểm tra cột thao tác.<br>4. Nếu UI cung cấp nút `Hủy đơn`, chọn nút và quan sát phản hồi cùng trạng thái sau refresh. | UI không hiển thị nút `Hủy đơn`. Nếu request hủy được gửi trực tiếp, API phải từ chối và trạng thái phải giữ nguyên `shipping`. | Actual result quan sát từ SUT: API trả HTTP 200 với `Order canceled successfully`; trạng thái dữ liệu đổi từ `shipping` sang `canceled`. | Fail | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau | GH-1 | [Issue #1](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/1) | Issue candidate: API chấp nhận hủy đơn ở trạng thái `shipping`. Dữ liệu đã được khôi phục sau test. |
| FR10-EP-006 | FR-10 | Order state machine | Domain Testing / EP | D-I03-03 | Chặn thao tác hủy lại đơn ở trạng thái cuối `canceled` (`Đã hủy`) | Có một đơn thuộc quyền `Test User` đang ở trạng thái `canceled`. | Trạng thái ban đầu = `canceled`; action = `Hủy đơn`. | 1. Mở lịch sử đơn hàng.<br>2. Xác nhận đơn ở trạng thái `Đã hủy`.<br>3. Kiểm tra cột thao tác hoặc gửi request hủy trực tiếp. | UI không hiển thị nút `Hủy đơn`; request hủy bị từ chối và trạng thái giữ nguyên `canceled`. | Actual result quan sát từ SUT: request hủy trả HTTP 400 với `Cannot cancel this order.`; trạng thái dữ liệu vẫn là `canceled`. | Pass | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau |  |  | Dữ liệu đã được khôi phục sau test. |
| FR10-EP-009 | FR-10 | Order state machine | Domain Testing / EP | D-I03-CONFIRMED | Hủy đơn ở trạng thái `confirmed` (`Đã xác nhận`) | Có một đơn thuộc quyền `Test User` đang ở trạng thái `confirmed`; phiên đăng nhập và quyền sở hữu hợp lệ. | Trạng thái ban đầu = `confirmed`; action = `Hủy đơn`. | 1. Mở lịch sử đơn hàng.<br>2. Xác nhận đơn ở trạng thái `Đã xác nhận`.<br>3. Chọn `Hủy đơn` hoặc gửi request tương ứng.<br>4. Quan sát response và trạng thái sau refresh. | Yêu cầu hủy được chấp nhận; trạng thái chuyển thành `canceled`. | Actual result quan sát từ SUT: API trả HTTP 200 với `Order canceled successfully`; trạng thái dữ liệu chuyển từ `confirmed` sang `canceled`. | Pass | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau |  |  | Dữ liệu đã được khôi phục sau test. |
| FR10-EP-010 | FR-10 | Order state machine | Domain Testing / EP | D-ADMIN-FINAL-STATE | Chặn transition từ trạng thái cuối `canceled` sang `delivered` | Có token admin hợp lệ và một đơn đang ở trạng thái `canceled`. | Trạng thái hiện tại = `canceled`; trạng thái yêu cầu = `delivered`. | 1. Gửi `PUT /api/admin/orders/:id/status` với body `{ "status": "delivered" }`.<br>2. Ghi nhận HTTP response.<br>3. Đọc lại trạng thái đơn. | API từ chối transition, trả lỗi 4xx và trạng thái đơn vẫn là `canceled`. | Actual result quan sát từ SUT: API trả HTTP 200 với `Order status updated`; trạng thái dữ liệu đổi từ `canceled` sang `delivered`. | Fail | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau | GH-2 | [Issue #2](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/2) | Issue candidate: trạng thái `canceled` vẫn chuyển được sang `delivered`. Dữ liệu đã được khôi phục sau test. |
| FR10-EP-011 | FR-10 | Order state machine | Domain Testing / EP | D-I03-DELIVERED | Chặn hủy đơn ở trạng thái cuối `delivered` (`Đã giao`) | Có một đơn thuộc quyền `Test User` đang ở trạng thái `delivered`. | Trạng thái ban đầu = `delivered`; action = `Hủy đơn`. | 1. Xác nhận đơn ở trạng thái `Đã giao`.<br>2. Gửi request hủy trực tiếp.<br>3. Ghi nhận response và trạng thái sau request. | Request hủy bị từ chối và trạng thái giữ nguyên `delivered`. | Actual result quan sát từ SUT: request hủy trả HTTP 400 với `Cannot cancel this order.`; trạng thái dữ liệu vẫn là `delivered`. | Pass | API execution log ngày 2026-06-29; HTTP response và trạng thái trước/sau |  |  | Dữ liệu đã được khôi phục sau test. |


---

# Test Cases - FR-16: Product import from CSV

- **Feature ID:** FR-16
- **Feature Name:** Product import from CSV
- **Technique:** Domain Testing / EP; Boundary Value Analysis (3-point)
- **Test case cuối cùng:** FR16-EP-001, FR16-EP-002, FR16-EP-003, FR16-EP-004, FR16-EP-005, FR16-EP-006, FR16-EP-007, FR16-EP-008, FR16-EP-009, FR16-EP-010, FR16-EP-011, FR16-EP-012, FR16-EP-013, FR16-EP-014, FR16-EP-015, FR16-EP-016, FR16-EP-017, FR16-EP-018, FR16-EP-019, FR16-EP-020, FR16-EP-021, FR16-EP-022, FR16-EP-023, FR16-EP-024, FR16-EP-025, FR16-EP-026, FR16-EP-027, FR16-BVA-TC-001, FR16-BVA-TC-002, FR16-BVA-TC-003, FR16-BVA-TC-004, FR16-BVA-TC-005, FR16-BVA-TC-006, FR16-BVA-TC-007, FR16-BVA-TC-008, FR16-BVA-TC-009
- **Test case bị loại:** Không có
- **Execution status hiện tại:** 18 Pass / 18 Executed — oracle pending / 0 Fail
- **Ghi chú:** Đã thực thi ngày 2026-06-29 qua UI và API localhost. Kết quả chỉ phản ánh hành vi quan sát được từ SUT; những case chưa có requirement hoặc oracle blackbox được đánh dấu `Executed — oracle pending`. Dữ liệu product tạo bởi test đã được xóa sau từng case.

## Test Case Table

| Test Case ID | Feature ID | Feature Name | Technique | Domain/Boundary ID | Test Objective | Preconditions | Input Data | Steps | Expected Result | Actual Result | Status | Evidence | Bug ID | GitHub Issue Link | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FR16-EP-001 | FR-16 | Product import from CSV | Domain Testing / EP | D01 | Kiểm tra file baseline được import thành công | Admin có JWT hợp lệ; category 1 tồn tại; name chưa tồn tại | `valid.csv`: header chuẩn và một row hợp lệ | Chọn file.<br>Kiểm tra preview.<br>Nhấn **Import 1 sản phẩm**. | Preview có 1 row; API HTTP 200; UI hiện `Import hoàn tất: 1/1 sản phẩm được thêm`; database tăng 1 product và danh sách được refresh. | Preview hiển thị 1 dòng; nút Import 1 sản phẩm enabled; HTTP 200; UI báo import 1/1; DB thêm đúng product name, price, description, imageUrl và category 1. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  | Baseline của các test UI. |
| FR16-EP-002 | FR-16 | Product import from CSV | Domain Testing / EP | D02 | Kiểm tra không chọn file | Mở tab Sản phẩm; chưa chọn file | Mở file picker rồi Cancel | Bấm chọn file.<br>Cancel file picker. | Không có preview hoặc request import; nút Import vẫn disabled; dữ liệu không đổi. | Actual result quan sát từ SUT: preview không xuất hiện; nút Import disabled; không có product mới trong DB. | Pass | UI/API execution ngày 2026-06-29 |  |  |  |
| FR16-EP-003 | FR-16 | Product import from CSV | Domain Testing / EP | D03 | Kiểm tra file có extension khác CSV | Baseline hợp lệ; admin có JWT hợp lệ | `products.txt` chứa nội dung comma-separated hợp lệ | Chọn file.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: file `products.txt` được tiếp nhận; HTTP 200; UI báo 1/1; DB thêm 1 product. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. |
| FR16-EP-004 | FR-16 | Product import from CSV | Domain Testing / EP | D04 | Kiểm tra file rỗng | Baseline hợp lệ | `empty.csv`, 0 byte | Chọn file rỗng.<br>Quan sát UI và request. | Preview length 0; nút Import disabled; không POST; database không đổi. | File 0 byte tạo preview 0 dòng; nút Import disabled; không gửi import; DB không đổi. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-005 | FR-16 | Product import from CSV | Domain Testing / EP | D05 | Kiểm tra file chỉ có header | Baseline hợp lệ | File chỉ có header chuẩn | Chọn file.<br>Quan sát preview và nút Import. | Không có product row trong preview; nút disabled; không POST; database không đổi. | File chỉ có header tạo preview 0 dòng; nút Import disabled; không gửi import; DB không đổi. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-006 | FR-16 | Product import from CSV | Domain Testing / EP | D06 | Kiểm tra delimiter dấu chấm phẩy | Admin có JWT hợp lệ | Header và row dùng `;`; dữ liệu logic khác hợp lệ | Chọn file.<br>Quan sát preview.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; UI báo 0/1 và `Hàng 2: Thiếu tên sản phẩm`; DB không đổi. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. |
| FR16-EP-007 | FR-16 | Product import from CSV | Domain Testing / EP | D07 | Kiểm tra dấu phẩy trong quoted description | Baseline hợp lệ | Description là `"Mềm, nhẹ"`; field khác hợp lệ | Chọn file.<br>Kiểm tra preview.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200 và insert 1; DB lưu description là ký tự quote + Mềm, imageUrl là nhẹ + ký tự quote; dữ liệu sau dấu phẩy bị chuyển sang cột kế tiếp. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Cần đối chiếu requirement về định dạng CSV. |
| FR16-EP-008 | FR-16 | Product import from CSV | Domain Testing / EP | D08 | Kiểm tra malformed CSV có quote không đóng | Baseline hợp lệ | Row `Áo,100,"Mô tả chưa đóng,,1` | Chọn file.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; UI báo 1/1; DB insert row và giữ quote trong description. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. |
| FR16-EP-009 | FR-16 | Product import from CSV | Domain Testing / EP | D09 | Kiểm tra các header alias được hỗ trợ | Baseline hợp lệ | Header `ten,gia,mo_ta,image,danh_muc`, một row hợp lệ | Chọn file.<br>Nhấn Import. | Alias map sang đủ năm field; insert 1; HTTP 200; errors rỗng. | Header alias được map đúng; HTTP 200; insert 1 với price 123, description Mô tả alias, image alias-image và category 2. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-010 | FR-16 | Product import from CSV | Domain Testing / EP | D10 | Kiểm tra sai header name | Baseline hợp lệ | Đổi `name` thành `product_name`; field khác hợp lệ | Chọn file.<br>Nhấn Import. | Mapped name rỗng; HTTP 200; `inserted=0`; errors có `Hàng 2: Thiếu tên sản phẩm`; database không đổi. | product_name không được nhận diện; HTTP 200; UI báo 0/1 và Hàng 2: Thiếu tên sản phẩm; DB không đổi. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-011 | FR-16 | Product import from CSV | Domain Testing / EP | D11 | Kiểm tra thiếu toàn bộ optional header | Admin có JWT hợp lệ; name mới | `name` và một row `Áo thun` | Chọn file.<br>Nhấn Import. | Insert 1 với price `0`, description/image rỗng, category 1; HTTP 200. | HTTP 200; insert 1 với price 0, description rỗng, imageUrl rỗng và category 1. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-012 | FR-16 | Product import from CSV | Domain Testing / EP | D12 | Kiểm tra header thừa và đổi thứ tự | Baseline hợp lệ | Header `extra,category_id,name,imageUrl,description,price`; row tương ứng | Chọn file.<br>Nhấn Import. | Field chuẩn map đúng theo key; cột `extra` không được gửi API; insert 1. | Cột thừa bị bỏ; thứ tự mới vẫn map đúng; HTTP 200; DB lưu name FR16 EP012, price 321 và category 2. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-013 | FR-16 | Product import from CSV | Domain Testing / EP | D13 | Kiểm tra header trùng | Baseline hợp lệ | `name,name,price` và row `Tên 1,Tên 2,100` | Chọn file.<br>Quan sát preview.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; DB insert product với giá trị name từ cột thứ hai. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. |
| FR16-EP-014 | FR-16 | Product import from CSV | Domain Testing / EP | D15 | Kiểm tra product name rỗng | Baseline hợp lệ | Name rỗng; mọi field khác hợp lệ | Chọn file.<br>Nhấn Import. | HTTP 200; `inserted=0`; errors có `Hàng 2: Thiếu tên sản phẩm`; row không được insert. | HTTP 200; inserted 0; UI hiển thị Hàng 2: Thiếu tên sản phẩm; DB không thêm row. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-015 | FR-16 | Product import from CSV | Domain Testing / EP | D16 | Kiểm tra price âm | Baseline hợp lệ | `price=-1000`; field khác hợp lệ | Chọn file.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; UI báo 1/1; DB lưu price -1000. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Rule nghiệp vụ cần xác minh. |
| FR16-EP-016 | FR-16 | Product import from CSV | Domain Testing / EP | D17 | Kiểm tra price không phải số | Baseline hợp lệ | `price=abc`; field khác hợp lệ | Chọn file.<br>Nhấn Import.<br>Truy vấn record vừa tạo. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; UI báo 1/1; DB lưu price dưới dạng text `abc`. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. |
| FR16-EP-017 | FR-16 | Product import from CSV | Domain Testing / EP | D18 | Kiểm tra category không tồn tại | Category 999999 không tồn tại; field khác baseline | `category_id=999999` | Chọn file.<br>Nhấn Import. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: HTTP 200; UI báo 1/1; DB lưu category_id 999999 dù category không tồn tại. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Rule category cần xác minh. |
| FR16-EP-018 | FR-16 | Product import from CSV | Domain Testing / EP | D19 | Kiểm tra image URL sai định dạng | Baseline hợp lệ | `imageUrl=not-a-url`; field khác hợp lệ | Chọn file.<br>Nhấn Import. | Không có URL validation; insert 1 với chuỗi `not-a-url`, HTTP 200. | HTTP 200; UI báo 1/1; DB lưu imageUrl not-a-url. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-019 | FR-16 | Product import from CSV | Domain Testing / EP | D20 | Kiểm tra duplicate product name | Không có `Áo trùng` trước test | Hai row cùng name `Áo trùng`; field khác hợp lệ | Chọn file.<br>Nhấn Import.<br>Đếm record theo name. | HTTP 200; `inserted=2`; database có hai record mới cùng name; không update/skip. | HTTP 200; UI báo 2/2; DB tạo 2 record cùng name FR16 DUP, không update hoặc skip. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-020 | FR-16 | Product import from CSV | Domain Testing / EP | D21 | Kiểm tra Unicode tiếng Việt | Baseline hợp lệ; file UTF-8 | `Điện thoại Việt Nam,100000,Mô tả tiếng Việt,,1` | Chọn file.<br>Kiểm tra preview.<br>Import.<br>Kiểm tra DB/UI. | Chuỗi tiếng Việt hiển thị và lưu không biến dạng; insert 1. | HTTP 200; UI báo 1/1; DB giữ nguyên name và description tiếng Việt. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  | Cần xác minh từ SUT thực tế. |
| FR16-EP-021 | FR-16 | Product import from CSV | Domain Testing / EP | D22 | Kiểm tra khoảng trắng đầu/cuối cell | Baseline hợp lệ | Name `  Áo thun  `; field khác hợp lệ | Chọn file.<br>Nhấn Import. | Preview/object name là `Áo thun`; database lưu name đã trim; insert 1. | HTTP 200; UI báo 1/1; DB lưu name FR16 EP021 sau khi loại khoảng trắng đầu/cuối. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-022 | FR-16 | Product import from CSV | Domain Testing / EP | D23 | Kiểm tra nhiều row đều hợp lệ | Hai name mới; admin có JWT hợp lệ | Hai row hợp lệ | Chọn file.<br>Nhấn Import. | Preview 2; HTTP 200; message `Import hoàn tất: 2/2 sản phẩm được thêm`; database tăng 2. | HTTP 200; UI báo 2/2; DB tăng đúng 2 product hợp lệ. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  |  |
| FR16-EP-023 | FR-16 | Product import from CSV | Domain Testing / EP | D24 | Kiểm tra batch có row hợp lệ và không hợp lệ | Baseline hợp lệ | Row đầu có name; row sau name rỗng; field khác hợp lệ | Chọn file.<br>Nhấn Import.<br>Kiểm tra UI và DB. | HTTP 200; `inserted=1`; message `Import hoàn tất: 1/2 sản phẩm được thêm`; errors có `Hàng 3: Thiếu tên sản phẩm`; chỉ row hợp lệ được insert, không rollback. | HTTP 200; UI báo 1/2 và Hàng 3: Thiếu tên sản phẩm; DB chỉ thêm row hợp lệ, không rollback. | Pass | Chrome headless + frontend-admin:5174 + API:3000, 2026-06-29 |  |  | Miền mục tiêu là batch composition; row lỗi chỉ sai name. |
| FR16-EP-024 | FR-16 | Product import from CSV | Domain Testing / EP | D26 | Kiểm tra request thiếu token | API client; body products hợp lệ; đã ghi count DB | POST không có Authorization | Gọi endpoint import. | HTTP 401 `{error:"Unauthorized"}`; không insert. | API trả HTTP 401 với error Unauthorized; inserted 0; DB không đổi. | Pass | Direct API localhost:3000, 2026-06-29 |  |  |  |
| FR16-EP-025 | FR-16 | Product import from CSV | Domain Testing / EP | D26 | Kiểm tra token không hợp lệ | API client; body products hợp lệ | `Authorization: Bearer invalid.jwt.token` | Gọi endpoint import. | HTTP 403 `{error:"Forbidden"}`; không insert. | API trả HTTP 403 với error Forbidden; inserted 0; DB không đổi. | Pass | Direct API localhost:3000, 2026-06-29 |  |  |  |
| FR16-EP-026 | FR-16 | Product import from CSV | Domain Testing / EP | D27 | Kiểm tra non-admin dùng valid token | Có JWT hợp lệ của user thường; body hợp lệ | Bearer user JWT | Gọi endpoint import trực tiếp. | Cần xác minh từ SUT thực tế hoặc tài liệu requirement. | Actual result quan sát từ SUT: JWT của user thường được API chấp nhận; HTTP 200; response inserted 1 và DB thêm product. | Executed — oracle pending | API execution ngày 2026-06-29; HTTP response và trạng thái trước/sau |  |  | Requirement phân quyền cần sinh viên xác minh. |
| FR16-EP-027 | FR-16 | Product import from CSV | Domain Testing / EP | D28 | Kiểm tra empty products array qua API | Admin JWT hợp lệ; API client | `{ "products": [] }` | POST endpoint import. | HTTP 400 `{error:"Không có dữ liệu để import"}`; database không đổi. | API trả HTTP 400 với error Không có dữ liệu để import; inserted 0; DB không đổi. | Pass | Direct API localhost:3000, 2026-06-29 |  |  |  |
| FR16-BVA-TC-001 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-02 / BV-FR16-ROW-001 | Kiểm tra B − 1 quanh candidate số product rows | Admin có JWT hợp lệ; tab Sản phẩm mở; DB ở trạng thái kiểm soát | `name,price,description,imageUrl,category_id` — 0 product rows | Chọn file chỉ có header.<br>Quan sát preview và nút Import.<br>Kiểm tra không có request import. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: preview rỗng; nút Import disabled; không POST; DB không đổi. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 0 rows. |
| FR16-BVA-TC-002 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-02 / BV-FR16-ROW-002 | Kiểm tra candidate số product rows | Admin có JWT hợp lệ; category 1 tồn tại; name mới | Header chuẩn và 1 row `Áo A,120000,Mô tả,,1` | Chọn file.<br>Xác nhận preview có 1 row.<br>Nhấn Import. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; UI báo 1/1; DB tăng 1 record. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 1 row. |
| FR16-BVA-TC-003 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-02 / BV-FR16-ROW-003 | Kiểm tra candidate số product rows | Admin có JWT hợp lệ; category 1 tồn tại; hai name mới | Header chuẩn và 2 row hợp lệ | Chọn file.<br>Xác nhận preview có 2 row.<br>Nhấn Import. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; UI báo 2/2; DB tăng 2 record. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 2 rows. |
| FR16-BVA-TC-004 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-04 / BV-FR16-NAME-001 | Kiểm tra candidate độ dài name | Admin có JWT hợp lệ; các field khác dùng baseline | Header chuẩn; row `,120000,Mô tả,,1` | Chọn file.<br>Nhấn Import.<br>Kiểm tra message và DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; inserted 0; UI báo `Hàng 2: Thiếu tên sản phẩm`; DB không đổi. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: name dài 0. |
| FR16-BVA-TC-005 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-04 / BV-FR16-NAME-002 | Kiểm tra candidate độ dài name | Admin có JWT hợp lệ; name `A` chưa tồn tại; field khác baseline | Header chuẩn; row `A,120000,Mô tả,,1` | Chọn file.<br>Nhấn Import.<br>Kiểm tra DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; insert 1/1; DB lưu name `A`. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: name dài 1. |
| FR16-BVA-TC-006 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-04 / BV-FR16-NAME-003 | Kiểm tra candidate độ dài name | Admin có JWT hợp lệ; name `AB` chưa tồn tại; field khác baseline | Header chuẩn; row `AB,120000,Mô tả,,1` | Chọn file.<br>Nhấn Import.<br>Kiểm tra DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; insert 1/1; DB lưu name `AB`. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: name dài 2. |
| FR16-BVA-TC-007 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-03 / BV-FR16-COL-001 | Kiểm tra candidate số header được nhận diện để tạo name | Admin có JWT hợp lệ; một data row; không có header alias name | `price` và row `120000` — 0 header name được nhận diện | Chọn file.<br>Nhấn Import.<br>Kiểm tra message và DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; inserted 0; UI báo thiếu tên; DB không đổi. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 0 recognized name header. |
| FR16-BVA-TC-008 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-03 / BV-FR16-COL-002 | Kiểm tra candidate số header được nhận diện để tạo name | Admin có JWT hợp lệ; name `A` mới | `name` và row `A` — 1 recognized header | Chọn file.<br>Nhấn Import.<br>Kiểm tra DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; DB lưu name A, price 0, description/image rỗng và category 1. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 1 recognized header. |
| FR16-BVA-TC-009 | FR-16 | Product import from CSV | BVA 3-point | BC-FR16-03 / BV-FR16-COL-003 | Kiểm tra candidate số header được nhận diện | Admin có JWT hợp lệ; name `A` mới | `name,price` và row `A,1` — 2 recognized headers | Chọn file.<br>Nhấn Import.<br>Kiểm tra DB. | Expected result cần được xác nhận bằng requirement hoặc oracle blackbox. | Actual result quan sát từ SUT: HTTP 200; DB lưu name A, price 1 và category 1. | Executed — oracle pending | UI/API execution ngày 2026-06-29 |  |  | Boundary candidate; test value: 2 recognized headers. |


---

# Test Cases - FR-20: Mobile Checkout

- **Feature ID:** FR-20
- **Feature Name:** Mobile: Checkout
- **Technique:** Domain Testing / EP and Boundary Value Analysis (3-point BVA)
- **Test case cuối cùng:** 18 EP test cases và 3 BVA test cases (`MCHECKOUT-BVA-QTY-003`, `MCHECKOUT-BVA-COUPON-001`, `MCHECKOUT-BVA-COUPON-003`)
- **Test case bị loại:** Không có
- **Execution status hiện tại:** 21 designed — 9 Pass, 12 Fail
- **Ghi chú:** Thực thi API ngày 2026-06-29; các case từng Blocked/Not executed được hoàn tất bằng source-assisted verification trên `frontend-mobile/App.js` và `backend/server.js`. Evidence ghi rõ trường hợp chưa có ảnh runtime.

## Test Case Table

| Test Case ID | Feature ID | Feature Name | Technique | Domain/Boundary ID | Test Objective | Preconditions | Input Data | Steps | Expected Result | Actual Result | Status | Evidence | Bug ID | GitHub Issue Link | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| MCHECKOUT-EP-001 | FR-20 | Mobile: Checkout | Domain Testing / EP | DC01 | Cart 1 sản phẩm hợp lệ — DC01 / RC01 | Baseline hợp lệ; chưa dùng voucher; ghi snapshot orders/cart. | id=1, quantity=1; total kỳ vọng server=30,000,000; JWT hợp lệ. | 1. Thêm product id=1 vào cart và mở checkout.<br>2. Kiểm tra danh sách/tổng read-only rồi chọn `Xác Nhận Thanh Toán`.<br>3. Quan sát UI, request/response, cart và orders dữ liệu hệ thống. | UI phải hiển thị đủ item và tổng; phía dịch vụ phải tự tính lại tổng từ dữ liệu tin cậy; tạo đúng 1 order `pending`; UI hiện thành công và clear cart. Message/điều hướng cần xác minh. | API trả HTTP 200, tạo order #5 total 30,000,000 `pending`. Source mobile render đủ cart và total read-only; sau response thành công đặt success view, clear cart và refresh orders. | Pass | API execution 2026-06-29; `frontend-mobile/App.js` lines 383–415, 662–690. |  |  | Source-assisted verification; chưa có screenshot mobile nhưng control flow khớp expected result của baseline. |
| MCHECKOUT-EP-002 | FR-20 | Mobile: Checkout | Domain Testing / EP | DC02 | Cart rỗng — DC02 / RC02 | Logged in; cart đã clear. | `cart=[]`. | 1. Mở màn hình Giỏ hàng.<br>2. Quan sát empty state và các action. | Hiện `Giỏ hàng của bạn đang trống`, không render nút tiến hành thanh toán; không tạo order. Hành vi API direct với empty items: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Request checkout với `items=[]`, `total_amount=0` vẫn trả HTTP 200 và tạo order #6 có total 0, status `pending`. Điều kiện không tạo order không được đáp ứng. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` HTTP 200; GET `/api/orders/6`. | GH-9 | [Issue #9](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/9) | Rep ID: RC02. Kiểm tra cô lập lỗi: Đạt; session/network hợp lệ. Execution: Issue candidate: empty cart can create an order. |
| MCHECKOUT-EP-005 | FR-20 | Mobile: Checkout | Domain Testing / EP | DQ02 | Quantity=0 — DQ02 / RQ02 | Product id=1 tồn tại; cart/network/session baseline. | nhập quantity `0`. | 1. Nhập `0` khi thêm/chỉnh product id=1.<br>2. Quan sát quantity và total trước checkout. | Cart không được giữ quantity=0; hệ thống phải chặn, loại item hoặc đưa về giá trị hợp lệ. Hành vi/message chính thức cần xác minh. | Request checkout chứa item quantity=0 vẫn trả HTTP 200 và tạo order #7. Chưa quan sát UI normalization, nhưng checkout không chặn dữ liệu quantity=0. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` với quantity=0, HTTP 200. | GH-9 | [Issue #9](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/9) | Rep ID: RQ02. Kiểm tra cô lập lỗi: Đạt; các baseline khác hợp lệ. Execution: Issue candidate: checkout accepts zero quantity. |
| MCHECKOUT-EP-010 | FR-20 | Mobile: Checkout | Domain Testing / EP | DS02 | User chưa đăng nhập — DS02 / RS02 | Logout; cart id=1 q=1. | `user=null`, không token. | 1. Từ cart chọn `Tiến hành thanh toán`.<br>2. Quan sát Alert và màn hình kế tiếp. | Hiện `Bạn cần đăng nhập để thanh toán!`, chuyển login, không gọi checkout/không tạo order, cart giữ nguyên. | Source `openCheckout` kiểm tra `!user`, hiển thị đúng Alert, chuyển `login` rồi return trước mọi request; không thay đổi cart. API direct không token cũng trả 401 và không tạo order. | Pass | API execution 2026-06-29; `frontend-mobile/App.js` lines 342–353. |  |  | Source-assisted verification of UI control flow. |
| MCHECKOUT-EP-011 | FR-20 | Mobile: Checkout | Domain Testing / EP | DS03 | Session hết hạn/invalid — DS03 / RS03 | Checkout screen đã mở; thay token bằng token expired/invalid. | id=1 q=1; JWT invalid. | 1. Chọn xác nhận thanh toán.<br>2. Quan sát response, Alert, cart và dữ liệu hệ thống. | API 403 `Forbidden`; UI hiện Alert `Lỗi khi thanh toán`; không tạo order và không clear cart. | API trả 403 và không tạo order. Source ném lỗi khi `!response.ok`, vào catch hiển thị Alert; `setCart([])` chỉ chạy trong success path nên cart được giữ. | Pass | API execution 2026-06-29; `frontend-mobile/App.js` lines 380–419. |  |  | Source-assisted verification of error UI and cart retention. |
| MCHECKOUT-EP-012 | FR-20 | Mobile: Checkout | Domain Testing / EP | DV04 | Voucher không tồn tại — DV04 / RV04 | Cart id=1 q=1; logged in. | mã=`NO_SUCH_CODE`. | 1. Mở checkout, nhập mã và chọn `Áp dụng`.<br>2. Quan sát message và total. | API 404; UI hiển thị `Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa`; không có coupon result, total không giảm, chưa tạo order. | API trả đúng 404/message. Source catch gán message vào `couponError`, giữ `couponResult=null`; UI render error và total tiếp tục dùng `cartTotal`; apply-coupon không tạo order. | Pass | API execution 2026-06-29; `frontend-mobile/App.js` lines 356–377, 720–740. |  |  | Source-assisted verification of coupon error rendering. |
| MCHECKOUT-EP-013 | FR-20 | Mobile: Checkout | Domain Testing / EP | DV03 | Voucher hết hạn — DV03 / RV03 | Cart id=1 q=1 (30,000,000); logged in. | mã=`EXPIRED`. | 1. Mở checkout, nhập mã và chọn `Áp dụng`.<br>2. Quan sát message/total. | API 400; UI hiển thị `Mã giảm giá đã hết hạn`; total không giảm; chưa tạo order/usage. | API trả đúng 400/message và không tạo order/usage. Source đưa lỗi vào `couponError`, không đặt `couponResult`; UI giữ nguyên `cartTotal`. | Pass | API execution 2026-06-29; `frontend-mobile/App.js` lines 356–377, 720–740. |  |  | Source-assisted verification of expired-coupon UI path. |
| MCHECKOUT-EP-014 | FR-20 | Mobile: Checkout | Domain Testing / EP | DT04 | Total client/server mismatch — DT04 / RT04 | Cart id=1 q=1; chặn request trước khi gửi. | items sum dữ liệu hệ thống=30,000,000; gửi `total_amount=1`. | 1. Xác nhận checkout và sửa duy nhất `total_amount` thành 1.<br>2. Quan sát response và order dữ liệu hệ thống. | Theo S1, dịch vụ checkout tự tính 30,000,000 và không chấp nhận 1; không order nào được lưu với total=1. Exact response khi mismatch: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Items có tổng 30,000,000 nhưng gửi `total_amount=1`; checkout vẫn trả HTTP 200 và order #8 lưu total=1, status `pending`. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` HTTP 200; GET `/api/orders/8`. | GH-10 | [Issue #10](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/10) | Rep ID: RT04. Kiểm tra cô lập lỗi: Đạt; chỉ sửa total trong request, item/session/network hợp lệ. Execution: Issue candidate: client-controlled total is trusted. |
| MCHECKOUT-EP-015 | FR-20 | Mobile: Checkout | Domain Testing / EP | DN02 | Network/API lỗi — DN02 / RN02 | Cart id=1 q=1; logged in; snapshot dữ liệu hệ thống; sau khi mở checkout làm API unreachable. | request hợp lệ nhưng connection fail. | 1. Chọn xác nhận thanh toán khi dịch vụ checkout không reachable.<br>2. Quan sát Alert/success view/cart và dữ liệu hệ thống. | Hiện Alert `Lỗi khi thanh toán`; không hiện success; cart giữ 1 item. Không có partial order; atomicity khi mất kết nối giữa chừng: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Endpoint unreachable làm fetch reject và không có request tới backend. Source đi vào catch hiển thị Alert; success state và cart clear chỉ nằm sau response thành công nên không chạy. Không có partial order trong biến thể connection-fail này. | Pass | Connection-failure execution 2026-06-29; `frontend-mobile/App.js` lines 380–419. |  |  | Pass cho biến thể endpoint unreachable; mất kết nối sau khi backend đã commit là scenario khác. |
| MCHECKOUT-EP-017 | FR-20 | Mobile: Checkout | Domain Testing / EP | DA05 | Shipping address Unicode — DA05 / RA05 | JWT hợp lệ; API/network/dữ liệu hệ thống baseline. | `shipping_address="12 Đường Nguyễn Huệ, TP.HCM"`, total hợp lệ. | 1. Gửi checkout API với duy nhất address là chuỗi Unicode đại diện.<br>2. Đọc order vừa tạo rồi cleanup. | Nếu address thuộc contract, order lưu nguyên vẹn Unicode. Tính bắt buộc/nguồn address trên mobile: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Checkout với địa chỉ `12 Đường Nguyễn Huệ, TP.HCM` trả HTTP 200; order #18 đọc lại đúng nguyên văn địa chỉ Unicode, total 30,000,000 và status `pending`. | Pass | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` UTF-8 HTTP 200; GET `/api/orders/18`; equality check=true. |  |  | Rep ID: RA05. Kiểm tra cô lập lỗi: Đạt ở mức API; mobile UI không có address nên cần proxy/API client. Execution: Dữ liệu test đã được cleanup sau khi xác nhận. |
| MCHECKOUT-EP-018 | FR-20 | Mobile: Checkout | Domain Testing / EP | DC06 | Cart nhiều sản phẩm hợp lệ — DC06 / RC06 | Logged in; product id=1,2 tồn tại; network/dữ liệu hệ thống baseline. | id=1 q=1 + id=2 q=1; tổng=58,000,000. | 1. Thêm hai product và mở checkout.<br>2. Xác nhận UI có đủ hai item và thực hiện checkout.<br>3. Kiểm tra request, response và dữ liệu order/items. | UI và request phải có đủ hai item; phía dịch vụ tự tính 58,000,000 từ cả hai và order phải biểu diễn đầy đủ đơn hàng. Chi tiết cách quan sát order items cần xác minh. | UI source render đủ hai item và tính tổng 58,000,000, nhưng request checkout dùng `cart.slice(0, -1)`, cố ý loại sản phẩm cuối trong khi vẫn gửi total của cả hai. Backend không lưu/kiểm tra items, nên order #10 vẫn có total 58,000,000 nhưng không bảo toàn đầy đủ cart. | Fail | API execution 2026-06-29; `frontend-mobile/App.js` lines 75–77, 383–394, 676–690; `backend/server.js` lines 297–307. | LOCAL-FR20-01 |  | New defect: multi-item checkout drops the last cart item from request. |
| MCHECKOUT-EP-019 | FR-20 | Mobile: Checkout | Domain Testing / EP | DV02 | Voucher hợp lệ — DV02 / RV02 | Xóa/kiểm soát usage SAVE10 của test user. | id=1 q=1; mã=`SAVE10`. | 1. Apply SAVE10.<br>2. Kiểm tra discount/final amount rồi xác nhận checkout.<br>3. Kiểm tra order, usage và cart. | Discount 10%=3,000,000; final=27,000,000; UI hiển thị đúng; success ghi một usage và clear cart. dịch vụ checkout vẫn phải tự xác minh/tính lại total theo S1; hiện tại cần xác minh tính toàn vẹn giữa apply-coupon và checkout. | Apply `SAVE10` cho total 30,000,000 trả HTTP 200 nhưng `discount_amount=-270,000,000` và `final_amount=300,000,000` dù message ghi giảm 10%. Checkout sau đó tạo order #11 total 300,000,000 và ghi usage. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/apply-coupon`, `/api/checkout`, `/api/coupon-usage`, đều HTTP 200. | GH-11 | [Issue #11](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/11) | Rep ID: RV02. Kiểm tra cô lập lỗi: Đạt; user chưa dùng SAVE10, cart/session/network hợp lệ. Execution: Issue candidate: percentage coupon calculation produces negative discount and inflated final total. |
| MCHECKOUT-EP-020 | FR-20 | Mobile: Checkout | Domain Testing / EP | DQ03 | Quantity âm — DQ03 / RQ03 | Product id=1; session/network baseline. | quantity=`-1`. | 1. Nhập -1 ở quantity.<br>2. Quan sát giá trị cart/tổng. | Cart/checkout không được giữ quantity âm; hệ thống phải chặn hoặc đưa về giá trị hợp lệ. Hành vi/message chính thức cần xác minh. | Request checkout chứa quantity=-1 vẫn trả HTTP 200 và tạo order #12. Checkout không chặn quantity âm. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` với quantity=-1, HTTP 200. | GH-9 | [Issue #9](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/9) | Rep ID: RQ03. Kiểm tra cô lập lỗi: Đạt; chỉ quantity mục tiêu invalid. Execution: Issue candidate: checkout accepts negative quantity. |
| MCHECKOUT-EP-021 | FR-20 | Mobile: Checkout | Domain Testing / EP | DQ05 | Quantity không nguyên — DQ05 / RQ05 | Product id=1; session/network baseline. | quantity=`1.5`. | 1. Nhập `1.5` khi thêm product.<br>2. Quan sát quantity/tổng trong cart. | Quantity không nguyên phải bị chặn hoặc xử lý theo rule đã xác nhận; không được tạo order sai. Hành vi chính thức cần xác minh. | Request checkout chứa quantity=1.5 vẫn trả HTTP 200 và tạo order #13. Checkout không chặn quantity không nguyên. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` với quantity=1.5, HTTP 200. | GH-9 | [Issue #9](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/9) | Rep ID: RQ05. Kiểm tra cô lập lỗi: Đạt; chỉ quantity mục tiêu invalid. Execution: Issue candidate: checkout accepts non-integer quantity. |
| MCHECKOUT-EP-022 | FR-20 | Mobile: Checkout | Domain Testing / EP | DC04 | Product trong cart không còn tồn tại — DC04 / RC04 | Add một test product; ghi snapshot; xóa product đó khỏi dữ liệu hệ thống trước confirm. | stale cart item q=1. | 1. Mở checkout với stale item.<br>2. Xác nhận thanh toán và kiểm tra order dữ liệu hệ thống. | dịch vụ checkout không được tin stale client item khi tự tính tổng; phải từ chối hoặc loại item theo rule chính thức và không tạo order sai. Cách xử lý/message: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Checkout với product id=999999 không tồn tại vẫn trả HTTP 200 và tạo order #14 total 1,000, status `pending`. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` HTTP 200; GET `/api/orders/14`. | GH-9 | [Issue #9](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/9) | Rep ID: RC04. Kiểm tra cô lập lỗi: Đạt nếu chỉ xóa product mục tiêu sau khi đã add; các baseline khác hợp lệ. Execution: Issue candidate: stale/nonexistent product can be checked out. |
| MCHECKOUT-EP-023 | FR-20 | Mobile: Checkout | Domain Testing / EP | DT02 | Total=0 — DT02 / RT02 | Cart id=1 q=1; JWT/network baseline; intercept request. | gửi `total_amount=0`. | 1. Xác nhận checkout và sửa total thành 0.<br>2. Quan sát response/order dữ liệu hệ thống. | dịch vụ checkout không chấp nhận total client; tự tính 30,000,000 hoặc từ chối request; không lưu order total 0. Exact response: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Cart chứa product hợp lệ nhưng gửi `total_amount=0`; checkout trả HTTP 200 và order #15 lưu total=0, status `pending`. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` HTTP 200; GET `/api/orders/15`. | GH-10 | [Issue #10](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/10) | Rep ID: RT02. Kiểm tra cô lập lỗi: Đạt; cart có product hợp lệ, chỉ sửa total request. Execution: Covered by client-controlled total issue; keep as distinct EP input. |
| MCHECKOUT-EP-024 | FR-20 | Mobile: Checkout | Domain Testing / EP | DT03 | Total âm — DT03 / RT03 | Cart id=1 q=1; JWT/network baseline; intercept request. | gửi `total_amount=-1`. | 1. Xác nhận checkout và sửa total thành -1.<br>2. Quan sát response/order dữ liệu hệ thống. | dịch vụ checkout không chấp nhận total client; tự tính lại hoặc từ chối; không lưu order total âm. Exact response: `Cần xác minh từ SUT thực tế hoặc tài liệu requirement.` | Cart chứa product hợp lệ nhưng gửi `total_amount=-1`; checkout trả HTTP 200 và order #16 lưu total=-1, status `pending`. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/checkout` HTTP 200; GET `/api/orders/16`. | GH-10 | [Issue #10](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/10) | Rep ID: RT03. Kiểm tra cô lập lỗi: Đạt; cart có product hợp lệ, chỉ sửa total request. Execution: Covered by client-controlled total issue; keep as distinct EP input. |
| MCHECKOUT-EP-025 | FR-20 | Mobile: Checkout | Domain Testing / EP | DV05 | Voucher tại đúng ngưỡng — DV05 / RV05 | SAVE10 active, còn hạn/còn lượt; tạo cart/server sum đúng 300,000 hoặc gọi apply API kiểm soát. | mã=`SAVE10`; total=300,000. | 1. Apply voucher tại đúng min order amount.<br>2. Quan sát response và final amount. | Theo requirement, `total >= min_order_amount` nên voucher phải được áp dụng tại đúng 300,000 ₫. | Apply `SAVE10` tại đúng min order amount 300,000 trả HTTP 400 `Đơn hàng chưa đủ giá trị tối thiểu 300,000 ₫ để áp dụng mã này`. | Fail | Kết quả kiểm thử 2026-06-29: POST `/api/apply-coupon`, HTTP 400. | GH-12 | [Issue #12](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/12) | Rep ID: RV05. Kiểm tra cô lập lỗi: Đạt; voucher/session/usage đều hợp lệ, chỉ total ở miền mục tiêu. Execution: Issue candidate: coupon is rejected at its exact minimum threshold. |
| MCHECKOUT-BVA-QTY-003 | FR-20 | Mobile: Checkout | BVA 3-point | BV-FR20-QTY-MIN / B+1 | Kiểm tra quantity ngay trên Valid Min | Product id=1 tồn tại; session/network baseline; không dùng coupon. | quantity=`2` | 1. Thêm product id=1 với quantity 2.<br>2. Mở checkout và xác nhận quantity/total.<br>3. Checkout rồi kiểm tra order và cart. | Quantity 2 được chấp nhận; tổng bằng hai lần đơn giá tin cậy; tạo đúng một order và clear cart. | Source giữ quantity 2 khi thêm cart, tính total bằng `price * quantity`, gửi đúng cart/total cho cart một item; backend tạo một order và success path clear cart. | Pass | Source-assisted: `frontend-mobile/App.js` lines 129–152, 75–77, 383–415; `backend/server.js` lines 297–307. |  |  | Static/source-assisted result; screenshot runtime vẫn nên bổ sung. |
| MCHECKOUT-BVA-COUPON-001 | FR-20 | Mobile: Checkout | BVA 3-point | BV-FR20-COUPON-MIN / B-1 | Kiểm tra coupon ngay dưới min order amount | SAVE10 active, còn hạn/còn lượt; session hợp lệ. | total=`299999` | Gọi apply-coupon với SAVE10 và total 299999; ghi response và final amount. | Coupon bị từ chối vì tổng nhỏ hơn 300000; không tạo coupon usage và tổng không thay đổi. | Backend chỉ vào nhánh áp dụng khi `total_amount > min_order_amount`; 299999 không qua điều kiện nên trả lỗi dưới ngưỡng. Frontend giữ `couponResult=null`, không tạo usage và tiếp tục hiển thị cart total. | Pass | Source-assisted: `backend/server.js` lines 363–436; `frontend-mobile/App.js` lines 356–377, 720–740. |  |  | Static/source-assisted boundary result. |
| MCHECKOUT-BVA-COUPON-003 | FR-20 | Mobile: Checkout | BVA 3-point | BV-FR20-COUPON-MIN / B+1 | Kiểm tra coupon ngay trên min order amount | SAVE10 active, còn hạn/còn lượt; session hợp lệ. | total=`300001` | Gọi apply-coupon với SAVE10 và total 300001; ghi response, discount và final amount. | Coupon được chấp nhận; discount bằng 10% theo rule SAVE10; final amount bằng total trừ discount. | 300001 qua điều kiện ngưỡng, nhưng backend tính percent bằng `total_amount * (1 - discount_value)`; với SAVE10 tạo discount âm và final amount tăng thay vì giảm 10%. | Fail | Source-assisted: `backend/server.js` lines 379–431; cùng root cause với Issue #11. | GH-11 | [Issue #11](https://github.com/nblongus/HW02-QAQC-Domain-Testing-on-EShop/issues/11) | Boundary B+1 confirms the percentage-calculation defect. |

## Boundary Value Analysis

### B1 — Xác định boundary candidates

| Boundary ID | Biến | Valid Min/Max | Nguồn | Trạng thái |
|---|---|---:|---|---|
| BV-FR20-QTY-MIN | Quantity của một cart item | Valid Min = 1 | Rule quantity phải là số nguyên dương; execution đã có q=0, q=1 | Đủ căn cứ cho BVA 3-point |
| BV-FR20-CART-MIN | Số item trong cart | Valid Min = 1 | Empty cart không được checkout; cart một item là baseline hợp lệ | Đủ căn cứ cho BVA 3-point |
| BV-FR20-COUPON-MIN | Tổng tối thiểu để dùng SAVE10 | Valid Min = 300000₫ | Requirement/response của SUT ghi min order amount 300000₫ | Đủ căn cứ cho BVA 3-point |

Không tạo boundary cho address, network, session hoặc total client-supplied vì chúng không có Valid Min/Max phù hợp hoặc total phải được server tính lại thay vì được coi là miền số hợp lệ từ client.

### B2–B3 — Sinh boundary values

| Boundary ID | B-1 | B | B+1 |
|---|---:|---:|---:|
| BV-FR20-QTY-MIN | 0 | 1 | 2 |
| BV-FR20-CART-MIN | 0 item | 1 item | 2 items |
| BV-FR20-COUPON-MIN | 299999₫ | 300000₫ | 300001₫ |

### B4 — Traceability và tái sử dụng test case

| Boundary ID | Giá trị | Test Case ID | Status |
|---|---:|---|---|
| BV-FR20-QTY-MIN | 0 | MCHECKOUT-EP-005 | Fail |
| BV-FR20-QTY-MIN | 1 | MCHECKOUT-EP-001 | Pass |
| BV-FR20-QTY-MIN | 2 | MCHECKOUT-BVA-QTY-003 | Pass — source-assisted |
| BV-FR20-CART-MIN | 0 item | MCHECKOUT-EP-002 | Fail |
| BV-FR20-CART-MIN | 1 item | MCHECKOUT-EP-001 | Pass |
| BV-FR20-CART-MIN | 2 items | MCHECKOUT-EP-018 | Fail — request drops last item |
| BV-FR20-COUPON-MIN | 299999₫ | MCHECKOUT-BVA-COUPON-001 | Pass — source-assisted |
| BV-FR20-COUPON-MIN | 300000₫ | MCHECKOUT-EP-025 | Fail — GH-12 |
| BV-FR20-COUPON-MIN | 300001₫ | MCHECKOUT-BVA-COUPON-003 | Fail — GH-11 |

### B5 — Review và rút gọn

Sáu EP test case chạm đúng boundary được tái sử dụng thay vì tạo test case trùng. Chỉ thêm ba test case cho các giá trị chưa được bao phủ. Mỗi case thay đổi một boundary mục tiêu; session, product, coupon và network còn lại phải giữ ở baseline hợp lệ.
