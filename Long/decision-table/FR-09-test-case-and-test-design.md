# FR-09 — Decision Table và Test Cases cho Mã Giảm Giá

## 1. Phạm vi và nguồn

- Requirement oracle: `eshop-sut/README.md`, mục **FR-09: Mã Giảm Giá**.
- Điểm vào API: `POST /api/apply-coupon`, mô tả tại `eshop-sut/api_specification.md`, mục 5.1.
- Dữ liệu mẫu: `eshop-sut/backend/database.js`, các mã `SAVE10`, `BIGBUY`, `VIP100`, `EXPIRED`.
- Mã nguồn `eshop-sut/backend/server.js` chỉ được dùng để xác định cách gọi SUT và nhận diện điểm cần test; không dùng hành vi implementation làm expected result.
- Trạng thái thực thi: **Đã thực thi 11 test case — 4 Pass, 7 Fail**.

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
| FR09-DT-001 | R1 | Decision Table | Mã không tồn tại; user đăng nhập, total hợp lệ | `POST /api/apply-coupon` với `{code: "NOT_FOUND", total_amount: 600000, user_id}` | 4xx; từ chối mã; không trả kết quả giảm giá/final amount đã giảm | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | Pass |
| FR09-DT-002 | R2 | Decision Table | `EXPIRED` active nhưng hết hạn; user chưa dùng | Gửi `EXPIRED`, `total_amount: 100000`, JWT hợp lệ | 4xx; thông báo phù hợp về hết hạn; không áp dụng giảm giá | Mã giảm giá đã hết hạn | Pass |
| FR09-DT-003 | R3 | Decision Table + BVA | `SAVE10` còn hạn, user chưa dùng; total dưới min đúng 1 ₫ | Gửi `SAVE10`, `total_amount: 299999`, JWT hợp lệ | 4xx; từ chối vì chưa đạt 300.000 ₫; không áp dụng giảm giá | Hệ thống báo áp dụng thành công, giảm 10%. Với món hàng 28.000.000 ₫, hiển thị tiết kiệm **-252.000.000 ₫** và thành tiền **280.000.000 ₫** | **Fail** |
| FR09-DT-004 | R4 | Decision Table | Các điều kiện khác hợp lệ nhưng không có JWT | Gửi `SAVE10`, `total_amount: 300000`, không có Authorization | 401/403 hoặc 4xx xác thực phù hợp; không áp dụng giảm giá | Bạn cần đăng nhập để thanh toán! | Pass |
| FR09-DT-005 | R5 | Decision Table | User đã dùng `SAVE10` 1/1 lần | Gửi `SAVE10`, `total_amount: 300000`, JWT hợp lệ | 4xx; từ chối do đạt giới hạn; không áp dụng giảm giá | Bạn đã sử dụng mã này 1 lần (đã đạt giới hạn) | Pass |
| FR09-PW-001 | R6/CR1 | Decision Table + Pairwise | Fixture PW01, C1–C5 đều T | Gửi `PW01`, `total_amount: 300000`, JWT hợp lệ | Thành công; discount = 30.000; final = 270.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |
| FR09-PW-002 | R6/CR1 | Decision Table + Pairwise | Fixture PW02, C1–C5 đều T | Gửi `PW02`, `total_amount: 300000`, JWT hợp lệ | Thành công dù usage = 1 < 2; discount = 30.000; final = 270.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |
| FR09-PW-003 | R6/CR2 | Decision Table + Pairwise | Fixture PW03, C1–C5 đều T | Gửi `PW03`, `total_amount: 600000`, JWT hợp lệ | Thành công; discount = 50.000; final = 550.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |
| FR09-PW-004 | R6/CR2 | Decision Table + Pairwise | Fixture PW04, C1–C5 đều T | Gửi `PW04`, `total_amount: 600000`, JWT hợp lệ | Thành công dù usage = 1 < 2; discount = 50.000; final = 550.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |
| FR09-PW-005 | R6/CR1 | Decision Table + Pairwise | Fixture PW05, C1–C5 đều T | Gửi `PW05`, `total_amount: 600000`, JWT hợp lệ | Thành công; discount = 60.000; final = 540.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |
| FR09-PW-006 | R6/CR2 | Decision Table + Pairwise + BVA | Fixture PW06, C1–C5 đều T | Gửi `PW06`, `total_amount: 500000`, JWT hợp lệ | Thành công tại biên `total = min`; discount = 50.000; final = 450.000 | Mã giảm giá không tồn tại hoặc đã bị vô hiệu hóa | **Fail (fixture/test data)** |

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

Kết quả thực thi và đối chiếu tĩnh ghi nhận:

- Route apply coupon hiện không dùng middleware xác thực và nhận `user_id` từ body, có nguy cơ vi phạm C4.
- So sánh ngưỡng trong implementation dùng `total_amount > min_order_amount`, trong khi FR-09 yêu cầu `>=`.
- Công thức percent trong implementation dùng biểu thức khác `total × discount_value / 100`.
- C1 gộp hai nguyên nhân “không tồn tại” và “inactive”. Bộ hiện tại dùng đại diện “không tồn tại”; nếu cần coverage theo miền dữ liệu, bổ sung một case inactive nhưng vẫn ánh xạ R1.
- **Defect quan sát tại FR09-DT-003:** hệ thống chấp nhận mã khi expected result là từ chối và tính sai nghiêm trọng. Với giá hàng 28.000.000 ₫, giảm 10% đúng phải là 2.800.000 ₫ và thành tiền 25.200.000 ₫; actual lại hiển thị tiết kiệm -252.000.000 ₫ và thành tiền 280.000.000 ₫.
- **Vấn đề dữ liệu kiểm thử tại FR09-PW-001…006:** toàn bộ mã `PW01`–`PW06` đều bị SUT báo không tồn tại hoặc đã vô hiệu hóa. Cần tạo/activate đúng sáu fixture ở mục 6 rồi chạy lại; kết quả hiện tại chưa chứng minh lỗi của công thức percent/fixed hoặc pairwise rule R6.
